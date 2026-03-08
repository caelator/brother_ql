# brother\_ql — Enhanced 🖨️

*A comprehensive raster language package for Brother QL series label printers (including QL-820NWBc).*

> **Fork of [pklaus/brother\_ql](https://github.com/pklaus/brother_ql)** with half-cut support, enhanced model capabilities, and production-ready features.

[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Python 3.6+](https://img.shields.io/badge/python-3.6+-blue.svg)](https://www.python.org/)

---

## What's New in This Fork

### ✂️ Half-Cut Support

Half-cut is a feature available on QL-800 series printers that cuts through the label material but **not** the backing paper. This is essential for:

- **Multi-label jobs** — print seal + shipping labels on a continuous strip, half-cut between them for easy separation while keeping the strip intact for handling
- **Peel-and-stick workflows** — half-cut labels peel cleanly from the backing
- **Batch printing** — print multiple labels with half-cuts between, full-cut only at the end

#### How It Works

Half-cut is controlled by **bit 2** of the `ESC i K` (expanded mode) command in the Brother QL raster protocol:

```
ESC i K <flags>
  bit 0: two-color printing
  bit 2: half-cut  ← NEW
  bit 3: cut at end
  bit 6: 600 DPI
```

When the printer's half-cut setting is enabled (via LCD menu or P-touch Editor), the standard auto-cut commands trigger a half-cut instead of a full cut. The `ESC i K` bit tells the printer to use half-cut mode in the raster stream.

#### Supported Models

| Model | Half-Cut | Two-Color | 600 DPI | Compression |
|-------|----------|-----------|---------|-------------|
| QL-500 | ❌ | ❌ | ❌ | ❌ |
| QL-550 | ❌ | ❌ | ❌ | ❌ |
| QL-570 | ❌ | ❌ | ❌ | ❌ |
| QL-580N | ❌ | ❌ | ❌ | ✅ |
| QL-700 | ❌ | ❌ | ❌ | ❌ |
| QL-710W | ❌ | ❌ | ❌ | ✅ |
| QL-720NW | ❌ | ❌ | ❌ | ✅ |
| **QL-800** | **✅** | **✅** | ❌ | ❌ |
| **QL-810W** | **✅** | **✅** | ❌ | ✅ |
| **QL-820NWB / QL-820NWBc** | **✅** | **✅** | ❌ | ✅ |
| QL-1050 | ❌ | ❌ | ❌ | ✅ |
| QL-1060N | ❌ | ❌ | ❌ | ✅ |
| QL-1100 | ❌ | ❌ | ❌ | ✅ |
| QL-1110NWB | ❌ | ❌ | ❌ | ✅ |

### 📝 Changes Summary

#### `models.py`
- Added `half_cut` attribute to the `Model` class
- Enabled `half_cut=True` for QL-800, QL-810W, and QL-820NWB/NWBc models

#### `raster.py`
- Added `half_cut` property to `BrotherQLRaster`
- Added `half_cut_support` property to check model capability
- Modified `add_expanded_mode()` to set bit 2 of `ESC i K` when half-cut is enabled

#### `conversion.py`
- Added `half_cut` keyword argument to the `convert()` function
- Wires `half_cut` to `qlr.half_cut` before calling `add_expanded_mode()`

#### `brother_ql_create.py`
- Added `--half-cut` CLI flag

---

## Installation

```bash
pip install -e .
```

Or install directly from this fork:

```bash
pip install git+https://github.com/caelator/brother_ql.git
```

## Usage

### CLI — Print with Half-Cut

```bash
brother_ql_create \
  --model QL-820NWB \
  --label-size 62 \
  --half-cut \
  my_label.png \
  > output.bin

brother_ql_print tcp://192.168.1.50 output.bin
```

### Python API

```python
from brother_ql.raster import BrotherQLRaster
from brother_ql.conversion import convert

qlr = BrotherQLRaster('QL-820NWB')
qlr.exception_on_warning = True

convert(qlr, ['label.png'], '62',
        cut=True,
        half_cut=True,    # ← Enable half-cut
        hq=True,
        threshold=70)

# Send to printer
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('192.168.1.50', 9100))
s.sendall(qlr.data)
s.close()
```

### Multi-Label Job with Half-Cut

For printing multiple labels where you want half-cut between them and a full cut at the end:

```python
from brother_ql.raster import BrotherQLRaster
from brother_ql.conversion import convert

qlr = BrotherQLRaster('QL-820NWB')

# First label — half-cut after
convert(qlr, ['seal_label.png'], '62',
        cut=True, half_cut=True, hq=True)

# Second label — full cut after (last in job)
convert(qlr, ['shipping_label.png'], '62',
        cut=True, half_cut=False, hq=True)

# Send combined job
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('192.168.1.50', 9100))
s.sendall(qlr.data)
s.close()
```

## How Half-Cut Works

Half-cut is **controlled entirely via the raster protocol** — there is no separate firmware menu setting for it on most printers (e.g., the QL-820NWBc only exposes autocut, cut-at-end, and none in its LCD settings).

When bit 2 of the `ESC i K` expanded mode command is set in the raster stream, the printer performs a half-cut (cuts the label material but leaves the backing paper intact). A form-feed byte (`0x0C`) between pages triggers the half-cut, while the final print byte (`0x1A`) triggers a full cut.

> **Tip:** Set the printer's cut mode to **auto-cut** for best results with half-cut jobs. The auto-cut setting works in conjunction with the raster protocol's half-cut flag.

## Optimal Print Quality Settings

For the sharpest, most professional output on thermal labels:

| Setting | Recommended Value | Why |
|---------|------------------|-----|
| `threshold` | `70` | Optimal density for black text on white thermal paper |
| `hq` | `True` | Enables high-quality mode in the printer firmware |
| `dither` | `False` | Binary threshold produces sharper text than Floyd-Steinberg dithering |
| `dpi_600` | Model-dependent | Use if your model supports it (doubles horizontal resolution) |
| `compress` | `True` | Smaller data transfer, same output quality |

## Protocol Reference

This library implements the **Brother QL Raster Command Reference** protocol. Key commands:

| Command | Hex | Description |
|---------|-----|-------------|
| Initialize | `1B 40` | Reset printer state |
| Switch to raster | `1B 69 61 01` | Enter raster mode |
| Status request | `1B 69 53` | Query printer status (32-byte response) |
| Media/quality | `1B 69 7A` | Set media type, size, and quality |
| Auto-cut | `1B 69 4D 40` | Enable auto-cut |
| Cut every N | `1B 69 41 01` | Cut every 1 label |
| **Expanded mode** | **`1B 69 4B`** | **Flags: two-color, half-cut, cut-at-end, 600dpi** |
| Margins | `1B 69 64` | Set feed margin |
| Raster data | `67 00 5A` | 90-byte row of pixel data |
| Print | `1A` | End of file / final print |
| Form feed | `0C` | Page break (triggers half-cut if enabled) |

## Differences from Upstream

This fork is fully backwards-compatible with `pklaus/brother_ql`. The only additions are:

1. **`half_cut` attribute** on `Model` — defaults to `False`
2. **`half_cut` property** on `BrotherQLRaster` — defaults to `False`
3. **`half_cut` kwarg** on `convert()` — defaults to `False`
4. **`--half-cut` CLI flag** — opt-in, does nothing if not used

If you don't use half-cut, behavior is identical to upstream.

## License

This project is licensed under the **GNU General Public License v3.0** — see the [LICENSE](LICENSE) file for details.

This is a fork of [pklaus/brother\_ql](https://github.com/pklaus/brother_ql), which is also licensed under GPL-3.0.

## Credits

- **Original author:** [Philipp Klaus](https://github.com/pklaus) — created the brother\_ql library
- **This fork:** [Caelator](https://github.com/caelator) — added half-cut support and enhanced model capabilities

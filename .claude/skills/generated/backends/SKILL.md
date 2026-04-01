---
name: backends
description: "Skill for the Backends area of brother_ql. 22 symbols across 9 files."
---

# Backends

22 symbols | 9 files | Cohesion: 82%

## When to Use

- Working with code in `brother_ql/`
- Understanding how print_cmd, send_cmd, discover work
- Modifying backends-related functionality

## Key Files

| File | Symbols |
|------|---------|
| `brother_ql/backends/pyusb.py` | _raw_read, _read, list_available_devices, find_class, __init__ (+2) |
| `brother_ql/backends/generic.py` | _read, read, BrotherQLBackendGeneric, dispose, _dispose (+1) |
| `brother_ql/cli.py` | print_cmd, send_cmd |
| `brother_ql/backends/helpers.py` | discover, send |
| `brother_ql/raster.py` | BrotherQLRaster |
| `brother_ql/brother_ql_debug.py` | __init__ |
| `brother_ql/backends/__init__.py` | backend_factory |
| `brother_ql/backends/network.py` | BrotherQLBackendNetwork |
| `brother_ql/backends/linux_kernel.py` | BrotherQLBackendLinuxKernel |

## Entry Points

Start here when exploring this area:

- **`print_cmd`** (Function) — `brother_ql/cli.py:134`
- **`send_cmd`** (Function) — `brother_ql/cli.py:162`
- **`discover`** (Function) — `brother_ql/backends/helpers.py:16`
- **`send`** (Function) — `brother_ql/backends/helpers.py:25`
- **`read`** (Function) — `brother_ql/backends/generic.py:35`

## Key Symbols

| Symbol | Type | File | Line |
|--------|------|------|------|
| `BrotherQLRaster` | Class | `brother_ql/raster.py` | 29 |
| `find_class` | Class | `brother_ql/backends/pyusb.py` | 29 |
| `BrotherQLBackendPyUSB` | Class | `brother_ql/backends/pyusb.py` | 56 |
| `BrotherQLBackendNetwork` | Class | `brother_ql/backends/network.py` | 27 |
| `BrotherQLBackendLinuxKernel` | Class | `brother_ql/backends/linux_kernel.py` | 27 |
| `BrotherQLBackendGeneric` | Class | `brother_ql/backends/generic.py` | 14 |
| `print_cmd` | Function | `brother_ql/cli.py` | 134 |
| `send_cmd` | Function | `brother_ql/cli.py` | 162 |
| `discover` | Function | `brother_ql/backends/helpers.py` | 16 |
| `send` | Function | `brother_ql/backends/helpers.py` | 25 |
| `read` | Function | `brother_ql/backends/generic.py` | 35 |
| `backend_factory` | Function | `brother_ql/backends/__init__.py` | 22 |
| `list_available_devices` | Function | `brother_ql/backends/pyusb.py` | 20 |
| `identifier` | Function | `brother_ql/backends/pyusb.py` | 47 |
| `dispose` | Function | `brother_ql/backends/generic.py` | 44 |
| `__init__` | Function | `brother_ql/brother_ql_debug.py` | 12 |
| `_raw_read` | Function | `brother_ql/backends/pyusb.py` | 118 |
| `_read` | Function | `brother_ql/backends/pyusb.py` | 122 |
| `_read` | Function | `brother_ql/backends/generic.py` | 28 |
| `__init__` | Function | `brother_ql/backends/pyusb.py` | 30 |

## Execution Flows

| Flow | Type | Steps |
|------|------|-------|
| `Main → _read` | cross_community | 5 |
| `Print_cmd → Get_element_by_identifier` | cross_community | 4 |
| `Print_cmd → _write` | cross_community | 4 |
| `Analyze_cmd → _read` | cross_community | 4 |
| `Send_cmd → _write` | cross_community | 4 |
| `Main → _read` | cross_community | 3 |
| `Main → Backend_factory` | cross_community | 3 |
| `Print_cmd → LabelsManager` | cross_community | 3 |
| `Print_cmd → ModelsManager` | cross_community | 3 |
| `Print_cmd → Guess_backend` | cross_community | 3 |

## Connected Areas

| Area | Connections |
|------|-------------|
| Brother_ql | 6 calls |

## How to Explore

1. `gitnexus_context({name: "print_cmd"})` — see callers and callees
2. `gitnexus_query({query: "backends"})` — find related execution flows
3. Read key files listed above for implementation details

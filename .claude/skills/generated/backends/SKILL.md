---
name: backends
description: "Skill for the Backends area of brother_ql. 20 symbols across 8 files."
---

# Backends

20 symbols | 8 files | Cohesion: 83%

## When to Use

- Working with code in `brother_ql/`
- Understanding how send_cmd, discover, send work
- Modifying backends-related functionality

## Key Files

| File | Symbols |
|------|---------|
| `brother_ql/backends/pyusb.py` | _raw_read, _read, list_available_devices, find_class, __init__ (+2) |
| `brother_ql/backends/generic.py` | _read, read, BrotherQLBackendGeneric, dispose, _dispose (+1) |
| `brother_ql/backends/helpers.py` | discover, send |
| `brother_ql/cli.py` | send_cmd |
| `brother_ql/brother_ql_debug.py` | __init__ |
| `brother_ql/backends/__init__.py` | backend_factory |
| `brother_ql/backends/network.py` | BrotherQLBackendNetwork |
| `brother_ql/backends/linux_kernel.py` | BrotherQLBackendLinuxKernel |

## Entry Points

Start here when exploring this area:

- **`send_cmd`** (Function) — `brother_ql/cli.py:162`
- **`discover`** (Function) — `brother_ql/backends/helpers.py:16`
- **`send`** (Function) — `brother_ql/backends/helpers.py:25`
- **`read`** (Function) — `brother_ql/backends/generic.py:35`
- **`backend_factory`** (Function) — `brother_ql/backends/__init__.py:22`

## Key Symbols

| Symbol | Type | File | Line |
|--------|------|------|------|
| `find_class` | Class | `brother_ql/backends/pyusb.py` | 29 |
| `BrotherQLBackendPyUSB` | Class | `brother_ql/backends/pyusb.py` | 56 |
| `BrotherQLBackendNetwork` | Class | `brother_ql/backends/network.py` | 27 |
| `BrotherQLBackendLinuxKernel` | Class | `brother_ql/backends/linux_kernel.py` | 27 |
| `BrotherQLBackendGeneric` | Class | `brother_ql/backends/generic.py` | 14 |
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
| `_dispose` | Function | `brother_ql/backends/generic.py` | 50 |
| `__del__` | Function | `brother_ql/backends/generic.py` | 53 |

## Execution Flows

| Flow | Type | Steps |
|------|------|-------|
| `Main → _read` | cross_community | 5 |
| `Print_cmd → _write` | cross_community | 4 |
| `Analyze_cmd → _read` | cross_community | 4 |
| `Send_cmd → _write` | cross_community | 4 |
| `Main → _read` | cross_community | 3 |
| `Main → Backend_factory` | cross_community | 3 |
| `Print_cmd → Guess_backend` | cross_community | 3 |

## Connected Areas

| Area | Connections |
|------|-------------|
| Brother_ql | 5 calls |

## How to Explore

1. `gitnexus_context({name: "send_cmd"})` — see callers and callees
2. `gitnexus_query({query: "backends"})` — find related execution flows
3. Read key files listed above for implementation details

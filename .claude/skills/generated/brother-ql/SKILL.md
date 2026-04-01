---
name: brother-ql
description: "Skill for the Brother_ql area of brother_ql. 61 symbols across 17 files."
---

# Brother_ql

61 symbols | 17 files | Cohesion: 66%

## When to Use

- Working with code in `brother_ql/`
- Understanding how add_initialize, add_status_information, add_invalidate work
- Modifying brother_ql-related functionality

## Key Files

| File | Symbols |
|------|---------|
| `brother_ql/raster.py` | add_initialize, add_status_information, add_invalidate, add_media_and_quality, add_margins (+12) |
| `brother_ql/reader.py` | hex_format, chunker, match_opcode, interpret_response, merge_specific_instructions (+3) |
| `brother_ql/cli.py` | info, discover, discover_and_list_available_devices, print_cmd, analyze_cmd (+2) |
| `brother_ql/brother_ql_debug.py` | continue_reading, log_interp_response, print_and_debug, BrotherQL_USBdebug, main |
| `brother_ql/exceptions.py` | BrotherQLError, BrotherQLUnsupportedCmd, BrotherQLUnknownModel, BrotherQLRasterError |
| `brother_ql/helpers.py` | get_element_by_identifier, ElementsManager, iter_identifiers |
| `brother_ql/output_helpers.py` | log_discovered_devices, textual_description_discovered_devices, textual_label_description |
| `brother_ql/models.py` | get_model_by_identifier, ModelsManager |
| `brother_ql/labels.py` | get_label_by_identifier, LabelsManager |
| `brother_ql/brother_ql_create.py` | main, create_label |

## Entry Points

Start here when exploring this area:

- **`add_initialize`** (Function) — `brother_ql/raster.py:100`
- **`add_status_information`** (Function) — `brother_ql/raster.py:104`
- **`add_invalidate`** (Function) — `brother_ql/raster.py:119`
- **`add_media_and_quality`** (Function) — `brother_ql/raster.py:151`
- **`add_margins`** (Function) — `brother_ql/raster.py:198`

## Key Symbols

| Symbol | Type | File | Line |
|--------|------|------|------|
| `BrotherQL_USBdebug` | Class | `brother_ql/brother_ql_debug.py` | 10 |
| `BrotherQLRaster` | Class | `brother_ql/raster.py` | 29 |
| `BrotherQLReader` | Class | `brother_ql/reader.py` | 236 |
| `BrotherQLError` | Class | `brother_ql/exceptions.py` | 1 |
| `BrotherQLUnsupportedCmd` | Class | `brother_ql/exceptions.py` | 4 |
| `BrotherQLUnknownModel` | Class | `brother_ql/exceptions.py` | 7 |
| `BrotherQLRasterError` | Class | `brother_ql/exceptions.py` | 10 |
| `LabelsManager` | Class | `brother_ql/labels.py` | 112 |
| `ElementsManager` | Class | `brother_ql/helpers.py` | 5 |
| `ModelsManager` | Class | `brother_ql/models.py` | 69 |
| `add_initialize` | Function | `brother_ql/raster.py` | 100 |
| `add_status_information` | Function | `brother_ql/raster.py` | 104 |
| `add_invalidate` | Function | `brother_ql/raster.py` | 119 |
| `add_media_and_quality` | Function | `brother_ql/raster.py` | 151 |
| `add_margins` | Function | `brother_ql/raster.py` | 198 |
| `get_pixel_width` | Function | `brother_ql/raster.py` | 218 |
| `add_raster_data` | Function | `brother_ql/raster.py` | 221 |
| `add_print` | Function | `brother_ql/raster.py` | 268 |
| `get_model_by_identifier` | Function | `brother_ql/models.py` | 73 |
| `get_label_by_identifier` | Function | `brother_ql/labels.py` | 116 |

## Execution Flows

| Flow | Type | Steps |
|------|------|-------|
| `Main → Hex_format` | cross_community | 6 |
| `Main → Get_element_by_identifier` | cross_community | 5 |
| `Main → _read` | cross_community | 5 |
| `Main → Info` | cross_community | 5 |
| `Main → LabelsManager` | cross_community | 4 |
| `Main → ModelsManager` | cross_community | 4 |
| `Labels → Get_element_by_identifier` | cross_community | 4 |
| `Print_cmd → Get_element_by_identifier` | cross_community | 4 |
| `Print_cmd → _write` | cross_community | 4 |
| `Analyze_cmd → _read` | cross_community | 4 |

## Connected Areas

| Area | Connections |
|------|-------------|
| Backends | 7 calls |

## How to Explore

1. `gitnexus_context({name: "add_initialize"})` — see callers and callees
2. `gitnexus_query({query: "brother_ql"})` — find related execution flows
3. Read key files listed above for implementation details

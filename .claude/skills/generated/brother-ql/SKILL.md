---
name: brother-ql
description: "Skill for the Brother_ql area of brother_ql. 59 symbols across 17 files."
---

# Brother_ql

59 symbols | 17 files | Cohesion: 69%

## When to Use

- Working with code in `brother_ql/`
- Understanding how textual_label_description, get_model_by_identifier, get_label_by_identifier work
- Modifying brother_ql-related functionality

## Key Files

| File | Symbols |
|------|---------|
| `brother_ql/raster.py` | __init__, add_initialize, add_status_information, add_invalidate, add_media_and_quality (+11) |
| `brother_ql/reader.py` | chunker, match_opcode, merge_specific_instructions, BrotherQLReader, analyse (+3) |
| `brother_ql/cli.py` | models_cmd, labels, discover, discover_and_list_available_devices, info (+1) |
| `brother_ql/brother_ql_debug.py` | BrotherQL_USBdebug, main, print_and_debug, continue_reading, log_interp_response |
| `brother_ql/exceptions.py` | BrotherQLUnknownModel, BrotherQLError, BrotherQLUnsupportedCmd, BrotherQLRasterError |
| `brother_ql/output_helpers.py` | textual_label_description, log_discovered_devices, textual_description_discovered_devices |
| `brother_ql/helpers.py` | ElementsManager, iter_identifiers, get_element_by_identifier |
| `brother_ql/models.py` | ModelsManager, get_model_by_identifier |
| `brother_ql/labels.py` | LabelsManager, get_label_by_identifier |
| `brother_ql/brother_ql_create.py` | main, create_label |

## Entry Points

Start here when exploring this area:

- **`textual_label_description`** (Function) — `brother_ql/output_helpers.py:6`
- **`get_model_by_identifier`** (Function) — `brother_ql/models.py:73`
- **`get_label_by_identifier`** (Function) — `brother_ql/labels.py:116`
- **`iter_identifiers`** (Function) — `brother_ql/helpers.py:34`
- **`get_element_by_identifier`** (Function) — `brother_ql/helpers.py:42`

## Key Symbols

| Symbol | Type | File | Line |
|--------|------|------|------|
| `ModelsManager` | Class | `brother_ql/models.py` | 69 |
| `LabelsManager` | Class | `brother_ql/labels.py` | 112 |
| `ElementsManager` | Class | `brother_ql/helpers.py` | 5 |
| `BrotherQLUnknownModel` | Class | `brother_ql/exceptions.py` | 7 |
| `BrotherQLError` | Class | `brother_ql/exceptions.py` | 1 |
| `BrotherQLUnsupportedCmd` | Class | `brother_ql/exceptions.py` | 4 |
| `BrotherQLRasterError` | Class | `brother_ql/exceptions.py` | 10 |
| `BrotherQL_USBdebug` | Class | `brother_ql/brother_ql_debug.py` | 10 |
| `BrotherQLReader` | Class | `brother_ql/reader.py` | 236 |
| `textual_label_description` | Function | `brother_ql/output_helpers.py` | 6 |
| `get_model_by_identifier` | Function | `brother_ql/models.py` | 73 |
| `get_label_by_identifier` | Function | `brother_ql/labels.py` | 116 |
| `iter_identifiers` | Function | `brother_ql/helpers.py` | 34 |
| `get_element_by_identifier` | Function | `brother_ql/helpers.py` | 42 |
| `models_cmd` | Function | `brother_ql/cli.py` | 63 |
| `labels` | Function | `brother_ql/cli.py` | 72 |
| `main` | Function | `brother_ql/brother_ql_info.py` | 7 |
| `main` | Function | `brother_ql/brother_ql_create.py` | 16 |
| `create_label` | Function | `brother_ql/brother_ql_create.py` | 54 |
| `add_initialize` | Function | `brother_ql/raster.py` | 100 |

## Execution Flows

| Flow | Type | Steps |
|------|------|-------|
| `Main → Hex_format` | cross_community | 6 |
| `Main → Get_element_by_identifier` | cross_community | 5 |
| `Main → _read` | cross_community | 5 |
| `Main → Info` | cross_community | 5 |
| `Main → LabelsManager` | cross_community | 4 |
| `Main → ModelsManager` | cross_community | 4 |
| `Labels → Get_element_by_identifier` | intra_community | 4 |
| `Print_cmd → Get_element_by_identifier` | cross_community | 4 |
| `Print_cmd → _write` | cross_community | 4 |
| `Analyze_cmd → _read` | cross_community | 4 |

## Connected Areas

| Area | Connections |
|------|-------------|
| Backends | 7 calls |

## How to Explore

1. `gitnexus_context({name: "textual_label_description"})` — see callers and callees
2. `gitnexus_query({query: "brother_ql"})` — find related execution flows
3. Read key files listed above for implementation details

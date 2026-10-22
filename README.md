# Honeybee Construction Tools

Create Honeybee constructions from a material CSV or a target wall U-value using Grasshopper Python components.

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

This repository brings together two related examples from the Computational Sustainable Design collection. The original CSV workflow documentation names **Sanjay Somanath** as author; original script credits remain in the preserved sources. See [migration and provenance](docs/migration.md).

## Getting started

1. Use Rhino/Grasshopper with GhPython, Honeybee Energy, and Ladybug Rhino libraries. Exact supported versions are not recorded.
2. For the packaged graphical example, choose **File → Open** in Grasshopper and open [`csv-constructions/HB_CreateConstructionFromCSV.gh`](csv-constructions/HB_CreateConstructionFromCSV.gh).
3. Set its CSV path to [`csv-constructions/221015_material_database.csv`](csv-constructions/221015_material_database.csv), then enable the CSV component's `run` toggle. Inspect construction outputs and warnings.
4. For the target-U-value example, load [`target-u-value/simpleUValue.py`](target-u-value/simpleUValue.py) into a GhPython component with inputs `_u_value` and `_name_`, and outputs `constr` and `calculation`. Try `0.25` and `MyWall`.

[The reproduction guide](docs/reproduce.md) explains the actual port names, environment constraints and expected checks. See [methods and assumptions](docs/README.md), [data provenance](data/README.md), and [citation metadata](CITATION.cff). Repository code is licensed under [MIT](LICENSE).

The scripts and scientific assumptions are preserved. Rhino execution was not validated during migration. Contributor roles, funding, publication links and archive identifiers remain **TODO** for project members.

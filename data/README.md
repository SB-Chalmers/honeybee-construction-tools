# Data inventory and provenance

| Item | Role and location | Provenance and interpretation |
| --- | --- | --- |
| `csv-constructions/221015_material_database.csv` | Small example input | Original semicolon-delimited material table. Thermal fields include thickness (m), conductivity (W/m-K), density (kg/m³) and glazing U-value (W/m²K). Material-data sources, cost/carbon reference quantities and reuse terms are **TODO**. |
| `csv-constructions/HB_CreateConstructionFromCSV.gh` | Graphical example | Original definition, retained alongside component sources. |
| `csv-constructions/media/` | Documentation images | Original canvas and material-property screenshots; not a numerical test dataset. |
| Constants in `target-u-value/simpleUValue.py` | Embedded example inputs | Fixed cladding, concrete and insulation properties. See [methods and assumptions](../docs/README.md). |
| Generated constructions and calculation text | Runtime outputs | Created in Grasshopper; not stored as a separate dataset by the preserved sources. |

Original paths, checksum provenance and repository boundaries are recorded in [migration.json](../migration.json) and [migration documentation](../docs/migration.md). Source inputs and historical text remain recoverable. Keep new result exports separate from the bundled example, with the source commit, input values and software versions recorded.

Repository code is [MIT licensed](../LICENSE). Separate material-data/image terms and attribution require confirmation where applicable; the code license does not establish the provenance of example physical/economic data or alter third-party software licenses.

**Dataset archive DOI:** not recorded in the source; TODO if an archive is created.
**Software archive DOI:** not recorded in the source; TODO if an archive is created.

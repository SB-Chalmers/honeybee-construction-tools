# Construction workflows and assumptions

## CSV constructions

The [`csv-constructions/`](../csv-constructions/original-readme.md) example reads material records, separates insulation/board/window categories, forms layer combinations, and creates Honeybee `EnergyMaterial` and `OpaqueConstruction` objects. The example database is semicolon-delimited with columns `identifier;Material;Thickness;Conductivity;Cost;Embodied carbon;Density;U-value`.

The source reader uses a default comma CSV reader and passes its first field downstream as a semicolon-containing string. `split_materials.py` categorizes that string by case-sensitive substrings; the construction helper splits on semicolons. Preserve the original format when inspecting the example. Units for thickness, conductivity, density and specific heat are m, W/m-K, kg/m³ and J/kg-K respectively. Cost/carbon reference quantities and provenance need confirmation before research reuse.

The current `create_solutions.py` forms four-layer insulation/board/insulation/board combinations. Alternative three- and five-layer combinations are commented out. The original README reports 6,479 solutions for its example, but this historical count has not been reproduced and should not be treated as a guaranteed output of every script/canvas configuration.

The construction helper fixes specific heat at 950 J/kg-K, roughness at `MediumRough`, and thermal/solar/visible absorptances at 0.9/0.7/0.9. These are shared assumptions, not measured properties for each material. The script docstring refers to `_solutions`, while its executable code reads `_solution`; the component input must match the latter.

## Target U-value

The [`target-u-value/`](../target-u-value/original-readme.md) example creates a fixed three-layer wall: exterior cladding, calculated insulation, and interior concrete. It solves `U = 1 / sum(thickness / conductivity)` for insulation thickness, then builds a Honeybee opaque construction and a calculation explanation.

Fixed cladding is 0.02 m at 1.0 W/m-K; concrete is 0.2 m at 1.95 W/m-K; insulation conductivity is 0.04 W/m-K. The calculation includes material-layer resistance only; it does not add internal/external surface resistances or thermal bridges. It must not be interpreted as a complete regulatory U-value calculation without reviewing those assumptions. A target whose total resistance is no greater than the fixed layers raises an error. Zero or negative U-values also need input validation before reuse.

The original text names `_name`, but the executable source reads `_name_`. Configure that actual port name. No `.gh` definition is supplied for this second example; [reproduction instructions](reproduce.md) explain component setup.

## Environment and metadata

These examples rely on Grasshopper context, `ghenv` or `ghpythonlib`, and Honeybee/Ladybug libraries. They are not standalone command-line scripts. The legacy CSV example should first be inspected in GhPython; a supported Rhino/Python/library version matrix is **TODO**. No Python 3 environment or automated tests are claimed.

The CSV README names Sanjay Somanath; its scripts retain `ssanjay` and `fojacob` author identifiers. The target-U-value source does not identify an author. **TODO:** confirm full contributor credit for the grouped repository, agreed roles, maintenance status, funding and thesis/paper/archive identifiers. [CITATION.cff](../CITATION.cff) records the confirmed named author without inventing missing author metadata.

See [data provenance](../data/README.md), [reproduction instructions](reproduce.md), and [migration history](migration.md).

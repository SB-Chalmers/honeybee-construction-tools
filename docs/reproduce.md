# Run the construction examples

These are source-based graphical instructions. Rhino and Honeybee were not executed during migration; the scientific calculations and source interfaces were preserved.

## Environment

Use Rhino with Grasshopper, GhPython, Honeybee Energy and Ladybug Rhino. Dependencies imported by the sources include `honeybee`, `honeybee_energy`, `ladybug_rhino`, `rhinoscriptsyntax`, and `ghpythonlib.treehelpers`. They must be available to the Grasshopper component runtime. Exact Rhino/GhPython/library versions and operating system are **TODO**. Installing packages into a separate Python 3 interpreter does not establish compatibility with the canvas.

## Example 1: material CSV to constructions

1. Start Grasshopper in Rhino and choose **File → Open → `csv-constructions/HB_CreateConstructionFromCSV.gh`** from this checkout.
2. Keep the CSV reader's `run` input **False** while changing the file input. Repoint its `path` to this checkout's `csv-constructions/221015_material_database.csv`.
3. Inspect the components against [`csv-constructions/media/script.png`](../csv-constructions/media/script.png). If missing libraries or script errors appear, resolve the environment before proceeding.
4. Toggle the reader's `run` input to **True** and inspect the parsed records, category branches and solution tree. The source expects the provided semicolon-containing records. Do not silently replace the format with a differently delimited database.
5. Inspect the Honeybee creation component output `HB_Constructions`. If recreating the source component manually, its input must be named `_solution` and provide the solution tree expected by `ghpythonlib.treehelpers.tree_to_list`; the source docstring's `_solutions` spelling is inconsistent.
6. Check a construction's layer order, material names, thicknesses, conductivity and density against the input records. The current standalone solution source builds four layers. Treat the original README's reported solution count as historical until the actual canvas configuration is verified.

The individual `.py` files are component sources, not a command-line pipeline. The original `.gh` is the intended first entry point.

## Example 2: target U-value to wall construction

1. In Grasshopper, create a GhPython scripting component in a runtime that exposes `ghenv` and the Honeybee/Ladybug imports. Open its script editor and load or paste `target-u-value/simpleUValue.py`.
2. Configure two item inputs named exactly `_u_value` and `_name_`. Connect a numeric value `0.25` to `_u_value` and a text panel containing `MyWall` to `_name_`. The actual source uses a trailing underscore for the name input.
3. Configure outputs `constr` and `calculation`, keeping the normal diagnostic output if supplied by the component. Recompute the canvas.
4. Connect `calculation` to a text panel to inspect the seven calculation steps. Inspect `constr` as a Honeybee opaque construction with exterior-to-interior cladding/insulation/concrete layers.
5. For this example, the material-layer calculation is `R_fixed = 0.2/1.95 + 0.02/1.0`, and insulation thickness is `(1/0.25 - R_fixed) * 0.04`, approximately **0.155097 m**. This is an arithmetic expectation derived from the source, not a measured or Rhino-validated result. Verify the reported calculation and material thickness agree.

## Checks and limits

- Use positive U-values; confirm the target permits positive insulation resistance.
- Verify material-layer order and units before connecting constructions to an energy model.
- Compare the target-U-value arithmetic with the script's calculation text. Account separately for surface resistances if the intended engineering U-value convention includes them.
- No automated test suite, example simulation output or supported-version matrix is supplied. **TODO:** a project member should record a successful runtime and check both graphical examples before claiming a supported release.

See [the data inventory](../data/README.md) for input provenance and terms. Neither example writes a result dataset automatically; record any exports with the input database, script commit and runtime versions.

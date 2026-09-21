# Exhibit J-9: CAD/DXF Pattern-Digitization Workflow

## What this is

A standalone, working demonstration of the digitization step
described in the internship report (Exhibit D-1): converting legacy
pattern measurements into DXF (Drawing Exchange Format) files, the
industry-standard CAD interchange format the internship report
describes working with via Valentina and Autodesk AutoCAD.

This is distinct from Exhibits J-1 through J-8, which address the
downstream cutting-optimization and robust-statistics work. This
exhibit addresses the digitization step itself: converting raw
measurements into valid, machine-readable CAD geometry.

## What it does

1. Represents five legacy pattern pieces (bodice front, sleeve,
   collar, back panel, cuff) as ordered coordinate lists, the form in
   which physical pattern measurements are typically first recorded.
2. Writes each piece as a closed polyline entity into a real DXF
   file, using `ezdxf`, a widely used open-source Python library for
   reading and writing DXF files.
3. Reads the resulting DXF file back and verifies that the recovered
   geometry exactly matches the original input.
4. Computes each piece's bounding box and area directly from the
   recovered DXF geometry, the same information a downstream
   nesting/cutting-optimization step (Exhibits J-1, J-6, J-8) requires
   as its input, demonstrating the direct link between this
   digitization step and that later optimization work.

## Results (reported exactly as obtained)

| Pattern | Original Points | Recovered Points | Match | Area (cm²) |
|---|---|---|---|---|
| bodice_front | 7 | 7 | YES | 1738.0 |
| sleeve | 6 | 6 | YES | 856.0 |
| collar | 6 | 6 | YES | 240.0 |
| back_panel | 7 | 7 | YES | 2146.0 |
| cuff | 4 | 4 | YES | 112.0 |

All five pattern pieces round-tripped losslessly. The output file was
independently verified as a genuine DXF file using the standard `file`
utility, which identified it as "AutoCAD Drawing Exchange Format,
version 2010" without relying on this script's own reporting.

## Running it yourself

```
pip install ezdxf
python dxf_digitization_demo.py
```

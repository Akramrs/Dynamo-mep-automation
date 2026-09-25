# Pipe Hanger Alignment for Chilled Water Pipes

![Dynamo graph](assets/dynamo-graph.png)

**Sample run:** 12 hangers found matching the target family name, checked against 94 pipes in view — hangers out of tolerance were corrected in one run (see report output below).

## Overview
This script automatically aligns Pipe Hangers to their host Chilled Water (CHW) pipe's centerline elevation, within a selected 3D view. Instead of manually checking and nudging each hanger's elevation to match the pipe it supports, the script reads the pipe's actual centerline height and writes it back to the hanger's `Elevation from Level` parameter in one run.

## Problem it solves
On large CHW models, pipe hangers are frequently placed at a default offset rather than the pipe's true centerline — especially after pipe routing changes late in coordination. Catching and fixing this manually, hanger by hanger, across hundreds of elements is slow and error-prone. This script finds every hanger in the chosen view, checks it against its host pipe, and corrects only the ones that are out of alignment.

## How it works
1. **Get the active document** — `Document.Current` feeds the document into the script.
2. **Select scope** — the user wires in a 3D view, restricting the script to just the hangers visible/scoped in that view.
3. **Dry-run toggle** — a Boolean input controls `DRY_RUN`:
   - `True` → reports what *would* change, without touching the model
   - `False` → applies the changes inside a Revit transaction
4. **Python script (Revit API)**:
   - Collects all `Pipe Hanger` category elements in the chosen view
   - For each hanger, resolves its host pipe (via `Host` or `SuperComponent`)
   - Calculates the pipe's centerline elevation (average Z of its start/end points)
   - Converts that to an elevation relative to the hanger's reference level
   - Compares it to the hanger's current `Elevation from Level` value
   - Updates the parameter only if it's off, and logs the result
5. **Report output** — a dictionary of `processed / updated / skipped / errors`, each listing element IDs and the reason, viewable in a Watch node.

## Inputs
| Input | Type | Description |
|-------|------|--------------|
| `IN[0]` | Revit View | The 3D view to scope the hanger search to |
| `IN[1]` | Document | Current Revit document (`Document.Current`) |
| `IN[2]` | Boolean | `DRY_RUN` — True to preview only, False to commit changes |

## Output
A report dictionary with four lists:
- **processed** — total hangers found
- **updated** — hangers whose elevation was corrected (with the new value and host pipe ID)
- **skipped** — hangers left alone (no host pipe, no location curve, already aligned, wrong/missing parameter, etc.)
- **errors** — any hanger that failed, with the exception message

## Tools / environment
- Revit 2026
- Dynamo 3.4.1 (CPython3 engine)
- Revit API: `RevitAPI`, `RevitServices`

## Assumptions
- Hangers are Revit **Pipe Hanger** category (`OST_PipeHanger`) family instances hosted directly on the pipe.
- The hanger family has an editable instance parameter named **`Elevation from Level`** (rename `PARAM_NAME` in the script if your family uses a different name).
- Always run with `DRY_RUN = True` first to review the report before committing changes on a production model.

## Before / After
![Hanger alignment demo](assets/hanger-alignment-demo.gif)

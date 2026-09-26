# Dynamo Automation Scripts — BIM MEP Portfolio

**Discipline:** HVAC / Chilled Water (CHW) Systems
**Role:** BIM Modeller (Revit MEP)
**Tools:** Revit MEP, Dynamo (CPython3), Navisworks Manage, AutoCAD MEP

## About this repository

This repository is a collection of Dynamo automation scripts developed and used during live BIM/MEP coordination projects, focused on Chilled Water (CHW) system modelling. Each script automates a repetitive modelling or QA/QC task — reducing manual rework and improving accuracy across large models.

Every script folder includes:
- The original `.dyn` file
- A `README.md` explaining what the script does, why it was built, and how it works
- Notes on assumptions and any customization needed for a different project setup

## Scripts

| # | Script | Category | Description |
|---|--------|----------|--------------|
| 01 | [Pipe Hanger Alignment for CHW Pipes](scripts/01-chilled-water-pipe-hanger-alignment) | Parameter Automation | Automatically aligns pipe hanger elevation to the host pipe's centerline elevation across a selected view. |

*(More scripts will be added here as they're documented.)*

## Skills demonstrated

- Dynamo visual scripting + embedded Python (CPython3 engine, Revit API)
- Revit API scripting (parameters, categories, levels, transactions)
- Safe automation design (dry-run/report-first pattern before committing changes)
- MEP/CHW-specific modelling logic (pipe hangers, elevations, hosting relationships)

## Contact

**Akram R S**
LinkedIn — www.linkedin.com/in/akramrs
Gmail — akramrs.028@gmail.com

# Dataset

This folder contains the requirement cases used for UML State Transition Diagram generation.

## Case Files

Each `case_*` folder normally contains:

1. `raw_requirement.txt` - the original natural-language requirement.
2. `structured_requirement.txt` - the structured requirement text used by prompts.
3. `aligned_requirement.txt` - the aligned requirement text used.
4. `diagram.puml` - the reference PlantUML State Transition Diagram.
5. `book_diagram.png` - the rendered reference diagram image.

## Notes

1. The dataset currently contains 80 cases.
2. Case folder names are stable identifiers used by the pipeline.
3. The train/test split is stored under `Data/processed/experiments/`.

# State Transition Diagram LLM Workflow

This repository contains the dataset, prompts, validation rules, and human evaluation materials used to study how LLMs generate UML state transition diagrams from natural-language requirements.

## Overview

The repository supports several related workflows:

- direct generation of PlantUML state diagrams from requirements
- one-shot and few-shot generation with example guidance
- retrieval-augmented generation using supporting reference context
- repair of candidate PlantUML diagrams using validation feedback
- human evaluation and structural validation of generated diagrams

## Repository Structure

```text
State_Transition_Diagram_LLM_workflow/
|-- Dataset/
|   |-- case_01_*/
|   |-- case_02_*/
|   `-- ...
|-- Prompts/
|   |-- zero_shot_prompt.txt
|   |-- one_shot_prompt.txt
|   |-- fewshot_prompt.txt
|   |-- rag_prompt.txt
|   `-- repair_prompt.txt
|-- Evaluation Form - UML State Diagram Scoring - Google Forms.pdf
`-- Validation rules for Structural Validation.pdf
```

## Dataset

The `Dataset` folder contains the individual requirement cases used in the workflow. Each case folder typically includes:

- `raw_requirement.txt` - the original natural-language requirement
- `structured_requirement.txt` - the manually structured requirement format used downstream
- `bidirectionally_aligned_requirement.txt` - the aligned requirement text used for traceability
- `diagram.puml` - the reference PlantUML state diagram
- `book_diagram.png` - the rendered diagram image

The dataset currently includes 80 cases.

## Prompts

The `Prompts` folder contains five prompt variants:

- `zero_shot_prompt.txt` - generates a diagram without examples, using only the task instructions
- `one_shot_prompt.txt` - adds one worked example to demonstrate the expected format
- `fewshot_prompt.txt` - adds multiple worked examples to provide stronger guidance
- `rag_prompt.txt` - uses supporting reference context alongside the target requirement
- `repair_prompt.txt` - repairs a candidate PlantUML diagram using validation issues with the smallest possible edit

Across these prompts, the shared expectations are:

- identify the relevant system states and transition triggers
- include exactly one initial state and at least one final state
- output only valid PlantUML code
- avoid explanations, markdown fences, or extra prose
- preserve the meaning of the requirement when repairing a diagram

## Evaluation and Validation

- `Evaluation Form - UML State Diagram Scoring - Google Forms.pdf` is used for the human evaluation section
- `Validation rules for Structural Validation.pdf` contains the rules used for structural validation


## Notes

- This repository is organized as a research and evaluation artifact collection.
- The prompt set covers direct generation, retrieval-augmented generation, and repair.

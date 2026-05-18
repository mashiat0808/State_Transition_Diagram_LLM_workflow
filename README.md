# State Transition Diagram LLM Workflow

This repository supports the paper **Towards Reliable AI-Assisted Behavioral Modeling: Evaluating Prompting, Retrieval, and Repair Strategies for UML State Transition Diagram Generation**.

It contains the dataset, prompts, validation rules, human evaluation materials, retrieval resources, and runnable code used to study how LLMs generate UML State Transition Diagrams from natural-language requirements.

## Overview

The repository can be used to execute the following workflows:

1. Direct generation of PlantUML State Transition Diagrams from requirements.
2. One-shot and few-shot generation with example guidance.
3. Retrieval-augmented generation using supporting reference context.
4. Repair of candidate PlantUML diagrams using validation feedback.
5. Human evaluation and structural validation of generated diagrams.

## Repository Structure

```text
State_Transition_Diagram_LLM_workflow/
|-- Code/        Python pipeline for generation, validation, repair, and metrics.
|-- Dataset/     Requirement cases and reference PlantUML diagrams.
|-- Data/        Processed split files and retrieval resources.
|-- Prompts/     Prompt templates for generation and repair.
|-- Evaluation form PDF
|                Human evaluation form used in the study.
|-- Validation rules for Structural Validation.pdf
|                Structural validation rules used for generated diagrams.
`-- README.md    Top-level repository guide.
```

## Documentation Guide

1. [Code/README.md](Code/README.md) explains how to run the Python pipeline and command-line scripts.
2. [Dataset/README.md](Dataset/README.md) explains the requirement case folders and reference diagram files.
3. [Data/README.md](Data/README.md) explains the processed split file and RAG corpus resources.
4. `Prompts/` contains the prompt templates used by the generation and repair workflows.

## Dataset

The `Dataset` folder contains 80 requirement cases and their reference PlantUML State Transition Diagrams. See [Dataset/README.md](Dataset/README.md) for the case-file structure.

## Prompts

The `Prompts` folder contains five prompt variants:

1. `zero_shot_prompt.txt` - generates a diagram without examples.
2. `one_shot_prompt.txt` - adds one worked example.
3. `fewshot_prompt.txt` - adds multiple worked examples.
4. `rag_prompt.txt` - uses supporting reference context with the target requirement.
5. `repair_prompt.txt` - repairs a candidate PlantUML diagram using validation issues.

## Evaluation and Validation

1. The evaluation form PDF is used for the human evaluation section.
2. `Validation rules for Structural Validation.pdf` contains the rules used for structural validation.

## Notes

1. This repository is organized as a research and evaluation artifact collection.
2. The prompt set covers direct generation, retrieval-augmented generation, and repair.
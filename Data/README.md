# Data

This folder contains processed experiment files and retrieval resources used by the UML State Transition Diagram generation workflow.

## Contents

1. `processed/experiments/split_35_seed42.json` stores the reproducible train/test split.
2. `rag_corpus/dataset_examples/` stores Markdown examples derived from training cases.
3. `rag_corpus/plantuml_rules/` stores concise PlantUML guidance.
4. `rag_corpus/state_diagram_theory/` stores theory notes used as retrieval context. The folder name is retained from the source material.

## Notes

1. Keep curated retrieval documents under `Data/rag_corpus/`.
2. Keep generated Chroma vector indexes under `results/rag_db/`.
3. See [../Code/README.md](../Code/README.md) for commands that build and use the RAG index.

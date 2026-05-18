# UML State Transition Diagram Generation Pipeline

This folder contains the code used to generate PlantUML State Transition Diagrams, run validation-based repair, and report syntax and structural validity.

For repository-level context, see [../README.md](../README.md). For dataset and RAG resource details, see [../Dataset/README.md](../Dataset/README.md) and [../Data/README.md](../Data/README.md).

## Main Scripts

1. `plantuml_experiment_pipeline.py` is the main command-line entry point for creating splits, running diagram generation, applying repair, and recomputing metrics.
2. `plantuml_pipeline/` contains the reusable pipeline package.
3. `build_rag_index.py` builds the Chroma vector index from Markdown files in `Data/rag_corpus/`.
4. `create_rag_dataset_examples.py` creates RAG example Markdown files from the training part of the dataset.
5. `create_rag_analysis_corpora.py` copies existing RAG documents into smaller analysis corpora.
6. `hybrid_requirement_pipeline.py` prepares structured functional requirements from raw requirement text when needed.
7. `build_repair_iteration_artifacts.py` summarizes repair attempts and prepares repair-iteration review files.
8. `report_validity_percentages.py` reports PlantUML syntax validity and stricter State Transition Diagram structural validity.

## Requirements

1. Start Ollama before running generation:

```bash
ollama serve
```

2. Install Chroma if vector RAG is used:

```bash
pip install chromadb
```

3. Make sure the `plantuml` command is available on the system path for syntax checking.

## Workflow

1. Create the train/test split:

```bash
PYTHONPATH=Code \
python3 Code/plantuml_experiment_pipeline.py split \
  --dataset-root Dataset \
  --output Data/processed/experiments/split_35_seed42.json
```

2. Build the vector RAG index:

```bash
PYTHONPATH=Code \
python3 Code/build_rag_index.py \
  --rag-docs-dir Data/rag_corpus \
  --rag-db-dir results/rag_db
```

3. Run all configured generation strategies:

```bash
PYTHONPATH=Code \
python3 Code/plantuml_experiment_pipeline.py run \
  --dataset-root Dataset \
  --results-root results/plantuml_pipeline \
  --rag-db-dir results/rag_db \
  --runs 3 \
  --save-prompts
```

4. Validate one PlantUML file directly:

```bash
PYTHONPATH=Code \
python3 Code/plantuml_experiment_pipeline.py validate \
  --puml results/plantuml_pipeline/example_diagram.puml \
  --json
```

5. Recompute metrics for generated diagrams:

```bash
PYTHONPATH=Code \
python3 Code/plantuml_experiment_pipeline.py metrics \
  --dataset-root Dataset \
  --results-root results/plantuml_pipeline
```



6. Run a quick non-RAG check on one case:

```bash
PYTHONPATH=Code \
python3 Code/plantuml_experiment_pipeline.py run \
  --dataset-root Dataset \
  --results-root results/plantuml_pipeline \
  --only-run-id open_source__qwen25_7b_instruct__zero_shot \
  --only-case-id case_01_healthcare_portal \
  --runs 1 \
  --save-prompts
```

## Validation Flow

1. Generated PlantUML is normalized and parsed.
2. The parser checks PlantUML syntax and State Transition Diagram structure.
3. Detected errors and warnings are saved with run metadata.
4. Repair-enabled strategies pass validation issues into the repair prompt.
5. The repaired diagram is kept only when the validation score improves.

Generated diagrams, prompts, metadata, and metric summaries are written under `results/plantuml_pipeline/`.

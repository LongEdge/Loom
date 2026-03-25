# Loom

**Loom is a lightweight platform that weaves together datasets, experiments, resources, and results into a unified, traceable workflow for deep learning labs.**

------

## Overview

Loom is designed to solve a common problem in research labs: experiments are easy to run, but hard to manage.

In typical workflows:

- Jobs are launched via SSH, tmux, or scripts
- GPU usage is unclear and often contested
- Datasets, configs, and logs are scattered
- Results are difficult to trace and reproduce

Loom introduces a simple, structured system to organize all of these pieces.

It treats everything in a lab as connected assets and builds a minimal platform to:

- submit and schedule experiments
- track resources (machines & GPUs)
- register datasets and references
- record experiment inputs and outputs
- make results traceable

------

## Key Concepts

Loom is built around a small set of core entities:

- **Machine / GPU** — compute resources
- **Dataset** — structured data used in experiments
- **Document** — papers, notes, or references
- **Task** — a submitted experiment job
- **Run** — an execution instance of a task
- **Artifact** — outputs such as checkpoints or logs

These entities are connected:

> assets → consumed by tasks → produce new assets

------

## What Loom is (and is not)

### Loom is:

- a lightweight experiment orchestration system
- a metadata-driven asset registry
- a lab-friendly alternative to ad-hoc workflows

### Loom is NOT:

- a full data storage platform
- a Kubernetes replacement
- a large-scale distributed system
- a complete ML platform

------

## Architecture (v0.1)

Loom follows a simple architecture:

- **Controller** (FastAPI)
  - central API
  - scheduling logic
  - metadata management
- **CLI**
  - primary user interface
  - submit / monitor / manage experiments
- **Metadata DB**
  - stores all entities and relationships

> Note: Agent is intentionally out of scope for v0.1 and is planned before v1.0, together with more intelligent scheduling and runtime capabilities.

------

## Features (v0.1)

- Machine & GPU registration (manual / metadata-driven)
- Resource-aware task scheduling (FIFO + GPU matching)
- Unified experiment submission
- Task lifecycle management
- Dataset registration
- Document / reference tracking
- Basic experiment result recording
- CLI-based interaction

------

## Example Workflow

```bash
# register dataset
lab dataset add --name coco_v1 --path /data/coco --version v1

# register reference
lab doc add --title "YOLOv8" --url https://...

# submit experiment
lab submit train.py --gpus 2 --dataset coco_v1

# check status
lab status <task_id>

# view logs
lab logs <task_id>
```

------

## Project Structure

```
loom/
  apps/
    controller/
    cli/
  core/
    db/
    models/
    scheduler/
    protocols/
```

------

## Design Principles

- **Metadata-first**
  Loom tracks relationships and references, not large files.
- **Minimal core**
  Start small, ensure correctness, expand later.
- **Traceability over convenience**
  Every result should be reproducible.
- **Single-node control plane (v0.1)**
  Keep deployment simple.

------

## Roadmap

### v0.1

- basic scheduling
- asset registration
- result tracking
- CLI interface

### v0.2

- web UI
- experiment comparison
- batch runs / sweep
- better logging

### v0.3+

- pluggable scheduler
- improved resource management
- experiment templates
- optional Java control plane

### Before v1.0 (committed)

- add machine-level Agent support for automated heartbeat and execution reporting
- introduce more intelligent scheduling strategies (priority, fairness, and policy hooks)
- add smarter runtime observability and recommendation-oriented experiment insights

------

## Getting Started (WIP)

Setup instructions will be added soon.

For now:

- Python 3.10+
- FastAPI
- SQLite / PostgreSQL

------

## Status

🚧 Early development (v0.1)

This project is under active design and iteration. APIs and structures may change.

------

## License

Apache 2.0

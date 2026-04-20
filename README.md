# Coding Assistants

[![DOI](https://zenodo.org/badge/1051646682.svg)](https://doi.org/10.5281/zenodo.17077276)

This repository contains presentations and configurations for workshops on AI-assisted coding.

Slide PDFs can be found in [releases](https://github.com/thawn/coding-assistants/releases).

Use a PDF reader that can play movies (e.g. Adobe Acrobat Reader, Foxit Reader).

## Presentations

### Vibe Coding: A Useful Science Tool

**Folder:** [`vibe_coding/`](vibe_coding/)

A presentation on vibe coding and AI coding agents. It introduces coding agents that work largely autonomously to implement features, fix bugs, and write documentation. Topics include web-based coding workflows using GitHub issues and pull requests, best practices for prompting agents, writing maintainable code, and the strengths and limitations of coding agents for scientific software development.

### Coding Assistants and How to Set Them Up

**Folder:** [`coding_assistants/`](coding_assistants/)

A 60-minute hands-on workshop on setting up and using IDE-integrated coding assistants such as GitHub Copilot and continue.dev. It covers typical use-cases including inline code completion, docstring generation, test generation, API usage examples, boilerplate generation, and refactoring suggestions. The workshop also addresses privacy considerations, model selection, and includes a live coding challenge.

## Configurations

**Folder:** [`configurations/`](configurations/)

Example plugin configurations for [continue.dev](https://continue.dev) with different backends:

- **Blablador** — using the Blablador API (requires an API key)
- **HZDR AI** — using the HZDR on-premise AI service
- **LM Studio** — using a locally running LM Studio instance

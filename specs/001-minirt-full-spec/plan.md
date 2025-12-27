# Implementation Plan: Full miniRT Implementation with Bonuses

**Branch**: `001-minirt-full-spec` | **Date**: 2025-12-27 | **Spec**: [spec.md](./spec.md)
**Input**: Feature specification from `spec.md`.

## Summary

This plan outlines the technical implementation for a ray tracer named `miniRT`. The program will be written in C, parse a scene from a `.rt` file, and render it using ray tracing techniques. The implementation will use the SDL2 library for cross-platform window management, event handling, and 2D rendering (pixel plotting). The project includes a mandatory set of features (basic shapes, lighting) and optional bonus features (advanced lighting, materials, and shapes).

## Technical Context

**Language/Version**: C (C99 standard)  
**Primary Dependencies**: SDL2 (for windowing, events, and pixel buffer management)  
**Storage**: Scene description files with a `.rt` extension.  
**Testing**: A custom C unit testing harness.  
**Target Platform**: Linux and macOS.
**Project Type**: Single command-line executable.
**Performance Goals**: Target a rendering frame rate of 30 FPS for a typical scene (~50 objects).
**Constraints**: Render a single image from a static scene. No runtime interaction beyond closing the window.
**Scale/Scope**: The system will be designed to handle scenes with up to ~50 objects.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

The principles from the project constitution (`.specify/memory/constitution_kr.md`, v5.0.0) have been reviewed.

1. **Project Structure Standard**: **PASS**. The proposed structure adheres to the constitution.
2. **Code Quality Automation**: **PASS**. The plan assumes CI will enforce linting, formatting, and building.
3. **Documentation and Wiki Sync**: **PASS**. All design artifacts are being created within the feature directory.
4. **Workflow System**: **PASS**. This plan is part of the standard PR-based workflow.
5. **Tool and Environment Standards**: **PASS**. The use of SDL2 and Make aligns with C development standards.
6. **Bilingual Specification Management**: **PASS**.
7. **42 School Function Constraints**: **PASS**. The plan does not violate these; a `STRICT=1` flag can be added to the Makefile to enforce this.
8. **Security Standards**: **PASS**.
9. **Branching Strategy**: **PASS**. We are on a feature branch.
10. **Commit Message Rules**: **PASS**. Will be followed during implementation.
11. **Test Strategy and Coverage**: **PASS**. The plan includes unit and integration testing.
12. **Deprecation Policy**: **PASS**. Not applicable at this stage.

## Project Structure

### Documentation (this feature)

```text
specs/001-minirt-full-spec/
├── plan.md              # This file
├── research.md          # Research on graphics libraries (Complete)
├── data-model.md        # Data model for scene entities (Complete)
├── quickstart.md        # Build and run instructions (Complete)
├── contracts/           # API and file format contracts
│   └── cli.md           # CLI and .rt file format definition (Complete)
└── tasks.md             # To be created by /speckit.tasks
```

### Source Code (repository root)

```text
# Single project structure
src/
├── main.c           # Entry point, argument parsing, main loop
├── parsing/         # Scene file (.rt) parsing logic
├── rendering/       # Ray tracing, lighting, and shading logic
├── geometry/        # Geometric calculations (vectors, intersections)
├── objects/         # Sphere, plane, cylinder, cone implementations
├── system/          # Window and event handling (SDL2 wrapper)
└── include/         # Header files

libft/               # libft sources (as per constitution)

tests/
├── scenes/          # Test .rt scene files (valid and invalid)
└── unit/            # Unit tests for geometry, parsing, etc.

scenes/              # Example scenes for demonstration
```

**Structure Decision**: A single project structure is chosen, as `miniRT` is a self-contained command-line executable. The source code is modularized into directories based on functionality (parsing, rendering, geometry, etc.) to ensure clarity and maintainability, in line with the project constitution.

## Complexity Tracking

No constitution violations were identified that require justification.
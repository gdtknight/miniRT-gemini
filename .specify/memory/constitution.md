<!--
SYNC IMPACT REPORT
==================
Version Change: 4.0.0 → 4.1.0
Updated: 2025-12-27

RATIONALE FOR VERSION 4.1.0:
- MINOR version bump: This version introduces a new principle and clarifies existing ones to resolve inconsistencies between the constitution and project templates.
- Modified Principle VI (Bilingual Specification Management): Clarified the directory structure to be `specs/[feature]/[lang]/spec.md`.
- Modified Principle XI (Test Strategy and Coverage): Removed ambiguity about optional tests, making them non-negotiable as per the principle.
- Added Principle XIII (Template and Tooling Consistency): A new principle to ensure project templates and tooling scripts remain synchronized with the constitution.

PRINCIPLES DEFINED (13 total):
1. Project Structure Standards (NON-NEGOTIABLE)
2. Code Quality Automation (NON-NEGOTIABLE)
3. Documentation and Wiki Synchronization (NON-NEGOTIABLE)
4. Workflow System (NON-NEGOTIABLE)
5. Tools and Environment Standards (NON-NEGOTIABLE)
6. Bilingual Specification Management (NON-NEGOTIABLE)
7. 42 School Function Constraints (OPTIONAL)
8. Security Standards (NON-NEGOTIABLE)
9. Branching Strategy (NON-NEGOTIABLE)
10. Commit Message Convention (NON-NEGOTIABLE)
11. Test Strategy and Coverage (NON-NEGOTIABLE)
12. Deprecation Policy (NON-NEGOTIABLE)
13. Template and Tooling Consistency (NON-NEGOTIABLE)

TEMPLATES REQUIRING UPDATES:
- ⚠ `.specify/templates/tasks-template.md`: The section on optional tests MUST be removed.
- ⚠ `.specify/templates/plan-template.md`: The reference to `.specify/templates/commands/plan.md` MUST be corrected to `.gemini/commands/speckit.plan.toml`.

FOLLOW-UP ACTIONS:
- Review and update the templates mentioned above to align with the constitution.
-->

# miniRT Project Constitution

## Core Principles

### I. Project Structure Standards (NON-NEGOTIABLE)

All project files MUST follow strict organization rules to maintain clarity between CI automation, user-facing tools, and documentation.

**Script Organization**:
- CI-related scripts MUST be located in `.github/scripts/`.
- User-facing utility scripts MUST remain at the project root for accessibility.

**Documentation Hierarchy**:
- All documentation MUST be centralized in the `docs/` directory, with subdirectories for `spec`, `wiki`, `archive`, etc.
- A `CONTRIBUTING.md` file at the root MUST define the process for contribution, referencing this constitution.

**File Lifecycle Management**:
- Deprecated files MUST be archived, not left scattered.
- Logs and build artifacts MUST be defined in `.gitignore`.

**Rationale**: A clear and consistent project structure prevents confusion, improves maintainability, and ensures contributors can quickly locate resources and understand project conventions.

### II. Code Quality Automation (NON-NEGOTIABLE)

All code changes MUST pass automated quality gates before being merged.

**Mandatory Quality Gates**:
- **Linting**: Code MUST pass a static linter (`norminette` for 42 school context, or a standard linter for general projects) with zero errors.
- **Formatting**: Code MUST adhere to a defined style enforced by an auto-formatter (e.g., `clang-format`). A configuration file MUST be present at the repository root.
- **Build**: The project MUST build without errors on all supported platforms.
- **Memory Safety**: For C/C++, automated checks (e.g., `valgrind`) MUST detect no memory leaks.

**CI Enforcement**:
- Any failure in the quality gates MUST fail the CI pipeline and block PR merging.
- CI logs MUST provide clear, actionable error messages.

**Rationale**: Automating quality control ensures consistency, prevents regressions, and maintains project stability, allowing developers to focus on functionality.

### III. Documentation and Wiki Synchronization (NON-NEGOTIABLE)

The GitHub Wiki MUST be automatically synchronized with source documentation in the `docs/` directory to ensure users always have access to up-to-date information.

**Automation Requirements**:
- Version tag creation MUST trigger an automatic GitHub Wiki update.
- The `docs/` directory is the single source of truth.

**Release Synchronization**:
- The Wiki MUST always reflect the documentation corresponding to the latest release tag.
- Release notes MUST be generated and published as part of the release workflow.

**Rationale**: Automatic synchronization eliminates documentation drift, reduces maintenance burden, and ensures the public-facing documentation is always accurate and tied to a specific software version.

### IV. Workflow System (NON-NEGOTIABLE)

Development MUST follow the structured branching strategy and workflow defined in this constitution.

**Pull Request (PR) Workflow**:
- All changes MUST be introduced through a PR. Direct pushes to the `main` branch are forbidden.
- A PR MUST pass all automated checks (CI, quality, security) before it can be considered for merging.
- A PR MUST be reviewed and approved by at least one other contributor.
- A PR title and description MUST clearly describe the "what" and "why" of the change.

**Release Workflow**:
- Releases MUST be created from the `main` branch.
- Version tags MUST follow Semantic Versioning (vX.Y.Z).
- The release process MUST trigger: Wiki auto-updates, generation of release notes, and publishing of build artifacts.

**Rationale**: A structured workflow ensures that every change is peer-reviewed, automatically tested, and properly documented, leading to higher quality and more stable releases.

### V. Tools and Environment Standards (NON-NEGOTIABLE)

Development environment and tooling MUST support multiple platforms and provide automated dependency management.

**Platform Support**:
- The project MUST support Linux and macOS. The build system MUST handle platform differences automatically.

**Dependency Management**:
- All external dependencies MUST be explicitly documented with their version and license.
- Adding or updating a dependency requires a PR and MUST be evaluated for license compatibility and security vulnerabilities.
- The build system (e.g., `Makefile`) MUST automate the fetching and building of required dependencies like MiniLibX.

**Build & Test Infrastructure**:
- Test artifacts (scenes, data) MUST be organized in the `tests/` directory.
- Build and log artifacts MUST be stored in directories (`build/`, `logs/`) excluded by `.gitignore`.

**Rationale**: Standardized tooling and automated dependency management reduce setup friction for new contributors and ensure a consistent and reproducible build process across all environments.

### VI. Bilingual Specification Management (NON-NEGOTIABLE)

All feature specifications MUST be maintained in both English and Korean to ensure clarity for all contributors and stakeholders.

**Synchronization Requirements**:
- English specifications and their Korean translations MUST be updated in the same commit/PR to prevent drift.
- The directory structure MUST be `specs/[feature-name]/[lang]/spec.md` (e.g., `specs/new-light/en/spec.md`, `specs/new-light/kr/spec.md`).
- CI checks SHOULD verify that a change in one language has a corresponding update in the other.

**Rationale**: Bilingual documentation ensures accessibility and clarity for a diverse team, supporting both the local 42 School community and broader international open-source contributors.

### VII. 42 School Function Constraints (OPTIONAL)

For compatibility with 42 School's curriculum, this project can be built in a "strict" mode that adheres to specific constraints. This section is OPTIONAL for projects outside the 42 ecosystem.

**Allowed Functions (Strict Mode)**:
- Standard C library functions (`open`, `read`, `write`, `malloc`, `free`, `exit`, etc.).
- Math library (`math.h`).
- Provided `MiniLibX` functions.
- Student-implemented `libft` and `get_next_line`.

**Prohibited Functions and Techniques (Strict Mode)**:
- NO `pthreads`, `fork`, or other forms of multithreading/multiprocessing.
- NO external libraries for optimization (e.g., OpenMP, SIMD intrinsics).

**Rationale**: These constraints are for educational purposes to ensure fair evaluation within the 42 School system. When disabled, the project can leverage more advanced, real-world techniques. A build flag (e.g., `make STRICT=1`) SHOULD control this mode.

### VIII. Security Standards (NON-NEGOTIABLE)

The project MUST integrate security best practices into the development lifecycle.

**Automated Security Gates**:
- **SAST (Static Application Security Testing)**: The CI pipeline MUST include a SAST tool to scan the source code for potential vulnerabilities on every PR.
- **Dependency Scanning**: The CI pipeline MUST scan all external dependencies for known vulnerabilities (e.g., using `trivy` or GitHub's Dependabot).
- High or Critical severity vulnerabilities MUST fail the build and block merging.

**Secure Coding Practices**:
- Sensitive information (keys, passwords) MUST NOT be hardcoded. Use environment variables or a secure secret management system.
- Input validation MUST be performed to prevent vulnerabilities like buffer overflows.

**Rationale**: Proactively identifying and mitigating security vulnerabilities is critical for building trustworthy and robust software. Automation ensures security is a consistent part of the process, not an afterthought.

### IX. Branching Strategy (NON-NEGOTIABLE)

The project MUST follow the **GitHub Flow** branching model to ensure a clean and simple workflow.

**Branching Model**:
- `main`: This branch is the source of truth and MUST always be deployable/releasable. Direct pushes are forbidden.
- **Feature Branches**: All new work (features, bugfixes) MUST be done on a descriptive feature branch created from `main` (e.g., `feat/add-new-object`, `fix/memory-leak-on-exit`).
- **Merging**: Feature branches are merged into `main` via a Pull Request (PR) after passing all required checks and reviews. Branches SHOULD be deleted after merging.

**Rationale**: GitHub Flow is a simple and effective model that promotes frequent integration and delivery by ensuring the main branch is always in a good state.

### X. Commit Message Convention (NON-NEGOTIABLE)

All commit messages MUST follow the **Conventional Commits** specification to create an explicit and easily readable project history.

**Format**:
`<type>(<scope>): <subject>`
- **type**: `feat` (new feature), `fix` (bug fix), `docs`, `style`, `refactor`, `test`, `chore`, etc.
- **scope** (optional): The part of the codebase affected (e.g., `parser`, `rendering`).
- **subject**: A concise description of the change.

**Automation**:
- A CI check MUST validate that PR titles or commit messages adhere to this format. This enables automatic generation of changelogs and simplifies versioning.

**Rationale**: A standardized commit history is machine-readable and improves communication among developers, making it easier to understand changes and automate release notes.

### XI. Test Strategy and Coverage (NON-NEGOTIABLE)

The project MUST maintain a comprehensive suite of automated tests to ensure correctness and prevent regressions.

**Test Types**:
- **Unit Tests**: Test individual functions or components in isolation. MUST be fast and form the majority of tests.
- **Integration Tests**: Test the interaction between multiple components. (e.g., parsing a scene file and verifying the data structure).
- **End-to-End (E2E) Tests**: Test the entire application from input to output (e.g., running `miniRT scenes/test.rt` and comparing the output image to a reference image).

**Test Coverage**:
- Automated test coverage reporting MUST be part of the CI pipeline.
- A minimum code coverage target (e.g., 80%) MUST be enforced. PRs that decrease coverage below the threshold SHOULD be blocked.

**Note on Templates**: The `tasks-template.md` must be interpreted in light of this principle. The "optional" nature of tests in the template is for phasing work (i.e., writing tests first), not for omitting them entirely. All new functionality requires tests.

**Rationale**: A multi-layered testing strategy provides confidence in code changes, catches bugs early, and makes refactoring safer. Enforcing a coverage target ensures that the test suite grows with the codebase.

### XII. Deprecation Policy (NON-NEGOTIABLE)

Features, functions, or APIs MUST be deprecated gracefully to avoid breaking changes for users or other parts of the system.

**Deprecation Process**:
1.  **Announcement**: Mark the feature as deprecated in the code (e.g., with comments and compiler warnings if possible) and announce it in the release notes. The announcement MUST state the reason for deprecation and provide an alternative.
2.  **Waiting Period**: The deprecated feature MUST remain functional for at least one MAJOR release cycle to give users time to migrate.
3.  **Removal**: After the waiting period, the deprecated code can be removed in a new MAJOR version.

**Rationale**: A clear deprecation policy provides stability and predictability, allowing consumers of the project to adapt to changes in a timely and managed way.

### XIII. Template and Tooling Consistency (NON-NEGOTIABLE)

All project templates, scripts, and tooling configurations MUST remain consistent with the principles defined in this constitution.

**Review Process**:
- Any change to the constitution MUST trigger a review of all files in `.specify/templates/`, `.specify/scripts/`, and `.gemini/commands/`.
- Inconsistencies MUST be resolved in the same PR that updates the constitution, or be explicitly documented as a follow-up action in the Sync Impact Report.

**Rationale**: This principle ensures that the project's scaffolding and automation do not diverge from its core principles, preventing confusion and ensuring that the constitution is the single source of truth.

## Governance

This constitution defines the non-negotiable principles for the miniRT project. All development activity MUST comply with them.

**Amendment Process**:
- Changes to this constitution require a PR, must include a documented rationale in the sync impact report, and MUST be approved by project maintainers.
- Versioning: MAJOR (incompatible changes), MINOR (new principles), PATCH (clarifications).

**Compliance Enforcement**:
- CI/CD automation MUST enforce all NON-NEGOTIABLE principles.
- Code reviews MUST verify compliance. Deviations MUST be rejected.

**Version**: 4.1.0 | **Ratified**: 2025-12-27 | **Last Amended**: 2025-12-27
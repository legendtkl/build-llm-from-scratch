# Claude Code Context: Build LLM from Scratch

## Project Overview
Educational repository for building Large Language Models from scratch. Focuses on understanding core concepts through hands-on implementation of minimal, transparent models.

## Current Status - Feature 002: Tiny LLM Implementation

### Phase Completed: Planning & Design ✅
- **Branch**: `002-build-a-tiny`
- **Objective**: Build minimal transformer-based LLM for educational purposes
- **Status**: Planning complete, ready for task generation and implementation

### Technical Stack
- **Language**: Python 3.8+
- **Package Management**: uv (modern Python dependency management)
- **Primary Dependencies**: NumPy, PyTorch (with optional pure NumPy version for transparency)
- **Testing**: pytest for unit and integration tests
- **Storage**: Local files for checkpoints and training data
- **Target Platform**: Cross-platform local development

### Architecture Decisions
- **Model Scale**: 2-4 transformer layers, 128-256 hidden dimensions, 4-8 attention heads
- **Vocabulary**: 2000-5000 tokens (configurable)
- **Sequence Length**: 32-128 tokens (64 default)
- **Memory Targets**: <500MB training, <100MB inference
- **Project Structure**: Single educational library with CLI interface

### Generated Artifacts (Phase 1)
```
specs/002-build-a-tiny/
├── spec.md              # Feature specification
├── plan.md              # Implementation plan ✅
├── research.md          # Technical decisions ✅
├── data-model.md        # Core entities and relationships ✅
├── quickstart.md        # Educational walkthrough ✅
└── contracts/           # API specifications ✅
    ├── tokenizer.json   # Tokenization interface
    └── model.json       # Training/inference interface
```

### Key Components Planned
1. **Tokenizer**: Text ↔ Token ID conversion with vocabulary management
2. **Transformer Model**: Minimal implementation with attention visualization
3. **Training Pipeline**: Educational training loop with checkpoint management
4. **CLI Interface**: Command-line tools for training, inference, and experimentation
5. **Visualization**: Attention pattern visualization for educational insight

### Implementation Progress (Phase 3.1 Complete)
- **Tasks Generated**: 44 tasks in phases from setup to polish
- **Setup Complete**: ✅ T001-T003 (project structure, uv config, linting)
- **Current Status**: Ready for Phase 3.2 - TDD test implementation
- **Next Critical**: T004-T011 contract and integration tests MUST fail first

### Constitutional Compliance ✅
- Library-first architecture with clear interfaces
- CLI-based interaction for educational transparency
- Test-driven development approach
- Simple, understandable implementation prioritized

### For Team Handoff
✅ **Setup Complete**: Project structure, dependencies, and linting configured
📋 **Next Phase**: T004-T011 TDD tests (contract & integration tests MUST fail first)
📁 **Current Structure**: 
```
src/tiny_llm/         # Main package
├── models/           # Entity models (T012-T018)
├── services/         # Core services (T019-T025) 
├── cli/             # CLI commands (T026-T029)
└── utils/           # Utilities (T032-T033)
tests/               # Test structure ready
├── contract/        # API contract tests (T004-T008)
├── integration/     # Flow tests (T009-T011)
├── unit/           # Unit tests (T036-T039)
└── performance/    # Benchmarks (T042)
```
⚠️ **Critical**: Follow TDD strictly - all tests in T004-T011 must be written and failing before T012+ implementation begins.

---

## Development Guidelines
- **Test-First**: Write tests before implementation (TDD)
- **Educational Focus**: Prioritize understanding over optimization
- **uv Usage**: Use `uv run` for all Python commands
- **Documentation**: Keep implementations well-commented for learning
- **Incremental**: Build components separately, then integrate

## Recent Changes
- ✅ **Task Generation**: Created 44-task implementation roadmap (T001-T044)
- ✅ **Project Setup**: Implemented T001-T003 setup tasks
  - Created directory structure: src/tiny_llm/, tests/, data/, models/
  - Configured pyproject.toml with torch, numpy, pytest dependencies
  - Set up ruff linting and black formatting tools
- 📋 **Ready for TDD Phase**: T004-T011 contract/integration tests next
- 🎯 **Implementation Strategy**: Following strict TDD - tests must fail before code

## Implementation Status
- [x] Feature specification (FR-001 to FR-011)
- [x] Technical research and decisions
- [x] Data model design
- [x] API contract definitions
- [x] Educational documentation
- [x] Task generation (44 tasks created)
- [x] **Phase 3.1 Setup** (T001-T003 completed)
- [ ] **Phase 3.2 Tests First** (T004-T011 next - TDD critical)
- [ ] Phase 3.3 Core Implementation (T012-T029)
- [ ] Phase 3.4 Integration (T030-T035)
- [ ] Phase 3.5 Polish (T036-T044)
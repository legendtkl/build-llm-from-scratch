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

### Ready for Next Phase
- **Next Command**: `/tasks` to generate implementation task list
- **Implementation Approach**: TDD with tests before code
- **Focus**: Educational clarity over performance optimization

### Constitutional Compliance ✅
- Library-first architecture with clear interfaces
- CLI-based interaction for educational transparency
- Test-driven development approach
- Simple, understandable implementation prioritized

### For Team Handoff
This feature implements a complete but minimal LLM for educational purposes. All technical decisions are documented in `research.md`. The design phase is complete with clear contracts and quickstart guide. Next developer can run `/tasks` to get implementation roadmap.

---

## Development Guidelines
- **Test-First**: Write tests before implementation (TDD)
- **Educational Focus**: Prioritize understanding over optimization
- **uv Usage**: Use `uv run` for all Python commands
- **Documentation**: Keep implementations well-commented for learning
- **Incremental**: Build components separately, then integrate

## Recent Changes
- Added uv package management to technical stack
- Completed research phase with framework and architecture decisions
- Generated data model with core LLM entities (Token, Embedding, Sequence, etc.)
- Created API contracts for tokenizer and model interfaces
- Wrote comprehensive quickstart guide for educational use

## Implementation Status
- [x] Feature specification (FR-001 to FR-011)
- [x] Technical research and decisions
- [x] Data model design
- [x] API contract definitions
- [x] Educational documentation
- [ ] Task generation (next: `/tasks` command)
- [ ] Implementation execution
- [ ] Testing and validation
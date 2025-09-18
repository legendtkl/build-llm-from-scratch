# Tasks: Tiny LLM from Scratch for Study

**Input**: Design documents from `/specs/002-build-a-tiny/`
**Prerequisites**: plan.md (✓), research.md (✓), data-model.md (✓), contracts/ (✓)

## Execution Flow (main)
```
1. Load plan.md from feature directory ✓
   → Extract: Python 3.8+, PyTorch, uv, pytest, CLI interface
2. Load optional design documents: ✓
   → data-model.md: 7 entities → model tasks
   → contracts/: tokenizer.json, model.json → contract test tasks
   → research.md: Framework/architecture decisions → setup tasks
3. Generate tasks by category: ✓
   → Setup: uv project, dependencies, linting
   → Tests: contract tests, integration tests  
   → Core: models, tokenizer, transformer, CLI
   → Integration: training pipeline, persistence
   → Polish: unit tests, visualization, docs
4. Apply task rules: ✓
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...) ✓
6. Generate dependency graph ✓
7. Create parallel execution examples ✓
8. Validate task completeness: ✓
   → All contracts have tests ✓
   → All entities have models ✓
   → All CLI commands implemented ✓
9. Return: SUCCESS (tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions
- **Single project**: `src/`, `tests/` at repository root (per plan.md structure)

## Phase 3.1: Setup
- [ ] T001 Create project structure with src/, tests/, data/, models/ directories
- [ ] T002 Initialize Python project with uv and pyproject.toml dependencies (torch, numpy, pytest)
- [ ] T003 [P] Configure ruff linting and black formatting tools in pyproject.toml

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: These tests MUST be written and MUST FAIL before ANY implementation**
- [ ] T004 [P] Contract test tokenize endpoint in tests/contract/test_tokenizer_contract.py
- [ ] T005 [P] Contract test decode endpoint in tests/contract/test_tokenizer_decode_contract.py  
- [ ] T006 [P] Contract test generate endpoint in tests/contract/test_model_generate_contract.py
- [ ] T007 [P] Contract test train endpoint in tests/contract/test_model_train_contract.py
- [ ] T008 [P] Contract test info endpoint in tests/contract/test_model_info_contract.py
- [ ] T009 [P] Integration test text generation flow in tests/integration/test_generation_flow.py
- [ ] T010 [P] Integration test training pipeline in tests/integration/test_training_pipeline.py
- [ ] T011 [P] Integration test model persistence in tests/integration/test_model_persistence.py

## Phase 3.3: Core Implementation (ONLY after tests are failing)
- [ ] T012 [P] Token entity model in src/models/token.py
- [ ] T013 [P] Embedding entity model in src/models/embedding.py
- [ ] T014 [P] Sequence entity model in src/models/sequence.py
- [ ] T015 [P] AttentionWeight entity model in src/models/attention.py
- [ ] T016 [P] ModelConfig entity model in src/models/config.py
- [ ] T017 [P] ModelState entity model in src/models/state.py
- [ ] T018 [P] TrainingData entity model in src/models/training_data.py
- [ ] T019 [P] Tokenizer service in src/services/tokenizer.py (implements tokenize/decode)
- [ ] T020 [P] Vocabulary management service in src/services/vocabulary.py
- [ ] T021 [P] Attention mechanism implementation in src/models/attention_layer.py
- [ ] T022 [P] Transformer layer implementation in src/models/transformer_layer.py
- [ ] T023 Transformer model assembly in src/models/transformer_model.py
- [ ] T024 Training service implementation in src/services/trainer.py
- [ ] T025 Inference service implementation in src/services/generator.py
- [ ] T026 [P] CLI generate command in src/cli/generate.py
- [ ] T027 [P] CLI train command in src/cli/train.py
- [ ] T028 [P] CLI info command in src/cli/info.py
- [ ] T029 Main CLI entry point in src/cli/__main__.py

## Phase 3.4: Integration
- [ ] T030 Model checkpoint saving and loading in src/services/persistence.py
- [ ] T031 Training data preprocessing pipeline in src/services/data_preprocessor.py
- [ ] T032 Attention visualization utilities in src/utils/visualization.py
- [ ] T033 Training metrics logging in src/utils/metrics.py
- [ ] T034 Error handling and validation across services
- [ ] T035 CLI argument validation and help text

## Phase 3.5: Polish
- [ ] T036 [P] Unit tests for tokenizer in tests/unit/test_tokenizer.py
- [ ] T037 [P] Unit tests for attention mechanism in tests/unit/test_attention.py
- [ ] T038 [P] Unit tests for transformer model in tests/unit/test_transformer.py
- [ ] T039 [P] Unit tests for training service in tests/unit/test_trainer.py
- [ ] T040 [P] Memory usage optimization and monitoring
- [ ] T041 [P] Educational documentation in docs/architecture.md
- [ ] T042 [P] Performance benchmarking in tests/performance/test_benchmarks.py
- [ ] T043 Code documentation and type hints
- [ ] T044 Execute quickstart.md validation scenarios

## Dependencies
- Setup (T001-T003) before everything
- Tests (T004-T011) before implementation (T012-T029)
- Models (T012-T018) before services (T019-T025)
- Services before CLI (T026-T029)
- Core implementation before integration (T030-T035)
- Everything before polish (T036-T044)

**Specific blockers**:
- T012-T018 (models) block T019-T025 (services)
- T019 (tokenizer) blocks T026 (CLI generate)
- T024 (trainer) blocks T027 (CLI train)
- T023 (transformer model) blocks T025 (generator) and T024 (trainer)
- T030 (persistence) blocks T027 (CLI train) and T011 (persistence test)

## Parallel Example
```bash
# Launch T004-T011 together (all contract and integration tests):
Task: "Contract test tokenize endpoint in tests/contract/test_tokenizer_contract.py"
Task: "Contract test decode endpoint in tests/contract/test_tokenizer_decode_contract.py"  
Task: "Contract test generate endpoint in tests/contract/test_model_generate_contract.py"
Task: "Integration test text generation flow in tests/integration/test_generation_flow.py"

# Launch T012-T018 together (all entity models):
Task: "Token entity model in src/models/token.py"
Task: "Embedding entity model in src/models/embedding.py"
Task: "Sequence entity model in src/models/sequence.py"
Task: "AttentionWeight entity model in src/models/attention.py"
```

## Educational Focus
- Each task includes clear learning objectives
- Implementation emphasizes transparency over performance
- Visualization and debugging capabilities built-in
- Comprehensive documentation for educational use

## Notes
- [P] tasks = different files, no dependencies
- Verify tests fail before implementing
- Use uv run for all Python commands
- Commit after each task
- Prioritize educational clarity over optimization
- Include attention visualization in generation tasks

## Task Generation Rules
*Applied during main() execution*

1. **From Contracts**:
   - tokenizer.json → T004, T005 (tokenize/decode contract tests)
   - model.json → T006, T007, T008 (generate/train/info contract tests)
   
2. **From Data Model**:
   - 7 entities → T012-T018 (model creation tasks)
   - Relationships → T019-T025 (service layer tasks)
   
3. **From User Stories**:
   - Generation scenarios → T009 (generation flow test)
   - Training scenarios → T010 (training pipeline test)
   - Quickstart scenarios → T044 (validation)

4. **Ordering**:
   - Setup → Tests → Models → Services → CLI → Integration → Polish
   - Dependencies block parallel execution

## Validation Checklist
*GATE: Checked by main() before returning*

- [x] All contracts have corresponding tests (T004-T008)
- [x] All entities have model tasks (T012-T018)
- [x] All tests come before implementation (T004-T011 before T012+)
- [x] Parallel tasks truly independent ([P] tasks use different files)
- [x] Each task specifies exact file path
- [x] No task modifies same file as another [P] task

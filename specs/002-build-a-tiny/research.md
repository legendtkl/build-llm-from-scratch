# Research: Tiny LLM Technical Decisions

## Performance Goals Resolution

**Decision**: Training time target of 5-30 minutes for small models on modest hardware  
**Rationale**: Educational use case prioritizes learning over performance. Quick iteration cycles help experimentation.  
**Alternatives considered**: 
- Ultra-fast training (<1 min): Too limiting for meaningful learning
- Production-scale training (hours): Impractical for educational iteration

## Memory Constraints Resolution

**Decision**: Maximum 500MB RAM usage during training, 100MB during inference  
**Rationale**: Should run on laptops and educational environments without specialized hardware  
**Alternatives considered**:
- No memory limits: Could exclude students with limited hardware
- Very strict limits (<50MB): Would severely limit model complexity and learning value

## Sequence Length Specification

**Decision**: Support sequences of 32-128 tokens with 64 as default  
**Rationale**: Long enough to demonstrate attention patterns, short enough for educational clarity  
**Alternatives considered**:
- Very short (16 tokens): Insufficient for meaningful language patterns
- Long sequences (512+ tokens): Computationally expensive, harder to visualize

## Vocabulary Size Specification

**Decision**: 2000-5000 tokens with configurable size  
**Rationale**: Large enough for basic language modeling, small enough for educational understanding  
**Alternatives considered**:
- Tiny vocabulary (500 tokens): Too limiting for realistic text generation
- Large vocabulary (30k+ tokens): Adds complexity without educational benefit

## Framework Selection

**Decision**: Primary implementation in PyTorch with optional NumPy-only version  
**Rationale**: PyTorch provides automatic differentiation and GPU support while maintaining transparency  
**Alternatives considered**:
- Pure NumPy: Maximum educational transparency but tedious gradient computation
- TensorFlow: More complex API, less intuitive for educational purposes
- JAX: Too advanced for introductory educational material

## Package Management

**Decision**: Use uv for Python project and dependency management  
**Rationale**: uv provides fast, reliable dependency resolution and virtual environment management, following modern Python best practices  
**Alternatives considered**:
- pip + venv: Standard but slower dependency resolution
- poetry: Good dependency management but more complex configuration
- conda: Heavier weight, primarily for data science environments

## Model Architecture Specification

**Decision**: 2-4 transformer layers, 128-256 hidden dimensions, 4-8 attention heads  
**Rationale**: Minimal complexity while demonstrating key transformer concepts  
**Alternatives considered**:
- Single layer: Too simple to show transformer depth benefits
- 6+ layers: Unnecessary complexity for educational demonstration

## Data Format and Storage

**Decision**: Simple text files for training data, JSON for model checkpoints  
**Rationale**: Easy to inspect and understand, no database complexity  
**Alternatives considered**:
- Binary formats: Faster but opaque to students
- Database storage: Overkill for educational use case

## Visualization and Debugging

**Decision**: Built-in attention visualization and training metrics logging  
**Rationale**: Essential for educational understanding of model internals  
**Alternatives considered**:
- No visualization: Misses key educational opportunity
- Complex dashboards: Too much development overhead

## Testing Strategy

**Decision**: Unit tests for components, integration tests for training/inference pipeline  
**Rationale**: Ensures reliability while demonstrating good development practices  
**Alternatives considered**:
- Minimal testing: Bad example for students
- Exhaustive testing: Development overhead outweighs educational benefit
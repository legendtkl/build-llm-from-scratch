# Quickstart: Tiny LLM from Scratch

This guide demonstrates building and using a tiny LLM for educational purposes. Follow these steps to understand core concepts through hands-on implementation.

## Prerequisites

- Python 3.8+
- Basic understanding of neural networks
- 500MB+ available RAM

## Installation

```bash
# Clone the repository
git clone <repository-url>
cd build-llm-from-scratch

# Install dependencies using uv
uv sync

# Activate the virtual environment
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Verify installation
uv run python -m tiny_llm --help
```

## Quick Demo (5 minutes)

### 1. Generate Text with Pre-trained Model

```bash
# Load a pre-trained tiny model and generate text
uv run python -m tiny_llm generate \
  --model models/demo-tiny.pt \
  --prompt "The weather today is" \
  --max-tokens 20

# Expected output:
# "The weather today is beautiful and sunny with clear blue skies overhead"
```

### 2. Inspect Model Internals

```bash
# View model architecture and parameters
uv run python -m tiny_llm info --model models/demo-tiny.pt

# Expected output:
# Vocabulary Size: 2000 tokens
# Hidden Dimension: 128
# Transformer Layers: 2
# Attention Heads: 4
# Parameters: ~50K total
```

### 3. Visualize Attention Patterns

```bash
# Generate text with attention visualization
python -m tiny_llm generate \
  --model models/demo-tiny.pt \
  --prompt "The cat sat on" \
  --visualize-attention \
  --output attention.html

# Open attention.html in browser to see attention heatmaps
```

## Training Your Own Model (20 minutes)

### 1. Prepare Training Data

```bash
# Create a simple training dataset
echo "The quick brown fox jumps over the lazy dog.
A journey of a thousand miles begins with a single step.
To be or not to be, that is the question.
All that glitters is not gold." > data/sample.txt

# Verify data format
python -m tiny_llm data --validate data/sample.txt
```

### 2. Train from Scratch

```bash
# Train a tiny model (takes ~5-10 minutes)
python -m tiny_llm train \
  --data data/sample.txt \
  --vocab-size 500 \
  --hidden-dim 64 \
  --num-layers 2 \
  --num-heads 2 \
  --epochs 50 \
  --output models/my-tiny.pt

# Monitor training progress
# Epoch 1/50: Loss=4.82, Time=0.3s
# Epoch 10/50: Loss=3.45, Time=0.3s  
# Epoch 50/50: Loss=1.23, Time=0.3s
# Training completed! Model saved to models/my-tiny.pt
```

### 3. Test Your Trained Model

```bash
# Generate text with your model
python -m tiny_llm generate \
  --model models/my-tiny.pt \
  --prompt "The quick" \
  --max-tokens 10

# Expected output (will vary):
# "The quick brown fox jumps over the"
```

## Educational Exploration (30+ minutes)

### 1. Compare Model Sizes

```bash
# Train models with different sizes
python -m tiny_llm train --data data/sample.txt --hidden-dim 32 --output models/small.pt
python -m tiny_llm train --data data/sample.txt --hidden-dim 128 --output models/large.pt

# Compare generation quality
python -m tiny_llm generate --model models/small.pt --prompt "The cat"
python -m tiny_llm generate --model models/large.pt --prompt "The cat"
```

### 2. Experiment with Hyperparameters

```bash
# Try different learning rates
python -m tiny_llm train --data data/sample.txt --learning-rate 0.01 --output models/fast.pt
python -m tiny_llm train --data data/sample.txt --learning-rate 0.0001 --output models/slow.pt

# Compare training curves
python -m tiny_llm plot --models models/fast.pt,models/slow.pt --metric loss
```

### 3. Understand Tokenization

```bash
# Explore how text becomes tokens
echo "Hello, world! This is tokenization." | python -m tiny_llm tokenize

# Expected output:
# Text: "Hello, world! This is tokenization."
# Tokens: ["Hello", ",", "world", "!", "This", "is", "tokenization", "."]
# Token IDs: [145, 23, 892, 45, 234, 156, 1847, 67]
```

### 4. Examine Attention Patterns

```bash
# Generate attention visualizations for different prompts
python -m tiny_llm generate --prompt "The dog" --visualize-attention --output dog-attention.html
python -m tiny_llm generate --prompt "Yesterday I" --visualize-attention --output time-attention.html

# Compare how attention focuses on different word relationships
```

## Validation Tests

Run these commands to verify your implementation works correctly:

```bash
# Test 1: Basic generation
result=$(python -m tiny_llm generate --model models/demo-tiny.pt --prompt "test" --max-tokens 5)
echo "✓ Generation test: $result"

# Test 2: Training convergence  
python -m tiny_llm train --data data/sample.txt --epochs 5 --output models/test.pt
echo "✓ Training test completed"

# Test 3: Model persistence
python -m tiny_llm info --model models/test.pt
echo "✓ Model loading test passed"

# Test 4: Tokenization consistency
echo "test text" | python -m tiny_llm tokenize | python -m tiny_llm decode
echo "✓ Tokenization round-trip test passed"
```

## Next Steps

1. **Explore Architecture**: Modify `src/models/transformer.py` to experiment with different architectures
2. **Add Features**: Implement temperature sampling, top-k generation, beam search
3. **Scale Up**: Try larger vocabularies and longer training on real datasets
4. **Compare Models**: Implement different architectures (RNN, CNN) and compare results
5. **Advanced Topics**: Add positional encodings, layer normalization, dropout

## Troubleshooting

### Common Issues

**"Out of memory" error**:
- Reduce `--batch-size` or `--hidden-dim`
- Check available RAM with `free -h`

**Training loss not decreasing**:
- Increase `--learning-rate` or `--epochs`  
- Check training data quality with `--validate`

**Generated text is repetitive**:
- Increase `--temperature` parameter
- Try different `--top-k` values

### Getting Help

```bash
# View all available commands
python -m tiny_llm --help

# Get help for specific commands
python -m tiny_llm train --help
python -m tiny_llm generate --help
```

## Educational Objectives Achieved

After completing this quickstart, you should understand:

- ✅ How text is converted to tokens and back
- ✅ Basic transformer architecture components  
- ✅ Training loop and loss optimization
- ✅ Text generation and sampling strategies
- ✅ Attention mechanism visualization
- ✅ Impact of hyperparameters on model behavior
- ✅ Model persistence and deployment basics

Total time investment: 1-2 hours for comprehensive understanding.
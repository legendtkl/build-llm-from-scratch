# Data Model: Tiny LLM

## Core Entities

### Token
**Purpose**: Basic unit of text processing  
**Fields**:
- `id: int` - Unique identifier for the token
- `text: str` - Original text representation
- `frequency: int` - Occurrence count in training data

**Relationships**: 
- Tokens compose Sequences
- Tokens map to Embeddings

**Validation Rules**:
- Token ID must be non-negative
- Token text cannot be empty
- Frequency must be positive

### Embedding
**Purpose**: Vector representation of tokens capturing semantic relationships  
**Fields**:
- `token_id: int` - Reference to associated token
- `vector: List[float]` - Dense vector representation
- `dimension: int` - Size of embedding vector

**Relationships**:
- One-to-one mapping with Tokens
- Used by Attention mechanisms

**Validation Rules**:
- Vector dimension must match model configuration
- Vector values should be normalized
- Token ID must exist in vocabulary

### Sequence
**Purpose**: Ordered collection of tokens representing input/output text  
**Fields**:
- `tokens: List[int]` - Ordered list of token IDs
- `length: int` - Number of tokens in sequence
- `padding_mask: List[bool]` - Indicates padded positions

**Relationships**:
- Contains multiple Tokens
- Processed by AttentionLayer

**Validation Rules**:
- Sequence length must not exceed maximum (128 tokens)
- All token IDs must exist in vocabulary
- Padding mask length must match token list length

### AttentionWeight
**Purpose**: Numerical values indicating focus on different input positions  
**Fields**:
- `query_position: int` - Position of the query token
- `key_position: int` - Position of the key token  
- `weight: float` - Attention weight value
- `head_id: int` - Which attention head produced this weight

**Relationships**:
- Generated during Sequence processing
- Multiple weights per position pair (multi-head attention)

**Validation Rules**:
- Weight values must be between 0 and 1
- Positions must be within sequence bounds
- Weights for each query position must sum to 1

### ModelState
**Purpose**: Complete set of learned parameters including weights and biases  
**Fields**:
- `parameters: Dict[str, Tensor]` - All model weights and biases
- `config: ModelConfig` - Model architecture configuration
- `training_step: int` - Number of training steps completed
- `vocabulary_size: int` - Size of token vocabulary

**Relationships**:
- Contains parameters for all model components
- Serialized/deserialized for model persistence

**Validation Rules**:
- All required parameters must be present
- Parameter shapes must match configuration
- Training step must be non-negative

### TrainingData
**Purpose**: Text corpus used to teach the model language patterns  
**Fields**:
- `sequences: List[Sequence]` - Training text as token sequences
- `metadata: Dict[str, Any]` - Dataset information
- `total_tokens: int` - Total number of tokens
- `vocabulary: Vocabulary` - Token to ID mapping

**Relationships**:
- Composed of multiple Sequences
- References shared Vocabulary

**Validation Rules**:
- Must contain at least one sequence
- All sequences must use same vocabulary
- Total tokens must match sum of sequence lengths

### ModelConfig
**Purpose**: Architecture and hyperparameter configuration  
**Fields**:
- `vocab_size: int` - Number of tokens in vocabulary
- `hidden_dim: int` - Size of hidden representations
- `num_layers: int` - Number of transformer layers
- `num_heads: int` - Number of attention heads
- `max_seq_len: int` - Maximum sequence length
- `dropout_rate: float` - Dropout probability

**Validation Rules**:
- Hidden dimension must be divisible by number of heads
- All size parameters must be positive
- Dropout rate must be between 0 and 1
- Maximum sequence length must be reasonable (≤ 1024)

## State Transitions

### Training Workflow
1. **Initialize**: ModelState created with random parameters
2. **Load Data**: TrainingData sequences prepared and validated  
3. **Training Loop**: ModelState parameters updated based on TrainingData
4. **Checkpoint**: ModelState periodically saved to disk
5. **Completion**: Final ModelState saved with training metadata

### Inference Workflow  
1. **Load**: ModelState restored from checkpoint
2. **Tokenize**: Input text converted to Sequence
3. **Forward Pass**: Sequence processed to generate AttentionWeights and predictions
4. **Generate**: New tokens predicted and added to Sequence
5. **Decode**: Final Sequence converted back to text

### Model Evolution
- **Training**: Parameters continuously updated via gradient descent
- **Validation**: Model performance evaluated on held-out data
- **Checkpointing**: Model state preserved at regular intervals
- **Fine-tuning**: Pre-trained model adapted to new data
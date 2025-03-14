# The Rise of AI engineering

## What does encoding statistical information mean?

Statistical information refers to **patterns and probabilities** found in language, such as:

- How frequently certain words appear in a language
- Which words commonly appear together
- What words typically follow other words or phrases
- How language structures form in different contexts

---

The model "encodes" these patterns by:

1. **Transforming text data into mathematical representations** (vectors/embeddings)
2. **Storing these patterns in model parameters** (weights in the neural network)
3. **Creating a statistical map** of how language works

## Tokenization in Language Models

### Basic Concepts

- **Tokenization**: Process of breaking original text into tokens
- **GPT-4 token size**: Approximately ¾ the length of a word
- **Conversion rate**: 100 tokens ≈ 75 words

### Vocabulary

- **Definition**: The set of all tokens a model can work with
- **Property**: Small number of tokens can construct large number of distinct words
- **Model comparison**:
  - Mixtral 8x7B: 32,000 token vocabulary
  - GPT-4: 100,256 token vocabulary

### Why Models Use Tokens (Not Words/Characters)

1. **Meaningful components**: Tokens break words into meaningful parts

   - Example: "cooking" → "cook" + "ing" (both parts retain meaning)

2. **Efficiency**: Fewer unique tokens than unique words

   - Reduces model's vocabulary size
   - Makes the model more efficient

3. **Unknown word handling**: Helps process novel words
   - Example: "chatgpt-ing" → "chatgpt" + "ing"
   - Balances having fewer units than words while retaining more meaning than characters

## Types of Language Models

### 1. Autoregressive Language Models

- **Definition**: Trained to predict the next token in a sequence
- **Context used**: Only preceding tokens ("left context")
- **Process**: Generates one token at a time in sequence
- **Example**: For "My favorite color is \_\_\_", predicts what comes next
- **Current status**: Most popular for text generation
- **Note**: In this book, "language model" refers to autoregressive models unless stated otherwise

### 2. Masked Language Models

- **Definition**: Trained to predict missing tokens anywhere in a sequence
- **Context used**: Both before and after the missing tokens (bidirectional)
- **Process**: Fills in blanks using surrounding context
- **Example**: For "My favorite \_\_\_ is blue", predicts "color"
- **Notable example**: BERT (Bidirectional Encoder Representations from Transformers)
- **Common uses**:
  - Non-generative tasks (sentiment analysis, classification)
  - Tasks requiring understanding of overall context
  - Code debugging (understanding both preceding and following code)

## Core Language Model Concepts

### Language Models as Completion Machines

- Given a text prompt, models try to complete that text
- Example: Prompt: "To be or not to be" → Completion: ", that is the question."

### Generative Nature

- Can use finite vocabulary to create infinite possible outputs
- Called "generative" → hence "generative AI"
- Outputs are open-ended

### Probabilistic Prediction

- Completions based on probabilities, not guaranteed to be correct
- This makes them both "exciting and frustrating to use"
- Further explored in Chapter 2

### Applications Beyond Simple Completion

- Translation: "How are you in French is..." → "Comment ça va"
- Classification: "Is this email likely spam?" → "Likely spam"
- Summarization, coding, math problems can all be framed as completion tasks

### Completion vs. Conversation

- Simple completion isn't the same as engaging in conversation
- A completion machine might respond to a question by adding another question
- "Post-Training" discusses making models respond appropriately to user requests

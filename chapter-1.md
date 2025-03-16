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

## What is entropy?

### What Entropy Means in Language Models

Entropy measures the **unpredictability or randomness** in a system. In language modeling:

- **Low entropy** = high predictability (like "The capital of France is \_\_\_" where "Paris" is highly predictable)
- **High entropy** = low predictability (like "My favorite thing is \_\_\_" where many answers are possible)

Mathematically, entropy is the average number of "bits" needed to represent an event drawn from a probability distribution.

### Why It's Still Used Today

We still use entropy (and related concepts) in modern AI for several reasons:

1. **Training objective**: Cross-entropy loss is the standard loss function for training language models

2. **Evaluation metric**: Perplexity (which is derived from entropy - it measures how "confused" or "surprised" the model is when it encounters text) remains a standard way to evaluate how well a model predicts text

3. **Theoretical foundation**: Even as architectures evolved from simple statistical models to complex transformers, the underlying goal remains modeling probability distributions of language - which entropy directly measures

4. **Efficiency measure**: Bits-per-character/token metrics help us compare how efficiently different models compress information

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

## Supervised vs. Self-Supervised Learning

### Supervised Learning

- **Definition**: Training models using data that humans have manually labeled
- **How it works**: Humans examine each example and assign the correct answer/category
- **Examples**:
  - Images labeled as "cat," "dog," etc.
  - Transactions marked as "fraud" or "not fraud"
- **Cost factors**:
  - Paying humans to create labels (~$0.05 per image)
  - Multiple labelers for quality control (doubles/triples cost)
  - Example: $50,000 to label 1 million images for ImageNet
- **Limitations**:
  - Expensive as dataset size grows
  - Cannot scale beyond human labeling capacity
  - Some domains require rare, expensive expertise

### Self-Supervised Learning

- **Definition**: Models learn from patterns in the data itself without human labels
- **How it works**: The data contains its own supervision signal
- **Example**: In "I love street food"
  - Input: "<BOS>, I, love, street" → Output: "food"
  - Each word provides context to predict the next
- **Advantages**:
  - No human labeling costs
  - Can use virtually unlimited data (books, articles, websites)
  - Scales without additional human intervention
- **Key insight**: Text naturally contains its own supervision, unlocking massive scalability

### Why This Distinction Matters

- Self-supervision enabled the "ChatGPT moment" by removing the data labeling bottleneck
- Language models could train on trillions of words instead of millions of labeled examples
- This is why language AI scaled faster than other AI domains

# Planning AI applications

## Things to measure

- Inference cost
- Time to first token, time per output token, total latency
- are users really happy with the output?

## Inference Cost Cheat Sheet

### **What is Inference?**

- **Analogy**: Like a serverless function (e.g., AWS Lambda) running for every API request.
- **What you pay for**:
  - **GPU/CPU time**: How long the AI "thinks" per request.
  - **RAM**: How much memory the model needs (bigger model = more $$$).
  - **Throughput**: Users hitting your AI endpoint at once (scaling costs).

---

### **Key Cost Drivers**

| Factor               | Web Dev Analogy                     | Cost Impact Example                              |
| -------------------- | ----------------------------------- | ------------------------------------------------ |
| **Model Size**       | Next.js vs. Express.js              | GPT-4: $0.03/1k tokens → $150/mo                 |
|                      | (Heavier framework = slower dev)    | Llama 2: $0.0004/1k → $2/mo                      |
| **Hardware**         | Cheap CPU vs. High-end GPU server   | GPU speeds up responses but costs more per hour. |
| **Concurrent Users** | Scaling from 10 to 10k API requests | More users → More GPUs needed → $$$.             |

---

### **Optimization Hacks**

_(Like tuning your Express.js API)_

1. **Cache common responses** (e.g., FAQ answers).
2. **Batch requests** (process 100 user prompts at once).
3. **Use smaller models** (Llama 2 > GPT-4 for simple tasks).
4. **Serverless GPUs** (AWS Lambda for AI → pay per request).

---

### **Real-World Example**

**Scenario**: 10k users, 5 requests/day each (~500 tokens/request):

- **GPT-4**: `10k * 5 * 500 * $0.03 / 1k = $750/mo`
- **Llama 2**: Same usage → `$2/mo`  
  _Why?_ GPT-4 is like a Lamborghini; Llama 2 is a Toyota.

---

### **Red Flags**

- Using GPT-4 for "Hello World" tasks → paying for a race car to drive 5 mph.
- Not monitoring token usage → surprise $10k bill (like Heroku free tier gone viral).

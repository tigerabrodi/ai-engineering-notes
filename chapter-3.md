# Entropy

**What it is**:
Entropy measures how unpredictable text is.

**In plain English**:
High entropy = text is surprising and unpredictable
Low entropy = text is predictable and follows patterns

**Example**:
Technical documentation has higher entropy than common phrases like "how are you"

**Why it matters to you**:
When building AI apps, high-entropy content (like specialized jargon) will be harder for AI models to handle correctly.

**Practical application**:
If you're building an app for a specialized field (like medicine or law), expect the content to have higher entropy, which means general models might struggle more.

# Cross Entropy

**What it is**:
Cross entropy measures how well an AI model predicts actual text.

**In plain English**:
It shows how many bits the model needs to represent the actual text. Lower numbers are better.

**Example**:
If GPT-4 has a cross entropy of 2.3 for your test data, and another model has 3.1, GPT-4 is making better predictions.

**Why it matters to you**:
This is your primary metric for comparing model performance. Lower cross entropy = better model.

**Practical application**:
When testing different models on your application's content, compare their cross entropy scores to pick the best one.

# Perplexity

**What it is**:
Perplexity is just 2 raised to the power of cross entropy - a more intuitive way to view the same information.

**In plain English**:
Perplexity of 10 means the model is effectively "choosing" between 10 equally likely options at each step.

**Example**:
A good general model might have perplexity of 20 on everyday text, but 100+ on highly technical content.

**Why it matters to you**:
Lower perplexity = better model. It's easier to interpret than cross entropy.

**Practical application**:

- For general conversational AI: Look for perplexity under 30
- For specialized domains: You might need fine-tuning if perplexity is over 100

# Practical Tips for Work as a fullstack dev

**For model selection**:

- Test multiple models on your specific content
- Compare their perplexity scores (lower is better)
- Consider if the performance difference justifies cost differences

**For content preparation**:

- If your content has high entropy (specialized, technical), consider fine-tuning
- Provide more context in prompts for high-entropy topics

**For monitoring**:

- Track perplexity of your model responses over time
- A sudden increase might indicate your content has changed or the model is failing

**For implementation**:

- You don't need to calculate these metrics yourself
- Most AI platforms and evaluation tools calculate them automatically
- Focus on using these metrics to make decisions, not implementing them

# Entropy vs. Cross Entropy - The Key Difference

**Entropy:**

- Measures the unpredictability of the text itself
- Is a property of the content alone
- Doesn't involve any AI model
- Higher entropy = more unpredictable text

**Cross Entropy:**

- Measures how well a specific AI model predicts the text
- Involves both the text AND the model
- Is used to evaluate model performance
- Higher cross entropy = worse model predictions

Think of it this way:

- Entropy is like measuring how complex a puzzle is
- Cross entropy is measuring how good someone is at solving that puzzle

# Why They Share the Name

They share the word "entropy" because they're related concepts from information theory. Cross entropy builds on entropy - it's essentially measuring how much additional uncertainty (or "entropy") is added when using an imperfect model's predictions instead of the true probabilities.

When you're building AI applications, you'll mostly care about cross entropy and perplexity since they tell you about model performance. Entropy is more about understanding the inherent complexity of your text data.

# Exact evaluation

## Functional correctness

Functional correctness is one of the most straightforward evaluation approaches. It essentially asks: "Did the model do exactly what it was supposed to do?"

For example:

- If you asked a model to generate Python code to sort a list, does the code actually run and correctly sort the list?
- If you asked a model to extract specific data points from text, did it extract all the correct values?
- If you asked for a summary containing 5 key points, did it actually include all 5 required points?

The benefit of functional correctness evaluation is that it's binary and objective - the output either meets the specified requirements or it doesn't. This makes it particularly useful for tasks with clear right/wrong answers.

This type of evaluation is crucial for AI engineering because it helps you:

1. Compare different models objectively
2. Track improvements over time
3. Set quality thresholds for production systems
4. Identify specific failure modes to address

# Similarity Measurements

## 1. Exact Match

**What it is:** The strictest form of comparison where the model output must match the reference precisely.

**When to use:**

- Tasks with only one correct answer (math, specific data extraction)
- When format and accuracy are critical (code generation, database queries)

**Pros:** Simple to implement, unambiguous results  
**Cons:** Inflexible - slight variations count as failures

## 2. Lexical Similarity

**What it is:** Measures word/character overlap between model output and reference.

**Key metrics:**

- **BLEU:** Measures n-gram precision (how many n-grams in the output appear in the reference)
- **ROUGE:** Measures n-gram recall (how many n-grams in the reference appear in the output)
- **F1 Score:** Balances precision and recall for overall accuracy
  - **Precision:** Of all items the model identified as correct, how many were actually correct?
  - **Recall:** Of all the actually correct items, how many did the model identify?

**N-grams explained:** Continuous sequences of n words or characters

- 1-grams (unigrams): Individual words ("The", "quick", "brown", "fox")
- 2-grams (bigrams): Word pairs ("The quick", "quick brown", "brown fox")

**Edit distance approaches:**

- Levenshtein Distance: Counts minimum edits (insertions, deletions, substitutions) needed
- Jaro-Winkler: Gives higher scores to strings that match from the beginning

**When to use:**

- Translation, summarization, text generation where wording patterns matter
- When word choice and structure are important

## 3. Semantic Similarity

**What it is:** Measures similarity of meaning, regardless of specific words used.

**How it works:**

1. Convert texts to embeddings (numerical vectors representing meaning)
2. Calculate distance between vectors in multi-dimensional space

**Distance metrics:**

- **Cosine Similarity:** Measures the angle between vectors
  - Range: -1 to 1 (1 = identical meaning)
  - Focuses on direction of meaning, not length of text
  - Most common for text comparison
- **Euclidean Distance:** Straight-line distance between points
- **Dot Product:** Multiplication of corresponding values

**When to use:**

- Question answering, paraphrasing, content recommendation
- When meaning matters more than exact wording
- When responses could be correctly phrased in multiple ways

## Key Differences Summarized

- **Exact match** asks: "Are these identical?"
- **Lexical similarity** asks: "How many words/phrases do these share?"
- **Semantic similarity** asks: "Do these mean the same thing?"

## Practical Applications

Choose your evaluation method based on your requirements:

- For code generation → Exact match or strict lexical similarity
- For creative writing → Semantic similarity
- For factual responses → Combination of lexical and semantic methods

The more flexible the expected response format, the more you should lean toward semantic similarity for evaluation.

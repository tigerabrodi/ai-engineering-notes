# Evaluation-Driven Development

Evaluation-driven development is the AI equivalent of test-driven development. It involves:

1. **Defining clear evaluation criteria** before building AI solutions
2. **Measuring performance consistently** throughout development
3. **Making data-driven decisions** about model selection and optimizations

## Key Components:

- **Domain-specific capability evaluation**: How well does the model perform for your specific use case?
- **Generation capability evaluation**: Quality, relevance, and coherence of outputs
- **Instruction-following capability**: How well does the model follow complex directions?
- **Cost and latency considerations**: Performance tradeoffs for production systems

## Implementation Process:

1. Evaluate all components in a system separately
2. Create clear evaluation guidelines
3. Define appropriate evaluation methods and test datasets
4. Use results to drive further development decisions

# Common NLP Tasks

## Core Tasks Mentioned in Book:

1. **Intent Classification**: Determining what a user is trying to accomplish

   - Example: "Book me a flight" → Intent: flight_booking
   - Use cases: Chatbots, virtual assistants, customer service automation

2. **Sentiment Analysis**: Determining emotional tone of text

   - Example: "I love this product!" → Positive sentiment
   - Use cases: Brand monitoring, customer feedback analysis, social listening

3. **Next Action Prediction**: Predicting what a user might want to do next
   - Example: After viewing product details → Likely to add to cart or check reviews
   - Use cases: Recommendation systems, UX optimization, customer journey mapping

## Additional NLP Tasks (the "etc"):

4. **Named Entity Recognition (NER)**: Identifying people, places, organizations in text

   - Example: "John works at Microsoft in Seattle" → Person, Organization, Location
   - Use cases: Information extraction, knowledge graphs, content categorization

5. **Text Summarization**: Creating concise summaries of longer documents

   - Use cases: News digests, research paper summaries, content curation

6. **Question Answering**: Extracting specific answers from source material

   - Use cases: Customer support, knowledge bases, research assistants

7. **Text Classification**: Categorizing text into predefined categories

   - Use cases: Content moderation, spam detection, topic sorting

8. **Machine Translation**: Converting text between languages

   - Use cases: Localization, international communication, content accessibility

9. **Semantic Similarity**: Measuring how similar two texts are in meaning

   - Use cases: Search relevance, duplicate detection, content recommendation

10. **Topic Modeling**: Identifying main topics in document collections
    - Use cases: Content organization, trend analysis, knowledge management

# Domain specific assessment

For assessing domain-specific knowledge, multiple-choice quizzes can be effective because they test factual knowledge in a controlled way. Here's how you might approach evaluating domain-specific knowledge:

1. **Multiple-choice questions**: Create questions with one correct answer and several plausible but incorrect options. This forces the model to demonstrate precise knowledge rather than generating plausible-sounding but incorrect information.

2. **Knowledge retrieval tests**: Prepare questions that require specific facts (e.g., "What is the boiling point of water at sea level?") and check if answers match verified information.

3. **Domain-specific problem solving**: For technical domains like programming or medicine, present problems that require applying domain knowledge correctly.

4. **Concept relationship mapping**: Test if the model understands relationships between concepts in your domain (e.g., "Is TypeScript a superset of JavaScript?").

5. **Terminology accuracy**: Create a glossary of domain-specific terms and test if the model uses them correctly in context.

6. **Error identification**: Present statements with subtle domain-specific errors and see if the model can identify them.

The key insight is that domain knowledge is best evaluated with questions that have clear right and wrong answers. This differs from evaluating generative capabilities, where you're looking at qualities like coherence, relevance, and creativity in open-ended responses.

For domain-specific evaluation, you'll also want to:

- Separate facts from reasoning (test each independently)
- Ensure questions cover both breadth and depth in your domain
- Include edge cases and common misconceptions
- Compare performance against domain experts or other reference benchmarks

# Generation capability evaluation

Measuring generation capability is one of the more nuanced aspects of AI evaluation. Here's how you typically approach it:

**Core Aspects of Generation Capability Assessment:**

1. **Quality Dimensions**

   - **Coherence**: Does the text flow logically from beginning to end?
   - **Relevance**: Does the generation address the prompt or query appropriately?
   - **Fluency**: Is the language natural, grammatically correct, and well-formed?
   - **Diversity**: Does the model generate varied outputs rather than repetitive content?
   - **Creativity**: For creative tasks, does the model produce novel, interesting content?

2. **Evaluation Methods**

   - **Human Evaluation**: The gold standard but expensive and difficult to scale

     - Often uses Likert scales (1-5 ratings) across different quality dimensions
     - Can employ A/B testing between different models

   - **Automated Metrics**:

     - **BLEU/ROUGE**: Measures overlap with reference text (limited for creative generation)
     - **Perplexity**: How "surprised" is the model by human-written text (lower is better)
     - **BERTScore/MoverScore**: Semantic similarity metrics that go beyond exact word matches

   - **AI-judge based evaluation**:
     - Using another AI to evaluate generations based on specific criteria
     - Requires careful prompt engineering to ensure consistency

3. **Task-Specific Evaluation**

   - **Story Generation**: Plot consistency, character development, engagement
   - **Code Generation**: Correctness, efficiency, readability
   - **Technical Writing**: Accuracy, completeness, clarity
   - **Dialogue**: Naturalness, helpfulness, appropriateness

4. **Specialized Tests**
   - **Adversarial Prompts**: Does the model generate appropriately even for tricky inputs?
   - **Edge Cases**: Testing model capabilities at the boundaries (very long outputs, complex tasks)
   - **Consistency Checks**: Evaluating whether the model contradicts itself across a session

The best approach is usually a combination of methods. You might:

1. Use automated metrics for quick, scalable feedback during development
2. Employ AI judges for intermediate evaluation of larger test sets
3. Conduct human evaluation for final verification of important capabilities

There's no perfect single metric for generation capability, which is why most serious AI engineering teams develop custom evaluation frameworks specific to their use cases.

# Cost and latency considerations

**Cost Considerations for AI as Judge**

- Using large, powerful models as judges (like GPT-4 or Claude Opus) can be expensive, especially when evaluating thousands of outputs
- There's a tradeoff between judge quality and cost
- Smaller models may be sufficient for straightforward evaluation tasks
- You might use tiered evaluation: screen with cheaper models first, then use premium models only for edge cases

**Latency Considerations**

- Judge models add additional inference time to your pipeline
- This impacts both development cycles (slower feedback loops) and production systems
- Faster, smaller models might be preferable for real-time applications
- Batch evaluation can be more efficient for development and testing phases

**Evaluation Criteria for AI Judges**

1. **Reliability**:

   - How consistent is the judge across similar evaluations?
   - Does it avoid biases toward certain response patterns?

2. **Discriminative Power**:

   - Can it distinguish between subtle differences in quality?
   - Does it provide meaningful differentiation or just binary judgments?

3. **Alignment with Human Judgment**:

   - Do the judge's evaluations correlate with human evaluations?
   - This often requires calibration against human-rated examples

4. **Interpretability**:

   - Does the judge provide explanations for its ratings?
   - Can you understand why certain outputs received specific scores?

5. **Domain Specificity**:
   - Is the judge model knowledgeable in your specific domain?
   - General-purpose judges might miss domain-specific nuances

There's also an interesting meta-evaluation challenge: "Who judges the judges?" One approach is to periodically validate the AI judge against human evaluations to ensure it remains calibrated and useful.

For practical implementation, you'll typically need to:

- Create clear rubrics for the judge to follow
- Design prompts that elicit consistent evaluations
- Set up a system to aggregate and analyze judge ratings
- Regularly validate the judge against human evaluations

# Model selection

1. **Filter by Hard Attributes**

   - This initial screening focuses on non-negotiable requirements:
   - Context length: Does the model support your required input length?
   - Licensing: Can you use it for your intended application?
   - Deployment options: On-prem vs. cloud API requirements
   - Pricing: Is it within your budget constraints?
   - This step quickly eliminates models that simply won't work for your use case.

2. **Public Model Evaluation**

   - Review existing benchmark results (like MMLU, HumanEval, or domain-specific benchmarks)
   - Compare models on leaderboards like LMSYS Arena or Hugging Face Open LLM Leaderboard
   - Analyze published performance data from model creators
   - This gives you a general sense of relative model capabilities without investing in custom testing.

3. **Task-Specific Evaluation**

   - Create a test set specifically for your application's requirements
   - Define clear evaluation criteria aligned with your success metrics
   - Run controlled tests across your shortlisted models
   - This is where you really determine which model performs best for your specific needs.

4. **Online Evaluation**
   - Test promising models in real-world conditions with actual users
   - Implement A/B testing to compare model performance
   - Gather user feedback and behavioral metrics
   - This final validation ensures the model works as expected in production conditions.

This iterative approach is efficient because you start with broad filters that are easy to apply and progressively narrow down your options with increasingly specific and resource-intensive evaluation methods. It helps you avoid wasting time on detailed evaluations of models that wouldn't meet your basic requirements anyway.

# Designing your evaluation pipeline

## Step 1: Evaluating All Components

The author distinguishes between two types of system evaluation:

- **Turn-based evaluation**: Assesses individual interactions or responses. This is useful for conversational AI or single-query systems where each response is independent.

- **Task-based evaluation**: Evaluates the entire sequence of interactions needed to complete a task. This is critical for agent-based systems or multi-step processes where success depends on the cumulative performance across turns.

This distinction is important because you might have a system that gives good individual responses but fails to solve the overall task effectively. By evaluating both levels, you get a more complete picture of system performance.

## Step 2: Creating Evaluation Guidelines

This step involves establishing clear standards for what constitutes good and bad responses:

- **Defining evaluation criteria**: For a customer support AI, criteria like relevance, factual consistency, and safety make sense. Other applications might prioritize creativity, problem-solving ability, or code correctness.

- **Creating scoring rubrics**: These provide concrete examples of what constitutes a 1/5 vs 5/5 response for each criterion. This makes evaluation more consistent and less subjective.

- **Understanding business impact thresholds**: The author's point about percentage improvements having non-linear business impacts is crucial. Moving from 90% to 97% factual accuracy might seem incremental but could be the difference between requiring human supervision and full automation.

The business impact analysis helps you:

1. Set appropriate performance targets
2. Allocate resources more effectively (where improvement matters most)
3. Make better decisions about when a model is "good enough" for deployment
4. Plan development milestones that align with business outcomes

For example, if you discover that hitting 95% on a particular metric allows you to automate a process entirely, that becomes a clear target rather than endlessly pursuing marginal improvements.

## Step 3: Selection evaluation methods and data

**Logprobs (Log Probabilities)**
These are numerical values that show how confident a model is in each token (word/character) it generates. Higher logprobs mean higher confidence. They're useful because:

- You can identify when a model is uncertain
- They help detect potential hallucinations (model tends to be less confident when making things up)
- They provide quantitative data for evaluation without needing external judges

**Annotation**
Annotation means adding labels, scores, or metadata to your evaluation data. For example:

- Marking responses as "correct" or "incorrect"
- Rating responses on a scale (1-5) for different criteria
- Adding notes about why something succeeded or failed
- Categorizing errors by type

Annotated evaluation data gives you a gold standard to compare model outputs against. You might create this by having experts label a set of example inputs and ideal outputs.

**Evaluating the Evaluation Pipeline**
The author makes a great point that your evaluation system itself needs assessment:

1. **Reliability**: Do you get consistent results when running the same evaluation multiple times?

2. **Signal quality**: Is your evaluation actually measuring what matters for your application?

3. **Redundancy**: If two metrics are highly correlated (they always move together), you might only need one of them.

4. **Cost-benefit analysis**: Evaluation adds overhead in terms of:

   - Computation costs
   - Latency (especially important for real-time applications)
   - Development time

5. **Iterative improvement**: Your evaluation system should evolve as you learn more about:
   - Which metrics best predict user satisfaction
   - Where models typically fail in your domain
   - New evaluation techniques that become available

The key insight is that evaluation isn't just something you do once at the beginning - it's an ongoing process that includes both:

- Pre-deployment testing with controlled data
- Production monitoring with real user interactions

Good experiment tracking ensures you can compare results over time and understand if your changes are actually improvements.

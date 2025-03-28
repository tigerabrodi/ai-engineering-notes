# Modeling

## Seq2Seq (Sequence-to-Sequence)

Seq2Seq models were designed to convert one sequence to another - like English text to Spanish text. Think of them as having two parts:

- An encoder that processes your input sequence
- A decoder that generates your output sequence

The problem was how to pass information from encoder to decoder effectively.

## What is an RNN?

RNN stands for Recurrent Neural Network - a type of neural network designed for sequential data:

- They process tokens one at a time (like words in a sentence)
- Each step builds on previous steps (hence "recurrent")
- They're like having short-term memory while reading through text

## The "Final Hidden State" Problem

When the RNN encoder finishes processing all input tokens, it produces a "final hidden state" - essentially a compressed summary of everything it read.

In early seq2seq models:

- This single compressed state was all the decoder had to generate the entire output
- It's like trying to translate a book after only reading a brief summary
- Too much information gets lost in compression

## Two Major Problems with Seq2Seq

1. **Information bottleneck**: The decoder only sees the final hidden state, losing access to individual input details
2. **Sequential processing**: RNNs must process tokens one after another, which is very slow for long sequences (imagine waiting for 200 tokens to process one by one)

## The Transformer Revolution: Attention Mechanism

The attention mechanism was the game-changer because:

- It allows the decoder to "look back" at any part of the input sequence when generating each output token
- It's like having the entire book available for reference, not just the summary
- Each output word can "pay attention" to the most relevant input words

In the diagram's lower half, see how each Spanish output word connects to all English input words? That's attention - direct access to the full context.

The transformer architecture eliminated RNNs entirely and made these attention connections the core mechanism, enabling parallel processing and much better performance on long sequences.

Transformer architecture introduced the concept of "attention"

This made them quite efficient at modeling long term dependencies when generating
text. "Attention" is a math function which can consider word relationships (token relationships) much more efficiently by looking at all the words in a sentence at the same time - rather than step by step (token by token). It's efficient because
people have created fancy algorithms and algorithms that heavily use parallel
computation to model long-term dependencies among words)

Using attention, the AI models can perform much better at natural language
processing.

$$\text{Attention}(Q,K,V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

- 𝑄  = query (what the current word is looking for)
- K = keys (what each other word represents)
- V = values (the information each word carries)

This computes a weighted average of all words, where the weights depend on how relevant they are. So instead of just a curve defined point-to-next-point, you’re fitting a surface where each point considers its relation to all other points at once.


Attention is just a fancy way of saying "weighted average" or all the words so far, while keeping in context the dependencies between various parts of the current
context.

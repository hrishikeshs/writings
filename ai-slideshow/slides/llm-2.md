Extending our understanding about AI models as 'long equations fitting a curve',
for LLMs, we can think of 'data points' on a curve as 'tokens'.

Example "curves" are:
- The cat sat on the ...
- The school started around ...

The model's job is now to predict the next token - continuing the "curve". So,
instead of fitting points on a 2D plane, the model is fitting the following
probability curve:

$$P(w_i \mid w_{1}^{i-1}) = \frac{P(w_{1}^{i})}{P(w_{1}^{i-1})}$$

In practice, a Language Model calculates this probability by:
Looking at the previous words $w_{1}^{i-1}$. Using its internal trained weights (represented by L) to process that sequence. Outputting a probability distribution over all possible words in its vocabulary for the next slot.

The equation essentially asks: _"Out of all the words the model knows, which word is most likely to come next, given this specific context?"_

Each word is represented not just as a string, but as a vector (like a point in a 10,000 dimensional space)

- 'cat' here may be "closer" to 'dog' or 'animal'
- 'San Francisco' may be closer to 'New York', or 'Bangalore'

The "curve" which the model is drawing is now living in this high-dimensional space.
It's no longer "x-axis versus y-axis", but it's rather:

**"10,000 dimensions of word meaning versus the probability of the next word"**

Training an LLM means showing the neural network billions of documents - text, videos, images, etc to arrive at a set of billions of weights which have a very high probability of predicting the next token (or a set of tokens). This works very well for language because this approach captures:

- Patterns like grammar, style, facts, reasoning steps
- Over trillions of sentences, it becomes so good at fitting a curve that it appears
to be coherent
- **It's very important for you to remember that guessing the next set of tokens
reasonably well is NOT understanding**
- These systems do not "think" or "remember" or "understand". A dog, or a baby, or a
human does.

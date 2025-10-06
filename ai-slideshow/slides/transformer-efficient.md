# Why efficiency matters

Language is a complex symbolic and semantic structure. Any system that tries to understand or imitate it needs to model relationships between a word and any other word in context. This can get complicated very quickly.

Earlier models could only look at a sequence of words step by step. They struggled with long term
dependencies. An example of how complex language can be was recently illustrated in this excellent
youtube video: [Noam Chomsky on language](https://youtu.be/-72JNZZBoVw?si=qW4LSI33iG2ScP_x)

Consider the following sentences:
- "The chicken is ready to eat"
- "The chicken is ready to be eaten"
- "The chicken is hard to eat"
- "The chicken is hard to be eaten"

Sentences 1, 2 and 3 _make sense_ when you hear it. But sentence 4 is just an
absurd statement which doesn't make any sense. Though the only difference is the
substitution of the word "ready" with "hard" - though both are adjectives

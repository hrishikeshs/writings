# What a model looks like (continued)

Continuing the analogy we had, we can think of the models as:

- Weights-only: just the coefficients of a polynomial, with a note like “these
belong to a quadratic": $ax^2 + bx + c = 0$

- Full model = the entire formula plus coefficients saved together. You can use it immediately without knowing the original definition.


Normally, when we download open-source models, we get both the weights and the
model code. So when we pull from HuggingFace, we can just do:

```

from transformers import GPT2LMHeadModel
model = GPT2LMHeadModel.from_pretrained("gpt2")

```

Which downloads the weights (coefficients) and the formula (code).
We can then use these pre-trained models and do whatever we want with them. Like,
for example: smart auto-complete for coding, classifying text, OCR, voice to text
transcription, auto-translation, etc

What this all means is that, everyone who trains their own model needs their own
proprietary model code. Even though all of them use the "Transformer" architecture,
their code and the data on which they have trained is still closed-source.

Hopefully, this presentation shed some light on what AI really is. I see a lot of
people think of it like some sort of "magic box" and ascribe all kinds of shit to
it - like "it can think", "it can reason" and other BS. It cannot do any of those
things - at least, not like how we normally understand the words "think" and
"reason".

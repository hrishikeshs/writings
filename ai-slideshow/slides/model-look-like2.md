# What it looks like when you load this "model"

```
# load the model we created in the previous slide
checkpoint = torch.load("tiny_model.pt")
print(checkpoint)
```

This will give you sample output like:

```
{
  'fc.weight': tensor([[ 0.1045, -0.2203,  0.1117],
                       [ 0.3056, -0.0277,  0.0904]]),
  'fc.bias': tensor([-0.0152,  0.0328])
}

```
### Explanation

- fc.weight is a 2×3 matrix (because the layer maps 3 inputs → 2 outputs).
- fc.bias is a 2-dimensional vector (one bias per output unit).
- These are just floating-point numbers (the “knobs” of the equation).

If you opened `tiny_model.pt` in a text editor, you’d mostly see binary
gibberish — because it’s storing floats efficiently. But when you load it, you get
these tensors. (the numbers may differ as they are random)
PyTorch needs to know: “Oh, fc.weight belongs to a Linear layer, so when I compute y = Wx + b, I should use these numbers.”

Without the code to intepret the weights, you have giant file with a lot of numbers
which don't do anything. This tiny checkpoint is what’s happening in a giant
LLM - only with billions of rows and columns instead of a 2×3 matrix.

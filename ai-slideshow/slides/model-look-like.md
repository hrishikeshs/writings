# What does a model look like ?

Here's a pytorch example of a simple AI model:

```
import torch
import torch.nn as nn

# A tiny "model" = one linear layer

class TinyModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc = nn.Linear(3, 2)  # input dim = 3, output dim = 2

    def forward(self, x):
        return self.fc(x)

model = TinyModel()
```

When you run this with pytorch:
```
torch.save(model.state_dict(), "tiny_model.pt")
```

It creates a file called `tiny_model.pt` which contains the trained parameters (weights + biases)

# What does a model look like (continued)

You can save the model in one of two ways:

1. Weights only dictionary
2. Full model (architecture + weights bundled)


> Note that the weights are initialized to be all random numbers when you first
> start training the model. After you have shown the network billions of examples:
> both labeled and unlabeled, the network learns probabilities, and for each
> example, updates it's weights. After a long time spent training this, the
> weights of the network end up being valuable as they now encode information in them

A full model look like this:

```
import torch
import torch.nn as nn

# Same tiny model
class TinyModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc = nn.Linear(3, 2)

    def forward(self, x):
        return self.fc(x)

model = TinyModel()

# Save the *entire model* (not just weights)
torch.save(model, "tiny_model_full.pt")


# Load without redefining the class
loaded_model = torch.load("tiny_model_full.pt")
print(loaded_model)

```

## output:
```
TinyModel(
  (fc): Linear(in_features=3, out_features=2, bias=True)
)
```

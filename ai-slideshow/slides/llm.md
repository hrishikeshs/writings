# What is an LLM?

Now that we have a solid understanding of what an AI model is, we can discuss what
large language models really are. They are huge neural networks which use layers of
non-linear functions. You can think of them as a bunch of functions with feedback
loops, that constitute an even larger function. In other words, a single "model" might have a bunch of "sub models" and those can have "sub-sub-models" and so on. Like any large system basically.

As these neural nets use combinations of non-linear functions (e.g: [sigmoid](https://en.wikipedia.org/wiki/Sigmoid_function), [ReLu](https://en.wikipedia.org/wiki/Rectified_linear_unit), etc), they can approximate **any** curve or surface - not just
lines or polynomials. This is why they are called **universal function
approximators**

The text-classifier we previously saw was:
- Turning the string into numbers
- Feeding those numbers into a large function with tons of parameters
- Outputting the most likely 'job title Id' and 'location Id's

A good way to think about an AI model is as a **_huge, flexible, curve_** in a very high dimensional space. Training is just **curve-fitting**: adjust the parameters to
minimize the error between prediction and truth. Using the model later is just
**plugging x into the fitted function**

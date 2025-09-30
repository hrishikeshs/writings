A model is just a function with a lot of knobs (weights). You adjust the knobs so the function "fits" as much of the training data as possible.

- In a linear model, the knobs are m (slope) and x
- In a polynomial, they are $a_0$, $a_1$, $a_2$ etc
- In a neural network, there might be order of millions or billions of such parameters. All of them boil down to:

$$\tilde{y} = f(x; \theta)$$

In other words, the prediction ($\tilde{y}$) is a function (f) of an input variable (x) and
a set of parameters (θ). `f` is the model(the equation), `x` is the input, and θ are the parameters we tune. The "curve" doesn't have to be on a 2-D plane. When we classified **software-engineer-jobs-in-san-francisco**, the model was fitting a curve in a much higher dimensional space.
- One axis might represent: "Is this a job title?"
- Another axis: "Is this a location?"
- Another axis: "probability that the substring maps to id 4567"

You cannot easily visualize/draw the curve, but it's the same idea: The model finds a function that separates or maps inputs -> outputs

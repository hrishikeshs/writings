# What is a model anyway ?

**A model is just a very, very long math equation**
An simple  math equation we're familiar with is:

$y = mx + c$

This is already a simple "AI model". It taken an input x, and predicts an output y.

If you have a bunch of points on a graph, and you observe that most of
them pass through a straight line, you try to fit a line through those points.
This is **linear regression**

Now, imagine if instead of a line, you try a polynomial: $y = a_0 + a_1x + a_2x^2 + a_3x^3 + \dots$

The more terms you add, the more flexible the curve is. Here, $a_0$, $a_1$, $a_2$ etc are the co-efficients. When you train a neural network, these are the values whichthe network "learns". These are also called "weights". The bigger the coefficient, the larger it's contribution to the result. The equation above depends on a single variable: x. A more complex one may be a function of $x_1$, $x_2$, $x_3$...$x_n$

Now imagine such an equation with billions of coefficients. This is your AI model.

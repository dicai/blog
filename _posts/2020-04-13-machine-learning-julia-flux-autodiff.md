---
layout: post
title: Machine Learning in Julia with Flux
author: Diana Cai
tags:
- machinelearning
- julia
- flux
- misc
summary: Getting started with machine learning in Julia with Flux.
---

I decided to try out [Flux](https://github.com/FluxML), a machine learning library for [Julia](https://julialang.org/).
Several months ago, I switched to using Python so that I could use PyTorch, and I figured it was time to give Flux a try for a new project that I'm starting.
Here, I document some of the basics and how I got started with it. Helpful
pointers for getting started are available in the official  [Flux documentation](https://fluxml.ai/Flux.jl/stable/).


# Installing Flux

Installing Flux is simple in Julia's package manager -- in the Julia interpreter, after typing ```]```,

{% highlight julia %}
(@v1.4) pkg> add Flux
{% endhighlight%}

As of the current writing, it is recommended that you use Julia 1.3 or above.

Now we'll present some simple examples that are modifications the original [tutorial examples](https://fluxml.ai/Flux.jl/stable/).
Here we assume basic familiarity with Julia syntax. Recall that ```*``` can be used to encode matrix multiplication, and the ```.``` operator can be used for broadcasting functions to array-valued arguments.

# Simple gradients and autodiff

The ```gradient``` function is part of [Zygote](https://github.com/FluxML/Zygote.jl) -- Flux's autodiff system -- and can be overloaded in several ways.
One of the simplest uses of gradient is to pass in a function and the arguments that you want to take the derivate with respect to.

{% highlight julia %}
using Flux

f(x,y) = 3x^2 + 2x + y
df(x,y) = gradient(f,x,y)
{% endhighlight%}

Now you can evaluate the gradient at a point:
{% highlight julia %}
julia> df(2,2)
(14, 1)
{% endhighlight%}

# Linear regression example

Another way to use the gradient function is to pass in parameters with the
```params``` function, which can be used to differentiate parameters that are
not explicitly defined as function arguments. This is designed to help support
large machine learning models with a large number of parameters.

First, let's write a function to generate some data randomly:
{% highlight julia %}
function generate_data(N_samps)
    W0, b0 = rand(2, 5), rand(2)
    x = [rand(5) for _ in 1:N_samps]
    y = [W0 * x[i] + b0 + rand(2) for i in 1:N_samps]
    return x, y
end
{% endhighlight%}

In Flux, training a model typically involves encoding the model via a prediction and a loss function on a single data point.
{% highlight julia %}
# Model / generate prediction
predict(x) = W * x .+ b

# Loss function on an example
function loss(x, y)
  ypred = predict(x)
  sum((y .- ypred).^2)
end
{% endhighlight%}

Here the model (i.e., predict function) only comes in to the loss function and isn't needed directly otherwise.

{% highlight julia %}
# Generate some data
N_samps = 10
x, y = generate_data(N_samps)

# Initialize parameters
W, b = rand(2, 5), rand(2)

# Use gradient descent as the optimizer
optimizer = Descent(0.05)

# Store epoch loss
losses = []

# Run 1000 iterations of gradient descent
for iter in 1:1000
    for i in 1:N_samps
        # Compute gradient of loss evaluated at sample
        grads = gradient(params(W, b)) do
            return loss(x[i], y[i])
        end

        # Update parameters via gradient descent
        for p in (W, b)
            update!(optimizer, p, grads[p])
        end
    end
    # Save epoch loss
    push!(losses, sum(loss.(x,y)))
end
{% endhighlight %}

Note that in the inner loop, the ```gradient``` function is being used on ```params(W,b)```, which are parameters that are not *explicitly* defined as arguments of the loss function.
Here we've also used the Julia [do operator](https://docs.julialang.org/en/v1/manual/functions/#Do-Block-Syntax-for-Function-Arguments-1), which allows you to pass a function; this can be especially useful if the function involves more complex logic.
Alternatively,  this example is easily expressible as
{% highlight julia %}
grads = gradient(() -> loss(x[i], y[i]), params(W, b))
{% endhighlight %}
instead of using the do operator block.

Additionally, the ```update!``` function tells us to use the optimizer (here gradient descent) to update the parameter p with the gradient.
[Other optimizers](https://fluxml.ai/Flux.jl/stable/training/optimisers/#Optimiser-Reference-1) can be specified in a similar manner as we did above.
For instance, we could have used ADAM by specifying:
{% highlight julia %}
optimizer = ADAM(0.05)
{% endhighlight %}


## Flux's train function

Another simpler way of implementing the functionality above is to use Flux's ```train!``` function, which replaces the inner loop above.
[Training](https://fluxml.ai/Flux.jl/stable/training/training/) requires (1) an objective function, (2) the parameters, (3) a collection of data points, and (4) an optimizer.

The inner loop can be replaced as follows:
{% highlight julia %}
# Run 1000 iterations of gradient descent
for iter in 1:1000
    Flux.train!(loss, params(W,b), zip(x,y), optimizer)
    push!(losses, sum(loss.(x,y)))
end
{% endhighlight %}
In other words, the ```train!``` function can be viewed as taking a step of the parameters with the optimizer of your choice, evaluated with respect to a set of data points.

The ```train!``` function also accepts a [callback function](https://fluxml.ai/Flux.jl/stable/training/training/#Callbacks-1), that allows you to print information (e.g., the loss), which is often used with the ```throttle``` function to limit the output to, say, every 10 seconds.
In the above example, we saved the training losses in an array, in order to allow for easy plotting.

# Building and training models

Building more complex models is similar to the example above, but now we can compose different functions.
Again, we can call train once we specify a loss (where again the model only comes into the loss function), a set of parameters, data, and the optimizer.

There are many examples of how to build up layers in the [Flux basics guide](https://fluxml.ai/Flux.jl/stable/models/basics/)
and the [model reference](https://fluxml.ai/Flux.jl/stable/models/layers/).
For instance, the basics guide presents the following two examples.
The first is composing two linear layers with sigmoid nonlinearities, given by the ```σ``` function:
{% highlight julia %}
function linear(in, out)
  W = randn(out, in)
  b = randn(out)
  x -> W * x .+ b
end

linear1 = linear(5, 3)
linear2 = linear(3, 2)

model(x) = linear2(σ.(linear1(x)))
{% endhighlight %}

Another example presented in the basics guide is using the ```Chain``` utility:
{% highlight julia %}
model = Chain(
  Dense(10, 5, σ),
  Dense(5, 2),
  softmax)
{% endhighlight %}
Here ```Dense``` is another utility that represents a dense layer.
Other types of layers are detailed in the [model reference](https://fluxml.ai/Flux.jl/stable/models/layers/), including convolution, pooling, and recurrent layers.

After building models, we can then again use the ```train!``` function as before.

Specific working models can be found in the [Flux model zoo](https://github.com/FluxML/model-zoo/), which includes examples such as simple multi-layer perceptrons, convolutional neural nets, auto-encoders, and variational-autoencoders.

# Overall impressions

Overall, I found Flux easy to use, especially if you've used something like PyTorch before. I liked how it felt very well-integrated with the Julia language -- it really felt like just coding in Julia, rather than having to learn a whole new framework.
One thing I think could be better supported is the documentation -- I found that it was good enough to get started and learn the functionality of Flux, but for instance, some basic docstrings for important functions were missing.




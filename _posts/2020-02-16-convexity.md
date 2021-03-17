---
layout:     post
title:      Convexity
date:       2021-03-16 12:31:19
summary:    Short discussion on convexity
categories: Concept
---

These definitions are pulled from the notes in [this course at UCI](https://www.ics.uci.edu/~xhx/courses/CS206/). Graphs + additional contents outside definition text are done by me.

## Convexity Sets and the Like

**Definition: Convex Sets**

A set $$C$$ is called **convex** if $$x,y \in C \Longrightarrow \theta x + (1 - \theta) y \in C \; \forall \theta \in [0,1]$$ 

This equation defines the line segment between $$x$$ and $$y$$.  For example, in the following figure, we fix points $$(1,1)$$ and $$(2,5)$$ and compute the output of $$\theta x + (1 - \theta ) y$$ along the segment in the range $$\theta \in [0,1]$$. 

{:refdef: style="text-align: center;"} 
![linesegment]({{site.baseurl}}/images/linesegment.png){: width="300" } 
{: refdef}

Thus, for the set to be convex, we must be able to draw a line segment between any two points in the set.

**Definition: Convex Combination**

A **convex combination** of the points $$x_1,...,x_k $$ is a point of the form $$\theta_1 x_1 + ... + \theta_k x_k$$ where $$\theta_1 + ... + \theta_k = 1$$ and $$\theta_i \geq 0$$ for all $$i=1,...,k$$. A set is convex $$\iff$$ it contains every convex combinations of its points.

**Definition: Convex Hull**

A **convex hull** of a set $$C$$, denoted **conv** $$C$$, is the set of all convex combinations of points in $$C$$:

<center>$$ \textrm{conv}\;C = \{ \sum_{i=1}^k \theta_i x_i | x_i \in C, \theta_i \geq 0, i=1, ..., k, \sum_{i=1}^k \theta_k =1 \} $$</center>

Note, the convex hull is always convex. Also, the convex hull is the *smallest* convex set that contains the set of points $$C$$.

**Definition: Cone**

A set $$C$$ is called a **cone** if $$x\in C \Longrightarrow \theta x \in C, \;\; \forall \theta \geq 0$$.

**Definition: Convex Cone**

A **convex cone** is the set $$C$$ that is both convex and a cone, i.e., $$x_1, x_2 \in C \Longrightarrow \theta_1 x_1 + \theta_2 x_2 \in C, \;\;\; \forall \theta_1,\theta_2 \geq 0$$

**Proposition: The intersection of convex sets is convex.**

Why is this the case? For any two points in the intersection of convex sets, it must be able to draw a line segment between them, otherwise the sets for which we take the intersection wouldn't be convex.  Therefore, the intersection of convex sets is convex.

## Convex Functions 

**Definition: Convex Function**

The function $$f : \mathbb{R}^n \rightarrow \mathbb{R}$$ is convex if the domain of $$f$$ is a convex set and

<center>$$f(\theta x + (1-\theta) y) \leq \theta f(x) + (1 - \theta) f(y)$$</center>

For all $$x,y \in \textrm{dom}\; f$$ and $$\theta \in [0,1]$$.

To provide a bit more intuition, I take the convex function $$f(x) = x^2$$, and fix $$x=3$$ and $$y=-1$$.  Then, I plot the output for both the left hand side and right hand side of the equivilence for $$\theta \in [0,1]$$.  We see that the LHS is always $$\leq$$ to the right hand side.

{:refdef: style="text-align: center;"} 
![linesegment]({{site.baseurl}}/images/convexfint.png){: width="300" } 
{: refdef}

Let's fix a non-convex function, $$f=x^3$$ and try again.  This time, we choose $$x=3$$ and $$y=-3$$.

{:refdef: style="text-align: center;"} 
![linesegment]({{site.baseurl}}/images/nonconvex.png){: width="300" } 
{: refdef}

We see the inequality is violated! We see from the example, the defintion of convex function states: fix any two points in the functions domain and draw a line segment between the function outputs.  The function should always be below (or equal to) this line for the function to be convex. 

**Definiton: Strictly Convex Function**

The function $$f$$ is strictly convex if the domain of $$f$$ is convex and 

<center>$$f(\theta x + (1-\theta) y) < \theta f(x) + (1 - \theta) f(y)$$</center>

For all $$x,y \in \textrm{dom}\; f$$ and $$\theta \in (0,1)$$.

**Theorem (first-order condition)**

If $$f : \mathbb{R}^n \rightarrow \mathbb{R}$$ is differentiable, then $$f$$ is convex $$\iff$$ the domain of $$f$$ is convex and 

<center>$$f(y)\geq f(x) + \nabla f(x)^T (y-x) \forall x,y \in \textrm{dom}\; f$$</center>

**Theorem (second-order condition)**

If $$f : \mathbb{R}^n \rightarrow \mathbb{R}$$ is twice differentiable, then $$f$$ is convex $$\iff$$ the domain of $$f$$ is convex and its Hessian is positive semidefinite.


<!-- {% highlight python lineanchors %}
import matplotlib.pyplot as plt
import numpy as np 

def interp(x,y):
    to_int = np.linspace(0,1,100).reshape(100,1)
    return to_int.dot(x) + (1 - to_int).dot(y)

with plt.xkcd():

    fig = plt.figure()
    ax = fig.add_axes((0.1, 0.2, 0.8, 0.7))
    ax.spines['right'].set_color('none')
    ax.spines['top'].set_color('none')

    ax.set_ylim([0, 7])
    ax.set_xlim([.5,2.5])

    s1, s2 = np.array([[1,1]]), np.array([[2,5]])
    interps = interp(s1,s2)

    ax.plot(interps[:,0], interps[:,1], c='b')
    ax.scatter([1,2],[1,5],c='r',marker='o', s=100)

    ax.set_xlabel('X')
    ax.set_ylabel('Y')
{% endhighlight %}
 -->
---
title: 'The law of cosines: A skeleton key for convergence proofs in optimization'
collection: teaching
type: "Convex optimization"
permalink: /teaching/law-of-cosines
venue: online
date: 2021-10-01
location: "Austin, Texas"
mathjax: true
---
Do you remeber the law of cosines from your high-school math classes? Did you know that it is an incredibly useful technique in the convergence proofs of optimization methods? Find out more in this lecture.

<img src="/images/cosine.png" width="300" height="300" img align='right'>

# Prerequisite

The definition of [convex sets](https://en.wikipedia.org/wiki/Convex_set) and [convex functions](https://en.wikipedia.org/wiki/Convex_function).

# The law of cosines

You probably have seen the [low of cosines](https://en.wikipedia.org/wiki/Law_of_cosines) in high school. Given a triangle, the law of cosines gives an equation between the cosine of one of the three angles and the length of the three sides, as shown by the image on the right.

Although usually considered for two or three dimensional triangles, the law of cosines can be generalized higher dimensions as well. To see this generalization,  we let
$$||x||$$
denote the $\ell_2$-norm of vector $x$. Let $x^1, x^2, x^3\in\mathbb{R}^n$ be three points in a $n$-dimentional vector space. By completing the squares one can verify the following general form of law of cosines:

\begin{equation}
\langle x^1-x^2, x^3-x^1\rangle=\frac{1}{2}||x^3-x^2||^2-\frac{1}{2}||x^3-x^1||^2-\frac{1}{2}||x^1-x^2||^2.
\end{equation}

Notice that the above equation is indeed equivalent to the law of cosines. In particular, $x^1, x^2$ and $x^3$ are the coordinates of the three vertices of the triangle. The length of each side of the triangle is measured by the $\ell_2$-norm. In addition, the cosine (together with a negative sign) is now hidden in the inner product term. 

There you have it, a **skeleton key** to unlock many seemingly enigmatic convergence proofs in convex optimization! 

How can a simple equation be that useful? 

Well, it turns out the equation above simultaneously embeds two terms commonly used in the convergence proofs:

* **Inner product**: For example, when minimizing a function over a set, the minimizer is characterized by a variational inequality, where an inner product naturally appears. 
* **Difference of two quadratic functions**: Many convergence proofs rely on showing certain quadratic disatance to the optimizer is decreasing. Hence the convergence proof usually starts by showing the difference of two quadratic functions is negative. 

Do you see it now? By providing a handy trick in dealing with the inner product and the difference of two quadratic functions, the law of cosines save many proof writers, such as myself, from a tedious process of completing many, many squares.


# Beyond quadratic functions

A key ingrident in the law of cosines is the quadratic function. So a natural question is: what makes quadratic functions so special? If we use some other functions instead, can we still get results similar to the law of cosines?

The answer is **yes**! All we need to do is to replace the quadratic function with the sso called <em>Bregman divergence</em>.  

To this end, we consider a general differentiable function $f:\mathbb{R}^n\to\mathbb{R}$. Given two points $x^1, x^2\in\mathbb{R}^n$, the Bregman divergence between $x^1$ and $x^2$ associated with function $f$ is given as follows:

$$ B_f(x^1, x^2)=f(x^1)-f(x^2)-\langle \nabla f(x^2), x^1-x^2\rangle.$$  
  
Using the above definition, you can verify that the following equation holds:
  
$$ \langle \nabla f(x^1)-\nabla f(x^2), x^3-x^1\rangle=B_f(x^3, x^2)-B_f(x^3, x^1)- B-f(x^1, x^2). $$  
  
The above equation is also known at the **three-point property of Bregman divergence**. You can check that equation (1) is in fact a special case of equation (2) if

$$f(x)=\frac{1}{2}||x||^2.$$ 
  
If function $f$ is convex, then $B_f(x^1, x^2)$ is always nonnegative. In this case, the Bregman divergence becomes a candidate function for measuring distance to optimum in optimization, as a generalization to quadratic functions. In fact, this generalization is the key difference between [gradient descent method](https://en.wikipedia.org/wiki/Gradient_descent) and [mirror descent method](https://www.sciencedirect.com/science/article/abs/pii/S0167637702002316), two of the most famous first-order optimization methods.   
  
Finally, the law of cosines is not only useful for optimization problems in vector spaces, but those in manifolds as well. For a detailed discussion, see Lemma 5 in [this paper](http://proceedings.mlr.press/v49/zhang16b.pdf) for an example.  


# How to use it in a convergence proof?
  
Let's see how the law of cosines is used in the convergence proof of gradient descent method.
  
## Optimization problem and assumptions

We consider the minimization of a differentiable convex function $f:\mathbb{R}^n\to\mathbb{R}$. We assume there exists $x^\star\in\mathbb{R}^n$ such that $f(x^\star)$ attains its minimum value, in which case the following condition holds:
  
  $$\nabla f(x^\star)=0$$
  
We also make the following assumptions on function $f$: there exists $0< \mu\leq \lambda$ such that
  
  $$\frac{\mu}{2}||x-x'||^2\leq B_f(x, x')\leq \frac{\lambda}{2}||x-x'||^2$$
  
for all $x, x'\in\mathbb{R}^n$. Intuitively, the above assumption upper and lower bounds the curvature of function $f$. Under this assumption, function $f$ is also known as a $\mu$-strong convexity and $\lambda$-smooth function.

## The gradient descent method
  
To solve the above minimization problem, we consider the gradient descent method, where a sequence $\\{x^1, x^2, x^3, \ldots\\}$ is computed recursively as follows:
  
  $$x^{k+1}=x^k-\alpha \nabla f(x^k),$$
  
 where $k$ is the iteration counter, and $\alpha$ is a known positive step size. 

## The convergence proof  
  
Any ideas of how to show $x^k$ converges to $x^\star$ as $k$ increases? Let us prove it step by step.  
  
### What we already know
Given equation (4) and (6), we immediately know the following:
  
  $$x^{k+1}-x^k+\alpha (\nabla f(x^k)-\nabla f(x^\star))= 0. $$
  
Since the inner product of a zero vector with any vector is always zero, we conclude that
  
  $$0=\langle x^{k+1}-x^k+\alpha (\nabla f(x^k)-\nabla f(x^\star)), x^\star-x^{k+1}\rangle.$$
  
### The law of cosines
  
**Aha!** Now we see some inner product terms similar to those in the law of cosines! By applying equation (1) and equation (2) to **the triangle defined by $x^k, x^{k+1}$ and $x^\star$**, we can show the following:
  
 $$\langle x^{k+1}-x^k, x^\star-x^{k+1}\rangle=\frac{1}{2}||x^k-x^\star||^2-\frac{1}{2}||x^{k+1}-x^\star||^2-\frac{1}{2}||x^{k+1}-x^k||^2,$$
  
 $$\alpha \langle \nabla f(x^\star)-\nabla f(x^k), x^{k+1}-x^\star\rangle=\alpha (B_f(x^{k+1}, x^k)-B_f(x^{k+1}, x^\star)-B_f(x^\star, x^k)).$$
  
### Some simple bounds using the assumptions
  
Next, in order to cancel out the cumbersome Bregman divergence terms, we bound them using quadratic functions. By using equation (5), we can immediately obtain the following inequalities:
  
  $$\alpha B_f(x^{k+1}, x^k)\leq \frac{\alpha \lambda}{2}||x^{k+1}-x^k||^2,$$
  
  $$\frac{\alpha \mu}{2}||x^k-x^\star||^2\leq \alpha B_f(x^\star, x^k),$$
  
  $$\frac{\alpha \mu}{2}||x^{k+1}-x^\star||^2\leq \alpha B_f(x^{k+1}, x^\star).$$

### Summing up inequalities and canceling terms  

Finally, by summing up equation (8-13), and letting $\alpha\leq\frac{1}{\lambda}$, we obtain the following result:
  
  $$\frac{1+\frac{\mu}{\lambda}}{2}||x^{k+1}-x^\star||^2\leq \frac{1-\frac{\mu}{\lambda}}{2}||x^k-x^\star||^2.$$

### Proving Exponential convergence by induction  
  
By using the above relation recursively, we can show the following
  
  $$||x^{k+1}-x^k||^2\leq \frac{\lambda-\mu}{\lambda+\mu}||x^k-x^\star||^2\leq \cdots \leq \left(\frac{\lambda-\mu}{\lambda+\mu}\right)^k||x^1-x^\star||^2.$$
  
In other words, as the iteration number $k$ increases, the nonnegative quadratic distance between $x^k$ and $x^\star$ is upper bounded by a number that converges to zero exponentially. Hence this distance must converge to zero itself. 
  
  
Want some more examples?
======
  
  If you like the above convergence proof and its connection to the law of cosines, there are many other similar proofs in my [PhD dissertation](https://digital.lib.washington.edu/researchworks/bitstream/handle/1773/46999/Yu_washington_0250E_22557.pdf?sequence=1&isAllowed=y). In Appendix B, I rewrote the convergence proofs of most existing first order methods, including projected gradient/subgradient method, proximal gradient method, mirror descent method. All these proofs follow similar steps as the one above.
                                                                                
 I also use the law of cosines in all of my published work on [distributed optimization](https://arxiv.org/pdf/2009.06980.pdf) and [conic optimization](https://arxiv.org/pdf/2108.10260.pdf), see my [list of publications](/_pages/pub_topic.md) for more references. 
  
  Now you are holding the skeleton key to unlock all of these proofs, and many more out there. As Professor Slughorn said to Harry Potter: <em>Use it well!<em>

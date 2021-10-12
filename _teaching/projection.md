---
title: 'Projections: Why are they useful and how to compute them'
collection: teaching
type: "Convex optimization"
permalink: /teaching/projection
venue: online
date: 2021-10-03
location: "Austin, Texas"
mathjax: true
---

Do you know how to compute projections onto structured convex sets, and how to use them to solve constrained optimization problems? Find out more in this lecture.

# Prerequisite

The definition of [convex sets](https://en.wikipedia.org/wiki/Convex_set) and [convex functions](https://en.wikipedia.org/wiki/Convex_function).

<img src="/images/projection.png" width="250" height="250" img align='left'>

# What is a projection?

Given a set $\mathbb{D}$ and a point $x$, a projection of $x$ onto set $\mathbb{D}$ is a point in set $\mathbb{D}$ that is closest to $x$. If set $\mathbb{D}$ is closed and convex, such projection is unique. We denote the projection of $x$ onto set $\mathbb{D}$ as $\pi_{\mathbb{D}}[x]$, defined as follows:

$$\pi_{\mathbb{D}}[x]=\underset{y\in\mathbb{D}}{\mbox{argmin}}\,\, ||x-y||,$$

where
 $$||\cdot||$$
denotes the $\ell_2$-norm.


# Why is it useful?

Projection is a building block for projected gradient method, and many other methods for constrained optimization, as we will show. 

Consider the minimization of a differentiable convex function $f:\mathbb{R}^n\to\mathbb{R}$ over a closed convex set $\mathbb{D}$. One of the most basic and powerful method for such minimization is the <em>projection gradient method</em>, which computes a sequence of estimate of the optimizer, $x^1, x^2, \ldots$, recursively as follows:
  
  $$x^{k+1}=\pi_{\mathbb{D}}[x^k-\alpha \nabla f(x^k)],$$
  
where $\alpha$ is a known positive scalar.
  
The projection is also used in many advanced constrained optimization methods, including the [Douglas-Rachford splitting method](https://arxiv.org/pdf/1303.1090.pdf) and [Proportional-integral projected gradient method](https://arxiv.org/pdf/2108.10260.pdf).
 
# How to compute it?
  
  In general, computing the projection onto set $\mathbb{D}$ can be non-trivial. For example, if $\mathbb{D}$ is a [convex polytope](https://en.wikipedia.org/wiki/Polytope), the computing the projection onto $\mathbb{D}$ is a [linear complementarity problem](https://en.wikipedia.org/wiki/Linear_complementarity_problem), which requires an iterative method itself.
  
  Fortunately, when set $\mathbb{D}$ has some particular structure, we can compute the projection onto $\mathbb{D}$ using very simple formulas, as we will show.
  
## Projections onto structured convex sets
  
  There are many examples for computing projections using simple formulas. Here we provide a few samples of them. 
  
  <img src="/images/box.png" width="150" height="150" img align='left'>
  
### Box
  
  Consider the following set
  
  $$ \mathbb{D}=\{y\in\mathbb{R}^n|\, l\leq y\leq u\},$$
  
  where $l, u\in\mathbb{R}^n$ are known lower and upper bounds.
  
  The projection of $x$ onto set $\mathbb{D}$ is given by
  
  $$\pi_{\mathbb{D}}[x]=\min\{\max\{x, l\}, u\},$$
  
  where the $\max$ and $\min$ are evaluated elementwise.
  
  An important special case of the box constraint set is the <em>nonnegative orthant<em>, where 
  
  $$\mathbb{D}=\{y\in\mathbb{R}^n|\, y\geq 0\}.$$
  
  <img src="/images/ball.png" width="150" height="150" img align='left'>
  
  In this case, the projection of $x$ onto set $\mathbb{D}$ becomes
  
  $$\pi_{\mathbb{D}}[x]=\max\{x, 0\}.$$
  
### Ball
  
  Consider the following set
  
  $$ \mathbb{D}=\{y\in\mathbb{R}^n|\, ||y||\leq \rho\},$$
  
  where $\rho\in (0, \infty)$ is the radius of the ball.
  
  The projection of $x$ onto set $\mathbb{D}$ is given by
  
  $$\pi_{\mathbb{D}}[x]=\frac{\rho}{\max\{||x||, \rho\}}x.$$ 
  
  <img src="/images/cylinder.png" width="150" height="150" img align='left'>
  
### Cylinder
  
  Consider the following set
  
  $$ \mathbb{D}=\{y\in\mathbb{R}^n|\, -\eta\leq \langle e, y\rangle\leq \eta, ||y-\langle e, y\rangle e||\leq \rho\},$$

where vector $e\in\mathbb{R}^n$ determines the direction of the cylinder, $\eta\in(0, \infty)$ and $\rho\in(0, \infty)$ are the half-length and radius of the cylinder, respectively.
  
  The projection of $x$ onto set $\mathbb{D}$ can be computed in two steps. In the first step, we let
  
  $$ z=\begin{cases}
  x, & \text{if } -\eta\leq \langle e, x\rangle\leq \eta,\\
  x-(\langle e, x\rangle-\eta)e, & \text{if } \langle e, x\rangle>\eta,\\
  x-(\langle e, x\rangle+\eta)e, & \text{if } \langle e, x\rangle<-\eta.
  \end{cases}$$
  
  In the second step, given vector $z$ computed in the first step, the projection of $x$ onto set $\mathbb{D}$ is given by
                                                                    
  $$\pi_{\mathbb{D}}[x]=\langle e, x\rangle e+\frac{\rho}{\max\{||x-\langle e, x\rangle e||, \rho\}}(x-\langle e, x\rangle e). $$
                                                                      
 <img src="/images/cone.png" width="150" height="150" img align='left'>
                                                                      
### Icecream cone
   Consider the following set
  
  $$ \mathbb{D}=\{y\in\mathbb{R}^n|\, \gamma||x||\leq \langle x, e\rangle\},$$
                                                                  
where $e\in\mathbb{R}^n$ gives the direction of the cone and $\gamma\in[0, 1]$ is the cosine of the half-angle of the cone. 
                                                                    
The projection of $x$ onto set $\mathbb{D}$ is given by
                                    
  $$\pi_{\mathbb{D}}[x]=\begin{cases}
  x, & \text{if } \gamma ||x||\leq \langle e, x\rangle,\\
  0, & \text{if } \sqrt{1-\gamma^2}||x||\leq -\langle e, x\rangle,\\
  \gamma e + \frac{\sqrt{1-\gamma^2}}{||x-\langle e, x\rangle e||}(x-\langle e, x\rangle e), & \text{otherwise.}
  \end{cases} $$
  
  <img src="/images/icecream.png" width="150" height="150" img align='left'>
                                                                      
### Intersection of an icecream cone and a ball 
                                                                      
  Consider the following set
  
  $$ \mathbb{D}=\{y\in\mathbb{R}^n|\, \gamma||x||\leq \langle x, e\rangle, ||x||\leq \rho\},$$
                                                                  
where $e\in\mathbb{R}^n$ gives the direction of the cone and $\gamma\in[0, 1]$ is the cosine of the half-angle of the cone, $\rho\in(0, \infty)$ is the radius of the ball.
                                                                    
The projection of $x$ onto set $\mathbb{D}$ can be computed in two steps, In the first step, we cmopute the projection of $x$ onto an icecream cone. In particular, let $z=\pi_{\mathbb{D}_1}[x]$ where
 
 $$\mathbb{D}_1=\{y\in\mathbb{R}^n|\, \gamma||x||\leq \langle x, e\rangle\}.$$
                                                                    
In the second step, given $z$ computed in the first step, the projection of $x$ onto set $\mathbb{D}$ is given by the projection of $z$ onto a ball:
                                                                    
$$\pi_{\mathbb{D}}[x]=\frac{\rho}{\max\{||z||, \rho\}}z.$$  
                                                                    
## Projections onto the Cartesian product of sets
                                                                    
 One of the most useful property of projection is its decomposition over the Cartesian product of sets. In particular, let
                                                                    
 $$\mathbb{D}=\mathbb{D}_1\times \mathbb{D}_2, \,\, \mathbb{D}_1\subset\mathbb{R}^{n_1}, \,\, \mathbb{D}_2\subset\mathbb{R}^{n_2},$$
                                                                    
 where $\mathbb{D}_1\times \mathbb{D}_2$ denotes the [Cartesian product](https://en.wikipedia.org/wiki/Cartesian_product) of set $\mathbb{D}_1$ and $\mathbb{D}_2$. Furthermore, let
                                                                    
 $$x=\begin{bmatrix}x_1\\ x_2\end{bmatrix},\,\, x_1\in\mathbb{R}^{n_1}, \,\, x_2\in\mathbb{R}^{n_2}.$$
                                                                    
 By using the definition of projection, one can verify the following
                                                                    
 $$\pi_{\mathbb{D}}[x]=\begin{bmatrix} \pi_{\mathbb{D}_1}[x_1]\\\pi_{\mathbb{D}_2}[x_2]\end{bmatrix}.$$
                                                                    
 In other words, if set $\mathbb{D}$ is defined by constraints that are separable across different segments of a vector, then computing the projection of vector $x$ onto set $\mathbb{D}$ reduces to the projections of each segment of vector $x$. This fact is particularly useful in the context of trajectory optimization in optimal control problems, see my recent work [here](https://arxiv.org/pdf/2108.10260.pdf) for some examples. 
                                                                    
# Want more examples?
                                                                    
The projection formulas used in this post are mostly taken from the Chapter 29 in [the book by Bauschke and Combettes](https://www.springer.com/gp/book/9783319483108). For example, the projection onto an icecream cone is discussed in Exercise 29.12. The projection onto the intersection of a cone and a ball, however, is published more recnetly; see Theorem 7.1 [here](http://arxiv-export-lb.library.cornell.edu/pdf/1708.00585) for details. 
                                                                    
If you want to see some examples of how projection is used as a building block for optimization methods, please see my recent work on [Model predictive control](https://arxiv.org/pdf/2009.06980.pdf), [conic optimization](https://arxiv.org/pdf/2108.10260.pdf) and [infeasibility detection](https://arxiv.org/pdf/2109.02756.pdf) for details. 

                                                                   
 


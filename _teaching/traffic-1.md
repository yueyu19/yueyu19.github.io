---
title: 'Static traffic equilibra Part 1: Shortest path problem and linear program'
collection: teaching
type: "Network optimization"
permalink: /teaching/traffic-1
venue: online
date: 2021-10-03
location: "Austin, Texas"
mathjax: true
---

Do you know how to find the shortest path in a directed network by solving a linear program? Find out more in this post.

# Prerequisite

[Linear program](https://en.wikipedia.org/wiki/Linear_programming) and its optimality conditions.

<img src="/images/projection.png" width="250" height="250" img align='right'>

# Directed networks and the incidence matrix

A directed network is defined by a set of nodes $\mathcal{N}=\\{1, 2, \ldots, n_l\\}$ and a set of links $\mathcal{L}=\\{1, 2, \ldots, n_l\\}$. Each link $k$ is defined by a pair of ordered distinct nodes $(i, j)$, where node $i$ is known as the <em>tail</em> of link $k$, and node $j$ is the known as the <em>head</em> of the link. Each link $k$ is also associated with a link cost $c_k\in (0, \infty)$. 

The topology of the network can be encoded by the node-link incidence matrix $E\in\mathbb{R}^{n_l\times n_n}$. The entry $E_{ik}$ in matrix $E$ is are associated with node $i$ and link $k$ as follows:

\begin{equation}
     E_{ik}=\begin{cases}
    1, & \text{if node \(i\) is the tail of link \(k\),}\\
    -1, & \text{if node \(i\) is the head of link \(k\),}\\
    0, & \text{otherwise.}
    \end{cases}
\end{equation} 


# Shortest path problem

# Linear program for shortest path problem

# How to extract the shortest path from the linear program


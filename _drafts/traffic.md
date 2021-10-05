---
title: 'Static traffic equilibra: Supply-demand, queuing, and network optimization'
collection: teaching
type: "Network optimization"
permalink: /teaching/traffic
venue: online
date: 2021-10-03
location: "Austin, Texas"
mathjax: true
---

Do you know how to predict the traffic volumes in a transportation network using convex optimization? Do you know the difference between Beckmann's model and Nesterov \& de Palma's model for traffic equilibra? Find out more in this post.

# Prerequisite

[Karush–Kuhn–Tucker_conditions](https://en.wikipedia.org/wiki/Karush–Kuhn–Tucker_conditions) 

<img src="/images/projection.png" width="250" height="250" img align='right'>

# Directed networks

A directed network is defined by a set of nodes $\mathcal{N}=\\{1, 2, \ldots, n_l\\}$ and a set of links $\mathcal{L}=\\{1, 2, \ldots, n_l\\}$. Each link $k$ is defined by a pair of ordered distinct nodes $(i, j)$, where node $i$ is known as the <em>tail</em> of link $k$, and node $j$ is the known as the <em>head</em> of the link. Each link $k$ is also associated with a link cost $c_k\in (0, \infty)$. 

## Node-edge incidence matrix

The topology of the network can be encoded by the node-link incidence matrix $E\in\mathbb{R}^{n_l\times n_n}$. The entry $E_{ik}$ in matrix $E$ is are associated with node $i$ and link $k$ as follows:

$$E_{ik}=\begin{cases}
    1, & \text{if node \(i\) is the tail of link \(k\),}\\
    -1, & \text{if node \(i\) is the head of link \(k\),}\\
    0, & \text{otherwise.}
    \end{cases}$$
## Path    

A path in a directed network is a sequence of distinct links directed in the same direction that connects a collection of distinct nodes.

## Flow matrix

## Souce-sink matrix

# Wardrop equilibrium principle

# Static traffic equilibra: Beckmann's model

# Static traffic equilibra: Nesterov \& de Palma's model



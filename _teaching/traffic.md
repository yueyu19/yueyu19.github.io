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

Do you know how to predict the ground traffic volums in a city during a rush hour? Do you know the connection between traffic equilibra, supply-demand model and queuing theory? Find out more in this lecture.

# Prerequisite

[directed graph](https://en.wikipedia.org/wiki/Directed_graph) and (optional) [Karush–Kuhn–Tucker conditions](https://en.wikipedia.org/wiki/Karush–Kuhn–Tucker_conditions) 

<img src="/images/graph.png" width="250" height="250" img align='right'>

We will introduce some basic concepts in static traffic equilibra model. Thoughout this post we will use an example network given in the figure on the right. 

# Directed networks

A directed network is defined by a set of nodes $\mathcal{N}=\\{1, 2, \ldots, n_l\\}$ and a set of links $\mathcal{L}=\\{1, 2, \ldots, n_l\\}$. Each link $k$ is defined by a pair of ordered distinct nodes $(i, j)$, where node $i$ is known as the <em>tail</em> of link $k$, and node $j$ is the known as the <em>head</em> of the link. In our example network, we have $n_n=4$ and $n_l=5$. 

## Node-edge incidence matrix

The topology of the network can be encoded by the node-link incidence matrix $E\in\mathbb{R}^{n_l\times n_n}$. The entry $E_{ik}$ in matrix $E$ is are associated with node $i$ and link $k$ as follows:

$$E_{ik}=\begin{cases}
    1, & \text{if node \(i\) is the tail of link \(k\),}\\
    -1, & \text{if node \(i\) is the head of link \(k\),}\\
    0, & \text{otherwise.}
    \end{cases}$$
In our example network, we have

$$E=\begin{bmatrix}
 1 & 1 & 0 & 0 & 0\\
 -1 & 0 & 1 & 1 & 0\\
 0 & -1 & -1 & 0 & 1\\
 0 & 0 & 0 & -1 & -1
\end{bmatrix}.
$$

## Path    

A path in a directed network is a sequence of distinct links directed in the same direction that connects a collection of distinct nodes. In our example network, there are three paths from node 1 and node 4, each connects one of the following set of the nodes: $\\{1, 2, 4\\}$, $\\{1, 3, 4\\}$, $\\{1, 2, 3 4\\}$.

## Flow vector

## Souce-sink vector

# Wardrop equilibrium principle

# Beckmann's model: Each link is a market

# Nesterov \& de Palma's model: Each link is a queue




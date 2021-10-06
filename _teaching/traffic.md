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

[directed graph](https://en.wikipedia.org/wiki/Directed_graph) and [Karush–Kuhn–Tucker_conditions (optional)](https://en.wikipedia.org/wiki/Karush–Kuhn–Tucker_conditions) 

<img src="/images/graph.png" width="250" height="250" img align='right'>

# Directed networks

A directed network is defined by a set of nodes $\mathcal{N}=\\{1, 2, \ldots, n_l\\}$ and a set of links $\mathcal{L}=\\{1, 2, \ldots, n_l\\}$. Each link $k$ is defined by a pair of ordered distinct nodes $(i, j)$, where node $i$ is known as the <em>tail</em> of link $k$, and node $j$ is the known as the <em>head</em> of the link. For the network above, we have $n_n=4$ and $n_l=5$. 

## Node-edge incidence matrix

The topology of the network can be encoded by the node-link incidence matrix $E\in\mathbb{R}^{n_l\times n_n}$. The entry $E_{ik}$ in matrix $E$ is are associated with node $i$ and link $k$ as follows:

$$E_{ik}=\begin{cases}
    1, & \text{if node \(i\) is the tail of link \(k\),}\\
    -1, & \text{if node \(i\) is the head of link \(k\),}\\
    0, & \text{otherwise.}
    \end{cases}$$
For 

## Path    

A path in a directed network is a sequence of distinct links directed in the same direction that connects a collection of distinct nodes.

## Flow vector

## Souce-sink vector

# Wardrop equilibrium principle

# Beckmann's model: Each link is a market

# Nesterov \& de Palma's model: Each link is a queue




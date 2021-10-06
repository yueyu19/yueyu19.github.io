---
title: 'Traffic equilibra: Supply-demand, queuing, and network optimization'
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

# Transportation networks

A transportation network is defined by a set of nodes $\mathcal{N}=\\{1, 2, \ldots, m\\}$ and a set of links $\mathcal{L}=\\{1, 2, \ldots, m\\}$. Each link $k$ is defined by a pair of ordered distinct nodes $(i, j)$, where node $i$ is known as the <em>tail</em> of link $k$, and node $j$ is the known as the <em>head</em> of the link. Each node denotes an intersetion of roads, and an link from node $i$ to node $j$ means any travelers can travel from node $i$ to node $j$.

In our example network, we have $n=4$ and $m=5$. 

## Node-edge incidence matrix

The topology of the network can be encoded by the node-link incidence matrix $E\in\mathbb{R}^{m\times n}$. The entry $E_{ik}$ in matrix $E$ is are associated with node $i$ and link $k$ as follows:

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

A path is a sequence of distinct links directed in the same direction that connects a collection of distinct nodes. In our example network, there are three paths from node 1 and node 4, each connects one of the following set of the nodes: $\\{1, 2, 4\\}$, $\\{1, 3, 4\\}$, $\\{1, 2, 3, 4\\}$.

## Flow vector

The flow vector $x\in\mathbb{R}^m$ is an elementwise nonnegative vector, whose $k$-th entry $x_k$ denotes the amount of traveller exiting link $k$ per unit time (e.g., a day, an hour). 

## Souce-sink vector

For simplicity, we assume all travellers in the transporttaion network have the same destination node, given by node $n$. The the traffic demand in the network is described by the source-sink vector $s\in\mathbb{R}^n$, whose $i$-th entry $x_i$ ($i\neq n$) denotes the amount of travellers starting their trips from node $i$. Further, we let $x_n=-\sum_{i=1}^{n-1} x_i$.

# Wardrop equilibrium principle

# Optimization-based models for Traffic equilibra

## Beckmann's model

## Nesterov \& de Palma's model




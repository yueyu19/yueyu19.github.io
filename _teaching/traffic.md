---
title: 'Static traffic equilibra: Supply-demand model, queuing model, and convex optimization'
collection: teaching
type: "Network optimization"
permalink: /teaching/traffic
venue: online
date: 2021-10-03
location: "Austin, Texas"
mathjax: true
---

Do you know how to numerically predict the traffic patterns in a transportation network? Do you know the connection between traffic equilibra, supply-demand models and queuing models? Find out more in this lecture.

# Prerequisite

[Directed graph](https://en.wikipedia.org/wiki/Directed_graph), [supply-demand model](https://en.wikipedia.org/wiki/Supply_and_demand), [queueing model](https://en.wikipedia.org/wiki/Queueing_theory)

<img src="/images/graph.png" width="250" height="250" img align='right'>

We will first introduce some basic concepts in transportation networks, then discuss two optimization-based models for static traffic equilibra. Thoughout this lecture we will use the example network in the figure on the right. 

# Transportation network basics

A transportation network contains a set of nodes $\mathcal{N}=\\{1, 2, \ldots, n\\}$ and a set of links $\mathcal{L}=\\{1, 2, \ldots, m\\}$. Each link $k$ denotes a pair of ordered distinct nodes $(i, j)$, where node $i$ is the <em>tail</em> of the link, and node $j$ is the the <em>head</em> of the link. Each node denotes an intersetion of roads, and the presence of a link from node $i$ to node $j$ means any travelers can travel from node $i$ to node $j$.

In our example network, we have $n=4$ and $m=5$. 

## Node-link incidence matrix

The node-link incidence matrix $E\in\mathbb{R}^{m\times n}$ describes the topology of the network. The entry $E_{ik}$ in matrix $E$ is associated with node $i$ and link $k$ as follows:

$$E_{ik}=\begin{cases}
    1, & \text{if node $i$ is the tail of link $k$,}\\
    -1, & \text{if node $i$ is the head of link $k$,}\\
    0, & \text{otherwise.}
    \end{cases}$$
    
In our example network, we have

$$E=\begin{bmatrix}
 1 & 1 & 0 & 0 & 0\\
 -1 & 0 & 1 & 1 & 0\\
 0 & -1 & -1 & 0 & 1\\
 0 & 0 & 0 & -1 & -1
\end{bmatrix}.$$

## Paths    

A path is a sequence of distinct links in the same direction that connects a collection of distinct nodes. In our example network, there are three paths from node 1 and node 4, each connects one of the following set of the nodes: $\\{1, 2, 4\\}$, $\\{1, 3, 4\\}$, $\\{1, 2, 3, 4\\}$.

## Flow vector

The flow vector $x\in\mathbb{R}^m$ is an elementwise nonnegative vector, whose entry $x_k$ denotes the amount of travelers exiting link $k$ per unit time (e.g., a day, an hour). 

In our example network, suppose the link flows are given as follows.

| link | flow |
|----|----|
| $(1, 2)$ | 0.6|
| $(1, 3)$ | 0.4|
| $(2, 3)$ | 0.7|
| $(2, 4)$ | 0.7|
| $(3, 4)$ | 1.1|

Then the flow vector $x$ is given by:

$$x=\begin{bmatrix}
0.6\\
0.4\\
0.7\\
0.7\\
1.1
\end{bmatrix}.$$

## Souce-sink vector

For simplicity, we assume that all travellers in the transporttaion network have the same destination, denoted by node $n$. The source-sink vector $s\in\mathbb{R}^n$ describes the the traffic demand in the network. Its $i$-th ($i\neq n$) entry $s_i$ denotes the amount of travellers exiting node $i$ and heading towards node $n$ per unit time (also know as the traffic demand for origin-destination pair $(i, n)$). Further, we let $s_n=-\sum_{i=1}^{n-1} s_i$.

In our example network, suppose that the traffic demand among different nodes is as follows.

|origin-destination pair| demand|
|-------|--------|
| (1, 4) | 1 |
| (2, 4) | 0.8 |
| (3, 4) | 0 |

Then the source-sink vector is given by: 

$$s=\begin{bmatrix}
1\\
0.8\\
0\\
-1.8
\end{bmatrix}.$$

## Flow conservation constraints

The node-link incidence matrix, flow vector and source-sink vector jointly satisfy the <em>flow conservation constraint</em>, given by the following system of linear equations:

$$ Ex=s.$$

These equations state that, at each node, the total incoming flow equals the total outgoing flow. If $s_i>0$, then node $i$ <em>generates</em> an amount of $s_i$ incoming flow. At node $n$, a total amount of $\sum_{i=1}^{n-1} s_i$ incoming flow <em>vanishes</em>. 

You can check that the node-link incidence matrix in equation (2), the flow vector in equation (3), and the source-sink vector in equation (4) satisfy the flow conservation constraints in equation (5).

## Static traffic equilibra and Wardrop equilibrium principle

Static traffic equilibra is a class of models for traffic patterns, where the link flows and traffic demands remain approximately constant during the time of interest. Such equilibra typically happens during rush hours where the congestion in the network is at its the maximum. Wardrop equilibra assume the cost of exiting each link (e.g., time or fuel cost) is a nondecreasing function of its link flow, due to congestion effects.

[Wardrop equilibrium principle](https://en.wikipedia.org/wiki/John_Glen_Wardrop), a key characterization of static traffic equilibra, states that only the paths with the lowest sum of link costs are used by the travelers. The principle agrees with our intuition that travelers would swicth to an alternative path with lower cost, whenever available. 

# Optimization-based models for traffic equilibra

There are different optimization-based models for computing the link flow vector at a static traffic equilibra, each based on different assumptions on the link traffic dynamics. Here we discuss two popular ones. 

## Beckmann model: supply and demand

In Beckmann model, the traffic dynamics on each link is modeled as a market: the supply side corresponds to the link itself, selling the option of exiting the link at a cost, the demand side corresponds to the travelers who wish to exit the link. As the amount of travelers increases, the cost of exiting a link increaes in a way similar to how the price of goods increses with the number of potential buyers. In particular, Beckmann model assumes that the cost of exiting link $k$ is a continuous and non-decreasing function of link flow $x_k$, given by function $\ell_k:\mathbb{R}\to\mathbb{R}$.

Under these assumptions, you can solve for the equilibrium-flow vector using the following convex optimization problem:

$$\begin{array}{ll} \underset{x}{\mbox{minimize}} & \sum_{k=1}^m \int_{\alpha=0}^{x_k} \ell_k(\alpha)d\alpha\\
\mbox{subject to} & Ex=s,\,\, x\geq 0.
\end{array}$$

If $x^\star\in\mathbb{R}^n$ is an optimal solution of the above optimization problem, then $x^\star$ immediately satisfies the flow conservation constraints. Furthermore, using the [Karush–Kuhn–Tucker conditions](https://en.wikipedia.org/wiki/Karush–Kuhn–Tucker_conditions), you can prove that the Wardrop equilibrium principle holds, where the cost of exiting link $k$ at equilibra equals $\ell_k(x_k^\star)$.

First introduced in the 1960s, Bekcmann model has been used widely in evaluating and designing transportation network. However, there are several limitations in this model:
* There is no capacity constraints on link flows. In practice, the flow on each link always has an easy-to-estimate capacity, usually determined by number of lanes and green light time. Without these capacity constraints, Beckmann model can give flow patterns far from reasonable estimates. There are several attemptes to add additional capacity constraints in Beckmann model, see [the paper by Larsson and Patriksson](https://www.sciencedirect.com/science/article/pii/0191261595000167) for an example. However, they caused unwanted side effects, as discussed [the paper by Correa et al](https://pubsonline.informs.org/doi/abs/10.1287/moor.1040.0098). 
* The assumption of link travel cost increases with flow is problematic. Intuitively, the travel cost of a link largely depend on its travel time. And the travel time on a link should increase with the amount of travelers (known as the link loading), not the amount of travelers exiting the link.  

## Nesterov & de Palma model: queuing

As an effort to address the limitations in Beckmann model, Nesterov & de Palma introduced an alternative model. Instead of a market, the traffic dynamics on each link is modeled as a queue. In each queue, the departure rate (or service rate) is upper bounded, and the waiting time is lower bounded. As a result, the flow on each link has an explicit upper bound, and the travel cost on link $k$ has an explicit lower bound. We let $f\in\mathbb{R}^m$ and $c\in\mathbb{R}^m$ denote the elementwise nonnegative vectors for link flow upper bounds and travel cost lower bounds, where the entry $f_k$ and $c_k$ are associated with link $k$.

Under these assumptions, you can solve for the equilibrium-flow vector using the following linear program:

$$\begin{array}{ll} \underset{x}{\mbox{minimize}} & c^\top x\\
\mbox{subject to} & Ex=s,\,\, x\geq 0, \,\,x\leq f.
\end{array}$$

If $x^\star\in\mathbb{R}^n$ is an optimal solution of the above linear program, then $x^\star$ immediately satisfies the flow conservation constraints and link capacity constraints. Furthermore, using the Karush–Kuhn–Tucker conditions, you can prove that the Wardrop equilibrium principle holds, where the cost of exiting link $k$ at equilibra equals $c_k+p_k$. Here $p_k$ is the travel cost increase caused by congestion, which satisfies the following conditions:
* if $x_k^\star<f_k$, then $p_k=0$,
* if $x_k^\star=f_k$, then $p_k\geq 0$.

# Want more references?

The is a hugh literature on Beckmann model. One of my personal favorite is [the book by Patriksson](https://books.google.com/books?hl=en&lr=&id=PDhkBgAAQBAJ&oi=fnd&pg=PP1&dq=traffic+assignment+problem+patriksson&ots=pkeqLoahMN&sig=rrNMyVOh_PHXZbFKlLot72HcbSU#v=onepage&q=traffic%20assignment%20problem%20patriksson&f=false). There are fewer references on Nesterov & de Palma model, see [the paper by Nesterov and de Palma](https://link.springer.com/article/10.1023/A:1025350419398) and a comparison between Beckmann and Nesterove & de Palma model in [the paper by Chudak et al](https://www.research-collection.ethz.ch/handle/20.500.11850/3607). 





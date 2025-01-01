# 01 Lecture

## Terms

- **Agent** - person or AI that interacts with the environment
- **State** - current configuration of the environment
- **Action** - decision made by the agent
- **Transition Model** - describes the possible states after an action
- **Goal State** - desired state

## Search Problem

Search problem has the following components:

- **Initial state** - Initial configuration of the environment
- **Actions** - action/actions that the agent can take
- **Transition model** - describes the possible states after an action
- **Goal test** - a test to determine if the agent has reached the goal state
- **Path cost function** - assigns a numeric cost to for a particular path of actions (money, time, or anything we are trying to minimize)

### Node

A data structure that keep track of,

- A state
- A parent node (the node that generated this node)
- An action (action applied to parent node)
- A path cost (cost to reach this node)

### Approach

- Starts with frontier with the initial state
- Start with an empty explored set
- Repeat
  - If the frontier is empty, then no solution
  - Remove a node from the frontier
  - If the node contains the goal state, then return the solution
  - Expand the node, adding the resulting nodes to the frontier
  - Add the node to the explored set
  - Expand the node, adding the resulting nodes to the frontier if they aren't already in the frontier or explored set

### Search Strategies

- Uninformed Search
  - Breadth-first search
  - Depth-first search
  - Depth-limited search
  - Iterative deepening search
  - Uniform-cost search
- Informed Search
  - Greedy best-first search
  - A\* search

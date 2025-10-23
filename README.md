 # ExpNo:10 Implementation of Classical Planning Algorithm
# NAME: BALAJI V</li>
# REGISTER NUMBER: 25018082</li>

# AIM:
# To implement a classical planning algorithm to find a plan
# from initial state to goal state using a suitable search strategy.


# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>


from copy import deepcopy
from collections import deque

# Function to check if preconditions are satisfied
def preconditions_met(state, preconditions):
    for key, value in preconditions.items():
        if key not in state or state[key] != value:
            return False
    return True

# Function to apply the effect of an action
def apply_effect(state, effect):
    new_state = deepcopy(state)
    for key, value in effect.items():
        new_state[key] = value
    return new_state

# Function to check if goal state is reached
def goal_reached(state, goal_state):
    for key, value in goal_state.items():
        if key not in state or state[key] != value:
            return False
    return True

# The main planning function (using Breadth-First Search)
def find_plan(initial_state, goal_state, actions):
    queue = deque([(initial_state, [])])
    visited = []

    while queue:
        state, plan = queue.popleft()

        # Check if goal is achieved
        if goal_reached(state, goal_state):
            return plan

        # Avoid revisiting states
        state_tuple = tuple(sorted(state.items()))
        if state_tuple in visited:
            continue
        visited.append(state_tuple)

        # Try all possible actions
        for action_name, action_details in actions.items():
            if preconditions_met(state, action_details['precondition']):
                new_state = apply_effect(state, action_details['effect'])
                new_plan = plan + [action_name]
                queue.append((new_state, new_plan))

    return None
    
# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']
```
 Result:</li>

The program successfully implements a classical planning algorithm that determines a valid sequence of actions (plan) to reach the goal state from the initial state.</li>

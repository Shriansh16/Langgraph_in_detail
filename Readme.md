  # LangGraph

Agent workflows are represented as graphs.

## Components

### State
Represents the current snapshot of the application. Think of it as a central store that holds all relevant data during the workflow execution.

### Nodes
These are Python functions that represent agent logic. They:
- Receive the current state as input
- Perform some operation (like processing a task)
- Return an updated state

### Edges
These are Python functions that determine which node to execute next, based on the current state.

Edges can be:
- Conditional (based on state values)
- Fixed (always go to the same node)

## Creating a Graph (5 Steps)

1. **Define the State class**
   - This class defines what data you want to track and pass between nodes.

2. **Start the Graph builder**
   - Initialize the LangGraph builder to begin constructing your workflow.

3. **Create Nodes**
   - Define your logic steps using Python functions and register them as nodes.

4. **Create Edges**
   - Define how nodes connect and what path to follow using conditional logic or fixed paths.

5. **Compile the graph**
   - Finalize your graph to make it executable.

## 🔄 State Management in LangGraph

- **State is immutable**
  - You will never change the content of a state object directly.
  - Once a value is assigned, you don't modify it—you always return a new updated state instead.
  - This immutability helps in debugging and ensures clean and predictable state transitions.

- **Reducers**
  - For each field in your state, you can specify a special function called a reducer.
  - When you return a new state, LangGraph uses the reducer to combine the new value for a field with the existing state.

### 👉 This enables LangGraph to:
- Run multiple nodes in parallel, and
- Combine their state updates without overwriting each other.

## 🧠 Example
If two different parts of your code want to update the same field (e.g. a list), the reducer decides how to merge those updates.
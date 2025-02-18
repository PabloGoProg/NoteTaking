### Elements of a Prompt
1. **Instruction:** Task for LLM to do -- provides a task, description or instruction for how the model should perform,
2. **Context:** External information to guide the model.
3. **Input data:** Input for which you want a response.
4. **Output indicator:** Output type or format.
#### Sample
```
Given a list of customer orders and available inventory, determine which orders can be fulfilled and which items have to be restocked.  (Instruction)
  
This task is essential for inventory management and order fulfillment processes in ecommerce or retail businesses.  (Context)

(Input data)
Orders:

- Order 1: Product A (5 units), Product B (3 units)
- Order 2: Product C (2 units), Product B (2 units)

  
Inventory:

- Product A: 8 units
- Product B: 4 units
- Product C: 1 unit

(Output indicator)
Fulfillment status:
```

### Negative Prompting
Sometimes is easier to tell a model what should avoid to guide it to a desire output, including what you don't want to include in the output.
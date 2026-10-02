# What is VNPC?

VNPC stands for **Very Natural Pseudo Code**.  
Its function is to convert a program code into human language written according to the workflow of the program's purpose.

The result is made into a workflow structure resembling a sequence of events (plot), accompanied by:

- error handling,
- use of variables from the current file or other code,
- mathematical formulas or processing logic,
- as well as the expected result of an operation/function.

## Main Principles

1. **Default sequential**  
   The plot is written sequentially from top to bottom.

2. **Top-down design**  
   Start from the big goal, then go down to step details.

3. **Simplify without misleading**  
   VNPC may simplify, but must not omit important details that change the meaning of the program's logic.

4. **Async is not an absolute prohibition**  
   Async is not recommended if irrelevant, because it adds cognitive load.  
   However, if the modeled system is indeed asynchronous, async must still be represented.  
   This can be done with markers such as `[async]`, `[await]`, `[non-blocking]`, `[callback]`, or `[event]`, while still maintaining the narrative flow from top to bottom.

5. **Focus on logical reasoning**  
   VNPC is used to understand flow, design programs, and trace logic errors when operation results do not match expectations.

## VNPC Writing Format

VNPC can be used to:

- convert existing code into human language,
- design a program from scratch,
- document workflows,
- help review and debug logic.

Example of writing async in VNPC:

```text
1. Receive a request from the user.
2. Validate input. If it fails, send 400.
3. [async] Start a query to the database.
4. [non-blocking] Do not block the process; serve other requests.
5. [await] When the query finishes, send 200 along with the data.
6. If an error occurs during the query, send 500 and log it.
```
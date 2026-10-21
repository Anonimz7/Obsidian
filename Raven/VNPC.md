# What is VNPC?

VNPC stands for Very Natural Pseudo Code.
Its function is to convert a program code into human language written according to the workflow of the program's purpose.

The result is a workflow structure resembling a sequence of events (plot), covering:

- error handling,
- edge cases,
- variables from the current file or other code,
- mathematical formulas or processing logic,
- expected result of an operation or function.

## Main Principles

1. Default sequential
   The plot is written sequentially from top to bottom.

2. Top-down design
   Start from the big goal, then go down to step details.

3. Simplify without misleading
   VNPC may simplify, but must not omit details that change the meaning of the program's logic—including asynchronous behavior when it is present.

4. Narrative coherence
   Steps are not a checklist. Each step should follow from the previous one logically, the way a plot moves—cause and effect, condition and consequence, premise and conclusion. When the connection is not self-evident, state it in human language: "because X, Y follows," "if X, then Y," "after X completes, Z starts." The reader should be able to follow why step N follows step N-1 without re-reading.

5. Focus on logical reasoning
   VNPC is used to understand flow, design programs, and trace logic errors when operation results do not match expectations.

## Use Cases

VNPC can be used to:

- convert existing code into human language,
- design a program from scratch,
- document workflows,
- help review and debug logic.
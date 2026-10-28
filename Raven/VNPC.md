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

1. Start with the program's purpose
   Begin the VNPC with a clear statement of what the program is for. Do not describe the document's format, structure, or rules to the reader. The structure should be self-evident from the writing itself.

2. Default sequential
   The plot is written sequentially from top to bottom.

3. Top-down design
   Start from the big goal, then go down to step details.

4. Simplify without misleading
   VNPC may simplify, but must not omit details that change the meaning of the program's logic—including asynchronous behavior when it is present.

5. Narrative coherence
   Steps are not a checklist. Each step should follow from the previous one logically, the way a plot moves—cause and effect, condition and consequence, premise and conclusion. When the connection is not self-evident, state it in human language: "because X, Y follows," "if X, then Y," "after X completes, Z starts." The reader should be able to follow why step N follows step N-1 without re-reading.

6. Focus on logical reasoning
   VNPC is used to understand flow, design programs, and trace logic errors when operation results do not match expectations.

7. Numbered sections with reconstruction
   When analyzing existing code, the narrative naturally unfolds in numbered sections (Bagian 1, Bagian 2, and so on), each covering one topic: state, DOM references, initialization, a function, or a workflow. At the end of each section, the core logic is mirrored in neutral pseudocode with informative names. This reconstruction is brief and shows the essential flow, not every line. It is a mirror of understanding, not a copy, and it appears inline at the end of each section so the explanation and its mirror stay together.

8. Closing summary
   End the entire document with a high-level summary of the whole flow. After all the detailed sections and reconstructions, provide a final "one-breath" recap (either a short narrative paragraph or a brief list) that ties the cause-and-effect chain together from start to finish. This allows the reader to step back and see the big picture clearly after going through the details.

## Use Cases

VNPC can be used to:

- convert existing code into human language,
- design a program from scratch,
- document workflows,
- help review and debug logic.
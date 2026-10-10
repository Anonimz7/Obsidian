# VNPC AGENT INSTRUCTIONS

## WHAT IS VNPC?

VNPC stands for Very Natural Pseudo Code.
Its function is to convert a program code into human language written according to the workflow of the program's purpose.

## VNPC FORMAT RULES

1. Default sequential: plot written top-down, in order.

2. Top-down design: start from the big goal, then descend into detail.

3. Simplify without misleading: VNPC may simplify, but never remove detail that changes the logical meaning. Do not include unnecessary loops, conditionals, or data structures—if a step does not affect the outcome, remove it or collapse it.

4. Async is not forbidden, but is discouraged when irrelevant. If the modeled system is truly asynchronous, represent it with markers such as [async], [await], [non-blocking], [callback], or [event], while keeping the narrative flow top-down.

5. Focus on logic reasoning: VNPC is used to understand flow, design programs, and trace logic errors when operation results do not match expectations. The logic must be testable and traceable—every step should be verifiable in isolation or by the verification point defined in rule 12.

6. VNPC output must include, where relevant:
    a. Error handling.
    b. Variables used (from the current file or other code).
    c. Mathematical formulas or processing logic.
    d. Expected result of an operation or function.
    e. Edge cases explicitly: empty input, null, overflow, or boundary conditions.

7. VNPC use cases:
    a. Convert existing code into human language (reverse).
    b. Design a program from scratch (forward).
    c. Document a workflow.
    d. Assist logic review and debugging.

## PROJECT STRUCTURE TREE

8. VNPC output includes project structure trees showing files and folders only. No function names, no call hierarchies, no dependency arrows. Tree is structural, not behavioral.

9. Two types of tree:
    a. Contextual tree: shows only project files and folders directly involved in the logic being discussed. Output one contextual tree per distinct logic that crosses file boundaries. If a logic is self-contained in one file, skip the contextual tree for that logic. External libraries (pandas, react, lodash) are not shown—only files within the project.
    b. Full tree: shows the entire project structure, for overall understanding. Output the full tree exactly once per VNPC document, regardless of how many contextual trees exist.

10. Order: all contextual trees first (in order of appearance in the numbered steps), then the single full tree, as the final section of the VNPC document.

11. Format: ASCII tree using ├── └── │ characters. Mermaid allowed only if the user requests it. For VNPC design: contextual tree shows planned files for the discussed logic; full tree shows the overall planned structure. For VNPC analysis: contextual tree shows actual files involved in the discussed logic; full tree shows the actual project structure. If a tree cannot be determined (incomplete context), state: "Tree unavailable. Reason: [reason]." and skip that tree only. Do not guess. Depth: full depth unless the user requests a limit. If depth exceeds 5 levels, split by module.

## VERIFICATION POINT

12. Verification point:
    a. Include a verification point for each function whose output can be checked in isolation, without running the entire system.
    b. Placement: immediately after the step that describes the function, not at the end of the document.
    c. Format: compact block, maximum 5 lines.
       Function: [name]
       Input: [minimum input]
       Expected: [output]
       Pass: [condition]
       Run: [execution mechanism]
    d. The Run field is mandatory. It must state how to execute the verification: assertion, test command, endpoint call, REPL snippet, or other mechanism appropriate to the project type and language.
    e. If the execution mechanism is unknown (framework not yet chosen, environment not defined), state: "Run: unavailable. Reason: [reason]." and continue.
    f. If a function cannot be verified in isolation (depends on external state, requires full app context), skip it. Do not force a verification point.
    g. If the verification method is unknown entirely, state: "Verification point unavailable. Reason: [reason]." and skip.

## OUTPUT FORMAT

13. Direct answer only. No introductions, conclusions, or follow-up questions.

14. VNPC output is written as numbered steps in plain text, without code fences unless the user explicitly requests a code block.

15. If a diagram is needed, use Mermaid.

16. If a table is needed, use Markdown table.

17. If reasoning is required, present steps 1, 2, 3 concisely.

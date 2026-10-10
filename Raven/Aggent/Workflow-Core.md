# WORKFLOW CORE

## MODE SELECTION

1. At the start of each turn, five modes are possible: phase mode, bypass mode, auto mode, research mode, discussion mode.

2. If the user states a phase → phase mode (rules 11–49).

3. If the user prefixes "Bypass:" or "Direct:" → bypass mode (rule 58).

4. If the user prefixes "Research:" → research mode (rule 71).

5. If the user prefixes "Discuss:" → discussion mode (rule 86).

6. If the user replies "Auto" → auto mode (rule 64).

7. If neither is stated, offer once: "No phase stated. Reply 'Auto' for automatic phase selection, 'Research:' for research mode, 'Discuss:' for discussion mode, or state a phase."

8. Do not infer. Do not guess. Wait for the user's reply.

## PHASE DETECTION

9. The user must state the phase at the start of every turn, including turns within the same phase (e.g. "Phase 4. [message]").

10. If the phase is not stated, reply: "State the phase." and stop. Do not infer the phase from context. Do not guess. A phase may span multiple turns; the phase label must be repeated each turn.

## PHASE 0 — CONTEXT BUILDING

11. Phase 0 is used when code already exists and context must be built before design. Skip Phase 0 for greenfield projects.

12. Two sub-phases exist, called separately:
    a. Phase 0. Inspect all | {target} → produces inspection_notes.md
    b. Phase 0. Reverse all | {target} → produces design_vnpc_reverse.md from actual code

13. Scope:
    a. "all" means the entire project.
    b. "{target}" means a module, folder, or file specified by the user.

14. Size assessment:
    a. At the first turn of Phase 0, assess whether the scope fits one turn.
    b. If the scope is small, proceed directly and output the result file.
    c. If the scope is large (many modules, large codebase, complex dependencies), create a task file:
       - task_inspect.md for Phase 0. Inspect
       - task_reverse.md for Phase 0. Reverse
    d. Task file structure: task ID, description, dependency, status (pending/done). Same structure as flow_task.md.

15. Verification turn (once):
    a. In the turn after size assessment, state: "Size assessment: [small/large]. [one-sentence reason]."
    b. The user may confirm or correct. The model may also self-correct if new information emerges.
    c. After this single verification turn, no further re-verification is done.

16. Multi-turn execution:
    a. If a task file was created, work one sub-task per turn. Update the task file after each completed sub-task.
    b. The phase label "Phase 0. Inspect" or "Phase 0. Reverse" must be repeated each turn.
    c. When all sub-tasks are done, output the final result file.

17. Output files:
    a. Phase 0. Inspect → inspection_notes.md (system map: modules, dependencies, integration points, available verification points).
    b. Phase 0. Reverse → design_vnpc_reverse.md (VNPC of actual code, with verification points as documentation). Phase 1 uses design_vnpc.md separately; reverse output never overwrites Phase 1 output.
    c. If scope is "all" and multiple modules exist, output one file per module: inspection_notes_{module}.md or design_vnpc_reverse_{module}.md.
    d. If scope is "{target}", output a single file.

18. Transition:
    a. End with: "Phase 0 complete. Send a new message to start Phase 1, or stop here for documentation only."
    b. The user may ignore the offer if only documentation is needed.

19. Phase 0 does not modify code. It is read-only.

## PHASE 1 — DESIGN (VNPC)

20. Produce or read the design. Write it to design_vnpc.md.

21. End with: "Phase 1 complete. Send a new message to start Phase 2."

22. Do not execute Phase 2 in this turn. If the user requests it, reply: "Phase 1 complete. Send a new message to start Phase 2." and stop.

## PHASE 2 — FLOW TASK

23. Read design_vnpc.md before building flow_task.md.

24. flow_task.md structure: task ID, description, dependency, status (pending/done).

25. End with: "Phase 2 complete. Send a new message to start Phase 3."

26. Do not execute Phase 3 in this turn.

## PHASE 3 — BUILDING

27. Write code based on flow_task.md.

28. Update flow_task.md after each completed task. One task = one update.

29. No debugging. No bug fixing. No code execution. No test run. No static analysis beyond syntax check. Environment setup is allowed only if required to run the code. If a potential bug is noticed, note it in flow_task.md as a comment under the related task. Do not analyze, do not propose a fix.

30. End with: "Phase 3 complete. Send a new message to start Phase 4."

## PHASE 4 — DEBUGGING

31. Analyze the code. Do not modify any code file under any circumstance.

32. Allowed: point to line, quote code, explain hypothesis. Do not suggest fixes. Only document symptom, suspected cause, file/line, and verification status. If a fix idea appears, record it as a hypothesis, not as a recommendation.

33. Phase 4 may span multiple turns. The phase label must be repeated each turn.

34. Collect findings across all Phase 4 turns. Write to the debug file only when the user says "session end" or "tutup sesi".

35. Debug file naming: flow_task_debug_bugN.md, where N is the bug order number.

36. Debug file structure: (1) symptom, (2) suspected cause, (3) file/line, (4) verification status.

37. End with: "Phase 4 complete. Send a new message to start Phase 5."

## PHASE 5 — FIX

38. Read the relevant flow_task_debug_bugN.md.

39. Apply only fixes derived from that file.

40. If the debug file provides insufficient basis, reply: "Insufficient basis for fix." and stop. Do not invent solutions. Insufficient basis is a finding, not a change—it does not produce a changelog entry.

41. No testing. No verification. No re-analysis.

42. To close Phase 5 and write the changelog, the user says "session end" or "tutup sesi". Output the changelog entry per rule 50.

43. If no "session end" is stated, do not write a changelog entry. End the turn without changelog output.

## PHASE DISCIPLINE

44. Never merge phases within one turn.

45. Never skip phases.

46. Never fix code during Phase 4.

47. Never test during Phase 5.

48. If the user attempts to violate the sequence, reply: "Sequence violation: [phase]." and stop.

49. If the model's output contains an implicit fix (e.g. "the cause is X, so it should be Y"), treat it as a violation. Reply: "Implicit fix detected. Rephrase as hypothesis only." and stop.

## CHANGELOG

50. Maintain changelog.md in the project root, following Keep a Changelog format.

51. Trigger: write a changelog entry when the user says "session end" or "tutup sesi" during Phase 5, or when the user explicitly requests a release. Do not write at any other time.

52. Entry structure:
    ## [version] - YYYY-MM-DD
    ### Added
    ### Changed
    ### Fixed
    ### Removed

53. Version format: semantic versioning (MAJOR.MINOR.PATCH).

54. Only include user-visible changes: features, behavior, fixes that affect use. Exclude internal refactors, comments, formatting. Exclude unresolved cases ("insufficient basis for fix")—they are findings, not changes.

55. Do not invent version numbers. Do not use [Unreleased] unless the user explicitly requests it. If the user has not stated a version, ask once: "State the version number." and stop.

56. Output the entry only. The user is responsible for appending to changelog.md. Do not add notes on what was included or excluded.

57. Do not write changelog entries at any other phase.

## BYPASS MODE

58. The user may suspend the phased protocol for a single turn by prefixing the message with "Bypass:" or "Direct:".

59. At the start of the response, state: "Bypass mode. Phase protocol suspended."

60. In bypass mode, rules 9–57 do not apply. Respond per Instructions.md and rules 1–8.

61. Bypass mode lasts one turn. The next turn returns to mode selection (rule 1) unless bypass is repeated.

62. Bypass mode does not disable verification, epistemic labels, or safety rules in Instructions.md.

63. Bypass mode does not produce phase artifacts: no design_vnpc.md, no design_vnpc_reverse.md, no inspection_notes.md, no flow_task.md, no debug files, no changelog.

## AUTO MODE

64. When the user replies "Auto", classify the task using the table below. State: "Auto → Phase N. [one-sentence reason]."

65. Execute per that phase's rules.

66. If confidence < 90%, reply: "State the phase." and stop.

67. If the task spans more than one phase, reply: "Multiple phases detected. State one phase." and stop.

68. Auto mode applies to the current turn only. Next turn returns to mode selection (rule 1).

69. Auto mode never merges phases, never skips phases, never bypasses phase rules (rules 9–57).

70. User may override mid-turn: "Override: Phase M" switches to Phase M.

Classification table:
    - Context building from existing code, inspect or reverse → Phase 0
    - Design, architecture, VNPC, "what should this do" → Phase 1
    - Task list, flow, dependencies, "what needs to happen" → Phase 2
    - Write code, implement, build → Phase 3
    - Analyze, debug, find cause, "why does this fail" → Phase 4
    - Apply fix from debug file → Phase 5
    - git, read file, list files, calculate, single-shot explain (non-phase) → Direct

## RESEARCH MODE

71. Trigger: user prefixes the message with "Research:".

72. Purpose: gather, compare, and synthesize information. Not for building, not for fixing.

73. At the start, state: "Research mode. [topic]."

74. Research mode may span multiple turns. The prefix "Research:" must be repeated each turn.

75. Allowed: web search, source comparison, data gathering, hypothesis exploration, question formulation, literature-style summary.

76. Not allowed: writing code, modifying code, creating design_vnpc.md, creating design_vnpc_reverse.md, creating inspection_notes.md, creating flow_task.md, creating debug files, creating changelog entries. Research is read-only.

77. Epistemic labels from Instructions.md 11 apply. Every claim must carry [verified], [inferred], [speculative], or [uncertain]. Irrational factors labeled [irrational-factor].

78. Output structure: state the question, list findings with sources, note contradictions, conclude with what is known and what remains open.

79. End with: "Research continues. Send another Research: message, or state a phase."

80. To close research, user says "session end" or "tutup sesi". Output: research_notes.md with (1) research code, (2) topic, (3) findings, (4) sources, (5) open questions, (6) epistemic status per finding.

81. Research code format: #RND-N, where N is a sequential integer starting from 1. Every research session gets a unique code. If multiple research sessions occur, increment N (RND-1, RND-2, RND-3).

82. The research code must appear at the top of research_notes.md and in any cross-reference to that research.

83. If the user starts a new research session without closing the previous one, treat it as continuation of the same code. Only increment N when the user says "session end" or "tutup sesi" and then starts a new Research: session.

84. Research mode does not transition automatically to any phase. User must state the phase next turn.

85. Research mode does not bypass verification, epistemic labels, or anti-slop rules.

## DISCUSSION MODE

86. Trigger: user prefixes the message with "Discuss:".

87. Purpose: exchange ideas, test arguments, explore trade-offs. Not for gathering external data, not for building.

88. At the start, state: "Discussion mode. [topic]."

89. Discussion mode may span multiple turns. The prefix "Discuss:" must be repeated each turn.

90. Allowed: reasoning exchange, counter-arguments, thought experiments, trade-off analysis, hypothesis testing between user and model.

91. Not allowed: web search, source gathering, writing code, modifying code, creating phase artifacts.

92. Epistemic labels apply only when factual claims are made. Pure reasoning does not require labels.

93. Discussion does not produce files. No research_notes.md, no design_vnpc.md, no flow_task.md.

94. End with: "Discussion continues. Send another Discuss: message, or state a mode."

95. Discussion mode does not transition automatically to any phase or mode.

96. Discussion mode does not bypass verification, epistemic labels, or anti-slop rules.
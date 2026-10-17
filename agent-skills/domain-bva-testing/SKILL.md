---
name: domain-bva-testing
description: >-
  Design and review software test cases using equivalence partitioning and
  Boundary Value Analysis. Use when analyzing a feature requirement, selecting
  representative inputs, documenting expected results, or reviewing execution
  evidence and test outcomes.
---

# Domain Testing and Boundary Value Analysis

Use this workflow to create traceable, defensible test cases from a feature requirement. Treat the requirement, source code, UI/API behavior, and the tester assumptions as separate evidence sources.

## 1. Establish the oracle

1. Read the applicable requirement and its referenced security, API, UI, or data rules. Identify the exact requirement IDs and quote or paraphrase only the relevant clauses.
2. Record each explicit constraint: data type, allowed values, requiredness, minimum/maximum, length, role, state, and expected observable result.
3. Mark information that is missing or conflicting as **unspecified**. Inspect the implementation or schema for context, but do not silently turn implementation behavior into a requirement. Ask for clarification when the expected behavior cannot be established.
4. For an unspecified behavior, either label the test exploratory or leave its expected result unresolved. Do not mark it Passed/Failed or report a bug without a justified oracle.

## 2. Partition the domain

For every input or relevant state:

1. Identify equivalence classes that should produce the same behavior.
2. Separate valid and invalid classes only when the requirement supports that distinction.
3. Select a representative value for each class and explain why it represents that class.
4. Consider interactions between fields, roles, authentication, persisted state, and prior actions when they can change the outcome.
5. Avoid redundant cases unless they check a distinct requirement or risk.

For a category name, possible input partitions include ordinary non-empty names, empty input, whitespace-only input, and any explicitly constrained length or character set. If the requirement only says the name is required and cannot be empty, do not assume whitespace is empty after trimming unless the specification says so.

## 3. Apply Boundary Value Analysis

1. Derive boundaries from explicit requirements or verified contracts (for example, a minimum, maximum, length limit, or allowed quantity range).
2. For a numeric boundary `b`, consider `b-1`, `b`, and `b+1` when meaningful and safe. For a range `[min,max]`, inspect values just below, at, just above each endpoint.
3. For string length `n`, consider lengths `n-1`, `n`, and `n+1`, and empty input only when relevant.
4. For state transitions, test immediately before and after the specified transition condition.
5. If no limit is specified, do not invent a boundary. Record the gap and use exploratory values only with an appropriately qualified expected result.

## 4. Write executable cases

Each case should contain:

- a stable, unique ID;
- requirement or contract source;
- preconditions and role;
- exact input data;
- numbered actions that another tester can repeat;
- an observable expected result;
- the rationale for the partition or boundary;
- an evidence location and, after execution, actual result and status.

Keep expected results testable: state the message, route, response code/body, persisted record, or state change to inspect. Do not mix expected and actual results.

## 5. Execute safely and classify evidence

1. Confirm the correct test environment, role, and starting state. Use isolated, disposable test data when writes are involved.
2. Capture evidence that shows the relevant input/action and outcome. Redact credentials, cookies, bearer tokens, and personal data.
3. Clean up only records created by the test, then verify seeded or unrelated data remains intact.
4. Assign statuses from observed evidence:
   - **Passed:** actual result matches a requirement-based expected result;
   - **Failed:** actual result reproducibly violates that expected result;
   - **Inconclusive:** the oracle or evidence is insufficient to decide;
   - **Not Executed:** no execution occurred (including a deliberately skipped case).
5. A UI success toast alone does not prove a backend state change. Inspect the relevant API or persisted state when required by the case.
6. Stop if the environment or baseline is unexpected, or if continuing could affect unrelated data.

## 6. Report and reconcile

1. Record each case once in the project source-of-truth test-case file, preserving its ID and evidence path.
2. Report a bug only for a reproducible, requirement-backed failure. Include steps, expected/actual results, environment, and evidence. Keep observations and unspecified behavior separate from confirmed bugs.
3. Update the feature analysis, bug register, AI review, and summary counts when a result changes. Reconcile totals so each designed case has exactly one current status.
4. Distinguish cases designed from cases executed. Do not count exploratory suggestions as designed/executed cases unless they are formally added and run.

## Worked example: category name required

Assume the requirement says a category name is required and cannot be empty, but says nothing about trimming whitespace:

| Input | Expected basis | If the app accepts it |
|---|---|---|
| `A` | Non-empty; valid representative | Pass if the category is created as expected |
| empty string | Explicitly disallowed | Fail; record the reproducible violation |
| three spaces | Whitespace treatment is unspecified | Inconclusive/exploratory; do not claim a bug |

This example illustrates how to keep an observed result separate from the requirement oracle. Replace its assumptions with the actual feature specification before using it for another system.

---
title: Finding Counterexamples
weight: 1
---

testcase.ac runs submitted code and reference code on the same input and looks
for an input where their outputs differ.

## How to use it

### Run a saved problem

On the home page, you can search by problem id, problem type, or title:
[https://testcase.ac/](https://testcase.ac/)

To run counterexample search for a problem, the problem directory in the
repository needs these files:

- `correct_*`: at least one reference solution.
- `generator_*`, `singlegen_*`, or `testcase_*.txt`: at least one input provider.
- `checker.cpp`: required for special-judge problems, when `metadata.yaml` has `isSpecialJudge: true`.

If counterexample search is available for the problem, paste your submitted code
and click "Find counterexample".

### Run without a saved problem

Link: [https://testcase.ac/custom-invocation](https://testcase.ac/custom-invocation)

The `Custom Invocation` page can run code that is not registered in the
repository. You directly enter submitted code, reference code, execution limits,
generators, text testcases, and an optional checker.

## How it runs

testcase.ac creates inputs with generators, single generators, and text
testcases. Then it runs both the submitted code and reference code with each
input.

For each input, testcase.ac compares the submitted code output with the
reference code output. Without a checker, it compares outputs in a BOJ-like way:
some differences between spaces and newlines are ignored, and whitespace at the
end of the output is ignored. With a checker, the checker receives the input,
submitted output, and reference output, then decides whether the submitted
output is accepted.

### Reading results

When testcase.ac finds counterexamples, it separates wrong-output samples and
execution-failed samples. It shows up to three samples for each kind, removes
duplicates, and sorts shorter samples first.

`No counterexample found` means the submitted code and reference code both ran
successfully and printed the same output for the tried inputs. It is not a proof
that the submitted code is always correct.

## Common limits

- Counterexample search is limited to 90 seconds, including compile time.
- If counterexamples or execution failures happen too often, testcase.ac may stop before the requested number of tries. This prevents counterexample search from taking too long.

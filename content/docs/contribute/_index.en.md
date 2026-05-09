---
title: Contributing
weight: 2
---

To contribute problem data to testcase.ac, send a PR directly to the `testcase/`
directory in the GitHub repository.

## How to contribute

### Step 1: Add problem data locally

Fork the [testcase-ac/testcase-ac](https://github.com/testcase-ac/testcase-ac)
repository.

Each problem is added under `testcase/<problemType>/<externalId>/`. For example,
BOJ problem 1000 is added under
[testcase/boj/1000/](https://github.com/testcase-ac/testcase-ac/tree/main/testcase/boj/1000).

- Current `problemType` values include `boj` and `koi`, and other types can also be added.

Add the needed files to each problem directory. See
[`testcase/FORMAT.en.md`](https://github.com/testcase-ac/testcase-ac/blob/main/testcase/FORMAT.en.md)
for more detail.

- `metadata.yaml`: problem metadata. It contains the title, original problem link, execution limits, special-judge flag, and so on.
- `correct_*`: reference solution.
- `generator_*`: generator that receives a seed and creates random input.
- `singlegen_*`: single generator that creates one large fixed input.
- `testcase_*.txt`: fixed testcase.
- `validator.cpp`: input validator using `testlib.h`.
- `checker.cpp`: code used for special-judge problems to decide whether submitted output is accepted.

### Step 2: Verify it

Run this command locally to verify the changed problem directory.

```bash
./tests/verify/run_problems.sh testcase/boj/1000
```

Or, when you open a PR, the `Verify contributed problems` GitHub Actions
workflow verifies the changed problem directory. You can check the CI definition
at [.github/workflows/verify-problems.yml](https://github.com/testcase-ac/testcase-ac/blob/main/.github/workflows/verify-problems.yml).

Verification checks the following items:

- Generator / single-generator / fixed testcase outputs must pass `validator.cpp`.
- Each `generator_*` must produce the same output for the same seed.
- Each `singlegen_*` must produce the same output across repeated runs.
- If there are multiple `correct_*` files, their results must match on the same input.

### Step 3: Send a PR

Send a PR to the testcase-ac repository from the
[pull requests page](https://github.com/testcase-ac/testcase-ac/pulls). There is
currently no PR template, so write the description freely.

### Step 4: Merge the PR

The PR can be merged automatically with `/merge-testcase`, or manually by a
maintainer.

The `/merge-testcase` automatic merge checks these conditions:

- If a non-maintainer author requests automatic self-merge, they must already have at least one merged PR in this repository.
- All changed files must be inside problem directories under `testcase/`.
- Every changed problem directory must contain `validator.cpp`.
- The `Verify contributed problems` CI must pass.

Even if automatic merge fails, a maintainer can still merge the PR manually
after checking the situation. Examples include first-time contributors, or an
existing data issue that prevents CI from passing.

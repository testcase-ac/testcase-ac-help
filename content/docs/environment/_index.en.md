---
title: Runtime Environment
weight: 3
---

testcase.ac counterexample search runs on AWS Lambda.

- Server: AWS Lambda container
- Container definition: [`deploy/stresser.Dockerfile`](https://github.com/testcase-ac/testcase-ac/blob/main/deploy/stresser.Dockerfile)
- Architecture: `x86_64`
- Counterexample search time limit: 90 seconds

You can check the detailed deployment settings in
[`deploy/terraform/stresser`](https://github.com/testcase-ac/testcase-ac/tree/main/deploy/terraform/stresser).

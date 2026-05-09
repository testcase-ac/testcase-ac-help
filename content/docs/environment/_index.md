---
title: 실행 환경
weight: 3
---

testcase.ac의 반례 찾기는 AWS Lambda에서 실행됩니다.

- 서버: AWS Lambda 컨테이너
- 컨테이너 정의: [`deploy/stresser.Dockerfile`](https://github.com/testcase-ac/testcase-ac/blob/main/deploy/stresser.Dockerfile)
- 아키텍처: `x86_64`
- 반례 찾기 시간 제한: 90초

구체적인 배포 설정은 [`deploy/terraform/stresser`](https://github.com/testcase-ac/testcase-ac/tree/main/deploy/terraform/stresser)에서 확인할 수 있습니다.

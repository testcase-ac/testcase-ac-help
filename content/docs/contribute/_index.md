---
title: 기여하기
weight: 2
---

testcase.ac의 문제 데이터에 기여하려면 GitHub 리포지토리의 `testcase/` 디렉터리에 직접 PR을 보내면 됩니다.

## 기여 방법

### 1단계: 로컬에서 문제 데이터 추가

[testcase-ac/testcase-ac](https://github.com/testcase-ac/testcase-ac) 리포지토리를 포크합니다.

각 문제는 `testcase/<problemType>/<externalId>/` 디렉터리에 추가합니다. 예를 들어, BOJ 1000번 문제는 [testcase/boj/1000/](https://github.com/testcase-ac/testcase-ac/tree/main/testcase/boj/1000) 디렉터리에 추가합니다.

- `problemType`은 현재 `boj`, `koi`가 있으며, 다른 유형도 추가할 수 있습니다.

각 문제 디렉터리에는 필요한 파일을 추가합니다. [`testcase/FORMAT.md`](https://github.com/testcase-ac/testcase-ac/blob/main/testcase/FORMAT.md)에서 더 자세한 내용을 확인해 주세요.

- `metadata.yaml`: 문제 메타데이터입니다. 제목, 원문 링크, 실행 제한, 스페셜 저지 여부 등을 작성합니다.
- `correct_*`: 정답 코드입니다.
- `generator_*`: 시드를 받아 랜덤 입력을 만드는 제너레이터입니다.
- `singlegen_*`: 큰 고정 입력 하나를 만드는 단일 제너레이터입니다.
- `testcase_*.txt`: 고정 테스트케이스입니다.
- `validator.cpp`: `testlib.h`를 사용하는 입력 밸리데이터입니다.
- `checker.cpp`: 스페셜 저지 문제에서 제출 코드의 출력이 정답으로 인정되는지 판단하는 코드입니다.

### 2단계: 검증하기

로컬에서 아래 명령어를 실행해 변경한 문제 디렉터리를 검증합니다.

```bash
./tests/verify/run_problems.sh testcase/boj/1000
```

또는 PR을 열면 `Verify contributed problems` GitHub Actions가 변경된 문제 디렉터리를 위 명령어를 사용해 검증합니다. 구체적인 CI 정의는 [.github/workflows/verify-problems.yml](https://github.com/testcase-ac/testcase-ac/blob/main/.github/workflows/verify-problems.yml)에서 확인할 수 있습니다.

검증에서는 다음 항목을 확인합니다.

- 제너레이터 / 단일 제너레이터 / 고정 테스트케이스의 출력이 `validator.cpp`를 통과해야 합니다.
- `generator_*`는 같은 시드에서 같은 출력을 만들어야 합니다.
- `singlegen_*`는 여러 번 실행해도 같은 출력을 만들어야 합니다.
- 여러 `correct_*` 코드가 있으면 같은 입력에서 결과가 일치해야 합니다.

### 3단계: PR 보내기

[https://github.com/testcase-ac/testcase-ac/pulls](https://github.com/testcase-ac/testcase-ac/pulls) 페이지에서 testcase-ac 리포지토리에 PR을 보냅니다. 현재는 따로 PR 템플릿이 없으니 자유롭게 작성해 주세요.

### 4단계: PR 머지

`/merge-testcase`로 자동 머지하거나, 관리자가 직접 머지할 수 있습니다.

`/merge-testcase` 자동 머지는 다음 조건을 확인합니다.

- 관리자가 아닌 작성자가 직접 자동 머지를 요청하는 경우, 이 리포지토리에서 이전에 머지된 PR이 하나 이상 있어야 합니다.
- 변경 파일이 모두 `testcase/` 아래의 문제 디렉터리에 있어야 합니다.
- 변경된 각 문제 디렉터리에 `validator.cpp`가 있어야 합니다.
- `Verify contributed problems` CI가 통과해야 합니다.

자동 머지가 실패해도 상황에 따라 관리자가 확인한 뒤 직접 PR을 머지할 수 있습니다. (예: 첫 기여자, 기존 데이터 오류로 CI를 통과할 수 없는 경우)

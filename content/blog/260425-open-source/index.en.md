---
title: "Releasing testcase.ac as open source"
date: 2026-04-25T00:00:00+09:00
---

TL;DR: Both the data and the web service code of testcase.ac are going open source. Visit [next.testcase.ac](https://next.testcase.ac) for a preview of the new testcase.ac.


## Introduction

Hello, I'm the developer of [testcase.ac](http://testcase.ac).

On April 15, the shutdown of Baekjoon Online Judge (hereafter BOJ[^1]) was announced.
BOJ has been the most familiar service for almost anyone in Korea who has ever tried solving algorithm problems. I myself once spent my days finding joy in solving problems on BOJ, so this announcement was, just like it was for many others, a very sad and disappointing piece of news to me.

[^1]: It is now time to return the name "Baekjoon." https://www.acmicpc.net/board/view/165922

Naturally, I started thinking about how to carry testcase.ac forward. Until BOJ's shutdown was announced, testcase.ac was getting around 500 visitors per day on average, with about 400 of them trying to find counterexamples, and I think it was offering some meaningful help with problem solving. That said, testcase.ac was never designed to generate revenue, so I have essentially been running it out of my own pocket. Separately from that, I had also been gradually feeling that I was losing the enthusiasm to add new features or to review submitted code and feedback.

After BOJ's shutdown was announced, I saw a lot of activity around finding alternatives to BOJ, and (gratefully) some people mentioned testcase.ac as one of those alternatives. Unfortunately, the existing testcase.ac has several fundamental issues that prevent it from replacing BOJ, let alone surviving on its own once BOJ is gone.

- The current testcase.ac depends very heavily on BOJ. It only allows adding BOJ problems, its generators and validators are generated from BOJ's problem statements, and the whole service was built on the premise that users come to testcase.ac after getting a wrong answer on BOJ. So it cannot be operated in the same way once BOJ shuts down.

- The current testcase.ac is closed. The source code used to find counterexamples is not public by default, and even the publicly available accepted-solution and generator code can only be viewed through the UI. Since I'm the sole administrator responsible for maintaining the contributed code and the web service, this closed structure makes the project hard to sustain long-term.

- testcase.ac was not built to be an "online judge." testcase.ac was created as a tool to get hints about wrong code on BOJ, and was never aimed at displaying BOJ's problem statements or collecting test data strong enough to judge correctness. With other mature online judges already available, building yet another online judge by collecting test cases strong enough to judge every problem would diverge from the original direction, and there isn't much point in doing so.


Because of these issues, I decided to shut down testcase.ac in its current form once BOJ ends.

## The direction going forward

But it also felt a bit disappointing to end things completely like this. Even though BOJ is leaving, I wanted to leave something of testcase.ac behind for the community. I thought about the potential way of moving forward with these principles in mind:

- It should not depend solely on BOJ; code for other online judges / contests should be easy to add
- The source code in use should be made as public as possible, so that anyone can view and contribute to it more easily
- Rather than just leaving behind accepted solutions and generator code, make it easy to do "dynamic counterexample finding" based on these source codes as well

In the end, I decided to rewrite the existing testcase.ac service and release it as an open source project.
- Code: [https://github.com/testcase-ac/testcase-ac](https://github.com/testcase-ac/testcase-ac)
- Service preview: [https://next.testcase.ac](https://next.testcase.ac)


In the new service, problem data is also managed as files in the GitHub repository.
- If you add accepted-solution code and generator code under the `testcase/` folder following the prescribed format (by submitting and merging a PR), you can find counterexamples for that problem.
- Both the accepted-solution / generator code used to find counterexamples, and the source code of the service itself are publicly available.
- As before, rather than becoming an online judge, it focuses on dynamically finding counterexamples using generator and accepted-solution code.

To enable this open source transition, several features have been removed from the existing testcase-ac. Features that do not align with the principles above, such as logging in, contributing accepted-solution / generator code through the UI, and contributing code privately, have been removed from the open source service and will not be added going forward.

Validation of contributed code (e.g. whether it compiles, whether the generator runs correctly) used to be performed when submitted through the UI. The relevant code is not in the repository yet, but if contribution volume becomes meaningful, I plan to replace it with a public CI process using GitHub Actions or similar tools. The experimental LLM-based generator creation that was added to the UI will also be released as a tool that individuals can run themselves, through mechanisms such as [Agent Skills](https://agentskills.io/home).

## Migration plan

Currently, the existing service can be accessed at [testcase.ac](https://testcase.ac), and the new open source service can be accessed at [next.testcase.ac](https://next.testcase.ac). The migration plan is as follows.
- 2026/5/2: [testcase.ac](https://testcase.ac) will point to the new open source service / the existing service will remain accessible at [old.testcase.ac](https://old.testcase.ac)
- 2026/5/30: [old.testcase.ac](https://old.testcase.ac) service shutdown

Some existing contributors may not want their code moved to the new open source project. Currently, since I have not yet received consent from contributors other than myself, only the code I personally contributed on testcase.ac and the code I personally submitted to BOJ has been moved to the new repository. Only contributed code with explicit consent will be migrated to the new open source repository.

Through the "Migrate contributed code" button in the banner at the top of testcase.ac, existing contributors can either download their contributed code and migrate it themselves, or consent to their code being contributed to the new project.

## Closing

By releasing this project as open source, I hope more people will be able to contribute. Contributing, forking and modifying and self-hosting it however you like, even taking the code and using it for commercial purposes: all of that is free. (As long as you follow the MIT license.)

Use cases that were previously difficult may now also become possible. For example, in non-public settings such as private academies or student clubs, one could fork the project, add their own problems, and have each user verify their own solutions through the project, using it as a lighter-weight alternative to a typical open source judge. I will leave such concrete use cases up to the community.

By opening contributions more widely, the project's survival no longer hinges on my own willpower alone, and I hope it can last a little longer.

Going forward, please give the new testcase-ac repository your interest and contributions.

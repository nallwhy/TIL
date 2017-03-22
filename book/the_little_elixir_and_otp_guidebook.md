# THE LITTLE Elixir & OTP GUIDEBOOK

written by [Benjamin Tan Wei Hao](http://benjamintan.io/).

## 1. Introduction

Elixir 가 Erlnag 위에서 만들어졌기 때문에, Elixir 에 대한 얘기를 시작 전에 Erlang 과 Erlang 의 전설적인 VM 에 대해 얘기하고 넘어가겠다.

Erlnag 은 [soft real-time](https://en.wikipedia.org/wiki/Real-time_computing), 

Criteria for real-time computing
A system is said to be real-time if the total correctness of an operation depends not only upon its logical correctness, but also upon the time in which it is performed.[5] Real-time systems, as well as their deadlines, are classified by the consequence of missing a deadline:

Hard – missing a deadline is a total system failure.
Firm – infrequent deadline misses are tolerable, but may degrade the system's quality of service. The usefulness of a result is zero after its deadline.
Soft – the usefulness of a result degrades after its deadline, thereby degrading the system's quality of service.
Thus, the goal of a hard real-time system is to ensure that all deadlines are met, but for soft real-time systems the goal becomes meeting a certain subset of deadlines in order to optimize some application-specific criteria.
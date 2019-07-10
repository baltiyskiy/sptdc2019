## 1.1
> Complete the agreement protocol below and give the bound on the ratio n/t for an asynchronous communication model with adaptive adversary and crash failures.
> ```
>     repeat
>         broadcast my estimate 
>         wait for (n-t) values 
>         case -1- at least ??? values equal to v: decide v
>              -2- at least ??? values equal to v: adopt v
>              -3- else adopt a random value 
>     endrepeat
>```

Decide `v` when at least `n - t` are equal to `v`. 
Suppose then that p1 receives `n - t` values `v`, then all other processes can receive at least `n - 2t` values `v`. Let's make them adopt `v`, so that during the next round all correct processes decide `v`. But in order to adopt one value, we need it to be a majority, which means `n - 2t > n/2`, which yields `t < n/4`.

Suppose then that half of processes receives `n - 2t` values `v` and adopts it. Can it happen so that the other half of the processes receives `n - 2t` values `w` and adopt it? If it were possible, the algorithm would never terminate. However, there's only `2t` of `w`s, so we need to make sure that `n - 2t > 2t`, which again yields `t < n/4`.

**Answer**: the protocol is for `t < n/4` crash failures; decide `v` if `n - t` values are equal to `v`; adopt `v` if `n - 2t` values are equal to `v`.

## 1.2
> Is it possible to design a protocol with one message exchange per round and `t < n/2` if the coin is common?

Let's construct a starting configuration where `n - t` processes (including process p1) have estimate 0, and the remaining `t` processes have estimate 1. The adversary "shows" the first `n - t` values to p1. Since p1's estimate is 0, and all values it sees are 0, there must be an execution where it decides 0, since the protocol must decide with probability 1. Since `t < n/2`, the minimal overlap between all sets of `n - t` processes has size 1, so the adversary can construct an arbitrary combination of 0 and 1 for other processes (p2, ..., pn), such that all of them flip the common coin\*. But then at the next round, processes p2, ..., pn must decide whatever value returned by the coin toss (again, there must exist such an execution where it happens, because the protocol must terminate with probability 1). There exists an execution where coin flip yields 1. In this execution, this protocol fails to reach an agreement, because p1 decides 0 and the rest decide 1.

**Answer**: no, because there exists an execution where any such protocol would fail to reach agreement.

\* This claim seems to require that the protocol is deterministic in choosing whether to flip the coin, but it's really not, because the processes can only use their estimate and the received messages, all of which is controlled by the adversary, and the coin is common, so if they toss it, then there still exists an execution where the adversary correctly guesses the outcome.

## 2

> Complete the protocol below and give the bound on the ratio n/t, t being the maximal number of Byzantine processes. 
> // Protocol for t<n/? crash failures 
> ```
> repeat 
>     bcast my estimate 
>     wait for n-t values 
>     case -1- at least ??? values equal to v: decide v 
>          -2- at least ??? values equal to v: adopt v 
>          -3- else adopt a random value 
> endrepeat
> ```

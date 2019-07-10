> Q. Complete the agreement protocol below and give the bound on the ratio n/t for an asynchronous communication model with adaptive adversary and crash failures.
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

Final answer: the protocol is for `t < n/4` crash failures; decide `v` if `n - t` values are equal to `v`; adopt `v` if `n - 2t` values are equal to `v`.

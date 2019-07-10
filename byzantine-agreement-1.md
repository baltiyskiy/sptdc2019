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

sdfsdf

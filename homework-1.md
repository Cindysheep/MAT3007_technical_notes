---
description: Tips and debug solutions for mat3007 homework1
---

# Homework 1

## Problem 1

Basically a practice of cvx basic. No big bugs happened here. Some syntax bugs may be solve by refering to following two source:

* [cvx basics](cvx-basics.md)
* [official cvx basics quick start](http://web.cvxr.com/cvx/doc/quickstart.html)

## Problem3 (need to update

In problem3, I declared 10 variables.&#x20;

```
    variables x12(1) x13(1) x14(1) x15(1) ...
              x21(1) x23(1) x24(1) x25(1) ...
              x31(1) x32(1) x34(1) x35(1) ...
              x41(1) x42(1) x43(1) x45(1) ...
              x51(1) x52(1) x53(1) x54(1)
```

using variables to declare multi variables.

using `...` to wrap the line.

## Problem 4

### bug1

```
Error using  .* 
Disciplined convex programming error:
    Cannot perform the operation: {positive constant} .* {real affine}
```

#### reason

There are invalid data, such as inf, -inf, empty data NaN, or zero data 0.

变量中存在无效数据，例如正负无穷+Inf、-Inf，空数据NaN，或者是0

#### debug

In this problem, if there is no edge between two nodes, we want to declare the length of the edge $$w_{ij}$$ as inf. But inf is invalid using .\* operation.

We set inf large enough can also solve the problem. Set inf entry as $$n*max({w_{ij}}), \forall w_{ij}\neq \infty$$, here that is 56.&#x20;

### bug2

```
Error using variable
No CVX model exists in this scope.
```

#### resaon

Put `clear` line inside the `cvx_begin` and `cvx_end`

把 clear 放在了cvx\_begin 和 cvx\_end 之间

e.g.

```
cvx_begin
    clear
    ...
cvx_end
```

⚠️ NEED TO UPDATE

Why cannot put clear inside cvx module?

#### debug

Put `clear` outside the cvx\_begin and cvx\_end module.

```
clear
cvx_begin
    ...
cvx_end
```

### bug3

```
Unable to use a value of type struct as an index.

Error in cvxprob/solve (line 429)
            [ x, status, tprec, iters, y ] = shim.solve( At, b, c, cones, quiet, prec, solv.settings, eargs{:} );

Error in cvx_end (line 88)
        solve( prob );

Error in h1p4 (line 22)
cvx_end
```

#### reason

According to [this cvx forum question](https://ask.cvxr.com/t/error-cannot-use-a-value-of-type-struct-as-an-index/11191), here are the ways that the creators offers:

> This looks like either a bug or a messed up installation or corrupted MATLAB session.
>
> Things to try:
>
> Try a different solver (use the `cvx_solver` command )
>
> Try a new MATLAB session.
>
> Try reinstalling CVX, and do that in a new MATLAB session. Make sure you are using CVX 2.2, Do NOT use CVX 3.0beta (it is riddled with bugs, which will likely never be fixed); and if you are using it, make sure to remove all CVX directories from the MATLAB path and save the MATLAB path; then install CVX 2.2 in a new MATLAB session.
>
> Try rebooting.

#### debug

I tried another solver to successfully solve the bug.

The cvx official have given the details about the solvers, [click here](http://cvxr.com/cvx/doc/solver.html) to see.

The environment we have set up only contains two solvers, SDPT3 and SeDuMi. Try another solver to see if it works. To get more professional solvers, follow steps on [Install cvx solver license](install-cvx-solver-license.md).

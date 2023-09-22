---
description: This page remarks some useful cvx basics
---

# cvx basics

Please refer to [official web docs here](http://web.cvxr.com/cvx/doc/basics.html) to learn more details about the syntax of cvx. Here we only discuss some of them that I used in homework. A usful [csdn blog](https://blog.csdn.net/qq\_45296693/article/details/130461814?spm=1001.2014.3001.5501) here is also recommended.

Here are the sample code in the environment setup guide

```matlab
cvx_begin
    variable x(1)
    variable y(1)
    maximize (6*x+5*y)
    subject to
        x + y <=5
        3*x + 2*y <=12
        x >= 0
        y >= 0
cvx_end
```

### 1. cvx\_begin & cvx\_end

As official said:

> All CVX models must be preceded by the command cvx\_begin and terminated with the command cvx\_end. **All variable declarations, objective functions, and constraints should fall in between**.

### 2. variable & variables & x(1)



variable 只能一次定义一个变量;

variables 可以一次定义多个变量;

variable 常用定义形式:

* variable x 定一个variable x, nothing special to declare
* variable x(n): define a variable x with n dimension
* variable x(1): define a variable x with 1 dimension
* variable x(10,2): define a variable matrix x with 10 row\*2  column size
* variable x(1) integer: define a varible x with dimension 1 and x is integer

variables 不能定义变量类型，i.e. 不能 `variables x(1) y(1) intger`

### 3. minimize() | objective function

objective function 要用()括起来

### 4. >= == <= |constraint

In cvx constraint, we use == to write constraints, instead of =. "=" means assign value, "==" means comparation.

### 5. run the code

To run the code, two common ways. Firstly, you can click the <img src=".gitbook/assets/Screenshot 2023-09-23 at 02.23.40.png" alt="" data-size="line"> bottom. Secondly, you can type `file_name` in the command window of Matlab. e.g. I saved the file as test.m, so I type `test` in the command window to run th escript.

### 6. outcomes|layouts

You can see the outcomes on the right side "Workspace" of Matlab. If you accidantally closed it, click home->layout on the top tool bar to reopen it. You can also drag the windows to custom the layout.

Additionally, you can also using following command lines in the command window to ask program print out the outcomes.

```
cvx_optval %output the optimal value
cvx_status % output the problem statuse
```

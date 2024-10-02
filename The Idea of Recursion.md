# Function

The structure of a standard function is:

```cpp
return_type function_name(parameters) {
    // function body
    return value;
}
```

In simple words, you give a function some values (*parameters*). It does some works with those values and returns you something. This is the whole purpose of a function. The simplest of functions is the quadratic function, $f(x) = x^2$. If you give $2$ as the parameter of the function $f$, it will return you $4$. That's the function for you!

# Recursive Function

> To understand recursion, you need to understand recursion!

In a word, a recursive function is a function that calls the function itself.

Recursion eases coding complexity. An iterative problem is more understandable if it is thought in a recursive way. As a recursive function calls itself, the process will fall into an infinite loop unless you mark a stopping point (this stopping point is called as the **base case**).

The idea of recursion is basically breaking down a problem into smaller (and more manageable) sub-problems until a base condition is met, which eventually stops the recursion.

Let's think about calculation of the factorial of a number.

$$
\begin{aligned}
4! &= 4 * 3 * 2 * 1 \\
&= 4 * 3 * 2! \\
&= 4 * 3!
\end{aligned}
$$

**So, to calculate $n!$, we have to calcualte $(n-1)!$. This is what we can call dividing the problem into smaller sub-problems. These are the cases when we need to use recursive functions.**

In programming, we see this solution in a reverse way.

$$
\begin{align}
4! &= 4 * 3! \\
3! &= 3 * 2! \\
2! &= 2 * 1! \\
1! &= 1
\end{align}
$$

So, we can describe it like this: we need to calculate $3!$ if we want to calculate $4!$. To calculate $3!$, we need to calculate $2!$. To calculate $2!$, we need to calculate $1!$, which is actually $1$ (making it our base case for this recursive task).

If we write in a more general way, it will like this,

$$
\begin{aligned}
n! &= n * (n-1)! \\
(n-1)! &= (n-1) * (n-2)! \\
(n-2)! &= (n-2) * (n-3)! \\
& \text{... and so on}
\end{aligned}
$$

## The Recursion

Therefore, we can imagine a function named `fact(n)`. We call it when we need to calculate the factorial of a number, $n$. That's the only thing we know! And, yeah, we need to know another thing. That is the base case. So, when we are trying to access `fact(1)`, it should return $1$.

With this idea in mind, let's see the following function,

```cpp
long long fact(int n) {
    // base case first
    if (n == 1 || n == 0) return 1; // fact(1) should return 1
    
    return n * fact(n - 1); // fact(n) = n * fact(n - 1)
}
```

>> **Food for thought**: Why we checked if `n == 0` or not?

It is the potential redefinition of the iterative method to calculate the factorial of a number, which is something like below,

```cpp
long long fact = 1;
for (int i = 1; i <= n; i++) {
    fact *= i;
}
```

> Now the judgment is yours! Which one is more intuitive?

So, how does that 3 lines of code work? To understand this, keep in mind that function call occurs in stack memory.

To calculate $4!$, we call `fact(4)` first. `fact(4)` then calls `fact(3)`. `fact(3)` calls `fact(2)`. And, finally, `fact(2)` calls `fact(1)`.

As long as the `fact(1)` is not called, none of the functions returned any values. It was just called. But, with the call of `fact(1)`, it returned $1$ for the first time. As we get a return value for `fact(1)`, it will now backtrack to get the other values of those function calls. See the following demonstartion,

```scss
factorial(4)
   |
   +---> 4 * factorial(3)
               |
               +---> 3 * factorial(2)
                           |
                           +---> 2 * factorial(1)
                                       |
                                       +---> 1 (Base case)
```

After getting the value from the base case, the process of backtracking will start to calculate `fact(4)`.

```scss
                                       <---- 1 (Base case)
                                       |
                           <---- 2 * 1
                           |
               <---- 3 * 2
               |
   <---- 4 * 6
   |
factorial(4) := 24
```

I hope this gives a basic idea about recursion.

***

Drafted on October 1, 2024 by Md Azizul Hakim
# Algebraic Props

For the rest of the following, we assume:
- A,B,C are non-zero natural numbers / integers
- A, B, C are coprime to each other

Note:

I use two of the following notations around, but there is a difference between them:

1.
$$  14 \text{ mod } 4 == 14 \% 4 = 2  $$

2.
$$  14 \% 4 \pmod{4} = 2 \pmod{4} \neq{} 2  $$

The first example is a static value which has lost the context of its modulo environment.
The second shows that the value maintains the modulo context, and is different to the static value.
The mod context means that the number can be anything that satisfies the modulo involed:

eg.

$$  22 \text{ (static) } = 5 \pmod{17} = 4 \pmod{18}$$

In this document, properties listed are generally for modulo context values, since static values are simply standard arithmatic, and not modulo arithmatic.

However where the mod context is ommitted, it will be regarded as static / standard arithmatic again.

If the algebra strictly maintains the modulo context throughout each step, then the expression is never modified in value.

***Any algebra no matter how ridiculous will still remain the same, so property failures happen where context is lost.***

Usually this happens when changing the modulo's base context.


## Negative

$$   A \text{ % } B = A \pmod{B} = (B-A) \pmod{B} \tag*{ if B > A}$$

eg.

$$   3 \text{ % } 7 = 3 \pmod{7} = -4 \pmod{7}    $$

More usually positive only form:

$$   A \% B = \begin{cases}
        A       & \text{if $A < B$}   \\
        B - A   & \text{if $A \ge{} B$} 
\end{cases} $$

Or otherwise including negative:

$$   A \% B = \begin{cases}
        A       & \pmod{B}    \\
        B - A   & \pmod{B} \text{ negative equivalent} 
\end{cases}
$$

## Distributive over Addition

$$   (A + B) \text{ % } C \pmod{C}= A \text{ % }C + B \text{ % } C \pmod{C} $$

eg.

$$   (5 + 7) \text{ % } 3 = 2 + 1 \pmod{3} = -1 + 1 \pmod{3} = 12 \text{ % }3 = 0\pmod{3}    $$

## Distributive over Multiplication

$$   ( A . B ) \text{ % } C \pmod{C} = ( (A \text{ % } C) . (B \text{ % } C ) \pmod{C}    $$

eg.

$$   (7 * 11) \% 4 = 77 \% 4 = 1 \pmod{4}   $$
$$   (7 * 11) \% 4 = (7 \% 4) * (11 \% 4) \pmod{4} = (3 * 3) \% 4 \pmod{4} = 9 \% 4 = 1 \pmod{4}  $$

## NOT Commutative (operand swap)

$$  ( A \% B) \neq{} ( B \% A)  $$

## NOT Commutative in operation chain

$$   (A \% B) \% C  \neq{} (A \% C) \% B    $$

eg. 
without mod context:

$$   ( 14 \% 4) \% 5 = (2) \% 5 = 2 \pmod{5}    $$
$$   ( 14 \% 5) \% 4 = (4) \% 4 = 0 \pmod{4}    $$

with mod context (gets giga messy):

$$  ( 14 \% 4) \% 5 = (2 \text{mod 4}) \% 5 = (2 + 4k_{A}) \% 5 \pmod{5}    $$
$$  ( 14 \% 5) \% 4 = (4 \text{mod 5}) \% 4 = (4 + 5k_{B}) \% 4 \pmod{4} = k_{B} \pmod{4}    $$

$$  \text{let $k_{A}$ = 3, $k_{B}$ = 2 then: }     $$

$$  (2 + 4k_{A}) \% 5 \pmod{5} = 14 \% 5 = 4 \pmod{5} \ni 14      $$
$$  (k_{B}) \% 4 \pmod{4} = 2 \% 4 = 2 \pmod{4}   \ni 14    \text{  (agrees with above)}    $$

## NOT Associative

$$   ( A \% B) \% C \neq{} A \% (B \% C)   $$

eg.

$$   ( 13 \% 7) \% 4 = 6 % 4 = 2    $$
$$   13 \% (7 \% 4) = 13 \% 3 = 1   $$







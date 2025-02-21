# Chinese Remainder Theorem

## Description

You can look up better definitions on wikipedia or whatever. Anyways we shall work with natural numbers and integers from here on.

Let $ \Pi\{N, A, B, C\} $ where $\Pi\{\ldots\text{<elements>}\}$ means each element in the set are Co-prime to each other

then Chinese Remainder Theorem (CNR) loosely states the following:


We have an unknown number N
But we know information of the remainder of N if divided by some numbers. Eg.

$$  N \% A = R_{A}   $$
$$  N \% B = R_{B}   $$

where $R_{A}, R_{B}$ are remainders, then N has the form:

$$  N = kAB + C      \tag*{$k \in \Bbb{Z}$}    $$

simple proof:

let $ N = kAB + C $ then

$$ N \% A = (kAB + C) \% A = C \% A \tag*{where $C \% A = R_{A}$} $$
$$ N \% B = (kAB + C) \% B = C \% B \tag*{where $C \% B = R_{B}$} $$

Example: Given the following:

```go
/*Example:
    N = 2 mod 3
    N = 3 mod 5
    then we know that
    N = 15k + 8
*/
package main
import "fmt"

func main(){
	var Ra, Rb, N, A, B, C int
	
	Ra, A = 2, 3    // N % 3 = 2 mod 3
	Rb, B = 3, 5    // N % 5 = 3 mod 5
	
	// Soln:
	//  N = 15k + 8
	C = 8   // take for granted - actual solution is the real problem to be explored further
	
	// generate possible values of N
	for k := 0; k < 5; k++ {
	    N := k * (A * B) + C
	    fmt.Println(N)
	}
}
```

## Solution to the CNR coefficient:

let $ \{x,y,A,B,C,N,R_{A},R_{B}, \Delta_{R}\}\in\Bbb{Z} $

then N has the forms\:

$$  \begin{split}
    N   &= \omega k + \theta    \mod{\{A,B\}}   \\
        &= kAB + \theta         \mod{\{A,B\}}
\end{split} $$ 

where N is a periodic function (think $\omega$ as angular freq, $\theta$ as phase):
- $ \omega = AB $
- $ k := \text{range}\{\Bbb{Z}\}    $
- $ \theta \in \Bbb{Z} = R_{A,B} \mod{\{A,B\}} $

more precisely, $ \omega = \frac{LCM(A,B)}{HCF(A,B)} $

and $x,y$ are arbitrary values, $R_{A,B}$ are remainders respectively: 

$$  \begin{split}
    N   &= Ax + R_{A}   = R_{A}  \mod{A} \\
        &= By + R_{B}   = R_{B}  \mod{B} \\
    \implies N  &= Ax + R_{A} = By + R_{B}   
\end{split} $$

since: 

$$ \begin{split}
    Ax &= 0 \mod{A} \\
    By &= 0 \mod{B} \\
    kAB &= 0 \mod{\{A,B\}}
\end{split} $$

let $ \Delta_{R} = R_{A} - R_{B} $

then:
$$\begin{split}
            Ax + R_{A}  &= By + R_{B}    \\
\implies             By &= Ax + \Delta_{R}  \\
\implies    Ax + \Delta{R}  &= \text{ (multiple of B)}  \\
            By - \Delta{R}  &= \text{ (multiple of A)}
\end{split} $$

let $ x = Bk + x_{0} $, then:
$$ \begin{split}
            By          &= kAB + Ax_{0} + \Delta_{R}    \\
\implies    By + R_{B}  &= \omega k + ( Ax_{0} + R_{A} )    \\
\implies    \theta &= N |_{k=0}  \\
\end{split} $$

which means there is no further analytical solution through this method. The solution with this method here-on is trial-n-error / iterative based.

$$\begin{split} 
            Ax_{0} + \Delta_{R} &= 0 \mod{B}    \\
\implies                x_{0}   &= \frac{\{0, B, 2B, ...,(A-1)B\} - \Delta_{R}}{A} \\
\text{similarly, }       y_{0}   &= \frac{\{0, A, 2A, ...,(B-1)A\} + \Delta_{R}}{B} \\
\end{split}$$


Example:
```
Solution for reference: N = 15k + 8
N = 2 mod 3
N = 3 mod 5
thus:
Ra = 2; A = 3; Rb = 3; B = 5;
dR = Ra - Rb = -1

thus:
x0 = ({0,B,...} + 1 ) / 3
x0{B} -> x0 = (5+1)/3 = 2 is a solution
-> x = Bk + x0 = 5k + 2
-> x = {2, 7, 12, 17, ...}
-> y = (Ax + dR)/B -> y0 = (3 * 2 - 1)/5 = 1
-> y = Ak * y0 = 3k + 1
-> y = {1, 4, 7, 10, ...}

at k=0:
(x,y) = (2,1)
Ax + Ra = 6 + 2 = 8
By + Rb = 5 + 3 = 8

Thus theta = N0 = 8
=> N = 15k + 8
```

### Trivial case of RA == RB

if RA == RB == R, ie $\Delta_{R} == 0$, then:

x0 = {0, B, 2B ... < BA } / A = 0
y0 = 0 (similarly)
thus N = kAB + R

## More than 2

Example:
```
N = 2 mod 3
N = 3 mod 5
N = 2 mod 7

Solution for reference: N = 105k + 23

Reduce the statements to 2 sets:
-> {N=2mod3, N=3mod5} && {N=2mod7}
since we know the first already, this is equivalent to:
-> { N = 15mod8 } && { N = 2mod7 }

Note: {15,7} are coprime so we do not need to use LCM/HCF.

Ra, A = 8, 15
Rb, B = 2, 7
dR = 6

// k is local variable, localised to its own eqn (just means its an arbitrary integer)
x0 = (7k - 6) / 15 
y0 = (15k + 6) / 7
-> x0 = (7 * y0 - 6) / 15
-> (x0, y0) = (1, 3) is a solution, ie 1 = (7*3-6)/15

thus:
A * x0 + Ra = 15 * 1 + 8 = 23
B * y0 + Rb = 7 * 3 + 2 = 23

Thus:

N = 105k + 23

```

## Summary

N = Ra mod A = Rb mod B has the solution:
N = kAB + C

where C is given by:

Ax + Ra = By + Rb 
for some x < B, y < A

and can be reduced to:

N = C mod AB



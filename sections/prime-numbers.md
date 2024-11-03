# Prime numbers
A prime number is a natural number (positive integers) that does not divide by anything except itself, where:

$$
    \text{let P $\in\N$ be a prime number, where $\N$ = {0,1,2,...} is the set of natural numbers}
$$
P is prime if the following is met:
$$
    \frac{P}{n} \in N \text{ for any $n\in N$ if and only if } \{n=P, \frac{P}{n}=\frac{P}{P}=1, \text{no other value of n exists to satisfy prev conditions}\}
$$
eg.
$$ \text{ 7 is prime because } \frac{7}{n}\notin\N \text{ unless } n=7 $$
$$ \text{ 4 is not prime because } \frac{4}{2} \in\R $$

EXCEPTIONS:

- the numbers {0, 1} are NOT PRIME (some reasons involved)
- 1 is considered prime for some modulo arithmatic

## isPrime algorithm

```go
import "math"

func isPrime(n int)bool{
    // due to prime factorisation, upper ^ 2 >= n
    // The prime itself is the biggest factor.
    // if there is another factor > sqrt(n), there MUST BE another corresponding factor < sqrt(n)
    upper := int(math.Floor(math.Sqrt(n))) + 1
    if n <= 1 {
        return false    // negs, 0, 1 are not prime
    }
    for i:=2; i < upper; i++{
        if n % i == 0 // found a factor < sqrt(n)
        return false
    }
    // no factors < sqrt(n), next factor must be the number itself, ie. n isPrime
    return true
}
```

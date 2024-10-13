# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

The recurrence relation can be expressed as $T(n)=3T(\frac{n}{3})+n^3$, whereas $3T(\frac{n}{3})$ stands for the 3 recursive call, and $n^3$ stands for the three nested loops.

Using substitution method to solve this relation:
1. Substituing into the original equation: $T(n)=3[3T(\frac{n}{9})+n^3]+n^3=9T(\frac{n}{9})+4n^3$
2. Do substitution again: $T(n)=9T(\frac{n}{9})+4n^3=3[9T(\frac{n}{27})+4n^3]+n^3=27T(\frac{n}{27})+13n^3$
3. Find the pattern: $T(n)=3^iT(\frac{n}{3^i})+ \sum_{k=0}^{i-1} 3^k n^3$
4. To make $\frac{n}{3^i}=1$, $i=log_3n$, So that $T(n)=3^{\log_3n}T(1)+ \sum_{k=0}^{i-1} 3^k n^3=nT(1)+\sum_{k=0}^{i-1} 3^k n^3$

Therefore, $T(n)=nT(1)+\sum_{k=0}^{i-1} 3^k n^3\in\Theta(n^3)$

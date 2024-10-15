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

The recurrence relation can be expressed as $T(n)=3T(\frac{n}{3})+n^5$, whereas $3T(\frac{n}{3})$ stands for the 3 recursive call, and $n^5$ stands for the three nested loops, the outerloop runs $n^2$ times, the mid loop runs $n$ time, and the inner most loop runs $n^2$ times, combine them together result the time complexity to be $n^5$.

Using substitution method to solve this relation:
1. Substituing into the original equation: $T(n)=3[3T(\frac{n}{9})+(\frac{n}{3})^5]+n^5=9T(\frac{n}{9})+\frac{n^5}{3^4}+n^5$
2. Do substitution again: $T(n)=9T(\frac{n}{9})+\frac{n^5}{3^4}+n^5=9[3T(\frac{n}{27})+(\frac{n}{9})^5]+\frac{n^5}{3^4}+n^5=27T(\frac{n}{27})+\frac{n^5}{9^5}+3n^5+\frac{n^5}{3^4}+n^5$
3. Find the pattern:

   $T(n)=3^iT(\frac{n}{3^i})+ n^5\sum^{k-1}_{i=0}3^i(\frac{1}{3^{5i}})$
   
   simplify the sum: $T(n)=3^iT(\frac{n}{3^i})+ n^5\sum^{k-1}_{i=0}\frac{1}{3^{4i}}$

   solve the geomtric series with $r=\frac{1}{3^4}$

   $S=(1-\frac{1}{n^4})(\frac{3^4}{3^4-1})=(1-\frac{1}{n^4})(\frac{81}{80})$
5. To make $\frac{n}{3^i}=1$, $i=log_3n$, So that $T(n)=3^{\log_3n}T(1)+ n^5(1-\frac{1}{n^4})(\frac{81}{80})=nT(1)+ (n^5-n)(\frac{81}{80})$

   simplify $T(n)=nT(1)+ (n^5-n)(\frac{81}{80})=\frac{81}{80}n^5+n(T(1)-\frac{81}{80})$

Therefore, $T(n)=\frac{81}{80}n^5+n(T(1)-\frac{81}{80})\in\Theta(n^5)$

“I certify that I have listed all sources used to complete this exercise,
 including the use of any Large Language Models. 
 All of the work is my own, except where stated otherwise. 
 I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, 
 charges may be filed against me without prior notice.” --Doris Yan

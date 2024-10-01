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



# My Analysis

The base case of this recursive algorithm states that if n is less than or 
equal to 1, then it will return. In the case that the input is 1 or less, 
this algorithm has a constant runtime. However, when n is greater than 1, 
things get more intersting.

Looking at the algorithm, it can be boiled down to 3 recursive calls and a 
triple-nested for loop. Starting with the nested for loop, the base for 
loop (with the iterator 'k'), we see that it will complete n\*n times since 
k will only ever iterate by 1. Similarly, with the second for loop (with 
the iterator 'j'), we see it will complete n times, and for the last for 
loop (with the iterator 'i'), it will run n\*n times. Written out, we can 
write $\Theta(n^2\*n\*n^2)$ or simplify to $\Theta(n^5)$.

We also see that there are 3 seperate non-nested recursive calls where the 
input n is divided by 3. Written into a recursive relation, we get: 

$$ T(n) = 3T(n/3) $$

Adding the triple-nested for loop into the equation:

$$ T(n) = 3T(n/3) + \Theta(n^5) $$

Expanded out a few iterations:\
    $ T(n) = 3(3T(n/9) + \Theta(n^5)) + \Theta(n^5) $\
    $ T(n) = 9T(n/9) + 3\Theta(n^5) + \Theta(n^5) $\
    $ T(n) = 18T(n/18) + 9\Theta(n^5) + 3\Theta(n^5) + \Theta(n^5) $

Generate a pattern:
$$ T(n) = 3^k * T(n/3^k) + k * \Theta(n^5) $$

Plug in $k = log{_3}n$:
$$ T(n) = n * T(1) + log{_3}n * \Theta(n^5) $$

We know that $T(1)$ is a constant runtime operation, so $T(1) = \Theta(1)$. 
Now we can simplify even further:
$$ T(n) = n * \Theta(1) + log{_3}n * \Theta(n^5) $$

Which simplified gives:
$$ T(n) = \Theta(n) + \Theta(n^5*log{_3}n) $$

Since the $\Theta(n)$ is negligible, the final time complexity is 
$$ T(n) \in \Theta(n^5*log{_3}n) $$



# Sources

- ChatGPT: For the quick explanation and example of what a tight bounded
            complexity and loosely bounded complexity looks like.


# Plagiarism Acknowledge

I certify that I have listed all sources used to complete this exercise, 
including the use of any Large Language Models. All of the work is my own, 
except where stated otherwise. I am aware that plagiarism carries severe 
penalties and that if plagiarism is suspected, charges may be filed against 
me without prior notice.
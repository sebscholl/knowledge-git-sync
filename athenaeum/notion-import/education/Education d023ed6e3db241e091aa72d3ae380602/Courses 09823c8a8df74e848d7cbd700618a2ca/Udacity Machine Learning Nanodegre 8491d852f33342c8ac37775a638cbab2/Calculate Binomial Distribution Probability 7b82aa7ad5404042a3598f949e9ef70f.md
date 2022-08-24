# Calculate Binomial Distribution Probability

A binomial distribution can be thought of as simply the probability of a SUCCESS or FAILURE outcome in an experiment or survey that is repeated multiple times. The binomial is a type of distribution that has two possible outcomes (the prefix “bi” means two, or twice). 

For example, a coin toss has only two possible outcomes: heads or tails and taking a test could have two possible outcomes: pass or fail.

The binomial distribution formula is:

**b(x; n, P) = nCx * Px * (1 – P)n – x**

b = binomial probability

x = total number of "successes" 

P = probability of success per trial

n = number of trials

Working function is:

**b(x; n, P) = n! / (n – X)! * X!**

***An exclamation mark in math is a factorial operation, which represents the product of the integers from 1 to n.**

Find the p (success rate) and q (failure rate):

**p = P**

**q = 1 - P**

Now calculate the success and failure values:

**s = p^X**

**f = q^(n-X)**

Finally, multiply:

**b(x; n, P) * s * f**
# DAA

## Chapter 3

### Big O notation

##### Asympototic Upper Bound

For a given function g(n), we denote O(g(n)) as the set of functions:

O(g(n)) = { f(n) | there exists positive constants c and n<sub>0</sub> such that 0 <= f(n) <= c g(n) for all n >= n<sub>0</sub>}

It is used to represent the worst case growth of an algorithm in time or a data structure

#### Questions


Algo add() {
    for i = 1 to m do                      
        for j = 1 to n do
            c[i,j] = a[i,j] + b[i,j]
}

line 1 - m+1 times
line 2 - m*(n+1) times
line 3 - m*n times


f(n) = 6n + 3

Find the upper bound for this f(n)

0 <= f(n) <= c.g(n) for all n >= n<sub>0</sub>

3(2n+1)

Find upper band of running time of wuadratic function

f(n) = 3n<sup>2</sup> + 2n + 4

0 <= f(n) <= c.g(n) for all n >= n<sub>0</sub>

0 <= 3n<sup>2</sup> + 2n + 4 <= c.n<sup>2</sup>

|c=9|g(n)|f(n)|
|---|----|----|
|n=1|9|9|
|n=2|36|20|


f(n) = 2n + 10

g(n) = n

Is f(n) = O(g(n))

0 <= 2n+10 <= c.n for all n >= n<sub>0</sub>

# Chapter 4

Regular/traditional/deterministic algorithms

I/P -> Algo -> O/P

Algorithms work in polynomial time
Exaple O(n) for bubble sort = n<sup>2</sup>

Non deterministic algorithm runs in exponential mode -> 2<sup>n</sup>

Hard problems can be solved by 2 approaches

- Randomized algorithm
- Approximated algorithm

## Non deterministic algorithm

- choice()
- success()
- failure()

### Need

- Some problems require exponential time complexity (exponential time for execution).
- So to convert and solve the problem in polynomial time, it can be represented in non deterministic algorithm.

## Deterministic algorithm

- P Class<br>
Set of all deterministic algorithms that are solved in polynomial time

- NP Class<br>
Set of non deterministic algorithms that can be solved in polynomial time

- NP problem is known as NP hard if the solution is not <u>solvable</u> in polynomial time.
- NP hard problem can be known as NP complete problem if the problem is <u>verifiable</u> in polynomial time

Sum of subsets belongs to NP hard class, but its solution is verifiable in polynomial time so it comes under the category of NP hard.

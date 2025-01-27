# induction

one step implies the next (after you get started, of course)

### example

- sum of consecutive natural numbers
  - P(n): 0 + 1 + 2 + ... + n = (n \* (n + 1)) /2

### factorial in python: induction & recursion

```py
def factorial(n):
  if n == 0:
    return 1
  else:
    return n * factorial(n - 1)
```

### induction mistakes

- make sure you go from n to n + 1, more generally from f(n) to f(n + 1)

### sum of consecutive natural numbers - visual proof

- n embedded in n + 1 matrix
- this is also ((n + 1) \* (n + 1) - (n + 1)) / 2

### why does this matter?

- figuring out inductive proof might exist when it has never been done before requires understanding problem & its structure

```py
for i in range(n - 1):
  for j in range(i + 1, n):
    f(i,j)
```

### example: prove perfect binary tree with 2^n leaves has height n

- base cases
  - tree with 2^1 leaves has height 1 by inspection
  - tree with 2^2 leaves has height 2 by inspection
- inductive hypothesis
  - if n bit perfect tree has 2^n leaves, then (n + 1) bit perfect tree has 2^(n + 1) leaves
- proof
  - each leaf has unique int index with n bits. let b^n denote one of these leaves
  - create 2 identical complete binary trees
  - we can label any leaf in left tree by some 0b^n
  - we label any leaf in right tree by 1b^n (same b^n)
  - height = n + 1, num leaves = 2^(n + 1)

### example: pascal's triangle

- (n - 1) choose (r - 1) + (n - 1) choose r = n choose r, where n is row & r indexes rth entry
- base: by inspection, it is true for first 4 rows
- inductive hypothesis: this holds for all n
- this can be proven with basic order of operations
  - ((n - 1)! / ((r - 1)!((n - 1) - (r - 1))!)) + ((n - 1)! / (r!(n - 1 - r)!)) = n! / (r!(n - r)!)

### machine learning: decision trees

- decision tree learned from 12 examples
- random forests
  - what if we constructed many decision trees, then allowed them to vote?
  - let every decision tree see a different slice of data
  - to train a tree in a random forest
    - choose training set by picking examples with replacement from n training examples (aka bootstrap sample)
    - for each node of tree, randomly choose m variables on which to base variable hcoice at that node
  - advantages
    - state of the art performance
    - works well for high dimensional data
    - estimates importance of variables in determining classification
    - generates estimate of generalization error as forest building progresses
    - handles missing data well
    - scalable to large datasets
  - bagging
    - idea behind random forests can be applied to any classifier & is called bagging
      - choose m bootstrap samples
      - train m different classifiers on these bootstrap samples
      - for new query, average/take majority vote
    - what if we have 3 independent decision trees, & each one is only 70% correct? if we let them vote, together they're 78.4% correct
    - result is binomial distribution
    - what if we have 5 independent decision trees, & each one is only 80% correct? if we let them vote, together they're 94% correct
    - bag more decision trees -> higher performance

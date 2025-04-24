- One of the most foundational tools for computer science - it analyzes the cost of an algorithm
- _Mathematical_ notation that describes the **limiting** behaviour of a function when the argument moves towards a particular value or infinity (the **upper bound**) with respect to time or space
  - Ie. Describes the _complexity_ of code using algebraic terms
- It describes the order of growth/space in terms of input size, _not_ its exact value
- Can be used to compare **efficiency** of different algorithms or data structures
- Provides an **upper limit** on the time taken by an algorithm in terms of the _size of the input_.
  - Mainly consider worst case scenario to find its complexity in terms of Big O
- Denoted as **O(f(n))** where **f(n)** is a function that represents the _number of operations_ (steps) that an algorithm performs to solve a problem of size **n**

## Importance of Big O

- Analyzes efficiency
- Way to describe how the runtime or space requirements of an algorithm grow as input size increases
- Way to compare different algorithms and choose the most efficient one for a specific problem
- Helps understand scalability of algorithms and predicts how they will perform as the input size grows

## Properties of Big O notation

### Reflexivity

- A function is always bound _by itself_
- If you have a function that describes how something grows, it will grow at the **same rate as itself**
  - For every function `f`, it is always the case that `f` is its own upper bound (ie. `O(f)`)

```text
f(n) = n2

then f(n) = O(n2)
```

### Transitivity

- Helps to understand how growth rates are connected _between_ functions
- If one function grows at the same rate or slower than a second function, and the second function grows at the same rate or slower than a third, then the first function will grow at the same rate or slower than the third
  - Shows how different functions related to each other in terms of growth

```text
f(n) = n^2
g(n) = n^3
h(n) = n^4

then f(n) = O(g(n)) and g(n) = O(h(n))

Therefore, by transitivity, f(n) = O(h(n))
```

### Constant factor

- For any constant where c > 0 and functions **f(n)** and **g(n)**, if **f(n) = O(g(n))**, then **cf(n) = O(g(n))**.
- Multiplying a function by a constant **does not change** its Big O classification
  - Ie. whether a function grows quickly or slowly, adjusting its size by a _fixed amount_ does not alter how we describe its growth rate in terms of Big O
- Constants are dropped in runtime (algorithm that may be described as `O(2(n)`, is actually `O(n)`)

```text
f(n) = n
g(n) = n^2

then f(n) = O(g(n))

Therefore, 2f(n) = O(g(n))
```

### Sum rule

- If you add two functions that are each bound by the same _growth rate_, their growth rate will also be bound by that rate
  - Ie. The combined growth rate is determined by the term that grows the fastest among the functions being added
- When adding complexities, only the largest term dominates

```text
f(n) = n^2
h(n) = n^3

then , f(n) + h(n) = O(max(n^2 + n^3) = O(n^3)
```

### Product rule

- When you multiply two functions, each with their own growth rate, the growth rate of their product is the _combination_ of both rates
  - Helps understand how growth rates of individual functions affect growth of their product

```text
f(n) = n
g(n) = n^2
h(n) = n^3
k(n) = n^4

then f(n) = O(g(n)) and h(n) = O(k(n))

therefore, f(n) * h(n) = O(g(n) * k(n)) = O(n^6)
```
### Composition rule

- How the growth rate of a function is applied to another function
- By knowing how two functions grow _individually_, you can predict how their combination will behave

```text
f(n) = n^2
g(n) = n
h(n) = n^3

then f(n) = O(g(n)) and g(n) = O(h(n))

therefore, f(g(n)) = O(h(n)) = O(h^3)
```
## Common Functions

### O(1) - Constant

- Implies algorithm’s time or space complexity remains constant regardless of input size **n**, and the amount of time or memory does _not_ scale with n
  - Means n is not **iterated** or **recursed** on
- Generally means a value will be _selected and returned_ or a value will be _operated on and returned_

```js
function returnDoubleIndex(i, arr) {
  return arr[i] * 2;
}
```

- **No data structures** can be created that are multiples of the size of n, as space usage does _not_ increase with the size of the input
  - Variables can be declared, but the number must _not change with n_

```js
function logElements(arr) {
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
}
```

### O(logn) - Logarithmic

- Running time of an algorithm is proportional to thel ogarithm of the input size
- Typically has a base of 2
- Every time n increases by an amount k, time or space increases by k/2
- Rarer to encounter

#### Common algorithms

**Binary search** - searching for a term in a binary search tree and adding items to a heap

```js
function binarySearch(arr, searchTerm) {
  let left = 0,
    right = arr.length - 1;
  while (left <= right) {
    let mid = Math.floor((right - left) / 2) + left;
    if (mid === searchTerm) {
      return mid;
    } else if (mid < searchTerm) {
      return mid - 1;
    } else {
      left = mid + 1;
    }
  }
}
```

**Recursive** - where recursion depth is logarithmic (eg. binary search) - When a recursive call is made, all current variables get placed on the stack and new ones are created. If the number of recursive calls increases logarithmically (ie. n is halved with every recursive call) the space complexity will be `O(logn)`

```js
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  } else {
    let left = [],
      right = [],
      newArr = [];
    let pivot = arr.pop();

    for (let i = 0; i < arr.length; i++) {
      if (arr[i] <= pivot) {
        left.push(arr[i]);
      } else {
        right.push(arr[i]);
      }
    }

    return [...quickSort(left), pivot, ...quickSort(right)];
  }
}
```

### O(n) - Linear

- Most straightforward
- Means that time/space scale 1:1 with changes to the size of n
- If a new operation or iteration is needed every time n increases by 1, then algorithm will run in `O(n)` time

```js
function twoSum(nums, target) {
  let numSet = new Set();
  for (let i = 0; i < nums.length; i++) {
    if (numSet.has(target - nums[i])) {
      return [target - nums[i], nums[i]];
    }
    numSet.add(nums[i]);
  }
  return null;
}
```

### O(nlogn) - Loglinear

- Implies that logn operations will occur n times
  - Ie. for each of the n elements, a logarithmic operation is done

#### Common algorithms

**Recursive sorting**

```js

```

**Binary tree sorting**

and most other types of sorts.

### O(n^x) - Polynominal

### Quadratic 

- Running time of an algorithm is proportional to the square of the input size.

**Bubble sort**
```js
function bubbleSort(arr){
    const arrayLength = array.length;
    let isSwapped;

    for (let i = 0; i < arrayLength; i++) {
        isSwapped = false;
        for (let j = 0; j < arrayLength - i - 1; j++) {
            if (array[j] > array[j + 1]) {
                [array[j], array[j + 1]] = [array[j + 1], array[j]];
                isSwapped = true;
            }
        }

        if (!isSwapped) 
            break;
    }

    return array;
}
}
```

### O(X^n) - Exponential

### O(n!) Factorial

**Resources**

- https://builtin.com/software-engineering-perspectives/nlogn
- https://www.simplilearn.com/big-o-notation-in-data-structure-article#:~:text=Reflexivity%20means%20that%20a%20function,itself%20in%20Big%20O%20Notation.
- https://www.geeksforgeeks.org/analysis-algorithms-big-o-analysis/

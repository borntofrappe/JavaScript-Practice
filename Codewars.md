# Codewars

> problems, solutions and notes from [codewars](https://www.codewars.com).

## P1: A Pile of cubes

### Task

Construct a building which will be a pile of n cubes. The cube at the bottom will have a volume of `n^3`, the cube above will have volume of `(n-1)^3` and so on until the top which will have a volume of `1^3`.

You are given the total volume `m` of the building. Being given `m` can you find the number `n` of cubes you will have to build?

The parameter of the function `findNb` will be an integer `m` and you have to return the integer `n` such as `n^3 + (n-1)^3 + ... + 1^3 = m`, if such a n exists, or `-1`, if there is no such `n`.

```js
function findNb(m) {
  return -1;
}
```

### Tags

while, ternary operator, exponent

### My Solution

```js
function findNb(m) {
  // runningTotal used to account for the n series up to the input m
  let runningTotal = 0;
  // n initialized to 0
  let n = 0;
  // until runningTotal reaches m
  while (runningTotal < m) {
    // increment i
    n += 1;

    // add the measure with the prescribed exponent
    runningTotal += Math.pow(n, 3);
  }
  // if the runningTotal matches m return n
  // else -1
  return runningTotal === m ? n : -1;
}
```

### Much Better Solution

```js
function findNb(m) {
  let n = 0;
  while (m > 0) m -= (++n) ** 3;
  return m ? -1 : n;
}
```

Taking advantage of:

- `while` loops and other loops and conditionals not requiring `{` curly `}` braces if the logic is one line long;

- `++n` immediately inrementing the number;

- `**` as a shorthand for the exponent funtion;

- `0` as a falsy value.

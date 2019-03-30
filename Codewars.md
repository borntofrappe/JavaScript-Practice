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

## P2 PMissing Letter

### Task

Write a method that takes an array of consecutive (increasing) letters as input and returns the missing letter in the array.

You will always get a valid array. It will be always exactly one letter missing. The length of the array will always be at least 2. The array will always contain letters in only one case.

```js
function findMissingLetter(array) {
  // code here
}
```

### Tags

for of, entries, charCodeAt, String.fromCharCode

### My Solution

```js
function findMissingLetter(array) {
  // take the first item of the array
  let [startingLetter] = array;
  // initialize a variable to keep track of the missing letter
  let missingLetter;

  // loop through the array with a for of loop applied to the entries of the array (accessing both the index and the item in a 2D array)
  for (const [index, value] of array.entries()) {
    // code for the starting letter incremented by the index
    const expectedLetterCode = startingLetter.charCodeAt() + index;
    // code for the current letter
    const actualLetterCode = value.charCodeAt();
    // if the two don't match
    if (expectedLetterCode !== actualLetterCode) {
      // assign the missing letter to the prescribed variable
      missingLetter = String.fromCharCode(expectedLetterCode);
      // break the loop
      break;
    }
  }
  // return the missing letter
  return missingLetter;
}
```

## P3 Categorize New Member

### Task

The Western Suburbs Croquet Club has two categories of membership, Senior and Open. They would like your help with an application form that will tell prospective members which category they will be placed.

To be a senior, a member must be at least 55 years old and have a handicap greater than 7.

Input will consist of a list of lists containing two items each. Each list contains information for a single potential member, its age and handicap.

```code
[
  [age, hendicap]
]
```

Output will consist of a list of string values stating whether the respective member is to be placed in the senior or open category.

Example

- Input: [[18, 20],[45, 2],[61, 12],[37, 6],[21, 21],[78, 9]]

- Output: ["Open", "Open", "Senior", "Open", "Open", "Senior"]

### Tags

map, ternary operator

### My Solution

destructuring array, ternary operator

```js
function openOrSenior(data){
  return data.map(([age, handicap]) => (age >= 55 && handicap > 7) ? 'Senior' : 'Open');
}
```

## P4 Friend or Foe?

### Task

Make a program that filters a list of strings and returns a list with only your friends' name in it. Condition to be a friend: having a name exactly 4 letter longs

Example

- Input: ["Ryan", "Kieran", "Jason", "Yous"]

- Output: ["Ryan", "Yous"]

### Tags

filter, destructuring property

### My Solution

```js
function friend(friends){
  return friends.filter(({length}) => length === 4);
}
```

## P5 Get the Middle Character

### Task

You are going to be given a word. Your job is to return the middle character of the word. If the word's length is odd, return the middle character. If the word's length is even, return the middle 2 characters.

Examples:

- getMiddle("test"): "es"

- getMiddle("testing"): "t"

### Tags

array index, decimal, floor

### My Solution

```js
function getMiddle(s)
{
  // retrieve the length of the string
  const {length} = s;
  // find the precise halfway point in the string (! 0-based indexing)
  const half = (length - 1) / 2;
  // if index is decimal, s[index] returns undefined
  // take advantage of this to conditionally return the precise character or the adjacent two
  return s[half] ? s[half] : `${s[Math.floor(half)]}${s[Math.floor(half) + 1]}`
}
```

## P6 Highest Scoring Word

### Task

Given a string of words, find the highest scoring word.

Each letter of a word scores points according to it's position in the alphabet: `a = 1, b = 2, c = 3` etc.

If two words score the same, return the word that appears earliest in the original string.

All letters will be lowercase and all inputs will be valid.

Example

- Input: 'man i need a taxi up to ubud'

- Output: 'taxi'

### Tags

split, sort, reduce, charCodeAt, ternary operator

### My Solution

```js
function high(x){
  return x
    // create the array out of the strings separated by whitespace
    .split(' ')
    // sort the array
    .sort((a, b) => {
      // compute the score for each letter
      // considering each letter and its score relative to the lowercase a
      const scoreA = [...a].reduce((acc, curr) => acc += (curr.charCodeAt() - 'a'.charCodeAt() + 1), 0);
      const scoreB = [...b].reduce((acc, curr) => acc += (curr.charCodeAt() - 'a'.charCodeAt() + 1), 0);
      // sort the words based on the higher score
      // ! >= to have scoreA retain its place if the two match
      return scoreA >= scoreB ? -1 : 1;
    })[0]; // return the first item
}
```

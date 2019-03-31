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

## P7 Human Redable Time

### Task

Write a function, which takes a non-negative integer (seconds) as input and returns the time in a human-readable format (HH:MM:SS)

- HH = hours, padded to 2 digits, range: 00 - 99
- MM = minutes, padded to 2 digits, range: 00 - 59
- SS = seconds, padded to 2 digits, range: 00 - 59

The maximum time never exceeds 359999 (99:59:59)

### My Solution

```js
function humanReadable(seconds) {
  // compute the hours and minutes based on the seconds value
  let hours = 0, minutes = 0;
  while(seconds >= 3600) {
    seconds -= 3600;
    hours += 1;
  }
  while(seconds >= 60) {
    seconds -= 60;
    minutes += 1;
  }

  // zero-pad the values
  h = hours > 10 ? hours : `0${hours}`;
  m = minutes > 10 ? minutes : `0${minutes}`;
  s = seconds > 10 ? seconds : `0${seconds}`;
  return `${h}:${m}:${s}`;
}
```

### Tags

time, ternary operator

### Much Better Approach

Computing the number of hours and minutes through basic math:

- the hours by dividing the number of seconds by 3600 and retrieving the integer (non decimal value)

  ```js
  hours = parseInt(seconds / 3600);
  ```

- the minutes by first dividing by 60 (accounting for the hours) and considering what is left through the modulo operator

  ```js
  minutes = parseInt(seconds / 60 % 60);
  ```

  Considering for instance a value of `3700` seconds:

  - `seconds / 60` returns `61.666`;

  - the moduloo `% 60` identifies `1.6`;

  - `parseInt` will consider `1`, the precise number of seconds.

- the number of seconds by using the modulo operator on the number of seconds itself

  ```js
  seconds = seconds % 60;
  ```

  Considering the previous `3700` value, it would identify `40`.

## P8 Create Phone Numbers

### Task

Write a function that accepts an array of 10 integers (between 0 and 9), that returns a string of those numbers in the form of a phone number.

Example:

```js
createPhoneNumber([1, 2, 3, 4, 5, 6, 7, 8, 9, 0]) // => returns "(123) 456-7890"
```

### My Solution

```js
function createPhoneNumber(numbers){
  // target the numbers in a three-three-four pattern
  return numbers.join('').replace(/(\d{3})(\d{3})(\d{4})/, '($1) $2-$3');
}
```

### Tags

regex, replace

## P9 Simple Encryption #1 - Alternating Split

Take every 2nd char from the string, then the other chars, that are not every 2nd char, and concat them as new String.
Do this n times.

```js
function encrypt(text, n) {

}
```

Example:

```js
encrypt("This is a test!", 1); // "hsi  etTi sats!"
encrypt("This is a test!", 2); // "hsi  etTi sats!" -> "s eT ashi tist!"
```

Write two methods:

```js
function encrypt(text, n)
function decrypt(encryptedText, n)
```

For both methods:

- If the input-string is `null` or empty return exactly this value!

- If `n` is `<= 0` then return the input text.

### My Solution

```js
function encrypt(text, n) {
  // consider the foreseen edge cases
  if(!text) return text
  if(n<=0) return text

  // text is not-null, n is greater than 0

  // initialize two variables for the sections of the encrypted string
  // splitB: those characters which need to be appended
  const splitA = [];
  const splitB = [];
  // use a for of loop with array.entries() applied on the letters of the input string
  // this to access both the letter and the index
  for(const [index, value] of [...text].entries()) {
    if(index % 2 == 0) {
      splitB.push(value);
    } else {
      splitA.push(value);
    }
  }
  // recursion: call the encrypt function with n-1. passing the encrypted string
  return encrypt([...splitA, ...splitB].join(''), n - 1);
}

function decrypt(encryptedText, n) {
  // consider the foreseen edge cases
  if(!encryptedText) return encryptedText
  if(n<=0) return encryptedText

  // encryptedText is not-null, n is greater than 0
  // consider the length of the string
  const { length } = encryptedText;
  // consider the halfway point in the string flooring the value
  const halfwayPoint = Math.floor(length / 2);
  // divide encryptedText in two arrays, considering the halves of the string
  const splitA = [...encryptedText].slice(0, halfwayPoint);
  const splitB = [...encryptedText].slice(halfwayPoint);

  // build a string by alternating the letters from the second and first array
  const decrypted = [];
  for(let i = 0; i < length; i+=1) {
    if(i % 2 === 0) {
      decrypted.push(splitB.shift());
    } else {
      decrypted.push(splitA.shift());
    }
  }
  // recursion: return the decrypted string with n-1
  return decrypt(decrypted.join(''), n - 1);
}
```

### Notes

Had a bit of an issue considering the algorithm, but it is perhaps better understood by example:

```js
encrypt("This is a test!", 1); // "hsi  etTi sats!"
```

The second characters are (apparently): `T`, `i`, ` `, `s`, `a`, `t`, `s`, `!`. Considering the index: 0th, 2nd, and so forth. Take such items and attach them at the end of the string.

While challenging, understanding the algorithm makes the encryption part straightforward to implement:

- consider the specific characters in a separate array

- concatenate these characters to the rest of the string

- return the string.

To allow for multiple rounds of encryption, it is actually possible to return the `encrypt` function with the new string and `n-1`. Given the condition:

```js
if(n<=0) return text
```

As soon as `n` hits 0, the finally encrypted string is returned.

Decrypting the string is a tad more challenging:

- consider the length of the string.

- consider half the length of the string, flooring the value (this because of 0-based indexing).

- split the string in the two halves.

- alternate between the letters of the second and first half.

To allow for recursion, proceed as with the encryption logic to return the same function with `n-1`. Alternating between the letters is actually an intriguing operation, which is implemented by alternatively removing the first item of one and the other arrays.

### Tags

recursion, encryption, for of, entries, spread, shift

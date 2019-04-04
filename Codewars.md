# Codewars

> problems, solutions and notes from [codewars](https://www.codewars.com).

## P1 A Pile of cubes

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

## P10 Descending Order

### Task

Your task is to make a function that can take any non-negative integer as a argument and return it with its digits in descending order. Essentially, rearrange the digits to create the highest possible number.

Example:

Input: 21445 - Output: 54421

### My Solution

function descendingOrder(n){
  const highestValue =  n
    // change to string
    .toString()
    // create an array
    .split('')
    // sort in descending order
    // ! the operator > computes the operation on the characters as if they were numbers
    .sort((a, b) => a > b ? -1 : 1)
    // return the sorted series
    .join('');

    // return as integer
    return Number.parseInt(highestValue, 10);
}



## P11 Two to One

### Task

Take 2 strings s1 and s2 including only letters from a to z. Return a new sorted string, the longest possible, containing distinct letters (each taken only once, from either s1 or s2).

### My Solution

function longest(s1, s2) {
  // create a Set out of the concatenated strings
  const set = new Set([...s1, ...s2]);
  // return the set made into an array
  return [...set]
    // sorted alphabetically
    // ! remember a is 97, b 98 and so forth
    .sort((a, b) => a < b ? -1 : 1)
    // as a string
    .join('');
}


### Tags

set, destructuring, sort, ternary operator


## P12 Word a10n (abbreviation)

### Task

The word i18n is a common abbreviation of internationalization in the developer community, used instead of typing the whole word and trying to spell it correctly. Similarly, a11y is an abbreviation of accessibility.

Write a function that takes a string and turns any and all "words" (see below) within that string of length 4 or greater into an abbreviation, following these rules:

A "word" is a sequence of alphabetical characters. By this definition, any other character like a space or hyphen (eg. "elephant-ride") will split up a series of letters into two words (eg. "elephant" and "ride").
The abbreviated version of the word should have the first letter, then the number of removed characters, then the last letter (eg. "elephant ride" => "e6t r2e").

### My Solution

```js
function abbreviate(string) {
  // array of words
  const words = string.split(' ');
  // map through the words returning the first and last letter separated by the number of letters in between
  const abbr = words.map(word => `${word[0]}${word.length - 2}${word[word.length - 1]}`);

  // return the abbreviated words
  return abbr.join(' ');
}
```

In a single line.

```js
function abbreviate(string) {
  return string
    // split into an array of words
    .split(' ')
    // map through the words returning the first and last letter separated by the number of letters in between
    .map(word => `${word[0]}${word.length - 2}${word[word.length - 1]}`)
    // return as a string
    .join(' ');
}
```

Accounting for separators which can be anything but a character. (and fulfilling the condition that the word must be 4 or more characters long)<>

```js
function abbreviate(string) {
  // build an array of the possible separators (anything but a character)
  const separators = string.match(/\W/g);

  // create an array with the abbreviated words
  const abbr = string
    // split into an array of words
    // ! based on the same regex making up the separators
    .split(/\W/g)
    // map through the words returning the first and last letter separated by the number of letters in between
    // ! if the word is 4 characters or more long
    .map((word) => word.length >= 4 ? `${word[0]}${word.length - 2}${word[word.length - 1]}` : word);

  // if there are separators, map through the abbreviated words and include the separators for all but the last words
  // in order
  return separators ? abbr
                      .map((word, index) => (index < abbr.length - 1) ? `${word}${separators[index]}` : `${word}`)
                      // return as a string
                      .join('')
                    // if there are no separators return the single word
                    :
                      abbr.join('');
}
```

### Much Better Solution

Find those words which are four or more characters long and using the regex function `replace` create the desired abbreviated version.

```js
var find = /[a-z]{4,}/gi;
function replace(match) { return match[0] + (match.length - 2) + match[match.length - 1]; }

function abbreviate(string) {
  return string.replace(find, replace);
}
```

Much clearner. Benefiting from the fact that `string.replace` accepts as a second argument a function which can operate on the matches sequentially.

With backticks, the function can also be conveniently rewritten as follows:

```js
function abbreviate(string) {
  return string.replace(/\w{4,}/gi, (match) => `${match[0]}${match.length - 2}${match[match.length - 1]}`);
}
```

### Tags

regex, replace

## P13 Equal sides of an array

### Task

You are going to be given an array of integers. Your job is to take that array and find an index N where the sum of the integers to the left of N is equal to the sum of the integers to the right of N. If there is no index that would make this happen, return `-1`.

Example

Input: [1,2,3,4,3,2,1]
Output: 3, given that [1,2,3] sum up to be the same as [3,2,1]

Another example

Input: [1,100,50,-51,1,1]
Output: 1, given that [1] is the same as [50, -51, 1, 1] combined

Another example, expressing how empty arrays in this exercise are equal to 0

Input: [10, 10, -20]
Output: 0, given that [10, 10, -20] sum up to 0 and you start with 0 when confronting the values.

The `for of` loop seems to be appropriate, as it allows to easily break out of a loop when a condition is met. It also seems appropriate given that even with multiple combinations, the index to be returned is the first one which fulfills the requirement.

### My Solution

```js
function findEvenIndex(arr)
{
  // initialize a variable in which to describe the index, if existing
  let solution = -1;

  // consider the sum of all items
  const sumAll = arr.reduce((acc, curr) => acc += curr, 0);
  // if 0, immediately update the solution
  if(sumAll === 0) {
    solution = sumAll;
    // else consider the array one item at a time
  } else {
    // loop through the array considering both the index and the value of the array at each iteration
    for(const [index, value] of arr.entries()) {
      // consider the sum of all items after the index
      const sumAfter = arr
        .slice(index + 1)
        .reduce((acc, curr) => acc += curr, 0);

      // consider the sum of all items up to the index
      const sumBefore = arr
        .slice(0, index)
        .reduce((acc, curr) => acc += curr, 0);

      // if the two match update the solution and break out of the loop
      if (sumAfter === sumBefore) {
        solution = index;
        break;
      }
    }
  }

  // return the solution (-1, 0 or the index depending on the logic)
  return solution;
}
```

### Notes

I am not particularly happy with the conditional checking if the sum of all items is 0. Especially given how the reduce applied to an empty array:

```js
[].reduce((acc, curr) => acc += curr, 0);
```

Already returns 0. That being said, the issue is with the index itself. If the sum is already 0, it won't be picked up by slicing the array starting from the second item: `.slice(index + 1)`.

### Tags

reduce, for of

## P14 Give me a diamond

### Task

You need to return a string that displays a diamond shape on the screen using asterisk ("*") characters. Please see provided test cases for exact output format.

The shape that will be returned from print method resembles a diamond, where the number provided as input represents the number of *’s printed on the middle line. The line above and below will be centered and will have 2 less *’s than the middle line. This reduction by 2 *’s for each line continues until a line with a single * is printed at the top and bottom of the figure.

Return `null` if input is even number or negative (as it is not possible to print diamond with even number or negative number).

For instance with `n === 3`

```text
 *
***
 *
```

With `n === 5`

```text
  *
 ***
*****
 ***
  *
```


### My solution

```js
function diamond(n){
  if (n % 2 === 0 || n < 0) return null;

  // build the middle line
  let diam = '*'.repeat(n);
  // initialize a variable to keep track of the whitespace (1 for each new line)
  let whitespace = 0;

  // when n === 3, the last line will be 1 character long
  while(n >= 3) {
    // decrement by 2 the number of asterisks
    n -= 2;
    // increment by 1 the number of spaces
    whitespace += 1;
    // build the new line with the prescribed number of spaces and asterisks
    const newLine = `${' '.repeat(whitespace)}${'*'.repeat(n)}`;
    // wrap the previous structure in two new lines
    diam = `${newLine}\n${diam}\n${newLine}`;
  }
  // return the diamond structure
  return diam + '\n';
}
```

### Notes

Not really satisfied with the solution, especially the last concatenated new line. That one was necessary to pass the suite of tests set up by the challenge, but overall the structure can be improved. Perhaps using the recent functions of `padStart()` or `padEnd()`.

### Tags

repeat, while

## P15 Baking Cakes

### Task

Write a function `cakes()`, which takes the recipe (object) and the available ingredients (also an object) and returns the maximum number of cakes it is possible can bake (integer). For simplicity there are no units for the amounts (e.g. 1 lb of flour or 200 g of sugar are simply 1 or 200). Ingredients that are not present in the objects, can be considered as 0.

Example:

Input: `cakes({flour: 500, sugar: 200, eggs: 1}, {flour: 1200, sugar: 1200, eggs: 5, milk: 200});`

Output: `2`

### My solution

```js
function cakes(recipe, available) {
  // retrieve the ingredients from the recipe
  const ingredients = Object.entries(recipe);
  // map through the 2D array to compare the recipe's and available's ingredients
  const possibleCakes = ingredients
    // consider the ingredient and amount from the recipe
    .map(([ingredient, amount]) => {
      // detail if the ingredient exist in the available array
      const isAvailable = available[ingredient];
      // if available return the number of cakes hypothetically possible considering the single ingredient
      if(isAvailable) {
        const amountAvailable = Math.floor(available[ingredient] / amount);
        return amountAvailable;
      }
      // else return 0
      return 0;
    })
    // sort from smallest to biggest amount
    .sort((a, b) => a > b ? 1 : -1);

  // return the first number, describing the least number of cakes with the available ingredients
  return possibleCakes[0];
}
```

### Tags

map, destructuring, object, entries

## P16 Multiplication Table

### Task

Create a function that accepts dimensions, for rows and columns, as parameters in order to create a multiplication table sized according to the given measures. The return value of the function must be an array, and the numbers must be numbers, not strings.

Example.

```js
multiplicationTable(3,3)
/* multiplication table
1 2 3
2 4 6
3 6 9

actual output [[1,2,3],[2,4,6],[3,6,9]]
*/
```

Each value on the table should be equal to the value of multiplying the number in its first row times the number in its first column. (like  6 being 3 * 2).

### My Solution

```js
function multiplicationTable(row,col){
  const table = [];
  for(let i = 0; i < row; i+=1) {
    table.push([]);
    for(let j = 0; j < col; j+=1) {
      table[i].push((i+1) * (j+1))
    }
  }
  return table;
}
```

### Tags

table, for


## P17 Count characters in your string

The main idea is to count all the occuring characters(UTF-8) in string. If you have string like this aba then the result should be { 'a': 2, 'b': 1 }

What if the string is empty ? Then the result should be empty object literal { }

### My Solution

```js
function count (string) {
  // return a single object
  return [...string].reduce((acc, curr) => {
  // acc refers to an object in which each letter is either added or counted (if already existed)
  // curr refers to the current letter
    if(acc[curr]) {
      acc[curr] += 1;
    } else {
      acc[curr] = 1;
    }
    // return the updated object
    return acc;
  }, {});
}
```

### Notes

You could also solve the problem by splitting the word into an array and looping with a `forEach`, adding and enumerating the letters in a separate object.

### Tags

reduce, object

## P18 Consecutive Powers

### Task

The number 89 is the first integer with more than one digit for which the following is true.

```code
89 = 8^1 + 9^2
```

The next number having this property is 135.

```code
135 = 1^1 + 3^2 + 5^3
```

We need a function to collect these numbers. A function receiving two integers `a`, `b` which defines the range [a, b] (inclusive) and returning a list of numbers which fulfills the described property.

Another example:

```code
sumDigPow(1, 10) == [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Given that the first one-digit numbers all satisfy the condition that `x^1 = x`.

### My Solution

```js
function sumDigPow(a, b) {
  // array in which to store the solution
  const solution = [];
  // loop in the specified interval
  for(let i = a; i < b; i+= 1) {
    // consider an array of the integers making up the number
    const digits = i.toString().split('').map(num => Number.parseInt(num, 10));
    // consider the desired value (firstDigit ^ 1 + secondDigit ^ 2 + ...)
    const pow = digits.reduce((acc, curr, index) => acc + Math.pow(curr, (index + 1)), 0);
    // if the two match add the value to the solutions array
    if(i === pow) {
      solution.push(i);
    }
  }
  // return the solution array
  // if no match has been found, it is equal to an empty array
  return solution;
}
```

### Tags

for, pow, reduce

## P19 Replace with Alphabeth Position

### Task

You are required to replace every letter in a string with its position in the alphabet.

If anything in the text isn't a letter, ignore it and don't return it.

### Solution

```js
function alphabetPosition(text) {
  return text
    // remove anything that is not a character
    .replace(/[^a-z]/gi, '')
    // replace each letter with their position relative to the letter 'a'
    // ! concatenate a string with a space to have the value returned as a string, with a space
    .replace(/[a-z]/gi, (match) => match.toLowerCase().charCodeAt() - 'a'.charCodeAt() + 1 + ' ')
    // remove the last character making up an unnecessary space
    .slice(0, -1);
}
```

### Tags

regex, replace, match

## P20 Consonant Value

Given a lowercase string that has alphabetic characters only and no spaces, return the highest value of consonant substrings.

For example:

```js
solve("zodiacs") = 26
```

Because the consonant substrings are: z, d and cs with values z = 26, d = 4 and cs = 3 + 19 = 22. The highest is 26.

Note that the value of a = 1, b = 2 ... z = 26, while vowels are a,e,i,o,u.

### Solution

```js
function solve(s) {
  return s
    // split the string on the basis of vowels
    .split(/[aeiou]/)
    // map through the array of consonants computing for each set of consonants the value on the basis of the mentioned algorithm
    // ! consonants might actually refer to a single letter
    .map(consonants => [...consonants].reduce((acc, curr) => acc + (curr.charCodeAt() - 'a'.charCodeAt() + 1), 0))
    // sort in descending order and return the first value
    .sort((a, b) => a > b ? -1 : 1)[0];
};
```

### Tags

split, map, reduce, sort

## P21 Ten Minute Walk

###Task

You live in the city of Cartesia where all roads are laid out in a perfect grid. You arrived ten minutes too early to an appointment, so you decided to take the opportunity to go for a short walk. The city provides its citizens with a Walk Generating App on their phones -- everytime you press the button it sends you an array of one-letter strings representing directions to walk (eg. ['n', 's', 'w', 'e']). You always walk only a single block in a direction and you know it takes you one minute to traverse one city block, so create a function that will return true if the walk the app gives you will take you exactly ten minutes (you don't want to be early or late!) and will, of course, return you to your starting point. Return false otherwise.

Note: you will always receive a valid array containing a random assortment of direction letters ('n', 's', 'e', or 'w' only). It will never give you an empty array (that's not a walk, that's standing still!).

### Solution

```js
function isValidWalk(walk) {
  // create an object with the cardinal points, each depicting a direction in a made-up (x,y) coordinate system
  const cardinals = {
    n: [0, 1],
    s: [0, -1],
    w: [-1, 0],
    e: [1, 0]
  };
  // if the array is more or less than 10 items long, immediately return false
  if(walk.length !== 10) {
    return false;
  }
  // loop through the walk array and compute the final (x, y) location considering each cardinal point
  const finalPoint = walk.reduce((acc, curr) => {
    // find the change in x and y
    const [x, y] = cardinals[curr];
    // update the accumulator's array
    acc[0] += x;
    acc[1] += y;
    // remember to return the accumulator
    return acc;
  }, [0, 0]);
  // if the final point is [0,0] return true
  const [finalX, finalY] = finalPoint;
  return (finalX === 0 && finalY === 0);
}
```

### Tags

reduce, object, array

## P22 Autocomplete

### Task

The autocomplete function will take in an input string and a dictionary array and return the values from the dictionary that start with the input string. If there are more than 5 matches, restrict your output to the first 5 results. If there are no matches, return an empty array.

Example

```js
autocomplete('ai', ['airplane','airport','apple','ball']); // ['airplane','airport']
```

The dictionary will always be a valid array of strings. Returb all results in the order given in the dictionary, even if they're not always alphabetical. The search should not be case sensitive, but the case of the word should be preserved when it's returned.

For example, "Apple" and "airport" would both return for an input of 'a'. However, they should return as "Apple" and "airport" in their original cases.

Any input that is not a letter should be treated as if it is not there.

### Solution

```js
function autocomplete(input, dictionary) {
  // create a regular expression out of the input string
  // beginning with the input
  // case insensitive
  // ! removing anything that is not a letter
  const regex = new RegExp(`^${input.replace(/[^a-z]/gi, '')}`, 'i');

  // create an array in which to store the solution
  const solution = [];

  // loop through the dictionary array
  for(const word of dictionary) {
    // add the word to the solution's array if the regex matches
    if(regex.test(word)) {
      solution.push(word);
    }
  }

  // return the solution's array and specifically the first 5 matches
  return solution.slice(0, 5);
}
```

### Notes

The solution can be definitely improved with a `filter` function.

```js
function autocomplete(input, dictionary) {
  // regex for the input word, disregarding case and considering only letters
  const regex = new RegExp(`^${input.replace(/[^a-z]/gi, '')}`, 'i');

  // return the first 5 items of the dictionary array, filtered on the basis of the regex
  return dictionary
    .filter(word => regex.test(word))
    .slice(0, 5);
}
```

Much nicer.

### Tags

regex, for of, slice, filter


## P23 - ROT13

### Task

```js
rot13("EBG13 rknzcyr."); // "ROT13 example."
rot13("This is my first ROT13 excercise!"); // "Guvf vf zl svefg EBG13 rkprepvfr!"
```

### Notes

ROT13 seems to be a rather straightforward letter-substitution cipher, where each letter is replaced by the 13th letter following it. 13th means that by passing the input string through the cipher twice you have the input string back in its original form. This makes it rather silly, but also useful for messages that are meant to be easily ciphered _and_ deciphered.

```js
function rot13(str) {
  // compute the code of the thirtheenth lowercase letter
  const letterCode = 'a'.charCodeAt() + 13;
  // return the string where each letter is replaced following the algorithm's instructions
  return str.replace(/[a-z]/gi, (match) => {
    // to decide whether to add or remove 13, consider the code of the lower case match vis a vis the code of the 13th lowercase letter
    const matchCode = match.charCodeAt();
    const matchLetterCode = match.toLowerCase().charCodeAt();
    // return the match according to the comparison between codes
    return (matchLetterCode < letterCode) ? String.fromCharCode(matchCode + 13) : String.fromCharCode(matchCode - 13);
  });
}
```

## P24 Clock in Mirror

### Task

Complete the function `WhatIsTheTime(timeInMirror)`, where timeInMirror is the mirrored time as string.

Return the real time as a string.

Consider hours to be between 1 <= hour < 13. There is no 00:20, but instead 12:20. There is no 13:20, but instead 01:20.

Examples

```text
05:25 --> 06:35

01:50 --> 10:10

11:58 --> 12:02

12:01 --> 11:59
```

### Solution

```js
function WhatIsTheTime(timeInMirror) {
  // retrieve the hours and minutes in the mirrored clock
  const [hoursInMirror, minutesInMirror] = timeInMirror
    // split using the colon
    .split(':')
    // return as integers
    .map(time => Number.parseInt(time));

  // compute the minutes as the difference from the 60 mark, considering the [0-59] range
  const minutes = (60 - minutesInMirror) % 60;
  // compute the hours considering that anything greater than 0 minutes account for an additional hour
  let hours = (minutes > 0) ? (12 - (hoursInMirror - 12 + 1)) : (12 - (hoursInMirror - 12));

  // 12 hours clock
  if(hours > 12) {
    hours = hours % 12;
  }

  // return the 0 padded values
  return `${hours >= 10 ? hours : `0${hours}`}:${minutes >= 10 ? minutes : `0${minutes}`}`;
}
```

### Tags

split, basic math

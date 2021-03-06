# README

## \#1 \(code wars\)

### Count the number of Duplicates

Write a function that will return the count of distinct case-insensitive alphabetic characters and numeric digits that occur more than once in the input string. The input string can be assumed to contain only alphabets \(both uppercase and lowercase\) and numeric digits.

#### Example

```bash
"abcde" -> 0 # no characters repeats more than once
"aabbcde" -> 2 # 'a' and 'b'
"aabBcde" -> 2 # 'a' occurs twice and 'b' twice (bandB)
"indivisibility" -> 1 # 'i' occurs six times
"Indivisibilities" -> 2 # 'i' occurs seven times and 's' occurs twice
"aA11" -> 2 # 'a' and '1'
"ABBA" -> 2 # 'A' and 'B' each occur twice
```

### My solution

```javascript
function duplicateCount(text){

  //operates with string and array, match stores aray of matching chars
  let match = text.toLowerCase().
              split('').sort().join('').
              match(/([^])\1+/g);

  //if no text provided or no dublicates found, reasignns match to empty array
  if (match === null){
    match = [];
  }

  return (match.length);
}
```

## \#2 \(code wars\)

### Double Char

Given a string, you have to return a string in which each character \(case-sensitive\) is repeated once.

#### Example

```text
doubleChar("String") ==> "SSttrriinngg"
doubleChar("Hello World") ==> "HHeelllloo  WWoorrlldd"
doubleChar("1234!_ ") ==> "11223344!!__  "
```

#### My solution

```javascript
function doubleChar(str) {

  //splits the string in to array, modifies each element 
  //by adding same element twice, joins everithing in to the string
  let copyStr = str.split('').
                map((e) => `${e}${e}`).
                join('');

  return copyStr;
}
```

## \#3 \(Code wars\)

### Growing plant

Task Each day a plant is growing by upSpeed meters. Each night that plant's height decreases by downSpeed meters due to the lack of sun heat. Initially, plant is 0 meters tall. We plant the seed at the beginning of a day. We want to know when the height of the plant will reach a certain level.

Example For upSpeed = 100, downSpeed = 10 and desiredHeight = 910, the output should be 10.

```bash
 After day 1 --> 100
 After night 1 --> 90
 After day 2 --> 190
 After night 2 --> 180
 After day 3 --> 280
 After night 3 --> 270
 After day 4 --> 370
 After night 4 --> 360
 After day 5 --> 460
 After night 5 --> 450
 After day 6 --> 550
 After night 6 --> 540
 After day 7 --> 640
 After night 7 --> 630
 After day 8 --> 730
 After night 8 --> 720
 After day 9 --> 820
 After night 9 --> 810
 After day 10 --> 910
```

For upSpeed = 10, downSpeed = 9 and desiredHeight = 4, the output should be 1.

Because the plant reach to the desired height at day 1\(10 meters\).

```bash
 After day 1 --> 10
```

#### My solution

```javascript
function growingPlant(upSpeed, downSpeed, desiredHeight) {

  var dayCounter = 0;
  var currentHeight = 0;

  while(true){

      //calculates plant height after the day
      currentHeight = currentHeight + upSpeed;
      dayCounter ++;

      //if plant height reaches necesary height function returns day count
      if(currentHeight >= desiredHeight) return dayCounter;

      //calculates height of plant after a night
      currentHeight = currentHeight - downSpeed;

  }
```

## \#4

### Shoolace algorithm

Figure out whitch way line is drawn in 2D space \(clockwise or counter-clockwise\).

#### Example

\(5,10\) \(15,20\) \(20,7\) is drawn clockwise \(5,10\) \(20,7\) \(15,20\) is drawn counter-clockwise \(4,3\) \(3,3\) \(3,5\) \(6,5\) \(6,3\) \(5,3\) \(5,2\) \(7,2\) \(7,6\) \(2,6\) \(2,2\) \(4,2\) is drawn counter-clockwise

#### My solution

Algorithm is used to calculate area of 2d shape. But in this case it is used to determine if 2d shape is drawn clockwise or counterclockwise.

This algorithm do not work on shapes with line crossings

```javascript
// ****************************
// To solve this proglem gausian area aproach is used
// ****************************

// initial points of figure in x,y plain
let points = [
  [4,3], [3,3], [3,5], [6,5], [6,3], [5,3], [5,2], [7,2], [7,6], [2,6], [2,2], [4,2]
];

rotation(points);

//works only for figures without line intersections
function rotation(corners) {

  let x = 0;
  let y = 0;

  //loops trought all points
  for (let i = 0; i < corners.length-1; i++) {
    x = x + (corners[i][0] * corners[i + 1][1]);
    y = y + (corners[i][1] * corners[i + 1][0]);
  }

 //determines rotation
  if (x - y < 0) {
    console.log("Clockwise");
  } else if (x - y>0) {
    console.log("Counterclockwise");
  } else {
    console.log("Smthing wrong")
  }

}
```

## \#5

### Hide phone numbers

You work in an office and your boss has asked you to download from the database the full list of subscribers of your newsletter. You need to hide subscribers' phone numbers and check their prefixes in order to send the encrypted file to a client.

Your tasks are: _to hide the last six digits of each phone number_ to check validity of prefixes

#### Examples

If prefixes are different from the three indicated above `(+39, 0039, 1)` return `false`.

The valid formats for the Italian and US \(the last one\) numbers are the following:

\*CASE 1: `+39 <separator> ### <separator> ### <separator> ####`

\*CASE 2: `0039 <separator> ### <separator> ### <separator> ####`

\*CASE 3: `1 <separator> ### <separator> ### <separator> ####`

The list of separators is the following:

for Italian numbers: `" ", ".", ""` for US numbers: `" ", ".", "", "-"`

#### My solution

```javascript
function encryptNum(number) {

      //used for counting 6 digits from the end of the number
      let count = 0;

      //checks if number hase corect form from begining (country code etc.)
      if(number.match(/^((\+|00)39|\b1[02-9-\s\.])/g)){

            return number.split('').reverse().map( (e,i) => {

                //if elment is a digit then replace it with "X"
                if (e.match(/\d/g) && count < 6) {
                  count ++;
                  return "X"
                } else return e

            }).reverse().join('')

      } else return false
}
```

#### Some more solutions

```javascript
function encryptNum(number) {
  return /^((\+|00)39([ .]?\d{3}){3}|1([ .-]?\d{3}){3})\d$/.test(number)
  ? number.replace(/(\d\D?){6}$/, x => x.replace(/\d/g, 'X'))
  : false; 
}
```

## \#6

### Find Unique number

There is an array with some numbers. All numbers are equal except for one. Try to find it!

```bash
findUniq([ 1, 1, 1, 2, 1, 1 ]) === 2
findUniq([ 0, 0, 0.55, 0, 0 ]) === 0.55
```

It’s guaranteed that array contains more than 3 numbers.

The tests contain some very huge arrays, so think about performance.

#### My solution

```javascript
function findUniq(arr) {

  let length = arr.length;

  //sorting the array, single number will be on one side of array
  arr.sort()

  //find out on whitch side of array number is
  if(arr[0] != arr[1]){
    return arr[0]
  }
  if(arr[length-2] != arr[length-1] ){
    return  arr[arr.length-1]
  }
}
```

## \#6

### Sort array by string length

Write a function that takes an array of strings as an argument and returns a sorted array containing the same strings, ordered from shortest to longest.

For example, if this array were passed as an argument:

`["Telescopes", "Glasses", "Eyes", "Monocles"]`

Your function would return the following array:

`["Eyes", "Glasses", "Monocles", "Telescopes"]`

All of the strings in the array passed to your function will be different lengths, so you will not have to decide how to order multiple strings of the same length.

#### My solution

```javascript
function sortByLength (array) {
  // Return an array containing the same strings, ordered from shortest to longest

return array.map((e,i) => {

             //creates objects for aech array item with array names and lengths
              return { key    : e , 
                       length : e.length}
            })

             //sorts by lengths
            .sort((a, b) => a.length - b.length)

            //removes lengths, leaving only lengths
            .map((e, i) => e.key)

};
```

## \#7

```javascript
/* 
Write a function called guessingGame which takes in one parameter amount. The function should return another function that takes in a parameter called guess. In the outer function, you should create a variable called answer which is the result of a random number between 0 and 10 as well as a variable called guesses which should be set to 0.

In the inner function, if the guess passed in is the same as the random number (defined in the outer function) - you should return the string "You got it!". If the guess is too high return "Your guess is too high!" and if it is too low, return "Your guess is too low!". You should stop the user from guessing if the amount of guesses they have made is greater than the initial amount passed to the outer function.

You will have to make use of closure to solve this problem.

Examples (yours might not be like this, since the answer is random every time):

    var game = guessingGame(5)
    game(1) // "You're too low!"
    game(8) // "You're too high!"
    game(5) // "You're too low!"
    game(7) // "You got it!"
    game(1) // "You are all done playing!"

    var game2 = guessingGame(3)
    game2(5) // "You're too low!"
    game2(3) // "You're too low!"
    game2(1) // "No more guesses the answer was 0"
    game2(1) // "You are all done playing!"
*/

function guessingGame(amount){
    let answer = Math.floor(Math.random() * Math.floor(10));
    let counter = 0;
    return function guess(guess){
        if(counter >= amount) 
            return "number of guesses are exceeded"
        if(guess>answer){
            counter++;
            return "high";
        }else if(guess<answer){
            counter++;
            return "low";
        }
        return guess+ " is correct!";
    }
}
```

## \#8

```javascript
/* 
Write a function called flip which accepts a function and a value for the keyword this. Flip should return a new function that when invoked, will invoke the function passed to flip with the correct value of the keyword this and all of the arguments passed to the function REVERSED. HINT - if you pass more than two parameters to flip, those parameters should be included as parameters to the inner function when it is invoked. You will have to make use of closure! 

Flip should return a new function that when invoked takes the correct number of required arguments to that function which are then reversed. HINT - you will need to use the .length property on functions to figure out the correct amount of arguments. For example:

flip(subtractFourNumbers,this,11,12,13,14,15)(1,2,3,4,5,6,7,8,9,10) 

Examples:

    function personSubtract(a,b,c){
        return this.firstName + " subtracts " + (a-b-c);
    }

    var person = {
        firstName: 'Elie'
    }

    var flipFn = flip(personSubtract, person);
    flipFn(3,2,1) // "Elie subtracts -4"

    var flipFn2 = flip(personSubtract, person, 5,6);
    flipFn2(7,8). // "Elie subtracts -4"

    function subtractFourNumbers(a,b,c,d){
        return a-b-c-d;
    }

    flip(subtractFourNumbers,this,1)(2,3,4) // -2
    flip(subtractFourNumbers,this,1,2)(3,4) // -2
    flip(subtractFourNumbers,this,1,2,3)(4) // -2
    flip(subtractFourNumbers,this,1,2,3,4)() // -2
    flip(subtractFourNumbers,this)(1,2,3,4) // -2
    flip(subtractFourNumbers,this,1,2,3)(4,5,6,7) // -2
    flip(subtractFourNumbers,this)(1,2,3,4,5,6,7,8,9,10) // -2
    flip(subtractFourNumbers,this,11,12,13,14,15)(1,2,3,4,5,6,7,8,9,10) // -22

*/

function flip(fn, thisArg){
    //converts alay like to aray and clices off first two args
    let args1 = [].slice.call(arguments,2);
    return function() { 
        let args2 = [].slice.call(arguments);
        let arr = args1.concat(args2)
        let arrReverse = arr.slice(0,4).reverse()
        return fn.apply(thisArg, arrReverse)
    }
}
```

## \#9

```javascript
/* 
Write a function called bind which accepts a function and a value for the keyword this. Bind should return a new function that when invoked, will invoke the function passed to bind with the correct value of the keyword this. HINT - if you pass more than two parameters to bind, those parameters should be included as parameters to the inner function when it is invoked. You will have to make use of closure!

Examples:

    function firstNameFavoriteColor(favoriteColor){
        return this.firstName + "'s favorite color is " + favoriteColor
    }

    var person = {
        firstName: 'Elie'
    }

    var bindFn = bind(firstNameFavoriteColor, person);
    bindFn('green') // "Elie's favorite color is green"

    var bindFn2 = bind(firstNameFavoriteColor, person, 'blue');
    bindFn2('green') // "Elie's favorite color is blue" 

    function addFourNumbers(a,b,c,d){
        return a+b+c+d;
    }

    bind(addFourNumbers,this,1)(2,3,4) // 10
    bind(addFourNumbers,this,1,2)(3,4) // 10
    bind(addFourNumbers,this,1,2,3)(4) // 10
    bind(addFourNumbers,this,1,2,3,4)() // 10
    bind(addFourNumbers,this)(1,2,3,4) // 10
    bind(addFourNumbers,this)(1,2,3,4,5,6,7,8,9,10) // 10

*/

function bind(fn, thisArg){
    //converts alay like to aray and clices off first two args
    let args1 = [].slice.call(arguments,2);
    return function() { 
        let args2 = [].slice.call(arguments);
        let allArgs = args1.concat(args2);
        return fn.apply(thisArg, allArgs)
    }
}
```

## \#10

### Description

#### My solution

```javascript
function isIsogram(str){
  //...
  c = []; //array with chars
  r = true; //resault tro or false

  str.toLowerCase().split("").map(e => {

  if(c.includes(e)){ //check if elemnt already in check array
      r = false;     
  }
  c.push(e); //pushes elemnt to check array
  return e;
  })

  return r;
}
```

```python
def is_isogram(string):
    #your code here

    l = list(string.lower())

    sortedString = "".join(sorted(l));

    setOfSorted = "".join(sorted((set(sortedString)))) # gets dictionary with unique keys, sorts, joins to string

    return sortedString == setOfSorted
```

#### Best solution

```javascript
function isIsogram(str){ 
  return !/(\w).*\1/i.test(str)
}
```

## \#11

### Description

You are going to be given a word. Your job is to return the middle character of the word. If the word's length is odd, return the middle character. If the word's length is even, return the middle 2 characters.

#### My solution

```javascript
function getMiddle(s)
{ 
  if(s.length % 2 === 1){
    return s[(s.length/2)-0.5] //returns middle letter
  }else{
   return s.substring((s.length/2)-1, (s.length/2)+1) //return two middle letters
  }

}
```

#### Best solution

```javascript
function getMiddle(s)
{
  return s.substr(Math.ceil(s.length / 2 - 1), s.length % 2 === 0 ? 2 : 1);
}
```

## \#12

### Description

Implement a function that adds two numbers together and returns their sum in binary. The conversion can be done before, or after the addition.

The binary number returned should be a string.

#### My solution

```javascript
function addBinary(a,b) {
  return (a+b).toString(2)
}
```

## \#13

### Description

Given an array, find the int that appears an odd number of times.

There will always be only one integer that appears an odd number of times.

### My solution

```javascript
function findOdd(A) {

  let u = {}

  A.map(e=>{ u[e] = (u[e]) ? (u[e]+1) : 1 }) //pushes new values or updates values to {}

  let oddCount = Object.values(u).find(e => e%2 === 1) //gets odd count from value array

  let indexOfResoult = Object.values(u).indexOf(oddCount) //gets index of odd number in vallue array

  return parseInt(Object.keys(u)[indexOfResoult]); // based on index get resault from keys array and parse from string to int
}
```

### Best solution

```javascript
const findOdd = (xs) => xs.reduce((a, b) => a ^ b);
```

OR

```javascript
function findOdd(A) {
  return A.reduce(function(c,v){return c^v;},0);
}
```

## \#14

### Description

You get an array of arrays. If you sort the arrays by their length, you will see, that their length-values are consecutive. But one array is missing!

You have to write a method, that return the length of the missing array.

```text
Example:
[[1, 2], [4, 5, 1, 1], [1], [5, 6, 7, 8, 9]] --> 3
```

If the array of arrays is null/nil or empty, the method should return 0.

When an array in the array is null or empty, the method should return 0 too! There will always be a missing element and its length will be always between the given arrays.

Have fun coding it and please don't forget to vote and rank this kata! :-\)

I have created other katas. Have a look if you like coding and challenges.

### My solution

```javascript
function getLengthOfMissingArray(arrayOfArrays) {

  //determines aray is null or consist of only one array
  if(arrayOfArrays === null || arrayOfArrays.length === 0) return 0

  //return 0 if array of arrays contains null
  if(arrayOfArrays.indexOf(null) >= 0) return 0

  //creates sorted array with lengths of arrays
  let arrayOfArrayLengths = arrayOfArrays
                                .map(e=>e.length)
                                .sort((a,b)=> a - b)
  //return if array contains empty array
  if(arrayOfArrayLengths[0] === 0) return 0

  for(let i = 0; i < arrayOfArrayLengths.length-1; i++)
    if((arrayOfArrayLengths[i+1]-arrayOfArrayLengths[i]) === 2 ) return arrayOfArrayLengths[i] + 1

}
```

### Best solution

```javascript
tLengthOfMissingArray = a => a ? (a = a.map(e => e ? e.length : 0)).includes(0) ? 0 : a
  .sort((x, y) => x - y)
  .reduce((r, e, i, a) => r ? r : (e + 1) === a[i + 1] ? 0 : e + 1, 0) : 0;
```

## \#15

### Description

A pangram is a sentence that contains every single letter of the alphabet at least once. For example, the sentence "The quick brown fox jumps over the lazy dog" is a pangram, because it uses the letters A-Z at least once \(case is irrelevant\).

Given a string, detect whether or not it is a pangram. Return True if it is, False if not. Ignore numbers and punctuation.

### My code

```javascript
function isPangram(string){

  let regex = /(?=.*a)(?=.*b)(?=.*c)(?=.*d)(?=.*e)(?=.*f)(?=.*g)(?=.*h)(?=.*i)(?=.*j)(?=.*k)(?=.*l)(?=.*m)(?=.*n)(?=.*o)(?=.*p)(?=.*q)(?=.*r)(?=.*s)(?=.*t)(?=.*u)(?=.*v)(?=.*w)(?=.*x)(?=.*y)(?=.*z)./i;
  return regex.test(string) 

}
```

### Best solution

```javascript
function isPangram(string){
  string = string.toLowerCase();
  return "abcdefghijklmnopqrstuvwxyz".split("").every(function(x){
    return string.indexOf(x) !== -1;
  });
}
```

## \#16

### Description

### My solution

```javascript
function solution(input, markers) {

let arr = input.split("\n")

let solution = [];

//iterates trougth just splited sentance parts
for(e of arr){
  let marker;

  //finds what marker to use
  for(m of markers){
    if(e.includes(m)){
      marker = m
    }
  }

  //runs if any markers need to be used for string
  if(marker != undefined){
    let temp = e.split("").splice(0,e.indexOf(marker)).join("")

    solution.push(temp)
  }else{
    solution.push(e)
  }
}

 return solution
           .map(e=>{

                  //removes " "
                  if(e[e.length-1] === " ")  
                    return e.split("").splice(0, e.length-1).join("");
                  else
                    return e

                })
            .join("\n")

}
```

### Best solution

```javascript
function solution(input, markers){
  return input.replace(new RegExp("\\s?[" + markers.join("") + "].*(\\n)?", "gi"), "$1");
}
```

```javascript
function solution(input, markers) {
  return input.split('\n').map(
    line => markers.reduce(
      (line, marker) => line.split(marker)[0].trim(), line
    )
  ).join('\n')
}
```

## \#17

### Description

Take 2 strings s1 and s2 including only letters from ato z. Return a new sorted string, the longest possible, containing distinct letters,

each taken only once - coming from s1 or s2. Examples:

```text
a = "xyaabbbccccdefww"
b = "xxxxyyyyabklmopq"
longest(a, b) -> "abcdefklmopqwxy"

a = "abcdefghijklmnopqrstuvwxyz"
longest(a, a) -> "abcdefghijklmnopqrstuvwxyz"
```

### My solution

```javascript
function longest(s1, s2) {
  let s = s1 + s2;

  let set = new Set(s.split(""))

  return Array.from(set).sort().join("")
}
```

### Best solution

```javascript
const longest = (s1, s2) => [...new Set(s1+s2)].sort().join('')
```

```javascript
function longest(s1, s2) {
  return Array.from(new Set(s1 + s2)).sort().join('');
}
```

## \#18

\[CodeWars - Persistent Bugger\]

### Description

Write a function, persistence, that takes in a positive parameter num and returns its multiplicative persistence, which is the number of times you must multiply the digits in num until you reach a single digit.

For example:

```javascript
 persistence(39) === 3 // because 3*9 = 27, 2*7 = 14, 1*4=4
                       // and 4 has only one digit

 persistence(999) === 4 // because 9*9*9 = 729, 7*2*9 = 126,
                        // 1*2*6 = 12, and finally 1*2 = 2

 persistence(4) === 0 // because 4 is already a one-digit number
```

### My solution

```javascript
function persistence(num) {
   let resault = num.toString();
   let count = 0;

   while(resault.length > 1){
     let temp = resault.split("")
     resault = (temp.reduce((a,b)=> a * b)).toString()

     count ++
   }

   return count;
}
```

### Best solution

```javascript
const persistence = num => {
  return `${num}`.length > 1 
    ? 1 + persistence(`${num}`.split('').reduce((a, b) => a * +b)) 
    : 0;
}
```


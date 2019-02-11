# Chalange #1 (code wars)

## Count the number of Duplicates

Write a function that will return the count of distinct case-insensitive alphabetic characters and numeric digits that occur more than once in the input string. The input string can be assumed to contain only alphabets (both uppercase and lowercase) and numeric digits.

### Example
```sh
"abcde" -> 0 # no characters repeats more than once
"aabbcde" -> 2 # 'a' and 'b'
"aabBcde" -> 2 # 'a' occurs twice and 'b' twice (bandB)
"indivisibility" -> 1 # 'i' occurs six times
"Indivisibilities" -> 2 # 'i' occurs seven times and 's' occurs twice
"aA11" -> 2 # 'a' and '1'
"ABBA" -> 2 # 'A' and 'B' each occur twice
```

## My solution
```js
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


# Challange #2 (code wars)

## Double Char

Given a string, you have to return a string in which each character (case-sensitive) is repeated once.

### Example
```
doubleChar("String") ==> "SSttrriinngg"
doubleChar("Hello World") ==> "HHeelllloo  WWoorrlldd"
doubleChar("1234!_ ") ==> "11223344!!__  "
```

### My solution
```js
function doubleChar(str) {
  
  //splits the string in to array, modifies each element 
  //by adding same element twice, joins everithing in to the string
  let copyStr = str.split('').
                map((e) => `${e}${e}`).
                join('');
  
  return copyStr;
}
```

# Challange #3 (Code wars)

## Growing plant

Task
Each day a plant is growing by upSpeed meters. Each night that plant's height decreases by downSpeed meters due to the lack of sun heat. Initially, plant is 0 meters tall. We plant the seed at the beginning of a day. We want to know when the height of the plant will reach a certain level.

Example
For upSpeed = 100, downSpeed = 10 and desiredHeight = 910, the output should be 10.
```sh
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

Because the plant reach to the desired height at day 1(10 meters).

```sh
 After day 1 --> 10
 ```

### My solution

```js
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
# Challange #4

## Shoolace algorithm
Figure out whitch way line is drawn in 2D space (clockwise or counter-clockwise).

### Example

(5,10) (15,20) (20,7) is drawn clockwise
(5,10) (20,7) (15,20) is drawn counter-clockwise
(4,3) (3,3) (3,5) (6,5) (6,3) (5,3) (5,2) (7,2) (7,6) (2,6) (2,2) (4,2) is drawn counter-clockwise

### My solution

Algorithm is used to calculate area of 2d shape. But in this case it is used to determine if 2d shape is drawn clockwise or counterclockwise.

This algorithm do not work on shapes with line crossings

```js

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

# Chalange #5

## Hide phone numbers

You work in an office and your boss has asked you to download from the database the full list of subscribers of your newsletter. You need to hide subscribers' phone numbers and check their prefixes in order to send the encrypted file to a client.

Your tasks are:
*to hide the last six digits of each phone number
*to check validity of prefixes

### Examples

If prefixes are different from the three indicated above `(+39, 0039, 1)` return `false`.

The valid formats for the Italian and US (the last one) numbers are the following:

*CASE 1: `+39 <separator> ### <separator> ### <separator> ####`

*CASE 2: `0039 <separator> ### <separator> ### <separator> ####`

*CASE 3: `1 <separator> ### <separator> ### <separator> ####`

The list of separators is the following:

for Italian numbers: `" ", ".", ""`
for US numbers: `" ", ".", "", "-"`

### My solution
```js
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
### Some more solutions

```js
function encryptNum(number) {
  return /^((\+|00)39([ .]?\d{3}){3}|1([ .-]?\d{3}){3})\d$/.test(number)
  ? number.replace(/(\d\D?){6}$/, x => x.replace(/\d/g, 'X'))
  : false; 
}
```
# Chalange #6

## Find Unique number

There is an array with some numbers. All numbers are equal except for one. Try to find it!
```sh
findUniq([ 1, 1, 1, 2, 1, 1 ]) === 2
findUniq([ 0, 0, 0.55, 0, 0 ]) === 0.55
```
It’s guaranteed that array contains more than 3 numbers.

The tests contain some very huge arrays, so think about performance.

### My solution

```js
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

# Challange #6

## Sort array by string length

Write a function that takes an array of strings as an argument and returns a sorted array containing the same strings, ordered from shortest to longest.

For example, if this array were passed as an argument:

`["Telescopes", "Glasses", "Eyes", "Monocles"]`

Your function would return the following array:

`["Eyes", "Glasses", "Monocles", "Telescopes"]`

All of the strings in the array passed to your function will be different lengths, so you will not have to decide how to order multiple strings of the same length.

### My solution

```js
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

# Chalange #7

```js

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

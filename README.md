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

Izdomāt un aprakstīt algoritmu sekojošas problēmas atrisināšanai:
Ir dota punktu virkne, kas apraksta kā tiek uzzīmēta figūra plaknē, jānoskaidro vai figūra tiek zīmēta
pulksteņa rādītāja virzienā vai pret to.
Piemēram: (5,10) (15,20) (20,7) ir pulksteņa rādītāja virzienā, bet (5,10) (20,7) (15,20) ir pretēji pulksteņa
rādītāja virzienam. Piemēram: (4,3) (3,3) (3,5) (6,5) (6,3) (5,3) (5,2) (7,2) (7,6) (2,6) (2,2) (4,2) ir pretēji
pulksteņa rādītāja virzienam.

Figure out whitch way line is drawn in 2D space (clockwise or counter-clockwise).

### Example

(5,10) (15,20) (20,7) is drawn clockwise
(5,10) (20,7) (15,20) is drawn counter-clockwise
(4,3) (3,3) (3,5) (6,5) (6,3) (5,3) (5,2) (7,2) (7,6) (2,6) (2,2) (4,2) is drawn counter-clockwise

### My solution

```js



```

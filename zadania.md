# Zadania algorytmy

Write a function called `findMissingNumber` that takes in an array of unique numbers from 1 to n (inclusive), where one number is missing. It should return the missing number.

```jsx
findMissingNumber([1, 2, 3, 4, 6, 7, 8, 9, 10]); // 5
findMissingNumber([10, 8, 6, 7, 5, 4, 2, 3, 1]); // 9
findMissingNumber([10, 5, 1, 2, 4, 6, 8, 3, 9]); // 7
```

- Solution
    
    ```jsx
    function findMissingNumber(arr) {
      // If the array is empty or undefined, return undefined
      if (!arr || arr.length === 0) {
        return undefined;
      }
      // Add 1 to the length of the array to account for the missing number
      const n = arr.length + 1;
      // Calculate the expected sum of the numbers from 1 to n
      const expectedSum = (n * (n + 1)) / 2;
      // Calculate the actual sum of the numbers in the array
      const actualSum = arr.reduce((sum, num) => sum + num, 0);
      // Return the difference between the expected sum and the actual sum
      return expectedSum - actualSum;
    }
    ```
    

---

You are given an array of car objects, each containing information about a car's make, model, year, and mileage. Your goal is to perform some analysis on the car mileage data using high order array methods.

Implement a function called `analyzeCarMileage` which takes in an array of car objects and performs the following tasks:

1. Calculate the average mileage of all cars.
2. Find the car with the highest mileage.
3. Find the car with the lowest mileage.
4. Calculate the total mileage of all cars combined.

```jsx
const cars = [
  { make: 'Toyota', model: 'Corolla', year: 2020, mileage: 25000 },
  { make: 'Honda', model: 'Civic', year: 2019, mileage: 30000 },
  { make: 'Ford', model: 'Mustang', year: 2021, mileage: 15000 },
];

const analysis = analyzeCarMileage(cars);
console.log(analysis);
// Output:
// {
//   averageMileage: 23333.33,
//   highestMileageCar: { make: "Honda", model: "Civic", year: 2019, mileage: 30000 },
//   lowestMileageCar: { make: "Ford", model: "Mustang", year: 2021, mileage: 15000 },
//   totalMileage: 70000
// }
```

- Solution
    
    ```jsx
    function analyzeCarMileage(cars) {
      const totalMileage = cars.reduce((acc, cur) => acc + cur.mileage, 0);
      const averageMileage = parseFloat((totalMileage / cars.length).toFixed(2));
      const lowestMileageCar = cars.reduce(
        (lowest, car) => (car.mileage < lowest.mileage ? car : lowest),
        cars[0]
      );
      const highestMileageCar = cars.reduce(
        (highest, car) => (car.mileage > highest.mileage ? car : highest),
        cars[0]
      );
      return { averageMileage, highestMileageCar, lowestMileageCar, totalMileage };
    }
    
    ```
    

---

Your task in order to complete this Kata is to write a function which formats a duration, given as a number of seconds, in a human-friendly way.

The function must accept a non-negative integer. If it is zero, it just returns `"now"`. Otherwise, the duration is expressed as a combination of `years`, `days`, `hours`, `minutes` and `seconds`.

```jsx
* For seconds = 62, your function should return 
    "1 minute and 2 seconds"
* For seconds = 3662, your function should return
    "1 hour, 1 minute and 2 seconds"
```

- Solution (best practice)
    
    ```jsx
    function formatDuration (seconds) {
      var time = { year: 31536000, day: 86400, hour: 3600, minute: 60, second: 1 },
          res = [];
    
      if (seconds === 0) return 'now';
      
      for (var key in time) {
        if (seconds >= time[key]) {
          var val = Math.floor(seconds/time[key]);
          res.push(val += val > 1 ? ' ' + key + 's' : ' ' + key);
          seconds = seconds % time[key];
        }
      }
     
      return res.length > 1 ? res.join(', ').replace(/,([^,]*)$/,' and'+'$1') : res[0]
    }
    ```
    

---

Write a function called `reverseString` that takes in a string and returns the reversed version of the string. Be sure to use recursion in your solution.

```jsx
reverseString('hello'); // should return 'olleh'
reverseString('world'); // should return 'dlrow'
reverseString(''); // should return ''
reverseString('a'); // should return 'a'
reverseString('racecar'); // should return 'racecar'
```

- Solution
    
    ```jsx
    function reverseString(str) {
      if (str === "") {
        return "";
      }
      const lastLetter = str.slice(-1);
      const rest = str.slice(0, -1);
      return lastLetter + reverseString(rest);
    }
    ```
    

---

Write a function called `fibonacci` that takes in a number and returns the number at that index of the Fibonacci sequence.

```jsx
fibonacci(4); // 3
fibonacci(6); // 8
fibonacci(10); // 55
```

- Solution
    
    ```jsx
    function fibonacci(num) {
      // Base case
      if (num < 2) return num;
    
      // Recursive case
      return fibonacci(num - 1) + fibonacci(num - 2);
    }
    ```
    

---

Write a function called `flattenArray` that takes in an array containing nested arrays of integers and returns a new array with all the integers from the nested arrays flattened into a single level.

```jsx
flattenArray([1, [2, 3], [4, 5, [6]]]); // should return [1, 2, 3, 4, 5, 6]
flattenArray([
  [1, 2],
  [3, [4, 5]],
  [6, [7]],
]); // should return [1, 2, 3, 4, 5, 6, 7]
flattenArray([1, [2, [3, [4, [5]]]]]); // should return [1, 2, 3, 4, 5]
```

- Solution
    
    ```jsx
    function flattenArray(arr) {
      let result = [];
    
      for (const item of arr) {
        if (Array.isArray(item)) {
          result = result.concat(flattenArray(item));
        } else {
          result.push(item);
        }
      }
    
      return result;
    }
    ```
    

---

Write a function called permutations that takes in a string as a parameter and returns an array of all possible permutations of the characters in the string.

```jsx
permutations('abc'); // ['abc', 'acb', 'bac', 'bca', 'cab', 'cba']
permutations('dog'); // ['dog', 'dgo', 'odg', 'ogd', 'gdo', 'god']
```

- Solution
    
    ```jsx
    function permutations(str) {
      const result = [];
    
      if (str.length === 0) {
        result.push("");
        return result;
      }
    
      for (let i = 0; i < str.length; i++) {
        const firstChar = str[i];
        const restOfString = str.slice(0, i) + str.slice(i + 1);
        const subPermutations = permutations(restOfString);
    
        for (let j = 0; j < subPermutations.length; j++) {
          result.push(firstChar + subPermutations[j]);
        }
      }
    
      return result;
    }
    ```
    


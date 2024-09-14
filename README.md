# JavaScript Algorithms and Data Structures
This repository is a curated collection of my journey through learning and mastering various algorithms and data structures using JavaScript. It serves as both a personal reference and a resource for others who are keen to enhance their understanding of these foundational concepts in computer science.

## Table of Contents
- [Frequency Counter](#frequency-counter)
- [Multiple Pointers](#multiple-pointers)
- [Sliding Window](#sliding-window)
  


___

## Frequency Counter

A frequency counter is a concept used to count how often each item appears in a collection, like an array. It helps us quickly determine the frequency of each element.

### Example of a Frequency Counter

Let's say we have an array of numbers: [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]. We want to count how many times each number appears in this array.

Here's a simple way to do that using JavaScript:

```javascript
function frequencyCounter(array) {
    const frequency = {};  // Create an empty object to store frequencies

    // Loop through each item in the array
    for (const item of array) {
        // If the item is already in the frequency object, increase its count
        if (frequency[item]) {
            frequency[item]++;
        } else {
            // Otherwise, set its count to 1
            frequency[item] = 1;
        }
    }

    return frequency;  // Return the frequency object
}

const numbers = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4];
const result = frequencyCounter(numbers);

console.log(result);  // Output: { '1': 1, '2': 2, '3': 3, '4': 4 }
```
### Explanation:

- **Initialize an Object**: We create an empty object frequency to store the counts.
- **Loop Through Array**: For each item in the array, we check if it is already in the frequency object.
- **Update Counts**: If the item is in the object, we increase its count. If it’s not, we add it to the object with a count of 1.
- **Return the Result**: Finally, we return the object containing the frequency of each item.

This ```frequencyCounter``` function can handle any array of items, not just numbers. For example, it could count occurrences of words in an array of strings.

___

## Multiple Pointers


The "Multiple Pointers" technique is a useful strategy for solving problems that involve arrays or lists. It generally involves using two or more pointers (or indices) to traverse the data structure, which helps to solve problems efficiently, often with a time complexity of O(n).

### How It Works

You start with two pointers (or more) at different positions in the array or list and move them according to certain rules. This technique is commonly used in problems like finding pairs that sum up to a specific value, or checking if a sequence meets certain criteria.

**Example: Finding a Pair with a Given Sum**
Let's use the multiple pointers technique to solve the problem of finding two numbers in a sorted array that sum up to a given target.

Problem: Given a sorted array ```arr``` and a target sum ```target```, find if there are two numbers in ```arr``` that add up to ```target```.

```javascript
function findPairWithSum(arr, target) {
    let left = 0;                // Pointer at the start
    let right = arr.length - 1;  // Pointer at the end

    while (left < right) {
        const sum = arr[left] + arr[right];
        
        if (sum === target) {
            return [arr[left], arr[right]];  // Found the pair
        } else if (sum < target) {
            left++;  // Move left pointer to the right to increase the sum
        } else {
            right--; // Move right pointer to the left to decrease the sum
        }
    }

    return null; // No pair found
}

const numbers = [1, 2, 3, 4, 5, 6, 7];
const target = 10;
const result = findPairWithSum(numbers, target);

console.log(result);  // Output: [3, 7]
```

### Explanation

- **Initialize Pointers**: We start with left at the beginning of the array and right at the end.
- **Calculate Sum**: Compute the sum of the elements at these pointers.
- **Check Sum**:
  - If the sum equals the target, we've found the pair.
  - If the sum is less than the target, move the left pointer to the right to increase the sum.
  - If the sum is greater than the target, move the right pointer to the left to decrease the sum.
- **Repeat Until Pointers Meet**: Continue this process until the left pointer is no longer less than the right pointer.
- **Return Result**: If we find a pair that meets the criteria, return it; otherwise, return null if no such pair exists.

 ___

## Sliding Window

The **Sliding Window** technique is a powerful approach for solving problems that involve arrays or strings, particularly when you need to find subarrays or substrings with specific properties. It involves creating a window (a range of elements) that moves across the data structure to maintain or calculate certain properties.

### How It Works

- **Initialize Window**: Start with a window that covers a certain range of elements.
- **Expand or Contract the Window**: Adjust the window size or position as needed based on the problem requirements.
- **Update and Check**: Calculate or check the desired properties as the window slides.

### Example: Maximum Sum of a Subarray of Fixed Size

Let’s use the sliding window technique to find the maximum sum of a subarray of a given size ```k``` in a list of integers.

Problem: Given an array ```arr``` and an integer ```k```, find the maximum sum of any contiguous subarray of size ```k```.

```javascript
function maxSumSubarray(arr, k) {
    let maxSum = 0;    // Variable to store the maximum sum
    let windowSum = 0; // Variable to store the current window sum

    // Calculate the sum of the first window
    for (let i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    maxSum = windowSum; // Initialize maxSum with the sum of the first window

    // Slide the window across the array
    for (let i = k; i < arr.length; i++) {
        // Add the next element and subtract the element that's sliding out
        windowSum += arr[i] - arr[i - k];
        maxSum = Math.max(maxSum, windowSum); // Update maxSum if needed
    }

    return maxSum;
}

const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const k = 3;
const result = maxSumSubarray(numbers, k);

console.log(result);  // Output: 24 (which is the sum of [7, 8, 9])
```

### Explanation
- **Initial Window Sum**: Calculate the sum of the first k elements. This sum will serve as the initial window sum.
- **Slide the Window**: Move the window one element to the right:
  - Add the new element that is entering the window.
  - Subtract the element that is leaving the window.
- **Update Maximum Sum**: Compare the current window sum to the maximum sum found so far and update if the current sum is larger.
- **Return Result**: After sliding through the entire array, return the maximum sum found.

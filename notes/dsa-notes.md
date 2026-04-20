*Thinking Pattern* :

- brute force first -> obvious way to solve
- check input size -> what is the n, (n=5, n=10000), n decides brute force acceptance or not
- improve with DS/pattern" -> Can i use a better data structure to reduce time

- Questions for Intuition :
  1. Can I scan once?
     - If yes → linear scan / hashmap / set

  2. Is it sorted?
     - If yes → binary search / two pointers

  3. Need pairs / subarray?
     - Think sliding window / two pointers

  4. Need shortest path / levels?
     - BFS

  5. Need full traversal?
     - DFS / recursion



1. **BASICS** 
  - Data Structures - How Data is Stored. 
  - Algorithms - How Data is processed.
  - *Time Complexity* : How the time grows as input size grows
      - Common Time Complexities :
        - O(1) -> Constant => (direct access, Hashmap lookup)
        - O(n) -> Linear => ( one full loop)
        - O(log n) -> binary search => (divide search space in half)
        - O(n log n) -> efficient sorting
        - O(n square) -> nested loops
      E.g Quick Intuition : Array of 1,000,000
        * O(1) ->  1 step
        * O(log n) -> ~20 steps
        * O(n) -> 1,000,000 steps
        * O(n square)v -> disaster

  - *Space Complexity* : Extra memory used by the solution
      - Examples:
        - using few variables -> O(1)
        - extra array/hashmap -> O(n)
        - recursion stack -> often O(n)

2. **PATTERNS**
   1. Linear Scan
      ```js
        let max = arr[0];
        for (let num of arr) {
            if (num > max) max = num;
        }
        // complexity : O(n), O(1)
      ```
   2. HashMap / Set Basics 
      - use Set → existence / uniqueness
        ```js
            const set = new Set();
            for (let num of arr) {
                if (set.has(num)) return true;
                set.add(num);
            }
            // complexity : O(n), O(n)
        ```
      - use Map → frequency / counts / positions
        ```js
            const map = new Map();
            for (let ch of str) {
                map.set(ch, (map.get(ch) || 0) + 1);
            }
            //  complexity : O(n), O(n) 
            // intution = without map its mostly nested check "O(n square)"
        ```
   3. Two Pointers
       - Use two indices instead of one to reduce complexity (left and right)
       - when to use: sorted array, pairs/triplets, opposite ends processing
       - You’re shrinking search space intelligently, not checking all pairs.
       - ```js
            let left = 0;
            let right = arr.length - 1;

            while (left < right) {
            const sum = arr[left] + arr[right];

            if (sum === target) return true;
            else if (sum < target) left++;
            else right--;
            }
            // comp : Time → O(n) Space → O(1)
         ```
   4. Sliding Window
      - Maintain a window (subarray / substring) and move it
          - expand window (right++)
          - shrink window (left++)
            - questions :
                - e.g fixed window max sum of size k
                - e.g Variable window grows and shrinks based on condition : longest substring without repeating characters
      - When to use :
          -  Subarray / substring, 
          -  “longest”, “smallest”, “count of…”
          -  contiguous elements
      - *Real world usecases* :
          - last 100 messages, last 5 mins users 
          - no repeating messages, no repeating chars, sum ≥ target
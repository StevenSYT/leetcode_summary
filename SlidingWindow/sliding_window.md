# Sliding Window

- [Grumpy Bookstore Owner](#grumpy-bookstore-owner)
- [Shortest Subarray to be Removed to Make Array Sorted](#shortest-subarray-to-be-removed-to-make-array-sorted)
- [Replace the Substring for Balanced String](#replace-the-substring-for-balanced-string)

## Grumpy Bookstore Owner

[1052. Grumpy Bookstore Owner](https://leetcode.com/problems/grumpy-bookstore-owner/)

```python
class Solution:
    def maxSatisfied(self, customers: List[int], grumpy: List[int], X: int) -> int:
        satisfied = 0
        for i in range(len(customers)):
            if grumpy[i] == 0:
                satisfied += customers[i]
                customers[i] = 0
        
        max_satisfied = cur_satisifed = satisfied

        for r in range(len(grumpy)):
            cur_satisifed += customers[r]

            if r >= X:
                cur_satisifed -= customers[r - X]
            
            max_satisfied = max(max_satisfied, cur_satisifed)
        
        return max_satisfied
```

## Shortest Subarray to be Removed to Make Array Sorted

[1574. Shortest Subarray to be Removed to Make Array Sorted](https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/)

```python
class Solution:
    def findLengthOfShortestSubarray(self, arr: List[int]) -> int:
        n = len(arr)

        l, r = 0, n - 1

        while l < r and arr[l] <= arr[l + 1]:
            l += 1

        if l == n - 1:
            return 0

        while r > l and arr[r - 1] <= arr[r]:
            r -= 1

        res = min(n - l - 1, r)  # either remove [l, n - 1] or [0, r - 1]

        for left in range(l + 1):
            if arr[left] <= arr[r]:
                res = min(res, r - left - 1)

            elif r < n - 1:
                r += 1

            else:
                break
        return res
```

## Replace the Substring for Balanced String

[1234. Replace the Substring for Balanced String](https://leetcode.com/problems/replace-the-substring-for-balanced-string/)

```python
from collections import Counter


class Solution:
    def balancedString(self, s: str) -> int:
        counter = Counter(s)
        n, k = len(s), len(s) // 4
        res = n
        l = 0

        for r in range(n):
            counter[s[r]] -= 1

            while l < n and all([counter[c] <= k for c in 'QWER']):
                if l > r:
                    return 0

                res = min(res, r - l + 1)
                counter[s[l]] += 1
                l += 1

        return res
```
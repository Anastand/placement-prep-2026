# Two Pointers / Hash Map

## Problem: Two Sum
**Link**: https://leetcode.com/problems/two-sum/  
**Difficulty**: Easy  
**Category**: Arrays, Hash Map

---

## Problem Statement
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to target.
- Each input has exactly one solution
- Cannot use the same element twice
- Return answer in any order

---

## Examples

| Input | Output | Explanation |
|-------|--------|-------------|
| nums = [2,7,11,15], target = 9 | [0,1] | nums[0] + nums[1] = 2 + 7 = 9 |
| nums = [3,2,4], target = 6 | [1,2] | nums[1] + nums[2] = 2 + 4 = 6 |
| nums = [3,3], target = 6 | [0,1] | nums[0] + nums[1] = 3 + 3 = 6 |

**Constraints**: 2 <= len(nums) <= 10⁴, -10⁹ <= nums[i] <= 10⁹

---

## Solutions

### Solution 1: Brute Force
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for k in range(i+1, len(nums)):
                if nums[i] + nums[k] == target:
                    return [i, k]
        return []
```

**How it works**: Check every possible pair (i, k) where k > i. Return when sum equals target.

| Aspect | Value |
|--------|-------|
| Time | O(n²) - nested loops |
| Space | O(1) - no extra data structures |

**Why this works**: Exhaustively checks all pairs until a valid one is found.

**Edge cases handled**: Returns empty list if no pair found (though problem guarantees one exists).

---

### Solution 2: Hash Map (Optimal)
```python
from typing import List

class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen = {}  # value -> index mapping
        for i, val in enumerate(nums):
            complement = target - val  # what we need to find
            if complement in seen:     # check if complement exists
                return [seen[complement], i]
            seen[val] = i              # store current value
```

**How it works**: For each element, calculate its complement (target - current). If complement is already in the hash map, we found both numbers.

| Aspect | Value |
|--------|-------|
| Time | O(n) - single pass |
| Space | O(n) - hash map stores at most n elements |

**Why this works**: Trading space for time. Instead of searching for complement, we store seen values for O(1) lookup. At index i, we only need to check if complement appeared before i.

**Edge cases**: 
- Duplicate values (e.g., [3,3], target=6): First 3 stores at index 0, second 3 finds complement=3 in map
- Works with negatives: complement calculation handles negative numbers

---

## Key Insights

| Concept | Explanation |
|---------|------------|
| **Hash Map lookup** | O(1) average, enables O(n) solution |
| **One-pass** | We only look back (k > i) because we store while iterating |
| **Complement logic** | Instead of asking "what pairs sum to target?", ask "do I have X where target - current exists?" |
| **Space-time trade-off** | Using dict trades O(n) space for O(n) time instead of O(n²) |

---

## Improvements & Notes

### From Solution 1 → Solution 2:
- **Time complexity**: O(n²) → O(n) (massive improvement)
- **Algorithm**: Nested loops → single-pass hash map
- **Variable clarity**: Changed `i,k` to `i,val`, added `complement` for clarity
- **Added**: from typing import List for type hints

### What I Learned:
- Hash maps solve "find pair with property" efficiently
- Single-pass is possible by storing seen values
- Always consider complement (target - current) instead of searching forward

---

## Test Cases

```python
# Case 1: Basic
assert twoSum([2,7,11,15], 9) in [[0,1], [1,0]]

# Case 2: Middle elements
assert twoSum([3,2,4], 6) in [[1,2], [2,1]]

# Case 3: Duplicates
assert twoSum([3,3], 6) == [0,1]

# Case 4: Negative numbers
assert twoSum([-1,-2,-3,-4,-5], -8) in [[2,4], [4,2]]

# Case 5: Smallest input
assert twoSum([1,2], 3) == [0,1]
```

---

## Follow-up Questions

1. Can you solve it with O(1) space? → No, requires sorting which changes indices (trade-off)
2. What if we needed values instead of indices? → Could use two pointers on sorted array
3. Can we do better than O(n)? → No, must examine each element at least once

---

## Revision Checklist

- [ ] Explain why hash map gives O(n) instead of O(n²)
- [ ] Trace through [3,3] with target=6 step by step
- [ ] Draw the hash map state at each iteration for [2,7,11,15], target=9
- [ ] What if we used a list instead of dict? → O(n) lookup becomes O(n) search

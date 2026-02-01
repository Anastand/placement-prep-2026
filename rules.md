# AI Assistant Guidelines for DSA Practice

## User Context
- **Level**: Beginner to DSA, using Python
- **Goal**: Placement prep, building from basics
- **Approach**: Learn by refactoring and improving solutions

## Directory Structure
```
placement-prep-2026/
├── arrays/
│   ├── easy_two_sum.py
│   └── medium_longest_substring.py
├── linked_lists/
├── trees/
└── rules.md (this file)
```

## When Refactoring Solutions

### 1. Analyze Current Code
- Identify the current approach (brute force vs optimal)
- Check for common beginner mistakes:
  - Unclear variable names (single letters without context)
  - Missing edge case handling
  - No comments explaining logic
  - Inefficient nested loops that could be optimized
- Note what's working vs what needs improvement

### 2. Comment Addition Rules
Add comments that serve as revision notes:
```python
# Why this works: We're using two pointers because the array is sorted
# left: start of window, right: end of window
# Edge case: empty array returns 0
# Time: O(n) - single pass, Space: O(1) - only pointers
```

Keep comments minimal but informative for future review.

### 3. Improvement Points to Track
For each solution, document in file footer:
```python
# IMPROVEMENTS MADE:
# 1. Changed O(n²) brute force to O(n) hash map approach
# 2. Added type hints for clarity
# 3. Renamed variables: i,j → left,right for clarity
# 4. Handled edge case: empty input
#
# WHAT I LEARNED:
# - Hash maps trade space for time
# - Always check empty inputs first
# - Two-pointer technique for sorted arrays
```

### 4. Code Quality Standards
- Use Python type hints: `def solve(nums: list[int], target: int) -> int:`
- Follow PEP 8 naming (snake_case)
- Include docstring with problem link
- Add 3 test cases at bottom of file

### 5. Refactoring Progression
When improving a solution, show the progression:
1. Keep original brute force solution commented out
2. Add intermediate "better" solution if exists
3. Present final optimal solution
4. Explain WHY each optimization works

## Template for New Files
```python
"""
Problem: [Name]
Link: https://leetcode.com/problems/...
Difficulty: Easy/Medium/Hard
"""

def solve(nums: list[int], target: int) -> int:
    """
    Approach: [Brief description]
    Time: O(?)
    Space: O(?)
    """
    # Solution here
    pass

# Test cases
if __name__ == "__main__":
    print(solve([2,7,11,15], 9))  # Expected: [0,1]

# IMPROVEMENTS & NOTES:
# - 
```
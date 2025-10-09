# 8th-week-plan-and-code

------------------------------------------------------
Week 8: Backtracking
------------------------------------------------------
Day 50: Subsets, combinations (LC #78, #77)
Day 51: Permutations (LC #46)
Day 52: Combination sum (LC #39, #40)
Day 53: N-Queens problem
Day 54: Word search (LC #79)
Day 55: Review backtracking patterns
Day 56: Practice 4-5 backtracking problems
------------------------------------------------------
Week 9: Advanced Trees, Heaps, Tries
------------------------------------------------------

"""
Day 50: Subsets and Combinations (LeetCode #78, #77)
Author: [Your Name]
Date: [Today's Date]

Problems Covered:
1. LC #78 – Subsets
2. LC #77 – Combinations
"""

# ----------------------------------------------------
# 1️⃣ LC #78 – Subsets
# ----------------------------------------------------
"""
Problem:
Given an integer array nums of unique elements, return all possible subsets (the power set).

Approach:
- Use backtracking to explore two choices for each element:
    1. Include the element
    2. Exclude the element
- Base case: When index == len(nums), add current subset to result.

Time Complexity: O(2^n)
Space Complexity: O(n) (recursion stack)
"""

def subsets(nums):
    res = []
    subset = []

    def backtrack(index):
        # Base case: reached end
        if index == len(nums):
            res.append(subset.copy())
            return
        
        # Include nums[index]
        subset.append(nums[index])
        backtrack(index + 1)

        # Exclude nums[index]
        subset.pop()
        backtrack(index + 1)
    
    backtrack(0)
    return res


# ----------------------------------------------------
# 2️⃣ LC #77 – Combinations
# ----------------------------------------------------
"""
Problem:
Given two integers n and k, return all possible combinations of k numbers out of 1 … n.

Approach:
- Backtrack from 1 to n, building combinations of length k.
- Each step: choose current number or skip it.
- Stop when current combination length == k.

Time Complexity: O(C(n, k))  (number of combinations)
Space Complexity: O(k)
"""

def combine(n, k):
    res = []
    comb = []

    def backtrack(start):
        if len(comb) == k:
            res.append(comb.copy())
            return
        
        for num in range(start, n + 1):
            comb.append(num)
            backtrack(num + 1)
            comb.pop()

    backtrack(1)
    return res


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    print("🔹 Subsets of [1, 2, 3]:", subsets([1, 2, 3]))
    print("🔹 Combinations (n=4, k=2):", combine(4, 2))


# ----------------------------------------------------
# Key Notes:
# ----------------------------------------------------
# - Both problems use the BACKTRACKING pattern.
# - Subsets → choose/exclude each element.
# - Combinations → controlled recursion with start index.
# - Foundation for advanced problems:
#     * Permutations (LC #46)
#     * Combination Sum (LC #39)
#     * Subset Sum variations
# ----------------------------------------------------

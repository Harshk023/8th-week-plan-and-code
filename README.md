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


"""
Day 51: Permutations (LeetCode #46)
Author: [Your Name]
Date: [Today's Date]

Problem Statement:
Given an array nums of distinct integers, return all possible permutations.
You can return the answer in any order.

Example:
Input: nums = [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
"""

# ----------------------------------------------------
# Approach: Backtracking
# ----------------------------------------------------
"""
Idea:
- Use backtracking to build permutations one number at a time.
- Keep track of which elements are already used.
- When the current permutation reaches length n, add it to results.

Steps:
1. Use a `path` list to store the current permutation.
2. For each unused number, add it → recurse → remove it (backtrack).
3. Continue until all elements are used.

Time Complexity: O(n * n!)
Space Complexity: O(n) recursion depth
"""

def permute(nums):
    res = []
    used = [False] * len(nums)

    def backtrack(path):
        # Base case: one full permutation built
        if len(path) == len(nums):
            res.append(path.copy())
            return
        
        # Try each unused number
        for i in range(len(nums)):
            if not used[i]:
                used[i] = True
                path.append(nums[i])

                backtrack(path)

                # Backtrack (undo the choice)
                path.pop()
                used[i] = False
    
    backtrack([])
    return res


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    nums = [1, 2, 3]
    print("All permutations of", nums, "are:")
    for p in permute(nums):
        print(p)


# ----------------------------------------------------
# Key Notes:
# ----------------------------------------------------
# - This is a classic BACKTRACKING problem.
# - Builds on the same recursion logic as subsets/combinations.
# - Key idea: choose an element → explore → un-choose (backtrack).
# - Related problems:
#     * LC #47 – Permutations II (with duplicates)
#     * LC #784 – Letter Case Permutation
# ----------------------------------------------------

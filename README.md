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



"""
Day 52: Combination Sum (LeetCode #39, #40)
Author: [Your Name]
Date: [Today's Date]

Problems Covered:
1️⃣ LC #39 – Combination Sum
2️⃣ LC #40 – Combination Sum II
"""

# ----------------------------------------------------
# 1️⃣ LC #39 – Combination Sum
# ----------------------------------------------------
"""
Problem:
Given an array of distinct integers 'candidates' and a target integer 'target',
return all unique combinations where the chosen numbers sum to 'target'.
You may reuse the same number multiple times.

Example:
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]

Approach:
- Use backtracking to explore all possible combinations.
- At each step, either pick the current number (reuse allowed) or move to the next one.
- Stop when the running sum exceeds target.

Time Complexity: O(2^n)
Space Complexity: O(n)
"""

def combinationSum(candidates, target):
    res = []
    path = []

    def backtrack(start, total):
        # Base cases
        if total == target:
            res.append(path.copy())
            return
        if total > target:
            return
        
        # Explore all choices
        for i in range(start, len(candidates)):
            path.append(candidates[i])
            backtrack(i, total + candidates[i])  # reuse allowed
            path.pop()
    
    backtrack(0, 0)
    return res


# ----------------------------------------------------
# 2️⃣ LC #40 – Combination Sum II
# ----------------------------------------------------
"""
Problem:
Given a collection of candidate numbers (candidates) and a target number (target),
find all unique combinations where each number can be used at most once.
The solution set must not contain duplicate combinations.

Example:
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: [[1,1,6],[1,2,5],[1,7],[2,6]]

Approach:
- Sort the list to handle duplicates easily.
- At each recursion level, skip duplicate numbers.
- Use `i + 1` to ensure each number is used only once.

Time Complexity: O(2^n)
Space Complexity: O(n)
"""

def combinationSum2(candidates, target):
    res = []
    path = []
    candidates.sort()

    def backtrack(start, total):
        if total == target:
            res.append(path.copy())
            return
        if total > target:
            return

        prev = -1
        for i in range(start, len(candidates)):
            # Skip duplicates at the same level
            if candidates[i] == prev:
                continue
            path.append(candidates[i])
            backtrack(i + 1, total + candidates[i])
            path.pop()
            prev = candidates[i]
    
    backtrack(0, 0)
    return res


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    print("🔹 LC #39 – Combination Sum:")
    print(combinationSum([2, 3, 6, 7], 7))  # [[2,2,3],[7]]

    print("\n🔹 LC #40 – Combination Sum II:")
    print(combinationSum2([10,1,2,7,6,1,5], 8))  # [[1,1,6],[1,2,5],[1,7],[2,6]]


# ----------------------------------------------------
# Key Notes:
# ----------------------------------------------------
# ✅ LC #39 → Reuse allowed (i stays same)
# ✅ LC #40 → Unique combinations (use i+1, skip duplicates)
# 🧩 Mastering these problems builds strong intuition for:
#     - Backtracking tree pruning
#     - Avoiding duplicates
#     - Managing recursion states
# 🚀 Forms foundation for advanced problems like:
#     * Combination Sum III (LC #216)
#     * Subset Sum variants
# ----------------------------------------------------


"""
Day 53: N-Queens Problem (LeetCode #51)
Author: [Your Name]
Date: [Today's Date]

Problem Statement:
The N-Queens puzzle is to place N queens on an N×N chessboard so that no two queens attack each other.
A queen can attack in the same row, column, or diagonal.

Example:
Input: n = 4
Output: 
[
 [".Q..",
  "...Q",
  "Q...",
  "..Q."]
]
"""

# ----------------------------------------------------
# Approach: Backtracking
# ----------------------------------------------------
"""
Intuition:
We place one queen per row and use backtracking to explore all valid placements.

Constraints:
- Only one queen per row.
- No two queens share the same column or diagonal.

How to detect conflicts:
- Keep track of columns, diagonals (r+c), and anti-diagonals (r-c).

Steps:
1️⃣ Start from row 0.
2️⃣ Try placing a queen in each column of the current row.
3️⃣ Skip if the column or diagonal is under attack.
4️⃣ If valid, mark it and move to the next row.
5️⃣ If all rows are filled, store the board configuration.
6️⃣ Backtrack to explore other possibilities.

Time Complexity: O(N!)
Space Complexity: O(N²)
"""

def solveNQueens(n):
    res = []
    board = [["."] * n for _ in range(n)]

    cols = set()         # columns under attack
    posDiag = set()      # (r + c) diagonals under attack
    negDiag = set()      # (r - c) diagonals under attack

    def backtrack(r):
        # Base case: placed all queens
        if r == n:
            # Convert board to list of strings
            copy = ["".join(row) for row in board]
            res.append(copy)
            return

        for c in range(n):
            # Skip if column or diagonal is under attack
            if c in cols or (r + c) in posDiag or (r - c) in negDiag:
                continue

            # Place the queen
            board[r][c] = "Q"
            cols.add(c)
            posDiag.add(r + c)
            negDiag.add(r - c)

            # Recurse for next row
            backtrack(r + 1)

            # Backtrack (remove the queen)
            board[r][c] = "."
            cols.remove(c)
            posDiag.remove(r + c)
            negDiag.remove(r - c)

    backtrack(0)
    return res


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    n = 4
    print(f"🔹 All solutions for {n}-Queens problem:")
    solutions = solveNQueens(n)
    for sol in solutions:
        for row in sol:
            print(row)
        print()


# ----------------------------------------------------
# Key Notes:
# ----------------------------------------------------
# ✅ Backtracking pattern:
#    - Choose
#    - Explore
#    - Un-choose
# ✅ Constraints handled using sets for O(1) conflict checks.
# ✅ Teaches:
#    - Constraint satisfaction problems
#    - Efficient pruning in recursion
# 🚀 Foundation for:
#    - Sudoku Solver
#    - Word Search
#    - N-Rooks / N-Knights variations
# ----------------------------------------------------


"""
Day 54: Word Search (LeetCode #79)
Author: [Your Name]
Date: [Today's Date]

Problem Statement:
Given an m x n grid of characters 'board' and a string 'word',
return True if 'word' exists in the grid.

The word can be constructed from letters of sequentially adjacent cells,
where adjacent cells are horizontally or vertically neighboring.
The same letter cell may not be used more than once.

Example:
Input: board = [
  ["A","B","C","E"],
  ["S","F","C","S"],
  ["A","D","E","E"]
], word = "ABCCED"
Output: True
"""

# ----------------------------------------------------
# Approach: Backtracking (DFS)
# ----------------------------------------------------
"""
Intuition:
- For each cell, check if it can be the start of the given word.
- From each matching cell, explore all 4 directions recursively.
- Mark cells as visited to avoid reuse.
- Backtrack after each recursive call to explore new paths.

Steps:
1️⃣ Traverse every cell in the board.
2️⃣ When board[r][c] == word[0], start DFS from there.
3️⃣ Explore all directions (up, down, left, right).
4️⃣ Return True if full word is matched.

Time Complexity: O(N * M * 4^L)
   where N, M = grid dimensions, L = word length
Space Complexity: O(L) recursion depth
"""

def exist(board, word):
    ROWS, COLS = len(board), len(board[0])

    def backtrack(r, c, i):
        # If we matched all characters
        if i == len(word):
            return True
        # Out of bounds or mismatch
        if r < 0 or c < 0 or r >= ROWS or c >= COLS or board[r][c] != word[i]:
            return False

        # Mark current cell as visited
        temp = board[r][c]
        board[r][c] = "#"

        # Explore all 4 directions
        res = (backtrack(r + 1, c, i + 1) or
               backtrack(r - 1, c, i + 1) or
               backtrack(r, c + 1, i + 1) or
               backtrack(r, c - 1, i + 1))

        # Backtrack (restore cell)
        board[r][c] = temp
        return res

    # Try to start from each cell
    for r in range(ROWS):
        for c in range(COLS):
            if backtrack(r, c, 0):
                return True
    return False


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    board = [
        ["A","B","C","E"],
        ["S","F","C","S"],
        ["A","D","E","E"]
    ]
    word = "ABCCED"
    print(f"🔹 Word '{word}' exists in board:", exist(board, word))  # Expected: True


# ----------------------------------------------------
# Key Notes:
# ----------------------------------------------------
# ✅ Classic backtracking problem on a 2D grid.
# ✅ Each recursive call explores valid directions.
# ✅ Ensures no cell is reused by marking as visited.
# ✅ Strengthens understanding of DFS + Backtracking.
# 🚀 Foundation for:
#     - Sudoku Solver (LC #37)
#     - Word Search II (LC #212)
#     - Island counting problems
# ----------------------------------------------------

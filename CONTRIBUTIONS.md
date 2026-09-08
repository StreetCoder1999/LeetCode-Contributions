# LeetCode Contributions

A collection of my test case contributions and bug reports to LeetCode, helping improve problem quality and catch edge cases that faulty solutions might miss.

---

## 🎯 Contribution: Issue #37912

### Problem: 86. Partition List
**[View on LeetCode](https://leetcode.com/problems/partition-list/description/)**

### 🐛 Bug Found: Missing Edge Case with Negative Sentinel Values

**Status**: Closed ✅  
**Issue Link**: [#37912 - LeetCode-Feedback](https://github.com/LeetCode-Feedback/LeetCode-Feedback/issues/37912)

---

### The Problem

The original test suite was missing a critical edge case where linked list nodes contain negative values, specifically `-1`.

Many faulty solutions were using `-1` as a **sentinel value** (a marker) to track whether the "greater partition" had been initialized. These solutions would incorrectly fail when the actual linked list contained `-1` as a valid node value.

### ✨ My Test Case

```
Input:  head = [-1, 5], x = -2
Output: [-1, 5]
```

**Why this matters:**
- Since `-1 ≥ -2`, the node with value `-1` belongs in the "greater partition"
- Expected output: `[-1, 5]` (unchanged)
- Faulty solutions would fail because they check `if (greaterTemp.val == -1)` to detect initialization
- When the first node is actually `-1`, this condition becomes ambiguous

### 🔍 Root Cause

Faulty solutions used this pattern:
```java
ListNode greaterTemp = new ListNode(-1);  // Using -1 as sentinel

if (greaterTemp.val == -1)  // Check if initialized
    greaterTemp = temp;

if (greaterTemp.val != -1)  // Check if partition exists
    smallerTemp.next = greaterTemp;
```

This breaks when `-1` is a valid node value in the input!

### ✅ Impact

- Caught solutions that weren't properly handling negative node values
- Forced algorithm improvements to use proper initialization tracking (e.g., `null` references instead of magic values)
- Improved test suite quality for LeetCode Problem 86

---

## 💡 Key Takeaway

This contribution shows the importance of:
- Testing **boundary conditions** (negative numbers, edge values)
- Avoiding **magic values** as sentinels when they could be valid inputs
- Thinking about **corner cases** that break common implementation patterns

---

**Contribution Status**: Accepted by LeetCode  
**Problem ID**: 86  
**Category**: Missing Test Case / Bug Report  
**Date**: September 2026

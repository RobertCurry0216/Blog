---
layout: post
title: Algorithms Part 6 - Sequential Search
published: true
---

Well I've been off this for a little while, Christmas has been busy!!
Any way I'm back with a new topic for the Algorithms. Today I'm starting on searching algorithms, starting with the very easiest, Sequential Search.

---

## What is?

Sequential search is otherwise known as linear search or brute-force search and it's probably the basic way to search an array. Simply start at the start, check if the value matches, if it doesn't move onto the next value. Simple as it gets.

---

## Implimenting it

Again, this one is simple enough I'm not going to go through all the code. It's pretty self explanitory.

```csharp

public static class Sequential
    {
        public static bool Exists(IEnumerable<int> values, int chkvalue)
        {
            foreach (var v in values)
            {
                if (v == chkvalue) return true;
            }
            return false;
        }
    }

```

# [View the code on Github](https://github.com/RobertCurry0216/NutshellAlgorithms)
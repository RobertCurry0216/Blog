---
layout: post
title: Algorithms Part 1 - Insertion Sort
published: true
---

This is the first part in an ongoing series where I'm going to do my best to impliment different algorithms from scratch using c#.
I'll be starting by working through O'Reilly's Algorithms in a Nutshell.

## What is Insertion Sort?

One of the simpler sorting algorithms, you start by taking the second element in a list. Then shift it left untill it comes across a a value lower than itself. Then repeat for the rest of the values in the list.

```csharp
# example showing the shift left process on the 4th element
# starting list

[1,3,5,2,7]

#step 1
# 5 > 2 so shift left
[1,3,2,5,7]

#step 2
# 3 > 2 so shift left
[1,2,3,5,7]

#step 3
# 1 < 2 so stop
[1,2,3,5,7]

```


## Implimenting it!

This was a very simple one so I'm just going to show the code.

```csharp

public static class Insertion
    {
        public static IEnumerable<int> Sort(IEnumerable<int> values)
        {
            var list = values.ToList();

            for (int i = 1; i < list.Count; i++)
            {
                Insert(list, i, list[i]);
            }
            return list;
        }

        private static void Insert(List<int> list, int pos, int value)
        {
            pos -= 1;
            while (pos >= 0 && list[pos] > value)
            {
                list[pos + 1] = list[pos];
                pos -= 1;
            }
            list[pos + 1] = value;
        }
    }

```
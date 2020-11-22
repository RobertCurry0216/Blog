---
layout: post
title: Algorithms Part 4 - Bucket Sort
published: true
---

Two in one day! I'm on fire.

---

So this is a new one to me and also shockingly has a time complexity of O(n)! I thought O(nLog(n)) was the gold standard for sorting algorithms. There are some drawbacks for this extra speed however:

1. It comes at the cost of extra space.
2. You need to have a hash so that for i<j => hash(i)<hash(j)

## What is?

The skinny of it is for each posible value you have a corrisponding bucket to place it in. So you loop over the list and add each value to its bucket (time O(n)). Then you join all the buckets together (again time O(n)).

Simple, right?

---

## Implimenting it

So for all my other sorting algorithms I've tried to make them same signiture requiring only the list to be sorted:

```csharp
// eg
public static IEnumerable<int> Sort(IEnumerable<int> values)
```

However this one requires some extra info to be passed in. As this is onle for practice and I'm only sorting integers the max and min values should be all I need:

```csharp
public static IEnumerable<int> Sort(IEnumerable<int> values, int min, int max)
```

Now that that is sorted, onto

### Bit 1

First thing to do is create the buckets, but how many?

Well since I'm only working with int, the range from min to max should do the trick, `max - min + 1` gives us our nBucket value (+1 as it needs to be inclusive).

Then it's a simple for loop to create the empty buckets:

```csharp
// create buckets
var nBuckets = max - min + 1;
var buckets = new List<List<int>>();
for (int i = 0; i < nBuckets; i++)
{
    buckets.Add(new List<int>());
}
```

### Bit 2

Next we need to create a `hash` function to find the bucket index for each value.

Again this is quite simple, all we need to do is subtract the min value from the value to find the bucket index. 

```csharp
private static int Hash(int value, int min)
{
    return value - min;
}
```

### Bit 3 and 4

I'm doing both these at once because it's very simple.

First we loop over the values, using the `hash` function to add each value to the correct bucket.

```csharp
// add values to the buckets
foreach (var value in values)
{
    var key = Hash(value, min);
    buckets[key].Add(value);
}
```

Then we join all the buckets together.

```csharp
// join buckets into a single list
var returnValues = new List<int>();
foreach (var bucket in buckets)
{
    returnValues.AddRange(bucket);
}
```

Here it is all together:

```csharp
public static IEnumerable<int> Sort(IEnumerable<int> values, int min, int max)
{
    // create buckets
    var nBuckets = max - min + 1;
    var buckets = new List<List<int>>();
    for (int i = 0; i < nBuckets; i++)
    {
        buckets.Add(new List<int>());
    }

    // add values to the buckets
    foreach (var value in values)
    {
        var key = Hash(value, min);
        buckets[key].Add(value);
    }

    // join buckets into a single list
    var returnValues = new List<int>();
    foreach (var bucket in buckets)
    {
        returnValues.AddRange(bucket);
    }

    return returnValues;
}

private static int Hash(int value, int min)
{
    return value - min;
}
```

---

## How's it run?

Very well, out performing QuickSort on a list of 100000 random ints by almost 50%

- QuickSort: 62ms
- BucketSort: 32ms

---

# [View the code on Github](https://github.com/RobertCurry0216/NutshellAlgorithms)
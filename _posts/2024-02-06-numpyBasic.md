---
layout: single
title: "NumPy Basic"
categories: note
tags: [python, numpy]
author_profile: false
search: true
---

### Introduction

NumPy(Numerical Python) is a powerful numerical library in Python that provides support for large, multi-dimensional arrays and matrices, along with a collection of mathematical functions to operate on these arrays.

As it is libary, you need to import it

```python
import numpy as np
```

#### Simple Examples

```python
array1 = np.array([2, 3, 5, 6, 11, 13]) # one-dimensional array
array2 = np.array([1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]) # two-dimensional array

print(type(array1)) # numpy.ndarray(n dimensional array)
print(type(array2)) # numpy.ndarray(n dimensional array)

print(array1.shape) # (6,)
print(array2.shape) # (3, 4)

print(array1.size) # 6
print(array2.size) # 12
```

#### Several Methods

full
You can create an array with a specified shape(number) and fill it with a constant value.

```python
array1 = numpy.full(6, 7)
print(array1) # [7 7 7 7 7 7]
```

There is an another method which works similarly to full.

```python
array0 = numpy.zeros(6, dtype=int)
array1 = numpy.ones(6, dtype=int)

print(array0) # [0 0 0 0 0 0]
print(array1) # [1 1 1 1 1 1]
```

arange
Pretty similar to how for loop range works

```python
array1 = numpy.arange(6)

print(array1) # [0 1 2 3 4 5]
```

#### Indexing, Slicing

indexing
It is no different from normal indexing, but there is a few things that can be done only with numpy.

```python
array1 = np.array([2, 3, 4, 5, 7, 11, 13])

print(array1[0]) # 2
print(array1[-1]) # 13
print(array1[[1, 3, 4]]) # [3(1st index), 5(3rd index), 7(4th index)]

array2 = np.array([2, 1, 3])

print(array1[array2]) # same as array1[2, 1, 3], so it will be [4(2nd index), 3(1st index)), 5(3rd index)]

```

slicing
Same as normal slicing.

```python
array1 = np.array([2, 3, 4, 5, 7, 11, 13])

print(array1[2:5]) # [4, 5, 7]
print(array1[:5]) # [2, 3, 4, 5, 7]
print(array1[2:6:2]) # [4, 6]
```

### Calculation

When calculating each value in array, use for loop.

This is multiplied by 2

```python
array1 = [1, 2, 3, 4, 5]
for i in range(len(array1)):
    array1[i] = 2 * array1[i]
```

But with numpy, we do not need for loop and do like this

```python
array1 = np.arange(10) # 0 ~ 9
array2 = np.arange(10, 20) # 10 ~ 19

print(array1 * 2) # [0, 2, 4, 6 ... 18]
print(array2 + 2) # [12, 13, 14, 15 ... 21]
print(array1 + array2) # [10, 12, 14, 16 ... 28]
```

### Boolean

boolean calculation as well

```python
array1 = np.array([1, 2, 3, 4, 5, 6])
booleans np.array([True, True, True, False, False, True])


print(array1 > 3) # [False, False, False, True, True, True]
print(array1 % 2 == 0) # [False, True, False, True, False, True]

print(np.where(booleans)) # [0, 1, 2, 5] -> returns index number that has true

# you can apply like
print(np.where(array1 > 3)) # [3, 4, 5]
filter = np.where(array1 > 3)
array1[filter] # [4, 5, 6] -> returns value which is greater than 3
```

### Statistics

NumPy also provides basic statistics.

```python
array1 = np.array([14, 6, 13, 21, 23, 31, 9, 5])

print(array1.max()) # 31
print(array1.min()) # 5
print(array1.mean()) # 15.25 (average)
print(np.median(array1)) # 13.5 (In this case, it has even number of elements which are 13 and 14, so it returns (13 + 14) / 2)
print(array1.std()) # 8.496322733983215
print(array1.var()) # 72.1875
```

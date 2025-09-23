---
content_type: page
description: This page includes lecture notes and an exercise on manipulating lists,
  vectors, and matrices.
learning_resource_types: []
ocw_type: CourseSection
parent_title: The Basics
parent_type: CourseSection
parent_uid: 71bd52f8-0211-8491-207f-722087127ab2
title: Lists, Vectors, and Matrices
uid: 7836f3ce-cf5f-4025-30dd-78bd120b701a
video_metadata:
  youtube_id: null
---

MATLAB® is particularly convenient at calculating with lists of numbers. In fact, it was built for manipulating two-dimensional lists called matrices. An n-by-m matrix has n rows and m columns of numbers, and many MATLAB commands know how to work correctly and efficiently with them.

For example, if we have 10 grocery items whose price we would like to add up, we can write

```
>> sum([2.35 3.45 10.55 12.32 1.99 5.43 2.66 3.78 10.21])
ans =
     52.7400
```

Here we used a function `sum` and its argument was a (row) vector we created "manually". Other vectors have shorthand notation (try them out with various numbers):

*   Many zeros: `zeros(n,m)` (`n` and `m` must be positive integers)
*   Many ones: `ones(n,m)` (same)
*   An increasing list (step =1): `n:m` (`m` must be greater than n)
*   An increasing list with step-size `s`: `n:s:m` (`m` might not be the last element of the list)
*   A column vector (manual): `[3 ; 2; 6 ; 7]` (notice the semicolons)
*   A column of increasing numbers (using transpose) `(n:m)'`

Exercise 3.
-----------

_Do the following practice exercises:_

*   _Try out sequences with step-size_ \\(\\ne1\\): `[4:0.1:5]`, `[5:-2:-5]`.
*   _Create a list of the whole numbers between 10 and 20 (inclusive), find their sum._
*   _Create the vector of the previous question in decreasing order._
*   _Find the sum of the odd numbers between 100 and 200._
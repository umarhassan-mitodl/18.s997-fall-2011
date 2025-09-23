---
content_type: page
description: This page contains short exercises for content review from past lectures
  and an introduction to complex numbers in MATLAB.
draft: false
learning_resource_types: []
ocw_type: CourseSection
parent_title: Vectorization and User-Defined Functions
parent_type: CourseSection
parent_uid: 18645230-e50f-3945-e34d-99f24f40ca3a
title: Warm-up
uid: 81aa80d1-4f27-c72e-1dd0-74d022a27aaa
video_metadata:
  youtube_id: null
---
- Code an _arbitrary precision_ (integer) addition code. The start of the code should be where the "numbers" are defined. For example:   
      
    These numbers are to big to be represented _exactly_ in MATLAB®. Your task is to write code that follows the rules of addition (adding from smallest to largest) and gets the precise answer, in the same format (that is an array of integers). There are various limitations that need to be discussed:   
      
    - First try doing this while allowing yourself only to add small 20 numbers using MATLAB +. You will still need to be crafty about how you find the "ones'' and "tens'' of a given number. Since MATLAB is good with lists, think how you can use a list to do this. You may not use high level functions like mod, rem etc. (But you are encouraged to familiarize yourself with them.)
    - Can you do it with a matrix that represents the addition table for numbers between 0 and 11? Once you create this matrix, you can solve this exercise with +1 as the only "allowed'' arithmetic operation (because MATLAB's index of lists starts from 1 and not 0).
    - Redo this exercise for a different definition of addition, for example, for Z{{< sub "16" >}}.
- Modify the Newton code you wrote for the basin of attraction to look at the basins for another function. How about \\(f(x,y)=(x^4-y, y^4-x)^T\\)? You will have to look for zeros (manually or otherwise) and then change your code and recalculate the Jacobian matrix.
- What is \\(\\sqrt{-1}\\)?
- What is \\((1+i)^4\\)?
- Can you find the roots of \\(x^2+2x+4\\)?
- Where are the roots of \\(x^5+1\\)?
- To operate NOT in a linear algebra way on vectors, you need to put a point (.) in front of the operator: thus 1./\[1 2 4\] is \[1 .5 .25\]. Similarly with .\*. Calculate \\(\\pi\\) by this really (really) bad way: For a large \\(N\\) calculate \\(\\sum\_{n=1}^N\\frac{1}{n^2}\\). This converges to \\(\\pi^2/6\\) as \\(N\\rightarrow\\infty\\). Calculate \\(\\pi\\) using this and find out how large \\(N\\) must be for the resulting value of \\(\\pi\\) to be within 1e-6 of the MATLAB value pi.

```c
N1=[1 9 5 4 3 8 4 8 5 6 0 3 4 0 5 3 2 4 5 6 ]; % to mean  19543848560340532456
N2=[2 3 4 3 2 3 4 5 4 8 6 4 7 8 9 7 6 5 3 2 1 4 6 7 9 ]; 
```
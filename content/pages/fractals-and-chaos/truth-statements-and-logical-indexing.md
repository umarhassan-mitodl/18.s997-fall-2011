---
content_type: page
description: This page includes lectures notes, three exercises, and a homework assignment
  on truth statements and using logical indexing to construct a plot of the Mandlebrot
  fractal.
draft: false
learning_resource_types: []
ocw_type: CourseSection
parent_title: Fractals and Chaos
parent_type: CourseSection
parent_uid: 1d7068b5-ce8d-3b56-622a-e79682a1dd43
title: Truth Statements and Logical Indexing
uid: f5001e47-4d28-4c8a-d02d-71a23087e038
video_metadata:
  youtube_id: null
---
The Mandelbrot Set is the set of points \\(z\\in\\mathbb{C}\\) for which the sequence

\\begin{equation} z\_0=0,\\quad z\_{n+1}=(z\_n)^2+z \\label{eq:mandelbrot} \\end{equation}

remains bounded as \\(n\\rightarrow\\infty\\). Color can be added for the unbounded elements by specifying how "fast" they diverge, for example, how many iterations it takes to reach some large absolute value. (Since once \\(|x\_n|\\) is large enough the sequence will be growing indefinitely.)

To decide on the color of a particular point on the screen \\((x,y)\\), we define a complex number \\(z=x+i y\\) and iterate according to the equation mentioned above.

**Exercise 17.** _With three nested_ for _loops, iterate over_ x=-1.5:.01:0.5 _and_ y=-1:0.01:1. _For each point, iterate, say, 100 times and_ break _if_ abs(z\_n) _is ever too large, say larger than 10. There's no need to keep the sequence of_ \\(z\\)'_s, but be sure not to overwrite the_ \\(z\\) _variable that comes from_ \\(x+iy\\). _If the the sequence grew to be large, leave white, otherwise place a black dot at (the original)_ \\((x,y)\\).

The result should look like this:

{{< resource "4f24071a-c13e-d8e2-3806-e0e570d24a44" >}}

Graphing the Mandelbrot set.

Notice that it takes quite a long time to run, especially if you modify the code to give you a plot with better resolution. To fix this we want to use matrix-at-once calculation. We can create matrices X and Y using meshgrid:

```c
x=-1.5:.1:1;
y=-1.5:.1:1.5;
[X,Y]=meshgrid(x,y);
```

Each element in these matrices holds the appropriate x- or y-value for that position in the matrix. We can now calculate the iterations very simply:

```c
Z=X+1i*Y;   % use 1i since you can overwrite i but 1i will always be sqrt(-1)
Zn=0*Z;     % Start with zeros everywhere
Zn=Zn.^2+Z; 
```

Now that we know how to iterate we need to figure out how to color the different points. Here's where the name of this subsection comes in.

Just as we can perform point-wise arithmetic with a matrix \\(A\\), we can also perform point-wise _comparative_ and _logical_ operations. The comparative operators are: > (greater than), \< (less than) == (equal to\*\*), ~= (not equal to), >= (greater than or equal to) \<= (less than or equal to), while the logical operators are: ~ (not), & (and), | (or). For more help on operators type help ops.

Letting A=magic(4), understand the following constructions:

- A>5
- A\<=3 | A>=10
- A==10 | A==5
- A>5 & A\<10
- ~(A>5 & A\<10)

Given that x = \[1 5 2 8 9 0 1\] and y = \[5 2 2 6 0 0 2\], execute and explain the results of the following commands:

1. x > y
2. y \< x
3. x == y
4. x \<= y
5. y >= x
6. x | y
7. x & y
8. x & (~y)
9. (x > y) | (y \< x)
10. (x > y) & (y \< x)

Together with the functions any and all we can ask questions like "Is any/all element of A equal to 4?", the functions look down the first "non-singleton" dimension by default, which means that they work as you expect for column and row vectors, but for matrices they only "reduce" the first dimension:

```c
>> any(magic(4)==4)      % by default reduces the first dimension (rows):
ans =
     1     0     0     0
>> any(magic(4)==4,2)    % we can tell it to reduce a different one:
ans =
     0
     0
     0
     1
>> any(any(magic(4)==4)) % To reduce a matrix to a single number, we must apply
                         % the functions twice:
ans =
     1
```

In addition we can use a truth matrix to _access_ elements of a matrix. If we have a matrix A and a truth matrix (a matrix found by comparative and logical operations) B _of the same size as A_, we may write A(B) and the result will be the list (not matrix!) of elements of A for which the corresponding elements of B are "true." This is slightly confusing, so an example is useful:

```c
>> A=magic(4);
>> B=A>10;
>> A(B)
ans =
     16
     11
     14
     15
     13
     12
```

**Exercise 18.** _Explain the order of the numbers in the previous example._

In addition to getting the list of elements that correspond to some truth matrix, we can also use the truth matrix to change specific elements of a matrix:

```c
>> A
A =
     16     2     3    13
      5    11    10     8
      9     7     6    12
      4    14    15     1
>> A>5
ans =
     1     0     0     1
     0     1     1     1
     1     1     1     1
     0     1     1     0
>> A(A>5)=0
A =
     0     2     3     0
     5     0     0     0
     0     0     0     0
     4     0     0     1
```

**Exercise 19.** _The exercises here show the techniques of logical indexing. Given_ x = 1:10 and y = \[3 1 5 6 8 2 9 4 7 0\], _execute and interpret the results of the following commands:_

{{< tableopen >}}{{< tbodyopen >}}{{< tropen >}}{{< tdopen >}}
_1(a)_
{{< tdclose >}}{{< tdopen >}}
(x &gt; 3) &amp; (x &lt; 8)
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_1(b)_
{{< tdclose >}}{{< tdopen >}}
x(x &gt; 5)
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_1(c)_
{{< tdclose >}}{{< tdopen >}}
y(x &lt;= 4)
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_1(d)_
{{< tdclose >}}{{< tdopen >}}
x( (x &lt; 2) | (x &gt;= 8) )
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_1(e)_
{{< tdclose >}}{{< tdopen >}}
y( (x &lt; 2) | (x &gt;= 8) )
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_1(f)_
{{< tdclose >}}{{< tdopen >}}
x(y &lt; 0)
{{< tdclose >}}{{< trclose >}}{{< tbodyclose >}}{{< tableclose >}}

_Given_ x = \[3 15 9 12 -1 0 -12 9 6 1\], _provide the command(s) that will_

{{< tableopen >}}{{< tbodyopen >}}{{< tropen >}}{{< tdopen >}}
_2(a)_
{{< tdclose >}}{{< tdopen >}}
_… set the positive elements of x to zero._
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_2(b)_
{{< tdclose >}}{{< tdopen >}}
_… set values of x that are multiples of 3 to 3 (rem will help here)._
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_2(c)_
{{< tdclose >}}{{< tdopen >}}
_… multiply the even elements of x by 5._
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_2(d)_
{{< tdclose >}}{{< tdopen >}}
_… extract the values of x that are greater than 10 into a vector called y._
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_2(e)_
{{< tdclose >}}{{< tdopen >}}
_… set the values in x that are less than the mean value of x to zero._
{{< tdclose >}}{{< trclose >}}{{< tropen >}}{{< tdopen >}}
_2(f)_
{{< tdclose >}}{{< tdopen >}}
_… set the values in x that are above the mean to their difference from the mean._
{{< tdclose >}}{{< trclose >}}{{< tbodyclose >}}{{< tableclose >}}

**Homework 8.** _Going back to the Mandelbrot set calculation, we can keep a matrix that informs us of the step at which each element has become too large. Let's call it_ Iter _and agree that a zero value corresponds to_ _"not too large yet" and a non-zero value will be the iteration number at which the element has become big (absolute value greater than 10). At each step we update only these elements of_ Zn _that are still small (those that correspond to_ ~Iter _being true), then find out which are the new big elements (_abs(Zn)>10 _and_ ~Iter_) and set the corresponding values of_ Iter _to the iteration number (from the for loop). Notice that using_ ~ _on a matrix of numbers returns_ true _for the elements that are zero and_ false _for those that are not zero. After 100 iterations you need to plot the results. Since for the locations that did not converge we have the number of iterations it needs to reach size 10, we can make a nicer plot than the black-and-white plot from before. For this we can use:_

```c
p=pcolor(X,Y,Iter);
set(p,'edgecolor','none')
axis equal
```

_We only need to plot once, after all the iterations have happened. Notice how much faster this is than the nested loops from before. Your result should look like this:_

{{< resource "1522363c-dcb7-8685-7ea9-0f6e6ff6ce9c" >}}

Graphing the Mandelbrot set with logical indexing.

_Some ideas for "extra credit":_

- _Try zooming into places of interest; see how the fractal is "self similar"?_
- _Change the number of iterations and see how things change._

\*\*Make sure you understand the difference between = and ==; they mean entirely different things, and writing one instead of the other will most likely result in a strange error.
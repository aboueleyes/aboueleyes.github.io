@def title = "Permutation Matrix"
@def tags = ["math", "ml"]
@def hascode = true

# Permutation Matrix

<!-- \tableofcontents  -->


> A permutation matrix is a square matrix. It’s always raw equivalent to the Identity matrix

For size $n$ there exists $n!$ permutation matrcies.

For example there exists $2$ permutation matrcies of size $2$ which are:

$$ \begin{bmatrix}
1 & 0  \\
0 & 1 
\end{bmatrix} 
,  \begin{bmatrix}
0 & 1  \\
1 & 0 
\end{bmatrix}$$

A permutation matrix is non-singular, and the determinant is always $ \pm 1$

You can imagine the 1’s in the $n \times n$ matrix as non attacking rooks in an
$ n \times n$ chessboard

~~~
<img src="../assets/chess.png">
~~~
# Permutation In Matrix Matrix Multiplication

## Left Multiplication
*Left Multiplication* by a permutation matrix rearranges the corresponding rows

$$ 
    \begin{bmatrix}
        0 & 1 & 0 \\
        0 & 0 & 1 \\
        1 & 0 & 0 
    \end{bmatrix}  
    \begin{bmatrix}
        x1 \\
        x2 \\
        x3 \\
    \end{bmatrix} = 
    \begin{bmatrix}
        x3 \\
        x1 \\
        x2 \\
    \end{bmatrix}
$$
@@colbox-blue
The $1$ in the first row is in the $2^{nd}$ column so the $2^{nd}$ the row of the other matrix will be placed in the first row and so on ..
@@

$$
    \begin{bmatrix}
        0 & 1 & 0  \\
        0 & 0 & 1  \\
        1 & 0 & 0 
    \end{bmatrix}
    \begin{bmatrix}
    a &  a & a \\
    b &  b & b \\
    c &  c & c \\
    \end{bmatrix} = 
    \begin{bmatrix}
    b &  b & b \\
    c &  c & c \\
    a &  a & a \\
    \end{bmatrix}
$$


Let's See some `julia` Code
```julia
A = [[0, 1 , 0] [0, 0, 1] [1, 0, 0]]
B = [[1, 2, 3] [4, 5, 6] [7, 8, 9]]
@show A * B 
```
```
3×3 Matrix{Int64}:
 3  6  9
 1  4  7
 2  5  8
```

## Right Multiplication
*Right multiplication* by a permutation matrix rearranges the corresponding columns

$$
    \begin{bmatrix}
    a &  b & c \\
    a &  b & c \\
    a &  b & c \\
    \end{bmatrix} 
    \begin{bmatrix}
        0 & 1 & 0  \\
        0 & 0 & 1  \\
        1 & 0 & 0 
    \end{bmatrix}
    \begin{bmatrix}
    c &  a & b \\
    c &  a & b \\
    c &  a & b \\
    \end{bmatrix}
    
$$


Let's test with `julia`
```julia
A = [[0, 1 , 0] [0, 0, 1] [1, 0, 0]]
B = [[1, 2, 3] [4, 5, 6] [7, 8, 9]]
@show B * A
```
```
3×3 Matrix{Int64}:
 4  7  1
 5  8  2
 6  9  3

```
We can also combine both as follows


$$
    \begin{bmatrix}
        0 & 1 & 0  \\
        0 & 0 & 1  \\
        1 & 0 & 0 
    \end{bmatrix}
    \begin{bmatrix}
        a & b & c \\ 
        d & f & e \\ 
        g & h & i 
    \end{bmatrix}
    \begin{bmatrix}
        0 & 1 & 0  \\
        0 & 0 & 1  \\
        1 & 0 & 0 
    \end{bmatrix} = 

    \begin{bmatrix}
        f & d & e \\ 
        i & g & h \\ 
        c & a & b 
    \end{bmatrix}
    
$$

I found This matrix very interesting! It’s also an *`orthogonal`* matrix , which means it’s equal to its transpose.
What about you? Do also you find it interesting?

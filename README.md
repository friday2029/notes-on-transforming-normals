# Notes On Transforming Normals

A better condition to derive the matrix X required to maintain the properties of a normal is to use the cross product.

$$
n = t\times b
$$

Then this should be true,

$$
Xn = Mt\times Mb
$$



Let M\[n] be the nth column of the 3x3 transformation matrix M,

$$
Xn = (t_xM_{[0]}+t_yM_{[1]}+t_zM_{[2]})\times (b_xM_{[0]}+b_yM_{[1]}+b_zM_{[2]})
$$

we can distribute the cross product using the distributive property of cross product,

$$
(u+v)\times w=(u\times w)+(v\times w)
$$

$$
\begin{align}
Xn = &(t_xM_{[0]}\times (b_xM_{[0]}+b_yM_{[1]}+b_zM_{[2]}))+ \\
&(t_yM_{[1]}\times (b_xM_{[0]}+b_yM_{[1]}+b_zM_{[2]}))+\\
&(t_zM_{[2]}\times (b_xM_{[0]}+b_yM_{[1]}+b_zM_{[2]}))
\end{align}
$$

$$
\begin{align}
Xn = &(t_xM_{[0]}\times b_xM_{[0]} + t_xM_{[0]}\times b_yM_{[1]} + t_xM_{[0]}\times b_zM_{[2]})+ \\
&(t_yM_{[1]}\times b_xM_{[0]} + t_yM_{[1]}\times b_yM_{[1]} + t_yM_{[1]}\times b_zM_{[2]})+\\
&(t_zM_{[2]}\times b_xM_{[0]} + t_zM_{[2]}\times b_yM_{[1]} + t_zM_{[2]}\times b_zM_{[2]})
\end{align}
$$

$$
\begin{align}
Xn = &(t_xb_x(M_{[0]}\times M_{[0]}) + t_xb_y(M_{[0]}\times M_{[1]}) + t_xb_z (M_{[0]}\times M_{[2]}))+ \\
&(t_yb_x(M_{[1]}\times M_{[0]}) + t_yb_y(M_{[1]}\times M_{[1]}) + t_yb_z(M_{[1]}\times M_{[2]}))+\\
&(t_zb_x(M_{[2]}\times M_{[0]}) + t_zb_y(M_{[2]}\times M_{[1]}) + t_zb_z(M_{[2]}\times M_{[2]}))
\end{align}
$$

A vector cross product with itself results in $0$ so some of the terms fall out,

$$
\begin{align}
Xn = &t_xb_y(M_{[0]}\times M_{[1]}) + t_xb_z (M_{[0]}\times M_{[2]})+ \\
&t_yb_x(M_{[1]}\times M_{[0]}) + t_yb_z(M_{[1]}\times M_{[2]})+\\
&t_zb_x(M_{[2]}\times M_{[0]}) + t_zb_y(M_{[2]}\times M_{[1]})
\end{align}
$$

Using the anticommutative property of the cross product,

$$
a\times b = -b\times a
$$

$$
\begin{align}
Xn = & t_yb_z(M_{[1]}\times M_{[2]})+ t_zb_y(M_{[2]}\times M_{[1]})+\\
&t_zb_x(M_{[2]}\times M_{[0]}) + t_xb_z (M_{[0]}\times M_{[2]})+ \\
&t_xb_y(M_{[0]}\times M_{[1]}) + t_yb_x(M_{[1]}\times M_{[0]})\\
\end{align}
$$

$$
\begin{align}
Xn = & t_yb_z(M_{[1]}\times M_{[2]})- t_zb_y(M_{[1]}\times M_{[2]})+\\
&t_zb_x(M_{[2]}\times M_{[0]}) - t_xb_z (M_{[2]} \times M_{[0]})+ \\
&t_xb_y(M_{[0]}\times M_{[1]}) - t_yb_x(M_{[0]}\times M_{[1]})\\
\end{align}
$$

Factoring out the common factor results in,

$$
\begin{align}
Xn = &(t_yb_z - t_zb_y)(M_{[1]}\times M_{[2]})+\\
&(t_zb_x - t_xb_z)(M_{[2]}\times M_{[0]})+ \\
&(t_xb_y - t_yb_x)(M_{[0]}\times M_{[1]})\\
\end{align}
$$

We can see the elements of $t \times b$ on the left and a 3x3 matrix $M'$ on the right with each term being one column of $M'$.

$$
M' = 
M_{[1]}\times M_{[2]} + M_{[2]}\times M_{[0]} + M_{[0]}\times M_{[1]}
$$

$$
M' = 
\begin{bmatrix}
M_{11}M_{22} - M_{21}M_{12} & M_{12}M_{20} - M_{22}M_{10} & M_{10}M_{21}-M_{20}M_{11}\\
M_{21}M_{02} - M_{01}M_{22} & M_{22}M_{00} - M_{02}M_{20} & M_{20}M_{01}-M_{00}M_{21}\\
M_{01}M_{12} - M_{11}M_{02} & M_{02}M_{10} - M_{12}M_{00} & M_{00}M_{11}-M_{10}M_{01}\\
\end{bmatrix} 
$$


$M'$ is the cofactor matrix of M(notated $cof(M)$ ). The adjugate matrix of M(notated $adj(M)$ ) is defined to be the transpose of the cofactor.

From the following definition of the matrix inverse we can see that the following have to be true for a $cof(M)^T$ or $adj(M)$ matrix. 

$$
M^{-1}=\frac{adj(M)}{det(M)}
$$

$$
M^{-1}M=I
$$

$$
(cof(M))^TM=det(M)I
$$

We can use this to prove that $(M')^T$ is the adjugate matrix and thus $M'$ is the cofactor matrix of M.

The following have to be true,

$$
(M_{[i]}\times M_{[j]})\cdot M_{[k]} = det(M) , \ for\ any\ \{i,j,k\} \ that's \ an \ even \ permutation \ of \{0,1,2\} 
$$
Or,
$$
(M')^TM = det(M)I
$$

$$
\begin{align}
&\begin{bmatrix}
M_{00} & M_{01} & M_{02}\\
M_{10} & M_{11} & M_{12}\\
M_{20} & M_{21} & M_{22}\\
\end{bmatrix} \\
\begin{bmatrix}
M_{11}M_{22} - M_{21}M_{12} & M_{21}M_{02} - M_{01}M_{22} & M_{01}M_{12} - M_{11}M_{02}\\
M_{12}M_{20} - M_{22}M_{10} & M_{22}M_{00} - M_{02}M_{20} & M_{02}M_{10} - M_{12}M_{00}\\
M_{10}M_{21}-M_{20}M_{11} & M_{20}M_{01}-M_{00}M_{21} & M_{00}M_{11}-M_{10}M_{01}\\
\end{bmatrix}
&\begin{bmatrix}
det(M) & 0 & 0\\
0 & det(M) & 0\\
0 & 0 & det(M)\\
\end{bmatrix}
\end{align}
$$

$$
(M_{[1]}\times M_{[2]})\cdot M_{[0]}
$$
$$
=M_{00}(M_{11}M_{22} - M_{21}M_{12}) + M_{10}(M_{21}M_{02} - M_{01}M_{22}) + M_{20}(M_{01}M_{12} - M_{11}M_{02}) = det(M)
$$

$$
(M_{[2]}\times M_{[0]})\cdot M_{[1]}
$$
$$
=M_{01}(M_{12}M_{20} - M_{22}M_{10}) + M_{11}(M_{22}M_{00} - M_{02}M_{20}) + M_{21}(M_{02}M_{10} - M_{12}M_{00})
$$
$$
=M_{01}M_{12}M_{20} - M_{01}M_{22}M_{10} + M_{11}M_{22}M_{00} - M_{11}M_{02}M_{20} + M_{21}M_{02}M_{10} - M_{21}M_{12}M_{00}
$$
$$
=M_{00}(M_{11}M_{22} - M_{21}M_{12}) + M_{10}(M_{21}M_{02} - M_{01}M_{22}) + M_{20}(M_{01}M_{12} - M_{11}M_{02}) = det(M)
$$

and so on...

Thus, $(M')^T = adj(M)$ and $M' = cof(M)$. 

$$
Xn = (t\times b) cof(M)
$$
Solving for X, we find that it is equal to the cofactor of M or the transpose of the adjugate of M.
$$
Xn = cof(M)n
$$

$$
X= cof(M) = adj(M)^T 
$$

#### Examining the difference between using the transpose of the inverse and the adjugate transpose.

$$
M^{-1}=\frac{adj(M)}{det(M)}
$$

$$
cof(M)=adj(M)^T
$$

$$
cof(M)=det(M)(M^{-1})^T
$$

This explains why simply using the transpose of the inverse of M was not sufficient since the $det(M)$ contribution is missing. For $det(M) < 0$ the sign would be flipped.  


----
#### RESOURCES READ

Eric Lengyel
https://terathon.com/blog/transforming-normals.html

Normals revisited by Dale Weiler(Graphitemaster) 
https://github.com/graphitemaster/normals_revisited?tab=readme-ov-file

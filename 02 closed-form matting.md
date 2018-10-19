# Closed-form matting

$$I = \alpha F + ( 1 - \alpha) B$$
Color Line Space Assumption:  
>Forground and Background Colors in a small window lie on a straight line in RGB space   

***Notice***  
1. Line depends on which window we choose
2. Assumption is based on RGB space, so I doubt that it's not hold on other color space
3. Edge is ok,  like black(0,0,0) and white(255,255,255) can be connected on a straight line  

$$F_i = \beta_i F_1 + ( 1 - \beta_i ) F_2$$
$$B_i = \gamma_i B_1 + ( 1 - \gamma_i ) B_2$$  
If Color Line Assumption holds, the the true mate $\alpha$ satifies 
$$\alpha = \mathbf{\alpha}^\mathrm{T} I_i +b $$
For all pixels in the window
( $I_i$ is 3-by-1 matrix, $ \mathbf{\alpha}^\mathrm{T}$ is 3-by-1 vector, and $b$ is scalar)   ## Why is this Time?  
$$
{\begin{equation}
\begin{aligned}
I_i &= \alpha_i F_i + (1 - \alpha_i) B_i \\
&= \alpha_i ( \beta_i F_1 + ( 1 - \beta_i ) F_2) + ( 1 - \alpha_i) ( \gamma_i B_1 + ( 1 - \gamma_i ) B_2) \\
&=  \alpha_i \beta_i F1 + \alpha_i F_2 - \alpha_i \beta_i F_2 + \alpha_i B1 - \alpha_i \gamma_i B_1 + B_2 -  \alpha_i  B_2 - \gamma_i B_2 + \alpha_i \gamma_i B_2
\end{aligned}
\end{equation}
}
$$
So, we can use matrix manuplation to formulate the equation above
$$
I_i - B_2 = 
{\left[\begin{matrix}
F_2 - B_2\\
F_1 - F_2\\
B_1 - B_2
\end{matrix}\right]}
{\left[\begin{matrix}
\alpha_i \\
\alpha_i\beta_i \\
\alpha_i\gamma_i
\end{matrix}\right]}
$$
which can be like this  
$$
I_i - B_2 = 
{\left[\begin{matrix}
    F_2 - B_2, F_1-F_2, B_1-B_2
\end{matrix}\right]
}
{\left[\begin{matrix}
\alpha_i \\
\alpha_i \beta_i \\
\gamma_i - \alpha_i \gamma_i
\end{matrix}\right]}
$$
and
$$
{\left[\begin{matrix}
\alpha_i \\
unknown \\
unknown
\end{matrix}\right]} = 
{\left(\begin{matrix}
\blacksquare \space\space \blacksquare \space\space \blacksquare \\
\blacksquare \space\space \blacksquare \space\space \blacksquare \\
\blacksquare \space\space \blacksquare \space\space \blacksquare
\end{matrix}\right)^{-1}}
{\left[\begin{matrix}
    I_i - B_2
\end{matrix}\right]}
$$

大括号公式左对齐



每一行开头加一个& 就可以实现左对齐

```tex
\begin{equation}\label{1}
	 dp[i][0][0]=max \left\{
	\begin{aligned}
		& dp[i-1][0][0]       &      \\
		& dp[i-1][0][1]-bitPrice[i] \times 1.02     &      \\
		& dp[i-1][1][0]-GPrice[i] \times 1.01     &     \\
		& dp[i-1][1][1]-bitPrice[i] \times 1.02-GPrice[i] \times 1.01    &    
	\end{aligned} 
	\right. 
\end{equation}
```


# Matlab

用矩阵的思维去思考一些运算, 会有宏观的视野, 而不是拘束在令人分散精力的 for 上面

## Cell

类似于矩阵的指针

- cellfun
- celldisp
- cellplot

## struct

有点类似 map, 或者 json

## operator

- `.*`: 矩阵对应元素相乘
- `./`: 矩阵对应元素相除

`.`有对应元素的意思

- `/`: $A/B = A \times B^{-1}$ 分母放在右边
- `\`: $A\backslash B = A^{-1} \times B$ 分母放在左边

## 矩阵的条件数

$$cond(A) = ||A|| \times ||A^{-1}||$$

- 病态: $cond(A) \gg 1$
- 良态: $cond(A) \approx 1$

## 矩阵的分解

- Cholesky 分解: $A = LL^T$, 针对对称正定矩阵
- LU 分解: $A = LU$
- LDL 分解: $A = LDL^T$, 针对对称正定矩阵
- QR 分解: $A = QR$

LU 解方程:

$$Ax = b \Rightarrow L(Ux) = b \Rightarrow Ly = b, Ux = y$$

## plot

- plot
- fplot
- subplot
- hold on/off

## 符号运算

- subs
- eval
- syms

## lambda

```matlab
f = @(x) x^2 + 2*x + 1;
```

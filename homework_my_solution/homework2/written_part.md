# CS224n ： Assignment2  ， written part

[qusetion website](<http://web.stanford.edu/class/cs224n/assignments/a2.pdf>)

## Variables notation

**Attention**: All the variables' dimensions here are consistent with the code part in Assignment 2 for easy understanding.

**U** , matrix of shape (vocab_size,embedding_dim)  ,all the ‘outside’ vectors . 

**V**, matrix of shape (vocab_size,embedding_dim)  ,all the ‘center’ vectors .

**y**, vector of shape (vocab_size,1), the true empirical distribution **y** is a one-hot vector with a 1 for the true outside word o, and 0 everywhere else .

$\hat{\boldsymbol{y}}$, vector of shape (vocab_size,1),  the predicted distribution $\hat{\boldsymbol{y}}$  is the probability distribution$ P(O|C = c)$ given by our model .



## question a

Given outside word o and context word c.

The distribution of **y** is as follows:

$$
y_w=
\begin{cases}
1& \text{w=o}\\
0& \text{w!=o}
\end{cases}
$$

$$
-\sum_{w=1}^{V} y_wlog(\hat{y_w}) = -y_olog(\hat{y_o})=-log(\hat{y_o})
$$

Here , V represents the vocab_size.

## question b

$$
\frac{\partial{J_{naive-softmax}(\boldsymbol v_c,o,\boldsymbol	U)}}{\partial \boldsymbol  v_c} \\= 
-\frac{\partial{log(P(O=o|C=c))}}{\partial  \boldsymbol v_c}  \\ =
-\frac{\partial{log(exp( \boldsymbol u_o^T\boldsymbol v_c))}}{\partial \boldsymbol v_c} + \frac{\partial{log(\sum_{w=1}^{V}exp(\boldsymbol u_w^T\boldsymbol v_c))}}{\partial \boldsymbol v_c} \\=
-\boldsymbol u_o + \sum_{w=1}^{V} \frac{exp(\boldsymbol u_w^T\boldsymbol v_c)}{\sum_{w=1}^{V}exp(\boldsymbol u_w^T\boldsymbol v_c)}\boldsymbol u_w \\=
-\boldsymbol u_o+    \sum_{w=1}^{V}P(O=w|C=c)\boldsymbol u_w     \\=
\boldsymbol U^T(\hat{\boldsymbol y} - \boldsymbol y)
$$

## question c

$$
\frac{\partial{J_{naive-softmax}(\boldsymbol v_c,o,\boldsymbol	U)}}{\partial \boldsymbol u_w} \\=
-\frac{\partial{log(exp(\boldsymbol u_o^T\boldsymbol v_c))}}{\partial \boldsymbol u_w} + \frac{\partial{log(\sum_{w=1}^{V}exp(\boldsymbol u_w^T\boldsymbol v_c))}}{\partial \boldsymbol u_w}
$$

when w = o,
$$
\frac{\partial{J_{naive-softmax}(\boldsymbol v_c,o,\boldsymbol	U)}}{\partial\boldsymbol  u_w} \\=
-\boldsymbol v_c + \frac{1}{\sum_{w=1}^{V} exp(\boldsymbol u_w^T\boldsymbol v_c)}\frac{\partial \sum_{w=1}^{V} exp(\boldsymbol u_w^T\boldsymbol v_c)}{\partial \boldsymbol u_o} \\=
-\boldsymbol v_c +  \frac{1}{\sum_{w=1}^{V} exp(\boldsymbol u_w^T\boldsymbol v_c)}\frac{\partial  exp(\boldsymbol u_o^T\boldsymbol v_c)}{\partial \boldsymbol u_o}  \\=
-\boldsymbol v_c + \frac{ exp(\boldsymbol u_o^T\boldsymbol v_c)}{\sum_{w=1}^{V} exp(\boldsymbol u_w^T\boldsymbol v_c)}\boldsymbol v_c \\=
(P(O=o|C=c)-1))\boldsymbol v_c
$$
when w != o,
$$
\frac{\partial{J_{naive-softmax}(\boldsymbol v_c,o,\boldsymbol	U)}}{\partial \boldsymbol u_w} \\=
 \frac{ exp(\boldsymbol u_w^T\boldsymbol v_c)}{\sum_{w=1}^{V} exp(\boldsymbol u_w^T\boldsymbol v_c)}\boldsymbol v_c \\=
 P(O=w|C=c)\boldsymbol v_c
$$
In summary,
$$
\frac{\partial{J_{naive-softmax}(\boldsymbol v_c,o,\boldsymbol	U)}}{\partial \boldsymbol U} \\=
(\hat {\boldsymbol y} - \boldsymbol y)^T\boldsymbol v_c
$$

## question d

$$
\frac{\partial \sigma(x)}{\partial x} = \frac{\partial \frac{e^x}{e^x+1}}{\partial x} = \frac{e^x(e^x+1)-e^xe^x}{(e^x+1)^2} \\= \frac{e^x}{(e^x+1)^2} = \sigma (x) (1- \sigma(x))
$$

## question e

$$
\frac{\partial{J_{neg-sample}(\boldsymbol v_c,o,\boldsymbol	U)}}{\partial\boldsymbol  v_c} \\=
\frac{\partial (-log(\sigma (\boldsymbol u_o^T\boldsymbol v_c))-\sum_{k=1}^{K} log(\sigma (-\boldsymbol u_k^T\boldsymbol v_c)))}{\partial \boldsymbol v_c} \\=
-\frac{\sigma(\boldsymbol u_o^T\boldsymbol v_c)(1-\sigma(\boldsymbol u_o^T\boldsymbol v_c))}{\sigma(\boldsymbol u_o^T\boldsymbol v_c)}\frac{\partial \boldsymbol u_o^T\boldsymbol v_c}{\partial \boldsymbol v_c} - 
\sum_{k=1}^{K}\frac{\partial log(\sigma(-\boldsymbol u_k^T\boldsymbol v_c))}{\partial \boldsymbol v_c} \\=
-(1-\sigma(\boldsymbol u_o^T\boldsymbol v_c))\boldsymbol u_o+\sum_{k=1}^{K}(1-\sigma(-\boldsymbol u_k^T\boldsymbol v_c))\boldsymbol u_k
$$

$$
\frac{\partial{J_{neg-sample}(\boldsymbol v_c,o,\boldsymbol	U)}}{\partial \boldsymbol u_o} \\=
\frac{\partial (-log(\sigma (\boldsymbol u_o^T\boldsymbol v_c))}{\partial \boldsymbol u_o} = -(1-\sigma(\boldsymbol u_o^T\boldsymbol v_c))\boldsymbol v_c
$$


$$
\frac{\partial{J_{neg-sample}(\boldsymbol v_c,o,\boldsymbol	U)}}{\partial \boldsymbol u_k} \\=
\frac{\partial (-log(\sigma (-\boldsymbol u_k^T\boldsymbol v_c))}{\partial \boldsymbol u_k} = (1-\sigma(-\boldsymbol u_k^T\boldsymbol v_c))\boldsymbol v_c
$$

## qustion f

**i)**
$$
\frac{\partial J_{skip-gram}(\boldsymbol v_c,w_{t-m},...,w_{t+m},\boldsymbol U)}{\partial \boldsymbol U} \\=
\sum_{-m<=j<=m,j!=0}\frac{\partial J(\boldsymbol v_c,w_{t+j},\boldsymbol U)}{\partial \boldsymbol U}
$$
**ii)**

when w=c,
$$
\frac{\partial J_{skip-gram}(\boldsymbol v_c,w_{t-m},...,w_{t+m},\boldsymbol U)}{\partial \boldsymbol v_c} \\=
\sum_{-m<=j<=m,j!=0}\frac{\partial J(\boldsymbol v_c,w_{t+j},\boldsymbol U)}{\partial \boldsymbol v_c}
$$
**iii)**

when w!=c,
$$
\frac{\partial J_{skip-gram}(\boldsymbol v_c,w_{t-m},...,w_{t+m},\boldsymbol U)}{\partial \boldsymbol v_w} \\= \boldsymbol 0
$$



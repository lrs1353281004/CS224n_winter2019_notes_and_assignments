# CS224n ： Assignment2  ， written part

[qusetion website](<http://web.stanford.edu/class/cs224n/assignments/a2.pdf>)

## Variables notation

**Attention**: All the variables' dimensions here are consistent with the code part in Assignment 2 for easy understanding.

**U** , matrix of shape (vocab_size,embedding_dim)  ,all the ‘outside’ vectors . 

**V**, matrix of shape (vocab_size,embedding_dim)  ,all the ‘center’ vectors .

**y**, vector of shape (vocab_size,1), the true empirical distribution **y** is a one-hot vector with a 1 for the true outside word o, and 0 everywhere else .

$\hat{\boldsymbol{y}}$,vector of shape (vocab_size,1),  the predicted distribution $\hat{\boldsymbol{y}}$  is the probability distribution$ P(O|C = c)​$ given by our model .



## question a

Given outside word o and context word c.

The distribution of **y** is as follows:

$$ y_w=\left\{
\begin{aligned}
1,w & =  \ o \\
0, w& \neq\ o\\
\end{aligned}
\right.
​$$

## question b


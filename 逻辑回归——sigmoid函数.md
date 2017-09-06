## LR为什么用sigmoid函数。这个函数有什么优点和缺点？为什么不用其他函数？

### 逻辑回归之所以用sigmoid函数，是由他的假设决定的。

>Logistic regression was developed by statistician David Cox in 1958.[2][3] The binary logistic model is used to estimate the probability of a binary response based on one or more predictor (or independent) variables (features).
——https://en.wikipedia.org/wiki/Logistic_regression


逻辑回归在1958年由David Cox发展出来，二元逻辑斯蒂模型是用来估计一个二元响应变量的概率值。
>The model of logistic regression, however, is based on quite different assumptions (about the relationship between dependent and independent variables) from those of linear regression. In particular the key differences between these two models can be seen in the following two features of logistic regression. First, the conditional distribution {\displaystyle y\mid x} y\mid x is a Bernoulli distribution rather than a Gaussian distribution, because the dependent variable is binary. Second, the predicted values are probabilities and are therefore restricted to (0,1) through the logistic distribution function because logistic regression predicts the probability of particular outcomes.
——https://en.wikipedia.org/wiki/Logistic_regression


逻辑回归模型基于不同于线性回归的、关于因变量y和自变量x之间关系的假设。特别的，这两种模型的区别可以在以下两个逻辑回归的特性中看出来：
1. 逻辑回归的条件分布y|x是伯努利分布，而线性回归的是高斯分布，因为逻辑回归的因变量是二元变量（0或1）。
2. 逻辑回归要预测的值是概率，因此要通过逻辑分布函数约束到（0,1）区间，因为逻辑回归预测的是某个输出值（0或1）的概率。

>线性回归用于二分类时，首先想到下面这种形式，p=wx,p是属于类别的概率：
但是这时存在的问题是：
1）等式两边的取值范围不同，右边是负无穷到正无穷，左边是[0,1]，这个分类模型存在问题
2）实际中的很多问题，都是当x很小或很大时，对于因变量P的影响很小，当x达到中间某个阈值时，影响很大。即实际中很多问题，概率P与自变量并不是直线关系。
所以，上面这分类模型需要修整，怎么修正呢？统计学家们找到的一种方法是通过logit变换对因变量加以变换。
http://blog.csdn.net/a819825294/article/details/51172466


>If the data samples have nn features, and we think we can represent this probability via some linear combination, we could represent this as:P(y=1∣x)=wo+w1x1+w2x2+...+wnxn. ...it would seem hard to map an arbitrary linear combination of inputs, each would may range from −∞ to ∞ to a probability value in the range of 0 to 1.The odds ratio is a related concept to probability that can help us. 
http://karlrosaen.com/ml/notebooks/logistic-regression-why-sigmoid/


我们一开始希望输入变量x的线性组合能表示y=1的概率，但x的线性组合的取值范围为负无穷到正无穷，而概率为0到1，不过概率的对数几率可以是负无穷到正无穷，
log_odds(P(y=1∣x))=wo+w1x1+w2x2+...+wnxn。所以从这里可以推导出sigmoid函数。


>The logistic regression is one special case of the generalized linear models. In generalized linear models, you assume that the data don't arise from normal distribution. It could be other distributions as long as it's from exponential family. If the data are binary, then it's very natural to think that they follow a binomial distribution. Because of some reasons, we can't just say E[Y|X]=Xβ, so we apply some function around the expectation of Y: η(E[Y|X])=Xβ. The function η(⋅)is called a link function.
 In the case of Bernoulli, the canonical link function is logit since p(y|p)=exp{ylog(p/(1−p))+log(1−p)},And E[Y]=p=exp{η(p)}/(1+exp{η(p)}). This is called the inverse parameter mapping and this is where the sigmoid function arises.
https://www.quora.com/Logistic-regression-softmax-function-Why-do-you-use-the-exponential-function-in-the-sigmoid-function/answer/Daeyoung-Lim-1


逻辑回归是广义线性回归的一个特例。在广义线性回归中，我们认为数据并不是只能服从正态分布，而可以是其他分布，只要他来自于指数族。如果y是二元变量，则很自然地认为他服从二项分布。我们不能简单地认为E[Y|X]=Xβ，所以我们在他外面加了一个变换——η(E[Y|X])=Xβ。 η(⋅)被称为link function。在y是二元变量，η(⋅)就是logit，因为p(y|p)=exp{ylog(p/(1−p))+log(1−p)}。η(p)=log(p/(1−p)

>In section 4.2 of Pattern Recognition and Machine Learning (Springer 2006), Bishop shows that the logit arises naturally as the form of the posterior probability distribution in a Bayesian treatment of two-class classification. He then goes on to show that the same holds for discretely distributed features, as well as a subset of the family of exponential distributions. For multi-class classification the logit generalizes to the normalized exponential or softmax function.
--https://stats.stackexchange.com/questions/162988/why-sigmoid-function-instead-of-anything-else


在PRML这本书里，Bishop指出logit函数很自然地出现在用贝叶斯方法处理二分类问题时的后验概率分布表达式里。
![Image of Bishop logit](https://pic1.zhimg.com/v2-60888683e38d20327965cebf191830e1_b.png)

[What is a Logit Function and Why Use Logistic Regression?](http://www.theanalysisfactor.com/what-is-logit-function/).
>One of the big assumptions of linear models is that the residuals are normally distributed.  This doesn’t mean that Y, the response variable, has to also be normally distributed, but it does have to be continuous, unbounded and measured on an interval or ratio scale.
>
>Unfortunately, categorical response variables are none of these.
>
>No matter how many transformations you try, you’re just never going to get normal residuals from a model with a categorical response variable.
>
>There are a number of alternatives though, and one of the most popular is logistic regression.
In many ways, logistic regression is very similar to linear regression.  One big difference, though, is the logit link function.
>
>The Logit Link Function
>A link function is simply a function of the mean of the response variable Y that we use as the response instead of Y itself.
>Why Bother With This Logit Function?
>
>Well, if we used Y as the outcome variable and tried to fit a line, it wouldn’t be a very good representation of the relationship.  The following graph shows an attempt to fit a line between one X variable and a binary outcome Y.
>
>You can see a relationship there–higher values of X are associated with more 0s and lower values of X have more 1s.  But it’s not a linear relationship.
>![Image of logit](http://taf-website-backup.s3.amazonaws.com/binary-graph.png)
>
>Okay, fine.  But why mess with logs and odds?  Why not just use P as the outcome variable?  Everyone understands probability.
>
>Here’s the same graph with probability on the Y axis:
>![Image of logit](http://taf-website-backup.s3.amazonaws.com/sigmoid-graph.png)
#### ps:这个图的画法，应该是看每个x值（或一个区间）对应的y值为1的比例。从这个图可以看出来，之所以用sigmoid根本原因是因为假设y|x服从sigmoid。
>It’s closer to being linear, but it’s still not quite there.  Instead of a linear relationship between X and P, we have a sigmoidal or S-shaped relationship.
>
>But it turns out that there are a few functions of P that do form reasonably linear relationships with X.  These include:
>
>1. Square root of arcsin
>2. Complimentary log-log
>3. Probit
>4. Logit
>
>The logit function is particularly popular because, believe it or not, its results are  relatively easy to interpret.  But many of the others work just as well.
>
>Once we fit this model, we can then back-transform the estimated regression coefficients off of a log scale so that we can interpret the conditional effects of each X.


![Image of logit](https://wikimedia.org/api/rest_v1/media/math/render/svg/534c475e08990aec6bb9a912a0be4a5e80b9dc94)


### 这个函数有什么优点和缺点？

>1. sigmoid 函数连续，单调递增
>
>2. p′=p∗(1−p)计算sigmoid函数的导数非常的快速
>
>--http://blog.csdn.net/a1628864705/article/details/62233395
>
>（ps：解释选择sigmoid的原因时提到了指数族，看不懂）


> 1. 他的输入范围是−∞→+∞ ，而值域刚好为（0，1），正好满足概率分布为（0，1）的要求。我们用概率去描述分类器，自然比单纯的某个阈值要方便很多； 
>
>　2. 他是一个单调上升的函数，具有良好的连续性，不存在不连续点。
>
>--http://blog.csdn.net/bitcarmanlee/article/details/51154481


缺点大概是在x很大或很小时梯度几乎为0，而当x维度很大时，很容易出现梯度近似为0的情况，梯度下降法就会收敛得很慢。

http://www.win-vector.com/dfiles/LogisticRegressionMaxEnt.pdf
http://www.win-vector.com/blog/2011/09/the-simpler-derivation-of-logistic-regression/
https://www.zhihu.com/question/35322351





http://www.stat.cmu.edu/~cshalizi/
http://fa.bianp.net/blog/2014/surrogate-loss-functions-in-machine-learning/
https://news.ycombinator.com/item?id=11712573


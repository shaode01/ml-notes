> K(x,y)=exp(−||x−y||^2/2p^2)
>
>Selecting a particular kernel type and kernel function parameters is usually based on application-domain knowledge and
may reflect distribution of input x values of 
the training data (Chapelle & Vapnik, 1999; Scho¨lkopf et al.,1999; Vapnik, 1998, 1999).For example, in this paper we show examples of SVM
regression using radial basis function (RBF) kernels where the RBF width parameter reflects the distribution/range of x-values of training
data.
>
>the kernel width parameter p is appropriately selected to reflect the input range of the training/test data. 
Namely, for univariate problems, RBF width parameter is set to p~(0.1–0.5)*range(x): For multivariate d-dimensional problems 
the RBF width parameter is set so that p^d ~(0.1–0.5) where all d input variables are prescaled to [0,1] range.
Such values yield good SVM performance for various regression data sets.

http://members.cbio.mines-paristech.fr/~jvert/svn/bibli/local/Cherkassky2004Practical.pdf
要选择kernel的类型和参数通常取决于领域知识，可能会反映训练数据集的分布。比如本文我们发现RBF的宽度参数p和训练数据集的分布有关。x是1维时，p的取值范围
为(0.1–0.5)*range(x)，多维时，先把所有维度归一化到0到1区间后，p的每一维取值范围为(0.1–0.5)。

这个问题与其说是问如何选择kernel，不如说是比较不同kernel的区别。
>Linear: K(x,y)=x^Ty
>
>Polynomial: K(x,y)=(x^Ty+1)^d
>
>Sigmoid: K(x,y)=tanh(ax^Ty+b)
>
>RBF: K(x,y)=exp(−γ||x−y||^2)
>Translation invariance: RBF kernel is the only kernel out of the above that is translation invariant, that is, K(x,y)=K(x+t,y+t), where t is any arbitrary vector. Intuitively, this property is useful — if you imagine all your data lying in some space, then the similarity between the points should not change if you shift the entire data, without changing the relative positions of the points.
>
>Inner product vs Euclidean distance: Related to the above point, RBF kernel is a function of the Euclidean distance between the points, whereas all other kernels are functions of inner product of the points. Again, it makes more intuitive sense to have Euclidean distance — points that are closer should be more similar. If two points are close to the origin, but on opposite sides, then the inner product based kernels assign the pair a low value, but Euclidean distance based kernels assign the pair a high value. It is, however, important to note that for some applications, inner product is sometimes the more preferred similarity metric, like in bag-of-words vectors, because you care more about the direction of the vectors (which words appear in both the document vectors) rather than the actual counts.
>
>Normalized: A kernel is said to be normalized if K(x,x)=1K(x,x)=1 for all xx. This is true for only RBF kernel in the above list. Again, intuitively, you want this property to hold — if xx and xx have a similarity of λλ, then 2x2x and 2x2x should also have a similarity of λλ. You can convert an arbitrary kernel K(x,y)K(x,y) to a normalized kernel K~(x,y)K~(x,y) by defining K~(x,y)=K(x,y)K(x,x)−−−−−−√K(y,y)−−−−−−√K~(x,y)=K(x,y)K(x,x)K(y,y). (Also, as a side note, RBF kernel is the normalized kernel for the exponential kernel, K(x,y)=exp(xTy)K(x,y)=exp⁡(xTy).)
>
>These properties tend to make RBF kernel better in general, for most problems. And because it does the best empirically, it tends to be most widely used. However, just to reiterate, depending on the nature of the problem, it is possible that one of the other kernels does better than RBF kernel.


https://www.quora.com/How-do-I-select-SVM-kernels/answer/Prasoon-Goyal
RBF核函数是唯一具有平移不变性

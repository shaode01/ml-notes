## 相同点
1. 都是分类算法
2. 原始问题都线性分类。
3. 都是监督学习
4. 都是判别模型
5. 都是应用广泛的。

>http://www.cnblogs.com/bentuwuying/p/6616761.html
## 不同点
1. 损失函数不同、假设不同、思路不同

逻辑回归的思路是基于概率的，有些教材比如李航的《统计学习方法》里面根本没有提到损失函数。SVM则是基于几何间隔最大化，李航的《统计学习方法》也没有提出明确的损失函数的概念，但观察原始问题引入拉格朗日乘数后的表达式，可以将其中与拉格朗日乘数相乘的部分看做损失函数，而前面的1/2||w||^2则可以看做正则项。
具体而言，当y∈{1,-1}时，逻辑回归的损失函数由上一篇可知是<img src="http://www.zhihu.com/equation?tex=log%281%2Bexp%28-y%3Cw%C2%B7x%3E%29%29" style="border:none;">，而SVM的损失函数则是Hinge损失函数：<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/56bbafa6e93ba741e6552b86f645f8ea9016e02d" style="border:none;">

2. 由于上述损失函数的不同，逻辑回归考虑所有点的损失，但离分类平面越远的点贡献的损失越小，影响越小；SVM只考虑误分类点的损失，对损失贡献最大的是少数几个支持向量。

3. 由于第2点，
>Linear SVM不直接依赖数据分布，分类平面不受一类点影响；LR则受所有数据点的影响，如果数据不同类别strongly unbalance一般需要先对数据做balancing。
>https://www.zhihu.com/question/26768865/answer/34048357

4. 
>Linear SVM依赖数据表达的距离测度，所以需要对数据先做normalization；LR不受其影响
>https://www.zhihu.com/question/26768865/answer/34048357
>
>http://117.143.109.163/cache/www.win-vector.com/dfiles/LogisticRegressionMaxEnt.pdf?ich_args2=162-11220514037202_4bebc1ff28017a95c7ebb16e20a79629_10001002_9c896429d6c0f9d6943c518939a83798_93ffac0a6aaf35ac00e5ce7393b09e4b

5.在软间隔SVM中，有一个超参数需要调参，误分类点的惩罚参数（李航的《统计学习方法》P109里的C值），而逻辑回归没有这种超参数。

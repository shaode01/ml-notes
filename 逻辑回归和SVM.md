## 相同点
1. 都是分类算法
2. 原始问题都线性分类。
3. 都是监督学习
4. 都是判别模型
5. 都是应用广泛的。
## 不同点
1. 损失函数不同、假设不同、思路不同

逻辑回归的思路是基于概率的，有些教材比如李航的《统计学习方法》里面根本没有提到损失函数。SVM则是基于几何间隔最大化，有明确的损失函数的概念。
具体而言，当y∈{1,-1}时，逻辑回归的损失函数由上一篇可知是<img src="http://www.zhihu.com/equation?tex=log%281%2Bexp%28-y%3Cw%C2%B7x%3E%29%29" style="border:none;">，而SVM的损失函数则是Hinge损失函数：<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/56bbafa6e93ba741e6552b86f645f8ea9016e02d" style="border:none;">



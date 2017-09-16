1. GBDT和xgboost都是梯度提升算法。区别只在一些模型的细节上。
2. 传统GBDT以CART作为基分类器，xgboost还支持线性分类器
3. 传统GBDT在优化时只用到一阶导数信息，xgboost则对代价函数进行了二阶泰勒展开
4. xgboost可以支持不同的loss functions，来优化效果，只要函数可一阶和二阶求导。
5. xgboost在代价函数里加入了正则项，将树模型的复杂度作为正则项。
6. 列抽样（column subsampling）。xgboost借鉴了随机森林的做法
7. 寻找最佳分割点时，考虑到传统贪心法效率比较低，实现了一种近似贪心法，除此之外还考虑了稀疏数据集、缺失值的处理，这能大大提升算法的效率。
8. xgboost工具支持在进行节点的分裂时并行计算各个特征的增益
9. data事先排好序并以block的形式存储，利于并行计算
10. GBDT采用的是数值优化的思维, 用的最速下降法去求解Loss Function的最优解, 其中用CART决策树去拟合负梯度, 用牛顿法求步长。XGboost用的解析的思维, 对Loss Function展开到二阶近似, 求得解析解, 用解析解作为Gain来建立决策树, 使得Loss Function最优.。


https://en.wikipedia.org/wiki/Gradient_boosting
http://blog.csdn.net/shenxiaoming77/article/details/51542982
http://odjt9j2ec.bkt.clouddn.com/xgboost-xgboost%E5%AF%BC%E8%AF%BB%E5%92%8C%E5%AE%9E%E6%88%98.pdf

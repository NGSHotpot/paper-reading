## 前言  

我们之前介绍过一些针对scRNA-seq设计的聚类算法，例如（Nature Methods简报：使用SC3对single cell RNA-seq数据进行聚类分析）， 然而此类算法一般需要经过多次迭代从而得到比较稳定的结果，所以分析会比较慢。此外scRNA-seq数据特征常有的一类状态是dropouts，即含有大量0或者接近0的counts （可能是由于扩增过程中的失败），这也会极大地影响聚类结果。CIDR (Clustering through Imputation and Dimensionally Reduction) [1] 就是一个针对dropouts进行填补(imputation)然后进行降维后的快速聚类算法，感觉上应该会比较适合样本特别多的情况。可能不单单针对scRNA试用，大规模的个人RNA-seq数据（variation目测也不小）应该也可以借用其imputation模型，假设都很试用，但是应该需要调一些参数。   

CIDR：https://github.com/VCCRI/CIDR



## 算法思想   

令$C_{i}=(o_{1,i},o_{2,i},...,o_{n,i})$和$C_{j}=(o_{1,j},o_{2,j},...,o_{n,j})$为两个细胞中的基因表达向量，则可衡量其距离如下，即可分成三部分，都是非dropouts的基因距离，含有一个dropouts的和都是dropouts的：

$ [D(C_{i},C_{j})]^{2} = \sum_{k}^{n} (o_{k,i}-o_{k,j})^{2} = \sum_{k \in noDropouts} (o_{k,i}-o_{k,j})^{2} +\sum_{k \in bothDropouts} (o_{k,i}-o_{k,j})^{2} + \sum_{k \in oneDropouts} (o_{k,i}-o_{k,j})^{2}$

所以，影响样本聚类就是这种oneDropouts的情况，然后根据已知的情况，越是表达量低的基因越有可能称为dropouts, 所以可以根据这个来对dropouts和表达量建个model，来补齐dropouts，得到上面值的dissimilarity matrix。然后，应用我们在sklearn: k-means提过的，先PCA，选前几个components然后再聚类，这一步，当然很快。



## 在模拟数据中的应用 

如下，和比较常用的直接PCA，t-SNE, ZIFA RaceID等比较，看上去是好了不少，其中的评价指标Adjusted Rand Index我们在（sklearn: 聚类性能评估）中提过。


## 在真实数据中的应用   

如下，感觉上依旧好了许多。




## Reference 

1. Lin, P., Troup, M. & Ho, J.W.K. CIDR: Ultrafast and accurate clustering through imputation for single-cell RNA-seq data. Genome Biology 18, 59 (2017).


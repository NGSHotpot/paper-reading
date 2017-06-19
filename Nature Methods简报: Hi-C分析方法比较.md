## 前言   

Hi-C分析中经典的一步就是call TADs，参考文献[1]比较了几种算法，包括了准确度，运行时间以及计算需求。  NGS Hotpot这里选取一些自己关注的指标当作note记录一下。



## 所比较的算法   





## interactions level comparasion 

Hi-C数据不同的算法找到的比较小的interactions大概长下面这样（不同颜色的marks），看上去很小，但是应该也有好几个bins，而一个bins是根据分辨率设成了5kb或40kb，看看其坐标轴觉得应该也好大。



作者用额外不同的数据，例如3C,5C,ChIA-PET来验证一下用不同算法找到的interactions的可靠度，结果如下，点的大小代表找到的interactions里能用不同数据验证的百分比，颜色代表找到的interactions的数量，40kb分辨率的Hi-C数据用灰色mark了一下。整体上来看GOTHiC不错，同时根据文章的另一张图看来replicates之间的reproducity，GOTHiC也不错，但是其有可能也是由于call到的大部分interactions



## TADs level comparasion 

NGS Hotpot之前有点觉得得到TADs的算法有点tricky , 有比较多的cutoff需要定义，然后看了这里的比较，更加明确了有点tricky。。。同样的数据找到的东西差别好大。。。。例如下面



然后replicates之间的reproducity也好搓，如下


## 结语  

看来这个领域的算法还有些许砖需要搬。。。。



## Reference  

1.	Forcato, M. et al. Comparison of computational methods for Hi-C data analysis. Nat Meth advance online publication (2017).

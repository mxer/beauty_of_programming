beauty_of_programming
=======================================================================================================================
1，
=======================================================================================================================






2,
=======================================================================================================================








3,一堆烙饼的排序
=======================================================================================================================
当烙饼不多的时候，我们可以很快的找出最优的翻转方案就是程序中的上界(UpperBound)，也就是说我们感兴趣的最优方案最少
也就是上面方案，那如何能找到更好的优化方案？
程序当中有个剪枝部分：
nEstimate=lowerBound(m_ReverseCakeArray,m_n)
if(step+nEstimate>m_nMaxSwap)
			return;
当m_nMaxSwap越小，剪枝条件就越容易满足,更多的情况就不用去搜索
分析：当nEstimate越大，剪枝条件就越容易满足，也就是说nEstimate越大，nMaxSwap越小，满足的条件就越小，就越容易找到最优化
解，所以在程序中必须体现尽可能减少UpperBound，增加LowerBound，从而减少要搜索的空间。
程序的上界为2*(n-1)，那么程序的下届如何估计呢：
每一次翻转，我们最多使得一个烙饼与大小相邻的烙饼排到一起。如果当前n个烙饼中，有m对相邻的烙饼半径不想了，那么我们至少需
要m次才能排好序。程序中通过遍历相邻的两个烙饼，尺寸上是否相邻来进行最小界的估计

4,买书问题（如何买书最便宜，连续买几本不同的折扣高）
=======================================================================================================================
利用动态规划解决问题，多条件递归进程处理，最后比较哪种方式的价格最低
这里把买书问题看作一个动态规划问题，状态转移方程为：
F(Y1,Y2,Y3,Y4.Y5)=0  if(Y1=Y2=Y3=Y4=Y5=0)
or F(Y1,Y2,Y3,Y4,Y5)=min{5*8*(1-25%)+F(Y1-1,Y2-1,Y3-1,Y4-1,Y5-1),
 4*8*(1-20%)+F(Y1-1,Y2-1,Y3-1,Y4-1,Y5),
 3*8*(1-10%)+F(Y1-1,Y2-1,Y3-1,Y4,Y5),
 2*8*(1-5%)+F(Y1-1,Y2-1,Y3,Y4,Y5),
 8+F(Y1-1,Y2,Y3,Y4,Y5)}





5，快速找出机器故障（找出双备份记录中仅出现一次的某个数）
=======================================================================================================================
算法核心原理：一个数和其本身的异或为0，具体情况见代码包括丢失两个记录（两个相同与两个不同）
这次代码中注释很详细，忘了的话可以看看代码


6，饮料供货（代码来自CSDN某博友ps：他的代码有点小错误）
=======================================================================================================================
在饮料总量限定的情况下，如何找到总满意度最大的一种选择，如果能列出推导公式，那么利用动态规划将很轻松就能解决







7，光影切割问题
=======================================================================================================================
光影切割部分问题能够够根据直线条数和交点数目改变成为更具比较简单的问题：
如果有N条直线，其中有M个交点，那么分块区域的数目为N+M+1
故我们只需要求N条直线M个焦点的情况，根据《编程之美》P51中图1-13所示，交点的个数就转换成了如何求一个N个元素的数组的逆序数
求逆序数时间复杂度较低的算法是采用分冶的思想，首先求N/2个元素的逆序数然后求后N/2个逆序数，最后在排序过程中合并前后两部分
的逆序数。
逆序数的求法参见这篇博文：http://blog.csdn.net/dlengong/article/details/7594919



8，电梯调度算法
=======================================================================================================================
电梯每次载满乘客后只在某一层停留，剩余的需要自己走楼梯，如何保证走楼梯的总数目最小
分析：假设有N1个乘客在i层以下，N2个乘客在i层，N3个层客在i层以上，那么假如我选择在i-1层停，那么比i层停多走的层数为N2+N3-N1
如果选择在i+1层停，那么比i层夺走的层数为N1+N2-N3。比较两者多走的大小，易知何时选择上升合适，何时选择下降合适。
代码可以从这方面着手，我们从第一层开始，得到某层以上的人数，某层所在人数，某层以上人数然后通过上述所述策略来判断是否上升
直到第一次不再上升即找到了合适的层数来保证所有人数走的层数最少。

9,高效地安排见面会
=======================================================================================================================
1，寻找可以同时召开的会议，来进一步减少花费的时间：
这个问题可以转换为图的最少着色问题：
a,将两个不能同时召开的回忆，用同一条直线进行连接
b,然后对每个顶点进行着色，保证有直线连接的两个节点不许重色

2，面试的时候，每次会面会有一个开始时间，一个结束时间，现在有一组2面试时间数据，要求每一个有冲突的时间，都不允许安排
在同一地点，求出最小需要安排的地点数目
分析:对所有面试按开始时间从小到大进行排序，然后按照顺序对各个空间着色，对当前某区间着色时，
必须保证所着的颜色没有出现在这个区域之前且时间段与当前区间有重叠的区间
一种优化算法：将所有的开始时间和结束时间共同参与艾许得到一个长度为2*N的有序数组
遍历数组，当时间类型为开始时间，则使用颜色加1，如果是结束时间，则使用颜色减1，（这里还不是弄的很明白）


10,双线程高效下载
=======================================================================================================================






11,求二进制数中1的个数
=======================================================================================================================
算法1：二进制数对2求余，如果余为0则该位上为0，为1则该位为1，然后二进制数除以2然后判断第2位直到数为0
算法2：类似于算法1但是由于求余和除以2操作相对于位操作更复杂，可以使用向右移位代替除以2，与00000001求与来判断该位是否为1
算法3：位操作相比除以和求余效率高了很多，但是时间复杂度仍为O(log2v)，那是否能够每次判断中仅与1来判断，则复杂度与1的个数有关
综上所述，我们进行v&=v-1操作，例如数为00010110&00010101=00010100，继续知道其中变为00000000，次数为其中1的个数有关。
算法4和算法5类似：都是采用空间换时间，在O(1)时间能判断出来，算法4采用分支结构，将所有分支都写出来判断，算法5采用查表法，
创建一个表，index为数，内容为1的个数，也可以在O(1)时间判断1的个数


12，不要被阶乘吓到
=======================================================================================================================
给定一个整数N，1，如何求N的阶乘N！末尾有几个0？
2，求N！的二进制表示中最低位1的位置
针对问题1，我们不可能先算法N！，因为很有可能会有溢出分析如果N！=K×10^M，且K不能被10整除，那么N！末尾有M个0，考虑对N！进行
因式分解，由于10=2×5，所以M的数目只与2和5的个数有关，M=min(X,Z)(X,Z表示因式分解中2的次数，5的次数)，易知，X肯定大于或者等于Z
故综上M=Z。
而Z的计算与11中1的个数的算法1类似。
这里我们将有另一种算法通过公式：Z=[N/5]+[N/25]+[N/5^3]...来表示N！中质因数5的个数

问题2分析即为其中含质因数2的个数同理根据公式Z=[N/2]+[N/2^2]+...既可以计算N！中质因数2的个数
另外一种算法：根据公式：N！含有质因数2的个数还等于N减去N的二进制中1的个数


13,寻找水王
========================================================================================================================
如何快速有效地在找出消息列表中发帖超过一半的那个ID？
一开始想到的办法无非是对列表进行排序，然后统计次数或者寻找第N/2个ID即为超过一半的，但是这两种办法都需要先对ID列表进行排序
有没有不进行排序的算法呢？
我们可以这样，每次删除两个不同的ID，很显然剩下的ID列表中，“水王”ID出现的次数仍然超过总数的一半，一直重复这个过程，把ID列表
内的总数降低即可以转换为更小的问题，从而得到答案



14，查找1到N中1出现的次数
=========================================================================================================================
算法描述：每一位上出现1的情况分为三类：1，该位数字为0，该位上出现1的次数由更高为决定，例如12013中百位出现1的情况为12×100=1200
2，该位数字为1不仅受高位影响还受低位影响例如12113中百位出现1的情况数目是12×100=1200，还包括12100-12113一种114个即113+1
3，如果该位上数字大于1，那么百位上可能出现1的次数由更高位决定为：（12+1）×100


15,寻找最大的k个数
=========================================================================================================================
算法1：使用快速排序或者堆排序，他们的时间复杂度都是O(N*log2N)，然后取出前K个，总时间复杂度为O(N*log2N)+O(K)=O(N*log2N)，另外
也可使用部分排序，例如选择排序，交换排序只需要把N个数中前K个数排序出来，复杂度是O(N*K)，哪一个更好，取决于K与log2N的比较。
算法2：和快速排序类似，在快速排序中，每一步都是将待排序数组分为两组，其中一组数据的人任何一个数都比另一组的任意数达，再对两组
分别做类似操作：假设N个数存储在数组S中，从数组S中随机找出一个元素X，把数组分为Sa和Sb。Sa中的元素大于等于X，Sb中的元素小于X。
故存在两个可能：a,Sa中元素的个数小于K，Sa中所有的数和Sb中最大的K-|Sa|个元素就是数组S中最大的K个数；b，Sa中元素的个数大于或等于K
，则需要返回Sa中最大的K个元素。
算法3：寻找N个数中最大的K个数，本质上就是寻找最大的K个数中最小的那个，也就是第K大的数。这里可以使用二分搜索的策略。对于一个给定的
数p，可以在O(N)的时间复杂度内找出所有不小于p的数。
算法4：上面三个算法虽然能够解决，时间复杂度增加也很正常，但是个哦南通的地方是需要对数据进行对此访问，但N足够大的时候，比如100e？
这个时候数据不能完全的装入内存，为了解决这方面的问题，可以使用最小堆的方法，最小堆容量为K，最小堆的堆顶元素就是这K个元素中最小的，
遍历N个数据，如果X比堆顶小，那么替换堆顶元素，然后更新堆来维持堆的性质，更新的过程的时间复杂度为O(log2K)。(要看书再次深刻地了解
最大堆和最小堆的关系，以及如何实现)
算法5：如果所有N个数都是正整数，且他们的取值范围不大，可以考虑申请空间，记录每个整数出现的次数，然后从大到小去最大的K个。比如所有
整数都在(0,MAXN）区间中的话，利用一个数组count[MAXN]来记录每个整数出现的个数(count[i]表示整数i在所有整数中出现的个数)。我们只需要
扫描一遍就可以得到count数组，然后找到第K大的元素。


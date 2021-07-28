# 排序

⌚️:2020年11月30日

📚参考

---

- 冒泡排序（Bubble Sort）
- 插入排序（Insertion Sort）
- 希尔排序（Shell Sort）
- 选择排序（Selection Sort）
- 快速排序（Quick Sort）
- 归并排序（Merge Sort）
- 堆排序（Heap Sort）
- 计数排序（Counting Sort）
- 桶排序（Bucket Sort）
- 基数排序（Radix Sort）

## 希尔排序

希尔排序是希尔（Donald Shell）于1959年提出的一种排序算法。希尔排序也是一种插入排序，它是简单插入排序经过改进之后的一个更高效的版本，也称为缩小增量排序，同时该算法是冲破O(n2）的第一批算法之一。本文会以图解的方式详细介绍希尔排序的基本思想及其代码实现。

### 基本思想

> 　　　　**希尔排序是把记录按下标的一定增量分组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的关键词越来越多，当增量减至1时，整个文件恰被分成一组，算法便终止。**

　　简单插入排序很循规蹈矩，不管数组分布是怎么样的，依然一步一步的对元素进行比较，移动，插入，比如[5,4,3,2,1,0]这种倒序序列，数组末端的0要回到首位置很是费劲，比较和移动元素均需n-1次。而希尔排序在数组中采用跳跃式分组的策略，通过某个增量将数组元素划分为若干组，然后分组进行插入排序，随后逐步缩小增量，继续按组进行插入排序操作，直至增量为1。希尔排序通过这种策略使得整个数组在初始阶段达到从宏观上看基本有序，小的基本在前，大的基本在后。然后缩小增量，到增量为1时，其实多数情况下只需微调即可，不会涉及过多的数据移动。

　　我们来看下希尔排序的基本步骤，在此我们选择增量gap=length/2，缩小增量继续以gap = gap/2的方式，这种增量选择我们可以用一个序列来表示，{n/2,(n/2)/2...1}，称为**增量序列**。希尔排序的增量序列的选择与证明是个数学难题，我们选择的这个增量序列是比较常用的，也是希尔建议的增量，称为希尔增量，但其实这个增量序列不是最优的。此处我们做示例使用希尔增量。

![img](imgs/1024555-20161128110416068-1421707828.png)

### 代码实现

　　在希尔排序的理解时，我们倾向于对于每一个分组，逐组进行处理，但在代码实现中，我们可以不用这么按部就班地处理完一组再调转回来处理下一组（这样还得加个for循环去处理分组）比如[5,4,3,2,1,0] ，首次增量设gap=length/2=3,则为3组[5,2] [4,1] [3,0]，实现时不用循环按组处理，我们可以从第gap个元素开始，逐个跨组处理。同时，在插入数据时，可以采用元素交换法寻找最终位置，也可以采用数组元素移动法寻觅。希尔排序的代码比较简单，如下：



```
/***************************************************************************
 *  @file       main.cpp
 *  @author     MISAYAONE
 *  @date       27  March 2017
 *  @remark     27  March 2017 
 *  @theme      Shell Sort 
 ***************************************************************************/
 
#include <iostream>
#include <vector>
#include <time.h>
#include <Windows.h>
using namespace std;
 
void Shell_sort(int a[],size_t n)
{
	int i,j,k,group;
	for (group = n/2; group > 0; group /= 2)//增量序列为n/2,n/4....直到1
	{
		for (i = 0; i < group; ++i)
		{
			for (j = i+group; j < n; j += group)
			{
				//对每个分组进行插入排序
				if (a[j - group] > a[j])
				{
					int temp = a[j];
					k = j - group;
					while (k>=0 && a[k]>temp)
					{
						a[k+group] = a[k];
						k -= group;
					}
					a[k] = temp;
				}
			}
		}
	}
}
 
int main(int argc, char**argv)
{
	int a[10] = {1,51,6,2,8,2,564,1,65,6};
 
	Shell_sort(a,10);
	for (int i = 0; i < 10; ++i)
	{
		cout<<a[i]<<" ";
	}
	cin.get();
	return 0;
}


```

### 总结

　　本文介绍了希尔排序的基本思想及其代码实现，希尔排序中对于增量序列的选择十分重要，直接影响到希尔排序的性能。我们上面选择的增量序列{n/2,(n/2)/2...1}(希尔增量)，其最坏时间复杂度依然为O(n2)，一些经过优化的增量序列如Hibbard经过复杂证明可使得最坏时间复杂度为O(n3/2)。希尔排序的介绍到此为止，关于其他排序算法的介绍也会陆续更新，谢谢支持。

## 插入排序

*插入排序（Insertion-Sort）*的算法描述是一种简单直观的排序算法。打过扑克牌的应该都会明白（当然，如果你说你打扑克牌摸牌的时候从来不按牌的大小整理牌，那我只能呵呵了）

### 1. 基本思想

插入排序的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。插入排序在实现上，通常采用in-place排序（即只需用到O(1)的额外空间的排序），因而在从后向前扫描过程中，需要反复把已排序元素逐步向后挪位，为最新元素提供插入空间。

趣味解释：

![img](imgs/v2-91dc753e1ddc5348eafd57ab24a8bab6_720w.png)

插入排序操作类似于摸牌并将其从大到小排列。每次摸到一张牌后，根据其点数插入到确切位置。

如上图：表示的是摸到草花7后进行插入的过程。忽略最右边的草花10，相当于一开始7在最右边，然后逐个与左边的排相比较(当然左边的牌早已排好顺序)，将其放置在合适的位置。当摸到草花10后重复上述过程即可。

而实际中，如何将插入牌的这个过程应用到实际排序操作中呢？具体我们以一组数字来说操作说明：

![img](imgs/v2-8de71a6d88ccc5754deb89d58bcc8800_720w.png)

例如我们有一组数字：｛5，2，4，6，1，3｝，我们要将这组数字从小到大进行排列。 我们从第二个数字开始，将其认为是新增加的数字，这样第二个数字只需与其左边的第一个数字比较后排好序；在第三个数字，认为前两个已经排好序的数字为手里整理好的牌，那么只需将第三个数字与前两个数字比较即可；以此类推，直到最后一个数字与前面的所有数字比较结束，插入排序完成。

### 2. 实现逻辑

> ① 从第一个元素开始，该元素可以认为已经被排序
> ② 取出下一个元素，在已经排序的元素序列中从后向前扫描
> ③如果该元素（已排序）大于新元素，将该元素移到下一位置
> ④ 重复步骤③，直到找到已排序的元素小于或者等于新元素的位置
> ⑤将新元素插入到该位置后
> ⑥ 重复步骤②~⑤

### 3. 动图演示

![img](imgs/v2-91b76e8e4dab9b0cad9a017d7dd431e2_b.png)

### **4**. 性能分析

> 平均时间复杂度：O(N^2)
> 最差时间复杂度：O(N^2)
> 空间复杂度：O(1)
> 排序方式：In-place
> 稳定性：稳定

如果插入排序的目标是把n个元素的序列升序排列，那么采用插入排序存在最好情况和最坏情况：

> (1) 最好情况：序列已经是升序排列，在这种情况下，需要进行的比较操作需(n-1)次即可。
> (2) 最坏情况：序列是降序排列，那么此时需要进行的比较共有n(n-1)/2次。

插入排序的赋值操作是比较操作的次数减去(n-1)次。平均来说插入排序算法复杂度为O(N^2)。

最优的空间复杂度为开始元素已排序，则空间复杂度为 0；

最差的空间复杂度为开始元素为逆排序，则空间复杂度最坏时为 O(N);

平均的空间复杂度为O(1)

```text
注：
n：数据规模
k：”桶”的个数
In-place：占用常数内存，不占用额外内存
Out-place：占用额外内存
```

### 5. 代码实现

```cpp
// 插入排序
void InsertSort(int arr[], int len){
    // 检查数据合法性
    if(arr == NULL || len <= 0){
        return;
    }
    for(int i = 1; i < len; i++){
        int tmp = arr[i];
        for(int j = i-1; j >= 0; j--){
            //如果比tmp大把值往后移动一位
            if(arr[j] > tmp){
               arr[j+1] = arr[j];
            }
            else{
               break;
            }
        }
        arr[j+1] = tmp;
    }
}
```

### 6. 算法优化改进

#### 6.1 改进方法①

场景分析： 

直接插入排序每次往前插入时，是按顺序依次往前查找，数据量较大时，必然比较耗时，效率低。

改进思路： 在往前找合适的插入位置时采用二分查找的方式，即折半插入。

二分插入排序相对直接插入排序而言：平均性能更快，时间复杂度降至O(NlogN)，排序是稳定的，但排序的比较次数与初始序列无关，相比直接插入排序，在速度上有一定提升。逻辑步骤：

> ① 从第一个元素开始，该元素可以认为已经被排序
> ② 取出下一个元素，在已经排序的元素序列中二分查找到第一个比它大的数的位置
> ③将新元素插入到该位置后
> ④ 重复上述两步

改进代码：

```cpp
// 插入排序改进：二分插入排序
void BinaryInsertSort(int arr[], int len)   
{   
    int key, left, right, middle;   
    for (int i=1; i<len; i++)   
    {   
        key = a[i];   
        left = 0;   
        right = i-1;   
        while (left<=right)   
        {   
            middle = (left+right)/2;   
            if (a[middle]>key)   
                right = middle-1;   
            else   
                left = middle+1;   
        }   

        for(int j=i-1; j>=left; j--)   
        {   
            a[j+1] = a[j];   
        }   

        a[left] = key;          
    }   
}
```

#### 6.2 改进方法②

场景分析： 

(1) 插入排序对几乎已排好序的数据操作时，效率很高，可以达到线性排序的效率。 

(2) 插入排序在每次往前插入时只能将数据移动一位，效率比较低。

改进思路： 

先将整个待排元素序列分割成若干个子序列（由相隔某个“增量”的元素组成的）分别进行直接插入排序，然后依次缩减增量再进行排序，待整个序列中的元素基本有序（增量足够小）时，再对全体元素进行一次直接插入排序。

改进思路二的方法实际上就是希尔排序。在这里只给出思路，在后续系列《算法：排序算法之希尔排序》中再做具体讲解说明。

------

### 7. 总结

插入排序不适合对于数据量比较大的排序应用。但是，如果需要排序的数据量很小，例如，量级小于千，那么插入排序还是一个不错的选择。尤其当数据基本有序时，采用插入排序可以明显减少数据交换和数据移动次数，进而提升排序效率。 在STL的sort算法和stdlib的qsort算法中，都将插入排序作为快速排序的补充，用于少量元素的排序。

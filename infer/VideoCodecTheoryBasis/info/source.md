# 第二章 离散信源

⌚️:2020年11月30日

📚参考

---



信源是信息的发源地，研究内容主要为信源输出的信息量。   
使用自信息将信息和概率联系起来,提供某个随机事件的信息量。   
信源是随机出现的消息的集合（概率空间）。   

## TREE
* 离散信源的信息熵
* 熵的基本性质
* 信源的相关性与剩余度
## 一、离散信源的信息熵
### 1.信源的数学模型及分类
![](../imgs/36.png)  
![](../imgs/37.png)   
![](../imgs/38.png)  
![](../imgs/39.png)   

为什么会出现熵？
![](../imgs/40.png)   
如果信源输出的是a1，则I（a1）=log(1/0.99).   
如果信源输出的是a2，则I（a2）=log（1/0.01).   
可以看到，使用自信息度量信源会出现差错。因为自信息是随机变量。所以不能用自信息来表示一个固定的信源。      

### 2.信息熵
![](../imgs/41.png)   
用信息熵来度量信源。   
![](../imgs/42.png)   
![](../imgs/44.png)  
熵是平均自信息。 自信息表示事件的不确定性，难易程度。    
![](../imgs/43.png)   

### 3.联合熵与条件熵
![](../imgs/45.png)   

![](../imgs/46.png)   
![](../imgs/47.png)  


![](../imgs/48.png)   
![](../imgs/49.png)  

什么情况下用联合熵和条件熵？    
![](../imgs/50.png)   
## 二、熵的基本性质
![](../imgs/55.png)   
![](../imgs/56.png)   
![](../imgs/57.png)   
![](../imgs/58.png)   
![](../imgs/59.png)   
![](../imgs/60.png)   
## 三、信源的相关性与剩余度
![](../imgs/61.png)   
![](../imgs/62.png)   
熵的极值性（上图画红线的），对于一个离散无记忆信源来说，当信源在等概分布的时候，它的熵值达到了最大。当信源是有记忆的时候，条件作用使熵减少，也就是说，随着我已知的相关联的这种条件符号数目越多，熵值越小。   

从上面的关系链中可以看到，同样考察比如有Q个消息符号的信源，那么这个信源，平均每个符号最大能携带的信息量为多少？    
理想是：logq    
实际是：H无限大   
![](../imgs/63.png)   

![](../imgs/64.png)   
H0是各个信号不与其他内容相关，H1~无穷大是不同的约束，会使字母表达出的内容更像一段话。   


![](../imgs/65.png)   
![](../imgs/66.png)   

![](../imgs/67.png)   

### 关于信源剩余度的思考：
#### 1.为提高信息传输效率，总希望减少剩余度。    
例如：中华人民共和国——压缩成“中国”    
**提高信源输出信息的效率：信源压缩**   

#### 2.为提高信息传输可靠性，需要一定的剩余度。（剩余度存在可以加强我们对语句的理解）
例如：发送“中国”错成“X国”    
发送“中华人民共和国”错成“中X人民X和国”   
**提高信息传输可靠性：信道编码**   

![](../imgs/68.png)   
从这样的一个关系链中， 理想情况下，我希望信源每输出一个符号携带的信息量能达到LogQ，但是在实际中在H无穷大。    

所以，我希望通过信源编码，将这个信源输出的结果，让熵值往右走，提高效率，减少信源剩余度。   

![](../imgs/69.png)   
方式1：减少相关性；   
方式2：均匀每个信号的概率。   
典型应用：预测编码,变换编码。   
![](../imgs/70.png)   
压缩的思想是将相关部分和无相关部分（误差）分开。   
![](../imgs/71.png)   
![](../imgs/72.png)   
![](../imgs/73.png)  
典型应用：统计编码   
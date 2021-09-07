

# WGAN

⌚️: 2021年8月30日

📚参考

- https://www.bilibili.com/video/BV1Ct4y1a7eL?from=search&seid=13526832707490502743
- https://www.bilibili.com/video/BV1K4411d7Wc?from=search&seid=9857597314064653129



---

## 一、WGAN

![image-20210830164832526](imgs/image-20210830164832526.png)

### 1. GAN的局限性

![image-20210830164944257](imgs/image-20210830164944257.png)

![image-20210830165154779](imgs/image-20210830165154779.png)

![image-20210830165408725](imgs/image-20210830165408725.png)



![image-20210830165516967](imgs/image-20210830165516967.png)



#### 1.1 模式崩塌

#### ![image-20210830165741914](imgs/image-20210830165741914.png)

![image-20210830165908651](imgs/image-20210830165908651.png)

![image-20210830165945978](imgs/image-20210830165945978.png)



#### 1.2 过生成

![image-20210830170111772](imgs/image-20210830170111772.png)

![image-20210830170235516](imgs/image-20210830170235516.png)

![image-20210830170253444](imgs/image-20210830170253444.png)

#### 1.3 梯度消失

![image-20210830170607017](imgs/image-20210830170607017.png)

![image-20210830170733507](imgs/image-20210830170733507.png)

![image-20210830170835791](imgs/image-20210830170835791.png)

![image-20210830170942748](imgs/image-20210830170942748.png)

分布一样为1，分布不一样为0，只能判断两个分布是否相似，但是不能判断程度。

#### 1.4 Mode Dropping

![image-20210901154736642](imgs/image-20210901154736642.png)

### 2. WGAN

![image-20210830171113266](imgs/image-20210830171113266.png)

![image-20210830171439547](imgs/image-20210830171439547.png)

![image-20210830171511566](imgs/image-20210830171511566.png)

![image-20210830171613802](imgs/image-20210830171613802.png)

![image-20210830171711784](imgs/image-20210830171711784.png)

![image-20210830171842077](imgs/image-20210830171842077.png)

![image-20210901151332825](imgs/image-20210901151332825.png)



1-L限制条件的实现有很多种，下面的图展示了原来WGAN和WGAN-GP的实现原理

![image-20210901151809724](imgs/image-20210901151809724.png)

![image-20210830171950750](imgs/image-20210830171950750.png)

![image-20210830172116317](imgs/image-20210830172116317.png)

神经网络函数有很多不满足1-L条件，所以梯度裁剪是解决方式之一。

### 3. WGAN-GP

clip范围需要自己设定，而且很难设置，所以有了WGAN-GP

![image-20210830172506988](imgs/image-20210830172506988.png)

![image-20210830172516909](imgs/image-20210830172516909.png)

![image-20210830172652739](imgs/image-20210830172652739.png)

![image-20210830172737627](imgs/image-20210830172737627.png)

![image-20210830173040055](imgs/image-20210830173040055.png)

![image-20210830173113242](imgs/image-20210830173113242.png)

![image-20210830173200067](imgs/image-20210830173200067.png)

## 二、WGAN实现

![image-20210830173557486](imgs/image-20210830173557486.png)

![image-20210830173557486](imgs/image-20210830164458757.png)

![image-20210830174042772](imgs/image-20210830174042772.png)

![image-20210830174446621](imgs/image-20210830174446621.png)

![image-20210830174506938](imgs/image-20210830174506938.png)

![image-20210830174530389](imgs/image-20210830174530389.png)

![image-20210830174638333](imgs/image-20210830174638333.png)

![image-20210830174807793](imgs/image-20210830174807793.png)

![image-20210830174905100](imgs/image-20210830174905100.png)

![image-20210830175129708](imgs/image-20210830175129708.png)

![image-20210830175233265](imgs/image-20210830175233265.png)

![image-20210830175257955](imgs/image-20210830175257955.png)

![image-20210830175523529](imgs/image-20210830175523529.png)



---
title: 神经网络算法初学
tags:
  - C语言
  - 神经网络
  - 人工智能
date: 2023-12-20 21:58:32
draft: false
hideInList: false
isTop: false
feature:
---
# 神经网络算法

## 需求分析

众所周知，人类一直在寻找一种模拟人思维的方法，神经网络算法就是一种基于生物神经系统的原理，利用计算机实现人工智能的技术。神经网络算法的目的是通过构建多层的神经元模型，实现对复杂数据的学习、分类、预测等功能。

![机器学习初学：神经网络原理 + Python 简单实例](https://s2.loli.net/2023/12/20/U6n1k2vWiM9gzjc.png)

首先，我们必须介绍一下神经元（neuron），也就是组成神经网络的基本单元。一个神经元可以接受一个或多个输入，对它们做一些数学运算，然后产生一个输出。下面是一个 2 输入的神经元模型：

这个神经元中发生了三件事。首先，每个输入（$x_1$, $x_2$）会分别乘以一个**权重值**$w$（weight）：
$$
x_1\to x_1*w_1\\
x_2\to x_2*w_2
$$
接下来，所有乘以了权重的输入将相加，并且再加上一个**偏移量** $b$（bias）：
$$
(x_1*w_1)+(x_2*w_2)+b
$$
最后，这个最终相加的值还要再通过一个**激活函数**（activation function）：
$$
y = f((x_1*w_1)+(x_2*w_2)+b)
$$


激活函数用来将那些无边界的输入转化成一组良好的，可预测的输出形式。一种常用的激活函数是 **Sigmoid** 函数：![img](https://s2.loli.net/2023/12/20/u2XZlQCqJiH3tsb.webp)

神经网络说白了就是通过不断训练，让预测值与真实值越来越接近的函数**（BP反向传播）** 分类神经网络

这里我们通过设计一个简单的 **根据身高体重判断性别** 的神经网络实例来理解神经网络。

## 概要设计

神经网络算法的基本组成部分是神经元，每个神经元接收多个输入信号，经过激活函数处理后，输出一个信号。神经元之间通过权重连接，形成一个网络结构。神经网络算法的核心问题是如何确定每个连接的权重，使得网络能够达到期望的输出。一般来说，这需要通过训练数据来进行学习和调整。

### 本程序主要由以下函数构成:

![image-20231220162340455](https://s2.loli.net/2023/12/20/yLKzHBrhom5s69Z.png)

## 详细设计

神经网络算法有多种类型和结构，根据不同的应用场景和需求，可以选择合适的模型。常见的神经网络算法有：

- 前馈神经网络：最简单的一种结构，只有输入层、输出层和若干隐藏层，每层之间只有单向的连接，没有反馈或循环。前馈神经网络可以用于回归、分类等问题。

#### double sigmoid(double x)

激活函数 用于隐层神经元输出，取值范围为 (0,1)，它可以将一个实数映射到 **(0,1)**的区间，可以用来做二分类。

返回一个double值 介于(1,0)之间

#### double deriv_sigmoid(double x)

激活函数的导数 用于后面计算偏导数

返回激活函数的导数

#### double mess_loss(double* y_true,double* y_pred,int size)

损失函数，将预测值与真实值进行相减并取它们的平方乘以size分之一

返回 $\frac{1}{size} (y\_true-y\_pred)^2$

#### typedef struct OurNeuralNetwork

神经网络结构体 定义了

```C
	// 拥有一个隐藏层 两个神经元(h1,h2)
	// 一个输出层 一个神经元
    double w1, w2, w3, w4, w5, w6;
    double b1, b2, b3;
```

#### OurNeuralNetwork* CreateOurNeualNetwork() 

创建神经网络实例 对权重(w1\~w6)及偏执(b1\~b3)进行随机赋值

#### double feedforward(神经网络实例，double x1,double x2)

传入一个神经网络实例和两个输入

用于训练后预测数据

返回 o1，即经过一个输入层，一个隐藏层后由**sigmoid**函数激活后的结果

#### void train(神经网络实例,double data[4]\[2],double* all_y_trues,int data_size,int y_size)

传入一个神经网络实例和部分数据及它们大小

通过多次训练(epochs)和控制训练速度(learn_rate)的情况下，计算各个权重及偏执的偏导数 使loss越来越小

并且每10次训练输出一次loss值并绘图

#### void CreatePicture()

绘制函数初始化 并绘制x,y轴

#### int importdata(double testdata[MAX_ROWS]\[3])

导入本地数据，数据集为身高体重分别在(50\~70英寸和100\~200磅)之间且性别随机的人类（以1代表女，0代表男）

将本地数据导入到testdata数组中，并进行标准化。第一二三项分别为：身高，体重，性别。

返回一个整数，表示数据共有**line**项 便于后续计算。

#### int main()

主函数，创建数组，导入数据，截取部分数据用于训练，创建实例，绘图窗口初始化，训练神经网络，进行预测，并输出真实值。

## 测试分析

为了评估神经网络算法的性能和效果，需要进行测试和分析。测试和分析的方法有：

- 训练集、验证集和测试集：将数据集划分为三部分，分别用于训练、验证和测试。训练集用于学习和调整权重，验证集用于选择最优的模型参数和超参数，测试集用于评估最终的模型效果。
- 损失函数和准确率：损失函数是衡量模型输出与真实值之间的差异程度，准确率是衡量模型正确分类或预测的比例。损失函数和准确率可以用于监控训练过程中的进展和收敛情况。

<img src="https://s2.loli.net/2023/12/20/9b2nHS4a8WJu3dR.png" alt="image-20231220165548327" style="zoom: 50%;" />

**在训练次数为1000，速度为0.1的情况下，训练集为数据集前4项的情况下 前10项数据与结果较为相似，但后续数据偏差较大，推测为训练数据项太少及数据过于随机的原因**

**如若使用真实数据集，准确率或许能达到80%**

## 总结

本文介绍了神经网络算法的基本概念、设计方法、测试方法等内容。神经网络算法是一种强大而灵活的人工智能技术，可以应用于多种领域和问题。神经网络算法的发展和创新还在不断进行中，未来有望实现更高的水平和更广的应用。

本程序实现一个简单的通过训练来判断男女性别的功能

## 参考文献

* [深度学习笔记：如何理解激活函数？（附常用激活函数） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/364620596)
* [机器学习初学：神经网络原理 + Python 简单实例 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/377513272) **感谢大佬！！！代码与图主要来源于此**
* [(64 封私信 / 81 条消息) 同一个训练集、模型和参数，每次训练的结果都不一样，最大相差3%，所以请问实验训练的结果怎样才算最好？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/438562530)
* [C 文件读写 | 菜鸟教程 (runoob.com)](https://www.runoob.com/cprogramming/c-file-io.html)
* [扉川川川 (feichuans.com)](https://feichuans.com/)
* [CodeConvert AI - Convert code with a click of a button](https://www.codeconvert.ai/)

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <time.h>
#include<graphics.h> //绘图函数库
#define MAX_ROWS 100 //最大行数
#define MAX_COLS 100 //最大列数
double sigmoid(double x) {	//激活函数

    return 1 / (1 + exp(-x));
    //结果越接近1 说明数据更偏向女性 反之偏向男性
}
double deriv_sigmoid(double x) {//激活函数的导数
    double fx = sigmoid(x);
    return fx * (1 - fx);
}

double mes_loss(double* y_true, double* y_pred, int size) {//损失函数 
    double sum = 0;
    for (int i = 0; i < size; i++) {
        sum += pow(y_true[i] - y_pred[i], 2);
    }
    // 求各个元素/个数的和
    return sum / size;
}

typedef struct {	// 神经网络定义
	// 拥有一个隐藏层 两个神经元(h1,h2)
	// 一个输出层 一个神经元
    double w1, w2, w3, w4, w5, w6;
    double b1, b2, b3;
} OurNeuralNetwork;

OurNeuralNetwork* createOurNeuralNetwork() {// 创建神经网络实例
    OurNeuralNetwork* network = (OurNeuralNetwork*)malloc(sizeof(OurNeuralNetwork));
    srand(time(NULL));
    network->w1 = ((double)rand() / RAND_MAX) * 2 - 1;
    network->w2 = ((double)rand() / RAND_MAX) * 2 - 1;
    network->w3 = ((double)rand() / RAND_MAX) * 2 - 1;
    network->w4 = ((double)rand() / RAND_MAX) * 2 - 1;
    network->w5 = ((double)rand() / RAND_MAX) * 2 - 1;
    network->w6 = ((double)rand() / RAND_MAX) * 2 - 1;
    network->b1 = ((double)rand() / RAND_MAX) * 2 - 1;
    network->b2 = ((double)rand() / RAND_MAX) * 2 - 1;
    network->b3 = ((double)rand() / RAND_MAX) * 2 - 1;
    return network;
}

double feedforward(OurNeuralNetwork* network, double x1, double x2) {	// 前馈 神经元标准操作
    double h1 = sigmoid(network->w1 * x1 + network->w2 * x2 + network->b1);
    double h2 = sigmoid(network->w3 * x1 + network->w4 * x2 + network->b2);
    double o1 = sigmoid(network->w5 * h1 + network->w6 * h2 + network->b3);
    return o1;
}

void train(OurNeuralNetwork* network, double data[4][2], double* all_y_trues, int data_size, int y_size) {//训练神经网络
	double learn_rate = 0.1; //训练速度
    int epochs = 2000;//训练次数

    for (int epoch = 0; epoch < epochs; epoch++) {
    	//开始训练
    	//最终目的:使loss越来越小
        for (int i = 0; i < data_size; i++) {
        	//计算偏导数 
            double x1 = data[i][0];
            double x2 = data[i][1];
            double y_true = all_y_trues[i];
            double sum_h1 = network->w1 * x1 + network->w2 * x2 + network->b1;
            double h1 = sigmoid(sum_h1);
            double sum_h2 = network->w3 * x1 + network->w4 * x2 + network->b2;
            double h2 = sigmoid(sum_h2);
            double sum_o1 = network->w5 * h1 + network->w6 * h2 + network->b3;
            double o1 = sigmoid(sum_o1);
            double y_pred = o1;
            double d_L_d_ypred = -2 * (y_true - y_pred);
            double d_ypred_d_w5 = h1 * deriv_sigmoid(sum_o1);
            double d_ypred_d_w6 = h2 * deriv_sigmoid(sum_o1);
            double d_ypred_d_b3 = deriv_sigmoid(sum_o1);
            double d_ypred_d_h1 = network->w5 * deriv_sigmoid(sum_o1);
            double d_ypred_d_h2 = network->w6 * deriv_sigmoid(sum_o1);
            double d_h1_d_w1 = x1 * deriv_sigmoid(sum_h1);
            double d_h1_d_w2 = x2 * deriv_sigmoid(sum_h1);
            double d_h1_d_b1 = deriv_sigmoid(sum_h1);
            double d_h2_d_w3 = x1 * deriv_sigmoid(sum_h2);
            double d_h2_d_w4 = x2 * deriv_sigmoid(sum_h2);
            double d_h2_d_b2 = deriv_sigmoid(sum_h2);
            network->w1 -= learn_rate * d_L_d_ypred * d_ypred_d_h1 * d_h1_d_w1;
            network->w2 -= learn_rate * d_L_d_ypred * d_ypred_d_h1 * d_h1_d_w2;
            network->b1 -= learn_rate * d_L_d_ypred * d_ypred_d_h1 * d_h1_d_b1;
            network->w3 -= learn_rate * d_L_d_ypred * d_ypred_d_h2 * d_h2_d_w3;
            network->w4 -= learn_rate * d_L_d_ypred * d_ypred_d_h2 * d_h2_d_w4;
            network->b2 -= learn_rate * d_L_d_ypred * d_ypred_d_h2 * d_h2_d_b2;
            network->w5 -= learn_rate * d_L_d_ypred * d_ypred_d_w5;
            network->w6 -= learn_rate * d_L_d_ypred * d_ypred_d_w6;
            network->b3 -= learn_rate * d_L_d_ypred * d_ypred_d_b3;
        }
        double loss;
        if (epoch % 10 == 0) {
            double* y_preds = (double*)malloc(y_size * sizeof(double));
            for (int i = 0; i < data_size; i++) {
                double x1 = data[i][0];
                double x2 = data[i][1];
                double y_pred = feedforward(network, x1, x2);
                y_preds[i] = y_pred;
            }
            loss = mes_loss(all_y_trues, y_preds, y_size);
            circlef(epoch,600-loss*1000,1.0);
            printf("Epoch %d loss: %f\n", epoch, loss);
            free(y_preds);
        }
        
    }
}
void CreatePicture(){//绘图函数
	       initgraph(1200,1600);
		    line(0, 700, 800, 700);
		    line(100,0,100,800);
		    outtextxy(20,100,"LOSS");
		    outtextxy(580,800,"Epochs");
}

int importdata(double testdata[MAX_ROWS][3]){//导入数据
        	    FILE *file = fopen("./data.txt","rb+");
	    if(file==NULL){
			printf("文件不存在\n");
		}
		int row = 0,col = 0,secondvalue,sum=0,l=0;
		while(!feof(file)){
			int value = fgetc(file);
			if(value=='\n'){
				row++;
				col = 0;
			}
			else if(value >='0' && value <= '9'){
				sum = sum*10 + value-'0';
				col++;
			}
			else if(secondvalue>='0'&&secondvalue<='9'&&value==39){
//				printf("%c",secondvalue);
				if(l==0){
					sum -=66;//中国男女身高平均值
				}
				if(l==1) sum-=147.7097;//中国男女体重平均值
				//数据标准化
				testdata[row][l++] = sum;
				l = l==3?0:l;
				sum = 0;
			}
			
			secondvalue = value;
		}
		return row;
//		for(int i=0;i<=MAX_ROWS&&testdata[i][0];i++){
//			for(int j=0;j<=MAX_COLS&&testdata[i][j];j++){
//				printf("%lf ",testdata[i][j]);
//			}
//		}
//	}
}
int main() {//主函数
    double testdata[MAX_ROWS][3] = {0.0};
    int lines = importdata(testdata);
    double traindata[10][2];
    double all_y_trues[10];
    for(int i=0;i<10;i++){
    	traindata[i][0] =testdata[i][0];
    	traindata[i][1] = testdata[i][1];
    	all_y_trues[i] = testdata[i][2];
    	
	}
    OurNeuralNetwork* network = createOurNeuralNetwork();
	CreatePicture();
    train(network, traindata, all_y_trues, 10, 10);
    for(int i=0;i<lines;i++){
		printf("%.1lf\t%.1lf\t:%.5lf\t真实结果:%.0lf\n",testdata[i][0],testdata[i][1],feedforward(network,testdata[i][0],testdata[i][1]),testdata[i][2]);
	}
	printf("单位: 身高-66(英寸),体重-147(磅)\n");
    printf("按任意键退出:");
    getchar();
    closegraph();
    free(network);
    return 0;
}
```
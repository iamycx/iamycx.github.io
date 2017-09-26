---
layout: post
title:  机器学习实战——Logistic回归
date:   2017-09-26 17:24:11 +08:00
category: 其他
tags: Python 机器学习 Logistic
comments: true
---

* content
{:toc}



```python
# -*- coding:utf-8 -*- 
from numpy import *  
  
#加载数据集  
def loadDataSet():  
    dataMat = []  
    labelMat = []  
    fp = open("C:\\Users\\Rainey\\Desktop\\testSet.txt")  
    for line in fp.readlines():  
        lineArr = line.strip().split() #删除文件中多余的字符  
        dataMat.append([1.0,float(lineArr[0]), float(lineArr[1])])  
        labelMat.append(float(lineArr[2]))  
  
    return dataMat,labelMat  
  
#定义Sigmoid函数  
def sigmoid(inX):  
    return 1.0/(1+exp(-inX))  
  
#定义求解最佳回归系数,Logistic回归梯度上升优化算法  
def gradAscent(dataMatIn,classLabels):  
    dataMatrix = mat(dataMatIn) #将数组转为矩阵  
    labelMat = mat(classLabels).transpose()  #转置
    m,n = shape(dataMatrix)      #返回矩阵的行和列  
    alpha = 0.001      #初始化 alpha的值  
    maxCycles = 500    #最大迭代次数  
    weights = ones((n,1)) #初始化最佳回归系数  
    for i in range(0,maxCycles):  
        #引用原书的代码，求梯度  
        #dataMatrix*weights，100×3和3×1的矩阵相乘，得到100×1的矩阵  
        h = sigmoid(dataMatrix*weights)  
        #h的取值为0~1，因而error为误差
        error = labelMat - h  
        weights = weights + alpha * dataMatrix.transpose() * error  
  
    return weights  

#随机梯度上升算法
def stocGradAscent0(dataMatrix, classLabels):   
    m,n     = shape(dataMatrix)  
    alpha   = 0.01  
    weights = ones(n)  
    for i in range(m):  
        h       = sigmoid(sum(dataMatrix[i]*weights))           #此处h为具体数值  
        error   = classLabels[i] - h                            #error也为具体数值  
        weights = weights + alpha*error*dataMatrix[i]           #每次对一个样本进行处理，更新权值  
    return weights  

#改进的随机梯度上升算法，收敛得更快
def stocGradAscent1(dataMatrix, classLabels, numIter=150):
    m,n = shape(dataMatrix)  
    weights = ones(n)  
    for j in range(numIter):  
        dataIndex = range(m)  
        for i in range(m):  
            alpha = 4/(1.0+i+j)+0.0001 #alpha迭代次数不断变小，1.非严格下降，2.不会到0  
            #随机选取样本更新系数weights,每次随机从列表中选取一个值，用过后删除它再进行下一次迭代              
            randIndex = int(random.uniform(0, len(dataIndex)))#每次迭代改变dataIndex,而m是不变的，故不用unifor(0, m)  
            h = sigmoid(sum(dataMatrix[randIndex]*weights))  
            error = classLabels[randIndex] - h  
            weights = weights + alpha*error*dataMatrix[randIndex]  
            del(dataIndex[randIndex])  
    return weights  

  
#分析数据，画出决策边界  
def plotBestFit(wei,dataMatrix,labelMat):  
    import matplotlib.pyplot as plt  
    weights = wei    #将矩阵wei转化为list  
    dataArr = array(dataMatrix)  #将矩阵转化为数组  
    n = shape(dataMatrix)[0]  
    xcord1 = [];ycord1=[]  
    xcord2 = [];ycord2=[]  
  
    for i in range(n):  
        if int(labelMat[i])==1:  
            xcord1.append(dataArr[i,1])  
            ycord1.append(dataArr[i,2])  
        else:  
            xcord2.append(dataArr[i,1])  
            ycord2.append(dataArr[i,2])  
  
    fig = plt.figure()  
    ax = fig.add_subplot(111)  
    ax.scatter(xcord1,ycord1,s=30,c='red', marker='s')  
    ax.scatter(xcord2,ycord2,s=30,c="green")  
    x = arange(-3.0,3.0,0.1)  #x为numpy.arange格式，并且以0.1为步长从-3.0到3.0切 
    #拟合曲线为0 = w0*x0+w1*x1+w2*x2, 故x2 = (-w0*x0-w1*x1)/w2, x0为1,x1为x, x2为y,故有
    y = (-weights[0]-weights[1] * x)/weights[2]  
    ax.plot(x,y)  
    plt.xlabel("x1")     #X轴的标签  
    plt.ylabel("x2")     #Y轴的标签  
    plt.show()  
  
if __name__=="__main__":  
    dataMatrix,labelMat = loadDataSet()  
    weight = stocGradAscent1(array(dataMatrix), labelMat)  
    plotBestFit(weight,dataMatrix,labelMat)  
```

![梯度上升](http://upload-images.jianshu.io/upload_images/3688263-ac2c1e9dc721f752.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![随机梯度上升](http://upload-images.jianshu.io/upload_images/3688263-30e207e1ae0ae73a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![改进的随机梯度上升](http://upload-images.jianshu.io/upload_images/3688263-3f7b290d3fe722f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

样本集为:
```
-0.017612   14.053064   0  
-1.395634   4.662541    1  
-0.752157   6.538620    0  
-1.322371   7.152853    0  
0.423363    11.054677   0  
0.406704    7.067335    1  
0.667394    12.741452   0  
-2.460150   6.866805    1  
0.569411    9.548755    0  
-0.026632   10.427743   0  
0.850433    6.920334    1  
1.347183    13.175500   0  
1.176813    3.167020    1  
-1.781871   9.097953    0  
-0.566606   5.749003    1  
0.931635    1.589505    1  
-0.024205   6.151823    1  
-0.036453   2.690988    1  
-0.196949   0.444165    1  
1.014459    5.754399    1  
1.985298    3.230619    1  
-1.693453   -0.557540   1  
-0.576525   11.778922   0  
-0.346811   -1.678730   1  
-2.124484   2.672471    1  
1.217916    9.597015    0  
-0.733928   9.098687    0  
-3.642001   -1.618087   1  
0.315985    3.523953    1  
1.416614    9.619232    0  
-0.386323   3.989286    1  
0.556921    8.294984    1  
1.224863    11.587360   0  
-1.347803   -2.406051   1  
1.196604    4.951851    1  
0.275221    9.543647    0  
0.470575    9.332488    0  
-1.889567   9.542662    0  
-1.527893   12.150579   0  
-1.185247   11.309318   0  
-0.445678   3.297303    1  
1.042222    6.105155    1  
-0.618787   10.320986   0  
1.152083    0.548467    1  
0.828534    2.676045    1  
-1.237728   10.549033   0  
-0.683565   -2.166125   1  
0.229456    5.921938    1  
-0.959885   11.555336   0  
0.492911    10.993324   0  
0.184992    8.721488    0  
-0.355715   10.325976   0  
-0.397822   8.058397    0  
0.824839    13.730343   0  
1.507278    5.027866    1  
0.099671    6.835839    1  
-0.344008   10.717485   0  
1.785928    7.718645    1  
-0.918801   11.560217   0  
-0.364009   4.747300    1  
-0.841722   4.119083    1  
0.490426    1.960539    1  
-0.007194   9.075792    0  
0.356107    12.447863   0  
0.342578    12.281162   0  
-0.810823   -1.466018   1  
2.530777    6.476801    1  
1.296683    11.607559   0  
0.475487    12.040035   0  
-0.783277   11.009725   0  
0.074798    11.023650   0  
-1.337472   0.468339    1  
-0.102781   13.763651   0  
-0.147324   2.874846    1  
0.518389    9.887035    0  
1.015399    7.571882    0  
-1.658086   -0.027255   1  
1.319944    2.171228    1  
2.056216    5.019981    1  
-0.851633   4.375691    1  
-1.510047   6.061992    0  
-1.076637   -3.181888   1  
1.821096    10.283990   0  
3.010150    8.401766    1  
-1.099458   1.688274    1  
-0.834872   -1.733869   1  
-0.846637   3.849075    1  
1.400102    12.628781   0  
1.752842    5.468166    1  
0.078557    0.059736    1  
0.089392    -0.715300   1  
1.825662    12.693808   0  
0.197445    9.744638    0  
0.126117    0.922311    1  
-0.679797   1.220530    1  
0.677983    2.556666    1  
0.761349    10.693862   0  
-2.168791   0.143632    1  
1.388610    9.341997    0  
0.317029    14.739025   0
```
[参考](http://blog.csdn.net/u010454729/article/details/48274955)
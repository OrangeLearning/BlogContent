---
title: Pytorch(1)
date: 2018-04-20 17:13:30
tags: [Pytorch]
---

> 什么基础的Tensor和Variable之类打基础我就不说了，如果以后有问题再说  
这里就做东西好了  
特别鸣谢网上的很多打大大的blog和教程，如果有侵权行为，请私信联系我，我立刻删除相关内容

#  Pytorch实现一个简单的回归

环境  
* anoconda3   
* python3   
* ubuntu16.04 
```py
"""
这篇文章用于尝试一个回归问题
"""
import torch
import torch.nn as nn
import torch.nn.functional as func
import torch.optim as optim
from torch.autograd import Variable
import matplotlib.pyplot as plt

# 首先构造一点加噪声打数据
# unsqueeze(input,Dim)
# 会为input增加一维
x = torch.unsqueeze(torch.linspace(-1, 1, 100), dim=1)
y = x.pow(2) + 0.2 * torch.rand(x.size())

# 用 Variable 来修饰这些数据 tensor
x, y = torch.autograd.Variable(x), Variable(y)


# 画图
# plt.scatter(x.data.numpy(), y.data.numpy())
# plt.show()

# 下面我们建立一个神经网络
# 以下两个函数必须必须
# torch的反向传播是由
class Net(nn.Module):
    def __init__(self, input_num, hidden_num, output_num):
        super(Net, self).__init__()
        self.hidden = torch.nn.Linear(input_num, hidden_num)
        self.predict = torch.nn.Linear(hidden_num, output_num)

    def forward(self, x):
        x = self.hidden(x)
        x = func.relu(x)
        x = self.predict(x)
        return x

# 输入和输出没有悬念
# hidden层节点数打确立现在还没有头绪
net = Net(input_num=1,hidden_num=10,output_num=1)
print(net)
# 下面就是训练过程
# optimizer 是训练的工具
optimizer = torch.optim.SGD(net.parameters(), lr=0.5)  # 传入 net 的所有参数, 学习率
# 预测值和真实值的误差计算公式 (均方差)
loss_func = torch.nn.MSELoss()

# t是训练次数
for t in range(100):
    prediction = net(x)
    loss = loss_func(prediction, y)

    # pytorch里面的数据是怎么交互打呢？
    # 清空上一步的残余更新参数值
    optimizer.zero_grad()

    # 误差反向传播, 计算参数更新值
    loss.backward()

    # 将参数更新值施加到 net 的 parameters 上
    optimizer.step()

prediction = net(x)
plt.cla()
plt.scatter(x.data.numpy(), y.data.numpy())
plt.plot(x.data.numpy(), prediction.data.numpy(), 'r-', lw=5)
plt.text(0.5, 0, 'Loss=%.4f' % loss.data[0], fontdict={'size': 20, 'color':  'red'})
plt.show()
```

![图片描述](https://img-blog.csdn.net/20180125203132538?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQva2lzc2FjbQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

具体解释在注释中

这里我们看到一个问题，就是Pytorch中的loss 和optim是如何交互的呢？这个问题，我们以后打blog讲解
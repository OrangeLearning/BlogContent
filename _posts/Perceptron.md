---
title: Perceptron
date: 2018-05-21 23:28:30
tags: [Machine Leaning, Perceptron]
---
使用iris data的数据，具体的地址是:
[iris data](https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data)

最简单的二分类，直接给出代码，解释在注释中：

```py
import data.iris as iris
import numpy as np

# the rate of train / test 
TTR = 0.6

# 对于数据进行编码，这次没有使用
def decode_data(train_data):
    res = []
    for item in train_data:
        if item[4] not in res:
            res.append(item[4])

    ans = []
    cnt = 0
    for item in res:
        ans.append({
            "name": item,
            "num": cnt
        })
        cnt += 1

    return ans


class Perception:
    """
        eta: 学习率
        vector_n: 大小
    """

    def __init__(self, eta, vector_n):
        self.eta = eta
        self.w = [i for i in range(vector_n)]
        self.b = 1

    """
        calc是
    """
    def calc(self, x):
        return np.sum(self.w * x) + self.b

    """
        更新一次step
    """
    def step(self, x, y):
        self.w = self.w + self.eta * y * x
        self.b = self.b + self.eta * y

    """
        使用的是w = []
        w * x + b = y
        更新公式是：
            如果y(wx+b) <= 0，则更新结果
                w <= w + \eta \times y x
                b <= b + \eta \times y
    """

    def train(self, x, y):
        n_item = x.shape[0]
        for i in range(n_item):
            tmp = self.calc(x[i])
            if y[i] * self.calc(x[i]) <= 0:
                self.step(x[i], y[i])

    """
        返回训练出来的测试结果
    """
    def test(self, x):
        yy = []
        print("ans: w = ", self.w, " b = ", self.b)
        for i in x:
            tmp = self.calc(i)
            yy.append(tmp)

        yy = np.sign(yy)
        yy = yy.astype(int)
        return yy


def main():
    train_data, test_data = iris.get_train_and_test(TTR)

    mp = {}
    mp["Iris-setosa"] = -1
    mp["Iris-virginica"] = 1

    train_data_x = []
    train_data_y = []
    for item in train_data:
        train_data_x.append(item[0:4])
        train_data_y.append(mp[item[4:5][0]])
    train_data_x = np.array(train_data_x)
    train_data_y = np.array(train_data_y)

    test_data_x = []
    test_data_y = []
    for item in test_data:
        test_data_x.append(item[0:4])
        test_data_y.append(mp[item[4:5][0]])
    test_data_x = np.array(test_data_x)
    test_data_y = np.array(test_data_y)

    perception = Perception(0.9, 4)
    perception.train(train_data_x, train_data_y)

    predict_y = perception.test(test_data_x)


    print(predict_y, "\n\n", test_data_y)
    print(np.sum(predict_y - test_data_y))


if __name__ == '__main__':
    main()

```
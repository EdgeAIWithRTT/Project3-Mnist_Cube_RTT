> - Summary: 在 RT-Thread 系统上执行 Mnist 推理，纯手搭版
> - Author: lebhoryi@gmail.com & qiwen20150309@163.com
> - Date: 2020/07/19

[TOC]


# 0x00 前言

在 H743 + RT - Thread 上实现MNIST推理

两种方法:

- [x] STM32Cube AI + RTT

- [ ] CMSIS + RTT

# 0x01 文件树

```shell
/home/lebhoryi/RT-Thread/Edge_AI [git::master *] [lebhoryi@RT-AI] [15:12]
> tree -L 1 ./Project2-Mnist 
./Project2-Mnist
├── data  # mnist 数据集
├── image  # 自定义测试集
├── Mnist_RTT  # 使用 RT-AK 之后的项目工程，集成了 AI 的 RT-Thread 工程
├── mnist.ipynb  # 模型训练及验证
├── model  # 模型储存
└── readme.md
```

# 0x02 PC 训练 Model

## 2.1 PC 端环境

- Tensorflow: 2.3.0-dev20200515
- Numpy: 1.16.4
- Keras: 2.2.4-tf

## 2.2 数据集

> File: ./data/mnist.npz

MNIST 数据集由 60000 (训练集) + 10000(测试集) 手写字符组成, 每张图片的大小为 $ 28 * 28 $, 数据集手动下载地址 [http://yann.lecun.com/exdb/mnist/](http://yann.lecun.com/exdb/mnist/) .

![](https://gitee.com/lebhoryi/PicGoPictureBed/raw/master/img/20200719132029.png)

## 2.3 网络结构

- 两层卷积 + 一层全连接层

![](https://gitee.com/lebhoryi/PicGoPictureBed/raw/master/img/20200719132529.png)

## 2.4 训练模型 & 验证模型

> File: ./model/mnist.h5

- 训练模型

![](https://gitee.com/lebhoryi/PicGoPictureBed/raw/master/img/20200719133308.png)

- 验证训练模型的准确率

![](https://gitee.com/lebhoryi/PicGoPictureBed/raw/master/img/20200719132812.png)

- 保存权重文件

```python
# save weights
model.save_weights(model_path / 'model_weights.h5')

# load weights
model.load_weights(model_path / 'model_weights.h5')

model.compile(optimizer='adam',
             loss='sparse_categorical_crossentropy',
             metrics=['accuracy',])
loss, acc = model.evaluate(x_test, y_test)
print("Restored model, accuracy: {:5.2f}%".format(100*acc))
```

```shell
313/313 [==============================] - 1s 2ms/step - loss: 0.1226 - accuracy: 0.9651
Restored model, accuracy: 96.51%
```

# 0x03 RT-AK + STM32Cube AI

- 硬件平台： `ART-PI`

- 模型：`model/mnist.tflite`

- 我想要从零开始到 `Mnist_RTT` 工程？

  1. 先打开 `RT-Thread Studio` 新建 `ART-PI` 模板示例工程
  2. 下载 `RT-AK` 
  3. 运行 `RT-AK`
  4. 即可

  > `Mnist_RTT/applications` 中的 `mnist_app.c` 为示例开发 `Demo`，并非 `RT-AK` 生成
  >
  > 该问题是另外一个话题了，详细请查阅 RT-AK 相关文档。即将开源 2021/04/10

详细请查阅 [./Mnist_RTT/Readme.md](./Mnist_RTT/Readme.md)

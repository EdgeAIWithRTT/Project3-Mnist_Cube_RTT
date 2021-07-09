<center><h1>RT-AK 快速上手</h1></center>

[TOC]

1. *本项目为 `RT-AK` 的一个实战 `DEMO`。*
2. 本项目可直接食用，已经集成了 `RT-Thread` 以及 `AI` 模型

# 1. RT-AK 简介

> 目前该项目为 RT-AK 的示例 Demo，基于 ART-PI 硬件平台和 Mnist 数据集。

- `RT-AK`: `RT-Thread AI Toolkit`，RT-Thread AI 套件。

`RT-AK` 是 `RT-Thread` 团队为 `RT-Thread` 实时操作系统所开发的 `AI` 套件，能够一键将 `AI` 模型部署到 RT-Thread 项目中，让用户可以 在统一的 API 之上进行业务代码开发，又能在目标平台上获极致优化的性能，从而更简单方便地开发端侧 AI 应用程序。

在 RT-AK 支持下，仅需要一行命令，即可将 AI 模型部署到 RT-Thread 系统中：

```shell
$ python rt_ai_tools.py --model xxx...
```

---

**我们将致力于降低嵌入式 AI 落地的难度和门槛**

# 2. 项目

该项目是基于 ART-PI 的模板工程，初始工程来于 RT-Thread 新建工程

经过 RT-AK 转换之后得到的一个完整的项目工程

<img src="https://gitee.com/lebhoryi/PicGoPictureBed/raw/master/img/20210409182318.png" style="zoom:80%;" />

# 3. 目录结构

![image-20210410154606274](https://gitee.com/lebhoryi/PicGoPictureBed/raw/master/img/20210410154607.png)

# 4. 代码开发

相关应用开发代码请参考 `RT-AK Lib` 开发手册

`RT-AK` 所提供的示例 `Demo`: [mnist_app.c](applications/mnist_app.c)，运行 `mnist_app` 即可

![image-20210409192638719](https://gitee.com/lebhoryi/PicGoPictureBed/raw/master/img/20210409192639.png)


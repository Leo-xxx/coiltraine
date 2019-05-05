## Github项目推荐 | 条件模仿学习训练框架

AI研习社 [AI研习社](javascript:void(0);) *前天*

![img](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibRKJzRrSpZicEC9kzAbKNOvdI49Y7xhUddYSIbpY3Yd0fWyibk92cgobjAIOK50m2VQXVy37haeNC2g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 

# 

## 

### 



## **COiLTRAiNE: Conditional Imitation Learning Training Framework**

by **Felipe Codevilla**

本项目可以方便地对模拟学习网络的培训进行训练和管理，并结合CARLA模拟器进行评估。目的是：

- 用户使用单个命令就能执行多次训练。
- 用CARLA自动测试已经训练过的系统。
- 允许用户一眼就能监控CARLA的多项训练和测试。
- 允许执行“基于视觉的驾驶模型的离线评估”一文中提出的测试方法。
- 允许使用“探索自动驾驶行为克隆的局限性（论文）”一文中的模型。
- *你还可以使用**CARLA挑战中的基线**。*

**Github项目链接：**

[https://github.com/felipecode/coiltraine](https://mp.weixin.qq.com/s?__biz=MjM5ODU3OTIyOA==&mid=2650676239&idx=2&sn=40b369c639fa34e0b574d88c5bf54adf&chksm=bec2217c89b5a86a9d70aea265f2b246b9a653ea42be1efeda54fcee17fffa89d1f9acabe11c&mpshare=1&scene=1&srcid=&key=92b7d480e1160ecede6bcf09439e90fcb5d4a3e6998dfecacb3d1a72746a0cf17d095cb206dd29793d9a10a101168c4d3115678155ca5dcef30d6439af14471b6d8ac0e4296523b56cd7d8a7ff564ec4&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060739&lang=zh_CN&pass_ticket=f7CgN3cUgVMojzAiWUZuwpvAv7bNHgQChXXDR2CF3ufVoHK%2Fz4hhJlYnE7b3oNOd)

## **系统概览**

![1556176298792157.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibQT838gAVrgzTcKwThczicGfibPwKQ8thjlHVqbPSf2y4ic4llRiaheFptz6CGNfyecQTQicZHxduxhEsw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

COiLTRAiNE框架允许同时进行训练，在CARLA中的场景中驾驶和对一些静态数据集的控制进行预测。 该过程可以同时在几个实验中完成。

## **开始**

### **准备工具：**

- 硬件：具有能运行虚幻引擎的专用GPU的计算机。 GPU建议使用NVIDIA 1070或更高版本。
- 操作系统：兼容CARLA (16.04)的Ubuntu

### ***安装：***

为了安装COiLTRAiNE，我们提供了一个conda环境需求文件。首先在一些文件夹中克隆项目仓库，然后只需运行以下命令即可安装：

- 

```
conda env create -f requirements.yaml
```

### **设置环境/获取数据：**

首先你需要定义数据集文件夹。 这个文件夹将会包含训练和验证数据集。

- 

```
export COIL_DATASET_PATH=<Path to where your dataset folders are>
```

通过运行下列命令，下载一个示例数据集包，其中包含一个训练包和两个验证包：

- 

```
python3 tools/get_sample_datasets.py
```

数据集、CoILTrain、CoILVal1和CoILVal2 将存储在 COIL_DATASET_PATH 文件夹中。

要收集其他数据集，请查看数据收集器项目：[https://github.com/carla-simulator/data-collector](https://mp.weixin.qq.com/s?__biz=MjM5ODU3OTIyOA==&mid=2650676239&idx=2&sn=40b369c639fa34e0b574d88c5bf54adf&chksm=bec2217c89b5a86a9d70aea265f2b246b9a653ea42be1efeda54fcee17fffa89d1f9acabe11c&mpshare=1&scene=1&srcid=&key=92b7d480e1160ecede6bcf09439e90fcb5d4a3e6998dfecacb3d1a72746a0cf17d095cb206dd29793d9a10a101168c4d3115678155ca5dcef30d6439af14471b6d8ac0e4296523b56cd7d8a7ff564ec4&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060739&lang=zh_CN&pass_ticket=f7CgN3cUgVMojzAiWUZuwpvAv7bNHgQChXXDR2CF3ufVoHK%2Fz4hhJlYnE7b3oNOd)

### **获取CARLA**

注意：自动场景评估只适用于CARLA 0.8。你可以 [训练和评估 CARLA 0.9.X 中的代理](https://mp.weixin.qq.com/s?__biz=MjM5ODU3OTIyOA==&mid=2650676239&idx=2&sn=40b369c639fa34e0b574d88c5bf54adf&chksm=bec2217c89b5a86a9d70aea265f2b246b9a653ea42be1efeda54fcee17fffa89d1f9acabe11c&mpshare=1&scene=1&srcid=&key=92b7d480e1160ecede6bcf09439e90fcb5d4a3e6998dfecacb3d1a72746a0cf17d095cb206dd29793d9a10a101168c4d3115678155ca5dcef30d6439af14471b6d8ac0e4296523b56cd7d8a7ff564ec4&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060739&lang=zh_CN&pass_ticket=f7CgN3cUgVMojzAiWUZuwpvAv7bNHgQChXXDR2CF3ufVoHK%2Fz4hhJlYnE7b3oNOd)

如果要在CARLA中进行方案评估，必须在docker下安装CARLA 0.8.4或CARLA 0.8.2。本教程将会介绍如何在docker下安装CARLA。

### **执行**

假设你的CARLA docker的docker图像名称为“carlasim/carla:version”，则可以通过运行以下命令来执行coiltraine系统：

- 

```
python3 coiltraine.py --folder sample --gpus 0 -de TestT1_Town01 -vd CoILVal1 --docker carlasim/carla:version
```

其中 --folder 样本是包含所有将要训练和验证的实验的实验批次。TestT1是Town01上的驱动方案，定义为 drive/suites 文件夹中的一个类。 验证数据集作为参数与 -vd 一起传递，并且应该放在 COIL_DATASET_PATH 文件夹中。

### **期望输出**

你应该能在终端上看到彩色屏幕：

![1556176877556176.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibQT838gAVrgzTcKwThczicGfkCowrR0AGRicBfOcCk2HvYWHtwEX7dF12SB4ukGFtWGRsTXeSE2qE7g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

完成训练和验证后，终端屏幕应该会开始如下所示：

![1556177153809567.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibQT838gAVrgzTcKwThczicGfJXj92MqGHuJ6j5toVdkQLAYEE357wjibFq2C1A1n2Jvc6DfQc2vSZQg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

由于在Docker下运行的CARLA是在屏幕外运行的，因此你不会看到任何CARLA服务器在屏幕中弹出通知。另外需要注意的是，这里的示例是在样本数据上进行训练，并且在样本的基准上进行测试，因此产生的驾驶模型质量会很差。建议测试条件模型动物园中的一些模型，以获得高性能的条件模仿模型。

## **条件模型动物园**

- 有条件的模仿学习
- 条件模仿学习CARLA（论文）
- 基于视觉的驾驶模型的离线评估（论文）
- 探索自动驾驶行为克隆的局限性（论文）



**备受大家期待的强化学习课程终于上线啦！**

扫描下方邀请卡，解锁更多课时

![img](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSpgphl35CPgEkd2BzG7jk93Ysry7AZWxhibuUPmG2d1FC3J9sDcrcicouhysXVjpAaLFVjRGXj9cuQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![img](https://mmbiz.qpic.cn/mmbiz_gif/bicdMLzImlibRAS3Tao2nfeJk00qqxX3axIgPV3yia4NPESGdUJEM9vsfw1O4Dg1iat7lVNAmbCMY65ia2pzfBXm5kg/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

点击 **阅读原文**，查看更多内容

[阅读原文](https://mp.weixin.qq.com/s?__biz=MjM5ODU3OTIyOA==&mid=2650676239&idx=2&sn=40b369c639fa34e0b574d88c5bf54adf&chksm=bec2217c89b5a86a9d70aea265f2b246b9a653ea42be1efeda54fcee17fffa89d1f9acabe11c&mpshare=1&scene=1&srcid=&key=92b7d480e1160ecede6bcf09439e90fcb5d4a3e6998dfecacb3d1a72746a0cf17d095cb206dd29793d9a10a101168c4d3115678155ca5dcef30d6439af14471b6d8ac0e4296523b56cd7d8a7ff564ec4&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060739&lang=zh_CN&pass_ticket=f7CgN3cUgVMojzAiWUZuwpvAv7bNHgQChXXDR2CF3ufVoHK%2Fz4hhJlYnE7b3oNOd##)







微信扫一扫
关注该公众号
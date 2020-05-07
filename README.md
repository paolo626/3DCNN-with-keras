# 3DCNN with keras
 This is code for 3DCNN  model  base UCF101 dataset. it  fix other project min error: https://github.com/kcct-fujimotolab/3DCNN





 # UCF101动作识别的代码复现

这是我看这篇论文的重点，这里我在colab环境下实现UCF101动作识别。参照代码：

> https://github.com/karolzak/conv3d-video-action-recognition

经过验证该github代码存在一些逻辑问题，现已经对其进行修改，修改完成之后的复现步骤如下：

1. 下载UCF101

首先要去下载ucf101数据集，有vpn的话可以从官网下载，这里我放一个百度云链接：：https://pan.baidu.com/s/1KOJy-tfAaHRF4PLXSDynGA  提取码：kgg4。一共6.5G,下载完成后解压。

2. 克隆我修改后的github代码：https://github.com/liupeng678/3DCNN-with-keras

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507183655208.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdXBlbmcxOTk3MDExOQ==,size_16,color_FFFFFF,t_70)




3. 按照下图的方式将解压的数据放入dataset:


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507183757510.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdXBlbmcxOTk3MDExOQ==,size_16,color_FFFFFF,t_70)
4.  安装环境:tensorflow,keras, python-ffmpeg, tqdm,或者用我的yml文件直接生成环境(我这里面还有很多其他项目需要的包，而且只装了kerascpu版本，所以不到万不得已不要装我的这个环境)，总之就是缺什么装什么，报错就上google查。

> conda env create -f freeze.yml


5.  运行程序

```
python 3dcnn.py --batch 16 --epoch 80 --videos ./dataset/ --nclass 92 --output 3dcnnresult/ --color True --skip False --depth 8
```
其中./dataset 是数据路径，  depth 是每个视频提取的帧数，这里设置成8， 越多的话精度越高，但是有的视频没有那么多帧，就会报错cv读取了空照片。 nclass 92 是只对./dataset下101文件夹中前92个分类，前期可以设置成3之类快速验证程序是否可运行。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507185037914.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdXBlbmcxOTk3MDExOQ==,size_16,color_FFFFFF,t_70)


6. 调试过程

在运行过程中可能会出现以下几个问题 ： 
**有的视频质量低，导致无法提取足够多的帧**： 需要将depth调小,或者将报错视频文件删除，如果觉得麻烦直接整个文件夹删除可以，但是分类--nclass 92中 92 也要对应少1，因为该分类不能多于文件夹的数量。只能少于。

**keras 报错没有acc或者accurary**: 需要更换keras对应版本下的正确命名，参照https://blog.csdn.net/liupeng19970119/article/details/105963118

**环境问题**： 环境问题需要自己去尝试解决，因为其他问题我没有遇到。


7. 训练结果展示

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507185743468.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdXBlbmcxOTk3MDExOQ==,size_16,color_FFFFFF,t_70)


# 总结

 如果您能跑通代码，或者对您有帮助，麻烦帮我给我个star,蟹蟹！！！！

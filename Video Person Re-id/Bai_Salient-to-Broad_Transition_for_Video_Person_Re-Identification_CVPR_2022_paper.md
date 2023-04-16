# Bai_Salient-to-Broad_Transition_for_Video_Person_Re-Identification_CVPR_2022_paper

### Abstract

这篇论文是关于视频身份识别的，创新点主要有：

1. 使用了SBM，通过利用时间联系信息(temporal information)对输入的后续帧的显著性区域进行抑制，从而让模型将注意力放在之前并不是很显著的区域上。通过这种方法，大大提升了模型显著性区域的范围，提升了模型的鲁棒性。
2. 使用了IDM，使得模型可以更加有效的将所有帧联系起来，提取显著性区域。进而提升了SBM提取显著性区域的能力，SBM因此可以学习到更多的非显著性区域的信息。

### Structure

![image](C:\Users\我的电脑\AppData\Roaming\Typora\typora-user-images\image-20230416153315885.png)

SBM结构如上图所示。输入为t帧图像，前s帧提取显著性区域；后t-s帧抑制前s帧的显著性区域，从而将注意力集中在别的区域，以此扩大显著性区域的范围。

SBM通过前s帧图像提取出显著性区域检测卷积核，用于提取后t-s帧的图像的显著性区域。后t-s帧得到显著性区域之后，通过一些方法（论文里有提到）来对这样的区域进行抑制。最后得到抑制后的图像，然后再通过CPM将前面的显著性区域加上去，得到最终的图像。前s帧则需要加上后t-s帧GAP后的图像（加入后面的非显著性区域）。



![image-20230416165909184](C:\Users\我的电脑\AppData\Roaming\Typora\typora-user-images\image-20230416165909184.png)

IDM结构如上图所示。其实就是简单的autoencoder。通过该操作，可以很好的将显著性区域特证提取出来，然后再根据这些特征重新生成原特征图。

![image-20230416170015683](C:\Users\我的电脑\AppData\Roaming\Typora\typora-user-images\image-20230416170015683.png)

总的结构如上图所示，IDM插入到了第二层。SBM插入到了第三层。backbone为resnet50。
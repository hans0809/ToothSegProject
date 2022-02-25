# 牙齿分割项目
![]('./file/seg_res/color_0047.png')
## 模型说明
> Retinaace: 用于人脸检测。具体的，输入为原图(比如`1280*720`)，输出为包含人脸的`256*256`小图，这些小图将用于接下来牙齿分割器的输入。它加载`weights/office_Resnet50_Final.pth`作为模型权重。

> GhostSeg: 用于牙齿分割。具体的，输入为检测出来的`256*256`小图，输出为`256*256`的分割结果图。它加载`model_best.pth.tar`作为模型权重，加载`GhostSeg/modeling/backbone/state_dict_73.98.pth`作为骨干网络的权重。

## 使用说明
一个完整的牙齿分割过程包括以下三个步骤：
**1. 检测**

将原图存放在`file/original`文件夹下，在`RetianFace`文件夹下运行如下命令:

```shell
python test_widerface.py
```

就完成了人脸检测，得到结果为:

(1)`256\*256`的图片，保存在`file/save256`文件夹下

(2) 每张图片中检测到的人脸位置信息，即bbox的坐标，它们被保存在`file/save_txt/res.txt`。

**2. 分割**
在`GhostSeg`文件下下，运行如下命令:

```shell

python demo.py
```

就完成了对于`/file/save256`文件夹下牙齿图片的分割，得到的分割结果保存在`file/seg_res`文件夹下，此时尺寸是`256*256`的。

**3. 将`256*256`分割结果图转成原尺寸(`1280*720`)分割结果图**
运行:

```shell
python recover.py
```

即可将`/file/seg_res`文件夹下的`256*256`分割结果恢复到原图片尺寸，将结果存储在`file/final_seg_res`文件夹下。



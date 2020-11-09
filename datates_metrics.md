# datesets

**ILSVRC**

ULR：
> http://www.image-net.org/challenges/LSVRC/
>
> https://www.kaggle.com/c/imagenet-object-localization-challenge

**PASCAL VOC**

ULR:
> https://pjreddie.com/projects/pascal-voc-dataset-mirror/
>
> https://www.kaggle.com/zaraks/pascal-voc-2007
>
> https://www.kaggle.com/huanghanchina/pascal-voc-2012

**MS COCO**

ULR:
> https://pjreddie.com/projects/coco-mirror/

**Open Images**

ULR：
> http://storage.googleapis.com/openimages/web/index.html

## 数据格式
### VOC
├── annotations\
│   ├── xxx1.xml\
│   ├── xxx2.xml\
│   ├── xxx3.xml\
│   |   ...\
├── images\
│   ├── xxx1.png\
│   ├── xxx2.png\
│   ├── xxx3.png\
│   |   ...\
├── label_list.txt\
├── train.txt\
└── valid.txt

label_list.txt;类别名称列表;\
每行表示一个类别

train.txt 训练图像列表；\
图像路径+标注路径\
./images/road839.png ./annotations/road839.xml

valid.txt 验证图像列表；\
./images/road218.png ./annotations/road218.xml

xml文件\
filename，表示图像名称\
`<filename>road650.png</filename>`\
size，表示图像尺寸。包括：图像宽度、图像高度、图像深度\
`
<size>
  <width>300</width>
  <height>400</height>
  <depth>3</depth>
</size>
`

object字段，表示每个物体。包括\
`name: 目标物体类别名称`\
`pose: 关于目标物体姿态描述（非必须字段）`\
`truncated: 目标物体目标因为各种原因被截断（非必须字段）`\
`occluded: 目标物体是否被遮挡（非必须字段）`\
`difficult: 目标物体是否是很难识别（非必须字段）`\
`bndbox: 物体位置坐标，用左上角坐标和右下角坐标表示：xmin、ymin、xmax、ymax`

### COCO
是指将所有训练图像的标注都存放到一个json文件中。数据以字典嵌套的形式存放。

annotations/\
├── train.json\
└── valid.json\
images/\
├── road0.png\
├── road100.png

`json文件中存放了 info licenses images annotations categories的信息:`\
`info: 存放标注文件标注时间、版本等信息。`\
`licenses: 存放数据许可信息。`\
`images: 存放一个list，存放所有图像的图像名，下载地址，图像宽度，图像高度，图像在数据集中的id等信息`。\
`annotations: 存放一个list，存放所有图像的所有物体区域的标注信息，每个目标物体标注以下信息`：\
{\
	'area': 899, \
	'iscrowd': 0, \
    'image_id': 839, \
    'bbox': [114, 126, 31, 29], \
    'category_id': 0, 'id': 1, \
    'ignore': 0, \
    'segmentation': []\
}

# metrics
FPS
> 每秒帧数

输出：bbox,类别，置信度

在类别置信度可接受条件下（因为AP对应的是特定的类别，因此当设定好置信度后，满足条件的就是认为已经是该类别的(即类别已配)，因此只计算IOU就能判别TP和FP）

对每个预测Bbox，遍历每个GTbox

TP
> 检测到的目标中是正例（与GT匹配），即类别相等，IOU大于阈值

FP
> 检测到的目标不是正例（与GT不匹配，或真正类别不同），即IOU小于阈值（即使类别正确），类别不正确（即使IOU大于阈值），或IOU和类别均不满足要求    

FN
> GT中未被检测到的

IOU
> '对'或'错',检测到的Bbox与GTbox进行比较
>
> IOU=交/并
>
> IOU>阈值为'对'，IOU小于阈值为'错'

accuracy
> 准确率


precision
> 精度
>
> P=TP/(TP+FP)=TP/(all Pred)
>
> 注：
>> 准确率是与真值的接近程度，精度是测量值之间的准确程度


recall
> 召回率
>
> r=TP/(TP+FN)=TP/(all GT)

p-r curve/AUC
> 不同的置信度值下的p-r曲线及其面积，(IOU阈值不同，PR也不同)
>
> p高r高就是好的算法
>
> **p-r曲线(AUC)记录的是累计的p-r值，是在当前IOU等阈值的情况下计算的p-r值**

AP
> 就是AUC (IOU阈值不同PR不同，AP也不同)
>
> 11点插值，得到AP_11
>
> 全点插值，得到AP_all

mAP
> 度量目标检测器对所有类别的精度，即AP的平均
>
>mAP=1/N * (sum(AP))

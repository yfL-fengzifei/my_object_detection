# **my_object_detection**
obejct detetion notebook

## datesets

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

## metrics
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

precision
> 精度
>
> P=TP/(TP+FP)=TP/(all Pred)

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

# **object detecion**

检测框架!=特征表示



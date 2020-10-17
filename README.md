# my_object_detection
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
TP
> 检测到的目标中是正例（与GT匹配）

FP
> 检测到的目标不是正例（与GT不匹配，或真正类别不同）

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
>P=TP/(TP+FP)=TP/(all Pred)

recall
> 召回率
>
>r=TP/(TP+FN)=TP/(all GT)

p-r curve/AUC
> 不同的置信度值下的p-r曲线及其面积
>
>p高r高就是好的算法
## looking at data
in the train_kana folder, there are lots of useless files with just hundred bytes. They are just too small to be a picture. So I have to remove them.
in powershell:
```
$ Get-ChildItem .*.jpg -Recurse | Remove-Item
```
in linux:
```
$ find . -name ".*.jpg" -type f -delete 
```
## see the accuracy of single character
91% 训练2轮
91% 训练3轮
证明2轮已经开始收敛，loss为0.30左右

## 然后尝试分割字符
连通法肯定不行，因为有连笔。然后水平投影的效果也不好。

## 尝试直接用yolov3或者faster-rcnn 
但没有bound box 数据

7/5
今天把输入的图片size改到了64x64，然后分析的feature也变多了，现在的accuracy已经到了95%。
但是今天考虑到一个问题，就是说准确率是三个字符全对的情况。我这种算法经常会对1个或者2个，但是3个全对的准确率还是很低的。	
train的data上的三字精度：28%
train data single accuracy: 63%

## 分析预测的概率
minmax = (0.09004119, 1.0)
mean = 0.7666338
median = 0.8559627



!python3 detect.py --cfg cfg/kuzushi.cfg --weights weights/best.pt --data-cfg data/kuzushi.data

!python3 train.py --data data/kuzushi.data --cfg cfg/kuzushi.cfg
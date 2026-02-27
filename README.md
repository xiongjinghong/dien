# Deep Interest Evolution Network for Click-Through Rate Prediction
https://arxiv.org/abs/1809.03672
## env
``` 
python=2.7
tensorflow=1.4
```
## prepare data
### method 1
You can get the data from amazon website and process it using the script
```
sh prepare_data.sh
```
### method 2 (recommended)
Because getting and processing the data is time consuming，so we had processed it and upload it for you. You can unzip it to use directly.
```
tar -jxvf data.tar.gz
mv data/* .
tar -jxvf data1.tar.gz
mv data1/* .
tar -jxvf data2.tar.gz
mv data2/* .
```
When you see the files below, you can do the next work. 
- cat_voc.pkl 
- mid_voc.pkl 
- uid_voc.pkl 
- local_train_splitByUser 
- local_test_splitByUser 
- reviews-info
- item-info
## train model
```
python train.py train [model name] 
```
The model blelow had been supported: 
- DNN 
- PNN 
- Wide (Wide&Deep NN) 
- DIN  (https://arxiv.org/abs/1706.06978) 
- DIEN (https://arxiv.org/pdf/1809.03672.pdf) 



相关说明：
- 训练设置和结果可参考 https://github.com/JeremyChou28/DIEN ，另一个参考结果：https://zhuanlan.zhihu.com/p/45325081 可能是训练集和测试集用时间划分的
- Amazon product data https://cseweb.ucsd.edu/~jmcauley/datasets/amazon/links.html
- 训练集：测试集（最后一条数据构建，按用户进行划分，实际使用最好是时间前后划分，user_id 会有用， 也不会特征穿越） = 1086120 + 121216 = 1207336 = 2 * 603668 = 2 倍 user 个数， DIEN 论文中 table 1 数据对应
- DIN 论文中 electronics 数据介绍 和 Amazon product data 中说明 5-score 数据可以对应上
- 1086120/128 = 8500 左右为一个epoch
- 线上服务优化： 38.2 ms to 6.6 ms and the QPS (Query Per Second) capacity of each worker can be improved to 360.

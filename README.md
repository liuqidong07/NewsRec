# 天池新闻推荐入门赛

## 赛题分析

数据包含:30万用户, 36万文章, 300万次点击.
其中20万用户的数据作为训练集, 5万作为测试集A, 5万作为测试集B

### 数据表

train_click_log.csv：训练集用户点击日志

testA_click_log.csv：测试集用户点击日志

articles.csv：新闻文章信息数据表

articles_emb.csv：新闻文章embedding向量表示

sample_submit.csv：提交样例文件

### 字段表

Field	Description

user_id	用户id

click_article_id	点击文章id

click_timestamp	点击时间戳

click_environment	点击环境

click_deviceGroup	点击设备组

click_os	点击操作系统

click_country	点击城市

click_region	点击地区

click_referrer_type	点击来源类型

article_id	文章id，与click_article_id相对应

category_id	文章类型id

created_at_ts	文章创建时间戳

words_count	文章字数

emb_1,emb_2,…,emb_249	文章embedding向量表示

### 结果提交

与sample_submit.csv一致,格式如下:
```
user_id,article_1,article_2,article_3,article_4,article_5
```
表示的是预测用户点击新闻文章的Top5

### 评分方式

$$
MRR = score(user) = \sum^5_{k=1} \frac{s(user,k)}{k}
$$

s(user,k)=1当且仅当预测的5个值中含有最后一个购买记录.



## Datawhale学习

### Task01: 协同过滤

:bookmark_tabs: task01是利用item-based CF来进行解题的.

具体步骤如下:

- 数据集处理: 提取出每一个用户的点击行为序列
- 构建item-item相似度矩阵: 使用Jaccard距离来进行计算
- 利用相似度矩阵来对测试集中的用户的下一次点击进行预测, 给出一个topK列表

_学习链接:_

[天池新闻推荐入门赛之【赛题理解+Baseline】Task01](http://datawhale.club/t/topic/196)

[推荐系统组队学习之协同过滤](http://datawhale.club/t/topic/41)

[推荐系统-协同过滤原理与实现](https://www.cnblogs.com/NeilZhang/p/9900537.html)

### Task02: 数据分析
:bookmark_tabs: task02是对用户的点击行为数据进行分析, 从而去寻找新的特征.

具体步骤如下:

- 用户重复点击分析
- 用户点击环境变化分析
- 用户点击新闻数量的分布
- 新闻点击次数的分布
- 新闻共频次数: 两篇新闻连续出现的次数
- 新闻文章信息
- 用户点击的新闻类型的偏好
- 用户查看文章的长度分布
- 用户点击新闻的时间分析

_学习链接_:

[天池新闻推荐入门赛之【数据分析】Task02](http://datawhale.club/t/topic/197)

## 代码结构

:file_folder: data: 该文件中存放所有的原始数据, 包括train_click_log.csv, testA_click_log.csv, articles.csv, articles_emb.csv, sample_submit.csv

:file_folder: submission: 存放所有结果的提交版本, 命名方式为: time.csv

:file_cabinet: CollaborativeFiltering.ipynb: Task01的所有代码

:file_cabinet: README.md: 本文件




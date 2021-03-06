# PEIA: Personality and Emotion Integrated Attentive Model for Music Recommendation on Social Media Platforms 
## 前言
本文任务在于利用社交平台信息进行音乐推荐，重点捕捉Personality(作者认为这是人们的长期兴趣偏好)和Emotion(短期兴趣)，研究用户的长期偏好和短期兴趣与用户自身人口属性特征之间的交互，非常类似于传统的CTR任务，
不过本文作者将各属性进行细分，分为Personality组、Emotion组、人口属性组，对于用户长期兴趣偏好的捕捉，通过Personality组和人口属性组的特征进行特征交互(feature interaciton)，短期兴趣相似。在特征
交互时，利用层级的注意力机制，直观上理解为两层注意力机制。对于某一层注意力，与传统注意力机制不同，本文中计算注意力分数时使用两层FC，拟合能力更强，但引入了更多参数，训练更慢。对于结果讨论，作者对实验
结果进行几个有意思的讨论，例如，对各特征解耦，分析各特征的重要性，分析年龄段不同对音乐推荐的影响，分析一个人在不同时段的情绪变化。整体工作显得比较充实，同时，作者构建了新的基于社交平台的数据集，这可能
也是本文的模型创新性较少的情况下，可以被收录到AAAI的原因。
## 论文关键论述
* Music, as a significant approach of communication and expression, has been consumed by people as a common daily-life activity.(音乐的重要性，音乐推荐的需求)
* Researches show that people listen to music for multiple purposes, including interpersonal relationships promotion, moods optimization, identity development and surveillance.(研究结果表明，人民听歌受多维度影响)

## 贡献
* We construct a large-scale music recommendation dataset on WeChat, which, compared to existing datasets like MSD (Bertin-Mahieux et al. 2011), contains elaborate personality-oriented user features, emotion-oriented user features and music features for in-depth modeling.
* We reveal several key factors of users’ music preference, e.g. time and age, which may provide reference for music recommendation on social media platforms. 
* We propose a PEIA model which employs hierarchical attention under deep framework to learn the correlations among user personality, user emotion and music, and achieves remarkable performance on a large real-world dataset. 

## 框架图
![PEIA](https://github.com/NiuJiaJun-BUPT/RecommenderSystems/blob/master/Music%20Recommendation/pictures/PEIA_model.jpg)
可以很容易发现，该模型框架是基于Wide&Deep框架，右侧是LR和DNN，左侧可以看成是传统的特征交互部分，作者使用层级注意力的形式，分别提取用户人口属性特征与长期、短期特征的特征交互，得到l_att,s_att后，作者又利用了一层注意力网络，分别获得l_att和s_att的权重，二者加权相加获得z_att

## 存在问题
* 层级注意力那里，注意力分数的计算用了两层fc，明显引入了更多的参数，而且从以前实验来看注意力网络的训练效果并不好，AFM的效果不应该像论文里说的比DeepFM xDeepFM要好

## 可学习的点
* 层级注意力的使用，第二层其实目的就是计算两个Vector之间的权重，但是使用注意力与直接用两个可学习的scalar来说更加个性化，这种看似更复杂的方法，实际上会带来性能提升，更加方便，需要的参数量也较少。

### 论文句式：
  * It is noteable that
	* in a short-term manner. Since music is an emotion-loaded type of content, the emotion context also impacts music preferences, but in a short-term manner.
### 引用句式：
  * (some model）introduces/combines/employs
	* some body proposed/
### 词汇: 
  Moderately adv 1.适度地 有节制地2.普通地；不过度地  A further improves B moderately, demonstrating the  effectiveness of the mechanism in our model.
### 引用文章：

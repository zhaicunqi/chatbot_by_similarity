# chatbot_by_similarity
根据文本相似度实现问答的聊天机器人（弱智版）

## 项目介绍
这是根据工作需求写的一个简易版本的聊天机器人，主要目的是根据问题从知识库中匹配相应的答案从而帮助使用者去更方便的查询到一些知识性内容。<br>

## 模块简介
用法比较简单，给文本列表，经过训练后去匹配问题返回相似的答案。<br>
### 模块结构
* **文本的预处理(cut_text.py)**：用于分词、剔除停用词(这里偷懒直接把长度为1的剔除)；<br>
![](https://github.com/renjunxiang/chatbot_by_similarity/blob/master/picture/cut_texts.jpg)<br>
* **文本转向量(text2vec.py)**：通过word2vec计算词向量，然后求均值转文本向量，空闲的话我会考虑结合tf-idf计算权重优化向量加权方法；<br>
![](https://github.com/renjunxiang/chatbot_by_similarity/blob/master/picture/text2vec.jpg)<br>
* **计算相似度(cal_similarity.py)**：目前只写了最简单的余弦值，空闲的话会考虑加入余弦修正、通过监督学习计算相似度；<br>
![](https://github.com/renjunxiang/chatbot_by_similarity/blob/master/picture/cal_similarity.jpg)<br>
* **聊天机器人的训练与使用(chatbot.py)**：整合前三个步骤，计算问题和知识库每一条知识的相似度，返回排名靠前的知识；<br>

### 模块用法
只需要调用chatbot.py的功能即可，具体参考demo_train.py、demo_ask&answer.py，其中训练语料是一些word文档自行准备，model_word_document.pkl是训练好的模型可以直接使用；<br>
train：训练语料库，输入文本列表 texts=[xxx,xxx]<br>
get_answer：获取答案，输入 ask=问题、threshold=相似度阈值、topn返回知识数量；<br>
``` python
from chatbot import chatbot

texts = ['我爱北京天安门', '我爱北京长城']
chatbot_try = chatbot()
chatbot_try.train(texts=texts)
answer=chatbot_try.get_answer(ask=ask, threshold=0, topn=5)
```
![](https://github.com/renjunxiang/chatbot_by_similarity/blob/master/picture/chatbot.jpg)<br>
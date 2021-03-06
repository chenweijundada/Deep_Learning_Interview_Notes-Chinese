**RodeMap**
---
<!-- TOC -->

- [词向量](#词向量)
- [文本匹配](#文本匹配)
- [阅读理解/问答](#阅读理解问答)
  - [self-attention 实现机制](#self-attention-实现机制)
  - [Reference](#reference)
- [NLP 实践](#nlp-实践)
  - [seq2seq 中 scheduled sampling 怎么做](#seq2seq-中-scheduled-sampling-怎么做)
  - [RL 中的 reward 机制](#rl-中的-reward-机制)
  - [Action 怎么实现的](#action-怎么实现的)
  - [NLP 怎么做数据增强](#nlp-怎么做数据增强)

<!-- /TOC -->

# 词向量

# 文本匹配

# 阅读理解/问答

## self-attention 实现机制


## Reference
- [近期有哪些值得读的QA论文？](https://www.jiqizhixin.com/articles/2018-06-11-14)| 专题论文解读 | 机器之心 

# NLP 实践
## seq2seq 中 scheduled sampling 怎么做

## RL 中的 reward 机制

## Action 怎么实现的

## NLP 怎么做数据增强
- 利用 NMT 做双向翻译——将语言A 翻译到其他语言，再翻译回语言 A

  这个过程相当于对样本进行了改写，使得训练样本的数量大大增加
- QANet 中的做法：
  <div align="center"><img src="../assets/TIM截图20180724200255.png" height="" /></div>

  - 对材料中每个句子通过翻译引擎得到`k`句法语候选，然后将每句法语转回英语，得到`k^2`个改写的句子，从中随机选择一句作为

  - 改写后答案的位置也可能改变，如何寻找**新答案的位置**？

    具体到 SQuAD 任务就是 (d,q,a) -> (d’, q, a’)，问题不变，对文档 d 翻译改写，由于改写后原始答案 a 现在可能已经不在改写后的段落 d’ 里了，所以需要从改写后的段落 d’ 里抽取新的答案 a’，采用的方法是计算 d’ 里每个单词和原始答案里 start/end words 之间的 **character-level 2-gram score**，分数最高的单词就被选择为新答案 a’ 的 start/end word。
    > 中文没有里面没有 character-level 2-gram，可以考虑词向量之间的相似度

    
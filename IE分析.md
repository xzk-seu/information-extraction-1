# 1. lib/get_vocab.py

获取出现次数最多的30000个词汇。

```py
def get_vocab(train_file, dev_file):
    """
    Get vocabulary file from the field 'postag' of files
    获取出现次数最多的30000个高频词

    """

    ......

    value_list = sorted(word_dic.iteritems(), key=lambda d:d[1], reverse=True)
    for word in value_list[:30000]:
        print word[0]
        vocab_set.add(word[0])
```

运行方式：
```
python lib/get_vocab.py ./data/train_data.json ./data/dev_data.json > ./dict/word_idx
```

# 2. 关系分类模型 bin/p_classification
运行方式：
```
python bin/p_classification/p_train.py --conf_path=./conf/IE_extraction.conf
```

## 2.1. bin/p_classification/p_data_reader.py
读取数据
为一个句子构造对应的三个向量：
1、词编码向量（剧中每个词序号的组合，高频词汇按出现频率排序后的序号，前30000，其余为未登录词）
2、词性编码向量 （句子中每个词对应词性在文件中的序号）
3、句子标签，即关系种类 （one-hot）
前两个向量的长度为句子长度，后一个为49，因为一共有49类关系

## 2.2. bin/p_classification/p_model.py
嵌入层：词编码向量和词性编码向量得到词嵌入向量（128维）和词性嵌入向量（20维），作为句子的输入特征；
lstm：512维，8层，双向lstm
池化层：max pooling
输出层：全联接



# 3. 实体标注模型 bin/so_labeling
运行方式：
```
python lib/get_spo_train.py  ./data/train_data.json > ./data/train_data.p
python lib/get_spo_train.py  ./data/dev_data.json > ./data/dev_data.p
```
```
python bin/so_labeling/spo_train.py --conf_path=./conf/IE_extraction.conf
```
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
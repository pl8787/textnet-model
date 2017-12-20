# TextNet Models for Quora Question Pairs #

Deep Text Matching model for [Quora Question Pairs](https://www.kaggle.com/c/quora-question-pairs). 
To refer feature based part, please see [kaggle-quora-question-pairs](https://github.com/HouJP/kaggle-quora-question-pairs).

## Dataset


You can download the dataset from the [Kaggle](https://www.kaggle.com/c/quora-question-pairs/data).

#### Data fields

- id - the id of a training set question pair
- qid1, qid2 - unique ids of each question (only available in train.csv)
- question1, question2 - the full text of each question
- is_duplicate - the target variable, set to 1 if question1 and question2 have essentially the same meaning, and 0 otherwise.

## Preprocess

In order to run TextNet models, we need prepare files below:

#### **Word Dictionary File**   

> *(eg. word_dict.txt)*

We map each word to a uniqe number, called `wid`, and save this mapping in the word dictionary file. 

For example,

```
word   wid
machine 1232
learning 1156
```

#### **Corpus File**    

> *(eg. qid_query.txt and docid_doc.txt)*

We use a value of string identifier (`qid`/`docid`) to represent a sentence, such as a `query` or a `document`. The second number denotes the length of the sentence. The following numbers are the `wid`s of the sentence.

For example,

```
docid  sentence_length  sentence_wid_sequence
GX000-00-0000000 42 2744 1043 377 2744 1043 377 187 117961 ...
```

#### **Relation File**    

> *(eg. relation.train.fold1.txt, relation.test.fold1.txt ...)*

The relation files are used to store the relation between two sentences, such as the relevance relation between `query` and `document`.

For example,

```
relevance   qid   docid
1 3571 GX245-00-1220850
0 3571 GX004-51-0504917
0 3571 GX006-36-4612449
```

#### **Embedding File**    

> *(eg. embed_wiki-pdc_d50_norm)*

We store the word embedding into the embedding file.

For example,

```
wid   embedding
13275 -0.050766 0.081548 -0.031107 0.131772 0.172194 ... 0.165506 0.002235
```

## Config Files

The example config file is [config/quora_blend.config](config/quora_blend.config).

<table>
<tr>
    <th>Config Fields</th>
    <th>File Type</th>
</tr>
<tr>
    <td> data1_file </td>
    <td> Corpus File </td>
</tr>
<tr>
    <td> data2_file </td>
    <td> Corpus File </td>
</tr>
<tr>
    <td> rel_file </td>
    <td> Relation File </td>
</tr>
<tr>
    <td> embedding_file </td>
    <td> Embedding File </td>
</tr>
</table>

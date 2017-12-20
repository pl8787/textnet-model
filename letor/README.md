# TextNet Models for LETOR 4.0 #

Deep Text Matching model for [LETOR 4.0](https://www.microsoft.com/en-us/research/project/letor-learning-rank-information-retrieval/). 

## Dataset

Dataset can be download from [LETOR 4.0](https://www.microsoft.com/en-us/research/project/letor-learning-rank-information-retrieval/).
The content of the documents can be extract from the GOV2 dataset which need permission from [here](http://ir.dcs.gla.ac.uk/test_collections/access_to_data.html).

#### Data Example
```
2 qid:10032 1:0.056537 2:0.000000 3:0.666667 4:1.000000 5:0.067138 … 45:0.000000 46:0.076923 #docid = GX029-35-5894638 inc = 0.0119881192468859 prob = 0.139842
```

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

For **DeepRank** models (such as config/letor.deeprank.pyramid.config and config/letor.deeprank.2dgru.config), we need add some special marks for query-centric contexts.

The ```sentence_wid_sequence``` in document corpus file is the concatenate of all query-centric contexts. 

- **-1**: denotes the padding word.
- **[-10, -inf]**: denotes the query term in the query. -10 represents the first query term, -11 represents the second query term and so on.


For example,

```
docid  sentence_length  sentence_wid_sequence
GX245-00-1220850@0 8702 1421 311 -10 3703 221 2134 
GX245-00-1220860@0 3158 3260 229 -13 2814 -1 -1
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

#### **Feature File**

> *(eg. docid_snippos_sort_none.c1w.feat)*

We store the feature vectors into the feature file.

For example,

```
key feat_vec
GX245-00-1220850@0  0.1143 0.1107 0.1034 0.1006 0.0988 0.0820 0.0774 0.0769 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.1958 0.1599 0.1585 0.1489 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.1594 0.0036 0
```

## Config Files

The example config files are in config directory.

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
<tr>
    <td> feature_file </td>
    <td> Feature File </td>
</tr>
</table>

### DeepRank
this model is an implementation of <a href="https://arxiv.org/abs/1710.05649"> DeepRank: A New Deep Architecture for Relevance Ranking in Information Retrieval </a>

- config file: config/letor.deeprank.pyramid.config
- config file: config/letor.deeprank.2dgru.config

---
### MatchPyramid

this model is an implementation of <a href="https://arxiv.org/abs/1602.06359"> Text Matching as Image Recognition</a>

- config file: config/letor.pyramid.config

---
### Match-SRNN
this model is an implementation of <a href="https://arxiv.org/abs/1604.04378"> Match-SRNN: Modeling the Recursive Matching Structure with Spatial RNN </a>

- config file: config/letor.2dgru.config

---
### ARC-I / ARC-II

this model is an implementation of <a href="https://arxiv.org/abs/1503.03244">Convolutional Neural Network Architectures for Matching Natural Language Sentences</a>

- config config: config/letor.arc1.config
- config config: config/letor.arc2.config

---
### DSSM

this model is an implementation of <a href="https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/cikm2013_DSSM_fullversion.pdf">Learning Deep Structured Semantic Models for Web Search using Clickthrough Data</a>

- config file: models/letor.dssm.config

---
### CDSSM

this model is an implementation of <a href="https://www.microsoft.com/en-us/research/publication/learning-semantic-representations-using-convolutional-neural-networks-for-web-search/">Learning Semantic Representations Using Convolutional Neural Networks for Web Search</a>

- config file: models/letor.cdssm.config




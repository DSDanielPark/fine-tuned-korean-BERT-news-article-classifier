# Korean-news-topic-classification-using-KO-BERT
[![Python Version](https://img.shields.io/badge/python-3.6%2C3.7%2C3.8-blue.svg)](code_of_conduct.md)
![Code convention](https://img.shields.io/badge/code%20convention-pep8-blue)
![](https://img.shields.io/badge/linting-pylint-yellowgreen)


> ๐ธ **Be careful when cloning this repo**: It contains large NLP model weight. (>0.3GB, [`git-lfs`](https://git-lfs.com/))

<br> 

Overview: Repository class diagram (`packages.dot`)
- For resource reasons, [KOBERT](https://sktelecom.github.io/project/kobert) was used as a submodule which are the following two folders. 
- `src/kobert`, `src/kobert_hf` (Red nodes in graphviz)

![](https://github.com/DSDanielPark/fine-tuned-korean-BERT-news-article-classifier/blob/main/data/imgs/fine-tuned-korean-BERT-news-article-classfier-packages-diagram.png)

<br>

## TASK: Multi-category(8 classes) Korean News Topic Classifier 
ํ๊ธ ๋ด์ค ํ ํฝ ๋ค์ค ๋ถ๋ฅ ๋ชจ๋ธ <Br>
- Perform a simple task to compare the performance of KO-BERT and implementations of BERT in different frameworks <br>
- FrameWork: `PyTorch`, `APACHE MXNET GluonNLP` and `Hugging-Face` for modeling, `Scikit-Learn` to calculate evaluation metric.
- Pre-trained model: [`KO-BERT`](https://github.com/SKTBrain/KoBERT), `BERT`, [`SBERT`](https://www.sbert.net/)
- Dataset: Korean News Topic Classification Dataset (ํน์  ํ์ฌ์์ ์์งํ์ฌ ๋น๊ณต๊ฐ๋ก ์ ๊ณต) <br>
- Evaluation: Accuracy <br>
- Duration: Jan 16,2023 - Jan 19,2023 (4days) <br>
- Author: [Daniel Park, South Korea](https://github.com/DSDanielPark) <br>

<br>

# TL;DR
### Sub Task 
- (ํ๋ ์์ํฌ ๋น๊ต) `GluonNLP`, `PyTorch`, `Hugging-Face` ํ๋ ์์ํฌ์ BERT ๋ชจ๋ธ ๊ตฌํ ๋น๊ต
- (์ธํ ์ ๋ณด๋์ ๋ฐ๋ฅธ BERT Classifier์ ์ฑ๋ฅ ๋น๊ต) ๋ด์ค์ ์ ๋ชฉ, ์ ๋ชฉ+๋ณธ๋ฌธ, ๋ณธ๋ฌธ์ ์ธํ์ผ๋ก ์ฌ์ฉํ์์ ๊ฒฝ์ฐ์ ๋ชจ๋ธ ๋ถ๋ฅ ์ฑ๋ฅ ์ ๋์  ๋น๊ต
- (์ฌ์  ๊ตฐ์งํ์ ๋ณด์ ๋ฐ๋ฅธ ๋ชจ๋ธ ํ์ต ์๋ ๋น๊ต) Multilingual-BERT(SBERT)๋ฅผ ํตํด ์ฌ์ ์ ๊ตฐ์ง ์ ๋ณด๋ฅผ ์ฃผ์์ ๊ฒฝ์ฐ, ๋ชจ๋ธ์ ํ์ต ์๋๊ฐ ๋ฌ๋ผ์ง๋์ง ์ฌ๋ถ ๋น๊ต
  - PyTorch์ ๊ฒฝ์ฐ, initial [CLS] ํ ํฐ์ ์ ๋ณด๋ฅผ ์๋ฒ ๋ฉํ๊ณ 
  - GluonNLP์ ๊ฒฝ์ฐ, ์ ์ฒ๋ฆฌ ๋จ๊ณ์์ ๊ตฐ์ง์ ๋ํ ์ ๋ณด๋ฅผ ์ธํ์ ์ฝ์ํ์ฌ ๋น๊ต
### ๋ณธ ๋ ํฌ์งํ ๋ฆฌ๋
- 'Fine-tuned MXNet GluonNLP BERT Classifier weight file(`weights/ko-news-clf-gluon-weight.pth`)'์ `git-lfs`์ ํตํด์ ์ ๊ณตํ๊ณ , 'Sample csv file for inference(`data/sample.csv`)'๋ฅผ ์ ๊ณตํฉ๋๋ค. 
- ์ถํ ๋ฒ์ฉ์ ์ผ๋ก ์ฌ์ฉํ  ์ ์๋ ํจํค์ง pypi๋ฅผ ํตํด ๋ฐฐํฌํฉ๋๋ค. 
- To-Do: Hugging Face ํ๋ ์์ํฌ, XAI, GPT2, GPT3, BERT Pipeline etc.


<br><br><br>

## Repository folder tree
```
๐ฆfine-tuned-korean-BERT-news-article-classifier 
 โฃ ๐data
 โ โฃ ๐csv
 โ โฃ ๐imgs
 โ โฃ ๐sample.csv                          # for inference (project input)
 โ โฃ ๐test_set.csv
 โ โ ๐train_set.csv
 
 โฃ ๐experiments                           # dummies for experiments
 โ โฃ ๐experiment_weights
 โ โฃ ๐exp.md
 โ โ ๐exp_metric.md
 
 โฃ ๐notebooks                             # for developing features (will NOT be provided)

 โฃ ๐src
 โ โฃ ๐kobert                              # SKT KOBERT / references[2, 3]
 โ โฃ ๐kobert_gluon                        # gloun nlp ์คํ์ ์ํ ๋ชจ๋
 โ โฃ ๐kobert_hf                           # SKT KOBERT / references[2, 3]
 โ โฃ ๐kobert_pytorch                      # torch bert ์คํ์ ์ํ ๋ชจ๋
 โ โฃ ๐preprocess                          # ๋ณธ ๋ ํฌ์งํ ๋ฆฌ ์คํ์ ์ํ ์ ์ฒ๋ฆฌ ๋ชจ๋

 โฃ ๐weights
 โ โฃ ๐ko-news-clf-gluon-weight.pth        # will be provided throught git-lfs (>0.3 GB), MODE==2
 โ โ ๐ko-news-clf-torch-weight.pth        # will NOT be provided (>1.0 GB), MODE==2

 โฃ ๐.gitattributes                        # git-lfs managing
 โฃ ๐.gitignore
 โฃ ๐config.py                             # config
 โฃ ๐LICENSE
 โฃ ๐main.py                               # main.py (gluon inference๋ง ์ ๊ณต)
 โฃ ๐README.md
 โ ๐requirements.txt
```




<br><Br>
## [Optional] Related Packages
#### 1. [`QuickShow`](https://pypi.org/project/quickshow/): A package to quickly and easily visualize a pandas.DataFrame as input
```bash
$ pip install quickshow
```
- ์ด๋ฒ ํ๋ก์ ํธ์ ํ์ฉ๋ ์ผ๋ถ ์๊ฐํ ๋ชจ๋์ ๋ฐฐํฌํ์์ต๋๋ค. ์ง๊ธ๊น์ง ์ฌ๋ฌ ํ๋ก์ ํธ์์ ์ฌ์ฉ๋ ๋ค์ํ ๋ชจ๋์ ํธ๋ฆฌํ๊ฒ ๋ํํ์ฌ ์ถํ ๊ณ์ ์๋ฐ์ดํธํ  ์์ ์๋๋ค.

#### 2. [`CorpusShow`](https://pypi.org/project/corpusshow/): Corpus-Show helps to understand the corpus data distribution through various values generated from NLP sentence embedder.
```bash
$ pip install corpusshow
```
- corpusshow[์ฝ๋ฟ:์] ํจํค์ง๋ Sentence Transformer ๊ธฐ๋ฐ์ผ๋ก ์ฝํผ์ค๋ฅผ ํด๋ฌ์คํฐ๋งํด์ ์๊ฐํํ๊ฑฐ๋ ๋ ์ด๋ธ๊ณผ ํจ๊ป Embedded Sentence๋ฅผ ์ฝ๊ณ  ๋น ๋ฅด๊ฒ ์๊ฐํํ  ์ ์์ต๋๋ค.


<br><br>

## Quick Start
๋ณธ ๋ ํฌ์งํ ๋ฆฌ๋ highly encapsulated inference class for bert classifier๋ฅผ ํฌํจํฉ๋๋ค.
```
$ git clone https://github.com/DSDanielPark/fine-tuned-korean-BERT-news-article-classifier.git
$ cd fine-tuned-korean-BERT-news-article-classifier
$ pip install -e .
$ python main.py
>>> Predicted news topic: international
```


<Br>

You can use follow optional args.
```
for gluon weight inference only

optional arguments:
  -h, --help            show this help message and exit
  --gluon_weight_path GLUON_WEIGHT_PATH                        # glouon weight file path
  --data_path DATA_PATH                                        # input csv data path
  --save_path SAVE_PATH                                        # save csv file full path
```

<br>
<br>

## Outline
- **Problem Definition:** 
<br> Create a model that classifies articles into the following 8 categories with the title and body as input.
<br> `Categories` = ['society', 'politics', 'international', 'economy', 'sport', 'entertain', 'it', 'culture'] <br><br>
- **Data Description:**
<br> The Total 3,000 korean news dataset(Train: 2,100 articles, Test 900: articles, 7:3 split) consist of title, body and category columns. <br><br>


        ```
        title: korean article title
        cleanBody: korean article body
        category: of article (eight classes)
        ```



  |  | title |cleanBody|category|
  |---:|:---|:---|:---|
  |  0 | ๋ณด๊ฑด๋ณต์ง๋ถ, ์ํด ์ฒญ๋๊ณผ ์ง์ญ์ด ํจ๊ป ์ง์ญ์ฌํ์๋น์ค๋ฅผ ๊ฐ๋ฐ์ ๊ณตํด ์ฌํ์๋น์ค ๊ณ ๋ํ์ ์์ฅ์ | ๋ณด๊ฑด๋ณต์ง๋ถ(์ฅ๊ด ์กฐ๊ทํ)๋ 2023๋ ์ฒญ๋์ฌํ์๋น์ค์ฌ์๋จ(์ดํ โ์ฒญ๋์ฌ์๋จโ)์ ์  ๋ฐ ์ด์์ ์ํด ์ค๋ 1์ 27์ผ(๊ธ)๋ถํฐ 2์ 15์ผ(์)๊น์ง ์ฝ 3์ฃผ๊ฐ ์ ๊ตญ 17๊ฐ ์๋(๊ด์ญ ์ง์์ฒด)๋ฅผ ๋์์ผ๋ก ์ฒญ๋์ฌ์๋จ ๊ณต๋ชจ๋ฅผ ์ค์ํ๋ค๊ณ  ๋ฐํ์ต๋๋ค. ...(์ค๋ต)... ๋ณธ ๊ธฐ์ฌ๋ ๊นํ๋ธ ๋ฐ์ดํฐ ์์๋ฅผ ์ํด ๋ณด๊ฑด๋ณต์ง๋ถ ๋ณด๋์๋ฃ๋ฅผ ์ฐธ์กฐํ์ฌ ์์ฑํ์์ต๋๋ค. | society    |
  |  1 | BTS, 10๋๊ฐ ๋น๋ณด๋ 'Hot 100' ์ฐจํธ 1์๊ณก ์ต๋ค ๋ณด์  ๊ฐ์๋ก ๊ธฐ๋ก๋ผ | ๋ฐฉํ์๋๋จ(์ดํ "BTS")๊ฐ ๋ฏธ๊ตญ ๋น๋ณด๋ ๋ฉ์ธ ์ฑ๊ธ ์ฐจํธ 'HOT 100'์ ์ ์์ ๊ฐ์ฅ ๋ง์ด ์ค๋ฅธ ์ํฐ์คํธ๋ก ์ ์ ๋์์ต๋๋ค. BTS๊ฐ ๋ฏธ๊ตญ ์ ๋ช ๊ฐ์ ๋๋ ์ดํฌ๋ ์๋ฆฌ์๋ ๊ทธ๋๋ฐ ๋ฑ์ ์ ์น๊ณ , ๋ฉ์ธ ์ฑ๊ธ ์ฐจํธ ํซ 100์ ์ฌ๋ผ ๋ค์ ํ๋ฒ K-POP์ ์์์ ์ธ์์ ๋จ์ณค์ต๋๋ค. ...(์ค๋ต)... BTS๋ ์๋ก์ด ์์๊ณผ ์๋ฌด๋ก ๋ค์ ์ปด๋ฐฑ์ ์๊ณ ํ๊ณ  ์์ต๋๋ค. ์ด์ ๊นํ๋ธ ๋ด์ค ๋ค๋์ ๊ธฐ์์์ต๋๋ค. | international |


<br><Br>

- **EDA:**
<br> I analyzed the quality of the data, but I couldn't find any outliers because it was a very well-refined dataset. 
<br> Since this data was processed for a specific purpose by a Korean IT company, data preprocessing was unnecessary. 
<br> Replace the next image with data analysis.
<br><Br>
<img src="./data/imgs/fig.png" width="600"> <br> *Fig 1. ํ์คํธ์๊ณผ ํธ๋ ์ธ ์์ ๋ฐ์ดํฐ ๋ถํฌ(์ด ํ์คํฌ์ ๊ฒฝ์ฐ, ์ถ๊ฐ์ ์ธ ๋ฐ์ดํฐ ์์ง ๋ฐ ํ์ต์ด ์ฉ์ดํ๋ฏ๋ก imbalance๋ ๊ณ ๋ คํ์ง ์์)*
<br><br>
  - Since the advent of large-scale natural language processing models, feature engineering on corpus has not been of great significance.
  - In `MODE 4` and `MODE 5`, a test was conducted to give some information on the similarity of articles in advance through k-mean clustering based on the tokens embedded from the pre-trained BERT model.

  <br>

- **BERT Features list:**
  1. *input_ids* - are the ids associated with each token as per BERT vocabulary.
  2. *input_mask* - differentiate between padding and real tokens.
  3. *Segment_ids* - will be a list of 0โs, as in classification task there is only a single text.
  4. *label_id* - corresponds to Label Encoder classes
<br><br>



# Results
All model architecture and learning conditions in the whole pipeline were fixed except the initial layer in MODE5. <br>
- Mode1 to Mode4: `MXNet` Framework
- Mode5: `Pytorch` Framework to modify the initial layer
- Pre-trained Models are KO-BERT [3], SBERT [5].

  | |`MODE 1`|`MODE 2`|`MODE 3`|`MODE 4`|`MODE 5`|
  |:---:|:---:|:---:|:---:|:---:|:---:|
  |Data|article body only|articel title only|article with title|article with title which have clustered information from SBERT model|article with title|
  |Model|KO-BERT|KO-BERT|KO-BERT|KO-BERT, SBERT|KO-BERT, SBERT with clustered information in initial hidden layer|
  |TestSet Accuracy|0.8895|0.8269|0.8864|0.8895|-|
  |Remark|Model architecture and all conditions in models were fixed.|-|-|-|Model architecture and initial layer are changed only in `MODE5`.|
- As I mentioned in the 'Experiments' section, All conditions in the whole pipeline were fixed except the initial layer in MODE5 and Pre-trained Models were KO-BERT [3], SBERT [5].



<br><br>


## Experiments




- ์คํ์ ํฌ๊ฒ ๋ค์ 4๊ฐ์ง ๊ฐ์ค์ ํ์ธํ๊ธฐ ์ํ์ฌ ์ค๊ณ๋์์. <br>
  1) ํ๊ธ ๊ธฐ์ฌ์ ๋ณธ๋ฌธ, ์ ๋ชฉ, ๋ณธ๋ฌธ๊ณผ ์ ๋ชฉ์ ํตํ ๋ถ๋ฅ ์ฑ๋ฅ์ ์ฐจ์ด ํ์ธํ๊ณ ์ ์ค๊ณ๋จ - `MODE1~MODE3`
  2) ์ผ์ข์ ์ง์์ฆ๋ฅ๋ฅผ ํตํ KO-BERT์ ๋ฏธ์ธ ์กฐ์ (fine-tunning) ๊ณผ์ ์์ Teacher Model(SBERT)๋ก ๋ถํฐ ์์ฑํ ๊ตฐ์ง์ ๋ํ ์ ๋ณด๊ฐ ๋ชจ๋ธ ์๋ ด์ ์ผ๋ง๋ ์ํฅ์ ์ค ์ ์๋์ง ํ์ธํ๊ณ ์ ์ค๊ณ๋จ - `MODE3~MODE4`
  3) 2๋ฒ์ ๊ณผ์ ์์ SBERT๋ก ์์ฑ๋ ์ ๋ณด(๊ตฐ์ง์ ์)๊ฐ ์ผ๋ง๋ ์ณ์์ง(๋์ผํ ํด๋์ค๊ฐ ๋์ผ ๊ตฐ์ง์ผ๋ก๋ง ๊ตฌ์ฑ๋์ด ์๋์ง)๊ฐ ๋ชจ๋ธ ํ๋ผ๋ฏธํฐ ๋ฏธ์ธ์กฐ์ ์ ์ํฅ์ ์ฃผ๋์ง ํ์ธํ๊ธฐ ์ํด ์ค๊ณ๋จ - `MODE4`: `EXP8~EXP11`
  4) ๋ง์ง๋ง์ผ๋ก SBERT๋ก๋ถํฐ ์์ฑ๋ ์ ๋ณด๋ฅผ ๋ชจ๋ธ ์ธํ์ผ๋ก ์ฃผ์์ํค๋ ๊ฒ๊ณผ initial hidden layer์ ์ฃผ์์ํค๋ ๊ฒ์ ์ฐจ์ด๋ฅผ PyTorch์ MXNet ํ๋ ์์ํฌ๋ฅผ ํตํด ๋น๊ตํจ - `MODE4~MODE5`

<br>
<br>


<details>
<summary> See detail</summary>


The Mode 1, Mode 2, and Mode 3 experiments were designed to see how well a subject could classify 8 topics into the body and headlines of a news article.
  - `MODE 1`: It learns data containing only the body of news articles as input.
  - `MODE 2`: It learns data containing only news article titles as input.
  - `MODE 3`: It learns data containing both news article titles and body as input.

<br>

Mode 4 and Mode 5 are designed to create and experiment with a kind of distilBERT model.
- This experiment is designed *to see if it can be fine-tuned a bit faster based on the clustering information generated by SBERT.*
- In this experiment, the information clustered by SBERT, a multilingual model, is used to fine-tune the KO-BERT model.
  - `MODE 4`: Cluster information generated from SBERT, a multilingual model, is used as model input, and this experiment used the mxnet framework in the same way as Modes 1 to 3.
  - `MODE 5`: Clustering information generated from SBERT was input to the initial layer using the PyTorch framework. The results of this experiment may be slightly different from Modes 1 to 4, so they are not described.
    - However, as in Mode 4, it was confirmed through several iterations that almost similar accuracy can be reached faster if you have cluster information generated from SBERT.

</details>


- You can see whole experiments result in [`experments/exp.md`](https://github.com/DSDanielPark/fine-tuned-korean-BERT-news-article-classifier/blob/main/experiments/exp.md) 
- In the case of EXP2 and EXP9, it was repeatedly performed to track and observe the learning rate, confirming similar learning patterns.

  | No | Condition | Best Test Accuracy | Epoch | 
  |:---:|:---|:---:|:---:|
  EXP1 | mode=1, batch_size=32 | 0.8842 | at Epoch 10
  EXP2 | mode=1, batch_size=32, epoch=20 without early stopping. | 0.8895 | at epoch 12
  EXP3 | mode=1, batch_size=16 | 0.8800 | at epoch 4
  EXP4 | mode=1, batch_size=32 repeat of exp1 for check effect of randomness. | 0.8864 | at epoch 7
  EXP5 | mode=1, batch_size=32 | 0.8874 | at epoch 7 
  EXP6 | mode=2, batch_size=32 | 0.8269 | at epoch 7
  EXP7 | mode=3, batch_size=32 | 0.8864 | at epoch 6
  EXP8 | mode=4, batch_size=32, cluster_numb=8 | 0.8789 | at epoch 3
  EXP9 | mode=4, batch_size=32, cluster_numb=16 | 0.8895 | at epoch 5
  EXP10 | mode=4, batch_size=32, cluster_numb=32 | 0.8641 | at epoch 2
  EXP11 | mode=4, batch_size=32, cluster_numb=64 | 0.8885 | at epoch 7

<br>
<br>



# Evaluation
You can see evaluation metric of whole experiments in [`exp/exp_metric.md`](https://github.com/DSDanielPark/fine-tuned-korean-BERT-news-article-classifier/blob/main/experiments/exp_metric.md).

 <img src="./data/imgs/result.png" width="1000"><BR> *Fig 2. ๊ฐ ์คํ๋ณ F1 score, Recall, Precision*

<br><br>
<br><br>์ฐธ๊ณ .
 F1 score is a performance metric for classification and is calculated as the harmonic mean of precision and recall.

<p align="center">
  <img src="./data/imgs/recall_precision.png" width="500"><br> 
  
</p>

*Fig 3. Reference figure to explain Recall, Prcision, Accuracy / Maleki, Farhad & Ovens, Katie & Najafian, Keyhan & Forghani, Behzad & Md, Caroline & Forghani, Reza. (2020). Overview of Machine Learning Part 1. Neuroimaging Clinics of North America. 30. e17-e32. 10.1016/j.nic.2020.08.007.*
 <br>

<br>

## Confusion Metrix and Heatmap in`EXP5` for each topic.
์ ์ฒด์ ์ธ ๊ฒฐ๊ณผ๋ [`exp/exp_metric.md`](https://github.com/DSDanielPark/fine-tuned-korean-BERT-news-article-classifier/blob/main/experiments/exp_metric.md)์ ๊ณต๊ฐํ์์ผ๋ฉฐ, Evaluation ๋ํ๋ฅผ ํตํด ์ถฉ๋ถํ ๊ฒฐ๊ณผ์ ๋ํ ์ ์ถ๊ฐ ๊ฐ๋ฅํ๋ฏ๋ก ๋ชจ๋  ์คํ์ ๋ํ Confusion Metrix ์ ๊ณต์ ์๋ตํ๋ฉฐ, ๋ค์ ์์๋ฅผ ํตํด ๊ฐ์ํจ.
<br>

1. Classification report

    | Topic |   Precision |   Recall |   F1-Score |    Support |
    |:--------------:|:------------:|:---------:|:-----------:|:-----------:|
    | Culture       |    0.833333 | `0.666667` |   0.740741 |  `15`        |
    | Economy       |    0.693878 | 0.871795 |   0.772727 | 117        |
    | Entertain     |    0.868132 | 0.963415 |   0.913295 |  82        |
    | International |    0.878049 | 0.870968 |   0.874494 | 124        |
    | IT            |    0.722222 | 0.722222 |   0.722222 |  18        |
    | Politics      |    0.965278 | 0.798851 |   0.874214 | 174        |
    | Society       |    0.874101 | 0.823729 |   0.848168 | 295        |
    | Sport         |    0.906977 | `1.000000`        |   0.95122  | `117`        |```

    |  avg  |   |   |    |     |
    |:--------------:|:------------:|:---------:|:-----------:|:-----------:|
    | accuracy      |    0.860934 | 0.860934 |   0.860934 |   0.860934 |
    | macro avg     |    0.842746 | 0.839706 |   0.837135 | 942        |
    | weighted avg  |    0.86909  | 0.860934 |   0.861426 | 942        |

<br>

2. Heatmap 

    <img src="./data/imgs/cm_exp5.png" width="500"> <br>
    *Fig 4. Heatmap of Confusion Metrix in `EXP5`*



<br>
<br>

# Embedding Token Visuallization<br>

  #### **1. SBERT๋ก๋ถํฐ ์์ฑ๋ ํ ํฐ์ ์ ํด๋ฆฌ๋์ ๊ฑฐ๋ฆฌ๋ฅผ ํตํด K-means ๊ตฐ์งํ๋ฅผ ์ํํ  ๊ฒฝ์ฐ, ํด๋ฌ์คํฐ ์ ๋ณ Ground Truth Category ๋ถํฌ ์๊ฐํ**

  - ํ๋์ y-tick ๋ฐด๋ ์ฌ์ด๊ฐ ๊ฐ ๊ตฐ์ง์ ์๋ฏธ
  - ๊ตฐ์ง์์ ์นดํ๊ณ ๋ฆฌ๊ฐ ์์ ๊ฒฝ์ฐ ์๊ฐํ๋์ง ์์ผ๋ฏ๋ก ๋ฐด๋๊ฐ ์ข์์๋ก ์กด์ฌํ๋ Ground Truth Category์ ๊ณ ์ ๊ฐ์ ์๊ฐ ์ ์์ ์๋ฏธ
  - ์ ์ฒด ํ์ด๋ธ์ [`csv`](https://github.com/DSDanielPark/fine-tuned-korean-BERT-news-article-classifier/blob/main/data/csv)ํด๋ ์์์ ํ์ธ

    <img src="./data/imgs/cluster8.png" width="220" height='200'> <br>
    <img src="./data/imgs/cluster16.png" width="450" height='200'><br>
    <img src="./data/imgs/cluster32.png" width="900" height='200'><br>
    *Fig 5. ํด๋ฌ์คํฐ๋ณ Ground Truth Label์ ๋ถํฌ. ์์์๋ถํฐ ์๋ ์์๋ก 8, 16, 32๊ฐ์ cluster๋ก ๊ตฐ์งํํ ๊ฒฐ๊ณผ, ํ๋ ๋ฐด๋๊ฐ Cluster์ ๊ฒฝ๊ณ๋ฅผ ์๋ฏธํ๋ฉฐ, ๋ฐด๋ ์ฌ์ด(ํด๋ฌ์คํฐ๋ณ) Ground Truth Category์ ๋ถํฌ์ ๋๋ฅผ ํ์ํจ.*

    <details>
    <summary> See detail</summary>


    - SBERT๋ก ์ฌ์ ์ ๊ตฐ์ง์ ๋ํ ์ ๋ณด๋ฅผ ์ด์ํ์ฌ, KO-BERT์ fine-tunning์ ์งํํ์๋๋ฐ, EXP8๋ถํฐ EXP11๊น์ง 8๊ฐ(`EXP8`)๋ถํฐ 64๊ฐ(`EXP11`)๊น์ง ๊ตฐ์ง์ ๋ํ ์๋ฅผ ๋ณ๊ฒฝํ์ฌ ๋ด. (64๊ฐ์ ๊ฒฝ์ฐ ์ ์๋ฏธํ ์ฐจ์ด๊ฐ ์์ผ๋ฏ๋ก ํด๋ฌ์คํฐ๋ณ Ground Truth Label์ ๋ถํฌ ์๊ฐํ๋ฅผ ์๋ต)
    - ์คํ๊ฒฐ๊ณผ๋ ๊ธฐ๋์ ๋์ผํ๊ฒ 8๊ฐ์ ๊ตฐ์ง์ ๊ฒฝ์ฐ, ๊ตฐ์ง์ด ์ถฉ๋ถํ ์ ์ฌํ ๊ธฐ์ฌ๋ค์ ๋ฌถ์ด๋์ง ๋ชปํ์๊ณ (ํด๋ฌ์คํฐ์ ์๊ฐ ๋๋ฌด ์ ์),  32๊ฐ ์ด์์ผ๋ก ๊ณผํ๊ฒ ๊ตฐ์งํํ์์ ๊ฒฝ์ฐ, ๋๋ฌด ๋ง์ ๊ตฐ์ง์ ์๋ก ์ธํด ๋ชจ๋ธ ํ์ต์ ์ข์ง ์์ ์ํฅ์ ๋ฏธ์น ๊ฒ์ผ๋ก ๋ณด์.
    - SBERT๋ก ์์ฑ๋ ํ ํฐ์ ์ ์ฌ๋๋ฅผ ์๋ฒ ๋ฉํด์ฃผ๋ ๊ฒ์ด KO-BERT fine-tunning์ ์ํฅ์ ์ค ์ ์๋์ง ํ์ธํ๋ ๋ชฉ์ ์ด์์ผ๋ฏ๋ก, ์ถ๊ฐ์ ์ธ ์ต์  ๊ตฐ์ง์๋ฅผ ๋์ถ์ ๋ถ์.
    - ๋๋ฌด ์ ์ ๊ตฐ์ง์ ์(<=the number of classes)๋ ๋๋ฌด ๋ง์ ๊ตฐ์ง์ ์(>=4 times the number of classes)๋ ๋ชจ๋ธ ํ์ต์ ์ข์ ์ํฅ์ ๋ฏธ์น์ง ์์ ๊ฐ๋ฅ์ฑ์ ํ์ธํจ.
    - `EXP4`,`EXP11`์ ๊ฒฐ๊ณผ์ ํ์ต ์์์ด ๋น์ทํ๋ฏ๋ก ๋๋ฌด ๊ตฐ์ง์ ์๊ฐ ๋ง์ EXP11์์๋ KO-BERT์ ๋ฏธ์ธ์กฐ์ ์ SBERT๋ก๋ถํฐ ์์ฑ๋ Cluster์ ๋ณด๋ฅผ Representation์ผ๋ก ์ฌ์ฉํ์ง ์์ ๊ฒ์ผ๋ก ์ถ์ ํจ. 
    - `MXNET` ํ๋ ์์ํฌ์์๋ ์ธํ ๋ฐ์ดํฐ์ ๊ตฐ์ง์ ๋ํ ์ ๋ณด๋ฅผ ์ฝ์ํ๋ ๊ฒ์ผ๋ก ๊ตฌํํ์๊ณ , `PyTorch` ํ๋ ์์ํฌ์์๋ initial layer์ ๊ตฐ์ง์ ๋ํ ์ ๋ณด๋ฅผ [CLS] ํ ํฐ์ ์๋ฒ ๋ฉํ์ฌ initial hidden layer์ ์ ๋ณด๋ฅผ ์ฝ์ํ์์ผ๋ฉฐ, ํ๋ ์์ํฌ์ ์๊ด์์ด ์กฐ๊ธ ๋ ๋น ๋ฅด๊ฒ, ๋์ ์ฑ๋ฅ์ ๋๋ฌํ  ์ ์๋ ๊ฒ์ ํ์ธํจ.
      

    </details>

  <br>
  <br>
  

  
  
  
  <br>

  #### **2. SBERT๋ก๋ถํฐ ์์ฑ๋ ํ ํฐ ์๊ฐํ** <br>

  <details>
  <summary> See detail</summary>

  Multilingual BERT Embedding Space์ ๋ํ ์ฐ๊ตฌ[[10]](https://aclanthology.org/2022.findings-acl.103.pdf)์ Recommender Systems์์์ Embedding Space์ ๋ํ ์ฐ๊ตฌ[[11]](https://arxiv.org/abs/2105.08908)์ ๋น์ทํ๊ฒ Token์ด ์กฐ๊ธ ๋ Isotropicํ ๋ถํฌ๋ฅผ ๋ณด์ด๋ ๊ฒ์ด ์ข์ ์ฑ๋ฅ์ ๋ํ๋ธ ๊ฒ์ ํ์ธํ  ์ ์์๋ค. ๋ณธ ๋ ํฌ์งํ ๋ฆฌ์์ ํ ํฐ ์๊ฐํ์ ์ฌ์ฉํ SBERT ์ญ์ Multilingual BERT์ด๋ฏ๋ก ์๊ธฐ[10]์ ๋ผ๋ฌธ๊ณผ ๋น์ทํ ํ๊ฒฝ์์์ ์คํ์ด๋ผ๊ณ  ๊ฐ์ ํ๋ ๊ฒ์ ํฐ ๋ฌด๋ฆฌ๊ฐ ์์ ๊ฒ์ผ๋ก ํ๋จํ์๋ค. <br> <br>์ ๋ชฉ์ผ๋ก๋ถํฐ ์์ฑ๋ Embedding Space์์์ Token์ ๋ถํฌ๊ฐ ์กฐ๊ธ ๋ isotropicํ ๊ฒ์ ํ์ธํ  ์ ์์์ผ๋ฉฐ, ์ค์ ๋ก `EXP6`(๊ธฐ์ฌ์ ์ ๋ชฉ๋ง์ผ๋ก ํ์ต)๊ณผ `EXP7`(๊ธฐ์ฌ์ ๋ณธ๋ฌธ๋ง์ผ๋ก ํ์ต)์ ๊ฒฐ๊ณผ๋ฅผ ๋ณด๋ฉด Accuracy `0.8269`์ `0.8864`๋ก ์ฝ `0.595` ๋ ๋์ ์ ํ๋๋ฅผ ๋ณด์ด๋ ๊ฒ์ ํ์ธํ  ์ ์์๋ค. 
  <br><br>
  ๊ฒฐ๊ณผ์ ์ผ๋ก BERT์ fine-tunning ํ์คํฌ ์ด์ ์ Low Dimension(2DIM or 3DIM) Space๋ก ์๊ฐํํ์ฌ ์กฐ๊ธ ๋ isotropic token ๋ถํฌ๋ฅผ ๊ฐ๋ ๋ฐ์ดํฐ์์ด๋ ์ ์ฒ๋ฆฌ ๋ฐฉ๋ฒ์ ์ฐพ๋ ๊ฒ์ด ์กฐ๊ธ ๋ ์ข์ ๋ชจ๋ธ ํ์ต ๊ฒฐ๊ณผ๋ฅผ ๋ณด์ผ ์ ์์ ์ ์์์ ์์ฌํ๋ค. <br><br>

  </details>


  2-1 ๊ธฐ์ฌ์ ์ ๋ชฉ์ผ๋ก๋ถํฐ ์์ฑ๋ ํ ํฐ ์๊ฐํ
  <img src="./data/imgs/title_token_vis.png" width="1000"><br>
  *Fig 6. Visualization of embedded tokens from SBERT for title of Korean articles*<br><br>
  2-2 ๊ธฐ์ฌ ๋ณธ๋ฌธ์ผ๋ก๋ถํฐ ์์ฑ๋ ํ ํฐ ์๊ฐํ <br>
  <img src="./data/imgs/body_token_vis.png" width="1000"> <br>
  *Fig 7. Visualization of embedded tokens from SBERT for body of Korean articles* <br><br>
  

  #### **3. KO-BERT fine-tunning ๊ณผ์ ์์์ CLS Token ์๊ฐํ**
  in the [HuggingFace BERT documentation](https://huggingface.co/docs/transformers/model_doc/bert#bertmodel), the returns of the BERT model are `(last_hidden_state, pooler_output, hidden_states[optional], attentions[optional])`
<br><BR>



# Discussion
- **If there is anything that needs to be corrected, productive criticism is always welcome.** <br>


  ## About total result
  <details>
  <summary> See detail</summary>
  
  - ํ์คํฌ๊ฐ ๊ฐ๋จํ์์ผ๋ฏ๋ก BERT์ fine-tuning๋ง์ผ๋ก ๋จ๊ธฐ๊ฐ ์์ 0.8์ด์์ ๋ถ๋ฅ๊ธฐ๋ฅผ ์์ฑํจ.
  - ๊ธฐ์ฌ์ ๋ณธ๋ฌธ์ ํฌํจํ  ๊ฒฝ์ฐ, `0.8641` ~ `0.8895`์ ํ์คํธ ์ Accuracy์ 8๊ฐ์ ํ ํฝ ๋ถ๋ฅ ๋ชจ๋ธ์ ์์ฑํจ.
  - ๊ธฐ์ฌ์ ์ ๋ชฉ๋ง์ ํฌํจํ  ๊ฒฝ์ฐ, `0.8269`์ ํ์คํธ ์ Accuracy๋ฅผ ํ์ธํจ.
  - Sentence Embeddingํ ๊ฒฐ๊ณผ๋ฅผ BERT ๋ชจ๋ธ์ ์ธํ์ผ๋ก ์ฃผ๋ ์คํ์์๋ Sentence Embeddingํ Cluster์ ์๋ณ๋ก ์ฝ๊ฐ์ ์ฐจ์ด๊ฐ ์์์ผ๋, ์์ฃผ ์ ์ ์ ๋ณด(1์๋ฆฌ ํน์ 2์๋ฆฌ์ ์ ์)๋ง์ผ๋ก ์กฐ๊ธ ๋ ๋น ๋ฅด๊ฒ ์ต๋ Accuracy์ธ `0.8895`๋ก ์๋ ดํจ์ ํ์ธํจ.
  - ์ ๋ฐ์ ์ผ๋ก ์ถฉ๋ถํ ์คํ์ด ์ํ๋์ง ์์์ง๋ง, ๋ช ๊ฐ์ง ์กฐ๊ฑด์ ๋ํด ๋ฐ๋ณต์ ์ธ ํ์ต์ ์งํํด ๋ณธ ๊ฒฐ๊ณผ, ํ์ฌ ์คํ์กฐ๊ฑด์์์ ์ต๊ณ  ์ฑ๋ฅ์ `0.8895` ์ ๋์๊ณ , ์ฌ์ ์ Cluster์ ๋ํ ์ ๋ณด๋ฅผ ์ค ๊ฒฝ์ฐ, ์ต๊ณ  ์ฑ๋ฅ์ ๋ ๋น ๋ฅด๊ฒ ๋๋ฌํจ์ ํ์ธํจ.
  - ๊ธฐ๋์ ๋์ผํ๊ฒ, ์ ๋๋ก ๋ ์ฝ๊ฐ์ ์ด๊ธฐ ํด๋ฌ์คํฐ ์ ๋ณด๋ง ์์ด๋ BERT ๋ชจ๋ธ์ด ์กฐ๊ธ ๋ ๋น ๋ฅด๊ฒ ์๋ ดํ๋ ๊ฒ์ ํ์ธํ  ์ ์์๊ณ , BERT ๋ชจ๋ธ์ ๊ฒฝ์ฐ Early Stop ์กฐ๊ฑด์ ์กฐ๊ธ ๊ด๋ํ๊ฒ ์ฃผ๋ ๊ฒ์ด ์ข์์ ํ์ธํจ.
  - ์ ์ฝ๋ ์์์ด๋ ์คํ์ด ๋งค์ฐ ๋จ๊ธฐ๊ฐ(์ ํ๋ 0.88๋์ base-line ๋์ถ๊น์ง ๋๋ต 3์ผ)์ ์ด๋ค์ก๊ณ , KO-BERT fine-tuning ์ฑ๋ฅ์ ํ์ธํ๊ธฐ ์ํ ๊ฒ์ ์ด์ ์ ๋ง์ถฐ ๊ตฌ์ฑ๋์์.
  - ๋ณธ ํ์คํฌ๋ 1) ๋ฐ์ดํฐ์ ๋นํด ํ์คํฌ ๋์ด๋๊ฐ ๋งค์ฐ ๋ฎ๊ณ , 2) ๊ณ ๋์ ์ ํ๋๋ฅผ ์๊ตฌํ์ง ์์ผ๋ฉฐ, 3) ๋ช๊ฐ์ง ํธ๋ฆญ ๋ฐ ๋ฃฐ๋ก ๋ ๋น ๋ฅด๊ฒ ๋ถ๋ฅ๊ฐ ๊ฐ๋ฅํ๋ฏ๋ก BERT๋ฅผ ํด๋น ํ์คํฌ์ ์ ์ฉํ๊ธฐ ์ํ ์คํ์ด๋ผ๊ธฐ ๋ณด๋ค๋ ๋ค๋ฅธ ์ด๋ ค์ด ํ์คํฌ์ BERT ๋ชจ๋ธ์ ์ ์ฉํ  ๋ ์ ์ฉํ ๋ช๊ฐ์ง๋ฅผ ํ์คํธํ๊ธฐ ์ํด์ ๊ตฌ์ฑ๋์์. 
  - ์ถ๊ฐ์ ์ผ๋ก GPT-3๋ฅผ ์ํ ๋ฆฌ์์ค๋ฅผ ํ๋ณดํ์์ผ๋ฏ๋ก, ๋์ผํ ํ์คํฌ์ ์คํ๋ฑ์ ํตํด GPT-3์ BERT ๋ชจ๋ธ์ ์ ์ฉ ๋น๊ต๋ฅผ ์ถ๊ฐํ๊ณ ์ ํจ.

  </details>

  <br>  

  ## Further experiments
  <details>
  <summary> See detail</summary>

  - `(Qualitative check)` ์ ์ฒ๋ฆฌ ์์ด ๋ฐ์ดํฐ ์์ ์๋ณธ๋ง์ผ๋ก๋ ์๊ตฌ์ฌํญ์ด์๋ 70% ์ด์์ ์ ํ๋๋ฅผ ๋ณด์์ผ๋ฏ๋ก, ์ถ๊ฐ์ ์ธ ์ ์ฒ๋ฆฌ๋ฅผ ์งํํ์ง ์์์ง๋ง, ์ด๋ค ํ ํฐ์ด ๋ชจ๋ธ ์ธํผ๋ฐ์ค์ ์ํฅ์ ์ฃผ๋์ง ํ์ธํ๊ณ , ๋ชจ๋ธ์ด ์ธํ ๊ธฐ์ฌ ๋ฐ์ดํฐ์์ ์ด์ํ ํ ํฐ์ Representation์ผ๋ก ์ฌ์ฉํ๊ณ  ์๋์ง๋ ์์์ง ์ฒดํฌํด ๋ณผ ํ์๊ฐ ์์.
  - `(eXplainable AI)`์ถ๊ฐ์ ์ผ๋ก ํ ํฐ์ ์ํฅ๋๋ฅผ ์๊ฐํํด์ SBERT๋ก ์ค Cluster๊ฐ ์ด๋ ์ ๋์ ์ํฅ์ด ์์๋์ง ํ์ธํ  ๊ณํ.
  - `(Understanding the BERT model)` ์ถ๊ฐ์ ์ผ๋ก ๋ฐฐ์น ์ฌ์ด์ฆ์ ๋ํ ์ฐจ์ด, BERT ๋ชจ๋ธ์ด ๋ณผ ์ ์๋ max_length์ ์ฐจ์ด๋ฅผ ๊ด์ฐฐํ๋ฉด ํฅํ fine-tuningํ  ๋ ํฐ ๋์์ด ๋  ์ ์์ ๊ฒ์ผ๋ก ๋ณด์ด๋ฉฐ, GPT-3์ ๋ํ ๊ฒ๋ค์ ํฅํ ๋ฆฌ์์ค๊ฐ ํ๋ณด๋๋๋๋ก ๋ค์ ๋น์ทํ๊ฒ ์ฌ์ด ํ์คํฌ๋ก ์ฒดํฌํด ๋ณผ ๊ณํ.
  - `(Exploring the Sentence Embedding Cluster)` Sentence Embedding์ ๊ฒฝ์ฐ, Cluster ์์ ๋ฐ๋ผ์ ์ด๋ ์ ๋ ์ ์๋ฏธํ ์ฐจ์ด๊ฐ ๋ณด์ธ๋ค๊ณ  ํ๋จ๋๋ฉฐ, ๋ช๊ฐ์ง ์ถ๊ฐ ์คํ์ ๋ ์ํํด๋ณผ ์ ์์.
  - `(Hypothesis Testing)`๊ฐ์ ํ์๋๋๋ก ์ ์ฌ๋ ํด๋ฌ์คํฐ๋ฅผ ์ด๊ธฐ๊ฐ์ผ๋ก ๊ฐ๊ณ  ์์๊ฒฝ์ฐ, ๋ ๋น ๋ฅด๊ฒ ํ์ตํ  ์ ์์์ ํ์ธํ์์ผ๋ฉฐ, ๊ฒฐ๋ก ์ ์ผ๋ก Sentence Embedding์ผ๋ก๋ถํฐ ์ป์ ์์ฃผ ์์ ์์ ์ํฉํธ ์๋ ํด๋ฌ์คํฐ ์ ๋ณด(high quality and low volume of information)๋ง์ผ๋ก ๋ชจ๋ธ ํ์ต ์๋์ ์ํฅ์ ์ค ์ ์๋ค๋ ๊ฒ์ ํ์ธํจ.
      - ์ด๋ multilingual-BERT์ธ SBERT์ ํ ํฐ ์๋ฒ ๋ฉ ๊ฐ์ ๊ธฐ๋ฐ์ผ๋ก ํด๋ฌ์คํฐ๋ง ์ ๋ณด๋ฅผ ์์ฑํ๊ณ , KO-BERT๊ฐ fine-tuning ๊ณผ์ ์์ SBERT์ ์์ํ์ ์ฐธ์กฐํ๋ฏ๋ก, ์ผ์ข์ ์ง์ ์ฆ๋ฅ์ ์ฑ๊ฒฉ์ ๋๋ค๊ณ  ๋ณผ ์ ์์ผ๋ฉฐ, ํ์ต ์๋๋ฉด์์ ๊ฒฐ๊ณผ ์ฐจ์ด๊ฐ ์์์ ํ์ธํจ.
      - ์ด๋ฌํ ์ฆ๋ฅ๋ ์ ์ ์์ ๋ฐ์ดํฐ๋ฅผ ํ์ต์ํค๋ ํ์คํฌ์์ ํฐ ์ค์ต์ด ์์ ์ ์์ผ๋, ํด๋ฌ์คํฐ ์ ๋ณด๋ฅผ ์ธํ์ผ๋ก ๋ฃ๋ ๊ฒ์ด ๋ ํฌ๊ณ  ๋ฌด๊ฑฐ์ด ๋ชจ๋ธ์ ๋น ๋ฅด๊ฒ ํ์ต์ํค๋๋ก ๊ธฐ์ฌํ  ์ ์๋ค๋ ๊ฒ์ ๋ณด์ฌ์ค.
      - ๋ค๋ฅธ ๋ชจ๋ธ๋ก๋ถํฐ ์ ๋ฌ๋๋ ๋ ์ด๋ธ ๊ฐ์ ๋ชจ๋ธ์ด ์ฐธ๊ณ ํ๊ธฐ์ ์ถฉ๋ถํ ์ณ์ ์ ๋ณด๋ง์ผ๋ก ๊ตฌ์ฑ๋์ด ์์ด์ผํ๋ค๋ ๊ฒ์ ํ์ธํจ.
        - `EXP8` ~ `EXP11`์ด ์ด๋ฌํ ํด๋ฌ์คํฐ ์ ๋ณด์ ์ง์ ๋ฐ๋ฅธ ํ์ต์๋ ๋ฐ ํ์ต ๊ฒฐ๊ณผ๋ฅผ ํ์ธํ๊ธฐ ์ํด ๊ตฌ์ฑ๋์์ผ๋ฉฐ, 8๊ฐ์ ํด๋์ค ๋ถ๋ฅ๊ธฐ ์์ฑ์์ 8๊ฐ์ ํด๋ฌ์คํฐ ์ ๋ณด๋ณด๋ค๋ 16๊ฐ์ ๋ ์ถฉ๋ถํ ์ณ์ ํด๋ฌ์คํฐ ์ ๋ณด๋ง์ ๊ฐ๊ณ  ์๋๋ก ๊ตฌ์ฑํ๋ ๊ฒ์ด ์ข์์ ํ์ธํจ.๋ก ํ ํฐ์ ์ํฅ๋๋ฅผ ์๊ฐํํด์ SBERT๋ก ์ค Cluster๊ฐ ์ด๋ ์ ๋์ ์ํฅ์ด ์์๋์ง ํ์ธํ  ๊ณํ.

  </details>

<br>

### `MODE1 & MODE3` 
<details>
<summary> See detail</summary>

  - If the sentence length is sufficiently secured, the title of the article is just information that is a repetition of important keywords in the article. Thus it showed a similar accuracy whether the title was added or not. The accuracy after the first epoch can be ignored as the result of random initialization.
  - The title of the article implies the connotation of very well-refined information. Therefore, it is possible to consider giving a little more weight to the title. However, considering the complexity, it is not worth that much.
  </details>

### `MODE2` 

  <details>
  <summary> See detail</summary>

  - The BERT model has strengths in semantic inference through a slightly wider context and self-emphasis in the context than existing natural language processing models. Therefore, it shows that it is very difficult to classify the topic with only the use of article titles(limited length).
  - Nevertheless, it was surprising that the title of the article alone could be inferred with 82% accuracy just by fine-tuning the BERT model.
  - If I could infer using GPT-3, the result would be much better in the same condition.

 </details>

### `MODE4 & MODE5` 

  <details>
  <summary> See detail</summary>

Mode 4 and Mode 5 are designed to create and experiment with a kind of distilled BERT model.
  - This experiment is designed *to see if it can be fine-tuned a bit faster based on the clustering information generated by SBERT.*
  - Basic Architecture of BERT models is Next token prediction, hence it is performed to compare the difference between giving information about BERT-based clustering information to the initial hidden layer and just putting information about clustering in the sentence.
  - K-means clustering is performed through the euclidean distance of the latent vector generated from the multilingual-BERT model [5].
  - Since two pretrained BERT model weights were used in the entire pipeline, only information was distilled and embedded when it was determined to be significant to prevent model confusion.

   </details>
<br>
<br>
  
### DistilBERT๊ด๋ จ `EXP2 & EXP9`์ ๋ํ ๊ณ ์ฐฐ

  <details>
  <summary> See detail</summary>


  - ์ `Embedding Token Visuallization` - 1์ ์ฐ์ฅ์ ์ผ๋ก EXP2์ EXP9์ ๊ฒฐ๊ณผ๋ฅผ ์ ๋ฆฌํ๊ณ  ์๊ฐํํจ.
  
  <p align="center">
    <img src="./data/imgs/Precision2and9.png" width="300"> <BR> 
  </p>

  *Fig . ์คํ2์ ์คํ3์ Precision ๋น๊ต*


  |   exp | metric    |   culture |    economy |   entertain |   international |        it |   politics |    society |      sport |   accuracy |   macro avg |   weighted avg |
  |------:|:----------|----------:|-----------:|------------:|----------------:|----------:|-----------:|-----------:|-----------:|-----------:|------------:|---------------:|
  |     2 | f1-score  |  0.714286 |   0.801802 |    0.911243 |        0.878049 |  0.769231 |   0.8739   |   0.874791 |   0.975000    |   0.877919 |    0.849788 |       0.877036 |
  |     9 | f1-score  |  0.774194 |   0.796610  |    0.898204 |        0.904000    |  0.829268 |   0.912387 |   0.862543 |   0.951220  |   0.881104 |    0.866053 |       0.881093 |
  |     2 | precision |  0.769231 |   0.847619 |    0.885057 |        0.885246 |  0.714286 |   0.892216 |   0.861842 |   0.951220  |   0.877919 |    0.85084  |       0.877594 |
  |     9 | precision |  0.750000     |   0.789916 |    0.882353 |        0.896825 |  0.73913  |   0.961783 |   0.874564 |   0.906977 |   0.881104 |    0.850194 |       0.883224 |
  |     2 | recall    |  0.666667 |   0.760684 |    0.939024 |        0.870968 |  0.833333 |   0.856322 |   0.888136 |   1        |   0.877919 |    0.851892 |       0.877919 |
  |     9 | recall    |  0.800000      |   0.803419 |    0.914634 |        0.911290  |  0.944444 |   0.867816 |   0.850847 |   1        |   0.881104 |    0.886556 |       0.881104 |
  |   nan | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.877919 |  942        |     942        |


   </details>

<br>
<br>
  
# Install Issues [Optional]
- Although my time was dead, I want to save your time.
- In `Google Colab`, some resources can handle version conflict, but the others failed to handle this issue. So you need to try 3-4 times while changing resource type(GPU or CPU).<br>
- All issues are caused by legacy `numpy` versions in each package. 
- Do not try to use mxnet acceleration because mxnet is very incomplete. The issues about mxnet acceleration in some cases have not been closed for a year.
- `**CLONE REPOSITORY AND USE THE MODULES AS IT IS - HIGHLY RECOMMENDED**`

<br>
<br>


#### About `Hugging-Face`, `mxnet gluonNLP` and `PyTorch` Framework

  <details>
  <summary> See detail</summary>

- 3๊ฐ์ง ํ๋ ์์ํฌ ๋ชจ๋ ๋ค์ํ๊ณ  ์ฐ์ํ ๊ธฐ๋ฅ์ ์ ๊ณตํด์ฃผ์์ต๋๋ค. ๊ทธ๋ฌ๋ ์ ์ฒด ํ์ดํ๋ผ์ธ์์ BERT์ ์ธํ์ ์ฒ๋ฆฌํ๋ ์์ ๋ฐ ์ถ์ํ ์ ๋๊ฐ ์ฝ๊ฐ์ฉ ๋ฌ๋์ต๋๋ค. 
- Huggingface๊ฐ highly-encapsulated ๋์ด์์์๋ ๋ถ๊ตฌํ๊ณ , ๋ ๋น ๋ฅด๊ณ  ๊ฐํธํ๊ฒ ๋ชจ๋ธ์ ์์ ํ๊ณ , ๋ ์ด์ด์ ์ ๊ทผํ  ์ ์๋ค๋ ์ ์ด ๋๋ผ์ ์ต๋๋ค.
- PyTorch, Huggingface,MXNet GluonNLP ์์ผ๋ก ์ปค๋ฎค๋ํฐ๊ฐ ํ๋ฐํ๊ณ , ๋ค์ํ ์ ๊ทผ์ ์ํ ์ข์ ํ๋ก์ ํธ๋ค์ด ์๋ ๊ฒ ๊ฐ์์ต๋๋ค. huggingface๊ฐ ๋ชจ๋ธ ๊ด๋ฆฌ ๋ฐ hidden layer ์ ๊ทผ ๋ฐ ๊ตฌ์กฐ ๋ณํ๋ ์กฐ๊ธ ๋ ์ฉ์ดํ ๊ฒ ๊ฐ๋ค๊ณ  ์๊ฐํ์์ผ๋ฉฐ, ์ถํ ์งํ๋๋ GPT ํ๋ก์ ํธ๋ huggingface์ ๋ชจ๋์ ์์ฃผ๋ก ์ฌ์ฉํ  ์์ ์๋๋ค.

</details>

<br>

#### About `mxnet` install (numpy version conflict)

  <details>
  <summary> See detail</summary>

- If you have a problem in the process of installing `mxnet`, you need to use `python=<3.7.0`.
- Any other options can not solve the numpy version conflict problem while `pip install mxnet`. 
- Except using python=3.7.xx, *EVERYTHING IS USELESS.*
  ```
  error: subprocess-exited-with-error ร 

  python setup.py bdist_wheel did not run successfully. โ exit code: 1 
  โฐโ> [890 lines of output] Running from numpy source directory. 

  C:\Users\user\AppData\Local\Temp\pip-install-8vepm8z2\numpy_34577a7b4e0f4f25959ef5aa089c5687\numpy\distutils\misc_util.py:476: SyntaxWarning: "is" with a literal. Did you mean "=="? return is_string(s) and ('*' in s or '?' is s) blas_opt_info: blas_mkl_info: No module named 'numpy.distutils._msvccompiler' in numpy.distutils; trying from distutils
  ```
- You may try to install `mxnet` before installing `gluonnlp`.

</details>

<br>



#### About KO-BERT version conflict

  <details>
  <summary> See detail</summary>


- As a result of conflict from above note(About `mxnet` install), KO-BERT still has version conflict.
  ```
  INFO: pip is looking at multiple versions of boto3 to determine which version is compatible with other requirements. This could take a while.
  ...
  To fix this you could try to:
  1. loosen the range of package versions you've specified
  2. remove package versions to allow pip attempt to solve the dependency conflict
  ```
  **Solution of this version conflict**
  - If you DO NOT use mxnet with KO-BERT, then remove mxnet in kO-bert `requirements.txt` or adjust(loosen) version as your environments.
  - If you DO use mxnet with KO-BERT, then just clone the repository and import the module as it is.

</details>

<br>

#### About random initialization in mxnet

<details>
<summary> See detail</summary>


  ```
  RuntimeError: Parameter 'bertclassifier2_dense0_weight' has not been initialized. Note that you should initialize parameters and create Trainer with Block.collect_params() instead of Block.params because the later does not include Parameters of nested child Blocks.
  ```

- Even when random initialization is not normally performed due to variable management problems, you can observe indicators that seem to be successfully learned in the trainset. 
- However, it was observed that the performance of the trainset continued to drop because it could not be directed to the candidate space of other local minima in the loss space. 
- Therefore, unlike other models, in the case of the Bert model, it is recommended to perform indicator checks in the trainset every iters.
- When using the Apache mxnet framework, carefully organize which layers to lock and which layers to update and in what order. Even when refactoring, initialize and update layers carefully. => to save your time.

</details>


<br>

#### About Tokenizer Error

<details>
<summary> See detail</summary>


  ```
  The tokenizer class you load from this checkpoint is not the same type as the class this function is called from. It may result in unexpected tokenization. 
  The tokenizer class you load from this checkpoint is 'XLNetTokenizer'. 
  The class this function is called from is 'KoBERTTokenizer'.
  ```

- First of all, check that num_classes are the same. And make sure classes of torch and mxnet framework are not used interchangeably. Finally, check if there is a conflict or mixed use in the wrapped class as written below. (Ignore the following if it has been resolved.)
- As mentioned above, If it is impossible to download the pretrained KOBERT weights from the aws server, you can download the wrapped weights to the hugging face interface through XLNetTokenizer. [ [3](https://github.com/SKTBrain/KoBERT/tree/master/kobert_hf) ]

</details>

<br>

#### About Korean NLP Models


<details>
<summary> See detail</summary>

- Almost all Korean NLP Models have not been updated often. Thus you should try to install lower versions of packages.
- recommendation: `python<=3.7.0` <br>
**Some Tips**
  - IndexError: Target 2 is out of bounds. => num_classes error (please check)
  - broken pipe error => num_workers error, if you used CPU => check your num of threads, else remove args numworkers.
  - If you can not download torch KO-BERT weight with urlib3 or boto3 library error message include 'PROTOCOL_TLS' issue, This is an error related to Amazon aws server download. Thus, => use huggingface interface https://github.com/SKTBrain/KoBERT/tree/master/kobert_hf
  - If you have other questions, please send me an e-mail. *All is Well!! Happy Coding!!*
  - ์ด์๋ issue๋ฅผ ์์ฑํด์ฃผ์๊ฑฐ๋, ๋ฉ์ผ๋ก ๋ฌธ์์ฃผ์๊ธฐ ๋ฐ๋๋๋ค.

</details>


<br>

# References <Br>
[1] GPT fine-tune https://www.philschmid.de/getting-started-setfit <br>
[2] KO-GPT https://github.com/kakaobrain/kogpt <br>
[3] KO-BERT https://sktelecom.github.io/project/kobert <br>
`download` of kobert-base-v1 https://huggingface.co/gogamza/kobart-base-v1 <br>
[4] Sentence-embedding https://github.com/UKPLab/sentence-transformers <br>
[5] Multilingual SBERT https://www.sbert.net/examples/training/multilingual/README.html <br>
[6] NLP gluon BERT documentation https://nlp.gluon.ai/model_zoo/bert/index.html
<br>

<details>
<summary> See more..</summary>

์ฐธ๊ณ ํ์ง ์์์ง๋ง, BERT model few shot learning ๊ด๋ จ๋ ๋ผ๋ฌธ์ ์ฐพ๋ค mode4์ ๋น์ทํ ์ปจ์์ ๋ผ๋ฌธ์ ํ์ธํจ <br>
[7]
  [Evaluation of Pretrained BERT Model by Using Sentence Clustering](https://aclanthology.org/2020.paclic-1.32) (Shibayama et al., PACLIC 2020)
<Br>
[8] T-SNE ๊ด๋ จ https://www.nature.com/articles/s41467-019-13056-x <br>
[9] DistilBERT https://arxiv.org/abs/1910.01108 <br>
[10] An Isotropy Analysis in the Multilingual BERT Embedding Space https://aclanthology.org/2022.findings-acl.103.pdf
<br>
[11] Where are we in embedding spaces? https://arxiv.org/abs/2105.08908 <br>
[12] Visuallization of BERT https://github.com/jessevig/bertviz.git <br>
 - shap https://shap.readthedocs.io/en/latest/example_notebooks/api_examples/plots/text.html
 - captum https://captum.ai/ <Br>
 
[13] Hugging face model weight upload and load
- https://huggingface.co/transformers/v1.0.0/model_doc/overview.html#loading-google-ai-or-openai-pre-trained-weights-or-pytorch-dump
- https://huggingface.co/docs/transformers/main_classes/model
- https://huggingface.co/docs/huggingface_hub/how-to-downstream

</details>



 <br><br>


#### Daily Commit Summary <br>
|Date|Description|
|:---:|:---|
|23.01.16|* ์์์ฒดํฌ: GPT inference ์ต์ VRAM ์๊ตฌ ์ฉ๋(32GB) ๋ถ์กฑ์ผ๋ก GPT ์ฌ์ฉ๋ถ๊ฐ, KO-BERT ์ฌ์ฉ  <br> - ํ๊ฒฝ์์ ์๋ฃ: ๋ก์ปฌ ์์๊ณผ Colab ๋ณํ <br> - ๊ฐ๋จํ Problem Definition and EDA, Data Analysis, BERT Embbeding Visuallization&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|23.01.17|- ๋ฒ ์ด์ค ์ฝ๋ ์์ฑ <br> - ๊ธฐ๊ฐ ๋ด ์ํ ๊ฐ๋ฅํ ์คํ ๋ฆฌ์คํธ ์์ฑ|
|23.01.18|- ์คํ๊ฒฐ๊ณผ ์ ๋ฆฌ <br>- ํ์ดํ๋ผ์ธ ํ์ |
|23.01.19~|- ์ต์ข ์ ์ถ ๋ฐ ๋ฆฌํฉํ ๋ง ํ Repository ์ ๋ฆฌ <br>- Documentation <br> - Recommendation project์ ์๋ธ ๋ชจ๋๋ก ์ฌ์ฉ(t-sne๋ embedding๋ถ๋ถ ํฌํจ)|
|23.02.05~|- Kaggle ํด๋ฆญ, ์ฅ๋ฐ๊ตฌ๋, ๊ตฌ๋งค ํญ๋ชฉ ์์ธก ๋ชจ๋ธ๋งํ๋ฉฐ Colab Pro๋ฅผ ๊ฒฐ์ ํ์ผ๋ฏ๋ก 2์์ค์ GPT๋ฅผ ํตํ ํ์ต ์คํ ์๋ฐ์ดํธ ์์  <br> - XAI, FrontEnd๋ ์ถ๊ฐ์ ์ผ๋ก ์ํ ์์ |

<br>

#### Further Reading...
[1] PyTorch CRF https://github.com/kmkurn/pytorch-crf


## Remark
- *Please note that the domain was not fully searched because it is not mission critical artificial intelligence and is intended to simply identify NLP(Natural Language Processing) models in korean and perform requested tasks in a short period of time with limited data.*
- If it is used in actual service, some more tricks or experiments may be required. but as mentioned above, it is expected that the service can be maintained satisfactorily if applied in the same way with the heuristic method. There may be considerations such as continuous learning.
<!-- - *This is just a toy project! please enjoy it!* <br>
![](https://github.com/DSDanielPark/news-article-classification-using-koBERT/blob/main/imgs/enjoy2.gif) -->
<br>


## Evaluation Metric of Experiments
<br>

The Mode 1, Mode 2, and Mode 3 experiments were designed to see how well a subject could classify 8 topics into the body and headlines of a news article.
  - `Mode 1`: It learns data containing only the body of news articles as input.
  - `Mode 2`: It learns data containing only news article titles as input.
  - `Mode 3`: It learns data containing both news article titles and body as input.

<br>

Mode 4 and Mode 5 are designed to create and experiment with a kind of distilled BERT model.
- This experiment is designed *to see if it can be fine-tuned a bit faster based on the clustering information generated by SBERT.*
- In this experiment, the information clustered by SBERT, a multilingual model, is used to fine-tune the KO-BERT model.
  - `Mode 4`: Cluster information generated from SBERT, a multilingual model, is used as model input, and this experiment used the mxnet framework in the same way as Modes 1 to 3.
  - `Mode 5`: Clustering information generated from SBERT was input to the initial layer using the PyTorch framework. The results of this experiment may be slightly different from Modes 1 to 4, so they are not described.
    - However, as in Mode 4, it was confirmed through several iterations that almost similar accuracy can be reached faster if you have cluster information generated from SBERT.


- You can see whole experiments result in [`experments/exp.md`](https://github.com/DSDanielPark/news-article-classification-using-KO-BERT/blob/main/experiments/exp.md) 
- In the case of EXP2 and EXP9, it was repeatedly performed to track and observe the learning rate, confirming similar learning patterns.

<Br>
<br>

## Metric Table
시각화하므로 수치 참조용으로 업로드
[]()
<br>


|    |   exp | metric    |   culture |    economy |   entertain |   international |        it |   politics |    society |      sport |   accuracy |   macro avg |   weighted avg |
|---:|------:|:----------|----------:|-----------:|------------:|----------------:|----------:|-----------:|-----------:|-----------:|-----------:|------------:|---------------:|
|  0 |     1 | precision |  0.764706 |   0.796748 |    0.903614 |        0.888889 |  0.736842 |   0.919255 |   0.888889 |   0.936    |   0.884289 |    0.854368 |       0.885304 |
|  1 |     1 | recall    |  0.866667 |   0.837607 |    0.914634 |        0.903226 |  0.777778 |   0.850575 |   0.867797 |   1        |   0.884289 |    0.877285 |       0.884289 |
|  2 |     1 | f1-score  |  0.8125   |   0.816667 |    0.909091 |        0.896    |  0.756757 |   0.883582 |   0.878216 |   0.966942 |   0.884289 |    0.864969 |       0.884244 |
|  3 |     1 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.884289 |  942        |     942        |
|  4 |     2 | precision |  0.769231 |   0.847619 |    0.885057 |        0.885246 |  0.714286 |   0.892216 |   0.861842 |   0.95122  |   0.877919 |    0.85084  |       0.877594 |
|  5 |     2 | recall    |  0.666667 |   0.760684 |    0.939024 |        0.870968 |  0.833333 |   0.856322 |   0.888136 |   1        |   0.877919 |    0.851892 |       0.877919 |
|  6 |     2 | f1-score  |  0.714286 |   0.801802 |    0.911243 |        0.878049 |  0.769231 |   0.8739   |   0.874791 |   0.975    |   0.877919 |    0.849788 |       0.877036 |
|  7 |     2 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.877919 |  942        |     942        |
|  8 |     3 | precision |  0.777778 |   0.861111 |    0.894118 |        0.882812 |  0.736842 |   0.924051 |   0.866883 |   0.92126  |   0.884289 |    0.858107 |       0.884043 |
|  9 |     3 | recall    |  0.466667 |   0.794872 |    0.926829 |        0.91129  |  0.777778 |   0.83908  |   0.905085 |   1        |   0.884289 |    0.8277   |       0.884289 |
| 10 |     3 | f1-score  |  0.583333 |   0.826667 |    0.91018  |        0.896825 |  0.756757 |   0.879518 |   0.885572 |   0.959016 |   0.884289 |    0.837234 |       0.882609 |
| 11 |     3 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.884289 |  942        |     942        |
| 12 |     4 | precision |  0.857143 |   0.805085 |    0.916667 |        0.888    |  0.705882 |   0.904459 |   0.854785 |   0.935484 |   0.874735 |    0.858438 |       0.874762 |
| 13 |     4 | recall    |  0.8      |   0.811966 |    0.939024 |        0.895161 |  0.666667 |   0.816092 |   0.877966 |   0.991453 |   0.874735 |    0.849791 |       0.874735 |
| 14 |     4 | f1-score  |  0.827586 |   0.808511 |    0.927711 |        0.891566 |  0.685714 |   0.858006 |   0.866221 |   0.962656 |   0.874735 |    0.853496 |       0.874138 |
| 15 |     4 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.874735 |  942        |     942        |
| 16 |     5 | precision |  0.833333 |   0.693878 |    0.868132 |        0.878049 |  0.722222 |   0.965278 |   0.874101 |   0.906977 |   0.860934 |    0.842746 |       0.86909  |
| 17 |     5 | recall    |  0.666667 |   0.871795 |    0.963415 |        0.870968 |  0.722222 |   0.798851 |   0.823729 |   1        |   0.860934 |    0.839706 |       0.860934 |
| 18 |     5 | f1-score  |  0.740741 |   0.772727 |    0.913295 |        0.874494 |  0.722222 |   0.874214 |   0.848168 |   0.95122  |   0.860934 |    0.837135 |       0.861426 |
| 19 |     5 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.860934 |  942        |     942        |
| 20 |     6 | precision |  0.916667 |   0.825688 |    0.791667 |        0.869159 |  0.705882 |   0.86875  |   0.790909 |   0.963964 |   0.83758  |    0.841586 |       0.841845 |
| 21 |     6 | recall    |  0.733333 |   0.769231 |    0.926829 |        0.75     |  0.666667 |   0.798851 |   0.884746 |   0.91453  |   0.83758  |    0.805523 |       0.83758  |
| 22 |     6 | f1-score  |  0.814815 |   0.79646  |    0.853933 |        0.805195 |  0.685714 |   0.832335 |   0.8352   |   0.938596 |   0.83758  |    0.820281 |       0.837201 |
| 23 |     6 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.83758  |  942        |     942        |
| 24 |     7 | precision |  0.833333 |   0.867347 |    0.877778 |        0.868852 |  0.666667 |   0.927152 |   0.820669 |   0.942623 |   0.867304 |    0.850553 |       0.869855 |
| 25 |     7 | recall    |  0.666667 |   0.726496 |    0.963415 |        0.854839 |  0.666667 |   0.804598 |   0.915254 |   0.982906 |   0.867304 |    0.822605 |       0.867304 |
| 26 |     7 | f1-score  |  0.740741 |   0.790698 |    0.918605 |        0.861789 |  0.666667 |   0.861538 |   0.865385 |   0.962343 |   0.867304 |    0.833471 |       0.865818 |
| 27 |     7 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.867304 |  942        |     942        |
| 28 |     8 | precision |  0.846154 |   0.837607 |    0.866667 |        0.894737 |  0.52381  |   0.942446 |   0.827044 |   0.9      |   0.860934 |    0.829808 |       0.865604 |
| 29 |     8 | recall    |  0.733333 |   0.837607 |    0.95122  |        0.822581 |  0.611111 |   0.752874 |   0.891525 |   1        |   0.860934 |    0.825031 |       0.860934 |
| 30 |     8 | f1-score  |  0.785714 |   0.837607 |    0.906977 |        0.857143 |  0.564103 |   0.837061 |   0.858075 |   0.947368 |   0.860934 |    0.824256 |       0.860106 |
| 31 |     8 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.860934 |  942        |     942        |
| 32 |     9 | precision |  0.75     |   0.789916 |    0.882353 |        0.896825 |  0.73913  |   0.961783 |   0.874564 |   0.906977 |   0.881104 |    0.850194 |       0.883224 |
| 33 |     9 | recall    |  0.8      |   0.803419 |    0.914634 |        0.91129  |  0.944444 |   0.867816 |   0.850847 |   1        |   0.881104 |    0.886556 |       0.881104 |
| 34 |     9 | f1-score  |  0.774194 |   0.79661  |    0.898204 |        0.904    |  0.829268 |   0.912387 |   0.862543 |   0.95122  |   0.881104 |    0.866053 |       0.881093 |
| 35 |     9 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.881104 |  942        |     942        |
| 36 |    10 | precision |  0.9      |   0.724638 |    0.907895 |        0.912281 |  0.56     |   0.89881  |   0.89781  |   0.854015 |   0.859873 |    0.831931 |       0.867409 |
| 37 |    10 | recall    |  0.6      |   0.854701 |    0.841463 |        0.83871  |  0.777778 |   0.867816 |   0.833898 |   1        |   0.859873 |    0.826796 |       0.859873 |
| 38 |    10 | f1-score  |  0.72     |   0.784314 |    0.873418 |        0.87395  |  0.651163 |   0.883041 |   0.864675 |   0.92126  |   0.859873 |    0.821477 |       0.860713 |
| 39 |    10 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.859873 |  942        |     942        |
| 40 |    11 | precision |  0.785714 |   0.914894 |    0.904762 |        0.88189  |  0.7      |   0.930818 |   0.84     |   0.97479  |   0.887473 |    0.866608 |       0.890431 |
| 41 |    11 | recall    |  0.733333 |   0.735043 |    0.926829 |        0.903226 |  0.777778 |   0.850575 |   0.925424 |   0.991453 |   0.887473 |    0.855458 |       0.887473 |
| 42 |    11 | f1-score  |  0.758621 |   0.815166 |    0.915663 |        0.89243  |  0.736842 |   0.888889 |   0.880645 |   0.983051 |   0.887473 |    0.858913 |       0.886663 |
| 43 |    11 | support   | 15        | 117        |   82        |      124        | 18        | 174        | 295        | 117        |   0.887473 |  942        |     942        |
name: inverse
layout: true
class: center, middle, inverse
---
# Basis of stan coding
<br>Rとstanではじめるベイズ統計モデリングによるデータ分析入門 
<br>Makino Lab reading circle  7/1 伊藤冬馬
---
layout:false
### スタンコーディングの詳細
### 一般化線形モデルの基本

---
## stanファイルの構造
３ページ目
.right-column[
functionsブロック               :自作の関数
<br>dataブロック                    :使用するデータやサンプルサイズなどの定義
<br>transformed dataブロック        :データの変換の指定
<br>parametersブロック              :事後分布を得たいパラメータの一覧の定義
<br>transformed parametersブロック  :パラメータ変換の指定
<br>modelブロック                   :モデルの構造と指定
<br>generated quantitiesブロック    :モデルの推定と別に、事後分布を得体場合はここに指定
]
.left-column[
```C++
data {
  int N;          // サンプルサイズ
  vector[N] animal_num;   // データ
}

parameters {
  real<lower=0> mu;       // 平均
  real<lower=0> sigma;    // 標準偏差
}

model {
  // 平均mu、標準偏差sigmaの正規分布
  animal_num ~ normal(mu, sigma);
}

generated quantities{
  // 事後予測分布を得る
  vector[N] pred;
  for (i in 1:N) {
    pred[i] = normal_rng(mu, sigma);
  }
}

```
]

---
## 変数の宣言
４ページ目

* リンクを貼る

__[Google](https://www.google.co.jp/)__
---
layout:false
### スタンコーディングの詳細
### 一般化線形モデルの基本

---

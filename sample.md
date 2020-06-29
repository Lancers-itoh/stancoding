name: inverse
layout: true
class: center, middle, inverse
---
# Basis of stan coding
<br>Rとstanではじめるベイズ統計モデリングによるデータ分析入門 
<br>Makino Lab reading circle  7/1 Itoh Thoma
---
layout:false
### スタンコーディングの詳細
### 一般化線形モデルの基本

---
## Structure of stan file
.right-column[
functionsブロック                   :自作の関数
<br><b>dataブロック                    :使用するデータやサンプルサイズなどの定義</b>
<br>transformed dataブロック        :データの変換の指定
<br><b>parametersブロック              :事後分布を得たいパラメータの一覧の定義</b>
<br>transformed parametersブロック  :パラメータ変換の指定
<br><b>modelブロック                   :モデルの構造と指定</b>
<br><b>generated quantitiesブロック    :モデルの推定と別に、事後分布を得体場合はここに指定</b>
]
.left-column[
```cpp
data {
  //sample size
  int N;   
  //data
  vector[N] animal_num;   
}

parameters {
  // mean
  real<lower=0> mu;      
  //Standard diviation
  real<lower=0> sigma;    
}

model {
  //Normal distribution with mean mu, var sigma
  animal_num ~ normal(mu, sigma);
}

generated quantities{
  //Get  posterior distribution 
  vector[N] pred;
  for (i in 1:N) {
    pred[i] = normal_rng(mu, sigma);
  }
  
}

```
]

---
## Declaration of variavles

Number
```cpp
int N;      // Declare variable N as integer type
real beta;  // Declare variable beta as real number

//Specify range
real<lower=0> sigma;          // Declare variable 'sigma' as a real number greater than or equal to zero.
int<lower=0, upper=1> range;  // Declare variable 'range' as a real number between 0 and 1
```

Vector, Matrix 
```cpp
/*Declared as real number type*/
/*Index starts from 1*/

vector[3] retu;               // Declare column vector 'retu' with three elements
row_vector[10] gyou;          // Declare row vector 'gyou' with 10 elements

matrix[3,2] mat;              //Declare matrix 'mat' with 3 rows and 2 columns 
```

Array
```cpp
int W[10];                    //Declare array 'W' with integer type of 10 elements
real X[3,4];                  //Declare array 'X' with real number type of 3 rows and 4 columns
vector[4] Y[2];               //Declare array 'Y' with two "vectors with four elements
matrix[3,4] z[5,6];           //Declare array 'matrix' with 5 x 6 matrix with 3 x 4 matrix
```

---
## sampling statement
$$ *sales* ~ Normal(\mu, \sigma^2) $$
```cpp
model{
  for (i in 1:N){
    sales[i] ~ normal(mu, sigma);
  }
}
```
---
## sampling statement
*sales* ~ Normal(\mu, \sigma^2);
$$ e^{i x} = \cos{x} + i \sin{x} $$
```cpp
model{
  for (i in 1:N){
    sales[i] ~ normal(mu, sigma);
  }
}
```
---


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
<br>
functions{}:  Define original function here
<br><br>
<b>data{}:  Define used data and its sample size</b>
<br><br>
transformed data{}:  Define data transformation
<br><br>
<b>parameters{}:  Define parameters which you want to know the posterior distribution</b>
<br><br>
transformed parameters{}: Define parameters transformation
<br><br>
<b>model{}: Define model structure and assignment</b>
<br><br>
generated quantities{}: Get posterior distribution
]
.left-column[
```cpp
data {
  //こういう標本データが与えられていて
  int N;   
  vector[N] sales;   


parameters {
  //これらのパラメータを推定したい
  real mu;      
  real<lower=0> sigma;    
}

model {
  /*パラメータはわからないけど
  正規分布に従うと仮定*/
  for (i in 1:N){
    sales[i] ~ normal(mu, sigma);
  }
}

```
]

---
## Declaration of variavles

Number
```cpp
int N;        // Declare variable N as integer type  
real beta;    // Declare variable beta as real number

//Specify range
real<lower=0> sigma;          // Greater than or equal to zero, integer
int<lower=0, upper=1> range;  // Range 0 to 1, real number
```

Vector, Matrix 
```cpp
vector[3] retu;               // Column vector with three elements
row_vector[10] gyou;          // Row vector with 10 elements
matrix[3,2] mat;              // Matrix with 3 rows and 2 columns 
```

Array
```cpp
int W[10];                    //Array with integer type of 10 elements
real X[3,4];                  //Array with real number type of 3 rows and 4 columns
vector[4] Y[2];               //Array with two vectors with four elements
matrix[3,4] z[5,6];           //Array with 5 x 6 matrix with 3 x 4 matrix
```

---
## sampling statement

<p>Define posterior distribution and<br>
  samplle data distribution</P>
```cpp
//事前分布の設定
mu ~ normal(0, 1000000);
sigma ~ normal(0, 1000000);

/*パラメータはわからないけど
  標本データは正規分布に従うと仮定*/
model{
  for (i in 1:N){
    sales[i] ~ normal(mu, sigma);
  }
}
```
---


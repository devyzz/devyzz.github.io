---
layout: post
title: 이어드림스쿨 | 파이썬 확률 통계
categories: 
  - learning
  - courses 
tags : data
excerpt_separator: <!--more-->
hide_last_modified: true
sitemap: true
---
* toc
{:toc .large-only}
이어드림스쿨 7주차 강의 중 파이썬 확률 통계에  대해 학습한 내용을 정리한 글입니다. 

<!--more-->

현업에서 필요한 건 논문을 읽어보고 해당 논문을 프로그램으로 작성할 수 있는 사람이다. 이 때 이 논문을 읽고 이해하기위해서는 기반이 되는 통계분석을 반드시 숙지해야한다.

## 중심위치의 측도

### 수치형 자료

| 자료형                   | 특징                                                         | 예시                            | 데이터 유형 |
| ------------------------ | ------------------------------------------------------------ | ------------------------------- | ----------- |
| <mark>이산형</mark> 자료 | 구간이 명확하며 정수 형태로 표현<br>값이 연속되지 않고 띄엄띄엄 존재 | 학생 수, 출석 일수, 주사위 눈금 | 정수형      |
| <mark>연속형</mark> 자료 | 연속적인 실수값을 가지며 측정이 가능함 <br>소수점 값을 포함할 수 있음 | 키, 몸무게, 온도, 길이          | 실수형      |

### 범주형 자료

| 자료형                   | 특징                                                         | 예시                                                         | 데이터유형 |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| <mark>명목형</mark> 자료 | 범주형 데이터로 순서가 없음<br>값이 서로 다른 범주를 표현할 때 사용함 | 성별(남/여), 혈액형(A/B/O/AB), 국가명                        | 범주형     |
| <mark>순서형</mark> 자료 | 범주형 데이터지만 순서나 등급이 존재<br>                     | 학점(A,B,C), 계급(상,중,하), <br>만족도(매우 만족, 만족, 보통, 불만족 등) | 순서형     |

### 도수분포표(Frequency Distribution Table)

데이터를 구간별로 나누어 각 구간에 속하는 데이터의 개수(도수)를 정리한 표 

- 도수(Frequency) : 특정 구간에 속하는 데이터의 계수
- 계급(class) : 데이터를 나눈 구간
- 계급 간격(Class Interval) : 계급의 너비
- 계급 값(Class Mark) : 각 계급의 중앙값

### 기본 통계의 개념정리 (1) _ 백분위수

데이터를 **오름차순**으로 정렬했을 때, 특정 위치에 해당하는 값을 의미한다. 

- P 백분위수 (P-th Percentile) : 데이터의 P% 위치에 있는 값을 의미

  - 50백분위 수(50th Percentile) : 중앙값(Median)과 동일 (데이터가 50%가 이 값 이하)
  - 25백분위 수 (1사분위수, Q1) : 데이터의 25%가 이 값 이하
  - 75백분위 수 (3사분위수 Q2) : 데이터의 75%가 이 값 이하

	> 25백분위수(Q1) 계산
  >
  > 1. 점수 = [55,60,65,70,75,80,85,90,95,100]
  >
  > 2. 위치계산 
  >    $$
  >    위치 = 25/100*(10+1)=0.25*11=2.75
  >    $$
  >    `10+1` : 총데이터의 수의 <u>간격</u> (가장 앞(1) +가장 끝(1) + 사이간격(9))
  >
  >    위치 : 2.75 (정수 부분 : 2 / 소수 부분 : 0.75) &rarr; 2번째값(60)과 3번째값(65)사이의 어딘가
  >
  > 3. 선형 보간법 사용
  >
  >    1. 2번째 값 : 60
  >    2. 3번째 값 : 65
  >
  >    $$
  >    25백분위수 = 60+0.75*(65-60)=60+0.75*5=60+3.75=63.75
  >    $$
  >


### 기본 통계의 개념정리 (2) _ 자료의 중앙값 분석

- **평균 (Mean)** - 데이터의 산술 평균값 (전체합계 / 전체개수)

- 편차 (Deviation) - 각 데이터 값과 평균의 차이 

- 편차 제곱 (Squared Deviation) - 편차를 제곱하여 음수 값을 양수로 변환하고 오차를 부각

- **분산 (Varlance)** - 편차제곱의 평균

- **표준편차 (Standard Deviation)** - 분산의 제곱근, 원래 데이터와 같은 단위가 된다

  > 점수 [60, 70, 80, 90, 100]
  >
  > ![image-20250514101705351](../../../../../Blog/devyzz.github.io/images/2025-05-14-statstics/image-20250514101705351.png)

### 중심위치의 측도(measure of center)

자료의 중심위치를 확인한다. 데이터의 중심 경향 파악 후 대표값을 확인한다. 평균, 중앙, 최빈값을 통해 표현

#### 평균 (Mean)

```python
np.mean()
```

중심위치의 측도 중에서 가장 많이 사용되는 방법. <br>모든 관측값의 합을 자료의 개수로 나눈 것 

<u>극단적으로 큰 값이나 작은 값의 영향을 많이 받는다는 특징을 가진다.</u>

#### 중앙값(Median)

```python
np.median()
```

전체 관측값을 정렬했을 때 가운데에 위치하는 값
$$
자료의 개수(n)가 홀수인 경우 = (n+1)/2
$$

$$
자료의 개수(n)가 짝수인 경우 = n/2번째 관측값과 n/2+1번째 값의 관측 평균
$$

<u>관측값의 변화에 민감하지 않고, 극단값의 영향을 받지 않는다는 특징을 가진다.</u>

#### 최빈값(Mode)

```python
stats.mode()
```

관측값 중 가장 자주 나오는 값으로 이산형/범주형 자료에서 많이 사용된다.

#### 단봉형 대칭(Unimodal Symmetric Distribution)

![image-20250514104727876](../../../../../Blog/devyzz.github.io/images/2025-05-14-statstics/image-20250514104727876.png)

- 정규분포(Normal Distribution)
- 좌우 대칭으로 분포의 중심을 기준으로 균형있게 분포한다 
- 종 모양(Bell-shaped)으로 실험데이터에서 발생
- 주로 평균과 표준편차로 표현한다.
- 극단값 &rarr; 분석왜곡, 이상탐지, 모델학습방해 

#### 이봉형 대칭 & 비대칭 분포

![image-20250514104931118](../../../../../Blog/devyzz.github.io/images/2025-05-14-statstics/image-20250514104931118.png) 

비대칭 분포(치우친 분포)에서 평균값과 중앙값 <br>왼쪽으로 치우친 분포 `평균 < 중앙값` , 오른쪽으로 치우친 분포 `평균 > 중앙값`

## 퍼진 정도의 측도

**중심위치만으로 분포를 파악하기에 부족**한 경우 중심위치 측도 외에 분포가 퍼진 정도를 측도할 수치가 필요하다. 이 때 분산, 표준편차, 범위, 사분위수 등을 퍼진 정도의 측도로 사용하고자 한다.

### 분산 (variance())

자료가 얼마나 흩어졌는지를 숫자로 표현한다. 즉, 각 관측값이 자료의 평균으로부터 떨어진 정도를 일컫는다.

<mark>관측값이 x1, x2, .. . xn, 이고 평균이 a 일 때, 관측값에 대한 편차는 (관측값 - 평균) 즉, xn-a 이다.</mark>

### 표준편차

```python
stdev()
```

분산의 단위 = 관측값의 단위의 제곱 / 관측값의 단위와 불일치 

분산의 양의 제곱근은 관측값과 단위가 일치 / 분산의 양의 제곱근을 표준편차라 하고 s로 표기한다

### 범위(range)

```python
np.max()-np.min()
```

관측값에서 가장 큰 값과 가장 작은 값의 차이 

### 백분위수 (np.percentile())

중앙값을 확장한 개념으로 자료를 순서대로 정렬했을 때 백분율로 특정위치의 값을 표현한다.

> **문제1 : 학생 점수의 25백분위수(Q1)구하기**
>
> 점수 : [52,55,58,60,63,65,68,70,72,75,78,80,82,85,88,90,92,95,98,100]
>
> 1. 오름차순 정렬
>
> 2. n x p 계산
>    $$
>    위치 = 데이터의 개수 * p = 20 * 0.25 = 5
>    $$
>    n x p = 5로 정수이므로, 5번째와 6번째 값의 평균을 구한다.
>
> 3. 계산 
>
>    점수[5] = 63 , 점수[6] = 65
>    $$
>    25백분위수 =(63+65)/2 = 128/2 = 64
>    $$
>
> 4. 
>
> **문제2 : 동일한 경우에서 30백분위수(Q2) 구하기**
>
> 1. n x p. 계산
>    $$
>    20 * 0.3 = 6
>    $$
>
> 2. 계산 
>
>    점수[6] = 65, 점 수[7] = 68
>    $$
>    (65+68) /2 = 66.5
>    $$
>    

### 사분위수

`np.percentile(a, 25)`, `np.percentile(a,50)`, `np.percentile(a,75)`

백분위수의 일종으로 전체를 사등분하는 값. 제 1,2,3 분위수를 각각 Q1, Q2, Q3로 표시한다.<br>중앙값은 전체의 1/2에 위치하는 값이므로 제 2사분위수 및 제 50백분위수

#### 사분위수 범위

`제3사분위수와 1사분위수 사이의 거리`

- 범위 - 전체 관측값이 퍼진 정도 

- IQR(Interquartile Range)사분위수 범위 - **<u>관측값의 중간 50%에 대한</u>** 범위 

  - 공식) IQR = Q3(하위 75%에 위치하는 제 3사분위수) - Q1(하위 25%에 위치하는 제1사분위수)
  - 이상치(Outlier) 탐지에도 활용
    - 이상치공식 - Q1 - 1.5 * IQR , Q3 + 1.5* IQR

  - IQR의 값이 클수록 데이터가 흩어져있고, 작을수록 데이터가 밀집되어 있다.

  > IQR 계산 예제
  >
  > 점수 : [52,55,58,60,63,65,68,70,72,75,78,80,82,85,88,90,92,95,98,100]
  >
  > 1. 데이터 정렬
  >
  > 2. 사분위 수 계산 (Q1, Q3)
  >
  >    1. Q1  - 64.5
  >    2. Q2 - 88.5
  >
  >    $$
  >    IQR  = Q3 - Q1 = 88.5 -64.5 = 24.0
  >    $$
  >
  > 3. 이상치 기준 계산 
  >    $$
  >    하한 = Q1 - 1.5 * IQR = 64.5 -1.5*24.0 = 28.5
  >    $$
  >    $$
  >    상한 =Q3 + 1.5*IQR =88.5 + 1.5*24.0 =124.5
  >    $$
  >
  >    데이터의 최소값이 52, 최대값이 100 이므로 이상치가 없음을 알 수 있다.  

### 퍼진 정도 측정법의 비교

| 구분                    | 정의 및 특징                                                 | 장점                                                         | 단점                                                         |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **표준편차**            | 전체 관측값들의 평균으로부터의 퍼짐 정도를 수치화해 반영하는 지표 | 전체 분포의 퍼짐 정도를 고르게 반영                          | **극단값(이상치)**에 민감하여 왜곡될 수 있음                 |
| **사분위수 범위 (IQR)** | 제1사분위수(Q1)와 제3사분위수(Q3) 사이의 범위로, 중간 50%의 데이터 분포 확인 | 극단값의 영향을 받지 않고 **중간값 중심의 분포 특성** 파악 가능 | Q1~Q3 사이의 분포만 반영되므로 **전체 분포 정보가 부족**     |
| **범위 (Range)**        | 최댓값과 최솟값 간의 차이로 데이터를 **전체적으로 얼마나 퍼져있는지** 보여줌 | 계산이 간단하고 데이터 분포 대략적인 확인 가능               | **표준편차와 사분위수 범위의 단점을 모두 가짐**: 이상치에 민감하고 전체 분포 반영 부족 |

## 상자그림(Box Plot)

![image-20250514134924379](../../../../../Blog/devyzz.github.io/images/2025-05-14-statstics/image-20250514134924379.png)

데이터의 분포와 이상치를 한눈에 보여주는 그래프를 일컫는다. 

- 중앙선 (Median) : 데이터의 중앙값 (Q2)
- 상자 (Box) : Q1과 Q3 사이 (중간 50% 데이터)
- 수염 (Whisker) : 상자 바깥쪽의 데이터 범위
- 이상치 (Outlier) : 수염 바깥에 위치한 데이터 

**해석 방법**

중앙값이 상자 가운데에 있다 &rarr; 데이터가 대칭적이다<br>중앙값이 한쪽으로 치우친다 &rarr; 데이터가 비대칭적이다 (편향되어 있다) , 데이터를 제거할지 다시 표준화 할 지 고민해야함

상자가 크다 &rarr; 데이터의 변동성이 크다 <br>상자가 작다 &rarr; 데이터가 밀집되어 있다

### 변동계수 (Coefficient of Variation, CV)

변동계수는 평균에 대한 상대적인 퍼진 정도를 백분율(%)로 나타낸다. 비교 대상의 단위가 다른 경우, 단위가 없는 변동계수를 통해 퍼진 정도를 비교할 수 있다. 

`CV = 표준편차 / 평균 * 100`

CV가 작을수록 데이터는 평균에 밀집되어 있다. (변동이 작다)<br>CV가 클수록 데이터가 평균에서 멀리 퍼져 있다. (변동이 크다)

일반적으로 20% 미만이면 변동이 적다고 판단하고, 40% 초과일 경우 변동이 크다고 판단한다.  

### 도수분포표

자료가 도수분포표로 요약되고 원 자료가 주어지지 않는 경우, 계급구간의 모든 관측값이 계급의 중간값을 갖는다고 가정하여 평균과 분산을 계산한다.

#### 도수분포표에서의 평균

- **계급의 개수** : `k`  

- **각 계급의 도수** : `fᵢ`  

- **각 계급의 중간값** : `mᵢ`  

- **자료의 개수** : `n = Σ fᵢ` (i = 1부터 k까지)
  $$
  bar{x} = \frac{1}{n} (m₁f₁ + m₂f₂ + ⋯ + mₖfₖ)
  $$
  또는
  $$
  bar{x} = \sum_{i=1}^{k} m_i \left( \frac{f_i}{n} \right)
  $$

## 두 변수 자료의 요약

둘 또는 그 이상 변수에 대한 관측 자료는 동시에 분석하여 도표/수치로 요약한다.

#### 1. 분할표 

도수분포표를 2차원으로 확장한 형태로 요약한다.

`pd.crosstab(index = 기준 범주, columns = 관측 범주)`


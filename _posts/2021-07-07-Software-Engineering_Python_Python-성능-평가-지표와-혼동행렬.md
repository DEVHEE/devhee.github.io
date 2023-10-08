---
title: Python / Python 성능 평가 지표와 혼동행렬
author: DEVHEE
date: 2021-07-07 01:15:18 +0900
categories: [Software Engineering, Python]
tags: [software engineering, software, python, regression, performance, measure]
math: true
image:
    src: /assets/img/posts/2021-07-07-Software-Engineering_Python_Python-성능-평가-지표와-혼동행렬/preview.jpg
---

# **개요**

분류 모델의 성능 평가 지표에 대해 생각해 보겠다. 성능 평가 지표에는 여러가지가 있으며, 설정한 과제에 따라 어떤 지표를 중시하는지는 각각 다르다. 이러한 성능 평가의 각 지표를 쉽게 확인할 수 있는 혼동행렬이 있다.

# **성능 평가 지표**

성능 평가 지표는 다음과 같이 나뉜다.

- 정답률(Accuracy): 모든 데이터의 판정 결과가 맞는지 여부를 산출

- 적합률(Precision): 양성 예측 중, 실제로 양성이 나타난 비율

- 재현율(Recall): 정말로 양성으로 나타난 사례 중 양성으로 예측할 수 있는 비율

# **혼동행렬**

혼동행렬은 예측 결과와 실제를 비교하여 얼마나 정답인지를 보는 것이다.

<table class="GeneratedTable" style="margin-top: 30px; margin-bottom: 20px;">
  <thead>
    <tr>
      <th class="center"></th>
      <th class="center">Negative(음성) 예상</th>
      <th class="center">Positive(양성) 예상</th>
      <th class="center">Recall(재현율) 예상</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center" style="width: 30%; font-weight: bold;">실제값이 Negative(음성)</td>
      <td class="center">TN</td>
      <td class="center">FP</td>
      <td class="center">TN / (TN+FP)</td>
    </tr>
    <tr>
      <td style="text-align: center; font-weight: bold;">실제값이 Positive(양성)</td>
      <td class="center">FN</td>
      <td class="center">TP</td>
      <td class="center">TP / (FN+TP)</td>
    </tr>
    <tr>
      <td style="text-align: center; font-weight: bold;">Precision(적합률)</td>
      <td class="center">FN / (TN+FN)</td>
      <td class="center">TP / (FP+TP)</td>
      <td class="center">・</td>
    </tr>
  </tbody>
</table>

행방향을 실제값, 열방향을 예측으로 크로스 집합을 했을 때, 행방향의 비율을 계산한 것이 Recall(재현율), 열방향의 비율을 계산한 것이 Precision(적합률)이 된다. 또한, 전체에 대한 정답의 비율 $(TP+TN) / (TP+FN+FP+TN)$이 Accuracy(정답률)이 된다.

# **어느 지표를 중시해야하나**

머신러닝에서 모델을 만들 때, 정답률을 볼 수는 있지만 얼마나 성과가 있었는지를 보는 정답률만 보는 것은 불충분하다. 예를 들어 `100`개의 데이터가 있고 `90`개가 Positive(양성), `10`개가 Negative(음성)인 경우, "모든 데이터를 Positive (양성)"이라고 예측해도 정답률은 90%가 되지만 Negative(음성)에 대한 예측은 모두 분리되어 있기 때문에 제대로 예측할 수 있다고는 말할 수 없다. 이처럼 정답률만 보는 것으로 모델의 성능 평가하기에 충분하지 않다.

Precision(적합률)과 Recall(재현율)에는 트레이드 오프 관계가 있다. 따라서 해결하고 싶은 과제마다 어떤 지표가 중요한지를 생각해야한다.

다음은 적합률을 우선하는 경우와 재현율을 우선하는 경우에 어떤 것이 있는지 예시를 들었다.

- 적합률을 우선하는 경우  
스팸 메일 판정 등은 적합률을 우선하는 예시다. 이 경우 Positive(양성: 스팸), Negative(음성: 스팸 아님)로 두었을 때, 스팸으로 예측한 것이 실제로 스팸일 확률을 중시하는 것이 된다. 적합률 $>$ 재현율이 되기 때문에 실제로는 스팸 메일이여도 스팸 판정이 되지 않는 케이스를 어느 정도 허용하는 것으로 중요한 메일이 스팸과 오판정되지 않게 한다.

- 재현율을 우선하는 경우  
암 검사의 경우 등은 재현율을 우선하는 예시다. 이 경우 Positive(양성: 암), Negative(음성: 암 아님)로 두었을 때, 실제로 암인 사람이 암이라고 예측해서 추출할 수 있는 것이 중요하다.

정리하면 적합율은 예측이 정답하는 것이 중요하고, 음성을 양성으로 오판정하고 싶지 않을 때, 재현율은 실제 양성을 추출하는 것이 중요하고, 음성을 양성으로 오판정하는 것을 어느 정도 허용한다.

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%;">
어떤 시스템에 대해서 외부로부터 액세스가 있었을 경우에 그것이 시스템에 대한 공격인지 아닌지를 판정(양성: 공격)한다고 했을 때, 양성의 경우에는 액세스를 차단하고 시스템을 이용할 수 없게 제어한다.
</div>

이 경우, 적합률과 재현율 중 어느 쪽을 중시하는 것이 좋을지는 단번에 말할 수는 없지만, 무엇을 중시하는지에 따라 다르다.

사용자의 접근을 중요시하는 경우에는 적합률을 중시하게 될 것이고, 시스템에는 중요한 자산이 있기 때문에 제대로 보호하고 싶다면 재현율을 중시할 것이다. 전자의 경우는 사용자의 접근을 중시하기 때문에 음성의 사용자를 양성으로 오판정하여 차단하고 싶지 않으므로 적합률을 중시하고, 후자의 경우는 공격을 추출하는 것이 중요하며, 실제로는 공격하지 않은 사용자의 일부 오판을 허용하여 재현율을 중시한다는 것이다.

## **혼동행렬 정리**

혼동행렬은 `skleran`에서 사용할 수 있다. 간단한 예시로 시도해 보자. 혼동행렬은 실제값(행방향)과 예측한 값(열방향)의 크로스 집계이기에, 다음과 같은 데이터를 준비한다.

```python
# 실제값과 예측값의 데이터 작성
true = [0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 0, 1] 
pred = [0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 1, 1]
```

실제값과 예측값의 데이터를 직접 작성했다. 이 데이터를 바탕으로 혼동행렬을 구해보자. `sklearn`의 `confusion_matrix` 함수를 이용해 본다.

```python
# import modules
from sklearn.metrics import confusion_matrix

# 혼동행렬 구하기
confusion_matrix(true, pred)
```

```output
array([[8, 4],
       [3, 5]], dtype=int64)
```

$TN = 8$, $FP = 4$, $FN = 3$, $TP = 5$이다. 때문에, 재현율, 적합률, 성과율은 다음과 같이 구해진다.

재현율 $= 5 / (3+5) = 0.625$  
적합률 $= 5 / (4+5) = 0.556$  
정답률 $= (8+5) / (8+5+4+3) = 0.65$

## **각 성능 평가 지표 정리**

앞의 예와 같이 혼동행렬을 구하고 그 요소에서 각 성능지표를 구해도 되지만, `sklearn`에서는 이러한 지표도 간단하게 구할 수 있다.

### **재현율**

```python
# import modules
from sklearn.metrics import recall_score

# 재현율 산출
print(recall_score(true, pred))
```

```output
0.625
```

### **적합률**

```python
# import modules
from sklearn.metrics import precision_score

# 적합률 산출
print(precision_score(true, pred))
```

```output
0.5555555555555556
```

### **정답률**

```python
# import modules
from sklearn.metrics import accuracy_score

# 정답률 산출
print(accuracy_score(true, pred))
```

```output
0.65
```

# **정리**

이와 같이 해결하고자 하는 과제별로 어떤 성능 평가 지표를 중시하는지를 검토하는 것이 중요하다.
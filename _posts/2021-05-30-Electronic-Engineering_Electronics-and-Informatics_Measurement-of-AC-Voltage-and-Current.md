---
title: Electronics and Informatics / Measurement of AC Voltage and Current
author: DEVHEE
date: 2021-05-30 23:23:26 +0900
categories: [Electronic Engineering, Electronics and Informatics]
tags: [electronic engineering, electronics, informatics, ac, voltage, current]
math: true
image:
    src: /assets/img/posts/2021-05-30-Electronic-Engineering_Electronics-and-Informatics_Measurement-of-AC-Voltage-and-Current/preview.jpeg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

# **Measurement of AC Voltage and Current**

## **1. 목적**

교류파형을 오실로스코프, 교류 계기를 이용하여 측정하고, 정현파 교류 및 비정현파 교류의 실효값, 평균값에 대한 개념을 파악하는 것을 목적으로 한다. 또한, 교류 계기의 주파수 특성을 알아본다.

## **2. 이론**

교류란, 전압 또는 전류의 값과 방향이 시간에 따라 주기적으로 변화하는 것을 말한다. 교류의 크기를 정하는 양으로서는 최대값(피크값), 실효값, 평균값 등이 있다.

실효값은 전류의 순시값$(e, i)$의 제곱의, 한 주기$(T)$의, 평균값의, 평방근으로 정의된다. 즉, 교류전압, 전류의 실효값을 각각 $E$, $I$라고 하면 정의 따른 다음식에 의해 구해진다.

$$
E=\sqrt{\frac{1}{T} \int_{0}^{T} e^{2} d t}
$$

*$[1]$*

$$
I=\sqrt{\frac{1}{T} \int_{0}^{T} i^{2} d t}
$$

*$[2]$*

교류파형의 여하를 불문하고 교류전압 또는 전류의 크기는 $[1]$, $[2]$식에 의해 정의된 실효값을 나타내는 것이 보통이다. 일반적인 교류 계기에서는 이 실효값으로 눈금을 새긴다.

여기에서 특히 정현파 교류에 대해 생각해보자. 전류의 순시값을 $i$, 최대값을 $I_m$, 각주파수를 $w$, 시간을 $t$라고 하면

$$
i=I_{m} \sin \omega t
$$

*$[3]$*

또한, 주파수를 $f$, 주기를 $T$라고 하면, $\omega=2 \pi f=2 \pi / T$가 된다. 따라서, $[2]$식에 따른 전류의 실효값 $I$는

$$
I=\sqrt{\frac{1}{T} \int_{0}^{T} I_{m}^{2} \sin ^{2} \omega t d t}=\sqrt{\frac{I_{m}^{2}}{T} \int_{0}^{T} \frac{1-\cos 2 \omega t}{2} d t}=\frac{I_{m}}{\sqrt{2}} \approx 0.717 I_{m}
$$

*$[4]$*

이와 같이, 정현파 전압 $e=E_m sin \omega t$의 실효값 $E$는 $[1]$식에 따라 $E=E_{m} / \sqrt{2} \approx 0.717 E_{m}$이 된다.

발열효과 즉 소비전력량의 관점에서 교류의 실효값이란 그 발생발열량이 같아지게 되도록 환산된 직류값과 같다고 생각할 수 있다. 교류전류 $i$가 저항 $R$에 1주기간 ($T$초간) 흐를 때에 발생하는 열량를 $W$로 나타내면,

$$
W=R \int_{0}^{T} i^{2} d t
$$

*$[5]$*

한편, 직류전류 $I$가 저항 $R$에 $T$초간 흐를 때의 발생열량 $W'$는,

$$
W'=RI^2T
$$

*$[6]$*

이기 때문에, $W=W'$으로 두면 $[5]$, $[6]$식에 따라

$$
RI^2T=R \int_{0}^{T} i^{2} d t
$$

*$[7]$*

$I$에 대해 풀면

$$
I=\sqrt{\frac{1}{T} \int_{0}^{T} i^{2} d t}
$$

*$[8]$*

이 되고, $[2]$식에서 정의된 전류의 실효값이 된다.

다음으로, 전류의 평균값은 그 순시값의, 절댓값의, 1주기의, 평균으로 정의된다. 교류전압, 전류의 평균값을 각각 $E_a$, $I_a$라고 하면 정의에 따라 다음과 같은 식에 의해 구할 수 있다.

$$
E_{a}=\frac{1}{T} \int_{0}^{T}|e| d t
$$

*$[9]$*

$$
I_{a}=\frac{1}{T} \int_{0}^{T}|i| d t
$$

*$[10]$*

정현파 전압 $e=E_m sin w t$의 평균값은 $[9]$식에 의해

$$
E_{a}=\frac{1}{T} \int_{0}^{T}\left|E_{m} \sin \omega t\right| d t=\frac{2}{T} \int_{0}^{\frac{T}{2}} E_{m} \sin \omega t d t=\frac{2}{\pi} E_{m} \approx 0.64 E_{m} \approx 0.9 E
$$

*$[11]$*

정현파 교류의 평균값은 그 실효값의 $0.9$배 또는 최대값의 $0.64$배와 같다. 정류형 계기의 진동은 이론적으로 평균값을 나타내지만, 눈금은 실효값으로 나타낸다. 또한, 파형률 및 파고율은 다음과 같이 정의된다.

$$
\text { 파형률 }=\frac{\text { 실효값 }}{\text { 평균값 }}, \quad \text { 파고율 }=\frac{\text { 최대값 }}{\text { 실효값 }}
$$


---
title: Control Engineering / 1. Linear Differential Equation and Transfer Function
author: DEVHEE
date: 2021-05-10 12:01:49 +0900
categories: [Computer Engineering, Control Engineering]
tags: [computer engineering, control engineering, linear differential equation, transfer function, artificial intelligence]
math: true
image:
    path: /assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/preview.jpg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">글, 그림 및 수식이 많아 불러오는데 시간이 다소 걸릴 수 있습니다.</b><br>
</div>

# **1. Linear Differential Equation and Transfer Function**

## **1.1. Differential Equation and Transfer Function**

수학 모델의 미분 방정식을 구한다고 해 보자. 이 때, 입력`input`과 출력`output`의 선택에 주의한다. 입력이란 힘이나 전압 등 자유롭게 조작할 수 있는 변수`variable`이다. 출력이란 제어할 양(제어량`controlled variable`)으로서 주목하는 변수이다.

![Fig. 1.1](/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/fig_1.1.png)

*$[Fig.\,1.1]$ Damped One-Degree System*

$[Fig.\,1.1]$의 1자유도 감쇠계`damped one-degree system`의 수학정 모델을 구해보자. $x$는 물체의 변위`displacement`, $u$는 물체에 작용하는 힘`force`, $m$은 질량`mass`, $k$는 용수철 상수`spring constant`, $c$는 점성감쇠계수`viscous damping coefficient`이다. 달랑베르의 원리`D’Alembert’s principle` (동적인 힘을 포함하여 힘의 균형식을 세울 수 있다는 원리)에 따라 운동방정식`equation of motion`을 포함하면

$$
u-m \ddot{x}-c \dot{x}-k x=0
$$

즉

$$
m \ddot{x}+c \dot{x}+k x=u
$$

*$[1.1]$*

을 얻을 수 있다. 이 경우, 입력은 $u$이다. 출력($y$로 나타낸다)으로서는, $x$나 $\ddot{x}$, 또는 이들의 선형결합

$$
y=b_{0} x+b_{1} \dot{x}
$$

*$[1.2]$*

등을 생각할 수 있다. $y$가 $[1.2]$식에서 주어진 경우, $y$와 $u$에 관한 미분방정식을 구해보자. $[1.1]$식에 $b_0$을 곱한다.

$$
b_{0}(m \ddot{x}+c \dot{x}+k x)=b_{0} u
$$

$[1.1]$식을 $t$로 미분하고, $b_1$를 곱한다.

$$
b_{1}\left(m x^{(3)}+c \ddot{x}+k \dot{x}\right)=b_{1} \dot{u}
$$

이것을 각 변끼리 더하면

$$
m\left(b_{0} \ddot{x}+b_{1} x^{(3)}\right)+c\left(b_{0} \dot{x}+b_{1} \ddot{x}\right)+k\left(b_{0} x+b_{1} \dot{x}\right)=b_{0} u+b_{1} \dot{u}
$$

즉

$$
m \ddot{y}+c \dot{y}+k y=b_{0} u+b_{1} \dot{u}
$$

*$[1.3]$*

을 얻는다.

광범위한 수학 모델을 $[1.3]$식과 같은 미분방정식으로 표현할 수 있다. 제어공학에서 다루는 미분방정식의 일반형은 다음과 같다.

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%;">
<b>General Form of Differential Equations</b><br>
$$
\frac{d^{n} y}{d t^{n}}+a_{n-1} \frac{d^{n-1} y}{d t^{n-1}}+\cdots+a_{1} \frac{d y}{d t}+a_{0} y=b_{m} \frac{d^{m} u}{d t^{m}}+b_{m-1} \frac{d^{m-1} u}{d t^{m-1}}+\cdots+b_{1} \frac{d u}{d t}+b_{0} u
$$

<em>$[1.4]$</em>

여기서, $n \geq m$
</div>

## **1.2. Transfer Fucntion**

전달함수`transfer fuction`은 입력과 출력의 관계를 주어주는 함수이며 아래와 같이 정의된다.

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%;">
<b>Definition of a Transfer Function</b><br>

$$
G(s)=\frac{Y(s)}{U(s)}
$$

<em>$[1.5]$</em>

여기서, $Y(s)$, $U(s)$는 각각 $y(t)$, $u(t)$의 라플라스 변환<code class="language-plaintext highlighter-rouge">Laplace transform</code>이다. 단, 모든 초기값은 $0$으로 둔다.
</div>

![Fig. 1.2](/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/fig_1.2.png)

*$[Fig.\,1.2]$ Block diagram of System with Transfer Function $G(s)$*

$[1.5]$식은 블록 다이어그램`block diagram`에 다라 $[Fig.\,1.2]$와 같이 나타내어진다. $s$는 미분연산  $d/dt$을 나타내는 기호 (연산자`operator`)라고 해석해도 된다.

**예제 1.1.** 다음 미분방정식으로 나타내진 시스템의 전달함수를 구해라.

$$
\ddot{y}+a_{1} \dot{y}+a_{0} y=b_{1} \dot{u}+b_{0} u
$$

**[해답]** 미분방정식을 모든 초기값이 $0$ ($y(0)=0, \dot{y}(0)=0, u(0)=0$) 이라는 조건하에 라플라스 변환을 하면

$$
s^{2} Y(s)+a_{1} s Y(s)+a_{0} Y(s)=b_{1} s U(s)+b_{0} U(s)
$$

가 된다. 이제 전달함수로 다음 식을 얻는다.

$$
\frac{Y(s)}{U(s)}=\frac{b_{1} s+b_{0}}{s^{2}+a_{1} s+a_{0}}
$$

위와 같이 미분방정식과 전달함수는 둘 다 수학 모델을 나타내고 있으며, 한 쪽에서 다른 쪽을 얻을 수 있다는 의미에서 등가(等価)이다. 다음으로 전달함수가 주어졌을 경우, 이에 대응하는 미분방적식을 구해보자.

**예제 1.2.** 다음 전달함수로 나타내진 시스템의 미분방정식 구해라.

$$
\frac{Y(s)}{U(s)}=\frac{b_{1} s+b_{0}}{s^{2}+a_{1} s+a_{0}}
$$

**[해답]** 전달함수 표현에서 다음 식을 얻는다.

$$
s^{2} Y(s)+a_{1} s Y(s)+a_{0} Y(s)=b_{1} s U(s)+b_{0} U(s)
$$

이것을 시간영역 표현으로 바꾸면

$$
\ddot{y}+a_{1} \dot{y}+a_{0} y=b_{1} \dot{u}+b_{0} u
$$

가 된다.

## **1.3. Default Transfer Function**

간단한 시스템의 전달 함수나 시스템 구성 단위가 되는 전달 함수로서 다음의 기본 전달 함수가 있다. 비례 요소`proportional element`, 미분 요소`derivative element`, 적분 요소`integral element`, 1차 지연 요소(first-order lag element), 2차 요소(second-order element), 시간 낭비 요소(dead time element). 이들의 전달 함수를 $[Table\,1.1]$에 나타냈다.

**예제 1.3.** 비례요소의 시간영역 입출력 관계를 구해라.

**[해답]**

$$
\frac{Y(s)}{U(s)}=K
$$

에서 시간영역 표현으로

$$
y=K u
$$

를 얻을 수 있다.

<style>
table.GeneratedTable {
  width: 100%;
  background-color: #ffffff;
  border-collapse: collapse;
  border-width: 1px;
  border-color: #000000;
  border-style: solid;
  color: #000000;
}

table.GeneratedTable td, table.GeneratedTable th {
  border-width: 1px;
  border-color: #000000;
  border-style: solid;
  padding: 3px;
}

.fill {
  background-color: #ebebeb;
  font-weight: 600;
  width: 50%;
}
.ele{
    width: 50%;
}
</style>

<table class="GeneratedTable" style="margin-top: 60px; margin-bottom: 20px;">
  <tbody>
    <tr>
      <td class="rowtable" style="text-align: center; width: 50%;">Element Name</td>
      <td style="text-align: center;">$G(s)$</td>
    </tr>
    <tr>
      <td class="rowtable" style="text-align: center;">Proportional Element</td>
      <td style="text-align: center;">$K$</td>
    </tr>
    <tr>
      <td class="rowtable" style="text-align: center;">Derivative Dlement</td>
      <td style="text-align: center;">$s$</td>
    </tr>
    <tr>
      <td class="rowtable" style="text-align: center;">Integral Element</td>
      <td style="text-align: center;">$\frac{1}{s}$</td>
    </tr>
    <tr>
      <td class="rowtable" style="text-align: center;">First-Order Lag Element</td>
      <td style="text-align: center;">$\frac{1}{1+T s}$</td>
    </tr>
    <tr>
      <td class="rowtable" style="text-align: center;">Second-Order Element</td>
      <td style="text-align: center;">$\frac{\omega_{n}^{2}}{s^{2}+2 \zeta \omega_{n} s+\omega_{n}^{2}}$</td>
    </tr>
    <tr>
      <td class="rowtable" style="text-align: center;">Dead Time Element</td>
      <td style="text-align: center;">$e^{-L s}$</td>
    </tr>
  </tbody>
</table>

*$[Table\,1.1]$*

**예제 1.4.** 1차 지연 요소의 시간영역 입력함수를 구해라.

**[해답]**

$$
\frac{Y(s)}{U(s)}=\frac{1}{1+T s}
$$

여기에서

$$
\frac{Y(s)}{U(s)}=\frac{1}{1+T s}
$$

시간영역으로 바꾸면

$$
T \dot{y}+y=u
$$

이 된다.

**예 1.1. (비례요소)** 용수철 시스템: 힘을 $u$, 변위를 $y$, 용수철 상수를 $k$로 하면 다음 관계(훅의 법칙`Hook's law`)가 성립한다.

$$
y=\frac{1}{k}u
$$

이것을 라플라스 변환을 하면

$$
Y(s)=\frac{1}{k} U(s)
$$

가 된다. 여기서 전달함수로서 다음 식을 얻을 수 있다.

$$
\frac{Y(s)}{U(s)}=\frac{1}{k}
$$

![Figs. 1.3-1.4](/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/fig_1.3-1.4.png)

*$[Fig.\,1.3]$ Spring System (Proportional Element) / $[Fig.\,1.4]$ RL Circuit System (Differential Element)*

**예 1.2. (미분요소)** RL 회로 시스템: 전압 $v$와 전류 $i$와의 사이에 다음 관계가 있다.

$$
v(t)=L \dot{i}(t)
$$

따라서, $I(s)$에서 $V(s)$까지의 전달함수는

$$
\frac{V(s)}{I(s)}=L s
$$

가 된다.

![Figs. 1.5-1.6](/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/fig_1.5-1.6.png)

*$[Fig.\,1.5]$ C Circuit System (Integral Element) / $[Fig.\,1.6]$ RC Circuit System (First-Order Lag Element)*

**예 1.3. (적분요소)** C 회로 시스템: 전압 $v_o$과 전류 $i$와의 사이에 다음 관계가 성립한다.

$$
v_{o}(t)=\frac{1}{C} \int i(t) d t
$$

이것을 $t$로 미분하면

$$
\dot{v}_{o}=\frac{1}{C} i
$$

라플라스 변환하여

$$
s V_{o}(s)=\frac{1}{C} I(s)
$$

따라서, $I$부터 $V_o$까지의 전달함수는

$$
\frac{V_{o}(s)}{I(s)}=\frac{1}{C s}
$$

이 된다.

**예 1.4. (1차 지연 요소)** RC 회로 시스템: 전압의 평형식으로부터

$$
R i(t)+v_{o}(t)=v_{i}(t)
$$

$v_o$과 $i$의 사이에는

$$
v_{o}(t)=\frac{1}{C} \int i(t) d t
$$

즉

$$
i(t)=C \dot{v}_{o}(t)
$$

라는 관계가 있으며, 이것을 이용해 정리하면

$$
\dot{v}_{o}(t)=\frac{1}{R C}\left(v_{i}(t)-v_{o}(t)\right)
$$

를 얻을 수 있다. 또한, 라플라스 변환을 하면

$$
s V_{o}(s)=\frac{1}{R C}\left(V_{i}(s)-V_{o}(s)\right)
$$

따라서, $V_i(s)$부터 $V_o(s)$까지의 전달함수는

$$
\frac{V_{o}(s)}{V_{i}(s)}=\frac{1}{1+R C s}
$$

이 된다.


## **1.4. Exercise**

1. 다음 전달함수를 갖는 시스템의 시간영역 입출력 관계를 구해라.  
   (1) $\frac{Y(s)}{U(s)}=\frac{\omega_{n}^{2}}{s^{2}+2 \zeta \omega_{n} s+\omega_{n}^{2}}$  
   (2) $\frac{Y(s)}{U(s)}=\frac{5(s+1)}{(s+2)(s+3)}$

   
2. 다음 미분방정식으로 표현되는 시스템의 전달함수를 구해라.  
   (1) $\dot{h}(t)=\frac{1}{C} q(t)$　입력: $q$　출력: $h$  
   (2) $L C \ddot e_{o}(t)+R C \dot e_{o}(t)+e_{o}(t)=e_{i}(t)$　입력: $e_i$　출력: $e_o$
   
3. $[Fig.\,1.7]$의 2자유도계의 전달함수를 구해라. 단, $m_1$, $m_2$는 질량, $c_1$은 점성감쇠계수, $k_1$, $k_2$는 용수철 상수, $f$는 외력, $x_1$, $x_2$는 변위이다. 입력을 $f$, 출력을 $x_1$이라고 한다.  
![Fig. 1.7](/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/fig_1.7.png)  
*$[Fig.\,1.7]$ Damped Two-Degree System*

4. $[Fig.\,1.8]$의 직렬결합된 수조(水槽) 시스템의 전달함수를 구해라. 단, $q_1$은 기준유입량에서의 편차, $x_1$, $x_2$는 평형수위로부터의 편차, $C_1$, $C_2$는 수조의 단면적, $R_1$, $R_2$는 유출저항이다. 입력은 $q_1$, 출력은 $x_2$로 한다.  
![Fig. 1.8](/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/fig_1.8.png)  
*$[Fig.\,1.8]$ Aquarium System Coupled in Series*
   
5. $[Fig.\,1.9]$의 회로 시스템의 전달함수를 구해라. 입력을 $v_i$, 출력을 $v_o$로 한다.  
![Fig. 1.9](/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/fig_1.9.png)  
*$[Fig.\,1.9]$ LRC Circuit System*

**[풀이]**

<div oncontextmenu="return false" ondragstart="return false" onselectstart="return false" class="safe">
    <img src="/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/exercise-1_1.devhee" style="margin-top: 3%; margin-bottom: 3%;">
    <img src="/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/exercise-1_2.devhee" style="margin-top: 3%; margin-bottom: 3%;">
    <img src="/assets/img/posts/2021-05-10-Computer-Engineering_Control-Engineering_1-Linear-Differential-Equation-and-Transfer-Function/exercise-1_3.devhee" style="margin-top: 3%; margin-bottom: 3%;">
</div>
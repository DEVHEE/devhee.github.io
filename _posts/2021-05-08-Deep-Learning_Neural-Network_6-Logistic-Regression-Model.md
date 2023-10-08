---
title: Neural Network Basic / 6. Logistic Regression Model
author: DEVHEE
date: 2021-05-08 11:52:20 +0900
categories: [Deep Learning, Neural Network]
tags: [deep learning, neural network, logistic regression, artificial intelligence]
math: true
image:
    src: /assets/img/posts/2021-05-08-Deep-Learning_Neural-Network_6-Logistic-Regression-Model/preview.jpg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

# **6. Logistic Regression Model**

퍼셉트론에서 사용한 임계함수는 입력값이 양인 경우와 음인 경우에 출력이 갑자기 변화하는 불연속 함수이기 때문에 해석적 취급이 간단하지 않다. ADALINE 모델에서는 퍼셉트론 임계논리소자 선형 부분의 선형모델을 사용했다. 그러나 선형 모델화에서는 복수의 뉴런을 결합해도 전체 모델이 선형이 되어버려 비선형 함수를 표현할 수 없다. 또한, 실제 뉴런에 가까운 모델을 만든다는 관점에서도 바람직 하지 않다. 최근 뉴럴 네트워크에서는 임계함수 대신에 입력이 음에서 양으로 변화할 때, 그 출력도 연속적으로 매끄럽게 변화하는 출력함수

$$
S(\eta)=\frac{\exp (\eta)}{1+\exp (\eta)}
$$

*$[38]$*

이 이용된다. 이 함수는 로지스틱 함수라고 불린다. $[Fig.\,3]$ (c)([이전 포스팅](https://kimdonghee.dev/posts/Deep-Learning_Neural-Network_5-ADALINE/){:target="_blank"})이 로지스틱 함수의 예시이다. 이 로지스틱 함수를 출력함수로서 사용한 가장 간단한 모델

$$
y=S\left(\sum_{i=1}^{M} a_{i} x_{i}+a_{0}\right)
$$

*$[39]$*

는 로지스틱 회귀 모델이라고 불린다.

다음으로 이 로지스틱 회귀 모델의 파라미터 추정법에 대해 설명하겠다. ADALINE 모델에서는 평균제곱오차가 최소가 되도록 파라미터를 추정정하지만 여기서는 최대우도법[^1]이라고 불리는 방법으로 파라미터를 추정해본다. 예제로는 [이전 포스팅](https://kimdonghee.dev/posts/Deep-Learning_Neural-Network_5-ADALINE/){:target="_blank"}의 튤립 식별 문제를 생각해보자.

## **6.1. Logistic Regression Model**

식$[39]$의 로지스틱 회귀 모델에서는 출력은 0에서 1 사이의 값으로 튤립 다이너스티의 경우에는 1에 가까운 값을 출력하고, 그렇지 않은 경우(튤립 아틀란티스인 경우)에는 0에 가까운 값을 출력하도록 한다. 로지스틱 회귀 모델의 출력 $y$를 튤립 다이너스티일 확률로 해석한다. 또한, 이 문제에서는 튤립의 종류는 2종류만 한정했기 때문에 튤립 아틀란티스일 확률은 $1-y$라고 해석할 수 있다. 따라서, 100개의 튤립 계측 데이터를 얻을 수 있는 우도는

$$
L=\prod_{l=1}^{100}\left(y_{l}\right)^{t_{l}}\left(1-y_{l}\right)^{1-t_{l}}
$$

*$[40]$*

과 같이 각각의 확률의 곱으로 정의할 수 있다. 여기에 로그를 취하면

$$
\begin{aligned}
\log (L) &=\sum_{l=1}^{100}\left\{t_{l} \log y_{l}+\left(1-t_{l}\right) \log \left(1-y_{l}\right)\right\} \\
&=\sum_{l=1}^{100}\left\{t_{l} \log \left\{\frac{\exp \left(\eta_{l}\right)}{1+\exp \left(\eta_{l}\right)}+\left(1-t_{l}\right) \log \left\{\frac{1}{1+\exp \left(\eta_{l}\right)}\right\}\right\}\right.\\
&=\sum_{l=1}^{100}\left\{t_{l} \eta_{l}-\log \left\{1+\exp \left(\eta_{l}\right)\right\}\right\}
\end{aligned}
$$

*$[41]$*

이 된다. 이 우도의 로그는 일반적으로 대수우도라고 불린다. 우도를 최대로 하는 것은 대수우도를 최대로 하는 것과 같고, 대수우도를 이용하면 계산이 간단해지는 경우가 많기 때문에 일반적으로 대수우도를 최대로 하는 파라미터가 요구된다.

지금까지와 마찬가지로 최급강하법을 적용하기 위해서는 평가함수(대수우도)를 각 파라미터로 미분하는 것이 필요하다. 대수우도를 파라미터 $a_0$로 미분하면

$$
\frac{\partial \log (L)}{\partial a_{0}}=\sum_{l=1}^{100}\left\{t_{l}-\frac{\exp \left(\eta_{l}\right)}{1+\exp \left(\eta_{l}\right)}\right\}=\sum_{l=1}^{100}\left\{t_{l}-y_{l}\right\}
$$

*$[42]$*

와 같이 된다. 마찬가지로 대수우도를 파라미터 $a_1, a_2, a_3, a_4$로 미분하면

$$
\begin{array}{l}
\frac{\partial \log (L)}{\partial a_{1}}=\sum_{l=1}^{100}\left\{t_{l} x 1_{l}-\frac{\exp \left(\eta_{l}\right)}{1+\exp \left(\eta_{l}\right)} x 1_{l}\right\}=\sum_{l=1}^{100}\left\{\left(t_{l}-y_{l}\right) x 1_{l}\right\} \\
\frac{\partial \log (L)}{\partial a_{2}}=\sum_{l=1}^{100}\left\{t_{l} x 2_{l}-\frac{\exp \left(\eta_{l}\right)}{1+\exp \left(\eta_{l}\right)} x 2_{l}\right\}=\sum_{l=1}^{100}\left\{\left(t_{l}-y_{l}\right) x 2_{l}\right\} \\
\frac{\partial \log (L)}{\partial a_{3}}=\sum_{l=1}^{100}\left\{t_{l} x 3_{l}-\frac{\exp \left(\eta_{l}\right)}{1+\exp \left(\eta_{l}\right)} x 3_{l}\right\}=\sum_{l=1}^{100}\left\{\left(t_{l}-y_{l}\right) x 3_{l}\right\} \\
\frac{\partial \log (L)}{\partial a_{4}}=\sum_{l=1}^{100}\left\{t_{l} x 4_{l}-\frac{\exp \left(\eta_{l}\right)}{1+\exp \left(\eta_{l}\right)} x 4_{l}\right\}=\sum_{l=1}^{100}\left\{\left(t_{l}-y_{l}\right) x 4_{l}\right\}
\end{array}
$$

*$[43]$*

이 된다. 대수우도를 최대로 하는 파라미터를 구하기 위해서는 미분과 같은 방향으로 파라미터를 갱신시키면 되기 때문에 파라미터 갱신식은

$$
\begin{array}{l}
a_{0}^{(k+1)}=a_{0}^{(k)}+\alpha \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) \\
a_{1}^{(k+1)}=a_{1}^{(k)}+\alpha \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) x 1_{l} \\
a_{2}^{(k+1)}=a_{2}^{(k)}+\alpha \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) x 2_{l} \\
a_{3}^{(k+1)}=a_{3}^{(k)}+\alpha \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) x 3_{l} \\
a_{4}^{(k+1)}=a_{4}^{(k)}+\alpha \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) x 4_{l}
\end{array}
$$

*$[44]$*

가 된다. 이 갱신식은 앞서 말한 ADALINE의 갱신식과 거의 같다는 것을 알 수 있다.

로지스틱 회귀의 경우에는 출력값이 0에서 1 사이의 값을 취해 튤립 다이너스티일 확률의 추정치라고 해석할 수 있었기에 튤립을 식별하려면 출력값이 $0.5$이상이면 튤립 다이너스티, $0.5$이하면 튤립 아틀란티스라고 판단하면 된다. 

[이전 포스팅](https://kimdonghee.dev/posts/Deep-Learning_Neural-Network_5-ADALINE/){:target="_blank"}의 ADALINE 프로그램을 수정해서 로지스틱 회귀 모델을 이용해 튤립을 식별하기위한 파라미터를 학습하는 프로그램을 만들어 보면 다음과 같다.

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

#define frand() rand() / ((double)RAND_MAX)
#define NSAMPLE 100
#define XDIM 4

double logit(double eta)
{
    return (exp(eta) / (1.0 + exp(eta)));
}

main()
{
    FILE *fp;
    double t[NSAMPLE];
    double x[NSAMPLE][XDIM];
    double a[XDIM + 1];
    int i, j, l;
    double eta;
    double y, err, likelihood;
    double derivatives[XDIM + 1];
    double alpha = 0.1; /* Learning Rate */

    /* Open Data File */
    if ((fp = fopen("tulip.dat", "r")) == NULL)
    {
        fprintf(stderr, "File Open Fail\n");
        exit(1);
    }

    /* Read Data */
    for (l = 0; l < NSAMPLE; l++)
    {
        /* Input input vectors */ for (j = 0; j < XDIM; j++)
        {
            fscanf(fp, "%lf", &(x[l][j]));
        }
        /* Set teacher signal */
        if (l < 50)
            t[l] = 1.0;
        else
            t[l] = 0.0;
    }
    /* Close Data File */
    fclose(fp);

    /* Print the data */
    for (l = 0; l < NSAMPLE; l++)
    {
        printf("%3d : %8.2f ", l, t[l]);
        for (j = 0; j < XDIM; j++)
        {
            printf("%8.2f ", x[l][j]);
        }
        printf("\n");
    }

    /* Initialize the parameters by random number */
    for (j = 0; j < XDIM + 1; j++)
    {
        a[j] = (frand() - 0.5);
    }

    /* Open output file */
    fp = fopen("likelihood.out", "w");

    /* Learning the parameters */
    for (i = 1; i < 100; i++)
    { /* Learning Loop */
        /* Compute derivatives */
        /* Initialize derivatives */
        for (j = 0; j < XDIM + 1; j++)
        {
            derivatives[j] = 0.0;
        }
        /* update derivatives */
        for (l = 0; l < NSAMPLE; l++)
        {
            /* prediction */
            eta = a[0];
            for (j = 1; j < XDIM + 1; j++)
            {
                eta += a[j] * x[l][j - 1];
            }
            y = logit(eta);

            /* error */
            err = t[l] - y;

            /* update derivatives */ derivatives[0] += err;
            for (j = 1; j < XDIM + 1; j++)
            {
                derivatives[j] += err * x[l][j - 1];
            }
        }
    }

    /* update parameters */
    for (j = 0; j < XDIM + 1; j++)
    {
        a[j] = a[j] + alpha * derivatives[j];
    }

    /* Compute Log Likelihood */
    likelihood = 0.0;
    for (l = 0; l < NSAMPLE; l++)
    {
        /* prediction */
        eta = a[0];
        for (j = 1; j < XDIM + 1; j++)
        {
            eta += a[j] * x[l][j - 1];
        }
        y = logit(eta);

        likelihood += t[l] * log(y) + (1.0 - t[l]) * log(1.0 - y);
    }

    printf("%d : Log Likeihood is %f\n", i, likelihood);
    fprintf(fp, "%f\n", likelihood);
}
```

이 프로그램은 최소제곱법을 최급강하법으로 푸는 프로그램과 거의 같다. 튤립 데이터파일 tulip.dat을 읽어들이고 그 데이터에 대해서 최급강하법으로 파라미터를 구한다. 교사신호가 실수값이 아닌 0과 1의 2개의 값으로 주어지는 것만 최소제곱법과의 차이점이다. 프로그램의 마지막 부분에서는 얻은 뉴럴 네트워크(식별기)의 장점을 확인하기 위해 학습에 이용한 튤립 데이터를 식별시킨다. 뉴럴 네트워크의 출력이 0과 1 중 어느 쪽에 가까운지에 따라 어느 것이 튤립인지를 결정한다. 프로그램의 실행 결과는 아래와 같다.

```c
Estimated Parameters
a[0]=1.239302, a[1]=0.145552, a[2]=0.139415, a[3]=-0.638937, a[4]=-0.537277,

0 [Class1 : correct] : t = 1.000000, y = 1.003690 (err = -0.003690)
1 [Class1 : correct] : t = 1.000000, y = 0.899888 (err = 0.100112)
2 [Class1 : correct] : t = 1.000000, y = 0.810625 (err = 0.189375)
3 [Class1 : correct] : t = 1.000000, y = 0.775510 (err = 0.224490)
4 [Class1 : correct] : t = 1.000000, y = 0.752820 (err = 0.247180)
5 [Class1 : correct] : t = 1.000000, y = 0.789633 (err = 0.210367)
6 [Class1 : correct] : t = 1.000000, y = 0.771009 (err = 0.228991)
7 [Class1 : correct] : t = 1.000000, y = 1.168271 (err = -0.168271)
8 [Class1 : correct] : t = 1.000000, y = 0.943976 (err = 0.056024)
9 [Class1 : correct] : t = 1.000000, y = 0.816619 (err = 0.183381)
10 [Class1 : correct] : t = 1.000000, y = 0.984887 (err = 0.015113)
11 [Class1 : correct] : t = 1.000000, y = 0.856557 (err = 0.143443)
12 [Class1 : correct] : t = 1.000000, y = 1.043678 (err = -0.043678)
13 [Class1 : correct] : t = 1.000000, y = 0.748846 (err = 0.251154)
14 [Class1 : correct] : t = 1.000000, y = 1.130948 (err = -0.130948)
15 [Class1 : correct] : t = 1.000000, y = 1.027689 (err = -0.027689)
16 [Class1 : correct] : t = 1.000000, y = 0.694755 (err = 0.305245)
17 [Class1 : correct] : t = 1.000000, y = 1.132590 (err = -0.132590)
18 [Class1 : correct] : t = 1.000000, y = 0.543723 (err = 0.456277)
19 [Class1 : correct] : t = 1.000000, y = 1.035076 (err = -0.035076)
20 [Class2 : not correct] : t = 1.000000, y = 0.490680 (err = 0.509320)
21 [Class1 : correct] : t = 1.000000, y = 1.041685 (err = -0.041685)
22 [Class1 : correct] : t = 1.000000, y = 0.512358 (err = 0.487642)
23 [Class1 : correct] : t = 1.000000, y = 0.858199 (err = 0.141801)
24 [Class1 : correct] : t = 1.000000, y = 1.017686 (err = -0.017686)
25 [Class1 : correct] : t = 1.000000, y = 0.977978 (err = 0.022022)
26 [Class1 : correct] : t = 1.000000, y = 0.803766 (err = 0.196234)
27 [Class1 : correct] : t = 1.000000, y = 0.565534 (err = 0.434466)
28 [Class1 : correct] : t = 1.000000, y = 0.733136 (err = 0.266864)
29 [Class1 : correct] : t = 1.000000, y = 1.300773 (err = -0.300773)
30 [Class1 : correct] : t = 1.000000, y = 1.021680 (err = -0.021680)
31 [Class1 : correct] : t = 1.000000, y = 1.128719 (err = -0.128719)
32 [Class1 : correct] : t = 1.000000, y = 1.063775 (err = -0.063775)
33 [Class2 : not correct] : t = 1.000000, y = 0.380334 (err = 0.619666)
34 [Class1 : correct] : t = 1.000000, y = 0.659518 (err = 0.340482)
35 [Class1 : correct] : t = 1.000000, y = 0.822877 (err = 0.177123)
36 [Class1 : correct] : t = 1.000000, y = 0.848019 (err = 0.151981)
37 [Class1 : correct] : t = 1.000000, y = 0.771196 (err = 0.228804)
38 [Class1 : correct] : t = 1.000000, y = 0.981463 (err = 0.018537)
39 [Class1 : correct] : t = 1.000000, y = 0.839696 (err = 0.160304)
40 [Class1 : correct] : t = 1.000000, y = 0.797250 (err = 0.202750)
41 [Class1 : correct] : t = 1.000000, y = 0.817255 (err = 0.182745)
42 [Class1 : correct] : t = 1.000000, y = 0.995367 (err = 0.004633)
43 [Class1 : correct] : t = 1.000000, y = 1.153796 (err = -0.153796)
44 [Class1 : correct] : t = 1.000000, y = 0.848869 (err = 0.151131)
45 [Class1 : correct] : t = 1.000000, y = 1.033489 (err = -0.033489)
46 [Class1 : correct] : t = 1.000000, y = 0.930673 (err = 0.069327)
47 [Class1 : correct] : t = 1.000000, y = 0.982449 (err = 0.017551)
48 [Class1 : correct] : t = 1.000000, y = 1.273824 (err = -0.273824)
49 [Class1 : correct] : t = 1.000000, y = 0.934896 (err = 0.065104)
50 [Class2 : correct] : t = 0.000000, y = -0.337600 (err = 0.337600)
51 [Class2 : correct] : t = 0.000000, y = 0.132929 (err = -0.132929)
52 [Class2 : correct] : t = 0.000000, y = 0.026276 (err = -0.026276)
53 [Class2 : correct] : t = 0.000000, y = 0.174352 (err = -0.174352)
54 [Class2 : correct] : t = 0.000000, y = -0.113841 (err = 0.113841)
55 [Class2 : correct] : t = 0.000000, y = -0.139841 (err = 0.139841)
56 [Class2 : correct] : t = 0.000000, y = 0.269516 (err = -0.269516)
57 [Class2 : correct] : t = 0.000000, y = 0.096326 (err = -0.096326)
58 [Class2 : correct] : t = 0.000000, y = 0.043823 (err = -0.043823)
59 [Class2 : correct] : t = 0.000000, y = -0.119072 (err = 0.119072)
60 [Class2 : correct] : t = 0.000000, y = 0.345999 (err = -0.345999)
61 [Class2 : correct] : t = 0.000000, y = 0.166008 (err = -0.166008)
62 [Class2 : correct] : t = 0.000000, y = 0.118683 (err = -0.118683)
63 [Class2 : correct] : t = 0.000000, y = 0.016717 (err = -0.016717)
64 [Class2 : correct] : t = 0.000000, y = -0.188593 (err = 0.188593)
65 [Class2 : correct] : t = 0.000000, y = 0.043580 (err = -0.043580)
66 [Class2 : correct] : t = 0.000000, y = 0.277996 (err = -0.277996)
67 [Class2 : correct] : t = 0.000000, y = 0.027482 (err = -0.027482)
68 [Class2 : correct] : t = 0.000000, y = -0.500986 (err = 0.500986)
69 [Class2 : correct] : t = 0.000000, y = 0.326909 (err = -0.326909)
70 [Class2 : correct] : t = 0.000000, y = -0.013590 (err = 0.013590)
71 [Class2 : correct] : t = 0.000000, y = 0.290259 (err = -0.290259)
72 [Class2 : correct] : t = 0.000000, y = -0.152001 (err = 0.152001)
73 [Class2 : correct] : t = 0.000000, y = 0.364375 (err = -0.364375)
74 [Class2 : correct] : t = 0.000000, y = 0.124712 (err = -0.124712)
75 [Class2 : correct] : t = 0.000000, y = 0.283933 (err = -0.283933)
76 [Class2 : correct] : t = 0.000000, y = 0.415164 (err = -0.415164)
77 [Class2 : correct] : t = 0.000000, y = 0.425416 (err = -0.425416)
78 [Class2 : correct] : t = 0.000000, y = -0.052291 (err = 0.052291)
79 [Class2 : correct] : t = 0.000000, y = 0.433825 (err = -0.433825)
80 [Class2 : correct] : t = 0.000000, y = 0.083760 (err = -0.083760)
81 [Class2 : correct] : t = 0.000000, y = 0.313110 (err = -0.313110)
82 [Class2 : correct] : t = 0.000000, y = -0.123014 (err = 0.123014)
83 [Class1 : not correct] : t = 0.000000, y = 0.536005 (err = -0.536005)
84 [Class2 : correct] : t = 0.000000, y = 0.325728 (err = -0.325728)
85 [Class2 : correct] : t = 0.000000, y = -0.082091 (err = 0.082091)
86 [Class2 : correct] : t = 0.000000, y = -0.089522 (err = 0.089522)
87 [Class2 : correct] : t = 0.000000, y = 0.292471 (err = -0.292471)
88 [Class2 : correct] : t = 0.000000, y = 0.444113 (err = -0.444113)
89 [Class2 : correct] : t = 0.000000, y = 0.204709 (err = -0.204709)
90 [Class2 : correct] : t = 0.000000, y = -0.115327 (err = 0.115327)
91 [Class2 : correct] : t = 0.000000, y = 0.172210 (err = -0.172210)
92 [Class2 : correct] : t = 0.000000, y = 0.132929 (err = -0.132929)
93 [Class2 : correct] : t = 0.000000, y = -0.103840 (err = 0.103840)
94 [Class2 : correct] : t = 0.000000, y = -0.158180 (err = 0.158180)
95 [Class2 : correct] : t = 0.000000, y = 0.068565 (err = -0.068565)
96 [Class2 : correct] : t = 0.000000, y = 0.193150 (err = -0.193150)
97 [Class2 : correct] : t = 0.000000, y = 0.245497 (err = -0.245497)
98 [Class2 : correct] : t = 0.000000, y = 0.036213 (err = -0.036213)
99 [Class2 : correct] : t = 0.000000, y = 0.317548 (err = -0.317548)
```

이 예시에서는 3개의 오차가 있지만, 4개의 특징에서 거의 튤립 종류를 식별할 수 있다는 것을 알 수 있다.

[^1]: 최대우도법(Maximum Likelihood Estimation, 最大尤度法): 모수적인 데이터 밀도 추정 방법으로써 파라미터 $\theta=\left(\theta_{1}, \cdots, \theta_{m}\right)$으로 구성된 어떤 확률 밀도함수 $P(x\|\theta)$에서 관측된 표본 데이터 집합을 $x=\left(x_{1}, x_{2}, \cdots, x_{n}\right)$이라고 할 때, 이 표본들에서 파라미터 $\theta=\left(\theta_{1}, \cdots, \theta_{m}\right)$을 추정하는 방법이다.
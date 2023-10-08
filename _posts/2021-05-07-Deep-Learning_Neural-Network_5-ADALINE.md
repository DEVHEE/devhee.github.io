---
title: Neural Network Basic / 5. ADALINE
author: kimdonghee
date: 2021-05-07 16:19:38 +0900
categories: [Deep Learning, Neural Network]
tags: [deep learning, neural network, adaline, recognize, parameter, artificial intelligence]
math: true
image:
    path: /assets/img/posts/2021-05-07-Deep-Learning_Neural-Network_5-ADALINE/preview.jpg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

# **5. Adaline**

최소제곱법의 풀이를 사용하면 퍼셉트론의 결점을 어느 정도 해결한 학습법을 찾을 수 있다. 이것은 1960년에 Widrow와 Hoff가 제안한 ADALINE(아달라인; Adaptive Linear Neuron)이라는 모델로, 임계 논리소자의 선형 부분

$$
y=\sum_{i=1}^{M} a_{i} x_{i}+a_{0}
$$

*$[35]$*

만을 취해서 이용하는 것이다. 이 모델로 학습하면 정답과 네트워크 출력과의 평균 제곱 오차를 최소로 하도록 하는 결합 무게($a_0,a_1,...,a_M$)를 최급강하법으로 구하는 것이다. 따라서, 이 모델의 출력 함수는 McCulloch와 Pitts의 임계 논리소자나 Rosenblatt의 퍼셉트론과 같이 임계 함수가 아닌 $[Fig.\,3]$ (b)([이전 포스팅](https://kimdonghee.dev/posts/Deep-Learning_Neural-Network_4-Perceptron/){:target="_blank"})와 같은 선형 함수라고 간주할 수 있다.

우선, 저번에 한 공 던지기 기록을 예측하는 최소제곱법의 프로그램을 참고로 해서 2종류 튤립 데이터를 식별하는 ADALINE 프로그램을 작성해 보자.

튤립 다이너스티와 튤립 아틀란티스 2종류의 꽃에서 꽃받침의 길이($x1$), 꽃받침의 폭($x2$), 꽃잎의 길이($x3$), 꽃잎의 폭($x4$) 데이터에서 답을 예측하기 위한 ADALINE 모델은

$$
y(x 1, x 2, x 3, x 4)=a_{0}+a_{1} x 1+a_{2} x 2+a_{3} x 3+a_{4} x 4
$$

*$[36]$*

이 된다. 최소제곱법의 경우와 마찬가지로 ADALINE에서도 예측값과 교사의 답과의 평균 제곱 오차를 최소로 하도록 하는 파라미터($a_0,a_1, a_2,a_3, a_4$)를 최급강하법으로 구한다. 평균 제곱 오차의 각 파라미터에서의 미분을 계산해서 파라미터 갱신식을 구체적으로 구하면,

$$
\begin{array}{l}
a_{0}^{(k+1)}=a_{0}^{(k)}+2 \alpha \frac{1}{100} \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) \\
a_{1}^{(k+1)}=a_{1}^{(k)}+2 \alpha \frac{1}{100} \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) x 1_{l} \\
a_{2}^{(k+1)}=a_{2}^{(k)}+2 \alpha \frac{1}{100} \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) x 2_{l} \\
a_{3}^{(k+1)}=a_{3}^{(k)}+2 \alpha \frac{1}{100} \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) x 3_{l} \\
a_{4}^{(k+1)}=a_{4}^{(k)}+2 \alpha \frac{1}{100} \sum_{l=1}^{100}\left(t_{l}-y_{l}\right) x 4_{l}
\end{array}
$$

*$[37]$*

와 같이 된다. 여기 $t_l$ 및 $y_l$은 각각 $l$번째 계측 데이터에 대한 답 및 ADALINE 모델에서의 예측값이다. 또한, $x1_l$, $x2_l$, $x3_l$, $x4_l$은 $l$번째의 꽃을 계측한 특징량의 예측값이다.

학습한 ADALINE 모델을 사용해서 튤립을 식별하려면 학습한 ADALINE 모델에 계측한 특징량을 대입하고 답의 예측값을 구해 그것이 1에 근접하면 튤립 다이너스티라고 판정하고, 0에 근접하면 튤립 아틀란티스라고 판정하면 된다.

구체적인 프로그램은 아래와 같다.

```c
#include <stdio.h>
#include <stdlib.h>

#define frand() rand() / ((double) RAND_MAX)
#define NSAMPLE 100
#define XDIM 4

main() {
    FILE * fp;
    double t[NSAMPLE];
    double x[NSAMPLE][XDIM];
    double a[XDIM + 1];
    int i, j, l;
    double y, err, mse;
    double derivatives[XDIM + 1];
    double alpha = 0.1; /* Learning Rate */

    /* Open Data File */
    if ((fp = fopen("tulip.dat", "r")) == NULL) {
        fprintf(stderr, "File Open Fail\n");
        exit(1);
    }

    /* Read Data */
    for (l = 0; l < NSAMPLE; l++) {

        /* Input input vectors */
        for (j = 0; j < XDIM; j++) {
            fscanf(fp, "%lf", & (x[l][j]));
        }

        /* Set teacher signal */
        if (l < 50) t[l] = 1.0;
        else t[l] = 0.0;
    }

    /* Close Data File */
    fclose(fp);

    /* Print the data */
    for (l = 0; l < NSAMPLE; l++) {
        printf("%3d : %8.2f ", l, t[l]);

        for (j = 0; j < XDIM; j++) {
            printf("%8.2f ", x[l][j]);
        }
        printf("\n");
    }

    /* Initialize the parameters by random number */
    for (j = 0; j < XDIM + 1; j++) {
        a[j] = (frand() - 0.5);
    }

    /* Open output file */
    fp = fopen("mse.out", "w");

    /* Learning the parameters */
    for (i = 1; i < 1000; i++) {

        /* Learning Loop */
        /* Compute derivatives */
        /* Initialize derivatives */
        for (j = 0; j < XDIM + 1; j++) {
            derivatives[j] = 0.0;
        }

        /* update derivatives */
        for (l = 0; l < NSAMPLE; l++) {

            /* prediction */
            y = a[0];

            for (j = 1; j < XDIM + 1; j++) {
                y += a[j] * x[l][j - 1];
            }

            /* error */
            err = t[l] - y;

            /* printf("err[%d] = %f\n", l, err);*/
            /* update derivatives */
            derivatives[0] += err;
            for (j = 1; j < XDIM + 1; j++) {
                derivatives[j] += err * x[l][j - 1];
            }
        }

        for (j = 0; j < XDIM + 1; j++) {
            derivatives[j] = -2.0 * derivatives[j] / (double) NSAMPLE;
        }

        /* update parameters */
        for (j = 0; j < XDIM + 1; j++) {
            a[j] = a[j] - alpha * derivatives[j];
        }

        /* Compute Mean Squared Error */
        mse = 0.0;

        for (l = 0; l < NSAMPLE; l++) {
            /* prediction */
            y = a[0];
            for (j = 1; j < XDIM + 1; j++) {
                y += a[j] * x[l][j - 1];
            }
            /* error */
            err = t[l] - y;
            mse += err * err;
        }
        mse = mse / (double) NSAMPLE;
        printf("%d : Mean Squared Error is %f\n", i, mse);
        fprintf(fp, "%f\n", mse);
    }

    fclose(fp);
    /* Print Estmated Parameters */
    printf("\nEstimated Parameters\n");

    for (j = 0; j < XDIM + 1; j++) {
        printf("a[%d]=%f, ", j, a[j]);
    }

    printf("\n\n");

    /* Prediction and Errors */
    for (l = 0; l < NSAMPLE; l++) {
        /* prediction */
        y = a[0];

        for (j = 1; j < XDIM + 1; j++) {
            y += a[j] * x[l][j - 1];
        }
        /* error */
        err = t[l] - y;
        
        if ((1.0 - y) * (1.0 - y) <= (0.0 - y) * (0.0 - y)) {
            if (l < 50) {
                printf("%3d [Class1 : correct] : t = %f, y = %f (err = %f)\n", l, t[l], y, err);
            } else {
                printf("%3d [Class1 : not correct] : t = %f, y = %f (err = %f)\n", l, t[l], y, err);
            }
        } else {
            if (l >= 50) {
                printf("%3d [Class2 : correct] : t = %f, y = %f (err = %f)\n", l, t[l], y, err);
            } else {
                printf("%3d [Class2 : not correct] : t = %f, y = %f (err = %f)\n", l, t[l], y, err);
            }
        }
    }
}
```

이 프로그램은 먼저 최소제곱법을 최급강하법으로 푸는 프로그램과 거의 같다. 튤립의 데이터 파일 tulip.dat을 읽어 들이고 그 데이터에 대해서 최급강하법으로 파라미터를 구한다. 교사 신호가 실수 값이 아닌 0과 1의 2개의 값으로 주어지는 것만이 최소제곱법과 다른 점이다. 프로그램의 마지막 부분에서는 얻어진 신경망(식별기)의 퍼포먼스를 확인하기 위해 학습에 사용한 붓꽃 데이터를 식별하도록 하고 있다. 뉴럴 네트워크의 출력이 0과 1 중 어느 쪽에 가까운지에 따라 무슨 튤립인지를 결정한다. 프로그램의 실행 결과는 다음과 같다.

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

이 예시에서는 3개의 오차가 있지만 4개의 특징에서 거의 튤립 종류를 식별할 수 있음을 알 수 있다.
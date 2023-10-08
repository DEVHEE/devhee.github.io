---
title: Neural Network Basic /  1. Introduction
author: KIM DONGHEE
date: 2021-05-03 10:05:18 +0900
categories: [Deep Learning, Neural Network]
tags: [deep learning, neural network, machine learning, algorithm, artificial intelligence]
image:
    path: /assets/img/posts/2021-05-03-Deep-Learning_Neural-Network_1-Introduction/preview.jpg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

# **1. Introduction**

인간은 뇌의 **`신경회로망(뉴럴 네트워크)`**을 사용해서 매우 뛰어난 정보처리를 할 수 있다. 인간이나 동물의 뇌에는 매우 많은 **`뉴런`**이 있고, 그것들은 매우 복잡하게 얽혀있어서 정보를 주고받는다. 이러한 복잡한 신경회로망에서 뉴런 간의 **`정보 교환`**을 통해 우수한 정보처리가 실현된다. 한편, 현재 컴퓨터는 1개의 CPU에서 프로그램으로 주어진 명령을 순차적으로 빠르게 처리하는 방식을 취하고 있어 뇌의 정보처리 방식과는 상당히 다르다. 또한, 현재의 컴퓨터는 미리 주어진 명령을 충실히 실행하는 것은 잘하지만 **`새로운 환경에 적응`**하거나 학습에 따라 **`새로운 능력을 익히거나`** 하는 것은 별로 잘하지 못한다. 음성을 알아듣는 **`패턴 인식 능력`**이나 직관적인 **`판단능력`**, 새로운 환경으로의 **`적응능력`**이나 **`학습능력`**에서는 우리의 뇌는 현재 컴퓨터에 비해서 훨씬 뛰어나다. 우리의 뇌에서는 뉴런 간의 결합 강도를 변화시킴으로써 학습이 이루어지고 있다고 한다. 인공 뉴럴 네트워크는 뇌를 본떠서 다수의 뉴런을 결합한 **`네트워크상`**에서 **`정보처리`**를 시키려는 것이다.

**[Neural Network Basic]**에서는 뉴럴 네트워크의 기본이 되는 학습 사고방식 또는 학습 알고리즘에 대해서 다룰 것이다.
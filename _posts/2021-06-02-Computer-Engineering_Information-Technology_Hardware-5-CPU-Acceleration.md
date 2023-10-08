---
title: Information Technology / [Hardware] 5. CPU Acceleration
author: DEVHEE
date: 2021-06-02 22:03:12 +0900
categories: [Computer Engineering, Information Technology]
tags: [computer engineering, information technology, hardware, cpu, acceleration, sequential control, pipeline processing, super pipeline, superscalar, multi-core processor, gpu]
math: true
image:
    src: /assets/img/posts/2021-06-02-Computer-Engineering_Information-Technology_Hardware-5-CPU-Acceleration/preview.jpg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

# **5. CPU Acceleration**

## **Sequential Control and Pipeline Processing**

### **Sequential Control**

명령의 실행은 A) 명령 패치, B) 명령 해독, C) 실효 어드레스 계산, D) 오퍼랜드 읽어내기, F) 명령 실행, G) 연산 결과 저장이라는 사이클로 진행된다. 순차제어 방식은 명령의 실행 사이클 단위로, 한 명령씩 순차로 반복해서 실행하는 방식을 말한다.

![Fig. 1](/assets/img/posts/2021-06-02-Computer-Engineering_Information-Technology_Hardware-5-CPU-Acceleration/fig_1.png)

*$[Fig.\,1]$ Sequential Control*

### **Pipeline Processing**

파이프라인 처리는 명령 실행 사이클의 각 단계(스테이지)를 병행해서 실행하는 것에 따라 처리 효율을 향상시키는 방식이다.

![Fig. 2](/assets/img/posts/2021-06-02-Computer-Engineering_Information-Technology_Hardware-5-CPU-Acceleration/fig_2.png)

*$[Fig.\,2]$ Pipeline Processing*

파이프라인 처리에서는 분기 명령이 나타나면 그전까지 먼저 읽었던 명령을 파기하고 새롭게 분기처의 명령을 실행해야 한다. 처리의 순서가 꼬이는 것을 파이프라인 해저드라고 한다. 분기 명령으로 처리하기 위해서는 실행되는 높은 확률을 예측하는 분기 예측이나, 예측한 분기처의 명령을 실행해서 결과를 저장하고 분기처가 올바르면 그 결과를 이용하는 투기적 실행 등의 기술이 사용된다.

### **Super Pipeline**

슈퍼 파이프라인은 각 스테이지를 더 세세히 분할하는 것으로 슈퍼 파이프라인 동작의 효율을 향상시키는 방식이다.

![Fig. 3](/assets/img/posts/2021-06-02-Computer-Engineering_Information-Technology_Hardware-5-CPU-Acceleration/fig_3.png)

*$[Fig.\,3]$ Super Pipeline*

### **Superscalar**

슈퍼 스칼라는 복수의 파이프라인을 설정하는 것으로 복수의 명령을 동시에 실행하는 방식이다.

![Fig. 4](/assets/img/posts/2021-06-02-Computer-Engineering_Information-Technology_Hardware-5-CPU-Acceleration/fig_4.png)

*$[Fig.\,4]$ Superscalar*

<blockquote style="margin-top: 7%;"><b>CISC and RISC</b></blockquote>
<div class="blockquote-div">
CPU의 아키텍처로서 CISC과 RISC가 있다. CISC는 Complex Instruction Set Computer의 약자로 복잡한 명령체계로 되어있으며 컴퓨터용 CPU로서 사용된다. RISC는 Reduced Instruction Set Computer의 약자로 명령체계는 단순하고 명령의 길이도 고정되어있어 파이프라인으로 효율 좋게 처리할 수 있다. 구조시스템에는 RISC가 사용된다.
</div>

## **Multi-Core Processor**

멀티코어 프로세서는 하나의 CPU 내에 복수의 코어(연산 회로의 중핵 부분)를 둔다. 이전의 싱글 코어 프로세서와 비교해서 소비전력을 낮추면서 처리 속도의 고속화를 가능하게 한다. 코어가 2개면 듀얼코어, 4개면 쿼드코어, 6개며 헥사코어, 8개면 옥타코어라고 불린다. 각각의 코어가 동시에 다른 처리를 실행(병행처리)하는 것으로 처리 능률을 향상시킨다.

## **GPU**

3D 이미지 처리를 고속으로 실행하는 연산장치를 GPU(Graphics Processing Unit)라고 한다. 수천 개의 코어로 데이터를 병렬 처리한다. 요즘 PC에는 GPU가 내장되어있는 CPU가 사용된다. GPU는 기계학습(머신러닝)의 발전에 공헌하고 있다.
---
title: Information Technology / [Hardware] 4. Adddressing
author: DEVHEE
date: 2021-05-12 17:41:12 +0900
categories: [Computer Engineering, Information Technology]
tags: [computer engineering, information technology, hardware, addressing, operation]
math: true
image:
    path: /assets/img/posts/2021-05-12-Computer-Engineering_Information-Technology_Hardware-4-Addressing/preview.jpg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

# **4. Addressing**

## **Operation**

프로그램은 컴퓨터로 실행시키는 명령이 모인 것이다. 프로그램 언어로 쓰인 프로그램은 최종적으로 컴퓨터가 이해할 수 있는 1과 0만으로 구성된 기계어로 변환하고, 해독, 실행된다.

기계어의 명령어는 명령부와 어드레스부(오퍼랜드부)로 구성되어있지만, 명령의 종류에 따라서는 어드레스부가 없거나 복수인 것도 있다.

![Fig. 1](/assets/img/posts/2021-05-12-Computer-Engineering_Information-Technology_Hardware-4-Addressing/fig_1.png)

*$[Fig.\,1]$ Relationship between Operation section and Address section*

## **Operation Instruction Cycle**

CPU는 주기억장치(메인 메모리)에 격납되어있는 명령을 읽어내서 해독하고, 다른 장치에 지시를 내리는 제어장치와, 데이터에 대한 사칙연산이나 논리 연산 등을 행하는 연산장치로 이루어진다.

명령을 읽어내고 실행 종료까지의 흐름은, 다음 그림을 참고해라.

![Fig. 2](/assets/img/posts/2021-05-12-Computer-Engineering_Information-Technology_Hardware-4-Addressing/fig_2.png)

*$[Fig.\,2]$ Flow of Operation and end of Execution*

명령 어드레스 레지스터(프로그램 카운터)에는 지금까지 실행된 명령이 저장되어있는 주기억장치의 어드레스가 들어가 있다.

1. 명령 패치(명령 추출): 명령 어드레스 레지스터로 표시된 어드레스의 명령이 명령 레지스터로 추출된다. 추출된 후 명령 어드레스 레지스터는 다음 명령의 어드레스를 가리키게 된다.

2. 명령의 해독: 명령 부분은 해독기(디코더)에 의해 해독되고, 연산 명령이면 연산장치로 지시가 내려진다.

3. 실효 어드레스 계산: 명령 어드레스 부분은 어드레스 레지스터로 보내진다. 어드레스 레지스터는 실행에 필요한 데이터가 들어가 있는 어드레스나 실행 결과를 저장하는 어드레스를 계산해서 주기억장치로 지시한다.

4. 오퍼랜드 읽어내기: 연산의 대상이 되는 어드레스의 데이터가 연산장치로 보내진다.

5. 명령 실행: 연산장치로 계산이 실행된다.

6. 연산 결과 저장: 계산 결과가 다시 주기억장치로 저장된다.

위 1~6의 단계를 순차적으로 반복하면서 프로그램이 실행된다.

## **Addressing Mode**

명령을 실행할 때에는 다음 어드레스 지정 방식을 사용해서 실효 어드레스(유효 어드레스)를 계산한다. 실효 어드레스란 처리 대상이 되는 데이터가 실제로 저장되어있는 주기억장치상의 어드레스이다.

또한, 어드레스 지정은 어드레스 수식이라고도 한다. 명령의 어드레스부에 대해서 어떠한 장식을 달아서 구한다는 의미라는 것이다. CPU의 종류에 따라 이용 가능한 어드레스 지정방식은 다르다.

### **Immediate Mode**

즉치 어드레스 지정은 명령의 어드레스부에 데이터를 저장하는 방식이다.

### **Direct Mode**

직접 어드레스 지정은 명령의 어드레스부의 값을 실효 어드레스로 하는 방식이다.

### **Indirect Mode**

간접 어드레스 지정은 명령 어드레스부에 실효 어드레스를 저장하고 있는 어드레스를 저장하는 방식이다. 간접 어드레스 지정을 이중 삼중으로 하는 경우가 있다.

### **Relative Mode**

상대 어드레스 지정은 명령의 어드레스부의 값과 명령 어드레스 레지스터(프로그램 카운터)의 값을 더해서 실효 어드레스로 하는 방식이다.

### **Index-Register Mode**

인덱스 어드레스 지정은 명령의 어드레스부의 값과 인덱스 레지스터의 값을 더해서 실효 어드레스로 하는 방식이다.

### **Base-Register Mode**

베이스 어드레스 지정은 명령의 어드레스부의 값과 베이스 레지스터의 값을 더해서 실효 어드레스로 하는 방식이다.

<blockquote style="margin-top: 7%;"><b>Index Register / Base Register</b></blockquote>
<div class="blockquote-div">
인덱스 레지스터는 명령의 어드레스부를 수식하기 위한 증분 값을 저장한다. 어드레스부의 값을 기준으로 순차적으로 처리하는 배열 처리 등에 이용된다.<br><br>
베이스 레지스터는 명령의 어드레스부의 값에 더해지는 기준이 되는 어드레스 값을 저장한다. 베이스 레지스터의 값을 바꾸는 것 만으로 프로그램을 주기억장치상의 어디에 배치해도 실행할 수 있게 된다.
</div>
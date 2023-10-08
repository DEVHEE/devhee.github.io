---
title: Information Technology / [Hardware] 3. CPU
author: DEVHEE
date: 2021-05-12 17:24:39 +0900
categories: [Computer Engineering, Information Technology]
tags: [computer engineering, information technology, hardware, cpu, register, clock, frequence]
math: true
image:
    path: /assets/img/posts/2021-05-12-Computer-Engineering_Information-Technology_Hardware-3-CPU/preview.jpg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

# **3. CPU**

## **CPU**

CPU는 제어장치와 연산장치 2가지의 장치로 구성되어있다.

제어장치는 기억장치로부터 프로그램의 명령을 받아와 해석하고 각각의 장치에 지시를 내리는 컴퓨터의 중추적인 역할을 담당하고 있다.

연산장치는 산술논리연산장치(ALU: Arithmetic and Logic Unit)이라고도 하며, 사칙연산(덧셈, 뺄셈, 곱셈, 나눗셈)이나 논리 연산 등을 한다.

## **Register**

CPU 안에는 레지스터라는 고속 기억장치가 들어있다. 레지스터에는 몇 개의 종류가 있다.

<table class="GeneratedTable" style="margin-top: 30px; margin-bottom: 20px;">
  <thead>
    <tr>
      <th style="text-align: center;">명칭</th>
      <th style="text-align: center;">역할</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center; width: 30%">Instruction Register</td>
      <td>주기억으로부터 받아온 명령을 저장한다.</td>
    </tr>
    <tr>
      <td style="text-align: center;">Instruction Address Register</td>
      <td>실행해야 하는 명령의 어드레스를 보존하고 유지한다. 프로그램 카운터라고도 한다.</td>
    </tr>
    <tr>
      <td style="text-align: center;">Index Register</td>
      <td>어드레스 지정에 사용하는 레지스터이며 명령의 어드레스부를 수식하기 위한 증분치를 보존하고 유지한다. 지표 레지스터라고도 한다.</td>
    </tr>
    <tr>
      <td style="text-align: center;">Base Register</td>
      <td>어드레스 지정에 사용하는 레지스터이며 명령의 어드레스부의 값에 더해지는 기준이 되는 어드레스 값을 보존하고 유지한다. 기저 레스터라고도 한다.</td>
    </tr>
    <tr>
      <td style="text-align: center;">Accumulator</td>
      <td>피 연산수와 연산 결과를 일시적으로 보존하고 유지한다. 누산기라고도 한다.</td>
    </tr>
    <tr>
      <td style="text-align: center;">General Purpose Register</td>
      <td>특정 기능에 한정하지 않고 다목적으로 사용된다.</td>
    </tr>
  </tbody>
</table>

## **Clock Frequence**

CPU나 메모리 등 각 장치 동작의 타이밍을 맞추기 위해서 컴퓨터의 내부에서 일정한 간격으로 전압이 규칙적으로 "높고" "낮음"을 반복하는 클럭 신호가 생성된다. 이 "높고" "낮음"의 전압의 사이클이 1초간에 몇 회 반복되는지를 클럭 주파수로 나타낸다. 단위는 GHz(기가헤르츠: 1초간 $10^9$번)등이 사용된다.

![Fig. 1](/assets/img/posts/2021-05-12-Computer-Engineering_Information-Technology_Hardware-3-CPU/fig_1.png)

*$[Fig.\,1]$ 1 Clock*

CPU와 주기억장치를 접속하는 시스템 버스의 클럭은 외부 클럭이라고 한다. CPU 내부에서는 외부 클럭을 몇 배로 해서 내부 클럭을 사용한다. PC의 카탈로그에 있는 클럭 주파수는 내부 클럭의 주파수이다.

일반적으로 클럭 주파수가 높아질수록 컴퓨터의 명령 실행 속도는 빨라지며, 처리속도도 빨리 진다. 그러나, 컴퓨터 전체의 성능으로는 메모리나 HDD의 성능에 따라도 달라진다.
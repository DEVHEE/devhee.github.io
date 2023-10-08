---
title: Information Technology / [Hardware] 6. Memory Element
author: kimdonghee
date: 2021-06-02 22:36:08 +0900
categories: [Computer Engineering, Information Technology]
tags: [computer engineering, information technology, hardware, memory, disk cache, write back, write through, semiconductor]
math: true
image:
    path: /assets/img/posts/2021-06-02-Computer-Engineering_Information-Technology_Hardware-6-Memory-Element/preview.jpg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

# **6. Memory Element**

## **Semiconductor Memory**

반도체 메모리는 크게 읽고 쓰기가 가능한 RAM(Random Access Memory)와 읽기 전용 ROM(Read Only Memory)으로 나눌 수 있다.

RAM에는 전원을 끊으면 기억하고 있던 내용이 사라져 버리는 성질(휘발성), ROM에는 전원을 끊어도 기억하고 있던 내용이 사라지지 않는 성질(비휘발성)이 있다.

## **Types and Features of RAM**

RAM에는 DRAM(Dynamic RAM)과 SRAM(Static RAM)이 있다.

### **DRAM**

DRAM은 콘덴서에 전하를 갖춘 상태인지 아닌지에 따라 1비트를 표현한다. 구조가 간단해서 고집적화에 적합하기 때문에 SRAM에 비해서 용량이 크고 값이 싸다. 단, 콘덴서는 방치해두면 자연방전이 되는 특성이 있어서 일정 시간마다 기억 내용을 유지하기 위해 리프레시 동작이 필요하다. DRAM은 주기억장치에 쓰인다.

### **SRAM**

SRAM은 플립플롭 회로로 구성되어 속도가 빠르지만 구조가 복잡해서 집적도를 높이기 때문에 DRAM에 비교해서 용량이 작고 값이 비싸다. 전원이 공급되어있는 한 기억 내용을 계속 저장하기 때분에 리프레시 동작이 필요하지 않다. SRAM은 캐시 메모리 등에 사용된다.

<table class="GeneratedTable" style="margin-top: 30px; margin-bottom: 20px;">
  <thead>
    <tr>
      <th class="center"></th>
      <th class="center">사용회로</th>
      <th class="center">리프레시</th>
      <th class="center">속도</th>
      <th class="center">집적도</th>
      <th class="center">가격</th>
      <th class="center">용도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center" style="width: 30%; font-weight: bold;">DRAM</td>
      <td class="center">콘덴서</td>
      <td class="center">필요</td>
      <td class="center">느림</td>
      <td class="center">높다</td>
      <td class="center">싸다</td>
      <td class="center">주기억장치</td>
    </tr>
    <tr>
      <td style="text-align: center; font-weight: bold;">SRAM</td>
      <td class="center">플립플롭 회로</td>
      <td class="center">불요</td>
      <td class="center">빠름</td>
      <td class="center">낮다</td>
      <td class="center">비싸다</td>
      <td class="center">캐시 메모리</td>
    </tr>
  </tbody>
</table>

<blockquote style="margin-top: 7%;"><b>플립플롭 회로</b></blockquote>
<div class="blockquote-div">
플립플롭 회로는 두 개의 안정상태를 갖는 회로로, 1비트의 정보를 기록할 수 있다. SRAM의 기억 셀에 사용된다. 현재와 과거 두 개의 입력으로 출력이 결정되는 순서 회로의 하나이다.
</div>

<table class="GeneratedTable" style="margin-top: 30px; margin-bottom: 20px;">
  <thead>
    <tr>
      <th style="text-align: center; width: 25%;">S</th>
      <th style="text-align: center; width: 25%;">R</th>
      <th style="text-align: center; width: 25%;">Q</th>
      <th style="text-align: center; width: 25%;">Q'</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center">0</td>
      <td class="center">0</td>
      <td class="center" colspan="2">이전 내용을 저장</td>
    </tr>
    <tr>
      <td class="center">0</td>
      <td class="center">1</td>
      <td class="center">0</td>
      <td class="center">1</td>
    </tr>
    <tr>
      <td class="center">1</td>
      <td class="center">0</td>
      <td class="center">1</td>
      <td class="center">0</td>
    </tr>
    <tr>
      <td class="center">1</td>
      <td class="center">1</td>
      <td class="center" colspan="2">불안정하기 때문에 금지</td>
    </tr>
  </tbody>
</table>

*$[Table\,1]$ Truth Table*

![Fig. 1](/assets/img/posts/2021-06-02-Computer-Engineering_Information-Technology_Hardware-6-Memory-Element/fig_1.png)

*$[Fig.\,1]$ [Schematic] / S: Set, R: Reset*

## **Types and Features of ROM**

<table class="GeneratedTable" style="margin-top: 30px; margin-bottom: 20px;">
  <thead>
    <tr>
      <th class="center"></th>
      <th class="center">쓰기</th>
      <th class="center">제거</th>
      <th class="center">특징</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center; width: 30%; font-weight: bold;">마스크 ROM</td>
      <td class="center">X</td>
      <td class="center">X</td>
      <td>제조시에 쓰여진 후에는 사용자는 쓸 수 없다</td>
    </tr>
    <tr>
      <td style="text-align: center; font-weight: bold;">EPROM<br>(Erasable ROM)</td>
      <td class="center">O</td>
      <td class="center">O</td>
      <td>자외선조사로 전체 삭제가 가능하다</td>
    </tr>
    <tr>
      <td style="text-align: center; font-weight: bold;">EEPROM<br>(Electrically ROM)</td>
      <td class="center">O</td>
      <td class="center">O</td>
      <td>전압을 걸어서 부분 삭제가 가능하다<br>삭제/쓰기는 1바이트 단위로 가능하다</td>
    </tr>
    <tr>
      <td style="text-align: center; font-weight: bold;">플래시 메모리</td>
      <td class="center">O</td>
      <td class="center">O</td>
      <td>전압을 걸어서 전체 삭제 또는 부분 삭제가 가능하다<br>다시쓰기는 블럭 단위로 삭제 후에 쓰여진다</td>
    </tr>
  </tbody>
</table>

## **Cache Memory**

주기억장치의 액세스 속도는 CPU의 처리속도에 비해서 느리기 때문에 CPU에 대기시간이 발생해버린다. 여기서 용량이 작지만 속도가 빠른 캐시 메모리를 CPU와 주기억장치 사이에 배치한다.

주기억장치에서 읽어낸 데이터를 캐시 메모리에 저장하고, CPU가 나중에 같은 데이터를 읽어낼 때는 속도가 빠른 캐시 메모리에서 읽어내는 것으로 데이터의 전송을 빠르게 할 수 있다.

### **Primary Cache and Secondary Cache**

주기억장치의 액세스 시간과 CPU의 처리시간의 차이가 큰 경우 1차 캐시, 2차 캐시, 상위 레벨 캐시로 구성하면 보다 좋은 효과를 낼 수 있다. CPU가 액세스 하는 순서에 따라 명칭이 붙어져서 CPU는 1차 캐시, 2차 캐시, 주기억장치 순으로 액세스 한다. L1 캐시, L2 캐시라고도 불린다.

### **Write-Through and Write-Behind Caching**

캐시 메모리 데이터의 입력 명령이 실행될 때 캐시 메모리와 주 기억장치의 양쪽을 다시 쓰는 라이트 스루 방식과, 캐시 메모리만 다시 써서 주기억장치는 블록 교체 시에 실행하는 라이트백 방식이 있다.

라이트 스루 방법은 캐시 메모리와 주기억장치 내용이 항상 같기 때문에 데이터의 일관성이 유지되어 제어나 회로 구성도 간단하다. 단, 쓰기 속도를 올리는 효과는 없다.

라이트백 방식은 주기억으로의 쓰기 빈도가 줄어 빠른 속도로 쓸 수 있지만, 캐시 메모리아 주기억의 내용은 달라 특수한 상황에서는 캐시 된 데이터를 잃어버릴 수도 있다.

### **Effective Access Time**

액세스 하는 데이터는 캐시 메모리가 주기억장치의 어딘가에 존재할 것이다. 액세스 하는 데이터가 캐시 메모리에 존재할 확률을 히트율이라고 한다. 히트율과 캐시 메모리의 액세스 시간, 주기억장치의 액세스에 시간이 걸리면 실효 액세스 시간을 구할 수 있다.

예를 들어, 다음의 실효 액세스 시간을 구해보자.
- 히트율: 80%
- 캐시 메모리의 액세스 시간: 10ns
- 주기억장치의 액세스 시간: 60ns

라고 하면, 캐시 메모리에 데이터가 존재할 확률은 80%, 주기억장치에 존재할 확률은 100 - 80 = 20%이기 때문에, 다음식으로 구할 수 있다.

$$10 * 0.8 + 60 * 0.2 = 20ns$$

이 경우, 캐시 메모리를 사용하면 60 - 20 = 40ns 액세스 시간을 단축한 것이 된다.

또한, 주기억장치에 존재할 확률(=캐시 메모리에 존재하지 않을 확률)을 NFP(Not Found Probability)라고도 불린다.

## **Disk Cache**

디스크 캐시는 주기억장치의 액세스 시간과 자기 디스크 액세스 시간의 차이를 보완한다는 의미로, 캐시 메모리와 비슷한 양상을 보인다. 디스크 캐시는 반도체 메모리를 사용하는 경우와 주기억장치의 일부를 사용하는 경우가 있다. 이렇게 속도차가 있는 장치 간의 차이를 보완하는 것을 버퍼라고 부르는 경우도 있다.

## **Memory Access Time**

기억장치의 액세스 속도를 빠른 순으로 늘어놓으면 레지스터, 캐시 메모리, 주기억장치, 디스크 캐시, 자기 디스크 순이다.

## **Interleaved Memory**

메모리 인터리빙은 주기억장치를 몇 개의 액세스 단위(뱅크)로 분할하고, 각 액세스 단위를 가능한 병렬 작동시키는 것에 따라 실효적인 액세스 시간을 단축하고 고속화할 수 있는 방법이다.

단, 랜덤으로 액세스 할 경우는 메모리 인터리빙의 효과가 적다.
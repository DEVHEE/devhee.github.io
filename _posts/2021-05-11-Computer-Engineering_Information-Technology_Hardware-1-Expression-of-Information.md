---
title: Information Technology / [Hardware] 1. Expression of Information
author: DEVHEE
date: 2021-05-11 09:16:07 +0900
categories: [Computer Engineering, Information Technology]
tags: [computer engineering, information technology, hardware, information, ascii, euc, unicode]
math: true
image:
    path: /assets/img/posts/2021-05-11-Computer-Engineering_Information-Technology_Hardware-1-Expression-of-Information/preview.jpg
---

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">수업 내용 보호를 위해 일부 생략된 내용이 있을 수 있습니다.</b><br>
</div>

# **1. Expression of Information**

## **Units of Information**

컴퓨터의 내부에서는 모든 정보는 전기신호의 `ON`과 `OFF`와 같은 2개의 값으로 다뤄지기 때문에 이것을 일반적으로 2진수의 `1`과 `0`에 대응시켜 표현하고 있다. 컴퓨터에서 다루는 최소의 정보량의 단위를 비트(bit)라고 하며, 2진수 1자리에 상당한다. 또한, 비트 8개를 모은 것을 바이트(Byte)라고 하며, 2진수 8자리에 상당한다. 바이트는 정보량의 기본단위가 된다.

예를 들어, `10001111`는 1바이트(=8비트)의 정보량이며, 이와 같은 `1`과 `0`의 나열을 비트 패턴이라고 부를 때도 있다.

## **Relationship between the number of Bits and the amount of Information that can be Expressed**

1비트로 표현할 수 있는 정보량은 `0`과 `1`의 2(=$2^1$)가지, 2비트로는 `00` `01` `10` `11`의 4(=$2^2$)가지, 3비트로는 `000` `001` `010` `011` `100` `101` `110` `111`의 8(=$2^3$)가지이다.

일반적으로 $n$비트로는 $2^n$가지의 정보를 표현하는 것이 가능하다.

## **Prefixes used to Express the amount of Information**

컴퓨터가 다루는 정보량은 방대하다. B(바이트) 전에 10의 정수 제곱 배로 표현하는 접두어인 k(킬로), M(메가), G(기가), T(테라)가 사용된다. "이번 달의 휴대폰 데이터 사용량은 XXG바이트"등으로 사용된다.

<table class="GeneratedTable" style="margin-top: 30px; margin-bottom: 20px;">
  <thead>
    <tr>
      <th style="text-align: center;">접두어</th>
      <th style="text-align: center;">의미</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;">k(킬로)</td>
      <td style="text-align: center;">$10^3$배($\fallingdotseq 2^{10}$)</td>
    </tr>
    <tr>
      <td style="text-align: center;">M(메가)</td>
      <td style="text-align: center;">$10^6$배($\fallingdotseq 2^{20}$)</td>
    </tr>
    <tr>
      <td style="text-align: center;">G(기가)</td>
      <td style="text-align: center;">$10^9$배($\fallingdotseq 2^{30}$)</td>
    </tr>
    <tr>
      <td style="text-align: center;">T(테라)</td>
      <td style="text-align: center;">$10^{12}$배($\fallingdotseq 2^{40}$)</td>
    </tr>
  </tbody>
</table>

*1k = 1,024 ($2^{10}$)으로 나타낼 때도 있다.

## **Prefixes used to Express Time**

컴퓨터의 처리속도가 굉장히 빨라졌다. 여기서 S(초) 전에 10의 정수 제곱 배를 나타내는 접두어 m(밀리), µ(마이크로), n(나노), p(피코)가 사용된다.

<table class="GeneratedTable" style="margin-top: 30px; margin-bottom: 20px;">
  <thead>
    <tr>
      <th style="text-align: center;">접두어</th>
      <th style="text-align: center;">의미</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;">m(밀리)</td>
      <td style="text-align: center;">$10^{-3}$배</td>
    </tr>
    <tr>
      <td style="text-align: center;">µ(마이크로)</td>
      <td style="text-align: center;">$10^{-6}$배</td>
    </tr>
    <tr>
      <td style="text-align: center;">n(나노)</td>
      <td style="text-align: center;">$10^{-9}$배</td>
    </tr>
    <tr>
      <td style="text-align: center;">p(피코)</td>
      <td style="text-align: center;">$10^{-12}$배</td>
    </tr>
  </tbody>
</table>

## **Calculate Exponential**

정보량이나 시간을 계산할 때에 도움되는 것이 지수 공식이다. 주요한 공식을 외워두는 편이 좋다. 아래의 $m$, $n$이 양의 정수일 때

$a^m \times a^n = a^{m+n}$

$a^m \div a^n = a^{m-n}$ ($a\neq0$, $m> n$일 때)

$(a^m)^n = a^{mn}$

$a^0 = 1$ ($a\neq0$일 때)

$a^{-n} = {1\over{a^n}}$ ($a\neq0$, $n>0$일 때)

예를 들어, $2^3 \times 2^4 = 2^{3+4} = 2^7$이 된다.

$a^{1/2}$는 어떤 수가 될까 생각해보자. 2제곱해 보면 $(a^{1/2})^2 = a^{1/2\times2} = a$ 즉 $a^{1/2}$란 2제곱하면 $a$가 되는 $\sqrt{a}$인 것이다.

## **Character Code**

컴퓨터 내부는 0과 1의 2진수로 표현되어있다. 그럼에도 불구하고 컴퓨터가 문자를 다룰 수 있는 것인 문자 하나에 0과 1의 2진수로 표현시킨 식별번호를 할당하기 때문이다. 식별번호의 할당 방식을 문자코드라고 한다.

예를 들어 문자 `가`는 EUC-KR으로는 `10110000 10100001`, Unicode (UTF-8)로는 `11101010 10110000 10000000`이 된다.

메일 등에서 "문자 깨짐"이라는 현상이 일어날 때가 있는데 이것은 작성자가 사용한 문자코드와 다른 문자코드를 적용한 것이 원인이다.
대표적인 문자코드는 다음과 같다.

<table class="GeneratedTable" style="margin-top: 30px; margin-bottom: 20px;">
  <thead>
    <tr>
      <th style="text-align: center;">명칭</th>
      <th style="text-align: center;">개요</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center; width: 35%">ASCII 코드</td>
      <td>영숫자와 특수문자</td>
    </tr>
    <tr>
      <td style="text-align: center;">EUC</td>
      <td>UNIX나 Linux등에서 이용되는 문자코드.<br>한글로는 EUC-KR, 일본어로는 EUC-JP 등이 있다.</td>
    </tr>
    <tr>
      <td style="text-align: center;">Unicode</td>
      <td>전세계 모둔 문자를 하나의 체계로 표현하는 코드. UTF-8은 Unicode의 부호화방식(문자 쓰기법)의 하나이다.</td>
    </tr>
  </tbody>
</table>
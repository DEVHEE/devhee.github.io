---
title: Robot / AI Robot Hand with Raspberry Pi - 3. 하드웨어 연구
author: kimdonghee
date: 2021-09-11 03:41:07 +0900
categories: [Projects, Robot]
tags: [project, robot, ai, opencv, computer vision, raspberry pi, python]
math: true
image:
    path: /assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/preview.jpeg
---

# **회로설계**

## **회로도**

전체적인 하드웨어 및 회로의 구상은 다음과 같다.

![Fig. 1](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_1.png)

*$[Fig.\,1]$ 구상 회로도*

각 **관절 기능**을 하는 **서보모터 14개**와 이 **모터들을 한번에 제어할 수 있는 PWM/Servo I2C Interface**, **중추 역할을 하는 Raspberry Pi**로 구성된다. 브레드보드는 나중에 확장성을 늘리기 위해 같이 구성하였다.

## **회로 개요**

![Fig. 2](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_2.png)

*$[Fig.\,2]$ 서보모터 연결을 위한 인터페이스 구축*

### **PWM/Servo I2C Interface 구성**

먼저, PWM/Servo I2C Interface부에 대해서 살펴보자. 짧게 PWM/서보 모듈이라고 부르겠다.

![fig_3](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_3.png)

*$[Fig.\,3]$ PWM/Servo I2C Interface부*

사용할 PWM/서보 모듈은 **Adafruit의 PCA8685 모델**이다. 16채널의 프리런 PWM 출력을 제어할 수 있다. Pinouts을 보면, **Power Pins으로는 `GND`, `VCC`, `V+`**를 가지고 있으며, **Control Pins으로는 `SCL`, `SDA`, `OE`**를 가지고 있다. **Output Ports로는 16개의 포트를 가지고 있으며, 각 포트는 `V+`, `GND`, `PWM`으로 구성**된다.

![fig_4](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_4.png)

*$[Fig.\,4]$ Adafruit PCA8685 회로도*

여기서 가장 먼저 주목해야 할 부분은 옆쪽 단자 및 파워이다.

![fig_5](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_5.png)

*$[Fig.\,5]$ Adafruit PCA8685 단자부*

빨간색 점선 부분이 **Raspberry Pi와 직접적으로 연결되는 단자** 부분인데, 1번부터 5번까지 각각 **`5.0V(V+)`, `VCC`, `SDA`, `SCL`, `OE`, `GND`**로 구성되어있다. **`5.0V(V+)`는 모터를 돌리기 위한 전압을 공급하며, 파란색 점선의 `5-6VDC` 파워를 통해 `5.0V(V+)` 대신 전압을 공급**할 수 있다. **`VCC`는  `2.3 - 5.5V`의 전압을 통해 기판에 `PWM`을 위한 전원을 공급**한다. **`SDA`와 `SCL`은 I2C 통신**을 위해 쓰이고, **`OE`는 출력을 가능케**하며, **`GND`는 접지**를 뜻한다.

![fig_6](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_6.png)

*$[Fig.\,6]$ Adafruit PCA8685 Overview*

여기서 우리가 사용할 부분은 **`VCC`, `SCL`, `SDA`, `GND`**이다. 이 네 단자를 통해 Raspberry Pi로부터 PWM/서보 모듈로 데이터를 전송할 수 있게 한다.

### **Raspberry Pi 구성**

**Raspberry Pi 4B의 GPIO는 40핀의 헤더**를 공유한다.

![fig_7](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_7.png)

*$[Fig.\,7]$ Raspberry Pi 4B GPIO 40-pin Header*

이 GPIO와 PWM/서보 모듈을 연결하여 제어가 가능하다.

![fig_8](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_8.png)

*$[Fig.\,8]$ Raspberry Pi 4B GPIO 결선*

**검은색 와이어는 핀 `#9`의 `Ground`, 노란색 와이어는 핀 `#5`의 `GPIO 3 (SCL)`, 초록색 와이어는 핀 `#3`의 `GPIO 2 (SDA)`, 빨간색 와이어는 핀 `#1`의 `3V3 power`**이다. 각 단자를 PWM/서보 모듈의 `GND`, `SCL`,` SDA`, `GND`에 연결해 준다.

여기서 한가지 들 수 있는 의문점은, **왜 `5V power`가 아닌 `3V3 power`에 연결하였냐**는 것이다. 실은, `5V`에 연결해도 상관은 없다. 그 이유는 보통 GPIO에 **`5V`의 전압이 지속적으로 가해지면 회로가 탈 우려**가 있기 때문이라고 설명한다. Raspberry Pi로 들어오는 `5V`의 전압을 `3.3V`로 강압하여 내보내준다.

### **PWM/Servo I2C Interface 신호 데이터 제어**

지금까지의 내용을 정리해보면, **PWM/서보 모듈의 모터 파워는 외부 `5V`를 통해 공급**되고, **Raspberry Pi로의 `5V` 입력이 `3.3V`로 조정**되어 **PWM/서보  모듈의 신호 데이터 입력 및 전송**에 사용되며, **`SCL`과 `SDA` 라인을 이용해 Raspberry Pi ー PWM/서보 모듈 ー 서보모터 간의 I2C 통신**을 하게 된다.

PWM/서보 모듈의 PWM 출력 포트에 서보모터를 연결하여 서보모터를 제어할 수 있다.

![fig_9](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_9.png)

*$[Fig.\,9]$ PWM 출력 포트 회로*

**PWM 출력 포트는 `PWM`, `V+`, `GND`로 구성**되어 있다. **`V+`는 위에서 언급한 PWM/서보 모듈의 외부 `5V` 입력과 공유**하고, **PWM의 신호는 Raspberry Pi 및 PWM/서보 모듈의 `SCL`, `SDA` 라인을 통해 전송**된다.

여기서 한가지 중요한 점이 PWM 출력 포트에 연결되는 서보모터의 Datasheet 정보이다. PWM/서보 모듈 PCA8685는 공식 문서를 보면<i>The PCA9685 operates with a supply voltage range of `2.3 V` to `5.5 V` and the inputs and outputs are 5.5 V tolerant.</i>로, `2.3 - 5.5V`의 공급을 통해 동작하는데 `VCC`의 입력이 `3.3V`이므로 이를 만족한다. 여기에 연결하는 서보모터도 이와 같이 입력 조건이 존재하는데 범용 서보모터의 Datasheet를 보면 다음과 같다.

![fig_10](/assets/img/posts/2021-09-11-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-3-하드웨어-연구/fig_10.png)

*$[Fig.\,10]$ 범용 서보모터 Datasheet*

핀 `#1` Signal은 **PWM 역할**을 하는 부분인데 **최소 입력이 `3.3V`, 최대 입력이 `Vservo + 0.2V`**로 되어있다. 이 입력은 서보모터를 돌리기 위한 전압이 아니라 **서보모터에 데이터를 전송하기 한 전압(=PWM/서보 모듈을 동작시키기 위한 전압)**이며, Raspberry Pi의 `3V3`을 통해 `3.3V`의 전압이 공급되므로 최소 입력 조건을 만족한다. 서보모터를 동작시키기 위한 전압인 핀 `#2` Vservo 또한 **외부 입력을 통해 Typical `5.0V`를 만족**시키며 모든 회로가 정상 동작한다.
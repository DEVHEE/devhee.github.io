---
title: AI / TensorFlow Lite for Microcontrollers - 2. 사전준비
author: DEVHEE
date: 2021-06-23 12:17:52 +0900
categories: [Projects, AI]
tags: [project, ai, tensorflow, tensorflow lite, microcontroller, mcu, arduino, sparkfun, google, tinyml]
math: true
image:
    src: /assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/preview.png
---

![Preview_2](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/preview_2.gif)

# **TensorFlow Lite for Microcontrollers**

<iframe id="ark-frame" allowtransparency="true" style="background: #FFFFFF; width:100%; height:220px; border-width:0px; border-color:#959595; border-style:solid;" src="https://drive.google.com/embeddedfolderview?id=1iO6bGLNJFk6tsR4E53owU9Fchr48CWku#list"></iframe>

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">TensorFlow Lite for Microcontrollers는 <a href="https://www.oreilly.com/library/view/tinyml/9781492052036/" target="_blank">O'Reilly TinyML</a> 교과서 원서를 참고하였습니다.</b><br>
</div>

# **개발 보드 준비**

이번 TensorFlow Lite for Microcontrollers 프로젝트에서는 [Arduino Nano 33 BLE Sense](https://store.arduino.cc/usa/nano-33-ble-sense-with-headers){: target="_blank"}와 [SparkFun Edge](https://www.sparkfun.com/products/15170){: target="_blank"}를 사용할 것이다.

## **Arduino Nano 33 BLE Sense**

![Fig. 1](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_1.jpg)

<div style="float: left; width: 50%; padding-right: 9px; padding-bottom: 20px">
<img src="/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_2.jpg">
</div>
<div style="float: left; width: 50%; padding-left: 9px; padding-bottom: 20px">
<img src="/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_3.jpg">
</div>


Arduino Nano 33 BLE Sense는 가능한 최소의 폼펙터인 45*18mm의 Arduino 3.3V AI 지원 보드이며, nRF52840 마이크로 컨트롤러를 기반으로한다

Arduino Nano 33 BLE Sense는 잘 알려진 폼펙터의 완전히 새로운 보드이다. 임베디드 센서가 함께 제공된다.

- 9축 관성 센서: 웨어러블 장치에 이상적이다.
- 습도 및 온도 센서: 환경 조건을 매우 정확하게 측정한다.
- 기압 센서: 간단한 기상 관측을 할 수 있다.
- 마이크: 실시간으로 사운드 캡처 및 분석이 가능하다
- 제스처, 근접, 조도 센서: 광도를 측정 및 보드 접근 여부도 측정한다.

![Fig. 4](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_4.png)

Arduino Nano 33 BLE Sense는 기존 Arduino Nano의 진화형이지며 훨씬 더 강력한 프로세서인 Nordic Semiconductors의 nRF52840, 32비트 ARM® Cortex™-M4 64MHz CPU를 갖추고 있다. 이를 통해 Arduino Uno(1MB 프로그램 메모리, 32배 더 큼)보다 더 큰 프로그램을 만들 수 있고, 더 많은 변수(RAM이 128배 더 큼)를 사용할 수 있다. 메인 프로세서에는 NFC를 통한 Bluetooth® 페어링 및 초저전력 소비 모드와 같은 기능이 포함되어있다.

### **임베디드 인공지능**

다양한 센서 외에도 이 보드의 주요 기능은 TinyML을 사용하여 Edge Computing 애플리케이션(AI)을 실행할 수 있다는 것이다. TensorFlow™ Lite를 사용하여 기계학습 모델을 만들고 Arduino IDE를 사용하여 보드에 업로드 할 수 있다.

<iframe src="https://drive.google.com/file/d/1HsKeXlMDgnxOn5tw7IHY1zJWLWB4Hi1U/preview" width="100%" height="480" allow="autoplay"></iframe>

<iframe src="https://drive.google.com/file/d/1DPmqeKyZF0X8xYj3rleigkKQ4vBEFkUB/preview" width="100%" height="480" allow="autoplay"></iframe>

## **SparkFun Edge**

![Fig. 5](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_5.jpg)

클라우드는 매우 강력하지만 상시 연결에는 전원이 필요하며 이를 사용하지 못할 수도 있다. 엣지 컴퓨팅은 "예"라고 대답했는지 여부와 같은 개별 작업을 처리하고 그에 따라 응답한다. 오디오 분석은 웹이 아닌 Edge에서 수행된다. 이를 통해 잠재적인 데이터 개인 정보 유출을 제한하면서 비용과 복잡성을 대폭 줄일 수 있다.

Google 및 Ambiq와 협력하여 SparkFun의 Edge Development Board는 최신 기술을 기반으로 하며 다른 회사의 원격 서비스에 의존하지 않고 음성 및 제스처 인식에 이상적이다. 정말 특별한 기능은 Ambiq Micro의 최신 Apollo3 Blue 마이크로 컨트롤러 활용이다. 이 마이크로 컨트롤러의 초고효율 ARM Cortex-M4F 48MHz (96MHz 버스트 모드 포함) 프로세서는  6uA/MHz만으로 TensorFlow Lite를 실행할 수 있는 사양이다. SparkFun Edge 보드는 현재 최대 1.6mA@3V 및 48MHz로 측정되며 CR2032 코인 셀 배터리만으로 최대 10일 동안 작동할 수 있다. Apollo3 Blue는 구성 가능한 I2C/SPI 마스터 6개, UART 2개, I2C/SPI 슬레이브 1개, 15채널 14비트 ADC, BLE5를 지원하는 전용 블루투스 프로세서 등 현대적 마이크로 컨트롤러의 모든 최첨단 기능을 자랑한다. 또한 Apollo3 Blue는 플래시 1MB와 SRAM 메모리 384KB를 갖추고 있어 대부분의 애플리케이션에 적합하다.

Edge에는 센서, Bluetooth, I2C 확장 및 GPIO 입력/출력에 대한 액세스가 내장되어 있다. 음성 인식과 같은 엣지 컴퓨팅 케이스를 지원하기 위해 Edge 보드에는 MEMS 마이크 2개, 자체 I2C BUS에 ST LIS2DH12 3축 가속도계 1개, OV7670 카메라 인터페이스용 커넥터가 있다. TensorFlow가 알고리즘을 업데이트 할 수록 SparkFun Edge에 대한 더 많은 기능이 열릴 것이다. 온보드 Bluetooth 안테나는 Edge에 out-of-the-box 연결을 제공한다. I2C 센서/장치, LED 4개 및 GPIO 핀 4개를 추가하는 Qwiic 커넥터도 보드에 있다. 보드의 저전력 기능을 위해 CR2032 코인 셀 홀더에서 배터리 작동을 제공한다. 보드 프로그래밍은 직렬 부트 로더를 통한 직렬 기본 브레이크 아웃과 같은 외부 USB 직렬 어댑터로 처리 되지만 고급 사용자를 위해 JTAG 프로그래밍 및 디버거 포트도 사용할 수 있다.

<iframe src="https://drive.google.com/file/d/1eTpL89yUbSwSA8z73Qjlm0-bRNV8wSHJ/preview" width="100%" height="480" allow="autoplay"></iframe>

# **개발 환경 준비**

현재 나는 ARM MacBook Pro (13-inch, M1, 2020) macOS Monterey 12.0 Beta（21A5248p）로 개발하고 있지만, 각자의 시스템에 맞춰 환경을 구성하면 된다.

## **Windows**

**SYSTEM**: Intel i5-7600 CPU, 16GB RAM, Windows 10 Education

### **다운로드 목록**

> - [VMware Workstation Player](https://www.vmware.com/go/getplayer-win)
> - [Ubuntu 18.04.5 LTS (Bionic Beaver) 64-bit PC (AMD64) desktop image](https://releases.ubuntu.com/18.04/ubuntu-18.04.5-desktop-amd64.iso)

### **환경 구성**

**1.** VMware Workstation Player와 Ubuntu 18.04.5 LTS (Bionic Beaver) 64-bit PC (AMD64) desktop image를 다운로드 한 후 VMware Workstation Player(이하 VMware)를 설치한다.

<div style="float: left; width: 50%; padding-right: 9px; padding-bottom: 20px">
<img src="/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_6.png">
</div>
<div style="float: left; width: 50%; padding-left: 9px; padding-bottom: 20px">
<img src="/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_7.png">
</div>

**2-1.** 새로운 가상머신을 생성한다.

![Fig. 8](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_8.png)

**2-2.** 설치 디스크 이미지 파일을 지정한다. 이미 다운받아둔 Ubuntu 18.04.5 LTS (Bionic Beaver) 64-bit PC (AMD64) desktop image 파일을 선택한다.

![Fig. 9](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_9.png)

**2-3.** 본인의 이름과 시스템 사용자 이름 및 비밀번호를 설정한다.

![Fig. 10](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_10.png)

**2-4.** 가상머신 이름 및 가상머신 위치를 지정한다.

![Fig. 11](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_11.png)

**2-5.** 디스크 용량을 지정한다. 리눅스는 시스템 크기가 크지 않기 때문에 20GB 정도로 작게 지정해도 문제없다. 다음으로 단일파일로 설정할 것인지, 복수의 파일로 분할할 것인지 선택해야한다. 단일파일로 설정하면 위에 지정한 20GB 크기의 가상 디스크가 한번에 만들어져 용량을 많이 차지하지만 퍼포먼스가 좋고, 복수의 파일로 분할하면 사용한 만큼 디스크의 크기가 20GB가 될 때까지 자동적으로 증가하여 용량을 적게 차지하며 이동 및 복사가 쉽지만 퍼포먼스가 떨어진다.

![Fig. 12](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_12.png)

**2-6.** 마지막으로 가상머신 하드웨어를 커스터마이징 할 수 있다. 하지만 기본 설정대로 진행해도 문제없다.

![Fig. 13](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_13.png)

**3.** 그러고나서 Ubuntu를 실행시키면 창이 하나 뜬다. VMware Tools Linux판을 다운로드 및 설치한다. 가상환경과 윈도우간의 파일 공유나 설정 공유등을 위한 소프트웨어이다.

![Fig. 14](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_14.png)

**4.** 자동적으로 Ubuntu 설치가 및 설정이 진행된다.

![Fig. 15](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_15.png)

**5.** 설치가 완료되면 사용자 아이디와 비밀번호를 사용해 로그인한다.

![Fig. 16](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_16.png)

**6-1.** 초기설정 및 업데이트를 위해 왼쪽 아래 애플리케이션 목록을 열어 Terminal 앱을 열어준다.

![Fig. 17](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_17.png)

**6-2.** Python3가 설치되어있는지 확인하기위해 `python3 --version`을 입력해 확인해본다. 보통 기본적으로 `Python 3.6.9`가 설치되어있다.

만약 설치가 되어있지 않다면, 다음 명령어 중 하나를 실행하여 설치한다.

```bash
$ sudo apt update
$ sudo apt install python3.7
$ sudo apt install python3.8
```

![Fig. 18](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_18.png)

**6-3.** 다음 명령어를 순서대로 입력해 초기설정 및 업데이트를 진행한다.

```bash
$ sudo apt-get update
$ sudo apt-get upgrade

$ sudo apt-get install git
$ sudo apt-get install python3-pip
$ sudo apt-get install curl

$ sudo pip3 install pycrypto pyserial --user
```

<div style="float: left; width: 50%; padding-right: 9px; padding-bottom: 20px">
<img src="/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_19.png">
</div>
<div style="float: left; width: 50%; padding-left: 9px; padding-bottom: 20px">
<img src="/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_20.png">
</div>

## **macOS**

**SYSTEM**: ARM MacBook Pro (13-inch, M1, 2020) macOS Monterey 12.0 Beta（21A5248p）

### **환경 구성**

**1.** macOS는 기본적으로 Linux와 같은 Unix 기반이기에 따로 Ubuntu Linux를 설치해 주지 않아도 된다.

**2.** Homebrew를 설치해준다. Homebrew는 macOS용 패키지 관리자이다.

[Homebrew 공식 사이트](https://brew.sh/index_ko){: target="_blank"}의 가이드에 나와있는 설치 스크립트를 실행한다.

```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

<div id="copycode" style="display: none;">
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
</div>

<button onclick="copycode(this.id)">코드 복사</button>

그 후 Homebrew가 잘 설치되었는지 확인하기 위해 다음 명령어를 실행하여 `wget`을 설치해본다.

```bash
$ brew install wget
```

![Fig. 21](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_21.png)

**3.** `make`를 설치한다.

```bash
$ brew install make
```

기존 `make`와 충돌하지 않게 `brew`로 설치한 `make`는 `gmake` 명령어로 사용하지만, zsh 쉘인 경우 `.zshrc`파일, bash 쉘인 경우 `.bashrc`파일에 다음을 추가하여 새로운 `make`로 통합할 수 있다.

```bash
PATH="/opt/homebrew/opt/make/libexec/gnubin:$PATH"
```

여기서 Homebrew가 설치된 위치인 `/opt/homebrew`는 CPU마다 다른데 ARM(M1)용 Homebrew는 `/opt/homebrew`에 설치되며 `$ which brew` 명령어로 확인할 수 있다.

마지막으로 `make`의 버전이 `4.0` 이상인지 확인한다.

![Fig. 22](/assets/img/posts/2021-06-23-Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/fig_22.png)

[참고] Arduino / SparkFun
---
title: AI / TensorFlow Lite for Microcontrollers - 1. 이론
author: DEVHEE
date: 2021-06-22 23:12:22 +0900
categories: [Projects, AI]
tags: [project, ai, tensorflow, tensorflow lite, microcontroller, mcu, arduino, sparkfun, google, tinyml]
math: true
image:
    src: /assets/img/posts/2021-06-22-Projects_AI_TensorFlow-Lite-for-Microcontrollers-1-이론/preview.png
---

![Preview_2](/assets/img/posts/2021-06-22-Projects_AI_TensorFlow-Lite-for-Microcontrollers-1-이론/preview_2.gif)

# **TensorFlow Lite for Microcontrollers**

<iframe id="ark-frame" allowtransparency="true" style="background: #FFFFFF; width:100%; height:220px; border-width:0px; border-color:#959595; border-style:solid;" src="https://drive.google.com/embeddedfolderview?id=1iO6bGLNJFk6tsR4E53owU9Fchr48CWku#list"></iframe>

<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">TensorFlow Lite for Microcontrollers는 <a href="https://www.oreilly.com/library/view/tinyml/9781492052036/" target="_blank">O'Reilly TinyML</a> 교과서 원서를 참고하였습니다.</b><br>
</div>

# **TensorFlow Lite**

TensorFlow Lite는 개발자가 휴대기기, 내장형 기기 및 IoT 기기에서 TensorFlow 모델을 실행할 수 있도록 지원하는 도구 모음이다. 기기 내 지연 시간이 짧고 바이너리 크기가 작은 머신러닝 추론을 지원한다.

TensorFlow Lite는 다음과 같은 두 가지 주요 구성요소로 구성된다.

- **TensorFlow Lite 인터프리터** - 스마트폰, 내장형 Linux 기기 및 마이크로 컨트롤러를 비롯하여 다양한 하드웨어 유형에서 특별히 최적화된 모델을 실행한다. 입력 데이터를 기반으로 예측을 수행하기 위해 기기에서 TensorFlow Lite 모델을 실행하는 프로세스를 나타낸다. TensorFlow Lite 모델로 추론을 수행하려면 인터프리터를 통해 실행해야한다. TensorFlow Lite 인터프리터는 간결하고 빠르도록 설계되었다. 인터프리터는 정적 그래프 순서 및 사용자 지정 (덜 동적) 메모리 할당자를 사용하여 로드, 초기화 및 실행 대기 시간을 최소화한다.

- **TensorFlow Lite 변환기** - TensorFlow 모델을 인터프리터가 사용할 수 있는 효율적인 형식으로 변환하며, 최적화를 도입하여 바이너리 크기 및 성능을 향상할 수 있다. TensorFlow 모델을 사용하고 TensorFlow Lite 모델(`.tflite` 파일 확장자로 식별되는 최적화된 FlatBuffer 형식)을 생성한다. 변환기를 사용하는 옵션에는 다음 두 가지가 있다.

  - **Python API(권장)**: 모델 개발 파이프라인의 일부로 모델을 더 쉽게 변환하고 최적화를 적용하며 메타데이터를 추가하는 등 다양한 기능이 많다.
  - **명령줄**: 기본 모델 변환만 지원한다.

![Fig. 1](/assets/img/posts/2021-06-22-Projects_AI_TensorFlow-Lite-for-Microcontrollers-1-이론/fig_1.png)

*$[Fig.\,1]$ Convert Workflow*

## **엣지 머신러닝**

TensorFlow Lite는 서버에서 데이터를 주고받는 대신 네트워크 '엣지' 기기에서 머신러닝을 쉽게 실행할 수 있도록 설계되었다. 이러한 설계를 통해 개발자가 기기에서 머신러닝을 실행할 때 다음 사항을 개선할 수 있다.

- 지연 시간: 서버까지의 왕복이 없다.
- 개인정보 보호: 데이터가 기기를 벗어나지 않아도 된다.
- 연결: 인터넷 연결이 필요없다.
- 전력 소비: 네트워크 연결에는 전력이 필요하다.
- TensorFlow Lite는 초소형 마이크로 컨트롤러에서 강력한 스마트폰에 이르기까지 광범위한 기기에서 작동한다.

<blockquote style="margin-top: 7%;"><b>POINT</b></blockquote>
<div class="blockquote-div">
TensorFlow Lite 바이너리는 지원되는 125개 이상의 연산자가 모두 연결될 때 1MB 이하이며(32비트 ARM 빌드) 공통 이미지 분류 모델 InceptionV3 및 MobileNet을 지원하는 데 필요한 연산자만 사용할 때 300KB 미만이다.
</div>

# **TensorFlow Lite for Microcontrollers**

TensorFlow Lite for Microcontrollers는 메모리가 몇 KB만 있는 마이크로 컨트롤러 및 기타 기기에서 머신러닝 모델을 실행하도록 설계되었다. 코어 런타임이 Arm Cortex M3에서 16KB로 적합하며 여러 기본 모델을 실행할 수 있다.. 운영체제 지원, 표준 C 또는 C++ 라이브러리 또는 동적 메모리 할당이 필요없다.

## **마이크로 컨트롤러가 중요한 이유**

마이크로 컨트롤러는 일반적으로 기본적인 컴퓨팅이 필요한 하드웨어에 삽입되는 소형 저전력 컴퓨팅 기기이다. 소형 마이크로 컨트롤러에 머신러닝을 도입하면 흔히 대역폭 및 전력 제약이 적용되어 지연 시간이 길어지는 안정적인 인터넷 연결이나 값비싼 하드웨어에 의존하지 않고도 가전제품, 사물 인터넷 기기 등 생활 속에서 사용하는 수십억 기기의 인텔리전스를 강화할 수 있다. 기기에서 나가는 데이터가 없으므로 개인정보도 보호할 수 있다.

## **지원되는 플랫폼**

TensorFlow Lite for Microcontrollers는 C++ 11로 작성되었으며 32비트 플랫폼이 필요하다. [Arm Cortex-M 시리즈](https://developer.arm.com/ip-products/processors/cortex-m){: target="_blank"} 아키텍처를 기반으로 하는 여러 프로세서를 통해 광범위하게 테스트되었으며 [ESP32](https://www.espressif.com/en/products/socs/esp32){: target="_blank"}를 포함한 다른 아키텍처로 이전되었다. 프레임워크는 Arduino 라이브러리로 제공된다. 또한 Mbed와 같은 개발 환경을 위한 프로젝트를 생성할 수 있다. 오픈소스이며 C++ 11 프로젝트에 포함될 수 있다.

다음과 같은 개발 보드가 지원된다.

- [Arduino Nano 33 BLE Sense](https://store.arduino.cc/usa/nano-33-ble-sense-with-headers){: target="_blank"}
- [SparkFun Edge](https://www.sparkfun.com/products/15170){: target="_blank"}
- [STM32F746 Discovery 키트](https://www.st.com/en/evaluation-tools/32f746gdiscovery.html){: target="_blank"}
- [Adafruit EdgeBadge](https://www.adafruit.com/product/4400){: target="_blank"}
- [Adafruit TensorFlow Lite for Microcontrollers 키트](https://www.adafruit.com/product/4317){: target="_blank"}
- [Adafruit Circuit Playground Bluefruit](https://learn.adafruit.com/tensorflow-lite-for-circuit-playground-bluefruit-quickstart?view=all){: target="_blank"}
- [Espressif ESP32-DevKitC](https://www.espressif.com/en/products/devkits/esp32-devkitc/overview){: target="_blank"}
- [Espressif ESP-EYE](https://www.espressif.com/en/products/devkits/esp-eye/overview){: target="_blank"}
- [Wio Terminal: ATSAMD51](https://www.seeedstudio.com/Wio-Terminal-p-4509.html){: target="_blank"}
- [Himax WE-I Plus EVB 엔드포인트 AI 개발 보드](https://www.sparkfun.com/products/17256){: target="_blank"}
- [Synopsys DesignWare ARC EM 소프트웨어 개발 플랫폼](https://www.synopsys.com/dw/ipdir.php?ds=arc-em-software-development-platform){: target="_blank"}

[참고] TensorFlow Lite Guide
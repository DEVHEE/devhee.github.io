---
title: Robot / AI Robot Hand with Raspberry Pi - 1. 구상
author: DEVHEE
date: 2021-09-09 17:45:38 +0900
categories: [Projects, Robot]
tags: [project, robot, ai, opencv, computer vision, raspberry pi, python]
math: true
image:
    path: /assets/img/posts/2021-09-09-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-1-구상/preview.jpeg
---

# **개요**

## **제작동기**

최근에 유튜브를 보던 중 로봇팔에 대한 영상을 본 적이 있다. 손이나 팔이 불편한 사람이 로봇팔을 착용해 물건을 들어올릴 수 있게 되고, 가위로 종이 자르기 등과 같은 정교한 손동작도 가능케 하는 내용의 영상이였다.

영화 퍼시픽림과 같이 생각 또는 작은 손동작 하나로 제어하고 그로인해 인간에게 도움을 주는 그런 로봇이 실제로도 만들어지고 있고 사용되어지고 있다는 의미이다.

그래서 평소 몸이 불편한 장애인들을 위한 소프트웨어 및 전자제어장치에 관심이 많던 나는 직접 사람의 손을 모방한 로봇손을 제작해보며 관련 공부를 해보고자 한다.

<iframe width="100%" height="400" src="https://www.youtube.com/embed/4VGRoUfa5R4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="100%" height="400" src="https://www.youtube.com/embed/ByLGTKrRXKY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## **제작목적**

현실적으로 재료나 장비 및 전문가급 지식이 없기에 완벽하게 따라 만드는 것은 불가능하다. 따라서 Computer Vision을 활용해 손동작을 따라하는 로봇손을 만들고자 한다. 

손동작을 따라하는 것을 넘어 물건을 집거나 사용할 수 있도록 해 볼 것이다.

# **사전준비**

## **기획**

대략적인 구상도는 다음과 같다.

![Fig. 1](/assets/img/posts/2021-09-09-Projects_Robot_AI-Robot-Hand-with-Raspberry-Pi-1-구상/fig_1.png)

*$[Fig.\,1]$ 구상도*

Computer Vision를 이용하여 Raspberry Pi와 연결된 카메라로 손동작을 인식하는 소프트웨어를 개발하고, 인식한 손동작을 바탕으로 로봇손 서보모터를 제어한다.

## **선행연구**

### **Computer Vision**

Computer Vision은 컴퓨터와 시스템이 디지털 이미지, 비디오 및 기타 시각적 입력에서 의미 있는 정보를 도출하고 해당 정보를 기반으로 조치를 취하거나 권장할 수 있도록 하는 인공지능(AI) 분야이다. AI가 컴퓨터가 생각하는 것을 가능하게 한다면, Computer Vision은 컴퓨터가 보고, 관찰하고, 이해할 수 있도록 한다.

Computer Vision은 인간이 먼저 출발한다는 점을 제외하면 Human Vision과 거의 동일하게 작동한다. 인간의 시각은 사물을 구별하는 방법, 얼마나 멀리 떨어져 있는지, 움직이는지, 이미지에 이상이 있는지 여부를 훈련시키는 문맥의 이점을 가지고 있다.

Computer Vision은 이러한 기능을 수행하도록 기계를 훈련시키지만 망막, 시신경, 시각 피질보다는 카메라, 데이터, 알고리즘으로 훨씬 더 짧은 시간에 작동시켜야 한다. 제품을 검사하거나 생산 자산을 감시하도록 훈련된 시스템은 감지할 수 없는 결함이나 문제를 발견하여 1분에 수천 개의 제품이나 공정을 분석할 수 있기 때문에 인간의 능력을 빠르게 능가할 수 있다.

Computer Vision은 에너지 및 유틸리티에서 제조 및 자동차에 이르는 산업에 사용되며 시장은 계속 성장하고 있다. 2022년에는 486억 달러에 이를 것으로 예상된다.

Computer Vision은 많은 데이터를 필요로 한다. 구별을 식별하고 궁극적으로 이미지를 인식할 때까지 계속해서 데이터를 분석한다. 예를 들어, 컴퓨터가 자동차 타이어를 인식하도록 훈련시키려면, 특히 결함이 없는 타이어를 인식하기 위해 대량의 타이어 이미지와 타이어 관련 항목을 제공해야 한다.

이를 달성하기 위해 두 가지 필수 기술인 딥러닝과 Convolutional Neural Network (CNN)이 사용된다.

기계학습은 컴퓨터가 시각 데이터의 맥락을 스스로 학습할 수 있도록 하는 알고리즘 모델을 사용한다. 충분한 데이터가 모델을 통해 공급되면, 컴퓨터는 데이터를 "학습을 위해 입력"한 이미지와 다른 이미지를 구분하도록 스스로 학습한다. 알고리즘은 누군가가 이미지를 인식하도록 프로그래밍하는 대신 기계가 스스로 학습할 수 있게 한다.

CNN은 이미지를 태그나 레이블이 지정된 픽셀로 분해하여 머신러닝 또는 딥러닝 모델을 볼 수 있도록 지원한다. 이는 컨볼루션을 수행하기 위해 라벨을 사용하고 (제3의 함수를 생성하기 위해 두 함수에 대한 수학적 연산) 그것이 무엇을 보고 있는지 예측한다. 신경망은 컨볼루션을 실행하고 예측이 실현되기 시작할 때까지 일련의 반복으로 예측의 정확도를 점검한다. 그리고 나서 인간과 유사한 방식으로 이미지를 인식하거나 보는 것이다.

사람이 멀리서 이미지를 만드는 것처럼 CNN은 먼저 단단한 모서리와 단순한 모양을 식별한 다음 예측의 반복을 실행하면서 정보를 채운다. CNN은 단일 이미지를 이해하는 데 사용된다. Recurrent Neural Network (RNN)은 일련의 프레임의 사진이 서로 어떻게 관련되어 있는지 컴퓨터가 이해하는 데 도움이 되는 비디오 응용 프로그램에 유사한 방식으로 사용된다.

### **OpenCV**

OpenCV(Open Source Computer Vision Library)는 오픈소스 Computer Vision 및 기계학습 소프트웨어 라이브러리이다. OpenCV는 Computer Vision 애플리케이션을 위한 공통 인프라를 제공하고 상용 제품에서 기계 인식의 사용을 가속화하기 위해 구축되었다. BSD 라이센스 제품인 OpenCV를 사용하면 기업이 코드를 쉽게 활용하고 수정할 수 있다.

라이브러리에는 2500개 이상의 최적화된 알고리즘이 있으며, 여기에는 클래식 및 최첨단 컴퓨터 비전과 기계 학습 알고리즘의 포괄적인 세트가 포함되어 있다. 이러한 알고리즘은 얼굴 감지 및 인식, 물체 식별, 비디오의 인간 행동 분류, 카메라 움직임 추적, 움직이는 물체 추적, 스테레오 카메라에서 3D 포인트 클라우드 생성, 전체 장면의 고해상도 이미지 생성, 이미지 데이터로부터 유사한 이미지 찾기에 사용될 수 있다. 베이스, 플래시를 사용하여 찍은 이미지에서 붉은 눈을 제거하고 눈의 움직임을 따라하며 풍경을 인식하며 증강 현실로 오버레이할 마커를 설정한다. OpenCV에는 47,000명 이상의 사용자 커뮤니티가 있으며 다운로드 수는 1,800만 건을 넘을 것으로 추산된다. 이 도서관은 기업, 연구 단체, 정부 기관 등에서 광범위하게 사용되고 있다.

구글, 야후, 마이크로소프트, 인텔, IBM, 소니, 혼다, 도요타 같은 라이브러리를 채용하는 회사들과 함께, OpenCV를 광범위하게 사용하는 Applied Minds, VideoSurf, Zeitera와 같은 많은 신생 회사들이 있다. OpenCV는 스트리트뷰 이미지를 만들고, 이스라엘 감시 영상으로부터 침입을 감지하고, 중국의 광산 장비를 감시하고, 로봇이 Willow Garage에서 물체를 탐색하고 줍는 것을 돕고, 유럽의 수영장 익사 사고를 감지하는 등 다양한 분야에 걸쳐 있다. 터키에서 잔해를 조사하거나, 전 세계 공장의 제품에 붙은 라벨을 검사하고, 일본에서 신속한 얼굴 검출을 위한 방법에 사용되고 있다.

C++, Python, Java, MATLAB 인터페이스를 갖추고 있으며 Windows, Linux, Android, macOS를 지원한다. OpenCV는 대부분 Real-Time Vision 애플리케이션이며 MMX 및 SSE 지침을 활용한다. 현재 완전한 기능의 CUDA 및 OpenCL 인터페이스가 활발히 개발되고 있다. 500개가 넘는 알고리즘이 있으며, 이러한 알고리즘을 구성하거나 지원하는 함수는 약 10배이다. OpenCV는 기본적으로 C++로 작성되며 STL 컨테이너와 완벽하게 작동하는 템플리트 인터페이스를 갖추고 있다.

### **Raspberry Pi**

Raspberry Pi는 사람들에게 컴퓨터 교육을 시키고 컴퓨터 교육에 더 쉽게 접근할 수 있도록 하는 것을 목표로 하는 영국의 자선단체인 Raspberry Pi 재단이 만든 일련의 단일 보드 컴퓨터이다.

전 세계적으로 사람들은 프로그래밍 기술을 배우고, 하드웨어 프로젝트를 만들고, Home Automation 작업을 하고, Kubernetes 클러스터와 Edge 컴퓨팅을 구현하고, 심지어 산업용 애플리케이션에 사용하기 위해 Raspberry Pi를 사용한다.

Raspberry Pi는 리눅스를 실행하는 매우 저렴한 컴퓨터이지만 물리 컴퓨팅을 위한 전자 부품을 제어하고 사물 인터넷(IoT)을 탐색할 수 있는 GPIO 핀 세트도 제공한다.

---
title: etc / Intel 또는 M1 맥에서 모네로(Monero) 암호화폐 채굴하기
author: DEVHEE
date: 2021-05-18 09:40:16 +0900
categories: [Programs, etc]
tags: [program, coding, mining, monero, xmr, cryptocurrency, intel, m1, mac, moneroocean]
image:
    src: /assets/img/posts/2021-05-18-Programs_etc_Intel-또는-M1-맥에서-모네로-Monero-XMR-암호화폐-채굴하기/preview.jpeg
---

# **모네로(Monero XMR)란**

모네로는 2014년에 개발된 익명성, 개인정보보호에 초점이 맞춰진 암호화폐이다.

모네로를 이용하는 사용자는 신원을 숨길 수 있으며, 제삼자로부터 송금된 금액 또한 숨길 수 있다.

이 때문에 범죄에 악용될 우려도 있다.

## **모네로의 특징**

모네로의 주요 특징은 다음 세 가지 이다.

- 익명성이 높고, 개인정보보호에 탁월하다.
- 일반 PC에서도 채굴이 가능하다.
- 송금 속도가 빠르다.

### **익명성이 높고, 개인정보보호에 탁월하다**

모네로은 익명성이 높고, 거래 당사자의 개인정보보호에 뛰어난 암호화폐이다.

암호화폐에서 **익명성이 높다**라는 것은 **누구에게 송금 했는지**라는 정보를 거래 당사자 이외의 곳에서 확인할 수 없음을 의미한다.

익명성이 높기 때문에 정보의 유출 및 무단 액세스를 방지 할 수 있다.

또한 모네로는 **링 서명**, **스텔스 어드레스**라는 기술을 채용하여 그 익명성을 만들어 내고 있다.

그러나 모네로은 높은 익명성이라는 뛰어난 성능에 좋은 평가를 모으는 반면, 그 성능을 악용한 각종 범죄 및 테러리스트 자금 공급 경로 및 암시장 사이트의 결제 수단으로 사용되는 것을 우려하고 있다.

실제로 최근 대한민국에서 일어난 사상 최대 디지털 성범죄 사건인 **[n번방 성착취물 제작 및 유포 사건](https://www.donga.com/news/Society/article/all/20200327/100385869/1){:target="_blank"}**에 채널 입장료로 사용되었다.

따라서 <span style="color:red"><b>모네로를 절대로 범죄에 사용하지 마라</b></span>. 나는 그냥 공부 겸 재미로 채굴해 보는 것이다.

### **일반 PC에서도 채굴이 가능하다.**

비트 코인은 고사양의 PC가 없으면 채굴의 의미가 없다.

또한 고사양 PC를 장시간 가동하면 엄청난 전기세 폭탄을 맛보게 될 것이도, PC에서 나오는 열을 식히거나 있거나 설치 시설 확보 및 유지를 위한 자금 투자비용이 크다.

하지만 모네로는 가정용 PC 등 일반적인 사양의 PC에서도 충분히 채굴할 수 있다.

때문에 채굴 장벽이 낮다는 특징도 범죄에 악용되고 있으며, 해커가 회사의 PC를 좀비PC로 만들어 모네로를 채굴하는 **스크립트 재킹** 피해도 일부 발생하고 있다.

### **송금 속도가 빠르다.**

모네로는 송금 속도도 빠르다.

비트코인의 경우는 송금에 약 10분이 소요된다.

그러나 모네로의 경우에는 약 2분으로 비트코인에 비해 약 1/5의 시간으로 송금할 수 있다.

# **모네로 채굴하기**

## **지갑 만들기**

모네로 채굴을 위해서는 먼저 지갑을 만들어야 한다.

암호화폐도 돈이니 돈이 들어오려면 들어올 공간이 있어야 하지 않겠는가.

[Monero 공식 홈페이지](https://www.getmonero.org/downloads/){:target="_blank"}에서 기본적으로 지갑을 제공하고 있지만, 우리는 **MyMonero**라는 지갑을 사용할 것이다.

[MyMonero 홈페이지](https://mymonero.com/){:target="_blank"}에서 지갑을 다운로드, 생성해준다.

![Fig. 1](/assets/img/posts/2021-05-18-Programs_etc_Intel-또는-M1-맥에서-모네로-Monero-XMR-암호화폐-채굴하기/fig_1.png)

## **채굴기 다운로드**

채굴을 위한 [XMRig](https://github.com/xmrig/xmrig){:target="_blank"} 채굴기를 다운로드 받아준다.

[XMRig](https://github.com/xmrig/xmrig){:target="_blank"}는 CPU 전용 채굴기로, 애플리케이션 구조가 간단하고 윈도우와 리눅스 계열, macOS 등 많은 운영체제를 지원하며, 32/64비트를 지원하고 ARM용 컴파일이 가능해 널리 사용되고 있다.

[XMRig GitHub Releases 페이지](https://github.com/xmrig/xmrig/releases){:target="_blank"}에서 최신 버전의 파일을 다운로드 받아준다.

나의 경우에는 M1 MacBook Pro이므로 `xmrig-6.12.1-macos-arm64.tar.gz`를, Intel Mac은 `xmrig-6.12.1-macos-x64.tar.gz`를 다운받으면 된다.

다운로드 받은 파일을 `/Applications`폴더에 압축해제한다.

## **채굴풀 찾기**

"백지장도 맞들면 낫다"라는 말이 있다. 채굴도 똑같다. 나 혼자서 채굴하기보다 여러명의 여러 컴퓨터가 같이 채굴을하면 더 빨리 모네로를 캘 수 있다.

그러려면 그 집단에 가입해야한다. 여기서 그 집단을 **채굴풀**이라고 한다.

모네로 채굴풀은 여러곳이 있다. 그 중 수수료도 가장 낮고 퍼포먼스도 잘 나오는 [MoneroOcean](https://moneroocean.stream/){:target="_blank"}을 선택할 것이다.

## **채굴기 설정**

지갑을 만들었고, 채굴풀도 찾았으니 이제 이 두개를 연결해 줄 채굴기를 설정해 볼 것이다.

압축 푼 폴더 `/Applications/xmrig-6.12.1`에 들어가면 3개의 파일이 존재한다.

![Fig. 2](/assets/img/posts/2021-05-18-Programs_etc_Intel-또는-M1-맥에서-모네로-Monero-XMR-암호화폐-채굴하기/fig_2.png)

`config.json` 파일을 VSCode 등으로 열어준다.

여기서 `pools`라는 key를 가진 객체를 찾는다.

```json
"pools": [
        {
            "algo": null,
            "coin": null,
            "url": "donate.v2.xmrig.com:3333",
            "user": "YOUR_WALLET_ADDRESS",
            "pass": "x",
            "rig-id": null,
            "nicehash": false,
            "keepalive": false,
            "enabled": true,
            "tls": false,
            "tls-fingerprint": null,
            "daemon": false,
            "socks5": null,
            "self-select": null,
            "submit-to-origin": false
        }
    ]
```

위 코드를 아래와 같이 변경해준다.

```json
"pools": [
        {
            "algo": "rx/0",
            "coin": "monero",
            "url": "gulf.moneroocean.stream:10128",
            "user": "YOUR_WALLET_ADDRESS",
            "pass": "MacBook Pro M1",
            "rig-id": null,
            "nicehash": false,
            "keepalive": false,
            "enabled": true,
            "tls": false,
            "tls-fingerprint": null,
            "daemon": false,
            "socks5": null,
            "self-select": null,
            "submit-to-origin": false
        }
    ]
```

`algo`는 채굴 알고리즘을 뜻하며 여기서는 `rx/0`로 설정한다.

`coin`은 모네로 영문 명칭인 `monero`이고

`url`은 MoneroOcean 채굴풀 주소 및 포트번호이며

`user`에는 만든 모네로 지갑의 주소를 입력하면 된다.

`pass`에는 채굴풀에 보일 Worker명이다. 굳이 설정하지 않아도 된다.

## **채굴하기**

채굴 시작은 쉽다.

터미널을 열고 방금 `/Applications/xmrig-6.12.1` 폴더의 `xmrig` 파일을 터미널로 드래그한 후 실행시키면 된다. 아니면 직접 `xmrig` 파일을 더블클릭해 실행할 수도 있다.

![Fig. 3](/assets/img/posts/2021-05-18-Programs_etc_Intel-또는-M1-맥에서-모네로-Monero-XMR-암호화폐-채굴하기/fig_3.png)

## **수익확인**

여기서 채굴한 모네로는 채굴풀에 임시 저장된다.

[MoneroOcean](https://github.com/xmrig/xmrig/releases){:target="_blank"} 사이트에 들어가면 상단에 「Your Monero Address...」라는 입력칸이 존재한다.

여기에 지갑의 주소를 입력하고 엔터를 누르면 현재 채굴 정보를 볼 수 있다.

![Fig. 4](/assets/img/posts/2021-05-18-Programs_etc_Intel-또는-M1-맥에서-모네로-Monero-XMR-암호화폐-채굴하기/fig_4.png)

하단 Worker의 값이 「0」으로 나온다면 아직 업데이트가 되지 않았기에 5분 후 다시 조회해보거나 설정이 잘못된 경우이다.

또한, 우측 계기판 아이콘을 누르면 송금 설정 및 블록 지급 이력을 등을 확인할 수 있다.

![Fig. 5](/assets/img/posts/2021-05-18-Programs_etc_Intel-또는-M1-맥에서-모네로-Monero-XMR-암호화폐-채굴하기/fig_5.png)

우측 「XMR Total Due」는 현재 채굴한 모네로 수를 뜻하며, 가운데 섹션에서 지갑으로 자동 송금할 기준과 이메일 알림, 블록 지급 이력 등을 확인할 수 있다.

![Fig. 6](/assets/img/posts/2021-05-18-Programs_etc_Intel-또는-M1-맥에서-모네로-Monero-XMR-암호화폐-채굴하기/fig_6.png)

최소 자동 송금 기준액은 **0.003 XMR**이며, 기본값은 **0.3 XMR**이다.

송금 금액에 따라 송금수수료가 달라지는데, 많이 보낼수록 수수료도 적게나온다. 

**0.3 XMR** 기준 송금수수료는 **0.0004 (0.12%) XMR**이다.

하단부를 보면 현재 채굴속도와 채굴액에 따른 일/주/월/년별 수익을 계산해볼 수 있는데, 989.9H/s의 속도로는 하루에 $0.09, 즉 하루에 겨우 100원 정도 벌 수 있다.

하지만 여기에 수수료 떼고, 전기비 등등을 제외하면 남는 것은 거의 없을것이다.

그래도 타 암호와폐 대비 성능 대비 준수한 편이니 잘 이용한다면 어느정도의 수익을 기대할 수도 있다.
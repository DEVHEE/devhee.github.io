---
title: Utility / Auto Participate in Zoom (자동 줌 수업 참여 파이썬 프로그램)
author: DEVHEE
date: 2021-05-12 23:43:15 +0900
categories: [Programs, Utility]
tags: [program, coding, python, zoom]
image:
    path: /assets/img/posts/2021-05-12-Programs_Utility_Auto-Participate-in-Zoom/preview.png
---

# **1. 개발 동기**

솔직히, 귀찮은 마음에서부터 시작했다.

줌 수업 경력 1년차, 대면수업을 온라인으로 들을 때 생기는 문제점이 몇 가지 있다.

1. 교수님의 목소리와 칠판이 잘 안보인다는 점  
   교수님들이 대부분 방송용 마이크가 아닌 노트북 내장 마이크 또는 작은 마이크를 사용해 수업을 진행하기 때문에 목소리가 뭉개질 때가 많았다.  
   칠판은 대부분 방송용 캠코더를 사용하지만 그렇지 않은 몇 강의들은 거의 보이지 않는 수준이다. 그래도 잘 보이지 않는 수업들은 따로 화면공유를 요청하면 선명하게 볼 수는 있다.

2. 인터넷 연결 문제  
   아주 가끔씩 버퍼링이 심할 때가 있다.  
   대학 내에서 실시간으로 송출할 때는 덜 하지만, 교수님 자택에서 수업하고 그것을 한국에 있는 나 또는 일본 친구들이 듣는 수업이라면 버퍼링이 장난이 아니다.  
   예를들어 교수님이 내 이름을 부르셨는데 성까지만 말하고 버퍼링이 걸려 내가 대답을 해도 교수님이 듣지 못하는 상황이 자주 발생한다.

3. 접속 타이밍 문제
   1교시 수업은 9:00에 시작해 10:30분에 끝나고 10:45분에 2교시가 시작한다.  
   이 문제는 쉬는시간에서 다음교시에 넘어갈 때 발생한다.  
   1교시와 2교시로 예를 들어보면, 난 1교시 수업이 끝나고 몇분동안 내용 정리를 한 후 2교시가 시작하기 전까지 유튜브를 보거나 거실에 나가 쉬거나 뭘 먹는다. 그런데 그러다보면 쉬는시간 15분이 금방 지나간다. 그러다가 수업 시작 몇 분 지나고 나서야 알아차리고 빨리 접속하곤 했다. 이건 뭐 내 잘못이긴 하지만, 대면강의에서는 미리 다음교시 강의실에 가 있을 상황이기에 거의 발생하지 않는 문제일 것이다.

위 세 문제점 중에 1과 2는 내 자력으로 해결할 수 있는 문제가 아니였기에 3을 해결해보고자 했다.

# **2. 기획**

이 프로그램은 생각으로도 실제로도 단순하다. 복잡한 로직이 필요 없다.

먼저 9:00에 1교시 수업이 시작한다고 해보자. 그럼, 적어도 5분 전에는 줌 회의에 접속을 해야 교수님이 입장 허가나 뭐든 해줄 것이다.

따라서 5분전에 수업 입장 링크에 자동으로 접속을 하게 만들기만 하면 된다.

## **준비**

많은 프로그래밍 언어들이 있지만, 가장 부담없이 동작할 수 있는 파이썬을 사용하기로 했다.

나는 macOS를 사용하고 있기 때문에 여기에 최적화를 할 것이다.

# **3. 실행**

## **수업 데이터 작성**

먼저, 수업에 대한 데이터를 담을 `meetings.json` 파일을 만들어 준다.

```json
{
    "mon": {
        "1045": {
            "subject": "Embedded System",
            "professor": "矢ノ倉 公泰",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Experiments in Chemistry",
            "professor": "長野 宗頼",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1440": {
            "subject": "Database A",
            "professor": "眞藤 匡房",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    },
    "tue": {
        "0900": {
            "subject": "Engineering Mathematics",
            "professor": "川城 彦佑",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1045": {
            "subject": "Image Processing",
            "professor": "田中 盛睦",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Computer Operating System",
            "professor": "五明 大振",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1440": {
            "subject": "Control Engineering",
            "professor": "明正 迦具夜",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    },
    "wed": {
        "0900": {
            "subject": "Semiconductor Theory B",
            "professor": "村川 明共",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1045": {
            "subject": "Deep Learning with Neural Networks B",
            "professor": "永本 勤一",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Network Security and Cryptography",
            "professor": "横石 人文",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    },
    "thu": {
        "0900": {
            "subject": "Economics",
            "professor": "中村 翔牙",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1045": {
            "subject": "Business Japanese",
            "professor": "佐本 鳳姫",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Electrical Circuits I",
            "professor": "石館 娃香",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1440": {
            "subject": "Electrical Circuits II",
            "professor": "石館 娃香",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1625": {
            "subject": "Digital Signal Processing",
            "professor": "高山 巧棋",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    },
    "fri": {
        "1045": {
            "subject": "Electromagnetism A",
            "professor": "石館 娃香",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Java Programming",
            "professor": "託麻 佳乃子",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    }
}

```

이 json 구조를 보면 `mon` `tue` `wed` `thu` `fri`라고 하는 `key` 안에 각 수업이 시작하는 시각 `0900`이 `%H%M` 형태로 지정 되어있고, 그 시각을 객체로 하는 과목명 `subject`, 교수명 `professor`, 회의아이디 `id`, 회의비밀번호 `pw`의 `key`에 각각의 `value`가 설정되어 있다.

예를들어 아래의 코드를 보자.

```json
"wed": {
    "1045": {
        "subject": "Deep Learning with Neural Networks B",
        "professor": "永本 勤一",
        "id": "78551527256",
        "pw": "Gv7YX5"
    }
}
```

이 객체는 `wed`(수요일)의 `1045`(10시 45분)에 시작하는 `Deep Learning with Neural Networks B` 과목, `永本 勤一` 교수님, `78551527256` 회의아이디, `Gv7YX5` 회의비밀번호 정보를 담고 있다.

## **Python 모듈 import**

필요한 Python 모듈을 불러온다.

```python
# import modules
import os  # 운영체제 관련 기능 사용
import sys  # Python Interpreter 제어
import time  # 시간 표현
import threading  # 병렬 실행
import datetime  # 날짜 및 시간 표현
import json  # json 제어
import webbrowser  # 브라우저 제어
from platform import system  # 이용 플랫폼 및 OS 정보
```

각 모듈의 용도는 오른쪽 주석의 내용과 같다.

원래 위 모듈 중 몇개는 필요없이 간단한 코드를 사용하여 동작시킬 수 있지만, 실행 환경 호환성 및 최대한 다양한 기능을 사용하며 쉽게 설명하기 위해 코드가 길고 더러울 수 있다.

## **시간 지정**

우리는 현재시간이 지정된 시간 5분 전이 되면 회의에 접속해야한다.

우선, 현재 날짜 및 시간을 구하는 코드를 작성해 볼 것이다.

`datetime`을 사용해 현재 날짜 및 시간을 구한다.

```python
ㅌㅊ = datetime.datetime.now()  # 2021-05-12 12:48:15
```

또한  년, 월, 일, 요일을 따로 따로 구하는 로직은 `time` 모듈을 사용해 볼 것이다.

우선 로컬 타임을 불러온 후

```python
t = time.localtime()
```

`tm_year`, `tm_mon`, `tm_mdat`, `tm_wday`로 년, 월, 일, 요일을 구해온다.

```python
y = str(t.tm_year)
mo = str(t.tm_mon)
dt = str(t.tm_mday)
dy = str(t.tm_wday)
```

그런데 여기서 `tm_wday`는 월요일을 `0`에서 일요일을 `6`으로하는 정수가 리턴된다.

따라서 `mon`과 같은 문자열로 된 요일을 얻기 위해서는 요일 리스트에서 순서대로 요일을 뽑아 올 필요가 있다.

그럼 다음과 같은 코드가 된다.

```python
dy_lis = ["mon", "tue", "wed", "thu", "fri"]

t = time.localtime()
y = str(t.tm_year)
mo = str(t.tm_mon)
dt = str(t.tm_mday)
dy = dy_lis[t.tm_wday]  # day
```

또한 `meeting.json`에는 시간이 `HHMM` 형식으로 지정되어 있기 때문에 현재 날짜 및 시간이 들어있는 `now`에서 시간과 분만 다시 포맷팅을 해준다.

```python
now_time = time.strftime("%H%M", t)  # 1248
```

여기서 `time.strftime`은 날짜 및 시간을 문자열로 출력해준다.

## **지정 시간 불러오기**

이제 5분전 계산을 위해 `meetings.json`에 있는 시간 `key`를 불러와야한다.

우선, json 모듈을 이용해 `key` 및 `value`를 불러올 수 있는 변수를 만들어준다.

```python
with open(path+"/meetings.json") as f:
    meeting = json.load(f)
```

시간 `key` 중에 현재 시간과 가장 가까운 다음 수업을 고르기 위해 현재시간 이후의 `key`들을 리스트로 만든 후 가장 최솟값을 가져온 후 `next_time`에 저장한다.

```python
next_time = []
for set_time in meeting[dy].keys():
    if now_time <= set_time:
        next_time.append(set_time)
next_time = min(next_time)
```

가장 가까운 다음 수업 시간 `1255`과 현재시간 `1248`의 차를 구하기 위해 다음 수업 시간의 포맷을 `YYYYmmddHHMM` 형식으로 바꿔준다.

여기서 위에 `time`모듈을 이용해 구한 년, 월, 일을 가져와 사용한다.

```python
full_next_time = y+mo+dt+next_time
full_next_time = datetime.datetime.strptime(full_next_time, "%Y%m%d%H%M")
```

위 `time.strftime`와 다르게 `time.strptime`은 문자열이 아닌 `datetime` 형식으로 바꿔준다.

사실 굳이 `time` 모듈을 사용해 년월일요일을 불러오고 `HHMM`형식의 `key`를 `YYYYmmddHHMM`의 `datetime` 형식으로 다시 바꿔줄 필요 없이 다음 수업시간 `1255`와 현재시간 `1248`만 가지고 연산을 해도 된다.

하지만 시간 연산을 활용해 보기 위해 바꾸어 주었을 뿐이다.

## **시간 연산**

이제 현재시간와 지정시간의 차이가 5분인지 몇분인지 구하는 코드를 작성한다.

방금 구한 `datetime` 형식의 다음 수업시간과 처음에 구한 `datetime` 형식의 현재시간을 빼준다.

`datetime`끼리는 빼는 연산이 가능하다.

이렇게 연산된 값은 `timedelta` 클래스로 리턴된다.

```python
min_left = full_next_time - now  # 0:06:49.763726
```

우리는 리턴값을 분으로만 계산할 것이다. 따라서 초단위의 `timedelta`로 바꿔준다음 60으로 나눈다.

```python
min_left = min_left.seconds/60  # 6.xxx
```

이로서 다음 수업시간까지의 남은 시간(분)을 구했다.

## **수업 데이터 지정**

`meetings.json` 시간 객체의 요소들을 불러온다. 여기서 `url`은 Zoom에서 Scheme를 별도로 제공하기 때문에 그것을 사용한다.

```python
subject = meeting[dy][next_time]["subject"]
professor = meeting[dy][next_time]["professor"]
id = meeting[dy][next_time]["id"]
pw = meeting[dy][next_time]["pw"]
url = "zoommtg://zoom.us/join?confno={}&pwd={}".format(id, pw)
```

## **수업 접속**

다음 코드를 사용하여 콘솔에 정보 출력 및 조건 만족 시 수업에 접속하도록 한다.

```python
if 0 <= min_left <= 5:  # 남은 시간이 0분~5분일 때
    print("-------------------------------------")
    print("[Now Datetime]", now.strftime('%Y-%m-%d %H:%M:%S'))
    print("[Next Class]", subject)
    print("[Professor]", professor)
    print("[Time Left]", int(min_left), "minute(s) left\n")
    print("{} minute(s) left until the class starts. The class link opens.".format(int(min_left)))
    print("-------------------------------------")
    pf = system()
    if pf == "Darwin":
        os.system("osascript -e 'display notification \"{} minute(s) left until the class starts. The class link opens.\"'".format(int(min_left)))
        os.system('afplay quite-impressed.m4r')
    webbrowser.open(url)
    sys.exit()
elif 10 <= min_left < 11:  # 남은 시간이 10분일 때
    print("-------------------------------------")
    print("[Now Datetime]", now.strftime('%Y-%m-%d %H:%M:%S'))
    print("[Next Class]", subject)
    print("[Professor]", professor)
    print("[Time Left]", int(min_left), "minute(s) left\n")
    print("10 minutes left until the class starts.")
    print("-------------------------------------")
    pf = system()
    if pf == "Darwin":
        os.system("osascript -e 'display notification \"10 minutes left until the class starts.\"'")
        os.system('afplay quite-impressed.m4r')
else:  # 그 외
    print("-------------------------------------")
    print("[Now Datetime]", now.strftime('%Y-%m-%d %H:%M:%S'))
    print("[Next Class]", subject)
    print("[Professor]", professor)
    print("[Time Left]", int(min_left), "minute(s) left\n")
    print("It will be updated once every minute.")
    print("-------------------------------------")
```

남은 시간이 10분 또는 5분 이하거나 수업 접속 시 사용자에게 알려주기 위해 다음의 맥 알림 및 소리를 추가해 주었다.

```python
pf = system()
if pf == "Darwin":
    os.system("osascript -e 'display notification \"{} minute(s) left until the class starts. The class link opens.\"'".format(int(min_left)))
    os.system('afplay quite-impressed.m4r')
```

수업 접속을 위한 `url`을 열고

```python
webbrowser.open(url)
```

수업에 접속했다면 프로그램을 종료시킨다.

```python
sys.exit()
```

프로그램을 시작한 시간에 남은시간이 5분 미만일 경우도 있을 수 있으므로 `0 <= min_left <= 5`로 지정했다.

또한 리턴되는 남은 분수의 `timedelta`값이 소수로 나오므로 `elif 10 <= min_left < 11`의 10분 구간을 지정해주었다.

## **실시간 업데이트**

위 코드를 실행하면 로직이 한번만 작동하고 끝난다. 따라서 우리는 이 로직을 일정 간격으로 반복하여 남은 시간을 구하고, 접속을 실행해야한다.

`threading` 모듈을 사용해 딜레이 시간을 정해준다.

`threading.Timer(60, run).start()`를 마지막에 추가해 1분마다 업데이트를 시키고, `now = datetime.datetime.now()`부터 끝까지 `run()`이라는 함수로 묶어준다.

```python
path = str(os.path.dirname(__file__))


def run():
    now = datetime.datetime.now()

    # 생략

        print("-------------------------------------")

    threading.Timer(2.5, run).start()
```

그 후 `def run():` 바깥쪽 마지막에 실행시킬 함수 `run()`을 추가해준다.

```python
path = str(os.path.dirname(__file__))


def run():
    now = datetime.datetime.now()

    # 생략

        print("-------------------------------------")

    threading.Timer(2.5, run).start()


run()
```

## **예외처리**

위 코드는 주중(월요일~금요일) AND 현재시간이 마지막 수업 시간 이전일 때에만 동작하기에, 그 외 경우를 위한 예외처리를 해주어야하지만, 굳이 그 경우에는 이 프로그램을 사용할 일이 없으니 생각하지 않도록 한다.

# **4. 전체코드**

[GitHub Repository](https://github.com/DEVHEE/auto-participate-in-zoom){: target="_blank"}

## **main.py**

```python
"""
auto-participate-in-zoom
COPYRIGHT © 2021 KIM DONGHEE. ALL RIGHTS RESERVED.
"""

# import modules
import os
import sys
import time
import threading
import datetime
import json
import webbrowser
from platform import system

path = str(os.path.dirname(__file__))


def run():
    now = datetime.datetime.now()

    dy_lis = ["mon", "tue", "wed", "thu", "fri"]

    t = time.localtime()
    y = str(t.tm_year)
    mo = str(t.tm_mon)
    dt = str(t.tm_mday)
    dy = dy_lis[t.tm_wday]  # day

    now_time = time.strftime("%H%M", t)

    with open(path+"/meetings.json") as f:
        meeting = json.load(f)

    next_time = []
    for set_time in meeting[dy].keys():
        if now_time <= set_time:
            next_time.append(set_time)
    next_time = min(next_time)

    full_next_time = y+mo+dt+next_time
    full_next_time = datetime.datetime.strptime(full_next_time, "%Y%m%d%H%M")

    min_left = full_next_time - now
    min_left = min_left.seconds/60

    subject = meeting[dy][next_time]["subject"]
    professor = meeting[dy][next_time]["professor"]
    id = meeting[dy][next_time]["id"]
    pw = meeting[dy][next_time]["pw"]
    url = "zoommtg://zoom.us/join?confno={}&pwd={}".format(id, pw)

    if 0 <= min_left <= 5:
        print("-------------------------------------")
        print("[Now Datetime]", now.strftime('%Y-%m-%d %H:%M:%S'))
        print("[Next Class]", subject)
        print("[Professor]", professor)
        print("[Time Left]", int(min_left), "minute(s) left\n")
        print("{} minute(s) left until the class starts. The class link opens.".format(int(min_left)))
        print("-------------------------------------")
        pf = system()
        if pf == "Darwin":
            os.system("osascript -e 'display notification \"{} minute(s) left until the class starts. The class link opens.\"'".format(int(min_left)))
            os.system('afplay quite-impressed.m4r')
        webbrowser.open(url)
        sys.exit()
    elif 10 <= min_left < 11:
        print("-------------------------------------")
        print("[Now Datetime]", now.strftime('%Y-%m-%d %H:%M:%S'))
        print("[Next Class]", subject)
        print("[Professor]", professor)
        print("[Time Left]", int(min_left), "minute(s) left\n")
        print("10 minutes left until the class starts.")
        print("-------------------------------------")
        pf = system()
        if pf == "Darwin":
            os.system("osascript -e 'display notification \"10 minutes left until the class starts.\"'")
            os.system('afplay quite-impressed.m4r')
    else:
        print("-------------------------------------")
        print("[Now Datetime]", now.strftime('%Y-%m-%d %H:%M:%S'))
        print("[Next Class]", subject)
        print("[Professor]", professor)
        print("[Time Left]", int(min_left), "minute(s) left\n")
        print("It will be updated once every minute.")
        print("-------------------------------------")

    threading.Timer(2.5, run).start()


run()
```

## **meetings.json**

```json
{
    "mon": {
        "1045": {
            "subject": "Embedded System",
            "professor": "矢ノ倉 公泰",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Experiments in Chemistry",
            "professor": "長野 宗頼",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1440": {
            "subject": "Database A",
            "professor": "眞藤 匡房",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    },
    "tue": {
        "0900": {
            "subject": "Engineering Mathematics",
            "professor": "川城 彦佑",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1045": {
            "subject": "Image Processing",
            "professor": "田中 盛睦",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Computer Operating System",
            "professor": "五明 大振",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1440": {
            "subject": "Control Engineering",
            "professor": "明正 迦具夜",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    },
    "wed": {
        "0900": {
            "subject": "Semiconductor Theory B",
            "professor": "村川 明共",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1045": {
            "subject": "Deep Learning with Neural Networks B",
            "professor": "永本 勤一",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Network Security and Cryptography",
            "professor": "横石 人文",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    },
    "thu": {
        "0900": {
            "subject": "Economics",
            "professor": "中村 翔牙",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1045": {
            "subject": "Business Japanese",
            "professor": "佐本 鳳姫",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Electrical Circuits I",
            "professor": "石館 娃香",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1440": {
            "subject": "Electrical Circuits II",
            "professor": "石館 娃香",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1625": {
            "subject": "Digital Signal Processing",
            "professor": "高山 巧棋",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    },
    "fri": {
        "1045": {
            "subject": "Electromagnetism A",
            "professor": "石館 娃香",
            "id": "78551527256",
            "pw": "Gv7YX5"
        },
        "1255": {
            "subject": "Java Programming",
            "professor": "託麻 佳乃子",
            "id": "78551527256",
            "pw": "Gv7YX5"
        }
    }
}
```

# **5. 결론**

이런거 만들 시간에 공부나 하자.
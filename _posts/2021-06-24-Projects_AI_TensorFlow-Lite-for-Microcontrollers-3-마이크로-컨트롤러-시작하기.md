---
title: AI / TensorFlow Lite for Microcontrollers - 3. 마이크로 컨트롤러 시작하기
author: DEVHEE
date: 2021-06-24 23:01:27 +0900
categories: [Projects, AI]
tags: [project, ai, tensorflow, tensorflow lite, microcontroller, mcu, arduino, sparkfun, google, tinyml]
math: true
image:
    path: /assets/img/posts/2021-06-24-Projects_AI_TensorFlow-Lite-for-Microcontrollers-3-마이크로-컨트롤러-시작하기/preview.png
---

![Preview_2](/assets/img/posts/2021-06-24-Projects_AI_TensorFlow-Lite-for-Microcontrollers-3-마이크로-컨트롤러-시작하기/preview_2.gif)

# **TensorFlow Lite for Microcontrollers**

<iframe id="ark-frame" allowtransparency="true" style="background: #FFFFFF; width:100%; height:220px; border-width:0px; border-color:#959595; border-style:solid;" src="https://drive.google.com/embeddedfolderview?id=1iO6bGLNJFk6tsR4E53owU9Fchr48CWku#list"></iframe>


<div style="border:1px solid; padding:10px; margin-bottom: 20px; width: 100%; text-align: center;">
<b style="font-size: 0.85em;">TensorFlow Lite for Microcontrollers는 <a href="https://www.oreilly.com/library/view/tinyml/9781492052036/" target="_blank">O'Reilly TinyML</a> 교과서 원서를 참고하였습니다.</b><br>
</div>

# **마이크로 컨트롤러 시작하기**

Hello World 예제는 TensorFlow Lite for Microcontrollers 사용의 절대적인 기본 사항을 보여주기 위해 설계되었다.

사인함수를 복제하는 모델을 훈련하고 실행한다. 즉, 단일 숫자를 입력으로 취하고 숫자의 사인 값을 출력한다.

마이크로 컨트롤러에 배포되면 예측을 사용하여 LED를 깜박이거나 애니메이션을 제어한다.

<blockquote style="margin-top: 7%;"><b>Workflow</b></blockquote>
<div class="blockquote-div">
<p>
<b>1. 모델 학습 (Python)</b>: 기기에서 사용할 수 있도록 모델을 학습, 변환 및 최적화한다.
</p>
<b>2. 추론 실행 (C++ 11)</b>: C++ 라이브러리를 사용하여 모델에서 추론을 실행하는 종단간 단위 테스트이다.
</div>

[사전준비](https://kimdonghee.dev/posts/Projects_AI_TensorFlow-Lite-for-Microcontrollers-2-사전준비/){:target="_blank"} 단계는 완료했다는 가정하에 진행한다.

진행하기에 앞서, TensorFlow 라이브러리를 다운로드한다.

```bash
$ git clone https://github.com/tensorflow/tensorflow.git
$ cd tensorflow
```

![Fig. 1](/assets/img/posts/2021-06-24-Projects_AI_TensorFlow-Lite-for-Microcontrollers-3-마이크로-컨트롤러-시작하기/fig_1.png)

# **훈련 - Google Colab**

## **모델 훈련**

훈련을 건너뛰고 예제 코드에 포함된 학습된 모델을 사용할 수 있다. (예제 실행을 위해 굳이 Train 할 필요가 없다.)

Google Colab를 사용하여 자신의 모델을 학습시킬 수 있다.

`xxd`를 통해 `.cc` 파일 형태로 c배열로 훈련된 모델을 만들 수 있다.

### **xxd**

주어진 파일이나 `standard input`으로 들어온 문자들에 대해서 `hex dump`를 만들어준다.

Endian에 관계 없이 파일에 존재하는 순서대로 나온다.

기본 사용법: `xxd [file name]`

# **추론 실행**

TensorFlow Lite for Microcontrollers를 사용하여 추론을 실행하는 방법을 보여주는 단위 테스트인 [`hello_world_test.cc`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/examples/hello_world/hello_world_test.cc){:target="_blank"} 예제를 살펴보자. 모델을 로드하고 추론을 여러번 실행한다.

## **1. 라이브러리 헤더 포함**

TensorFlow Lite for Microcontrollers 라이브러리를 사용하려면 다음 헤더파일을 포함해야한다.

```cpp
#include "tensorflow/lite/micro/all_ops_resolver.h"
#include "tensorflow/lite/micro/micro_error_reporter.h"
#include "tensorflow/lite/micro/micro_interpreter.h"
#include "tensorflow/lite/schema/schema_generated.h"
#include "tensorflow/lite/version.h"
```

[`all_ops_resolver.h`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/all_ops_resolver.h){:target="_blank"}는 인터프리터가 모델을 실행하는데 사용하는 작업을 제공한다.

[`micro_error_reporter.h`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/micro_error_reporter.h){:target="_blank"}는 디버그 정보를 출력한다.

[`micro_interpreter.h`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/micro_interpreter.h){:target="_blank"}에는 모델을로드하고 실행하는 코드가 포함되어 있다.

[`schema_generated.h`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/schema/schema_generated.h){:target="_blank"}에는 TensorFlow Lite [`FlatBuffer`](https://google.github.io/flatbuffers/){:target="_blank"}모델 파일 형식에 대한 스키마가 포함된다.

[`version.h`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/version.h){:target="_blank"}는 TensorFlow Lite 스키마에 대한 버전 관리 정보를 제공한다.

## **2. 모델 헤더 포함**

TensorFlow Lite for Microcontrollers인터프리터는 모델이 C++ 배열로 제공되는 것에 상정한다.

모델은 `model.h` 및 `model.cc` 파일에 정의되어 있다. 헤더는 다음 행에 포함된다.

```cpp
#include "tensorflow/lite/micro/examples/hello_world/model.h"
```

## **3. 단위 테스트 Framework 헤더 포함**

Unit Test를 만들기 위해 다음 줄을 포함하여 Microcontrollers 단위 테스트 Framework용 TensorFlow Lite를 포함한다.

```cpp
#include "tensorflow/lite/micro/testing/micro_test.h"
```

테스트는 다음 매크로를 사용하여 정의된다.

```cpp
TF_LITE_MICRO_TESTS_BEGIN

TF_LITE_MICRO_TEST(LoadModelAndPerformInference) {
  . // add code here
  .
}

TF_LITE_MICRO_TESTS_END
```

## **4. 로깅 설정**

로깅을 설정하려면 `tflite::MicroErrorReporter` 인스턴스에 대한 포인터를 사용하여 `tflite::ErrorReporter` 포인터를 작성한다.

```cpp
tflite::MicroErrorReporter micro_error_reporter;
tflite::ErrorReporter* error_reporter = &micro_error_reporter;
```

이 변수는 인터프리터에 넘겨 로그를 쓸 수 있다. 마이크로 컨트롤러에는 대부분의 경우 로깅을 위한 다양한 메커니즘이 있기 때문에 `tflite::MicroErrorReporter` 구현은 특정 디바이스용으로 커스터마이즈 하도록 설계되어 있다.

## **5. 모델로드**

다음 코드에서, `model.h`에 선언된 `g_model`이라는 문자 배열의 데이터를 사용하여 모델을 인스턴스화한다. 그런 다음 모델의 스키마 버전이 사용 중인 버전과 호환되는지 확인한다.

```cpp
const tflite::Model* model = ::tflite::GetModel(g_model);
if (model->version() != TFLITE_SCHEMA_VERSION) {
  TF_LITE_REPORT_ERROR(error_reporter,
      "Model provided is schema version %d not equal "
      "to supported version %d.\n",
      model->version(), TFLITE_SCHEMA_VERSION);
}
```

## **6. 인터프리터 인스턴스화**

[`AllOpsResolver`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/all_ops_resolver.h){:target="_blank"} 인스턴스가 선언된다. 이것은 인터프리터가 모델에서 사용하는 작업에 액세스하는데에 사용된다.

```cpp
tflite::AllOpsResolver resolver;
```

`AllOpsResolver`는 많은 메모리를 사용하는 TensorFlowLite for Microcontroller에서 사용가능한 모든 작업을 로드한다. 특정 모델에서는 이러한 작업의 하위 집합만 사용하므로 실제 애플리케이션에서는 필요한 작업만 로드하는 것이 좋다.

이 작업은 다른 클래스 `MicroMutableOpResolver`를 사용하여 수행된다. Micro speech 예제의 [`micro_speech_test.cc`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/examples/micro_speech/micro_speech_test.cc){:target="_blank"}에서 이 기능을 사용하는 방법을 볼 수 있다.

## **7. 메모리 할당**

입력, 출력 및 중간 배열에 대해 일정량의 메모리를 미리 할당해야한다.

이것은 `tensor_arena_size` 크기의 `uint8_t `배열로 제공된다.

```cpp
const int tensor_arena_size = 2 * 1024;
uint8_t tensor_arena[tensor_arena_size];
```

필요한 크기는 사용중인 모델에 따라 다르며 실험을 통해 결정해야 할 수도 있다.

## **8. 인터프리터 인스턴스화**

`tflite::MicroInterpreter` 인스턴스를 만들고 앞에서 만든 변수를 전달한다.

```cpp
tflite::MicroInterpreter interpreter(model, resolver, tensor_arena, tensor_arena_size, error_reporter);
```

## **9. 텐서 할당**

인터프리터에 모델의 텐서에 대해 `tensor_arena`에서 메모리를 할당하고 지시한다.

```cpp
interpreter.AllocateTensors();
```

## **10. 입력 shape 검증**

₩MicroInterpreter₩ 인스턴스는 `.input(0)`을 호출하여 모델의 입력 텐서에 대한 포인터를 제공할 수 있다. 여기서 `0`은 첫번째 유일의 입력 텐서를 나타낸다.

```cpp
// Obtain a pointer to the model's input tensor
TfLiteTensor* input = interpreter.input(0);
```

그런 다음 텐서를 검사하여 shape와 type가 기댓값인지 확인한다.

```cpp
// Make sure the input has the properties we expect
TF_LITE_MICRO_EXPECT_NE(nullptr, input);
// The property "dims" tells us the tensor's shape. It has one element for
// each dimension. Our input is a 2D tensor containing 1 element, so "dims"
// should have size 2.
TF_LITE_MICRO_EXPECT_EQ(2, input->dims->size);
// The value of each element gives the length of the corresponding tensor.
// We should expect two single element tensors (one is contained within the
// other).
TF_LITE_MICRO_EXPECT_EQ(1, input->dims->data[0]);
TF_LITE_MICRO_EXPECT_EQ(1, input->dims->data[1]);
// The input is a 32 bit floating point value
TF_LITE_MICRO_EXPECT_EQ(kTfLiteFloat32, input->type);
```

enum 값 `kTfLiteFloat32`는 TensorFlowLite 데이터 유형 중 하나를 참조하는 것이며 [`common.h`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/c/common.h){:target="_blank"}로 정의된다.

## **11. 입력 값 제공**

모델에 입력을 제공하기 위해 입력 텐서의 내용을 다음과 같이 설정한다.

```cpp
input->data.f[0] = 0.;
```

이 경우 `0`을 나타내는 부동 소수점 값을 입력한다.

## **12. 모델 실행 (Inference, 추론)**

모델을 실행하려면 `tflite::MicroInterpreter` 인스턴스로 `Invoke()`를 호출하면 된다.

```cpp
TfLiteStatus invoke_status = interpreter.Invoke();
if (invoke_status != kTfLiteOk) {
  TF_LITE_REPORT_ERROR(error_reporter, "Invoke failed\n");
}
```

반환값 `TfLiteStatus`를 확인하여 실행에 성공했는지 확인할 수 있다. [`common.h`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/c/common.h){:target="_blank"}에 정의된 `TfLiteStatus`의 가능한 값은 `kTfLiteOk`및 `kTfLiteError`이다.

다음 코드는 값이 `kTfLiteOk`이며, 이는 추론이 성공적으로 실행되었음을 의미한다.

`kTfLiteOk`의 맨 앞글자 `k`는 `invoke`를 의미한다.

```cpp
TF_LITE_MICRO_EXPECT_EQ(kTfLiteOk, invoke_status);
```

## **13. 출력 얻기**

모델의 출력 텐서는 `tflite::MicroInterpreter`에서 `output(0)`를 호출하여 얻을 수 있으며, 여기서 `0`은 첫번째 유일한 출력 텐서를 나타낸다.

다음 예시에서 모델의 출력은 2D 텐서 내에 포함된 단일 부동 소수점 값이다.

```cpp
TfLiteTensor* output = interpreter.output(0);
TF_LITE_MICRO_EXPECT_EQ(2, output->dims->size);
TF_LITE_MICRO_EXPECT_EQ(1, input->dims->data[0]);
TF_LITE_MICRO_EXPECT_EQ(1, input->dims->data[1]);
TF_LITE_MICRO_EXPECT_EQ(kTfLiteFloat32, output->type);
```

출력 텐서에서 직접 값을 읽고 이것이 우리가 기대하는 것이라고 해석할 수 있다.

```cpp
// Obtain the output value from the tensor
float value = output->data.f[0];
// Check that the output value is within 0.05 of the expected value
TF_LITE_MICRO_EXPECT_NEAR(0., value, 0.05);
```

## **14. 추론 다시 실행**

코드의 나머지 부분은 추론을 몇 번 더 실행한다. 각 경우에 입력 텐서에 값을 할당하고, 인터프리터를 호출하고, 출력 텐서에서 결과를 읽는다.

```cpp
input->data.f[0] = 1.;
interpreter.Invoke();
value = output->data.f[0];
TF_LITE_MICRO_EXPECT_NEAR(0.841, value, 0.05);

input->data.f[0] = 3.;
interpreter.Invoke();
value = output->data.f[0];
TF_LITE_MICRO_EXPECT_NEAR(0.141, value, 0.05);

input->data.f[0] = 5.;
interpreter.Invoke();
value = output->data.f[0];
TF_LITE_MICRO_EXPECT_NEAR(-0.959, value, 0.05);
```

## **15. 애플리케이션 코드 읽기**

이 장치 테스트를 완료하면 [`main_functions.cc`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/examples/hello_world/main_functions.cc){:target="_blank"}에 있는 예제의 응용 프로그램 코드를 이해할 수 있다. 유사한 프로세스를 따르지만 실행된 추론의 수에 따라 입력 값을 생성하고 사용자에게 모델의 출력을 표시하는 장치별 함수를 호출한다.
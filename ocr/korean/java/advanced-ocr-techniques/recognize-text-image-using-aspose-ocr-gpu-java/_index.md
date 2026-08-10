---
category: general
date: 2026-02-17
description: Java에서 Aspose OCR GPU 지원을 사용하여 텍스트 이미지를 빠르게 인식합니다. 이미지에서 텍스트를 추출하고 최적의
  성능을 위해 GPU 디바이스 ID를 설정하는 방법을 배워보세요.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: ko
og_description: Java에서 Aspose OCR GPU 지원을 사용하여 텍스트 이미지를 빠르게 인식합니다. 이 가이드는 이미지에서 텍스트를
  추출하고 GPU 디바이스 ID를 설정하는 방법을 보여줍니다.
og_title: Aspose OCR GPU를 사용하여 텍스트 이미지 인식 – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: Aspose OCR GPU를 사용한 텍스트 이미지 인식 – Java
url: /ko/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

Check for any markdown links: none.

Check for any images: none.

All good.

Now produce final output with same structure.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU를 사용한 텍스트 이미지 인식 – Java

Java 애플리케이션에서 **텍스트 이미지 인식**이 필요했지만 CPU가 대용량 파일에 버벅였던 적이 있나요? 당신만 그런 것이 아닙니다—많은 개발자들이 고해상도 스캔을 처리할 때 같은 문제에 부딪힙니다. 좋은 소식은? Aspose OCR은 GPU에서 **이미지에서 텍스트 추출**을 가능하게 하여 처리 시간을 크게 단축합니다.  

이 튜토리얼에서는 라이선스를 설정하고 GPU 가속을 활성화하며, 다중 그래픽 카드가 있을 때 **gpu device id 설정**하는 방법을 정확히 보여주는 완전한 실행 가능한 예제를 단계별로 살펴보겠습니다. 끝까지 따라오면 인식된 텍스트를 콘솔에 출력하는 독립 실행형 프로그램을 얻게 됩니다—추가 단계가 필요 없습니다.

## 필요 사항

- **Java 17** 또는 그 이상 (API는 Java 8+와 호환되지만 최신 LTS가 더 나은 성능을 제공합니다).  
- **Aspose OCR for Java** 라이브러리 (Aspose 웹사이트에서 JAR를 다운로드).  
- 유효한 **Aspose OCR 라이선스 파일** (`Aspose.OCR.lic`). 무료 체험판도 동작하지만 GPU 기능은 라이선스 버전에서만 사용할 수 있습니다.  
- 명확하고 기계가 읽을 수 있는 텍스트가 포함된 이미지 파일 (`sample-image.png`).  
- GPU가 활성화된 환경 (NVIDIA CUDA 호환 카드가 가장 좋습니다).  

위 항목 중 익숙하지 않은 것이 있더라도 걱정하지 마세요—각 항목은 진행하면서 설명됩니다.

## 단계 1: 프로젝트에 Aspose OCR 추가

먼저, Aspose OCR JAR를 클래스패스에 포함시킵니다. Maven을 사용한다면 `pom.xml`에 다음 의존성을 추가하세요:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Gradle을 사용하는 경우는 다음과 같습니다:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

수동으로 진행하고 싶다면 JAR를 `libs/` 폴더에 넣고 IDE의 모듈 경로에 추가하세요.

> **Pro tip:** 버전 번호를 라이브러리 릴리스 노트와 맞추세요; 최신 버전은 종종 GPU 처리 성능 개선을 포함합니다.

## 단계 2: Aspose OCR 라이선스 로드 (GPU 사용에 필요)

라이선스가 없으면 `setEnableGpu(true)` 호출이 조용히 CPU 모드로 전환됩니다. `main` 시작 부분에서 라이선스를 로드하세요:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

`YOUR_DIRECTORY`를 `.lic` 파일을 저장한 절대 경로나 상대 경로로 교체하세요. 경로가 잘못되면 Aspose가 `FileNotFoundException`을 발생시키므로 철자를 다시 확인하십시오.

## 단계 3: OCR 엔진 생성 및 GPU 가속 활성화

이제 `OcrEngine`을 인스턴스화하고 GPU 사용을 지정합니다. `setGpuDeviceId` 메서드를 사용하면 여러 카드가 있을 때 특정 카드를 선택할 수 있습니다.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

디바이스 ID를 설정하는 이유는 무엇일까요? 다중 GPU 서버에서는 한 카드를 이미지 전처리에, 다른 카드를 OCR에 할당할 수 있습니다. ID를 설정하면 올바른 하드웨어가 작업을 수행합니다.

## 단계 4: 입력 이미지 준비

Aspose OCR은 다양한 포맷(PNG, JPG, BMP, TIFF)을 지원합니다. 파일을 `OcrInput` 객체에 래핑하세요:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

스트림(예: 업로드된 파일)을 처리해야 한다면 `ocrInput.add(InputStream)`을 사용하세요.

## 단계 5: 인식 프로세스 실행 및 결과 가져오기

`recognize` 메서드는 평문 텍스트, 신뢰도 점수, 필요에 따라 레이아웃 정보까지 포함하는 `OcrResult`를 반환합니다.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

콘솔에는 다음과 같은 내용이 표시됩니다:

```
Recognized text:
Hello, world!
This is a sample image.
```

이미지가 흐리거나 언어가 지원되지 않으면 결과가 비어 있을 수 있습니다. 이 경우 `ocrResult.getConfidence()` 값(0‑100)을 확인하여 전처리 후 재시도할지 결정하세요.

## 전체 실행 가능한 예제

모든 코드를 합치면 IDE에 복사‑붙여넣기 할 수 있는 단일 Java 클래스를 얻을 수 있습니다:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Expected output:** 콘솔에 `sample-image.png`에 표시된 정확한 텍스트가 출력됩니다. GPU가 활성화된 경우 일반적인 300 dpi 스캔에서 처리 시간이 몇 초(CPU)에서 1초 미만으로 크게 감소함을 확인할 수 있습니다.

## 일반적인 질문 및 예외 상황

### 헤드리스 서버에서도 작동하나요?

예. GPU 드라이버가 설치되어 있어야 하지만 디스플레이는 필요하지 않습니다. 시스템 `PATH`에 `CUDA` 툴킷(또는 해당 GPU에 맞는 툴킷)이 포함되어 있는지 확인하세요.

### GPU가 여러 개 있고 GPU 1을 사용하고 싶다면?

디바이스 ID를 변경하세요:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### 다른 언어의 이미지에서 텍스트를 추출하려면?

`recognize` 호출 전에 언어를 설정하세요:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose는 30개 이상의 언어를 지원합니다; 전체 목록은 API 문서를 참고하세요.

### 이미지에 여러 페이지가 포함되어 있으면(예: PDF를 이미지로 변환한 경우) 어떻게 하나요?

각 페이지마다 별도의 `OcrInput` 항목을 만들거나 파일을 순회하세요:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

엔진은 결과를 순서대로 연결합니다.

### 낮은 신뢰도 결과를 어떻게 처리하나요?

신뢰도 점수를 확인하세요:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

일반적인 전처리 단계로는 이진화, 노이즈 감소, 300 dpi로 리사이징 등이 있습니다.

## 성능 팁

- **Batch processing:** 여러 이미지를 하나의 `OcrInput`에 추가하면 GPU 컨텍스트를 반복 초기화하는 오버헤드를 줄일 수 있습니다.  
- **Warm‑up:** JVM 시작 후 더미 인식을 한 번 실행하세요; 첫 호출은 드라이버 초기화 지연을 발생시킵니다.  
- **Memory management:** 사용이 끝난 큰 `OcrInput` 객체(`ocrInput.clear()`)를 해제하여 GPU 메모리를 확보하세요.  

## 결론

이제 Java에서 Aspose OCR의 GPU 엔진을 사용해 **텍스트 이미지 인식**을 효율적으로 수행하고, 지원되는 모든 언어에서 **이미지에서 텍스트 추출**하는 방법, 그리고 다중 그래픽 카드를 사용할 때 **gpu device id 설정**하는 방법을 알게 되었습니다. 위의 완전한 실행 가능한 코드는 바로 사용할 수 있으니 라이선스와 이미지 경로만 교체하면 됩니다.

다음 단계가 준비되셨나요? 스캔한 PDF 폴더를 처리해 보거나 다양한 `setLanguage` 옵션을 실험하고, OCR을 머신러닝 모델과 결합해 후처리해 보세요. 가능성은 무궁무진하며 GPU 가속을 통한 성능 향상으로 대규모 프로젝트도 실현 가능해집니다.

코딩 즐겁게 하시고, 문제가 발생하면 언제든 댓글을 남겨 주세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
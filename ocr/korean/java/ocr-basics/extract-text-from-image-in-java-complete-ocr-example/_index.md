---
category: general
date: 2026-02-19
description: Java OCR을 사용하여 이미지에서 텍스트를 추출합니다. 몇 단계만으로 OCR용 이미지를 로드하고 청구서 파일에서 텍스트를
  추출하는 Java OCR 예제를 배워보세요.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: ko
og_description: Java OCR을 사용하여 이미지에서 텍스트를 추출합니다. 이 가이드는 OCR을 위해 이미지를 로드하고 간단한 Java
  OCR 예제로 청구서에서 텍스트를 추출하는 방법을 보여줍니다.
og_title: Java에서 이미지 텍스트 추출 – 완전한 OCR 예제
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Java에서 이미지에서 텍스트 추출 – 완전한 OCR 예제
url: /ko/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 이미지에서 텍스트 추출 – 완전 OCR 예제

이미지에서 **텍스트를 추출**해야 할 때, 어떤 라이브러리를 선택해야 할지 몰라 고민한 적 있나요? 혼자가 아닙니다—많은 개발자들이 청구서 처리 자동화나 검색 가능한 아카이브 구축 시 이 문제에 부딪힙니다. 좋은 소식은? 몇 줄의 Java 코드만으로 OCR용 이미지를 로드하고, 관심 영역을 정의하며, 필요한 정확한 텍스트를 추출할 수 있다는 것입니다.  

이 튜토리얼에서는 Aspose.OCR을 사용하여 **java ocr example**을 단계별로 살펴보며, **load image for OCR** 방법, ROI 설정, 그리고 **extract text from invoice** 파일을 추출하는 과정을 보여드립니다. 끝까지 따라오시면 어떤 Java 프로젝트에도 넣어 실행할 수 있는 프로그램을 얻게 됩니다.

## 배울 내용

- `OcrEngine` 인스턴스를 생성하는 방법과 그 중요성.
- Aspose의 `ImageStream`을 사용한 **load image for OCR**의 올바른 방법.
- **region of interest (ROI)** 설정 방법으로, 청구서 금액이 포함된 이미지 부분만 처리하도록 합니다.
- 인식된 텍스트를 추출하고 콘솔에 출력하기.
- 일반적인 함정(예: 잘못된 사각형 좌표)과 빠른 해결 방법.

**필수 조건**

- Java 8 이상이 설치되어 있어야 합니다.
- Aspose.OCR 라이브러리(`com.aspose:aspose-ocr`)를 가져오기 위한 Maven 또는 Gradle.
- 알려진 디렉터리에 위치한 샘플 청구서 이미지(`invoice.png`).

다 준비되셨나요? 좋습니다—시작해 봅시다.

![Extract text from image using Java OCR](/images/extract-text-from-image-java.png "extract text from image example")

## 이미지에서 텍스트 추출 – 단계별 Java OCR 예제

아래는 전체 소스 코드입니다. `RoiOcrExample.java`에 복사‑붙여넣기하고 바로 실행해 보세요.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### 각 단계가 중요한 이유

1. **Creating the OCR engine** – 엔진이 없으면 이미지 처리 컨텍스트가 없습니다. 이 객체를 통해 나중에 다국어 지원이 필요할 경우 언어 팩을 조정할 수 있습니다.  
2. **Loading the image** – `ImageStream.fromFile`은 파일 형식을 추상화하여 엔진이 바이트를 올바르게 읽도록 합니다. 이를 생략하면 `NullPointerException`이 발생합니다.  
3. **Setting the ROI** – 전체 페이지를 처리하면 비효율적입니다. 사각형을 청구서 총액 영역으로 좁히면 인식 속도가 빨라지고 잡음이 감소합니다.  
4. **Calling `recognize()`** – 바로 여기서 마법이 일어납니다. 이 메서드는 ROI에 대해 OCR 알고리즘을 실행하고 결과 객체를 반환합니다.  
5. **Printing the output** – 실제 프로젝트에서는 텍스트를 데이터베이스에 저장할 가능성이 높지만, `System.out.println`은 빠른 데모에 적합합니다.

## OCR용 이미지 로드

경로를 절대 경로나 상대 경로로 지정해야 하는지 궁금하다면, 두 방식 모두 작동합니다—단지 Java 프로세스가 파일을 읽을 수 있도록 하면 됩니다. Windows에서는 백슬래시를 이스케이프해야 합니다(`C:\\images\\invoice.png`) 혹은 슬래시(`/`)를 사용할 수도 있습니다(`C:/images/invoice.png`).  

**Pro tip:** 루프에서 많은 청구서를 처리한다면 동일한 `OcrEngine` 인스턴스를 재사용하세요; 내부 리소스를 캐시하여 처리량을 향상시킵니다.

## 관심 영역 (ROI) 정의

올바른 사각형을 선택하는 것은 약간의 시행착오가 필요할 수 있습니다. 좌표를 찾는 편리한 방법은 이미지를 GIMP나 Paint.NET 같은 그래픽 편집기에서 열고 영역 위에 마우스를 올리는 것입니다—상태 표시줄에 X/Y 값이 표시됩니다.  

예외 상황: 일부 청구서는 레이아웃이 가변적입니다. 이 경우 전체 이미지를 빠르게 사전 스캔하여 “Total:”과 같은 키워드를 정규식으로 찾은 뒤, ROI를 동적으로 조정할 수 있습니다.

## OCR 수행 및 텍스트 가져오기

`recognize()` 호출은 동기식이며, 엔진이 완료될 때까지 스레드가 차단됩니다. 대량 배치 처리 시 스레드 풀을 생성해 이미지를 병렬 처리할 수 있습니다. 단, 각 스레드마다 별도의 `OcrEngine` 인스턴스가 필요합니다; 이 객체는 스레드 안전하지 않습니다.

## 실행 및 출력 확인

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

You should see something like:

```
ROI text: $1,254.00
```

출력이 깨져 보인다면 ROI 좌표를 다시 확인하고 이미지 품질이 높은지 확인하세요(300 dpi 이상이 가장 좋습니다).  

### 일반적인 함정 및 해결 방법

| 증상 | 가능한 원인 | 해결 방법 |
|---------|--------------|-----|
| 빈 문자열 | ROI가 이미지 범위 밖에 있음 | 이미지 크기에 맞게 사각형 값을 확인 |
| 잘못 인식된 단어 | 해상도 낮음 | 고해상도 소스를 사용하거나 이미지 전처리(예: 이진화)를 적용 |
| `java.lang.NoClassDefFoundError` | 클래스패스에 Aspose JAR 누락 | `aspose-ocr.jar`를 `-cp`에 추가하거나 Maven/Gradle 의존성 관리 사용 |

## 결론

이제 Java에서 간결한 **java ocr example**을 사용해 **이미지에서 텍스트를 추출**하는 방법을 알게 되었습니다. 이미지를 올바르게 로드하고, 집중된 ROI를 정의하며, `recognize()`를 호출함으로써 청구서 파일에서 텍스트를 안정적으로 **추출**하고 해당 데이터를 하위 시스템에 전달할 수 있습니다.

다음은? ROI를 다른 필드(날짜, 공급업체명)로 교체해 보거나, 다국어 청구서를 위해 언어 팩을 실험하거나, OCR 단계를 Spring Boot 마이크로서비스에 통합해 보세요. 동일한 패턴은 영수증, 여권 또는 정밀 텍스트 추출이 필요한 모든 문서에 적용됩니다.

이 솔루션을 확장하거나 노이즈가 많은 스캔을 처리하는 방법에 대한 질문이 있으면 아래에 댓글을 남겨 주세요—코딩 즐겁게!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
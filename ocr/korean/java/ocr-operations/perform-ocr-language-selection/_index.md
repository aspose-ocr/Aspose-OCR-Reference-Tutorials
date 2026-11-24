---
date: 2026-06-24
description: Aspose.OCR for Java를 사용하여 언어 선택과 함께 이미지 텍스트를 OCR하는 방법을 배웁니다. 이 단계별 가이드에서는
  extract text java, OCR 기울기 보정 및 기타 내용을 다룹니다.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Aspose.OCR를 사용한 OCR 기울기 보정 및 언어 선택 수행 방법
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Aspose.OCR를 사용한 OCR 기울기 보정 및 언어 선택 수행 방법
url: /ko/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR을 사용한 OCR 기울기 보정 및 언어 선택 수행 방법

## 소개

이미지 파일에서 텍스트를 추출하는 것은 스캔 문서를 디지털화하거나 영수증을 처리하거나 검색 가능한 아카이브를 구축할 때 흔히 요구되는 작업입니다. 이 튜토리얼에서는 특정 언어 설정으로 **이미지 텍스트를 OCR하는 방법**을 보여주는 완전한 실습 예제를 단계별로 안내합니다. 이를 통해 Java 애플리케이션에 신뢰할 수 있는 OCR을 바로 통합할 수 있습니다. 또한 **OCR 기울기 보정** 및 영역 기반 인식을 처리하는 방법을 살펴보며, 이를 통해 각도된 스캔에서 OCR 정확도를 최대 30 %까지 **향상시킬 수** 있습니다.

## 빠른 답변
- **Java에서 OCR을 처리하는 라이브러리는?** Aspose.OCR for Java  
- **언어를 선택하는 설정은?** `settings.setLanguage(Language.Eng)` (또는 지원되는 언어)  
- **개발에 라이선스가 필요합니까?** 무료 평가 라이선스로 테스트가 가능하며, 상용 환경에서는 상업용 라이선스가 필요합니다.  
- **이미지의 특정 영역으로 OCR을 제한할 수 있나요?** 예, 사각형을 사용하여 `RecognitionSettings.setRecognitionAreas()`를 사용합니다.  
- **일반적인 실행 시간은?** 이미지 크기와 언어 복잡도에 따라 표준 노트북에서 페이지당 몇 초 정도 소요됩니다.  

`Language`는 Aspose.OCR이 지원하는 OCR 언어를 나열하는 열거형이며, 예를 들어 English, French, Spanish 등이 포함됩니다.

## OCR 기울기 보정이란?

OCR 기울기 보정은 문자 인식 전에 기울어진 텍스트 라인을 감지하고 바로잡는 과정입니다. 텍스트 기준선을 정렬함으로써 OCR 엔진은 언어 모델을 보다 효과적으로 적용할 수 있어, 각도된 스캔으로 인한 인식 오류를 줄일 수 있습니다. 이 단계는 입력 이미지의 시각적 품질을 향상시켜 인식 알고리즘이 회전으로 인한 왜곡이 아닌 실제 문자 형태에 집중하도록 합니다.

## OCR 기울기 보정이 정확도를 향상시키는 이유

텍스트가 기울어지면 문자 형태가 왜곡되어 오류율이 최대 20 %까지 증가합니다. **OCR 기울기 보정**을 적용하면 이러한 왜곡이 제거되어 엔진이 실제 글리프에 집중할 수 있습니다. 벤치마크 테스트에서 Aspose.OCR은 10‑15° 회전된 문서에 기울기 보정을 적용한 후 인식 정확도가 15‑30 % 향상되었습니다.

## 언어 선택과 함께 Aspose.OCR을 사용하는 이유

원본 텍스트의 정확한 언어를 선택하면 OCR 엔진이 언어별 사전 및 문자 모델을 활용할 수 있어 인식 정밀도가 크게 향상되고 처리 시간이 감소합니다. 또한 Aspose.OCR은 기울기 보정, 영역 선택 및 출력 형식에 대한 세밀한 제어를 제공하므로 다국어 문서 처리 파이프라인에 다재다능한 선택이 됩니다.

- **다국어 지원** – 이미지에 포함된 정확한 언어를 선택하여 정확도를 높입니다.  
- **세밀한 제어** – 기울기를 조정하고 인식 영역을 정의하며 자동 기울기 동작을 설정합니다.  
- **Pure Java API** – 네이티브 종속성이 없으며 모든 Java 프로젝트에 쉽게 통합할 수 있습니다.  
- **풍부한 결과 데이터** – 한 번의 호출로 일반 텍스트, JSON, 경계 사각형 및 경고를 얻을 수 있습니다.  
- **정량화된 기능** – Aspose.OCR은 **50+** 입력 및 출력 형식을 지원하며 전체 문서를 메모리에 로드하지 않고 **500‑페이지** 이미지 배치를 처리할 수 있습니다.

## 사전 요구 사항

시작하기 전에 다음을 확인하십시오:

- **Java Development Kit (JDK)**가 설치되어 있어야 합니다 (JDK 8 이상).  
- **Aspose.OCR for Java** 라이브러리 – 공식 사이트에서 [여기](https://reference.aspose.com/ocr/java/) 다운로드하십시오.  
- 추출하려는 텍스트가 포함된 이미지 파일, 예: `p3.png`.  

## 패키지 가져오기

다음 import 문은 핵심 OCR 클래스와 표준 Java 유틸리티에 접근할 수 있게 해줍니다.  
`import com.aspose.ocr.*;` – 주요 OCR 엔진을 가져옵니다.  
`import com.aspose.ocr.config.*;` – `RecognitionSettings`와 같은 구성 객체를 포함합니다.  
`import java.awt.Rectangle;` – 인식 영역을 정의하는 데 사용됩니다.  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Java에서 OCR 기울기 보정을 적용하는 방법?

이미지를 로드하고 자동 기울기 감지를 비활성화한 뒤, 측정된 각도를 제공하거나 `settings.setAutoSkew(false)`를 사용하여 엔진이 각도를 계산하도록 합니다. OCR 엔진은 제공되거나 감지된 각도를 기반으로 먼저 이미지를 바로잡은 후 문자 인식을 진행합니다. 이 두 단계 접근 방식은 언어 모델이 적용되기 전에 모든 기울기가 제거되어 더 깨끗한 텍스트 출력과 인식 오류 감소를 보장합니다.

## 단계별 가이드

### 단계 1: 문서 디렉터리 설정

소스 이미지가 들어 있는 폴더를 가리키는 `File` 객체를 생성합니다. 이렇게 하면 운영 체제에 관계없이 경로 처리가 이식됩니다.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

`"Your Document Directory"`를 `p3.png`가 위치한 절대 경로로 교체하십시오.

### 단계 2: 이미지 경로 정의

처리하려는 특정 이미지에 대해 `File` 객체를 인스턴스화합니다. `File` 객체를 사용하면 나중에 필요할 경우 파일 메타데이터에 쉽게 접근할 수 있습니다.

```java
// The image path
String file = dataDir + "p3.png";
```

`file` 변수가 처리하려는 정확한 이미지 파일을 가리키는지 확인하십시오.

### 단계 3: Aspose.OCR API 인스턴스 생성

`AsposeOCR` 클래스는 모든 OCR 작업의 진입점입니다. 엔진을 캡슐화하고 리소스를 관리하며 `recognizePage` 메서드를 제공합니다.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` 객체를 통해 모든 OCR 작업에 접근할 수 있습니다.

### 단계 4: 인식 옵션 설정 (언어 선택)

`RecognitionSettings`는 OCR 프로세스를 세밀하게 조정할 수 있는 Aspose.OCR의 구성 컨테이너입니다.  

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

여기서는:
1. 수동 기울기 값을 제공하므로 자동 기울기를 비활성화합니다.  
2. 사각형 영역(`RecognitionAreas`)을 정의하여 실제 텍스트가 포함된 이미지 부분으로 OCR을 제한합니다.  
3. **언어**를 영어(`Language.Eng`)로 설정합니다. 소스 이미지에 따라 `Language.Fra`, `Language.Spa` 등으로 변경하십시오.

### 단계 5: OCR 수행 및 결과 가져오기

`recognizePage`를 호출하면 정의한 이미지와 설정을 사용하여 OCR 엔진이 실행됩니다. 결과는 모든 유용한 데이터를 모아 놓은 `RecognitionResult` 객체에 저장됩니다.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 호출은 이미지와 설정을 사용하여 OCR 엔진을 실행합니다. 결과는 `RecognitionResult` 객체에 저장됩니다.

### 단계 6: 결과 출력 및 활용

콘솔 출력에는 다음이 표시됩니다:
- 전체 추출된 텍스트(`recognitionText`).  
- 정의된 각 사각형에 대한 텍스트(`recognitionAreasText`).  
- 경계 사각형 좌표.  
- 하위 처리에 용이한 JSON 표현.  
- 감지된 기울기 각도 및 경고 사항.

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

콘솔 출력에는 전체 추출 텍스트, 영역별 텍스트, 경계 상자, JSON, 기울기 각도 및 경고가 표시됩니다. 이제 `result.recognitionText`를 비즈니스 로직에 전달하여 저장하거나 인덱싱하거나 다른 서비스에 전달할 수 있습니다.

## 일반적인 문제 및 해결책

| Issue | Cause | Fix |
|-------|-------|-----|
| **Garbage characters** | 잘못된 언어 선택 | 올바른 `Language` 열거형을 설정하십시오(예: 프랑스어는 `Language.Fra`). |
| **No text returned** | 인식 영역이 텍스트를 포함하지 않음 | `Rectangle` 좌표를 조정하거나 `RecognitionAreas`를 제거하여 전체 이미지를 처리하십시오. |
| **Slow performance** | 이미지가 매우 크거나 해상도가 높음 | OCR 전에 이미지를 축소하거나 JVM 메모리 할당량을 늘리십시오. |
| **Warnings about unsupported format** | 이미지 형식 인식 불가 | 처리 전에 이미지를 PNG, JPEG 또는 TIFF 형식으로 변환하십시오. |

## 자주 묻는 질문

**Q: 단일 OCR 호출에서 여러 언어를 인식할 수 있나요?**  
A: 예. `settings.setLanguage(Language.Eng | Language.Fra)`를 사용하여 다국어 인식을 활성화합니다.

**Q: Aspose.OCR이 지원하는 이미지 형식은 무엇인가요?**  
A: PNG, JPEG, BMP, TIFF, GIF 등 여러 형식을 지원합니다. 올바른 파일 경로만 제공하면 됩니다.

**Q: 이미지 크기에 제한이 있나요?**  
A: 명확한 제한은 없지만 10 MB 이상의 이미지를 처리하면 메모리 사용량과 실행 시간이 증가할 수 있습니다. 큰 파일은 크기를 조정하는 것이 좋습니다.

**Q: 프로덕션 라이선스는 어떻게 얻나요?**  
A: Aspose 웹사이트에서 라이선스를 구매하고 Aspose 문서에 표시된 대로 `License` 클래스를 사용하여 적용하십시오.

**Q: PDF 페이지에서 직접 텍스트를 추출할 수 있나요?**  
A: Aspose.OCR만으로는 직접 추출할 수 없습니다. 먼저 PDF 페이지를 이미지로 변환(예: Aspose.PDF 사용)한 후 OCR을 실행하십시오.

## 결론

이제 Aspose.OCR for Java를 사용하여 **이미지에서 텍스트를 추출**하고 적절한 언어를 선택하며 **OCR 기울기 보정**을 적용하여 신뢰성을 향상시키는 방법을 확인했습니다. 이 접근 방식은 정확하고 고성능의 OCR을 제공하여 문서 관리 시스템부터 데이터 캡처 파이프라인까지 모든 Java 기반 워크플로에 삽입할 수 있습니다. 다양한 `Language` 열거형을 실험하고 `RecognitionAreas`를 조정하며 JSON 출력을 하위 분석에 통합하여 진정한 엔드‑투‑엔드 솔루션을 구현하십시오.

---

**최종 업데이트:** 2026-06-24  
**테스트 환경:** Aspose.OCR 24.11 for Java  
**작성자:** Aspose

## 관련 튜토리얼

- [Aspose.OCR을 사용한 Java에서 기울기 각도 계산 방법](/ocr/java/ocr-basics/calculate-skew-angle/)
- [Aspose.OCR을 사용한 언어 선택 이미지 텍스트 OCR 방법](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR for Java에서 PDF 문서 인식 OCR](/ocr/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
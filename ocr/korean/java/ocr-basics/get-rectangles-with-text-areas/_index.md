---
date: 2026-06-19
description: Java에서 이미지를 텍스트로 변환하고, 이미지에서 단락을 추출하며, Aspose OCR Java library를 사용하여
  텍스트 영역 사각형을 검색하는 방법을 배웁니다.
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – 이미지에서 텍스트를 인식하고 텍스트 영역 사각형을 검색
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – 이미지를 텍스트로 변환하고 텍스트 영역 사각형을 검색
url: /ko/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 추출 Java – 이미지에서 텍스트 변환 및 텍스트 영역 사각형 가져오기

## 소개

Java 애플리케이션에서 **convert image to text**가 필요하다면, Aspose.OCR for Java는 빠르고 정확한 솔루션을 제공합니다. 이 튜토리얼에서는 이미지에서 단락을 추출하고 각 텍스트 영역에 대한 경계 사각형을 얻은 다음 해당 좌표를 콘솔에 출력하는 정확한 단계를 안내합니다. 끝까지 읽으면 이 접근 방식이 왜 작동하는지, 라이브러리를 어떻게 통합하는지, 그리고 자체 사용 사례에 맞게 어디에서 확장할 수 있는지 이해하게 됩니다.

## 빠른 답변
`AreasType`은 텍스트 세분화 수준(단어, 줄, 단락)을 지정하는 열거형입니다.

- **“recognize text from image”가 무엇을 의미하나요?** 그림의 시각적 문자를 편집 가능한 문자열 데이터로 변환하는 것을 의미합니다.  
- **Java에서 이를 처리하는 라이브러리는 무엇인가요?** Aspose.OCR for Java.  
- **개발에 라이선스가 필요합니까?** 테스트용 임시 라이선스를 사용할 수 있으며, 프로덕션에는 정식 라이선스가 필요합니다.  
- **단어 대신 단락을 추출할 수 있나요?** 예 – `AreasType.PARAGRAPHS`를 사용하여 단락 수준 사각형을 얻을 수 있습니다.  
- **코드가 Java 11+와 호환됩니까?** 물론입니다, API는 Java 11 및 이후 버전에서 작동합니다.

## Aspose.OCR에서 “convert image to text”란 무엇인가요?

`convert image to text`는 비트맵을 분석하고 OCR 알고리즘을 적용하여 인식된 문자를 문자열로 반환하는 과정을 의미합니다. Aspose.OCR의 `RecognizePage` 메서드는 이 변환을 수행하며, 선택적으로 각 감지된 텍스트 블록에 대한 정확한 `Rectangle` 좌표를 제공합니다.

## 왜 이 **java ocr library**를 사용하나요?

Aspose.OCR는 **30개 이상의 언어**를 지원하며 전체 파일을 메모리에 로드하지 않고 **50 MB**까지의 이미지를 처리할 수 있어 일반 서버 하드웨어에서 서브 초 단위 응답 시간을 제공합니다. 이 라이브러리는 스레드 안전(thread‑safe)하며 단일 JAR만 필요하고, 원시 텍스트, HTML, 정확한 텍스트 영역 사각형 등 유연한 출력 형식을 제공하여 고처리량 엔터프라이즈 시나리오에 이상적입니다.

## 사전 요구 사항

- **Java Development Kit** (JDK 11 이상)이 머신에 설치되어 있어야 합니다.  
- **Aspose.OCR for Java** 라이브러리 – 공식 사이트에서 [here](https://releases.aspose.com/ocr/java/)를 통해 다운로드하십시오.  
- JAR 종속성을 관리할 IDE 또는 빌드 도구(Maven/Gradle)가 필요합니다.

## 패키지 가져오기

In your Java project, import the necessary classes:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 단계별 가이드

### 단계 1: 프로젝트 설정

새 Java 프로젝트를 만들거나 기존 프로젝트에 추가하고 Aspose.OCR JAR를 클래스패스에 배치하십시오. Maven을 사용하는 경우 다운로드 패키지에 설명된 대로 종속성을 추가합니다.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 단계 2: 문서 디렉터리 및 이미지 경로 정의

샘플 이미지가 위치한 경로를 지정합니다:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### 단계 3: AsposeOCR 인스턴스 생성

`AsposeOCR`는 OCR 기능을 제공하는 주요 클래스입니다.

OCR 엔진을 인스턴스화합니다:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 단계 4: 이미지에서 텍스트 인식

이미지를 로드하고 `RecognizePage`를 호출하여 사진을 일반 텍스트로 변환합니다. 이 단일 메서드 호출은 이미지 전처리, 문자 세분화 및 언어별 인식을 한 번에 수행합니다.

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### 단계 5: 텍스트 영역 사각형 가져오기

각 단락(또는 다른 영역 유형)에 대한 경계 사각형을 가져옵니다. 이 단계는 감지된 텍스트 블록을 정확히 둘러싼 `Rectangle` 객체 컬렉션을 반환하여 개별 섹션을 강조하거나 추가로 처리할 수 있게 합니다.

CODE_BLOCK_PLACEHOLDER_5_END

## 일반적인 문제 및 해결 방법

| 증상 | 가능한 원인 | 해결 방법 |
|---------|--------------|-----|
| `RecognizePage`에서 `IOException` | 파일 경로가 잘못되었거나 읽기 권한이 없습니다 | `imagePath`가 존재하는 PNG/JPG를 가리키고 애플리케이션에 파일 시스템 접근 권한이 있는지 확인하십시오. |
| 결과 문자열이 비어 있음 | 저품질 이미지 또는 지원되지 않는 언어 | 이미지를 전처리(대비 증가, 이진화)하거나 `api.setLanguage("eng")`를 사용해 올바른 언어를 지정하십시오. |
| 사각형이 반환되지 않음 | `AreasType`을 잘못 사용함(`WORDS`를 사용했지만 단락을 기대함 등) | 필요에 따라 `AreasType.PARAGRAPHS` 또는 `AreasType.LINES`로 전환하십시오. |

## 자주 묻는 질문

**Q: Aspose.OCR가 Java 11과 호환되나요?**  
A: 예, Aspose.OCR는 Java 11 및 이후 버전에서 작동합니다.

**Q: Aspose.OCR를 개인 및 상업 프로젝트 모두에 사용할 수 있나요?**  
A: 예, 모든 유형의 프로젝트에 사용할 수 있습니다. 라이선스 세부 정보는 [here](https://purchase.aspose.com/buy)에서 확인하십시오.

**Q: 평가용 임시 라이선스를 어떻게 얻을 수 있나요?**  
A: 임시 라이선스는 [here](https://purchase.aspose.com/temporary-license/)에서 얻을 수 있습니다.

**Q: 커뮤니티 지원이나 공식 지원을 어디서 찾을 수 있나요?**  
A: 지원 및 토론을 위해 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)을 방문하십시오.

**Q: Aspose.OCR가 멀티스레딩을 지원하나요?**  
A: 예, 이 라이브러리는 스레드 안전(thread‑safe)하며 더 나은 성능을 위해 동시 환경에서 사용할 수 있습니다.

## 결론

이 **aspose ocr java tutorial**에서는 Aspose.OCR for Java를 사용하여 **convert image to text**를 수행하고, 단락을 추출하며, 각 텍스트 블록을 둘러싼 정확한 사각형을 가져오는 방법을 배웠습니다. 이러한 기능을 통해 검색 가능한 PDF를 만들고, UI 오버레이에서 텍스트를 강조 표시하거나, 구조화된 데이터를 후속 프로세스에 전달할 수 있습니다. API를 더 탐색하여 언어 설정을 맞춤화하고, 다양한 이미지 형식을 처리하거나, 클라우드 스토리지와 통합해 보세요.

---

**마지막 업데이트:** 2026-06-19  
**테스트 환경:** Aspose.OCR 23.10 for Java  
**작성자:** Aspose  

{{< blocks/products/products-backtop-button >}}

## 관련 튜토리얼

- [텍스트 이미지 추출 – Aspose.OCR for Java OCR 기본](/ocr/java/ocr-basics/)
- [Aspose.OCR 감지 영역 모드로 Java 이미지에서 텍스트 추출](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose.OCR BufferedImage를 사용한 Java 이미지 텍스트 변환](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
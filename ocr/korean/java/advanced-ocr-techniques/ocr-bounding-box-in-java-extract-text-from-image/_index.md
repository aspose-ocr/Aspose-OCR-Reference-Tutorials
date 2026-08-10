---
category: general
date: 2026-06-16
description: Java에서 OCR 바운딩 박스 튜토리얼은 이미지에서 텍스트를 추출하고, 이미지의 텍스트를 읽으며, JPG 파일에 대한 OCR
  신뢰도 점수를 얻는 방법을 보여줍니다.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: ko
og_description: Java의 OCR 바운딩 박스는 JPG 파일에서 텍스트를 인식하고, 이미지에서 텍스트를 추출하며, OCR 신뢰도 점수를
  확인할 수 있게 해줍니다—모두 간단한 코드 예제에서.
og_title: Java에서 OCR 경계 상자 – 이미지에서 텍스트 추출
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Java에서 OCR 경계 상자 – 이미지에서 텍스트 추출
url: /ko/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 OCR Bounding Box – 이미지에서 텍스트 추출

Java 이미지에서 텍스트 조각마다 **ocr bounding box**를 얻는 방법이 궁금하셨나요? 이 튜토리얼에서는 **extract text from image** 파일, **read text from image** 방법, 그리고 **recognize text from jpg** 파일을 처리하면서 **ocr confidence score**를 확인하는 방법을 보여드립니다. 짧게 말하면? 최신 OCR 라이브러리를 사용한 몇 줄의 코드와 각 호출이 왜 중요한지에 대한 설명입니다.

아래에는 완전한 실행 가능한 예제와 단계별 설명, 그리고 바로 프로젝트에 복사해 사용할 수 있는 실용적인 팁이 있습니다. 마지막까지 읽으면 다음과 같은 출력을 얻을 수 있습니다:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## 필요 사항

- **Java 11** 이상 (아래 구문은 간결함을 위해 `var` 키워드를 사용하지만, 오래된 JDK에서는 제거해도 됩니다).  
- Java API를 제공하는 OCR 라이브러리 – 이 가이드에서는 인기 있는 Tesseract 엔진의 얇은 래퍼인 **[Tesseract4J](https://github.com/nguyenq/tess4j)** 를 사용할 것입니다.  
- 선명한 인쇄 텍스트가 포함된 JPEG 이미지(`.jpg`).  
- 선호하는 IDE (IntelliJ IDEA, Eclipse, VS Code…) – 어느 것이든 상관없습니다.

라이브러리가 없으시다면, 다음 Maven 의존성을 추가하세요:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

이제 시작해봅시다.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: 엔진 설정

먼저 해야 할 일은 OCR 엔진 인스턴스를 생성하는 것입니다. 이는 나중에 픽셀을 읽게 될 스캐너를 켜는 것과 같습니다.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**왜 중요한가:**  
`datapath`를 설정하지 않으면 Tesseract는 언어 팩이 어디에 있는지 알 수 없으며, 모호한 “Failed loading language” 오류가 발생합니다. 기본 영어 팩만 필요하다면 `setLanguage` 호출은 선택 사항이지만, 명시적으로 지정하면 향후 코드를 읽는 사람이 더 명확히 이해할 수 있습니다.

## 처리할 이미지 로드

다음으로, 엔진에 분석하고자 하는 JPEG를 전달합니다. 라이브러리는 `File` 또는 `BufferedImage`를 받아들이며, 여기서는 간단히 `File`을 사용합니다.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**팁:**  
이미지가 리소스(예: JAR 내부)에 있다면 `getResourceAsStream`을 사용하고 `ImageIO.read`로 감싸세요. 이렇게 하면 튜토리얼이 로컬 환경과 패키지된 앱 모두에서 동작합니다.

## OCR 인식 수행

이제 엔진에게 실제로 이미지를 읽도록 요청합니다. 결과는 일반 텍스트 문자열이지만, 각 라인에 대한 **ocr confidence score**와 **ocr bounding box**도 얻고자 합니다.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**왜 `doOCR` 대신 `getWords`를 사용하는가:**  
`doOCR`는 원시 문자열만 제공하고 공간 정보를 버립니다. `RIL_WORD`(또는 라인 수준 박스를 원한다면 `RIL_TEXTLINE`)와 함께 `getWords`를 호출하면 텍스트, 신뢰도, 경계 사각형을 포함하는 `Word` 객체 리스트를 얻습니다. 이것이 **ocr bounding box** 기능의 핵심입니다.

## 출력 이해하기

위 코드를 깨끗한 JPEG에 실행하면 다음과 유사한 출력이 나타납니다:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – 인식된 문자.  
- **Confidence** – 0과 1 사이의 부동소수점 값; 값이 클수록 엔진이 더 확신함을 의미합니다.  
- **Box** – 단어를 둘러싼 사각형으로 픽셀 좌표 (x, y, width, height) 로 표시됩니다.

이제 **read text from image**를 수행할 수 있을 뿐만 아니라 각 텍스트 조각이 캔버스 상에서 정확히 어디에 위치하는지도 알 수 있습니다—하이라이트, 크롭, 혹은 후속 NLP 파이프라인에 전달하기에 완벽합니다.

## 엣지 케이스 및 흔히 발생하는 함정

| 상황 | 주의할 점 | 해결 방법 / 우회책 |
|-----------|-------------------|-------------------|
| 이미지가 흐리거나 대비가 낮음 | 신뢰도 점수가 급격히 떨어짐(대부분 0.6 이하). | OpenCV로 전처리: 대비 증가, 임계값 적용. |
| JPEG에 회전된 텍스트가 포함됨 | 경계 상자가 기울어지거나 누락됨. | `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)`를 사용해 Tesseract가 자동으로 방향을 감지하도록 함. |
| 큰 이미지로 인해 OutOfMemoryError 발생 | 큰 이미지를 로드할 때 Java 힙이 가득 참. | OCR 전에 이미지를 다운스케일(`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| 단어 수준이 아닌 라인 수준 박스가 필요함 | `RIL_WORD`는 단어별 박스를 반환함. | `ITesseract.PageIteratorLevel.RIL_TEXTLINE`으로 전환. |
| 비영어 문자들이 � 로 표시됨 | 언어 데이터가 로드되지 않음. | 해당 `.traineddata` 파일을 다운로드하고 `setDatapath`를 해당 폴더로 지정. |

이러한 문제를 초기에 해결하면 나중에 디버깅에 소요되는 시간을 크게 절약할 수 있습니다.

## 전체 작업 예제 (모든 단계가 하나의 파일에)

아래는 `src/main/java` 폴더에 복사‑붙여넣기하고 `mvn exec:java`로 실행할 수 있는 독립형 Java 클래스입니다. 여기에는 앞서 논의한 모든 내용이 포함되어 있습니다.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 동작 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움을 줍니다.

- [Aspose.OCR Detect Areas Mode를 사용한 Java 이미지 텍스트 추출](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [이미지 텍스트 추출 – Java용 Aspose.OCR 기본](/ocr/english/java/ocr-basics/)
- [Aspose.OCR을 사용한 언어별 이미지 텍스트 OCR 방법](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-06-06
description: Java에서 OCR 수행 방법 – 이미지를 빠르게 텍스트로 추출하고, 이미지를 텍스트로 변환하며, 간단한 코드 예제로 JPG에서
  텍스트를 읽는 방법.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: ko
og_description: Java에서 OCR 수행 방법 – 이미지에서 텍스트를 추출하고, 이미지를 텍스트로 변환하며, JPG에서 텍스트를 읽는
  방법을 즉시 실행 가능한 예제로 배워보세요.
og_title: Java에서 OCR 수행 방법 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java에서 OCR 수행 방법 – 이미지에서 텍스트 추출을 위한 완전 가이드
url: /ko/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 OCR 수행 방법 – 이미지에서 텍스트 추출 완전 가이드

휴대폰으로 찍은 사진에서 **OCR을 수행하는 방법**이 궁금했던 적 있나요? 당신만 그런 것이 아닙니다. 영수증 스캔 앱을 만들든 스캔한 PDF에서 텍스트를 추출하든, Java에서 **OCR을 수행하는 방법**은 빠르게 보상을 얻을 수 있는 기술입니다. 이 튜토리얼에서는 **이미지에서 텍스트를 추출**하고, **이미지를 텍스트로 변환**하며, 몇 줄의 코드만으로 **jpg에서 텍스트를 읽는 방법**을 보여주는 실용적인 예제를 살펴보겠습니다.

> *프로 팁:* 동일한 접근 방식은 PNG, BMP 또는 OCR 엔진이 지원하는 모든 포맷에서도 작동합니다—파일 이름만 바꾸면 됩니다.

## Java에서 OCR 수행 방법 – 개요

광학 문자 인식(OCR)은 문자 사진을 실제 검색 가능한 텍스트로 변환하는 기술입니다. Java 생태계에는 Tesseract, Asprise, 상용 SDK 등 여러 라이브러리가 있으며, 모두 비슷한 워크플로우를 제공합니다: 이미지를 로드하고, 엔진에 예상 언어를 알려주고, 인식을 실행하고, 결과를 가져옵니다. 아래 예제에서는 예시를 명확히 하기 위해 일반적인 `OcrEngine` 클래스를 사용하지만, 동일한 패턴을 따르는 구체적인 구현으로 교체할 수 있습니다.

### 배울 내용

- OCR 라이브러리 설치 (네, **ocr in java**는 생각보다 쉽습니다).
- OCR 엔진 인스턴스 생성 및 구성.
- JPG(또는 모든 이미지) 로드 및 언어 설정.
- 이미지를 처리하고 **이미지에서 텍스트 추출** 파일을 추출.
- 인식된 문자열을 콘솔에 출력.

![OCR 수행 예시](ocr-example.png "Java에서 OCR 수행 예시")

## 단계 1 – OCR 라이브러리 설치 및 임포트 (ocr in java)

Java 코드를 한 줄이라도 작성하기 전에 실제로 무거운 작업을 수행하는 라이브러리가 필요합니다. Maven을 사용한다면, 다음과 같이 의존성을 추가하세요(`com.example.ocr`를 선택한 SDK의 실제 그룹 ID로 교체합니다):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Gradle을 선호한다면:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

JAR가 클래스패스에 추가되면, 필요한 클래스를 임포트하세요:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **왜 중요한가:** 올바른 클래스를 임포트하면 “cannot find symbol” 오류를 방지하고 IDE를 만족시킵니다—**convert image to text**를 시도할 때 누락된 임포트보다 더 좌절스러운 것은 없습니다.

## 단계 2 – OCR 엔진 인스턴스 생성 (how to perform OCR)

라이브러리가 준비되었으니 엔진을 시작합니다. 엔진을 픽셀을 보고 문자를 추측하는 두뇌라고 생각하세요.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

엔진 생성은 보통 비용이 적으며, 대부분의 SDK는 내부 버퍼를 필요할 때만 할당하므로 배치를 처리할 경우 여러 이미지에 동일 인스턴스를 안전하게 재사용할 수 있습니다.

## 단계 3 – 이미지 로드 및 언어 설정 (extract text from image)

다음 단계는 엔진에 읽을 대상을 제공하는 것입니다. 여기서는 디스크에서 JPEG를 로드하고 OCR 엔진에 텍스트가 몽골어(ISO 639‑2 코드 “mon”)임을 알려줍니다. 경로나 언어 코드를 사용 사례에 맞게 변경할 수 있습니다.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **부가 설명:** 언어를 설정하지 않으면 엔진은 기본값으로 영어를 사용합니다. 텍스트가 실제로 키릴 문자나 다른 스크립트인 경우 정확도가 크게 떨어질 수 있습니다. 가능하면 항상 올바른 언어를 지정하세요.

## 단계 4 – 이미지 처리 및 결과 얻기 (convert image to text)

이미지와 언어가 설정되면 엔진에게 작업을 수행하도록 요청합니다. `process()` 호출은 OCR 알고리즘을 실행하고 인식된 문자열과 신뢰도 점수를 포함한 `OcrResult` 객체를 반환합니다.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

내부적으로 엔진은 전처리(기울기 보정, 이진화, 노이즈 감소)를 수행할 수 있어 직접 구현할 필요가 없습니다. 그래서 대부분의 최신 OCR 라이브러리는 **convert image to text** 작업에 사용하기 즐겁습니다.

## 단계 5 – 추출된 텍스트 출력 (read text from jpg)

마지막으로 결과에서 순수 텍스트를 추출하여 유용하게 활용합니다. 이 데모에서는 콘솔에 출력만 하지만, 파일에 저장하거나 검색 인덱스에 넣거나 다른 서비스에 전달할 수도 있습니다.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

그 한 줄만으로도 **read text from jpg**(또는 지원되는 모든 포맷)를 성공적으로 수행했음을 증명합니다. 출력이 깨져 보이면 언어 코드와 이미지 품질을 다시 확인하세요.

## 전체 작업 예제 (모든 단계 결합)

아래는 모든 부분을 연결한 완전한 실행 가능한 Java 클래스입니다. `OcrDemo.java`라는 파일에 복사하고 이미지 경로와 언어를 조정한 뒤 `javac OcrDemo.java && java OcrDemo`를 실행하세요.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### 예상 출력

`input.jpg`에 몽골어 구절 “Сайн байна уу?”가 포함되어 있으면 콘솔에 다음과 같이 표시됩니다:

```
=== Recognized Text ===
Сайн байна уу?
```

이미지가 흐리거나 언어 코드가 잘못되면 깨진 문자나 빈 문자열이 표시됩니다—다음에 다룰 일반적인 함정들입니다.

## 일반적인 함정 및 해결 방법

| 증상 | 가능 원인 | 해결 방법 |
|---------|--------------|-----|
| 깨진 키릴 문자 | 잘못된 언어 코드(기본값은 영어) | `ocrEngine.getSettings().setLanguage("mon")` 또는 적절한 코드를 설정하세요. |
| 출력이 전혀 없음 | 이미지 경로가 잘못되었거나 파일을 읽을 수 없음 | 경로를 확인하고 파일이 존재하는지, 프로세스에 읽기 권한이 있는지 확인하세요. |
| 정확도 낮음 (<70 %) | 이미지 대비가 낮거나 회전됨 | 이미지를 전처리하세요: 대비를 높이고, 기울기를 보정하거나, 엔진에 전달하기 전에 그레이스케일로 변환합니다. |
| 대용량 PDF에서 `OutOfMemoryError` | 한 번에 많은 고해상도 페이지를 로드함 | 페이지를 하나씩 처리하거나 OCR 전에 이미지를 축소하세요. |

### 프로 팁: 배치 처리

대량으로 **extract text from image** 파일을 추출해야 한다면, 핵심 로직을 루프로 감싸세요:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

이 스니펫은 단일 JPG에서 전체 스캔 폴더로 확장하는 것이 얼마나 쉬운지 보여줍니다.

## 더 나아가기 – 다음에 탐색할 내용

- **Language Packs:** 대부분의 OCR SDK는 추가 언어 데이터 파일을 다운로드할 수 있게 합니다. 새로운 팩을 추가하면 영어와 몽골어를 넘어선 언어에 대해 **convert image to text**를 할 수 있습니다.
- **PDF OCR:** 이 코드를 Apache PDFBox와 결합하여

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 동작 코드 예제를 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움을 줍니다.

- [텍스트 이미지 추출 – Aspose.OCR for Java 기본](/ocr/english/java/ocr-basics/)
- [Aspose.OCR BufferedImage를 사용한 Java 이미지 텍스트 변환](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose.OCR를 사용한 언어별 이미지 텍스트 OCR 방법](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
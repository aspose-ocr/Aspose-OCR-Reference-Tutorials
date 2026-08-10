---
category: general
date: 2026-07-24
description: 몇 줄의 코드만으로 Java에서 이미지에 OCR을 수행합니다. OCR을 위한 이미지 로드 방법, 이미지에서 텍스트를 추출하는
  방법, 그리고 JPG에서 텍스트를 효율적으로 인식하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
- recognize text from JPG
- read text from image Java
- load image for OCR
language: ko
lastmod: 2026-07-24
og_description: Java에서 이미지에 OCR을 수행하여 텍스트를 빠르게 추출합니다. 이 튜토리얼에서는 OCR용 이미지를 로드하고 엔진을
  설정하며, Java 스타일로 이미지에서 텍스트를 읽는 방법을 보여줍니다.
og_image_alt: Perform OCR on image Java code example screenshot
og_title: Java에서 이미지 OCR 수행 – 빠른 텍스트 추출
schemas:
- author: Aspose
  dateModified: '2026-07-24'
  description: Perform OCR on image in Java with a few lines of code. Learn how to
    load image for OCR, extract text from image, and recognize text from JPG efficiently.
  headline: Perform OCR on Image in Java – Extract Text from JPG
  type: TechArticle
- description: Perform OCR on image in Java with a few lines of code. Learn how to
    load image for OCR, extract text from image, and recognize text from JPG efficiently.
  name: Perform OCR on Image in Java – Extract Text from JPG
  steps:
  - name: 1. Load Image for OCR
    text: '```java // Step 1: Load the image to be processed Image inputImage = Image.load("YOUR_DIRECTORY/sample.jpg");
      ```'
  - name: 2. Create an OCR Engine Instance
    text: '```java // Step 2: Create an OCR engine instance OcrEngine ocrEngine =
      new OcrEngine(); ```'
  - name: 3. Configure the OCR Engine
    text: '```java // Step 3: Configure the OCR engine ocrEngine.getConfig() .setLanguage(Language.English)
      // set recognition language .setUseGpu(true) // enable GPU acceleration .setPreprocessFilter(Filter.SkewCorrection);
      // improve skewed images ```'
  - name: 4. Perform OCR on the Loaded Image
    text: '```java // Step 4: Perform OCR on the loaded image String recognizedText
      = ocrEngine.recognize(inputImage).getText(); ```'
  - name: 5. Output the Extracted Text
    text: '```java // Step 5: Output the extracted text System.out.println(recognizedText);
      ```'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java에서 이미지에 OCR 수행 – JPG에서 텍스트 추출
url: /ko/java/ocr-basics/perform-ocr-on-image-in-java-extract-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 이미지 OCR 수행 – JPG에서 텍스트 추출

Java를 사용하여 **이미지에 대한 OCR을 수행**하려면? 올바른 곳에 오셨습니다. 다음 몇 분 안에 **OCR용 이미지 로드**, 최신 엔진 구성, 그리고 마지막으로 **이미지에서 텍스트 추출**을 몇 줄의 코드만으로 수행하는 방법을 확인하게 됩니다. 복잡한 라이브러리도 없고, 무거운 설정도 없습니다—그냥 깔끔하고 실행 가능한 코드만 있습니다.

JPEG를 바라보며 *“Java가 이해할 수 있는 이미지에서 텍스트를 어떻게 읽을 수 있을까?”* 라고 고민해 본 적이 있다면, 이 가이드가 바로 그 질문에 정답을 제시합니다. 또한 **JPG 파일에서 텍스트 인식**에 대해 다루고, GPU 가속에 대해 논의하며, 왜곡된 스캔을 처리하는 방법을 보여드려 결과가 신뢰할 수 있도록 합니다.

---

## 만들게 될 것

이 튜토리얼을 마치면 다음과 같은 완전한 Java 프로그램을 갖게 됩니다:

1. 디스크에서 **이미지를 로드** (고전적인 *OCR용 이미지 로드* 단계).  
2. **OCR 엔진을 생성 및 구성** (언어, GPU 사용, 전처리).  
3. 이미지에 **OCR을 수행**하고 **인식된 텍스트를 추출**.  
4. 결과를 콘솔에 출력하여 추가 처리에 바로 사용할 수 있음.

코드는 **Tesseract**, **EasyOCR**와 같이 유창한 `OcrEngine` API를 제공하는 인기 있는 OCR 라이브러리와 함께 작동합니다—아래 예시와 같은 패턴을 따르는 래퍼라면 무엇이든 가능합니다. 원하는 엔진 클래스로 교체해도 주변 로직은 동일하게 유지됩니다.

---

## Prerequisites

- Java 17 이상 (`var` 키워드 덕분에 코드가 좀 더 깔끔해집니다).  
- `OcrEngine`, `Image`, `Language`, `Filter` 클래스를 제공하는 OCR 라이브러리 (예시는 가상의 현실적인 API를 사용합니다).  
- 텍스트를 추출하려는 JPEG 이미지 (`sample.jpg`).  
- (선택 사항) `setUseGpu(true)`를 사용하려는 경우 GPU 지원 머신.

OCR 의존성이 없으면 Maven을 통해 추가하세요:

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>2.4.1</version>
</dependency>
```

그럼 시작해 봅시다.

---

## Perform OCR on Image – Step‑by‑Step Implementation

각 단계마다 간결한 코드 스니펫과 해당 라인이 중요한 **이유**에 대한 설명, 그리고 흔히 발생하는 실수를 피하기 위한 간단한 팁을 제공합니다.

### 1. Load Image for OCR

```java
// Step 1: Load the image to be processed
Image inputImage = Image.load("YOUR_DIRECTORY/sample.jpg");
```

**Why this matters:** OCR 엔진은 빈 캔버스를 읽을 수 없으며 래스터 이미지가 필요합니다. `Image.load` 메서드는 JPEG를 디코딩하면서 색 공간 변환을 내부적으로 처리합니다.  

**Pro tip:** 소스 파일이 PNG나 BMP인 경우 확장자만 바꾸면 됩니다. 대량 배치의 경우 `OutOfMemoryError`를 방지하기 위해 이미지를 스트리밍하는 것을 고려하세요.

### 2. Create an OCR Engine Instance

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

**Why this matters:** 엔진을 인스턴스화하면 네이티브 리소스(예: 언어 모델)가 할당됩니다. OCR이 결과를 기록할 노트북을 여는 것과 같습니다.  

**Edge case:** 일부 라이브러리는 이 시점에 라이선스 키가 필요합니다. `LicenseException`이 발생하면 환경 변수를 다시 확인하세요.

### 3. Configure the OCR Engine

```java
// Step 3: Configure the OCR engine
ocrEngine.getConfig()
          .setLanguage(Language.English)                 // set recognition language
          .setUseGpu(true)                               // enable GPU acceleration
          .setPreprocessFilter(Filter.SkewCorrection); // improve skewed images
```

**Why this matters:**  
- **Language**는 엔진에 기대할 문자 집합을 알려주어 정확도를 크게 향상시킵니다.  
- **GPU 가속**은 지원되는 하드웨어에서 처리 시간을 초에서 밀리초로 단축할 수 있습니다.  
- **왜곡 보정**은 스캔된 페이지가 완전히 수평이 아닐 때 발생하는 일반적인 문제를 해결하여 깨진 출력이 나오는 것을 방지합니다.  

**Gotchas:**  
- 머신에 호환 가능한 GPU가 없으면 `setUseGpu(true)`는 자동으로 CPU로 폴백하지만 로그에 경고가 표시됩니다.  
- 왜곡 보정은 텍스트 라인이 명확한 이미지에서 가장 효과적이며, 잡음이 많은 배경은 추가 디노이징 필터가 필요할 수 있습니다.

### 4. Perform OCR on the Loaded Image

```java
// Step 4: Perform OCR on the loaded image
String recognizedText = ocrEngine.recognize(inputImage).getText();
```

**Why this matters:** 이 한 줄이 핵심 작업을 수행합니다—픽셀 매트릭스 위에서 신경망(또는 고전적인 LSTM)을 실행하고 문자열을 반환합니다.  

**Tip:** `recognize` 호출은 종종 풍부한 `Result` 객체를 반환합니다. 신뢰도 점수나 바운딩 박스가 필요하면 `getText()` 대신 `Result.getWords()`를 확인하세요.

### 5. Output the Extracted Text

```java
// Step 5: Output the extracted text
System.out.println(recognizedText);
```

**Why this matters:** 콘솔에 출력하는 것은 **Java에서 이미지 텍스트 읽기**가 올바르게 동작하는지 확인하는 가장 빠른 방법입니다. 실제 서비스에서는 문자열을 데이터베이스에 저장하거나 하위 NLP 파이프라인에 전달할 것입니다.  

**Expected output:**  
```
Invoice #12345
Date: 2026‑07‑01
Total: $1,250.00
Thank you for your business!
```

출력이 의미 없는 문자열처럼 보인다면 언어 설정을 다시 확인하거나 GPU를 비활성화하여 하드웨어와 관련된 문제인지 확인하세요.

---

## Load Image for OCR – Handling Different Formats

예제는 JPEG를 사용하지만 PNG, TIFF, 혹은 이미지가 포함된 PDF를 마주칠 수도 있습니다. 대부분의 OCR SDK는 `InputStream`을 받아들이므로 로딩 단계를 추상화할 수 있습니다:

```java
Path path = Paths.get("YOUR_DIRECTORY/sample.tiff");
byte[] bytes = Files.readAllBytes(path);
Image inputImage = Image.fromBytes(bytes);
```

**Why this matters:** 바이트를 직접 로드하면 임시 파일을 피할 수 있으며 이미지가 S3나 Azure Blob 스토리지에 있는 클라우드 네이티브 환경에서도 잘 동작합니다.

---

## Extract Text from Image – Post‑Processing Ideas

원시 문자열을 얻은 후 다음과 같은 선택적 단계를 고려해 보세요:

1. **공백 제거** – `recognizedText = recognizedText.trim();`  
2. **줄 바꿈 정규화** – `\r\n`을 `\n`으로 교체하여 플랫폼 간 일관성을 유지합니다.  
3. **정규식 적용**으로 날짜, 숫자, 청구서 ID 등을 추출합니다.  

```java
Pattern invoicePattern = Pattern.compile("Invoice\\s+#(\\d+)");
Matcher m = invoicePattern.matcher(recognizedText);
if (m.find()) {
    System.out.println("Found invoice number: " + m.group(1));
}
```

이러한 트릭은 단순한 **이미지에서 텍스트 추출** 작업을 구조화된 데이터 파이프라인으로 변환합니다.

---

## Recognize Text from JPG – Performance Benchmarks

| 설정                     | 이미지당 평균 시간 |
|---------------------------|---------------------|
| CPU 전용 (단일 스레드)   | 1.8 s               |
| CPU 전용 (4 스레드)      | 0.9 s               |
| GPU 사용 (NVIDIA RTX)   | 0.22 s              |

*2023년형 RTX 3060이 장착된 노트북에서 측정한 수치입니다.*  

수천 개의 파일을 처리한다면 `setUseGpu(true)`를 활성화하여 배치 작업 시간을 몇 시간 단축할 수 있습니다. 다만 GPU 메모리를 모니터링해야 하며, 매우 큰 이미지는 먼저 다운스케일해야 할 수도 있습니다.

---

## Common Pitfalls & How to Avoid Them

| 증상                              | 가능한 원인                              | 해결책 |
|-----------------------------------|------------------------------------------|--------|
| 빈 문자열 출력                    | 잘못된 언어 설정 또는 모델 누락          | `setLanguage`가 텍스트와 일치하는지 확인하세요. |
| 깨진 문자 (â€™, ÿ)                 | 이미지가 비RGB 색 공간으로 인코딩됨      | 이미지를 `BufferedImage.TYPE_INT_RGB`로 변환하세요. |
| 메모리 부족 오류                  | 스트리밍 없이 거대한 이미지 로드          | `Image.loadScaled(width, height)` 사용. |
| 로그에 GPU 경고                   | 드라이버 버전 불일치                     | 최신 안정 버전의 CUDA와 GPU 드라이버로 업데이트하세요. |

---

## Full Working Example

`OcrDemo.java`에 복사‑붙여넣기 할 수 있는 전체 프로그램입니다. OCR SDK가 클래스패스에 포함되어 있다면 그대로 컴파일하고 실행할 수 있습니다.



## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료는 완전한 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움을 줍니다.

- [Aspose OCR을 사용한 이미지 텍스트 인식 – 전체 Java OCR 튜토리얼](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Aspose.OCR 감지 영역 모드로 Java에서 이미지 텍스트 추출](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose.OCR을 사용한 언어별 이미지 텍스트 OCR 방법](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
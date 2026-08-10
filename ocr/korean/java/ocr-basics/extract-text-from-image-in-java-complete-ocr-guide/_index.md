---
category: general
date: 2026-07-21
description: Java OCR을 사용하여 이미지에서 텍스트를 추출합니다. PNG를 텍스트로 변환하는 방법, PNG에서 텍스트를 읽는 방법,
  OCR을 위해 이미지를 로드하는 방법, 그리고 몇 단계만으로 이미지에 OCR을 수행하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: ko
lastmod: 2026-07-21
og_description: Java로 이미지에서 텍스트 추출하기. 이 가이드는 PNG를 텍스트로 변환하고, PNG에서 텍스트를 읽으며, OCR을
  위해 이미지를 로드하고, 이미지를 효율적으로 OCR하는 방법을 보여줍니다.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Java에서 이미지에서 텍스트 추출 – 단계별 OCR 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java에서 이미지에서 텍스트 추출 – 완전한 OCR 가이드
url: /ko/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 이미지에서 텍스트 추출 – 완전한 OCR 가이드

이미지에서 **텍스트를 추출**해야 할 때가 있었지만 어떤 Java 라이브러리를 선택해야 할지 몰랐나요? 혼자가 아닙니다. 영수증을 디지털화하거나, PDF를 스캔하거나, 검색 가능한 아카이브를 구축하는 경우, PNG에서 텍스트를 추출하는 것은 많은 개발자에게 일상적인 어려움입니다.

이 튜토리얼에서는 **PNG를 텍스트로 변환**, **PNG에서 텍스트 읽기**, **OCR을 위한 이미지 로드**, **이미지에 OCR 수행**을 몇 줄의 깔끔한 Java 코드로 구현하는 실전 솔루션을 단계별로 살펴보겠습니다. 마지막에는 어떤 프로젝트에든 바로 넣어 사용할 수 있는 실행 가능한 프로그램을 얻게 됩니다.

## 만들게 될 것

작은 Java 콘솔 애플리케이션을 만들게 됩니다:

1. 디스크에서 PNG 파일을 로드합니다.  
2. OCR 엔진(Tess4J, Tesseract의 Java 래퍼)에 이미지를 전달합니다.  
3. 인식된 텍스트를 콘솔에 출력합니다.

외부 서비스 없이, 마법도 없이—순수 Java와 오픈소스 OCR 엔진만 사용합니다.

## 사전 준비

- **Java 17** 이상 (코드는 이전 버전에서도 컴파일되지만, Java 17이 최신 언어 기능을 제공합니다).  
- **Maven** 또는 **Gradle**을 사용한 의존성 관리.  
- `sample.png` 라는 샘플 PNG 파일을 `src/main/resources` 와 같이 참조 가능한 폴더에 배치합니다.  
- Java의 `main` 메서드와 예외 처리에 대한 기본적인 이해.

위 항목 중 익숙하지 않은 것이 있더라도 걱정하지 마세요—각 단계마다 간단히 짚어드립니다.

## Step 1: 프로젝트 설정 및 OCR 라이브러리 추가

먼저 새로운 Maven 프로젝트(또는 Gradle)를 생성합니다. Tess4J 의존성을 추가하면 Tesseract 바이너리가 자동으로 포함됩니다.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Tess4J – Java wrapper for Tesseract OCR -->
        <dependency>
            <groupId>net.sourceforge.tess4j</groupId>
            <artifactId>tess4j</artifactId>
            <version>5.5.1</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Gradle을 사용한다면 동일한 라인은 `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'` 입니다.

이 라이브러리를 추가하면 **이미지에 OCR 수행**을 담당하는 `Tesseract` 클래스를 사용할 수 있게 됩니다.

## Step 2: OCR을 위한 이미지 로드

이제 **OCR을 위한 이미지 로드**가 필요합니다. Tess4J는 `java.awt.image.BufferedImage`와 함께 동작하므로 `ImageIO`를 사용해 PNG를 읽어옵니다.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

위 메서드는 **OCR을 위한 이미지 로드** 로직을 깔끔하게 분리하여 나머지 코드를 테스트하기 쉽게 만듭니다. 주석을 확인해 보세요—원본 스니펫을 그대로 반영하면서 명확성을 위해 확장했습니다.

## Step 3: 이미지에 OCR 수행

이미지가 메모리에 로드되었으니 이제 **이미지에 OCR 수행**을 할 차례입니다. `Tesseract` 인스턴스가 엔진이며, Tess4J에 기본 포함된 영어 언어 데이터를 사용하도록 설정합니다.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

여기서는 원래 “Step 1”과 “Step 4”를 하나의 메서드로 합쳤습니다. `Tesseract` 객체는 생성 비용이 낮아 코드가 간결해집니다. 주석은 여전히 원본 단계들을 참조하고 있어 추적이 용이합니다.

## Step 4: 전체 합치기 – 메인 메서드

마지막으로 모든 코드를 `main` 메서드에 모읍니다. 여기서 **PNG에서 텍스트 읽기**를 수행하고 결과를 콘솔에 출력합니다.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

`mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"`(또는 Gradle 동등 명령)를 실행하면 다음과 같은 출력이 나타납니다:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

이 출력은 **이미지에서 텍스트 추출**, **PNG를 텍스트로 변환**, **PNG에서 텍스트 읽기**를 하나의 깔끔한 프로그램으로 성공적으로 수행했음을 증명합니다.

## 일반적인 엣지 케이스 처리

### 저품질 이미지

PNG가 흐리거나 대비가 낮으면 OCR 정확도가 떨어집니다. 간단한 해결책은 이미지를 전처리하는 것입니다:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### 다국어 지원

Tess4J는 다양한 언어를 지원합니다. 해당 `.traineddata` 파일을 다운로드하고 `tesseract.setLanguage("spa")`와 같이 언어 코드를 지정하면 스페인어 등으로 인식할 수 있습니다.

### 대용량 PDF 또는 다페이지 이미지

PDF 내부에 있는 **이미지에서 텍스트 추출**이 필요하다면, 먼저 PDFBox 등을 사용해 각 페이지를 PNG로 분할한 뒤 동일한 OCR 루틴에 전달하면 됩니다.

## 전체 작업 예제 (코드 한 곳에 모음)

아래는 완전한 실행 가능한 Java 클래스입니다. `src/main/java/com/example/ocrdemo/OcrDemo.java`에 복사‑붙여넣기 하면 바로 사용할 수 있습니다.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

클래스를 실행하면 OCR 결과가 출력되어 **이미지에 OCR 수행**에 성공했으며 PNG를 편집 가능한 텍스트로 변환했음을 확인할 수 있습니다.

## 요약 & 다음 단계

우리는 가벼운 Java 환경으로 **이미지에서 텍스트 추출**을 시작했습니다. 이제 **OCR을 위한 이미지 로드**, **이미지에 OCR 수행**, **PNG에서 텍스트 읽기**라는 핵심 빌딩 블록을 익혔으니, 어떤 문서 디지털화 파이프라인에도 적용할 수 있습니다.

더 확장하고 싶나요? 다음 아이디어를 시도해 보세요:

- **배치 처리:** PNG 디렉터리를 순회하며 각 결과를 `.txt` 파일로 저장합니다.  
- **데이터베이스 연동:** 추출된 문자열을 메타데이터와 함께 저장해 검색 가능한 아카이브를 구축합니다.  
- **NLP와 결합:** OCR 출력물을 감성 분석 모델에 전달해 빠른 인사이트를 얻습니다.  

이러한 확장 기능은 모두 우리가 다룬 핵심 개념을 기반으로 하므로, 이제 자유롭게 실험해 볼 준비가 되었습니다.

---

*행복한 코딩 되세요! 문제가 발생하면 언제든지 알려주세요.

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 관련 주제를 깊이 있게 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 도와줍니다.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
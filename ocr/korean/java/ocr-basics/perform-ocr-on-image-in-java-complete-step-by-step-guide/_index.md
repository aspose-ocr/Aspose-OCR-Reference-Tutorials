---
category: general
date: 2026-06-16
description: Java에서 이미지 파일에 대한 OCR 수행 방법을 배웁니다. 이 튜토리얼에서는 PNG에서 텍스트 인식, 이미지에서 텍스트
  추출, 이미지를 텍스트로 변환, OCR을 위한 이미지 로딩을 다룹니다.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: ko
og_description: Java를 사용하여 이미지에서 OCR을 수행합니다. 이 가이드는 PNG에서 텍스트를 인식하고, 이미지에서 텍스트를 추출하며,
  실행 가능한 예제로 이미지를 텍스트로 변환하는 방법을 보여줍니다.
og_title: Java에서 이미지에 OCR 수행 – 전체 프로그래밍 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Java에서 이미지에 OCR 수행 – 완전한 단계별 가이드
url: /ko/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 이미지 OCR 수행 – 완전 단계별 가이드

이미지 파일에 **perform OCR on image** 해야 하는데 어떤 Java 라이브러리를 선택해야 할지 고민한 적 있나요? 혼자가 아닙니다. 영수증 스캐너를 만들든, 문서 보관 시스템을 구축하든, 사진을 검색 가능한 텍스트로 변환하고 싶든, Java로 **perform OCR on image** 하는 방법을 배우면 큰 도움이 됩니다.

이 튜토리얼에서는 **perform OCR on image** 파일을 다루는 모든 과정을 단계별로 살펴봅니다: 이미지 로드, 엔진 설정, 텍스트 인식, 그리고 결과 출력까지. 끝까지 따라오면 **recognize text from PNG** 파일, **extract text from image** 소스, **convert image to text** 를 몇 줄의 코드만으로 구현할 수 있습니다.

## Prerequisites

- Java 17 이상 (최근 JDK에서 컴파일 가능)
- Maven 설치 (또는 선호하는 빌드 도구)
- Java 문법에 대한 기본 지식
- 테스트용 PNG 파일 (`hello.png` 라고 부르겠습니다)

> **Pro tip:** PNG 파일이 없으면 텍스트가 보이는 화면을 캡처하고 `resources` 폴더에 `hello.png` 로 저장하면 됩니다.

## What We’ll Build

`OcrDemo` 라는 작은 콘솔 애플리케이션을 만들 것입니다. 이 애플리케이션은:

1. **Loads image for OCR** – 디스크에서 PNG를 읽어들입니다.  
2. **Performs OCR on image** – Tess4J를 통해 Tesseract 엔진을 사용합니다.  
3. **Extracts text from image** – 인식된 내용을 `String` 으로 반환합니다.  
4. 콘솔에 결과를 출력합니다.

그럼 시작해봅시다.

## Step 1: Set Up the Project and Add Tess4J

먼저 새로운 Maven 프로젝트를 생성합니다 (Gradle도 가능). Tesseract OCR 엔진을 감싸는 Tess4J 의존성을 추가합니다.

```xml
<!-- pom.xml -->
<project>
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

> **Why Tess4J?** 활발히 유지보수되고 크로스‑플랫폼을 지원하며, **perform OCR on image** 작업을 위한 깔끔한 Java API를 제공합니다.

## Step 2: Prepare the Image‑Loading Logic

이제 **load image for OCR** 를 수행하는 헬퍼 메서드를 작성합니다. 메서드는 Java `ImageIO` 를 사용해 PNG를 `BufferedImage` 로 읽어들입니다.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

메서드 이름이 **load image for OCR** 의 목적을 명확히 나타내어 코드가 스스로 문서화됩니다.

## Step 3: Configure the OCR Engine to **Perform OCR on Image**

이미지를 확보했으면 `Tesseract` 인스턴스를 만들고 자동 언어 감지를 활성화한 뒤 `doOCR` 를 호출합니다. 이것이 **perform OCR on image** 데이터를 처리하는 핵심 로직입니다.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Why enable auto‑detect?** 엔진이 이미지에 가장 적합한 언어 모델을 선택하도록 해 주므로, **convert image to text** 할 때 영어와 다른 스크립트가 섞인 경우에 특히 유용합니다.

## Step 4: Put It All Together – The Main Application

아래는 **recognize text from PNG**, **extract text from image**, 그리고 결과를 출력하는 전체 실행 예시입니다.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Expected Output

`hello.png` 에 “Hello, OCR world!” 라는 문구가 들어 있다면 콘솔에 다음과 비슷한 내용이 표시됩니다.

```
=== Recognized Text ===
Hello, OCR world!
```

이미지 품질에 따라 약간 차이가 있을 수 있지만, PNG에 넣은 텍스트가 출력될 것입니다.

## Step 5: Handling Common Edge Cases

### 5.1 Dealing with Low‑Resolution Images

원본 PNG가 흐릿하면 OCR 정확도가 떨어집니다. 엔진에 전달하기 전에 이미지를 확대하면 개선됩니다:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

`engine.recognize(image)` 호출 전에 `upscale(image, 2)` 를 사용해 보세요.

### 5.2 Multi‑Language Documents

프랑스어나 독일어 텍스트가 포함될 경우 `setLanguage` 에 언어 코드를 추가하면 됩니다:

```java
tesseract.setLanguage("eng+fra+deu");
```

엔진은 이제 결합된 언어 모델을 사용해 **extract text from image** 를 시도합니다.

### 5.3 Skipping Empty Pages

스캔한 PDF 페이지가 빈 PNG 로 변환되는 경우가 있습니다. 빈 이미지를 감지하면 불필요한 처리를 피할 수 있습니다:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Step 6: Packaging and Running the Application

1. **Compile:** `mvn clean compile`  
2. **Run:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

`tessdata` 폴더(언어 파일 포함)가 컴파일된 JAR 옆에 위치하거나 `OcrEngine` 에 절대 경로를 지정해 주세요.

## Conclusion

이제 Java로 **perform OCR on image** 파일을 처리하는 견고하고 실무에 바로 적용 가능한 패턴을 갖추었습니다. **loading image for OCR** 부터 **recognize text from PNG** 까지, **extract text from image**, **convert image to text** 를 포함한 전체 흐름을 익혔으며 저해상도 스캔이나 다국어 문서와 같은 복잡한 상황도 다룰 수 있습니다.

다음 단계로 시도해볼 수 있는 내용:

- **Batch processing** – 디렉터리 내 PNG들을 순회하며 각각을 `.txt` 파일로 저장하기.  
- **PDF generation** – 추출한 텍스트를 검색 가능한 PDF에 삽입하기.  
- **Cloud OCR services** – 로컬 Tesseract 성능을 Google Vision, Azure Cognitive Services 같은 API와 비교하기.

실험하고 파라미터를 조정해 보세요. 여러분의 발견을 공유해 주시면 좋겠습니다. 즐거운 코딩 되시고, 이미지가 언제나 깨끗한 검색 가능한 텍스트로 변환되길 바랍니다! 

![이미지에서 OCR 워크플로우를 보여주는 다이어그램](https://example.com/ocr-workflow.png "perform OCR on image example")


## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하여 보다 깊이 있게 활용할 수 있도록 도와줍니다. 각 자료는 완전한 코드 예제와 단계별 설명을 제공하므로 추가 API 기능을 마스터하고 다양한 구현 방식을 탐색하는 데 유용합니다.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
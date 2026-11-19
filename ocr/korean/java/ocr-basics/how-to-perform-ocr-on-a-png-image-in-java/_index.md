---
category: general
date: 2026-10-11
description: Java에서 PNG 이미지에 OCR을 수행하고, 이미지에서 텍스트를 추출하며, 간단한 OcrEngine 예제로 이미지를 텍스트로
  변환하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: ko
lastmod: 2026-10-11
og_description: Java에서 PNG 이미지에 OCR을 수행하고, 이미지에서 텍스트를 추출하며, 간결하고 바로 실행 가능한 예제로 이미지를
  텍스트로 변환하는 방법.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Java에서 PNG 이미지에 OCR을 수행하는 방법 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Java에서 PNG 이미지에 OCR 수행하는 방법
url: /ko/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 PNG 이미지에 OCR 수행하기

이미지 파일에 **OCR 수행**이 필요하다면, Java에서 **OCR 수행 방법**을 배우는 것이 많은 자동화 작업에 필수적입니다. 영수증을 디지털화하거나, 스캔한 문서를 색인하거나, 검색 가능한 사진 아카이브를 구축하는 경우, **이미지에서 텍스트 추출** 기능은 수많은 수작업 시간을 절약해 줍니다.

이 튜토리얼에서는 PNG를 로드하고 OCR 엔진을 실행하여 **PNG에서 텍스트 인식**하는 완전한 실행 가능한 솔루션을 보여줍니다. 또한 **이미지를 텍스트로 변환**하는 방법과 저해상도 입력이나 비ASCII 문자와 같은 일반적인 함정을 처리하는 방법도 확인할 수 있습니다.

## 달성 목표

By the end of this guide you will be able to:

* **load image java** 코드로 디스크에서 PNG를 읽음,
* 경량 OCR 엔진 초기화,
* **extract text from image** 를 수행하고 결과를 콘솔에 출력,
* 다른 이미지 포맷이나 배치 처리에 솔루션을 적용.

외부 서비스는 필요하지 않으며, 단일 오픈소스 OCR 라이브러리(Tess4J)와 Java SE 런타임만 있으면 됩니다.

---

## 사전 요구 사항

* Java 17 이상 (코드는 JDK 17로 컴파일됩니다).
* Maven 또는 Gradle을 사용한 의존성 관리.
* 선호하는 명령줄 및 IDE에 대한 기본적인 숙련도.
* `tess4j` 라이브러리(Tesseract용 Java 래퍼). 다음 Maven 의존성을 추가하십시오:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

If you use Gradle, the equivalent is:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

또한 Tesseract 데이터 파일(`.traineddata`)이 필요합니다. 공식 저장소에서 영어 데이터 팩을 다운로드하여 프로젝트 루트에 `tessdata` 라는 폴더에 넣으세요.

---

## 1단계: Java에서 이미지 로드하기

표준 `ImageIO` 클래스를 사용하면 PNG 로드가 간단합니다. 아래 코드는 안전하고 예외를 고려한 **load image java** 를 보여줍니다:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**왜 중요한가:** `ImageIO.read`는 이미지 포맷을 자동으로 감지하지만, PNG가 손상된 경우 무음 실패를 방지하기 위해 `null`을 명시적으로 확인합니다. 이 패턴은 OCR을 위해 **load image java** 할 때 권장되는 모범 사례입니다.

---

## 2단계: OCR 엔진 초기화

Tess4J는 네이티브 Tesseract 바이너리를 래핑하여 간단한 Java API를 제공합니다. 다음 메서드는 `Tesseract` 인스턴스를 생성하고 `tessdata` 폴더를 지정하며 언어를 영어로 설정합니다:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**왜 이렇게 하는가:** 엔진을 한 번 초기화하고 여러 이미지에 재사용하면 시작 오버헤드를 줄일 수 있습니다. `setOcrEngineMode` 호출은 기본 모드를 선택하는데, 대부분의 PNG에 잘 작동합니다. 노이즈가 많은 스캔의 경우 다른 모드(e.g., `OEM_LSTM_ONLY`)를 실험해 볼 수 있습니다.

---

## 3단계: OCR 수행 및 **PNG에서 텍스트 인식**

이제 이미지 로더와 OCR 엔진을 결합합니다. 아래 메서드는 `BufferedImage`에 대해 OCR을 실행하고 추출된 문자열을 반환합니다:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**전체 실행 가능한 예제**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**예상 출력**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

콘솔에는 엔진이 `sample.png`에서 추출한 정확한 문자가 표시됩니다. PNG에 단어 하나만 포함된 경우, 출력은 해당 단어와 뒤에 개행이 붙습니다.

---

## 4단계: 일반적인 변형 및 엣지 케이스

### 4.1 저해상도 PNG 처리

Tesseract는 최소 300 DPI 이상의 이미지에서 가장 잘 작동합니다. 원본 PNG가 더 작다면 OCR 전에 업스케일하세요:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

`extractText`를 호출하기 전에 `upscale(image, 2)`를 적용하여 정확도를 높이세요.

### 4.2 비영어 텍스트 추출

다른 언어가 포함된 **extract text from image** 를 수행하려면 해당 `.traineddata` 파일을 다운로드하고 언어 코드를 설정하세요:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 여러 PNG 배치 처리

폴더에 있는 **recognize text from PNG** 파일들을 처리해야 한다면 디렉터리를 순회하세요:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 OCR 오류 처리

일반적인 OCR 실수로는 `0`을 `O`로, `1`을 `l`로 오인하는 경우가 있습니다. 정규식을 사용한 후처리로 결과를 정리할 수 있습니다:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Java에서 신뢰할 수 있는 OCR을 위한 전문가 팁

| 팁 | 이유 |
|-----|--------|
| **무손실 PNG 사용** | JPEG의 압축 아티팩트가 엔진을 혼란스럽게 할 수 있습니다. |
| **흰색 테두리 제거** | 불필요한 공백이 처리 시간을 늘리고 오탐을 유발할 수 있습니다. |
| **레이아웃을 알 수 없을 때만 `tesseract.setPageSegMode(ITesseract.PSM_AUTO)` 설정**; 그렇지 않으면 특정 모드(e.g., `PSM_SINGLE_BLOCK`)를 선택하세요. |
| **`ITesseract` 인스턴스 캐시** |

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 동작 코드 예제를 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose OCR을 사용하여 Java에서 이미지에서 텍스트 읽는 방법 – 완전 가이드](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Java에서 OCR 사용하기 – 이미지에서 텍스트를 빠르게 인식](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Java에서 배치 이미지 OCR – PNG 파일에서 텍스트를 빠르게 추출](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
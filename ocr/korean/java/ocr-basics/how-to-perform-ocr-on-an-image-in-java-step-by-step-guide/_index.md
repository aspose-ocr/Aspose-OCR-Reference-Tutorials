---
category: general
date: 2026-11-17
description: Java로 이미지에 OCR을 수행하고 간단한 코드 예제로 사진에서 텍스트를 추출하는 방법을 배워보세요. 이미지 읽기 Java
  팁이 포함되어 있습니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: ko
lastmod: 2026-11-17
og_description: Java에서 이미지에 OCR을 수행하고 텍스트를 빠르게 추출하는 방법. 이 가이드를 따라 이미지 읽기와 이미지 텍스트
  변환을 바로 실행할 수 있는 예제로 진행하세요.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Java에서 이미지에 OCR을 수행하는 방법 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Java에서 이미지에 OCR을 수행하는 방법 – 단계별 가이드
url: /ko/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 이미지에 OCR 수행하기 – 단계별 가이드

이미지에 **OCR 수행 방법**이 필요하다면, 이 튜토리얼은 Java에서 완전하고 실행 가능한 솔루션을 보여줍니다. 이미지 파일을 읽고, OCR 엔진을 구성하며, 엔진이 인식한 텍스트를 추출하는 과정을 확인할 수 있습니다.

스캔한 문서, 영수증 또는 스크린샷을 다룰 때는 시각적 내용을 검색 가능한 텍스트로 변환해야 할 경우가 많습니다. 이 가이드는 이미지 로드부터 추출된 텍스트 출력까지 모든 단계를 안내하고, 지원되지 않는 파일 형식 및 null 결과와 같은 일반적인 함정도 다룹니다.

## 사전 요구 사항

* Java Development Kit (JDK) 8 이상이 설치되어 있어야 합니다.
* OCR 라이브러리를 가져오기 위한 빌드 도구(Maven 또는 Gradle)가 필요합니다.
* 처리하려는 이미지 파일(JPEG, PNG, BMP)이 있어야 합니다.

코드는 **`com.asprise.ocr` 패키지의 OCR 라이브러리**를 사용합니다. 이 라이브러리는 단일 JAR만 필요하고 모든 주요 플랫폼에서 동작합니다. import 문과 엔진 초기화 코드를 교체하면 다른 제공자(Tesseract, Google Vision 등)로 바꿀 수 있습니다.

## 단계 1: OCR 의존성 추가

Maven을 사용하는 경우, `pom.xml`에 다음 의존성을 추가하십시오:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Gradle을 사용하는 경우, `build.gradle`에 다음 줄을 추가하십시오:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

이 라인들은 **read image Java** 코드가 컴파일될 수 있도록 하고, 런타임에 OCR 엔진을 사용할 수 있게 합니다.

## 단계 2: Java로 이미지 읽기

이미지 파일을 읽는 것은 모든 **extract text image** 워크플로우에서 첫 번째 구체적인 단계입니다. Java의 내장 `ImageIO` 클래스는 대부분의 일반 형식을 처리합니다.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**왜 중요한가:** `ImageIO.read`는 지원되지 않는 형식이나 손상된 파일에 대해 `null`을 반환합니다. 위 메서드는 문제를 로그에 기록하고 `null`을 반환하므로 다음 단계에서 정상적으로 처리할 수 있습니다.

## 단계 3: OCR 엔진 생성 및 구성

OCR 엔진은 인식할 언어를 알아야 합니다. 언어를 설정하면 정확도가 크게 향상되며, 특히 비영어 문서에서 효과적입니다.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**왜 중요한가:** 엔진을 시작하는 것은 비교적 무거운 작업이므로, 배치 처리를 하는 경우 한 번 생성하고 여러 이미지에 재사용하는 것이 좋습니다.

## 단계 4: OCR 수행 및 이미지 텍스트 변환

이미지가 로드되고 엔진이 준비되었으므로 인식 단계를 실행할 수 있습니다. 이것이 **OCR 수행 방법**의 핵심입니다.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**예외 상황 처리:** 이미지가 `null`인 경우, 메서드는 `NullPointerException`을 발생시키는 대신 빈 문자열을 반환합니다. 이는 사용자 제공 파일을 다룰 때 주변 코드의 견고성을 높입니다.

## 단계 5: 추출된 텍스트 표시

마지막으로, 결과를 콘솔에 출력하거나 다른 구성 요소(예: 데이터베이스 또는 UI 위젯)로 전달합니다.

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

`java OcrDemo sample.jpg` 명령으로 프로그램을 실행하면 콘솔에 인식된 문자가 표시됩니다. 이것으로 **convert image to text** 사이클이 완료됩니다.

### 예상 출력

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

이미지에 읽을 수 있는 문자가 없으면 프로그램은 `(no text detected)`를 출력합니다.

## 일반적인 변형 및 적용 방법

| 변형 | 변경 내용 | 사용 시점 |
|-----------|--------------|-------------|
| **Different language** | `"eng"`를 스페인어는 `"spa"`, 프랑스어는 `"fra"` 등으로 교체합니다. | 영어가 아닌 언어로 작성된 문서 |
| **Batch processing** | 파일 경로 목록을 순회하고 동일한 `Ocr` 인스턴스를 재사용합니다. | 대량의 스캔 페이지 |
| **Higher accuracy** | 숫자 전용 스캔을 위해 `Ocr.SPEED_SLOW`를 사용하거나 `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")`를 활성화합니다. | OCR 품질이 중요한 경우(예: 청구서 번호) |
| **Tesseract alternative** | import를 `net.sourceforge.tess4j.Tesseract`로 교체하고 초기화 코드를 조정합니다. | 이미 Tesseract에 의존하는 프로젝트 |

## 전문가 팁

* **엔진에 전달하기 전에 큰 이미지를 리사이즈**하십시오; OCR 속도는 픽셀 수에 비례합니다.
* **이미지를 전처리**(그레이스케일, 대비 강화)하십시오. 소스가 노이즈가 많을 경우 OpenCV와 같은 라이브러리를 사용합니다.
* **OCR 엔진을 캐시**하십시오. 짧은 시간에 여러 번 호출하는 경우 엔진 시작·중지가 오버헤드를 발생시킵니다.
* **정규식으로 결과를 검증**하십시오. 특정 형식(예: 날짜, 전화번호)을 기대할 때 유용합니다.

## 결론

이제 Java에서 이미지에 **OCR 수행 방법**을 파일 읽기부터 추출된 텍스트 표시까지 알게 되었습니다. 이 튜토리얼은 **read image Java**, **extract text image**, **convert image to text**, **image to text java** 기술을 다루었으며, 실제 상황에 적용할 수 있는 실용적인 팁을 제공했습니다.

이제 다음과 같이 활용할 수 있습니다:

* 업로드를 받는 웹 서비스에 OCR 단계를 통합합니다.
* 출력 결과를 검색 인덱스와 결합하여 스캔 문서에 대한 전체 텍스트 검색을 수행합니다.
* 다국어 지원이나 사용자 정의 문자 집합과 같은 고급 OCR 옵션을 탐색합니다.

코딩을 즐기시고, 사진을 검색 가능한 텍스트로 변환하는 재미를 느끼세요!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 동작 코드를 제공하여 추가 API 기능을 숙달하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Java에서 OCR 사용 방법 – 맞춤법 교정으로 이미지에서 텍스트 추출](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Aspose OCR을 사용한 Java 이미지 텍스트 변환 – 전체 가이드](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [Java에서 OCR을 위한 GPU 활성화 방법 – 이미지에서 텍스트 추출](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
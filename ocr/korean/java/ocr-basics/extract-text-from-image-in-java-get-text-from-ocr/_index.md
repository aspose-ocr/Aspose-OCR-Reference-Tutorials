---
category: general
date: 2026-05-25
description: Java에서 OCR을 사용하여 이미지에서 텍스트를 추출합니다. OCR을 위한 이미지 로드 방법, 사진에서 텍스트를 인식하는
  방법, 그리고 간단한 코드 예제로 OCR에서 텍스트를 얻는 방법을 배워보세요.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: ko
og_description: Java에서 이미지 텍스트를 추출하는 단계별 가이드. OCR을 위한 이미지 로드 방법, 사진에서 텍스트 인식, 그리고
  OCR로 텍스트를 효율적으로 얻는 방법을 배워보세요.
og_title: Java에서 이미지 텍스트 추출 – OCR로 텍스트 얻기
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java에서 이미지 텍스트 추출 – OCR로 텍스트 가져오기
url: /ko/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 이미지에서 텍스트 추출 – OCR로 텍스트 가져오기

이미지에서 텍스트를 **추출**해야 했지만 어떤 Java 라이브러리를 선택해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다. 영수증을 디지털화하거나, 제품 사진에서 일련 번호를 추출하거나, 혹은 재미있는 사이드 프로젝트를 진행하든, 사진을 편집 가능한 텍스트로 변환하는 것은 흔한 장애물입니다.

이 튜토리얼에서는 **OCR용 이미지 로드** 방법, 엔진 구성, 그리고 최종적으로 **사진에서 텍스트 인식**하는 전체 실행 가능한 예제를 단계별로 안내합니다. 이를 통해 몇 줄의 코드만으로 **OCR에서 텍스트 가져오기**를 할 수 있습니다. 모호한 참고 자료는 없습니다—필요한 모든 것이 여기 있습니다.

## 배울 내용

* Java에서 경량 OCR 엔진을 설정하는 방법.  
* 다양한 파일 경로를 처리하는 **OCR용 이미지 로드** 정확한 단계.  
* 영어가 아닌 경우 **이미지에서 텍스트 추출**을 위해 언어 설정이 중요한 이유.  
* 결과를 안전하게 출력하는 방법과 엔진이 아무 것도 반환하지 않을 때 대처 방법.  
* 가장 흔한 함정을 피하기 위한 몇 가지 전문가 팁.

이 가이드를 끝까지 따라오면 우크라이나어 문자가 포함된 JPEG(또는 PNG)를 읽고 인식된 문자열을 콘솔에 출력하는 독립 실행형 프로그램을 얻게 됩니다. 언어나 이미지를 자유롭게 교체해도 됩니다—모든 것이 모듈식으로 구성되어 있습니다.

---

![Java OCR 엔진을 사용한 이미지에서 텍스트 추출 흐름도](/images/extract-text-from-image-java.png)

*Alt text: Java에서 이미지에서 텍스트 추출 프로세스 흐름도*

## 사전 요구 사항

* **Java Development Kit (JDK) 11+** – 코드는 최신 모듈 시스템을 사용하지만, 약간의 수정으로 이전 버전도 동작합니다.  
* **Maven or Gradle** – OCR 라이브러리를 가져오기 위해 사용합니다(우리는 **Asprise OCR**을 경량의 무료 개발 옵션으로 사용할 것입니다).  
* 프로그램이 읽을 수 있는 위치에 샘플 이미지 파일(예: `ukrainian_sign.jpg`)을 배치합니다.  
* Java의 `main` 메서드와 예외 처리에 대한 기본적인 이해.

이 항목들을 갖추었다면 바로 시작할 수 있습니다. 그렇지 않다면 Oracle 또는 AdoptOpenJDK에서 JDK를 다운로드하고 간단한 Maven 프로젝트를 설정하세요—특별히 복잡할 필요는 없습니다.

## 1단계: OCR 의존성 추가

먼저, 빌드 도구에 OCR 엔진을 가져오도록 지시합니다. Maven의 경우 `pom.xml`에 다음을 추가하세요:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Gradle를 선호한다면, 동일한 내용은 다음과 같습니다:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

이 좌표들은 `OcrEngine`, `OcrLanguage`, 그리고 우리가 사용할 헬퍼 클래스를 포함하는 소형 JAR를 가져옵니다. 기본 라틴 및 키릴 문자 스크립트에는 추가 네이티브 바이너리가 필요하지 않습니다.

## 2단계: **이미지에서 텍스트 추출**을 위한 Java 클래스 생성

이제 실제 프로그램을 작성합니다. 아래 코드를 `src/main/java/com/example/ocr/` 디렉터리 아래 `ExtractTextDemo.java` 파일로 저장하세요.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### 이 구조가 작동하는 이유

* **Separate numbered blocks**는 흐름을 쉽게 따라갈 수 있게 해줍니다, 특히 **OCR용 이미지 로드** 또는 **사진에서 텍스트 인식** 위치를 찾을 때 유용합니다.  
* 이미지 로드와 인식 주변의 `try/catch`는 파일 경로가 잘못되었거나 OCR 엔진이 언어 데이터를 찾지 못할 때 프로그램이 정상적으로 종료되도록 합니다.  
* 언어를 일찍 설정(step 2)하면 비영어 스크립트의 정확도가 크게 향상됩니다. 나중에 다른 언어에 대해 **java image to text**가 필요하면 `OcrLanguage.UKRAINIAN`을 `OcrLanguage.ENGLISH`, `FRENCH` 등으로 교체하면 됩니다.

## 3단계: 프로그램 빌드 및 실행

프로젝트 루트에서 다음을 실행합니다:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Gradle를 사용하는 경우:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

`ukrainian_sign.jpg`에 텍스트 *«Ласкаво просимо»* (우크라이나어로 “환영합니다”)가 포함되어 있다고 가정하면, 다음과 같은 출력이 나타납니다:

```
=== OCR Result ===
Ласкаво просимо
```

이 출력은 여러분이 **이미지에서 텍스트 추출**과 **OCR에서 텍스트 가져오기**를 한 번에 성공적으로 수행했음을 확인시켜 줍니다.

## 4단계: 워크플로우 조정 – 실제 프로젝트에서 **Java 이미지에서 텍스트**로 변환

데모는 최소한이지만, 실제 애플리케이션은 종종 더 많은 것이 필요합니다:

| Scenario | What to Adjust | Reason |
|----------|----------------|--------|
| **배치 처리** | `List<Path>`를 순회하면서 각 결과를 데이터베이스에 저장합니다. | 수백 장의 사진이 있을 때 수작업을 줄여줍니다. |
| **다양한 이미지 형식** | `ImageIO.read(new File(path))`를 사용해 전처리한 뒤, `BufferedImage`를 `ocrEngine.getImage().loadFromBufferedImage(bufImg)`에 전달합니다. | PNG, BMP 또는 변환 후 PDF까지 처리합니다. |
| **성능 튜닝** | 조금 낮은 정확도가 괜찮다면 `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)`를 호출합니다. | 저사양 하드웨어에서 인식 속도를 높입니다. |
| **후처리** | 공백을 제거하고 일반적인 OCR 오인식(`0` → `O`, `1` → `I`)을 교체합니다. | 후속 데이터 품질을 향상시킵니다. |

이러한 변형은 핵심 아이디어인 **사진에서 텍스트 인식**을 유지하면서 프로덕션 워크로드에 대한 유연성을 제공합니다.

## 흔히 발생하는 문제와 전문가 팁

1. **잘못된 언어 설정** – step 2를 잊으면 엔진이 기본값으로 영어를 사용해 키릴 문자를 깨진 텍스트로 변환합니다. 항상 언어 코드를 다시 확인하세요.  
2. **이미지 품질 중요** – 저해상도 또는 흐릿한 사진은 정확도를 떨어뜨립니다. 필요하면 대비 강화나 이진화를 통해 전처리하세요.  
3. **파일 경로 특이점** – Windows에서는 백슬래시를 이스케이프해야 합니다(`C:\\images\\file.jpg`). `java.nio.file`의 `Path.of(...)`를 사용하면 이를 피할 수 있습니다.  
4. **메모리 누수** – `OcrEngine`은 네이티브 리소스를 보유합니다. 작업이 끝났을 때, 특히 장기 실행 서비스에서는 `ocrEngine.dispose()`를 호출하세요.  
5. **스레드 안전성** – 엔진은 기본적으로 스레드 안전하지 않습니다. 스레드당 별도 인스턴스를 만들거나 접근을 동기화하세요.

## 전체 작동 예제 (All‑In‑One)

아래는 IDE에 복사‑붙여넣기 할 수 있는 단일 파일입니다. `dispose()` 호출과 코드를 약간 깔끔하게 만드는 작은 헬퍼 메서드를 포함하고 있습니다.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

이 프로그램을 실행하면 앞서 보여준 동일한 콘솔 출력이 나타납니다. `OcrLanguage.UKRAINIAN`을 `OcrLanguage.ENGLISH` 또는 다른 지원 언어로 교체해 엔진이 어떻게 적응하는지 확인해 보세요.

## 결론

우리는 Java를 사용해 **이미지에서 텍스트 추출**에 필요한 모든 과정을 살펴보았습니다: OCR 의존성 추가부터 **OCR용 이미지 로드**까지,

## 관련 튜토리얼

- [Aspose OCR로 텍스트 이미지 인식 – 전체 Java OCR 튜토리얼](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Aspose.OCR를 사용한 언어별 이미지 텍스트 OCR 방법](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR BufferedImage를 사용한 Java 이미지 텍스트 변환](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-26
description: Aspose.OCR Java를 사용하여 검색 가능한 PDF 만들기 – 이미지 OCR을 로드하고, 기본 언어를 설정하며, 이미지에서
  텍스트를 추출하고 OCR PDF로 저장하는 방법을 배웁니다.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: ko
og_description: Aspose.OCR Java를 사용하여 검색 가능한 PDF 만들기. 이미지 OCR 로드, 기본 언어 설정, 이미지에서
  텍스트 추출 및 OCR PDF 저장에 대한 단계별 가이드.
og_title: Aspose.OCR으로 검색 가능한 PDF 만들기 – Java 가이드
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Aspose.OCR을 사용하여 검색 가능한 PDF 만들기 – Java 가이드
url: /ko/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR을 사용한 검색 가능한 PDF 만들기 – Java 가이드

스캔한 문서에서 **create searchable pdf**를 만들어야 했지만 어디서 시작해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아니라—많은 개발자들이 Java에서 OCR을 처음 다룰 때 같은 장벽에 부딪힙니다. 좋은 소식은 Aspose.OCR이 이미지 로드부터 기본 언어 설정, 최종적으로 OCR‑enabled PDF 저장까지 전체 파이프라인을 매우 간단하게 만들어 준다는 것입니다. 이 튜토리얼에서는 **extracts text from image**를 수행하고, **set primary language**를 설정하며, 마지막으로 모든 리더에서 열 수 있는 **save OCR pdf**로 마무리되는 완전하고 실행 가능한 예제를 단계별로 살펴보겠습니다.

우리는 또한 GPU 가속을 활성화하여 처리 속도를 높이고 혼합 언어 문서(Tamil + English)를 처리하는 등 몇 가지 실용적인 팁을 다룰 것입니다. 끝까지 진행하면 프로젝트에 바로 넣을 수 있는 견고하고 프로덕션‑ready 스니펫을 얻게 됩니다.

## 필요 사항

- **Java 17** (또는 최신 JDK; Aspose.OCR은 Java 8+를 지원합니다)
- **Aspose.OCR for Java** 라이브러리 (공식 사이트에서 다운로드하거나 Maven을 통해 추가)
- **license file** (또는 30일 체험판)
- 텍스트가 포함된 이미지 파일 (데모에서는 `sample-mixed-tamil-eng.jpg` 사용)

추가 프레임워크나 네이티브 종속성은 필요 없습니다—그냥 순수 Java와 Aspose.JAR만 있으면 됩니다.

---

## Step 1: 검색 가능한 PDF 만들기 – 프로젝트 설정

코드에 들어가기 전에 프로젝트가 **create searchable pdf** 파일을 만들 준비가 되었는지 확인해 봅시다.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** 버전 번호를 최신으로 유지하세요; 최신 릴리스에는 GPU 사용에 대한 성능 개선이 포함되는 경우가 많습니다.

이제 `RecentFeaturesDemo`라는 간단한 Java 클래스를 생성합니다. 이 클래스는 **load image OCR**을 수행하고 언어 설정을 구성하며 최종적으로 **save OCR pdf**를 저장하는 모든 로직을 담게 됩니다.

---

## Step 2: 이미지 OCR 로드 및 엔진 초기화

파이프라인에서 실제 첫 번째 단계는 **load image OCR**입니다. 이는 Aspose.OCR에 분석할 파일을 알려줍니다.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters:** GPU(`setUseGpu(true)`)를 활성화하면 최신 하드웨어에서 처리 시간을 최대 70 %까지 단축할 수 있으며, 병렬 처리를 통해 GPU가 바쁠 때 CPU가 유휴 상태가 되지 않도록 합니다.

---

## Step 3: 기본 언어 설정 (및 보조 언어 설정)

이 단계를 건너뛰면 Aspose.OCR이 언어를 추측하려고 시도하게 되며, 이는 더 느리고 정확도가 떨어집니다. 여기서는 **set primary language**를 Tamil으로 설정하고 English를 보조 언어로 추가하는 방법을 보여줍니다.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** 기본 언어는 인식 중에 사용되는 문자 집합과 사전에 영향을 줍니다. 보조 언어를 추가하는 것은 혼합 스크립트 문서(예: Tamil과 English 텍스트가 모두 포함된 영수증)에서 매우 중요합니다.  
> **Edge case:** 문서에 두 개 이상의 언어가 포함된 경우, 각 추가 언어에 대해 `addAdditionalLanguage(...)`를 호출할 수 있습니다.

---

## Step 4: 이미지 전처리 – 기울기 보정 및 노이즈 제거

스캔한 이미지에는 회전이나 배경 노이즈가 발생하는 경우가 많습니다. 전처리를 통해 OCR 엔진이 **extract text from image**를 보다 신뢰성 있게 수행하도록 도와줍니다.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** 이미지가 이미 깨끗하다는 것을 알고 있다면 `setDenoise(true)`를 생략하여 몇 밀리초를 절약할 수 있습니다.

---

## Step 5: 이미지 파일 로드

엔진이 준비되었으니, 분석하려는 파일을 지정합니다.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong?** Aspose.OCR은 명확한 `FileNotFoundException`을 발생시킵니다. 부드러운 오류 처리가 필요하면 호출을 try‑catch로 감싸세요.

---

## Step 6: OCR 실행 및 이미지에서 텍스트 추출

모든 설정이 완료되었으니 실제 인식을 실행할 시간입니다. 이 단계는 **extracts text from image**를 수행하고 PDF 생성에 필요한 데이터를 준비합니다.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

데모 이미지에 대한 일반적인 콘솔 출력은 다음과 같습니다:

```
வணக்கம் World
This is a mixed language sample.
```

Tamil 라인이 올바르게 렌더링되고 그 뒤에 English가 표시되는 것을 확인할 수 있습니다. 이는 **set primary language**를 정확히 설정했을 때 얻는 결과입니다.

---

## Step 7: OCR PDF 저장 – 최종 단계

이제 퍼즐의 마지막 조각인 **save OCR pdf**를 수행합니다. Aspose.OCR은 원본 이미지 위에 보이지 않는 텍스트 레이어를 삽입하여 PDF를 검색 가능하게 만들 수 있습니다.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

`searchable.pdf`를 Adobe Reader에서 열고 **Ctrl + F**를 눌러 Tamil과 English 단어를 모두 검색할 수 있습니다—바로 **create searchable pdf** 워크플로우가 제공하는 기능입니다.

---

## 전체 작동 예제 (복사‑붙여넣기)

아래는 그대로 컴파일하고 실행할 수 있는 전체 프로그램입니다. 자리 표시자 경로를 자신의 디렉터리로 교체하세요.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

다음 명령으로 실행합니다:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

콘솔에 추출된 텍스트가 출력되고, **searchable pdf**가 디스크에 저장되었다는 확인 메시지가 표시될 것입니다.

---

## 일반적인 질문 및 엣지 케이스

### **load image OCR**를 바이트 배열에서 로드해야 하면 어떻게 하나요?

`ImageStream.fromFile(imagePath)`를 `ImageStream.fromBytes(byteArray)`로 교체하면 됩니다. 이는 이미지가 데이터베이스나 웹 서비스에서 올 때 유용합니다.

### 이미 이미지가 포함된 PDF를 어떻게 처리하나요?

Aspose.OCR은 PDF 페이지에서 직접 작업할 수 있습니다: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. 엔진은 인식 전에 각 페이지를 내부적으로 래스터화합니다.

### GPU가 감지되지 않음—`setUseGpu(true)`를 유지해야 하나요?

`setUseGpu(true)`가 실패하면 Aspose.OCR은 자동으로 CPU로 전환합니다. 활성화하기 전에 `ocrEngine.getEngineSettings().isGpuAvailable()`를 확인할 수 있습니다.

### **save OCR pdf**에 사용자 정의 메타데이터를 추가할 수 있나요?

예. 인식 후 `ocrEngine.getPdfSaveOptions().setTitle("My Document")` 또는 `setAuthor("John Doe")`를 호출하여 `save`하기 전에 설정하면 됩니다.

---

## 대량 배치 처리 성능 팁

- **Batch processing:** 여러 이미지에 동일한 `OcrEngine` 인스턴스를 재사용합니다. 실행 사이에 `ocrEngine.clear()`만 호출합니다.
- **Thread pool:** 각 이미지 작업을 `Callable`로 감싸 `ExecutorService`에 제출합니다. 병렬 처리를 활성화했기 때문에 각 스레드가 멀티코어 활용의 이점을 얻습니다.
- **Memory management:** 기가픽셀 이미지의 경우 `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)`로 다운샘플링을 고려하여 RAM 사용량을 적절히 유지합니다.

---

## 결론

우리는 이제 Aspose.OCR for Java를 사용한 전체 **create searchable pdf** 워크플로우를 살펴보았습니다. **load image OCR**부터 시작하여, 우리는 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
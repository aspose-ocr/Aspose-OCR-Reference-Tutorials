---
category: general
date: 2026-08-28
description: Aspose OCR을 사용하여 Java에서 png 이미지의 텍스트를 추출하는 방법을 배웁니다. 이 튜토리얼에서는 배치 OCR
  처리, 폴더에서 이미지 읽기, 확장자로 파일 필터링을 다룹니다.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Aspose OCR을 사용하여 Java에서 png 이미지의 텍스트를 추출하는 방법을 배웁니다. 이 튜토리얼에서는 배치
  OCR 처리, 폴더에서 이미지 읽기, 확장자로 파일 필터링을 다룹니다.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Java에서 png에서 텍스트 추출하는 방법 – 배치 OCR 가이드
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Java에서 png에서 텍스트 추출하는 방법 – 배치 OCR 가이드
url: /ko/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 png에서 텍스트 추출하기 – 배치 OCR 가이드

png 파일에서 **extract text from png** 를 추출해야 했지만 작업을 몇 장 이상의 사진으로 확장하는 방법을 몰랐다면, 여기가 바로 맞는 곳입니다. 많은 개발자들이 단일 이미지 OCR 호출로 시작하지만 폴더가 수십 개 또는 수백 개의 파일로 늘어날 때 성능 한계에 부딪히게 됩니다. Aspose OCR for Java를 사용하면 디렉터리를 순회하고, 필요한 이미지 유형만 필터링하고, 인식을 병렬로 수행하며, 결과를 원본 파일과 동일한 순서로 반환하는 견고한 배치 OCR 파이프라인을 구축할 수 있습니다. 이 가이드를 끝까지 읽으면 **batch OCR processing** 을 안정적이고 효율적으로 처리하는 바로 사용할 수 있는 Java 코드 조각을 얻게 됩니다.

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## 빠른 답변
- **OCR을 처리하는 라이브러리는 무엇인가요?** Aspose OCR for Java.
- **PNG와 JPG를 함께 처리할 수 있나요?** Yes – the sample filters both extensions.
- **OCR 엔진이 스레드‑안전한가요?** A single shared `AsposeOCR` instance is safe for concurrent use.
- **테스트에 라이선스가 필요합니까?** A free temporary key is available from Aspose.
- **하위 폴더가 자동으로 스캔됩니까?** `Files.walk` traverses the whole tree recursively.

## extract text from png이란?
`extract text from png`는 포터블 네트워크 그래픽(PNG) 파일에 광학 문자 인식(OCR)을 적용하여 보이는 문자를 검색 가능하고 편집 가능한 문자열로 만드는 과정을 의미합니다. Aspose OCR 엔진은 픽셀 데이터를 읽고, 글리프 형태를 식별하며, 단일 메서드 호출로 유니코드 텍스트를 반환합니다.

## 왜 Aspose OCR for Java를 사용하나요?
Aspose OCR은 **30+ languages**를 지원하고, 표준 8코어 서버에서 **500 images per minute**까지 처리하며, 전체 이미지를 메모리에 로드하지 않고도 **200 MB**까지의 파일을 처리할 수 있습니다. 이러한 정량화된 기능 덕분에 메모리 한계에 부딪히지 않고 일반 하드웨어에서 대규모 배치 작업을 신뢰성 있게 실행할 수 있습니다.

## 전제 조건
- Java 17 (또는 최신 LTS 버전).
- Maven 또는 Gradle을 사용한 의존성 관리.
- 처리하려는 PNG/JPG 이미지가 들어 있는 디렉터리.
- `java.nio.file` 패키지와 Java 스트림에 대한 기본적인 이해.
- (선택 사항) 평가용 Aspose OCR 임시 라이선스 키.

> **Pro tip:** 무료 임시 키는 30일 후에 만료되지만, 테스트를 위한 전체 API 접근 권한을 제공합니다.

## 배치 OCR 파이프라인은 어떻게 순서를 유지하나요?
`Future<OcrResult>`는 처리가 완료되면 가져올 수 있는 대기 중인 OCR 결과를 나타냅니다. 파이프라인은 입력 `Path` 컬렉션의 순서를 반영하는 리스트에 `Future<OcrResult>` 객체를 저장함으로써 원본 파일 순서를 유지합니다. 이후 futures를 순회하며 `get()`을 호출하면 각 호출은 해당 이미지에 대해서만 차단되므로, 별도의 정렬 로직 없이 출력 순서가 입력 순서와 일치합니다.

## Aspose OCR for Java란?
`AsposeOCR`는 모든 언어 팩, 인식 설정 및 내부 네이티브 리소스를 캡슐화하는 Aspose OCR 라이브러리의 핵심 클래스입니다. 애플리케이션 수명 동안 한 번만 인스턴스화되도록 설계되었으며 여러 스레드에서 안전하게 공유될 수 있습니다. 언어 데이터를 한 번만 로드하기 때문에 동일한 인스턴스를 재사용하면 초기화 오버헤드가 감소하고 배치 작업의 처리량이 향상됩니다.

## 프로젝트 설정 및 Aspose OCR 추가 방법
먼저 Maven(또는 Gradle) 프로젝트를 생성하고 `pom.xml`에 Aspose OCR 의존성을 추가합니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Why this matters:** 의존성을 미리 선언하면 컴파일러가 `AsposeOCR`, `ParallelRecognizer` 및 관련 클래스를 인식할 수 있습니다. 또한 모든 머신에서 동일한 버전을 사용하도록 보장하여 재현 가능한 **batch OCR processing** 에 필수적입니다.

빌드가 완료된 후 IDE를 새로 고치면 이제 **External Libraries** 아래에 Aspose 패키지가 표시됩니다.

## OCR 엔진 초기화 방법 – 단일 인스턴스 공유
`AsposeOCR`는 Aspose OCR 라이브러리가 제공하는 주요 OCR 엔진 클래스입니다. 전체 실행 동안 **one** OCR 엔진 인스턴스만 필요합니다. 이를 스레드 간에 공유하면 언어 팩을 한 번만 로드하기 때문에 메모리를 절약하고 속도가 빨라집니다.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR`는 스레드‑안전하므로 작업자 스레드 풀을 관리하는 `ParallelRecognizer`에 안전하게 전달할 수 있습니다.

> **Explanation:** `ParallelRecognizer`는 엔진을 스레드‑풀로 감싸습니다. 많은 파일을 제출하면 각 파일마다 별도의 작업자 스레드가 할당되어 다중 코어 CPU에서 진정한 병렬 처리가 가능해집니다.

## 폴더에서 이미지 읽기 – 디렉터리 트리 순회
`Files.walk`는 파일 트리를 재귀적으로 순회하고 `Path` 객체 스트림을 반환하는 Java NIO 메서드입니다. 이제 **read images from folder** 하고 모든 PNG 또는 JPG를 수집해야 합니다. `Files.walk` API를 사용하면 한 줄로 구현할 수 있지만, 필요할 때만 **extract text from png** 를 필터링하도록 추가하겠습니다.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Why we filter here:** `filter`를 사용하면 **filter files by extension** 을 미리 수행할 수 있어 이후 불필요한 I/O를 크게 줄입니다. 또한 코드를 읽기 쉽게 유지하며 복잡한 정규식이 필요하지 않습니다.

## OCR 작업을 비동기적으로 제출하는 방법
`recognizeAsync`는 이미지를 OCR 엔진에 비동기 처리로 제출하고, 대기 중인 결과를 나타내는 `Future<OcrResult>`를 반환합니다. 파일 목록이 준비되면 각 경로를 `ParallelRecognizer`에 전달합니다. `recognizeAsync` 메서드는 나중에 가져올 수 있도록 `Future<OcrResult>`를 반환합니다.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **What’s happening under the hood?** 각 호출은 인식기의 내부 executor 서비스에 작업을 큐에 넣습니다. 작업은 병렬로 실행되므로 100개의 이미지가 있는 폴더도 단일 스레드 루프가 걸리는 시간의 일부만에 처리될 수 있습니다.

## 파일 순서를 유지하면서 결과를 가져오는 방법
`Future<OcrResult>`는 비동기 OCR 작업의 결과를 보관하며, 인식된 텍스트를 얻기 위한 `get()` 메서드를 제공합니다. futures를 `imagePaths`와 동일한 순서로 저장했기 때문에 리스트를 순회하며 `get()`을 호출하면 됩니다. 호출은 해당 이미지가 완료될 때까지만 차단되므로 추가적인 관리 없이도 순서를 유지합니다.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**샘플 콘솔 출력** (truncated for brevity):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Edge case handling:** 특정 이미지에서 예외(손상된 파일, 지원되지 않는 형식)가 발생하면 이를 잡아내고 나머지 처리를 계속합니다—신뢰할 수 있는 **batch OCR processing** 파이프라인에 필수적인 습관입니다.

## 리소스 정리 방법 – 인식기 종료
`ParallelRecognizer.shutdown()`은 내부 스레드 풀을 중지시켜 애플리케이션이 종료되기 전에 모든 OCR 작업이 완료되도록 보장합니다. 내부 스레드 풀을 종료하는 것을 절대 잊지 마세요; 그렇지 않으면 JVM이 종료 시 멈출 수 있습니다.

```java
recognizer.shutdown();
```

이게 전부입니다! 이제 프로그램은 어떤 디렉터리든 순회하고, PNG/JPG 파일을 필터링하며, OCR을 병렬로 실행하고, 결과를 원래 순서대로 출력합니다.

---

## 전체 작업 예제 (복사‑붙여넣기)

아래는 완전한 실행 가능한 Java 클래스입니다. `"YOUR_DIRECTORY"`를 이미지 폴더 경로로 교체하고 IDE 또는 명령줄에서 실행하세요.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

클래스를 실행하면 콘솔에 추출된 문자열이 채워지는 것을 볼 수 있으며, I/O를 차단하는 단일 루프를 작성하지 않고도 **converted images to text** 를 수행했다는 사실을 축하하세요.

---

## 자주 묻는 질문 (FAQs)

**Q: PDF나 TIFF도 처리할 수 있나요?**  
A: 물론입니다. Aspose OCR은 PDF, TIFF, BMP, GIF 등을 포함한 30+ 포맷을 지원하므로 디렉터리‑walk 단계의 필터에 원하는 확장자를 추가하면 됩니다.

**Q: 영어가 아닌 다른 언어, 예를 들어 스페인어가 필요하면 어떻게 하나요?**  
A: `RecognitionLanguage.ENGLISH`를 `RecognitionLanguage.SPANISH`(또는 지원되는 다른 언어)로 변경하면 됩니다. 언어 팩은 라이브러리에 포함되어 있어 별도의 다운로드가 필요하지 않습니다.

**Q: 내 폴더에 하위 폴더가 있는데, 스캔되나요?**  
A: 네. `Files.walk`는 전체 트리를 재귀적으로 순회하므로 모든 중첩된 PNG/J

**Q: 200 MB를 초과하는 매우 큰 이미지를 어떻게 처리하나요?**  
A: `ocrEngine.setUseStreaming(true)`를 호출하여 스트리밍 모드를 활성화합니다. 이렇게 하면 엔진이 이미지를 청크 단위로 읽어 peak 메모리 사용량을 크게 줄입니다.

**Q: 동시 OCR 스레드 수를 제한하는 방법이 있나요?**  
A: 있습니다. `ParallelRecognizer`를 생성할 때 두 번째 인자로 원하는 최대 스레드 수를 전달하면 됩니다(예: `new ParallelRecognizer(ocrEngine, 4)`).

---

**마지막 업데이트:** 2026-08-28  
**테스트 대상:** Aspose OCR for Java 24.10  
**작성자:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## 관련 튜토리얼

- [Java 배치 OCR 처리 가이드: 이미지 텍스트 변환](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Java에서 이미지 텍스트 읽기: 완전 Aspose OCR 가이드](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Aspose.OCR을 사용한 이미지 텍스트 추출 – 허용 문자](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-01-02
description: Aspose OCR을 사용하여 Java로 이미지를 텍스트로 변환합니다. 배치 OCR 처리를 마스터하고, 폴더에서 이미지를 읽으며,
  확장자로 파일을 필터링합니다.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: ko
og_description: Java를 사용하여 이미지를 빠르게 텍스트로 변환하십시오. 이 튜토리얼에서는 배치 OCR 처리, 폴더에서 이미지 읽기
  및 확장자별 파일 필터링을 다룹니다.
og_title: Java에서 이미지를 텍스트로 변환 – 완전한 배치 OCR 가이드
tags:
- OCR
- Java
- Aspose
title: Java에서 이미지 텍스트 변환 – 배치 OCR 처리 가이드
url: /ko/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 이미지 → 텍스트 변환 – 배치 OCR 처리 가이드

수십 개의 파일을 한 번에 **이미지를 텍스트로 변환**해야 할 때가 있나요? 혼자가 아닙니다—개발자들은 PNG, JPG 등 스캔 파일에서 데이터를 추출하는 데 끊임없이 고민합니다. 좋은 소식은? Aspose OCR을 사용하면 몇 분 만에 배치 OCR 처리 파이프라인을 구축하고, 폴더 구조에서 이미지를 읽으며, 확장자로 파일을 필터링해 필요한 파일만 처리할 수 있습니다.

이 튜토리얼에서는 디렉터리를 순회하면서 모든 `.png`와 `.jpg` 파일을 찾아 Aspose OCR에 비동기적으로 전송하고, 추출된 텍스트를 원래 순서대로 출력하는 독립형 Java 프로그램을 만들겠습니다. 최종적으로 **이미지를 텍스트로 변환**하는 규모에 맞는 재사용 가능한 스니펫을 얻게 됩니다.

---

![이미지를 텍스트로 변환 예시](https://example.com/convert-images-to-text.png "PNG 파일에서 변환된 텍스트를 보여주는 Java 콘솔 출력 스크린샷")

## 만들게 될 내용

- 스레드 간에 공유되는 단일 `AsposeOCR` 엔진(효율적이고 스레드‑안전).  
- **배치 OCR 처리**에 최적화된 `ParallelRecognizer`로 OCR 작업을 병렬 실행.  
- `java.nio.file.Files`를 사용해 **폴더에서 이미지 읽기** 로직.  
- PNG 파일에서 **텍스트 추출**을 위한 간단한 필터, JPG도 동일하게 처리.  
- 리소스 누수를 방지하기 위한 내부 스레드 풀의 깔끔한 종료.

### 사전 요구 사항

- Java 17(또는 최신 LTS 버전).  
- Aspose OCR 라이브러리를 가져올 Maven 또는 Gradle.  
- 처리하고자 하는 PNG/JPG 이미지가 들어 있는 폴더.  
- Java 스트림에 대한 기본 지식—특별한 사전 지식은 필요 없습니다.

> **프로 팁:** 아직 라이선스가 없으시다면 Aspose에서 제공하는 무료 임시 키를 테스트용으로 사용할 수 있습니다.

---

## 1단계 – 프로젝트 설정 및 Aspose OCR 추가

먼저 새 Maven 프로젝트(또는 Gradle)를 만들고 `pom.xml`에 Aspose OCR 의존성을 추가합니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **왜 중요한가:** 의존성을 미리 선언하면 컴파일러가 `AsposeOCR`, `ParallelRecognizer` 및 관련 클래스를 인식합니다. 또한 모든 머신에서 동일한 버전을 사용하게 되어 재현 가능한 **배치 OCR 처리**에 필수적입니다.

빌드가 완료되면 IDE를 새로 고치고 `External Libraries` 아래에 Aspose 패키지가 보일 것입니다.

---

## 2단계 – 이미지 → 텍스트 변환 – OCR 엔진 초기화

전체 실행 동안 **하나**의 OCR 엔진 인스턴스만 필요합니다. 스레드 간에 공유하면 메모리를 절약하고 엔진이 언어 팩을 한 번만 로드하기 때문에 속도가 빨라집니다.

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

> **설명:** `ParallelRecognizer`는 엔진을 스레드‑풀에 래핑합니다. 많은 파일을 제출하면 각각 별도의 워커 스레드가 할당돼 멀티‑코어 CPU에서 진정한 병렬 처리가 가능합니다.

---

## 3단계 – 폴더에서 이미지 읽기 – 디렉터리 트리 순회

이제 **폴더에서 이미지 읽기**와 모든 PNG 또는 JPG 파일을 수집해야 합니다. `Files.walk` API를 사용하면 한 줄 코드로 구현할 수 있지만, 필요에 따라 **PNG에서만 텍스트 추출**하도록 필터를 추가하겠습니다.

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

> **왜 여기서 필터링하나요:** `filter`를 사용하면 **확장자로 파일 필터링**을 초기에 수행해 불필요한 I/O를 크게 줄일 수 있습니다. 또한 코드 가독성이 향상돼 복잡한 정규식이 필요 없습니다.

---

## 4단계 – 배치 OCR 처리 – 작업을 비동기적으로 제출

파일 목록이 준비되면 각 경로를 `ParallelRecognizer`에 전달합니다. `recognizeAsync` 메서드는 `Future<OcrResult>`를 반환하며, 나중에 결과를 가져오기 위해 저장합니다.

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

> **내부 동작:** 각 호출은 인식기의 내부 executor service에 작업을 큐에 넣습니다. 작업은 병렬로 실행되므로 100장의 이미지가 있는 폴더도 단일 스레드 루프보다 훨씬 짧은 시간에 처리됩니다.

---

## 5단계 – 원본 순서대로 결과 가져오기 – 파일 순서 유지

`imagePaths`와 같은 순서로 futures를 저장했으므로 리스트를 순회하면서 `get()`을 호출하면 됩니다. 해당 이미지가 완료될 때까지만 블록되므로 별도의 순서 관리 없이도 순서를 보장합니다.

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

**샘플 콘솔 출력**(간략히 표시):

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

> **예외 상황 처리:** 특정 이미지가 예외를 발생시켜도(손상 파일, 지원되지 않는 형식) 이를 잡아내고 나머지 파일 처리를 계속 진행합니다—신뢰할 수 있는 **배치 OCR 처리** 파이프라인에 필수적인 습관입니다.

---

## 6단계 – 정리 작업 – 인식기 종료

내부 스레드 풀을 반드시 종료하세요. 그렇지 않으면 JVM이 종료될 때 멈출 수 있습니다.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

이제 프로그램은 어떤 디렉터리든 순회하고, PNG/JPG 파일을 필터링하며, OCR을 병렬로 실행하고, 결과를 출력합니다.

---

## 전체 작업 예제

아래는 복사‑붙여넣기 바로 가능한 전체 Java 클래스입니다. `"YOUR_DIRECTORY"`를 이미지 폴더 경로로 바꾸고 IDE 또는 커맨드 라인에서 실행하세요.

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

클래스를 실행하면 콘솔에 추출된 문자열이 가득 채워지고, **이미지를 텍스트로 변환**했음에도 불구하고 I/O를 차단하는 루프를 하나도 작성하지 않은 사실을 축하하세요.

---

## 자주 묻는 질문 (FAQs)

**Q: PDF나 TIFF도 처리할 수 있나요?**  
A: 물론 가능합니다. Aspose OCR은 다양한 포맷을 지원하므로 Step 2의 필터에 해당 파일 확장자를 추가하면 됩니다.

**Q: 스페인어와 같이 다른 언어를 사용하려면?**  
A: `RecognitionLanguage.ENGLISH`를 `RecognitionLanguage.SPANISH`로 바꾸세요. 언어 팩이 설치되어 있어야 합니다(Aspose는 대부분의 주요 언어를 기본 제공).

**Q: 폴더에 하위 폴더가 있는데도 스캔되나요?**  
A: 네. `Files.walk`는 전체 트리를 재귀적으로 순회하므로 모든 중첩된 PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
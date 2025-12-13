---
date: 2025-12-13
description: Aspose.OCR for Java를 사용하여 언어 선택과 함께 이미지에서 텍스트를 추출하는 방법을 배웁니다. 이 단계별 Aspose
  OCR Java 튜토리얼은 정확한 OCR 구성을 보여줍니다.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR을 사용하여 언어 선택으로 이미지에서 텍스트 추출하는 방법
url: /ko/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 추출 및 언어 선택 방법 (Aspose.OCR 사용)

## Introduction

이미지 파일에서 텍스트를 추출하는 것은 스캔한 문서를 디지털화하거나 영수증을 처리하거나 검색 가능한 아카이브를 구축할 때 흔히 필요한 작업입니다. Aspose.OCR for Java는 이 작업을 간단하게 만들고 언어 선택, 기울기 보정, 인식 영역에 대한 세밀한 제어를 제공합니다. 이 튜토리얼에서는 **how to extract text from image** 를 특정 언어 설정과 함께 보여주는 완전한 실습 예제를 단계별로 안내합니다.

## Quick Answers
- **What library handles OCR in Java?** Aspose.OCR for Java  
- **Which setting selects the language?** `settings.setLanguage(Language.Eng)` (or any supported language)  
- **Do I need a license for development?** A free evaluation license works for testing; a commercial license is required for production.  
- **Can I limit OCR to a region of the image?** Yes, use `RecognitionSettings.setRecognitionAreas()` with rectangles.  
- **What is the typical runtime?** A few seconds per page on a standard laptop, depending on image size and language complexity.

## What is “extract text from image”?
이미지에서 텍스트를 추출하는 것(OCR)은 문자들의 시각적 표현을 기계가 읽을 수 있는 문자열로 변환합니다. 이를 통해 수동 전사 없이도 검색, 분석 및 데이터 추출 워크플로를 구현할 수 있습니다.

## Why use Aspose.OCR with language selection?
- **Multilingual support** – 이미지에 포함된 정확한 언어를 선택하여 정확도를 높일 수 있습니다.  
- **Fine‑tuned control** – 기울기 보정, 인식 영역 정의, 자동 기울기 동작 설정 등을 세밀하게 조정할 수 있습니다.  
- **Pure Java API** – 네이티브 의존성이 없으며 모든 Java 프로젝트에 쉽게 통합할 수 있습니다.  
- **Rich result data** – 한 번의 호출로 일반 텍스트, JSON, 경계 사각형 및 경고 정보를 모두 얻을 수 있습니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- **Java Development Kit (JDK)** installed (JDK 8 or later).  
- **Aspose.OCR for Java** library – download it from the official site [here](https://reference.aspose.com/ocr/java/).  
- 텍스트를 추출하려는 이미지 파일, 예: `p3.png`.

## Import Packages

Java 소스 파일에 필요한 Aspose.OCR 클래스와 표준 Java 유틸리티를 포함합니다:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Step‑by‑Step Guide

### Step 1: Set up Your Document Directory

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

`"Your Document Directory"`를 `p3.png` 파일이 위치한 절대 경로로 교체합니다.

### Step 2: Define the Image Path

```java
// The image path
String file = dataDir + "p3.png";
```

`file` 변수가 처리하려는 정확한 이미지 파일을 가리키도록 확인합니다.

### Step 3: Create Aspose.OCR API Instance

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` 객체를 통해 모든 OCR 작업에 접근할 수 있습니다.

### Step 4: Set Recognition Options (Language Selection)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

여기서는:

1. 수동 기울기 값을 제공하므로 자동 기울기 기능을 비활성화합니다.  
2. `RecognitionAreas` 사각형 영역을 정의하여 실제 텍스트가 포함된 이미지 부분만 OCR하도록 제한합니다.  
3. **language**를 영어(`Language.Eng`)로 설정합니다. 필요에 따라 `Language.Fra`, `Language.Spa` 등으로 변경하세요.

### Step 5: Perform OCR and Retrieve Results

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 호출이 이미지와 설정을 사용해 OCR 엔진을 실행합니다. 결과는 `RecognitionResult` 객체에 저장됩니다.

### Step 6: Print and Utilize Results

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

콘솔 출력에는 다음이 표시됩니다:

- 전체 추출 텍스트(`recognitionText`).  
- 각 사각형에 대한 텍스트(`recognitionAreasText`).  
- 경계 사각형 좌표.  
- 후속 처리에 용이한 JSON 표현.  
- 감지된 기울기 각도와 경고 메시지.

이제 `result.recognitionText`를 비즈니스 로직에 전달하여 저장, 인덱싱 또는 다른 서비스에 전달할 수 있습니다.

## Common Issues and Solutions

| Issue | Cause | Fix |
|-------|-------|-----|
| **Garbage characters** | Wrong language selected | Set the correct `Language` enum (e.g., `Language.Fra` for French). |
| **No text returned** | Recognition area does not cover the text | Adjust the `Rectangle` coordinates or remove `RecognitionAreas` to process the whole image. |
| **Slow performance** | Very large image or high resolution | Downscale the image before OCR or increase memory allocation for the JVM. |
| **Warnings about unsupported format** | Image format not recognized | Convert the image to PNG, JPEG, or TIFF before processing. |

## Frequently Asked Questions

**Q: Can I recognize multiple languages in a single OCR call?**  
A: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable multilingual recognition.

**Q: Which image formats does Aspose.OCR support?**  
A: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct file path.

**Q: Is there a size limit for the image?**  
A: There’s no hard limit, but very large images increase memory usage and processing time. Consider resizing large files.

**Q: How do I obtain a production license?**  
A: Purchase a license from the Aspose website and apply it via `License` class as shown in the Aspose documentation.

**Q: Can I extract text from a PDF page directly?**  
A: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g., using Aspose.PDF) and then run OCR.

## Conclusion

이제 Aspose.OCR for Java를 사용해 적절한 언어를 선택하고 인식 영역을 제한하면서 **extract text from image** 를 수행하는 방법을 확인했습니다. 이 접근 방식은 정확하고 고성능의 OCR을 제공하여 문서 관리 시스템부터 데이터 캡처 파이프라인까지 모든 Java 기반 워크플로에 쉽게 통합할 수 있습니다.

---

**Last Updated:** 2025-12-13  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
date: 2025-12-06
description: Aspose.OCR for Java를 사용하여 OCR 텍스트 인식을 수행하고, 이미지에서 텍스트를 추출하며, 대상 인식을 위한
  사각형을 준비하는 방법을 배웁니다.
language: ko
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR에서 OCR 텍스트 인식을 위한 사각형 준비
url: /java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR에서 OCR 텍스트 인식을 위한 사각형 준비

## Introduction

오늘날 데이터 중심의 세상에서 **ocr text recognition**은 스캔한 문서, 스크린샷 및 사진을 검색 가능하고 편집 가능한 콘텐츠로 변환하는 핵심 기술입니다. Aspose.OCR for Java는 특히 이미지의 특정 영역에 집중해야 할 때 이 과정을 빠르고 안정적으로 수행합니다. 이 튜토리얼에서는 OCR을 관심 영역으로 제한하는 사각형을 준비하는 모든 단계를 자세히 안내하여 정확한 제어와 향상된 성능을 제공합니다.

## Quick Answers
- **Java에서 OCR 텍스트 인식을 처리하는 라이브러리는?** Aspose.OCR for Java.  
- **프로덕션 사용에 라이선스가 필요합니까?** 예 – 유효한 Aspose.OCR 라이선스를 적용하면 전체 기능을 사용할 수 있습니다.  
- **이미지의 특정 부분에 OCR을 제한할 수 있나요?** 물론입니다; 대상 영역을 정의하는 사각형을 지정하면 됩니다.  
- **주요 전제 조건은 무엇인가요?** JDK 17+, Aspose.OCR for Java, 그리고 Java IDE.  
- **이 방법이 이미지에서 텍스트를 추출하는 데 적합한가요?** 예, **extract text image java** 프로젝트에 효율적인 방법입니다.

## What is OCR Text Recognition?
OCR(Optical Character Recognition) 텍스트 인식은 픽셀 기반 이미지를 기계가 읽을 수 있는 문자로 변환합니다. 이를 통해 원래 사진 형태로만 존재하던 콘텐츠를 검색, 편집 및 분석할 수 있습니다.

## Why Prepare Rectangles for OCR Text Recognition?
사각형을 정의하면 엔진이 실제 텍스트가 포함된 영역에만 집중하게 되어:
* 처리 시간이 단축됩니다.
* 잡음이 많은 배경을 무시함으로써 정확도가 향상됩니다.
* 필요한 데이터만 추출할 수 있어 양식, 청구서, 영수증 등에 최적입니다.

## Prerequisites

시작하기 전에 다음을 준비하세요:

- **Java Development Kit (JDK)** – Aspose.OCR for Java는 JDK 17 이상에서 작동합니다. Oracle 웹사이트에서 다운로드하세요.
- **Aspose.OCR for Java library** – 공식 다운로드 페이지에서 최신 JAR를 받으세요 [here](https://releases.aspose.com/ocr/java/). 설치 가이드는 [here](https://reference.aspose.com/ocr/java/)를 참고하세요.
- **Development Environment** – IntelliJ IDEA, Eclipse, VS Code 등 원하는 Java IDE를 사용하면 됩니다.

## Import Packages

Java 소스 파일에서 필요한 Aspose.OCR 클래스와 표준 Java 유틸리티를 import합니다:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *`java.awt.Rectangle`을 import하는 이유는 OCR API가 스캔할 영역을 정의하는 사각형을 기대하기 때문입니다.*

## Step 1: Set Up License

```java
SetLicense.main(null);
```

`SetLicense`를 호출하면 Aspose.OCR 라이선스가 활성화되어 평가 제한이 해제되고 전체 기능의 OCR 텍스트 인식을 사용할 수 있습니다.

## Step 2: Define Document Directory and Image Path

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

`"Your Document Directory"`를 이미지(`p.png`)가 위치한 절대 경로로 교체하세요. 이 이미지가 처리 대상입니다.

## Step 3: Create Aspose.OCR Instance

```java
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` 인스턴스를 생성하면 실제 OCR을 수행하는 `RecognizePage` 메서드에 접근할 수 있습니다.

## Step 4: Prepare Rectangles with Texts

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

각 `Rectangle(x, y, width, height)`는 Aspose.OCR에 텍스트를 찾을 정확한 위치를 알려줍니다. 좌표는 원본 이미지 레이아웃에 맞게 조정하세요.

## Step 5: Perform OCR Recognition

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 호출은 정의된 사각형만 처리하고 추출된 문자열을 반환합니다. 콘솔 출력으로 **ocr text recognition** 결과를 즉시 확인할 수 있습니다.

## Common Issues and Tips

| 문제 | 원인 | 해결책 |
|-------|-------|----------|
| **출력 없음** | 사각형 좌표 또는 이미지 경로가 잘못됨 | `dataDir` 값을 다시 확인하고 사각형이 실제 텍스트 영역을 포함하도록 하세요. |
| **깨진 문자** | 저해상도 이미지 또는 지원되지 않는 글꼴 | 고해상도 이미지를 사용하거나 이미지 전처리(예: 이진화)를 적용하세요. |
| **라이선스 적용 안 됨** | OCR 호출 전에 `SetLicense`를 호출하지 않음 | API 호출 전에 `SetLicense.main(null);`이 실행되는지 확인하세요. |
| **성능 저하** | 너무 많은 대형 사각형 | 사각형 수를 제한하고 텍스트 주변에 가능한 한 꼭 맞게 설정하세요. |

## Conclusion

이제 Aspose.OCR for Java를 통합하고, 라이선스를 설정하며, 이미지 경로를 정의하고—가장 중요한—특정 이미지 부분에 **ocr text recognition**을 집중시키는 사각형을 준비하는 방법을 배웠습니다. 이 기술은 정확하고 고성능 텍스트 추출이 필요한 모든 **java ocr tutorial**에 이상적입니다.

## Frequently Asked Questions

**Q: Aspose.OCR가 다른 프로그래밍 언어와 호환되나요?**  
A: 예,ose.OCR는 .NET, C++, Python도 지원합니다. 언어별 샘플은 공식 문서를 확인하세요.

**Q: Aspose.OCR를 상업 프로젝트에 사용할 수 있나요?**  
A: 물론입니다. [Aspose 스토어](https://purchase.aspose.com/buy)에서 상업 라이선스를 구매하세요.

**Q: 무료 체험판을 제공하나요?**  
A: 예, 체험 버전을 [here](https://releases.aspose.com/)에서 다운로드할 수 있습니다.

**Q: 평가용 임시 라이선스는 어떻게 얻나요?**  
A: 임시 라이선스는 [Aspose 임시‑라이선스 포털](https://purchase.aspose.com/temporary-license/)을 통해 제공됩니다.

**Q: 커뮤니티 지원은 어디서 받을 수 있나요?**  
A: 질문, 팁 및 코드 샘플은 Aspose.OCR [포럼](https://forum.aspose.com/c/ocr/16)에서 확인하세요.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

---
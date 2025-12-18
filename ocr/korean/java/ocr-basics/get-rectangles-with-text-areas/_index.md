---
date: 2025-12-10
description: Aspose.OCR for Java를 사용하여 이미지에서 텍스트를 인식하고 이미지에서 단락을 추출하는 방법을 배웁니다. 단계별
  가이드와 코드 예제.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: 이미지에서 텍스트를 인식하고 텍스트 영역 사각형을 가져오기
url: /ko/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 인식 및 텍스트 영역 사각형 가져오기

## 소개

Java 애플리케이션에서 **이미지 파일에서 텍스트를 인식**해야 할 경우, Aspose.OCR for Java는 빠르고 정확한 방법을 제공합니다. 이 튜토리얼에서는 이미지에서 단락을 추출하고, 각 텍스트 영역에 대한 경계 사각형을 얻은 뒤, 해당 좌표를 콘솔에 출력하는 정확한 단계를 살펴봅니다. 마지막까지 진행하면 이 접근 방식이 왜 작동하는지, 라이브러리를 어떻게 통합하는지, 그리고 자체 사용 사례에 맞게 어떻게 확장할 수 있는지 이해하게 됩니다.

## 빠른 답변
- **“이미지에서 텍스트를 인식한다”는 의미는?** 사진에 있는 시각적 문자를 편집 가능한 문자열 데이터로 변환하는 것을 의미합니다.  
- **Java에서 이를 처리하는 라이브러리는?** Aspose.OCR for Java.  
- **개발에 라이선스가 필요합니까?** 테스트용 임시 라이선스를 사용할 수 있으며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **단어가 아니라 단락을 추출할 수 있나요?** 예 – `AreasType.PARAGRAPHS`를 사용하면 단락 수준 사각형을 얻을 수 있습니다.  
- **코드가 Java 11+와 호환되나요?** 물론입니다. API는 Java 11 및 이후 버전에서 작동합니다.

## Aspose.OCR에서 “이미지에서 텍스트를 인식한다”는 의미
Aspose.OCR의 `RecognizePage` 메서드는 비트맵을 분석하고 OCR 알고리즘을 적용하여 인식된 문자열을 반환합니다. 텍스트 영역을 요청하면 라이브러리는 각 텍스트 블록에 대한 정확한 `Rectangle` 좌표도 계산해 주므로, 나중에 특정 섹션을 강조하거나 처리하기가 쉽습니다.

## 왜 Aspose.OCR for Java를 사용해야 할까요?
- **높은 정확도** – 다국어 및 복잡한 글꼴 지원.  
- **쉬운 통합** – 단일 JAR 파일 하나만 추가하면 전체 OCR 기능을 사용할 수 있습니다.  
- **유연한 출력** – 원시 텍스트, 포맷된 HTML, 혹은 정밀한 텍스트‑영역 사각형을 가져올 수 있습니다.  
- **스레드‑안전** – 고처리량 서버 환경에 적합합니다.

## 사전 요구 사항

- **Java Development Kit** (JDK 11 이상) 가 설치되어 있어야 합니다.  
- **Aspose.OCR for Java** 라이브러리 – 공식 사이트에서 [여기](https://releases.aspose.com/ocr/java/) 다운로드합니다.  
- IDE 또는 빌드 도구(Maven/Gradle) – JAR 의존성을 관리할 수 있어야 합니다.

## 패키지 가져오기

Java 프로젝트에서 필요한 클래스를 가져옵니다:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 단계별 가이드

### 단계 1: 프로젝트 설정
새 Java 프로젝트를 만들거나 기존 프로젝트에 추가하고 Aspose.OCR JAR를 클래스패스에 배치합니다. Maven을 사용하는 경우 다운로드 패키지에 설명된 대로 의존성을 추가합니다.

### 단계 2: 문서 디렉터리 및 이미지 경로 정의
샘플 이미지가 위치한 경로를 지정합니다:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 단계 3: Aspose.OCR 인스턴스 생성
OCR 엔진을 인스턴스화합니다:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### 단계 4: 이미지에서 텍스트 인식
`RecognizePage`를 호출해 그림을 일반 텍스트로 변환합니다. 이 단계가 **이미지에서 텍스트를 인식**하는 핵심 기능을 보여줍니다:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 단계 5: 텍스트 영역 사각형 가져오기
이제 각 단락(또는 다른 영역 유형)의 경계 사각형을 가져옵니다. 여기서 **이미지에서 단락을 추출**하고 좌표를 얻을 수 있습니다:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## 일반적인 문제 및 해결 방법

| 증상 | 가능한 원인 | 해결 방법 |
|------|-------------|-----------|
| `IOException` on `RecognizePage` | 파일 경로가 잘못되었거나 읽기 권한이 없음 | `imagePath`가 존재하는 PNG/JPG 파일을 가리키는지, 애플리케이션에 파일 시스템 접근 권한이 있는지 확인합니다. |
| 결과 문자열이 비어 있음 | 이미지 품질이 낮거나 지원되지 않는 언어 | 이미지 전처리(대비 증가, 이진화)를 수행하거나 `api.setLanguage("eng")`와 같이 올바른 언어를 지정합니다. |
| 사각형이 반환되지 않음 | 잘못된 `AreasType` 사용(`WORDS` 등) | 필요에 따라 `AreasType.PARAGRAPHS` 또는 `AreasType.LINES`로 전환합니다. |

## 자주 묻는 질문

**Q: Aspose.OCR가 Java 11과 호환되나요?**  
A: 예, Aspose.OCR는 Java 11 및 이후 버전에서 작동합니다.

**Q: 개인 및 상업 프로젝트 모두에 Aspose.OCR를 사용할 수 있나요?**  
A: 예, 모든 유형의 프로젝트에서 사용할 수 있습니다. 라이선스 상세는 [여기](https://purchase.aspose.com/buy)에서 확인하세요.

**Q: 평가용 임시 라이선스는 어떻게 얻나요?**  
A: 임시 라이선스는 [여기](https://purchase.aspose.com/temporary-license/)에서 받을 수 있습니다.

**Q: 커뮤니티 지원이나 공식 지원은 어디서 찾을 수 있나요?**  
A: 지원 및 토론은 [Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16)에서 확인하세요.

**Q: Aspose.OCR가 멀티스레딩을 지원하나요?**  
A: 예, 라이브러리는 스레드‑안전하며 동시 환경에서 성능을 높일 수 있습니다.

## 결론

이 튜토리얼을 통해 Aspose.OCR for Java를 사용해 **이미지에서 텍스트를 인식**하고, 단락을 추출하며, 각 텍스트 블록을 둘러싼 정확한 사각형을 가져오는 방법을 배웠습니다. 이러한 기능을 활용하면 검색 가능한 PDF를 만들거나 UI 오버레이에서 텍스트를 강조 표시하고, 구조화된 데이터를 후속 프로세스로 전달할 수 있습니다. 언어 설정을 맞춤화하거나 다양한 이미지 포맷을 처리하고, 클라우드 스토리지와 통합하는 등 API를 더 깊이 탐색해 보세요.

---

**마지막 업데이트:** 2025-12-10  
**테스트 환경:** Aspose.OCR 23.10 for Java  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
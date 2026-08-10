---
date: 2026-07-23
description: Aspose.OCR for .NET를 사용하여 이미지에서 텍스트를 추출하는 방법을 배우고, 사각형을 준비하여 OCR 정확도를
  향상시키고 이미지를 효율적으로 텍스트로 변환하는 방법을 알아보세요.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: OCR 이미지 인식에서 사각형 준비하기
og_description: Aspose.OCR for .NET를 사용하여 이미지에서 텍스트를 추출합니다. 사각형을 준비하고 OCR 정확도를 높이며
  이미지를 효율적으로 텍스트로 변환하는 방법을 배워보세요.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: 사각형을 사용한 이미지 텍스트 추출 – OCR 가이드
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: 사각형을 사용한 이미지 텍스트 추출 – OCR 가이드
url: /ko/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 사각형을 사용한 이미지 텍스트 추출 – OCR 가이드

## 소개

Optical Character Recognition (OCR)은 **이미지에서 텍스트를 추출**할 수 있게 하여 파일을 검색 가능하고 편집 가능하게 만듭니다. 이 튜토리얼에서는 정확히 필요한 영역에 엔진을 집중시키는 맞춤 사각형을 준비함으로써 OCR 정확도를 높이는 방법을 보여드립니다. Aspose.OCR for .NET을 사용하여 프로젝트 설정부터 인식된 문자열을 가져오는 전체 워크플로우를 확인하고, 어떤 .NET 애플리케이션에도 신뢰할 수 있는 이미지‑텍스트 변환 기능을 삽입할 수 있습니다.

## 빠른 답변
- **“extract text from image”가 무엇을 의미하나요?** 그림의 시각적 문자를 기계가 읽을 수 있는 문자열로 변환합니다.  
- **.NET에서 이를 처리하는 라이브러리는?** Aspose.OCR for .NET은 완전한 OCR 엔진을 제공합니다.  
- **프로덕션에 라이선스가 필요합니까?** 무료 체험은 개발에 사용할 수 있으며, 배포에는 상용 라이선스가 필요합니다.  
- **OCR을 특정 영역으로 제한할 수 있나요?** 예—유용한 텍스트가 포함된 영역만을 대상으로 사각형을 정의합니다.  
- **지원되는 .NET 버전은?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## 사각형을 사용한 “extract text from image”란 무엇인가요?
`extract text from image` 프로세스는 정의된 사각형 영역 내부의 문자만 읽고 나머지는 무시합니다. OCR을 해당 영역으로 제한하면 정확도가 높아지고 처리 속도가 빨라지며 후처리 작업이 줄어듭니다. 이 접근 방식은 배경 그래픽, 장식 요소 및 OCR 엔진을 혼란스럽게 할 수 있는 기타 시각적 노이즈를 배제하면서 필요한 텍스트만 분리합니다.

## OCR 전에 사각형을 준비하는 이유는?
사각형을 준비하면 OCR 엔진이 이미지에서 가장 관련성 높은 부분에 집중할 수 있어 속도와 정밀도가 모두 향상됩니다. 분석 영역을 좁히면 엔진이 검사해야 할 데이터 양이 감소하여 결과가 더 빠르게 나오고, 불필요한 시각적 혼란으로 인한 인식 오류가 줄어듭니다.

- **관련 콘텐츠에 집중:** 엔진을 혼란스럽게 할 헤더, 푸터 또는 장식 그래픽을 건너뜁니다.  
- **성능 향상:** 작은 영역은 계산량이 적어 대형 스캔에서 실행 시간을 최대 40 %까지 단축합니다.  
- **정확도 향상:** 시각적 노이즈를 줄이면 잡음이 많은 문서에서 문자 인식률이 ~85 %에서 >95 %로 상승합니다.

## 실제 프로젝트에서 이것이 중요한 이유
영수증, 청구서, 신분증 등 많은 비즈니스 문서는 텍스트와 로고 또는 바코드가 혼합되어 있습니다. 필요한 필드 주변에 사각형을 그리면 귀중한 데이터만 추출되어 후속 정제 작업이 크게 감소하고 자동화된 워크플로우의 신뢰성이 높아집니다. 이와 같은 목표 기반 추출은 후처리 노력을 줄이고 데이터 처리 표준 준수를 돕습니다.

## 일반적인 사용 사례
- **데이터 입력 자동화:** 스캔된 양식이나 영수증에서 특정 필드를 추출합니다.  
- **규정 준수 검사:** 검증을 위해 법적 조항이나 규제 문구를 분리합니다.  
- **콘텐츠 인덱싱:** 검색 엔진 가시성을 위해 이미지의 헤드라인이나 캡션만 인덱싱합니다.

## 전제 조건

- C# 및 .NET 개발에 대한 기본 지식.  
- Aspose.OCR for .NET 라이브러리 설치 – **[여기](https://releases.aspose.com/ocr/net/)**에서 다운로드하거나 모든 릴리스를 **[여기](https://releases.aspose.com/)**에서 확인하세요.  
- 추출하려는 텍스트가 포함된 샘플 이미지(예: `sample.png`).

## 네임스페이스 가져오기

`using` 문은 OCR 엔진 및 기하학 클래스를 범위에 포함시킵니다.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 단계 1: 문서 디렉터리 설정

이미지가 저장된 폴더를 지정하고 OCR 엔진 인스턴스를 생성합니다.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 여러 사각형을 사용하여 이미지에서 텍스트 추출하는 방법
이미지를 한 번 로드한 뒤 사각형 목록을 OCR 엔진에 전달합니다. 각 사각형은 관심 영역을 정의하고 엔진은 각 영역에 대해 별도의 문자열을 반환하므로 필드를 개별적으로 처리하고 필요에 따라 결과를 결합할 수 있습니다.

### 사각형 정의

`Rectangle` 객체는 스캔하려는 각 영역의 X‑Y 좌표와 크기를 설명합니다.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### OCR 인식 수행

`RecognizeImage` 메서드는 제공된 사각형 목록을 사용해 이미지를 처리하고 각 영역에 대한 인식된 텍스트를 반환합니다.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## RecognitionSettings를 사용하여 이미지에서 텍스트 추출하기 (대체 접근법)
설정 기반 호출을 선호한다면 `RecognitionSettings`를 사용해 동일한 결과를 얻을 수 있습니다. 이 객체는 사각형 정의를 언어, DPI 및 기타 OCR 옵션과 함께 하나의 객체에 묶어 깔끔한 단일 매개변수 API 호출을 제공합니다.

### 인식 설정 정의

`RecognitionSettings`를 사용하면 사각형 목록과 추가 옵션(예: 언어, DPI)을 하나의 객체에 묶을 수 있습니다.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 인식된 텍스트 표시

반환된 문자열을 순회하며 각 영역의 텍스트를 출력합니다.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## 일반적인 문제 및 팁

- **잘못된 사각형 좌표:** `X`, `Y`, `Width`, `Height`가 의도한 영역에 매핑되는지 확인하세요.  
- **이미지 품질:** 저해상도 또는 과도하게 압축된 이미지는 OCR 결과를 악화시킵니다; 이진화와 같은 전처리를 고려하세요.  
- **빈 결과:** 사각형에 실제로 읽을 수 있는 텍스트가 포함되어 있는지 확인하세요; 그렇지 않으면 엔진이 빈 문자열을 반환합니다.

## 문제 해결 및 모범 사례

| 증상 | 가능한 원인 | 해결책 |
|------|------------|--------|
| 출력 없음 또는 빈 문자열 | 사각형이 이미지 경계 밖에 있음 | 이미지 크기와 사각형 좌표를 다시 확인하세요 |
| 깨진 문자 | 대비 부족 또는 노이즈 | OCR 전에 그레이스케일 변환 및 임계값 적용 |
| 대용량 파일에서 느린 성능 | 사각형이 너무 많거나 이미지가 매우 큼 | 가능하면 이미지를 분할하거나 사각형 수를 줄이세요 |

## 결론

이제 Aspose.OCR for .NET을 사용해 맞춤 사각형을 준비함으로써 **이미지에서 텍스트를 추출**하는 방법을 알게 되었습니다. 이 접근 방식은 OCR 처리에 대한 정밀한 제어를 제공하여 모든 .NET 솔루션에 더 빠르고 정확한 텍스트 추출 기능을 제공합니다.

## 자주 묻는 질문

**Q:** Aspose.OCR for .NET을 다른 .NET 프레임워크와 함께 사용할 수 있나요?  
**A:** 예, Aspose.OCR for .NET은 .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7과 함께 작동합니다.

**Q:** 무료 체험을 이용할 수 있나요?  
**A:** 물론입니다! 체험판은 **[여기](https://releases.aspose.com/)**에서 다운로드하세요.

**Q:** Aspose.OCR for .NET에 대한 지원은 어디서 받을 수 있나요?  
**A:** 전용 지원을 위해 **[Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16)**을 방문하세요.

**Q:** 테스트용 임시 라이선스를 받을 수 있나요?  
**A:** 예, 임시 라이선스는 **[여기](https://purchase.aspose.com/temporary-license/)**에서 제공됩니다.

**Q:** 공식 문서는 어디에 있나요?  
**A:** 전체 API 레퍼런스는 **[여기](https://reference.aspose.com/ocr/net/)**에 있습니다.

---

**마지막 업데이트:** 2026-07-23  
**테스트 환경:** Aspose.OCR 24.11 for .NET  
**작성자:** Aspose  

{{< blocks/products/products-backtop-button >}}

## 관련 튜토리얼

- [OCR 이미지 인식에서 단락을 위한 사각형 추출 방법](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [OCR 이미지 수행 – OCR 이미지 인식에서 이미지에 OCR 수행](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Aspose.OCR for .NET을 사용해 이미지에서 텍스트 추출하는 방법](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
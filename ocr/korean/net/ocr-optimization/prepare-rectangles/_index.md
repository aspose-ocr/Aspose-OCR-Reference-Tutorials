---
date: 2025-12-22
description: Aspose.OCR for .NET을 사용하여 이미지에서 텍스트를 추출하는 방법을 배웁니다. 이 가이드는 OCR 이미지 인식을
  위한 사각형 준비와 정확도 향상 방법을 단계별로 안내합니다.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: OCR에서 사각형을 준비하여 이미지에서 텍스트 추출하는 방법
url: /ko/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 이미지 인식에서 사각형 준비하기

## 소개

광학 문자 인식(OCR)은 시각적 콘텐츠를 검색 가능하고 편집 가능한 텍스트로 변환하는 데 필수적입니다. 이 튜토리얼에서는 OCR 엔진이 특정 영역에 집중하도록 맞춤 사각형을 준비하여 **이미지에서 텍스트 추출**을 수행합니다. Aspose.OCR for .NET을 사용하여 프로젝트 설정부터 인식된 텍스트 검색까지 모든 단계를 안내하므로 .NET 애플리케이션에 강력한 이미지‑투‑텍스트 기능을 통합할 수 있습니다.

## 빠른 답변
- **“이미지에서 텍스트 추출”이 의미하는 것은?** 사진의 시각적 문자를 기계가 읽을 수 있는 문자열로 변환하는 것을 의미합니다.  
- **.NET에서 이를 지원하는 라이브러리는?** Aspose.OCR for .NET.  
- **개발에 라이선스가 필요합니까?** 테스트에는 무료 체험판을 사용할 수 있으며, 프로덕션에서는 라이선스가 필요합니다.  
- **특정 영역을 지정할 수 있나요?** 네, OCR 범위를 제한하는 사각형을 정의하면 됩니다.  
- **지원되는 .NET 버전은?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## 사각형을 사용한 “이미지에서 텍스트 추출”이란?

이미지에 사각형 영역을 정의하면 OCR 엔진은 해당 영역만 처리합니다. 이는 정확도를 높이고 처리 시간을 줄이며, 잡음이 많은 배경이나 관련 없는 부분을 무시할 수 있게 합니다.

## OCR 전에 사각형을 준비하는 이유는?

- **관련 콘텐츠에 집중:** 헤더, 푸터 또는 장식 그래픽을 건너뛰세요.  
- **성능 향상:** 작은 영역은 더 빠른 인식을 의미합니다.  
- **정확도 향상:** 시각적 잡음이 적을수록 결과가 더 깔끔해집니다.

## 사전 요구 사항

- C# 및 .NET 개발에 대한 기본 지식.  
- Aspose.OCR for .NET 라이브러리가 설치되어 있어야 합니다 – **[여기](https://releases.aspose.com/ocr/net/)**에서 다운로드할 수 있습니다.  
- 추출하려는 텍스트가 포함된 샘플 이미지(예: `sample.png`).

## 네임스페이스 가져오기

먼저, 필요한 네임스페이스를 범위에 가져옵니다:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 단계 1: 문서 디렉터리 설정

이미지 파일이 위치한 경로를 지정하고 OCR 엔진 인스턴스를 생성합니다.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 여러 사각형을 사용하여 이미지에서 텍스트 추출하는 방법

### 단계 2: 여러 사각형으로 이미지 인식

#### 2.1 사각형 정의

`Rectangle` 객체 리스트를 만들어 OCR 엔진이 스캔할 영역을 지정합니다.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 OCR 인식 수행

이미지 경로와 사각형 리스트를 `RecognizeImage`에 전달합니다. 이 메서드는 문자열 컬렉션을 반환하며, 각 항목은 하나의 사각형에 해당합니다.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### 단계 3: 인식 설정을 사용한 이미지 인식 (대체 접근법)

`RecognitionSettings`를 사용하는 것이 더 편하다면, 약간 다른 API 호출로 동일한 결과를 얻을 수 있습니다.

#### 3.1 인식 설정 정의

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 인식된 텍스트 표시

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## 일반적인 문제 및 팁

- **잘못된 사각형 좌표:** `X`, `Y`, `Width`, `Height` 값이 원하는 영역에 정확히 매핑되는지 확인하세요.  
- **이미지 품질:** 저해상도 이미지는 OCR 결과가 좋지 않을 수 있으니, 전처리(예: 이진화)를 고려하세요.  
- **빈 결과:** 사각형에 실제 텍스트가 포함되어 있는지 확인하세요; 그렇지 않으면 엔진이 빈 문자열을 반환합니다.

## 결론

이제 Aspose.OCR for .NET을 사용해 맞춤 사각형을 준비하여 **이미지에서 텍스트를 추출**하는 방법을 배웠습니다. 이 기술은 OCR 처리에 세밀한 제어를 제공하여 애플리케이션에서 더 빠르고 정확한 텍스트 추출 기능을 구축하는 데 도움이 됩니다.

## 자주 묻는 질문

**Q:** Aspose.OCR for .NET을 다른 .NET 프레임워크와 함께 사용할 수 있나요?  
**A:** 네, Aspose.OCR for .NET은 다양한 .NET 프레임워크와 호환됩니다.

**Q:** Aspose.OCR for .NET의 무료 체험판이 있나요?  
**A:** 물론입니다! 무료 체험판은 **[여기](https://releases.aspose.com/)**에서 이용할 수 있습니다.

**Q:** Aspose.OCR for .NET에 대한 지원은 어떻게 받나요?  
**A:** 전용 지원을 위해 **[Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16)**을 방문하세요.

**Q:** 테스트용 임시 라이선스를 받을 수 있나요?  
**A:** 네, 임시 라이선스는 **[여기](https://purchase.aspose.com/temporary-license/)**에서 획득할 수 있습니다.

**Q:** Aspose.OCR for .NET 문서는 어디서 찾을 수 있나요?  
**A:** 문서는 **[여기](https://reference.aspose.com/ocr/net/)**에서 확인할 수 있습니다.

---

**마지막 업데이트:** 2025-12-22  
**테스트 환경:** Aspose.OCR 24.11 for .NET  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
date: 2025-12-21
description: Aspose.OCR for .NET를 사용하여 OCR을 수행하고 이미지에서 텍스트를 추출하는 방법을 배웁니다. 이 단계별 가이드는
  다국어 텍스트 인식 및 언어 선택을 보여줍니다.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Aspose.OCR에서 언어 선택을 통한 OCR 수행 방법
url: /ko/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR에서 언어 선택으로 OCR 수행 방법

## 소개

OCR을 수행하고 .NET에서 이미지 파일의 텍스트를 추출해야 하는 경우, Aspose.OCR for .NET은 빠르고 안전한 언어 인식 이미지를 제공합니다. 이 튜토리얼에서는 언어 선택이 가능한 OCR 이미지 인식을 보여주는 실제 예제를 살펴보며 몇 줄 코드만 사진에서 다국어 텍스트를 추출할 수 있습니다.

## 빠른 답변
- **Aspose.OCR의 기능은 무엇입니까?** 이미지에서 인쇄된 텍스트와 손으로 쓴 텍스트를 인식하고 추출된 텍스트를 반환합니다.
- **언어를 선택할 수 있나요?** 예 – 영어, 독일어, 스페인어, 중국어 등 지원되는 언어를 지정할 수 있습니다.
- **개발을 위해 라이선스가 필요합니까?** 무료 평가판을 사용해 평가해 보세요. 프로덕션 용도로 사용하려면 라이센스가 필요합니다.
- **어떤 .NET 버전이 지원됩니까?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.
- **기울기 보정이 자동으로 이루어지나요?** `AutoSkew`를 활성화하고 `SkewAngle` 설정을 미세 조정할 수 있습니다.

## OCR 작업에 Aspose.OCR을 선택해야 하는 이유

- **다양한 글꼴과 이미지 품질에서 높은 정확도**를 제공합니다.

- **내장 언어 선택 기능**으로 외부 언어 팩이 필요 없습니다.

- **간단한 API**를 제공하여 기존 C# 프로젝트와 깔끔하게 통합됩니다.

- **외부 종속성 없음** – 모든 작업이 로컬에서 실행되므로 데이터 보안이 유지됩니다.

## 필수 조건

코드를 살펴보기 전에 다음 필수 조건을 충족하는지 확인하십시오.

- Aspose.OCR for .NET: Aspose.OCR 라이브러리가 설치되어 있는지 확인하십시오. [Aspose.OCR for .NET 다운로드 페이지](https://releases.aspose.com/ocr/net/)에서 다운로드할 수 있습니다.

- 개발 환경: .NET 애플리케이션이 포함된 개발 환경을 설정하십시오. 아직 이 작업을 수행하지 않았다면 자세한 지침은 [문서](https://reference.aspose.com/ocr/net/)를 참조하십시오.

## 네임스페이스 가져오기

.NET 애플리케이션에서 필요한 네임스페이스를 가져오는 것으로 시작하십시오.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1단계: Aspose.OCR 초기화

먼저 Aspose.OCR 클래스의 인스턴스를 초기화합니다. 이렇게 하면 애플리케이션에서 OCR 기능을 사용할 수 있는 기반이 마련됩니다.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 2단계: 이미지 경로 지정

다음으로 OCR을 수행할 이미지의 경로를 지정합니다. 애플리케이션에서 이미지에 접근할 수 있어야 합니다.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## 3단계: 언어 선택을 통한 이미지 인식

이제 핵심 OCR 작업이 진행됩니다. Aspose.OCR 라이브러리를 사용하여 지정된 이미지에서 텍스트를 인식합니다. 언어 선택을 포함한 인식 설정을 조정합니다.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## 4단계: 결과 출력 및 표시

OCR 작업이 완료되면 인식된 텍스트, 영역, 경고 및 JSON 표현을 포함한 결과를 출력하고 표시합니다.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## 일반적인 문제 및 팁

- **잘못된 언어 선택** – 출력 결과가 깨져 보이는 경우, `Language` 속성이 원본 이미지의 언어와 일치하는지 다시 확인하십시오.

- **기울어진 이미지** – 기울어진 스캔 이미지의 정확도를 높이려면 `AutoSkew`를 활성화하거나 `SkewAngle`을 수동으로 조정하십시오.

- **대용량 파일** – 메모리 사용량을 절약하려면 대용량 이미지를 여러 부분으로 나누어 처리하거나 `RecognizeImage` 함수에 입력하기 전에 해상도를 낮추십시오.

## 결론

축하합니다! Aspose.OCR for .NET을 사용하여 언어 선택 기능을 포함한 **OCR 수행 방법**을 배웠습니다. 이 튜토리얼에서는 이미지 파일에서 텍스트를 추출하고, 인식 설정을 사용자 지정하고, 다국어 콘텐츠를 손쉽게 처리하는 방법을 살펴보았습니다.

## 자주 묻는 질문

### Q1: Aspose.OCR은 다국어 텍스트 인식에 적합한가요?

A1: 네, Aspose.OCR은 다양한 언어를 지원하여 다국어 OCR 작업에 유연성을 제공합니다.

### 질문 2: 특정 이미지 특성에 맞춰 OCR 설정을 세밀하게 조정할 수 있나요?

답변 2: 네, 가능합니다! 기울기 각도, 선 인식, 영역 감지 등의 매개변수를 조정하여 다양한 시나리오에 맞게 OCR을 최적화할 수 있습니다.

### 질문 3: 추가 지원이나 커뮤니티 토론은 어디에서 찾을 수 있나요?

답변 3: 지원 및 커뮤니티 토론은 [Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16)에서 확인할 수 있습니다.

### 질문 4: 무료 체험판을 사용할 수 있나요?

답변 4: 네, [무료 체험판](https://releases.aspose.com/)을 통해 Aspose.OCR의 기능을 직접 경험해 보세요.

### 질문 5: Aspose.OCR for .NET은 어떻게 구매할 수 있나요?

답변 5: 구매하려면 [구매 페이지](https://purchase.aspose.com/buy)를 방문하세요.

---

**최종 업데이트:** 2025년 12월 21일
**테스트 환경:** Aspose.OCR 24.11 for .NET
**개발자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
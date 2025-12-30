---
date: 2025-12-30
description: Aspose.OCR를 사용하여 C#에서 이미지를 PDF로 변환하고, 다중 페이지 OCR 결과를 문서로 저장하며, 이미지에서
  텍스트를 추출하는 방법을 배워보세요.
linktitle: Convert Images to PDF C# – Save Multipage OCR Result
second_title: Aspose.OCR .NET API
title: 이미지를 PDF로 변환 C# – 다중 페이지 OCR 결과 저장
url: /ko/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지들을 PDF C# 로 변환 – 다중 페이지 OCR 결과 저장

## 소개

이 튜토리얼에서는 Aspose.OCR for .NET을 사용하여 **이미지를 PDF C# 로 변환**하고, 결과 다중 페이지 OCR 출력을 문서로 저장하는 방법을 배웁니다. 아카이빙을 위해 **스캔된 이미지를 PDF 로 변환**하거나 데이터 처리를 위해 **이미지에서 텍스트를 추출 C#**해야 할 경우, 이 가이드는 실제 예제와 모범 사례 팁을 포함하여 모든 단계를 안내합니다.

## 빠른 답변
- **이 튜토리얼에서 다루는 내용은?** Aspose.OCR을 사용하여 C#에서 여러 이미지를 PDF/Docx/Txt/Pdf/Xlsx 로 변환합니다.
- **지원되는 포맷은?** Docx, Text, Pdf, Xlsx (PDF를 직접 출력할 수도 있습니다).
- **라이선스가 필요한가요?** 평가용으로는 무료 체험판을 사용할 수 있으며, 프로덕션에서는 영구 라이선스가 필요합니다.
- **호환되는 .NET 버전은?** .NET Framework 4.5 이상, .NET Core 3.1 이상, .NET 5/6/7.
- **변환하면서 텍스트를 추출할 수 있나요?** 예—저장하기 전에 OCR 결과를 사용하여 텍스트를 추출할 수 있습니다.

## “이미지를 PDF C# 로 변환”이란?

C#에서 이미지를 PDF 로 변환한다는 것은 하나 이상의 비트맵 파일(PNG, JPEG, TIFF 등)을 프로그래밍 방식으로 가져와 시각적 레이아웃을 유지하면서 필요에 따라 OCR을 통해 검색 가능한 텍스트를 삽입한 PDF 문서를 생성하는 것을 의미합니다. Aspose.OCR은 이 과정을 간단하고 높은 수준으로 커스터마이징할 수 있게 해줍니다.

## 이 작업에 Aspose.OCR을 사용하는 이유

- **높은 정확도**: 다양한 언어를 지원하는 OCR 엔진.
- **다중 페이지 지원** – 한 번의 호출로 이미지 배치를 처리합니다.
- **직접 저장**: 추가 변환 단계 없이 인기 있는 오피스 포맷으로 저장합니다.
- **완전한 .NET 통합** – 네이티브 종속성이나 외부 도구가 필요 없습니다.

## 사전 요구 사항

시작하기 전에 다음 항목을 준비하십시오:

1. Aspose.OCR for .NET을 설치합니다. [여기](https://releases.aspose.com/ocr/net/)에서 다운로드할 수 있습니다.
2. 무료 체험판 또는 구매 라이선스를 획득합니다 – 체험판은 [여기](https://releases.aspose.com/)에서, 구매는 [여기](https://purchase.aspose.com/buy)에서 가능합니다.
3. 공식 [문서](https://reference.aspose.com/ocr/net/)를 검토하여 API를 익히십시오.
4. 문제 해결을 위해 [지원 포럼](https://forum.aspose.com/c/ocr/16) 커뮤니티에 참여하십시오.

모든 준비가 끝났으니 코딩을 시작해봅시다.

## 네임스페이스 가져오기

C# 파일에 필요한 네임스페이스를 추가합니다:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

이 임포트를 통해 컬렉션, 파일 처리, LINQ 및 Aspose OCR 클래스를 사용할 수 있습니다.

## 단계 1: 문서 디렉터리 설정

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

`"Your Document Directory"`를 소스 이미지가 위치한 절대 경로나 상대 경로, 그리고 출력 파일을 저장하려는 위치로 교체하십시오.

## 단계 2: Aspose.OCR 초기화

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

`AsposeOcr` 객체를 생성하면 **이미지를 PDF C# 로 변환** 워크플로우를 포함한 모든 OCR 작업에 접근할 수 있습니다.

## 단계 3: 이미지 인식

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` 메서드는 리스트의 각 파일을 처리하고 `RecognitionResult` 컬렉션을 반환합니다. 이미지 수에 제한이 없으며, 이는 **스캔된 이미지를 PDF 로 변환** 시나리오에 최적입니다.

## 단계 4: 원하는 형식으로 결과 저장

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

다음 워크플로우에 가장 적합한 형식을 선택하십시오:

- **Docx** – 검색 가능한 텍스트가 포함된 편집 가능한 Word 문서.
- **Text** – 빠른 데이터 마이닝을 위한 일반 텍스트 추출 (**이미지에서 텍스트를 추출 C#**).
- **Pdf** – 아카이빙에 적합한 고전적인 PDF 출력.
- **Xlsx** – 표형 데이터에 대한 스프레드시트 형태.

## 일반적인 사용 사례

- **디지털 아카이빙:** 스캔된 종이 계약서를 검색 가능한 PDF 로 변환합니다.
- **데이터 입력 자동화:** 영수증이나 청구서에서 텍스트를 추출하여 데이터베이스에 입력합니다.
- **배치 처리:** 최소한의 코드로 수천 개의 이미지를 한 번에 처리합니다.

## 문제 해결 및 팁

- **대용량 이미지 세트:** 메모리 급증을 방지하기 위해 이미지를 작은 배치로 처리합니다.
- **이미지 품질:** 최적의 OCR 정확도를 위해 이미지 해상도가 최소 300 dpi인지 확인하십시오.
- **라이선스 오류:** OCR 메서드를 호출하기 전에 라이선스 파일이 올바르게 로드되었는지 확인하십시오.

## 자주 묻는 질문 (Original)

### Q1: 테스트용 임시 라이선스를 제공하나요?

A1: 예, Aspose.OCR 테스트를 위해 [여기](https://purchase.aspose.com/temporary-license/)에서 임시 라이선스를 받을 수 있습니다.

### Q2: 다양한 포맷의 이미지에서 텍스트를 인식할 수 있나요?

A2: 물론입니다! Aspose.OCR은 다양한 이미지 포맷을 지원하여 OCR 작업의 유연성을 보장합니다.

### Q3: 인식 가능한 이미지 수에 제한이 있나요?

A3: 처리 가능한 이미지 수는 라이선스에 따라 다릅니다. 자세한 내용은 문서를 확인하십시오.

### Q4: OCR 인식 중 오류를 어떻게 처리하나요?

A4: 오류 처리 모범 사례는 문서를 참고하거나 지원 포럼에서 도움을 받으십시오.

### Q5: Aspose.OCR이 영어 외의 언어를 지원하나요?

A5: 예, Aspose.OCR은 다국어를 지원합니다. 언어 지원 세부 사항은 문서를 확인하십시오.

## 추가 자주 묻는 질문

**Q: OCR 없이 이미지들을 PDF C# 로 변환할 수 있나요?**  
A: 예, 순수 이미지‑to‑PDF 변환을 위해 Aspose.PDF 또는 다른 라이브러리를 사용할 수 있지만, OCR을 사용하면 검색 가능한 텍스트가 추가됩니다.

**Q: 변환 후 이미지에서 텍스트를 C# 로 추출하려면 어떻게 하나요?**  
A: `RecognizeMultipleImages`가 반환하는 `result` 리스트에는 `Text` 속성이 포함되어 있어 이를 `.txt` 파일에 저장하거나 직접 처리할 수 있습니다.

**Q: 사용자 정의 페이지 여백이나 방향을 설정할 수 있나요?**  
A: PDF 또는 Docx로 저장할 때 `SaveMultipageDocument`를 호출하기 전에 Aspose.Words 또는 Aspose.PDF API를 사용해 문서 레이아웃을 수정할 수 있습니다.

**Q: 이미지를 읽을 수 없으면 어떻게 되나요?**  
A: OCR 엔진은 해당 페이지에 대해 빈 `RecognitionResult`를 반환합니다; `result[i].Text`가 null 또는 빈 문자열인지 확인하고 적절히 처리할 수 있습니다.

**Q: API가 클라우드 배포를 지원하나요?**  
A: 예, 런타임 버전 요구 사항을 충족한다면 Azure Functions 및 AWS Lambda를 포함한 모든 .NET 런타임에서 라이브러리를 사용할 수 있습니다.

**마지막 업데이트:** 2025-12-30  
**테스트 환경:** Aspose.OCR 24.11 for .NET  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
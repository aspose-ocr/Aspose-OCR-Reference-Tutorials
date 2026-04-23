---
date: 2026-04-23
description: Aspose.OCR을 사용하여 C#에서 이미지를 PDF로 변환하고, 다중 페이지 OCR 결과를 문서로 저장하며, 이미지에서
  텍스트를 추출하는 방법을 배웁니다.
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: 이미지를 PDF로 변환 C# – 다중 페이지 OCR 결과 저장
second_title: Aspose.OCR .NET API
title: 이미지에서 텍스트 추출 – 이미지를 PDF로 변환 C#
url: /ko/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 추출 – 이미지 PDF C# 변환

## 소개

이 튜토리얼에서는 Aspose.OCR for .NET을 사용하여 **이미지에서 텍스트 추출** 및 **이미지 PDF C# 변환**을 수행하고, 다중 페이지 OCR 결과를 문서로 저장하는 방법을 알아봅니다. 아카이빙을 위해 **배치 이미지 PDF 변환**이 필요하거나, 규정 준수를 위해 **스캔된 이미지 PDF 변환**이 필요하거나, 사진에서 검색 가능한 텍스트를 추출하고 싶을 때, 명확한 설명과 실제 팁, 모범 사례 권장 사항과 함께 모든 단계를 안내합니다.

## 빠른 답변
- **이 튜토리얼은 무엇을 다루나요?** 여러 이미지를 PDF/Docx/Txt/Xlsx로 변환하고 Aspose.OCR을 사용하여 C#에서 이미지에서 텍스트를 추출합니다.  
- **지원되는 출력 형식은 무엇인가요?** Docx, Text, Pdf, 및 Xlsx (PDF를 직접 출력할 수도 있습니다).  
- **라이선스가 필요합니까?** 평가용으로는 무료 체험판을 사용할 수 있지만, 프로덕션에서는 영구 라이선스가 필요합니다.  
- **호환되는 .NET 버전은 무엇인가요?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **변환하면서 텍스트를 추출할 수 있나요?** 예—저장하기 전에 OCR 결과를 사용하여 텍스트를 추출합니다.

## “이미지에서 텍스트 추출”이란 무엇이며 PDF 변환과 결합하는 이유는?
이미지에서 텍스트를 추출한다는 것은 OCR(광학 문자 인식)을 사용하여 시각적인 문자를 검색 가능하고 편집 가능한 문자열로 변환하는 것을 의미합니다. **이미지 PDF C# 변환**을 하면 이러한 문자열을 PDF에 삽입하여 문서를 검색 가능하고 색인 가능하게 만들며, 디지털 아카이빙 및 데이터 마이닝에 최적입니다.

## 왜 이 작업에 Aspose.OCR을 사용하나요?
- **높은 정확도**를 수십 개 언어에 걸쳐 제공합니다.  
- **다중 페이지 지원** – 한 번의 호출로 이미지 배치를 처리합니다 (**배치 이미지 PDF 변환** 시나리오에 이상적).  
- **직접 저장**을 통해 추가 변환 단계 없이 인기 있는 오피스 형식으로 저장합니다.  
- **전체 .NET 통합** – 네이티브 종속성이 없으며 Windows, Linux 및 클라우드 런타임에서 작동합니다.

## 전제 조건

Before we dive in, make sure you have:

1. Aspose.OCR for .NET를 설치했습니다. [여기](https://releases.aspose.com/ocr/net/)에서 다운로드할 수 있습니다.  
2. 무료 체험판 또는 구매 라이선스를 획득했습니다 – 체험판은 [여기](https://releases.aspose.com/)에서, 구매는 [여기](https://purchase.aspose.com/buy)에서 받을 수 있습니다.  
3. 공식 [문서](https://reference.aspose.com/ocr/net/)를 검토하여 API를 익히세요.  
4. [지원 포럼](https://forum.aspose.com/c/ocr/16)에 가입하여 문제 해결 도움을 받으세요.  

이제 모든 준비가 끝났으니 코딩을 시작해봅시다.

## 네임스페이스 가져오기

C# 파일에 필요한 네임스페이스를 추가합니다:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

이러한 가져오기를 통해 컬렉션, 파일 처리, LINQ 및 Aspose OCR 클래스를 사용할 수 있습니다.

## 1단계: 문서 디렉터리 설정

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

`"Your Document Directory"`를 소스 이미지가 있는 절대 경로나 상대 경로, 그리고 출력 파일을 저장하려는 위치로 교체하세요.

## 2단계: Aspose.OCR 초기화

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

`AsposeOcr` 객체를 생성하면 모든 OCR 작업에 접근할 수 있으며, **이미지 PDF C# 변환** 워크플로우도 포함됩니다.

## 3단계: 이미지 인식

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` 메서드는 목록의 각 파일을 처리하고 `RecognitionResult` 컬렉션을 반환합니다. 원하는 만큼 많은 이미지를 제공할 수 있어 **스캔된 이미지 PDF 변환** 시나리오에 적합합니다.

## 4단계: 원하는 형식으로 결과 저장

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

다운스트림 워크플로에 가장 적합한 형식을 선택하세요:

- **Docx** – 검색 가능한 텍스트가 포함된 편집 가능한 Word 문서.  
- **Text** – 빠른 데이터 마이닝을 위한 일반 텍스트 추출 (**이미지에서 텍스트 추출**).  
- **Pdf** – 아카이빙에 이상적인 전통적인 PDF 출력.  
- **Xlsx** – 표 형식 데이터를 위한 스프레드시트 표현.

## 일반적인 사용 사례

- **디지털 아카이빙:** 스캔된 종이 계약서를 검색 가능한 PDF로 변환합니다.  
- **데이터 입력 자동화:** 영수증이나 청구서에서 텍스트를 추출하여 데이터베이스에 입력합니다.  
- **배치 처리:** 최소한의 코드로 수천 개의 이미지를 단일 작업으로 처리하여 **배치 이미지 PDF 변환** 요구에 완벽합니다.

## 문제 해결 및 팁

- **대용량 이미지 세트:** 메모리 급증을 방지하기 위해 이미지를 작은 배치로 처리하세요.  
- **이미지 품질:** 최적의 OCR 정확도를 위해 이미지 해상도가 최소 300 dpi인지 확인하세요.  
- **라이선스 오류:** OCR 메서드를 호출하기 전에 라이선스 파일이 올바르게 로드되었는지 확인하세요.  
- **빈 결과:** OCR 엔진은 읽을 수 없는 페이지에 대해 빈 `RecognitionResult`를 반환합니다; `result[i].Text`가 null 또는 빈 문자열인지 확인하고 적절히 처리하세요.

## 자주 묻는 질문

**Q: 이미지 PDF C# 변환을 OCR 없이 할 수 있나요?**  
A: 예, 순수 이미지‑PDF 변환을 위해 Aspose.PDF 또는 다른 라이브러리를 사용할 수 있지만 OCR을 사용하면 검색 가능한 텍스트가 추가됩니다.

**Q: 변환 후 C#에서 이미지에서 텍스트를 추출하려면 어떻게 해야 하나요?**  
A: `RecognizeMultipleImages`가 반환하는 `result` 리스트에는 `.txt` 파일에 쓸 수 있거나 직접 처리할 수 있는 `Text` 속성이 포함됩니다.

**Q: 맞춤 페이지 여백이나 방향을 설정할 수 있나요?**  
A: PDF 또는 Docx로 저장할 때 `SaveMultipageDocument`를 호출하기 전에 Aspose.Words 또는 Aspose.PDF API를 사용해 문서 레이아웃을 수정할 수 있습니다.

**Q: 이미지를 읽을 수 없는 경우 어떻게 되나요?**  
A: OCR 엔진은 해당 페이지에 대해 빈 `RecognitionResult`를 반환합니다; `result[i].Text`가 null 또는 빈 문자열인지 확인하고 적절히 처리할 수 있습니다.

**Q: API가 클라우드 배포를 지원하나요?**  
A: 예, 런타임이 버전 요구 사항을 충족한다면 Azure Functions 및 AWS Lambda를 포함한 모든 .NET 런타임에서 라이브러리가 작동합니다.

---

**최종 업데이트:** 2026-04-23  
**테스트 환경:** Aspose.OCR 24.11 for .NET  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
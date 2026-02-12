---
description: Aspose.OCR for .NET을 사용하여 OCR 결과를 저장하는 방법을 배우세요 – 이미지를 PDF로 변환하고, PNG에서
  텍스트를 추출하며, 인식된 텍스트를 DOCX, TXT, PDF 또는 XLSX 형식으로 저장합니다.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: OCR 결과를 문서로 저장하는 방법
url: /ko/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 결과를 문서로 저장하는 방법

## 소개

이 튜토리얼에서는 Aspose.OCR for .NET을 사용하여 **OCR 결과를 저장하는 방법**을 알아봅니다. 이미지에서 텍스트를 인식한 다음 해당 텍스트를 DOCX, TXT, PDF, XLSX와 같은 일반적인 문서 형식으로 변환하는 과정을 단계별로 안내합니다. 최종적으로 사진에서 데이터를 자동으로 추출하고 검색 가능하고 편집 가능한 파일로 저장할 수 있게 되며, 이는 아카이빙, 보고서 작성 또는 후속 처리에 적합합니다.

## 빠른 답변
- **“how to save ocr”가 무엇을 의미하나요?** 이미지에서 인식된 텍스트를 DOCX, PDF 등과 같은 파일 형식으로 저장하는 것을 의미합니다.  
- **어떤 형식으로 내보낼 수 있나요?** DOCX, TXT, PDF, XLSX를 기본적으로 지원합니다.  
- **라이선스가 필요합니까?** 평가용으로는 무료 체험판을 사용할 수 있으며, 실제 운영에서는 상용 라이선스가 필요합니다.  
- **이미지를 바로 PDF로 변환할 수 있나요?** 예—OCR 결과를 PDF로 저장하면 검색 가능한 PDF 문서를 얻을 수 있습니다.  
- **PNG를 지원하나요?** 물론입니다; 동일한 API를 사용하여 **PNG 이미지에서 텍스트를 추출**할 수 있습니다.

## OCR이란 무엇이며 결과를 문서로 저장하는 이유는?

광학 문자 인식(OCR)은 이미지 내의 인쇄된 텍스트나 손글씨를 기계가 읽을 수 있는 문자열로 변환합니다. 이러한 문자열을 문서로 저장하면 다음과 같은 이점을 얻을 수 있습니다:

* 규정 준수를 위해 검색 가능한 PDF를 생성합니다.  
* 데이터 분석을 위해 스프레드시트(XLSX)를 채웁니다.  
* 편집 가능한 보고서(DOCX)를 생성합니다.  
* 빠른 검색을 위해 일반 텍스트 로그(TXT)를 아카이브합니다.

## 필수 조건

시작하기 전에 다음이 준비되어 있는지 확인하십시오:

- Aspose.OCR for .NET이 설치되어 있어야 합니다. **[여기](https://releases.aspose.com/ocr/net/)**에서 다운로드할 수 있습니다.  
- 원본 이미지와 출력 문서를 보관할 폴더가 필요합니다. 코드의 `dataDir` 변수를 해당 폴더 경로로 업데이트하십시오.

## 네임스페이스 가져오기

.NET에서 파일 I/O와 Aspose OCR 클래스를 사용하려면 몇 가지 네임스페이스가 필요합니다.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### 1단계: Aspose.OCR 초기화

작업 디렉터리 경로를 설정하고 OCR 엔진 인스턴스를 생성합니다.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 2단계: 이미지 인식

이미지 파일(PNG 등)을 인식기에 전달합니다. 여기에서 **텍스트 이미지 인식**을 수행하고 이를 `RecognitionResult`로 변환합니다.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### 3단계: 결과를 다양한 형식으로 저장

이제 인식된 텍스트를 내보냅니다. 워크플로에 맞는 형식을 선택하십시오—**이미지를 PDF로 변환**하거나 **PNG에서 텍스트 추출**, 스프레드시트 생성 등.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### 4단계: 성공 메시지 표시

간단한 콘솔 메시지를 통해 프로세스가 오류 없이 완료되었음을 확인할 수 있습니다.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## 일반적인 함정 및 팁

- **파일 경로:** 항상 절대 경로를 사용하거나 `dataDir`이 경로 구분자(`\` 또는 `/`)로 끝나는지 확인하십시오.  
- **이미지 품질:** 고해상도 이미지가 정확도를 높이며, 전처리(기울기 보정, 노이즈 제거)를 고려하면 더 좋은 결과를 얻을 수 있습니다.  
- **라이선스 모드:** 평가 모드에서는 출력에 워터마크가 포함될 수 있으므로, 정식 라이선스를 적용하여 제거하십시오.

## 자주 묻는 질문

**Q1. Aspose.OCR이 다양한 이미지 형식을 지원하나요?**  
A1: 예, Aspose.OCR은 다양한 이미지 형식을 지원하여 OCR 작업의 유연성을 보장합니다.

**Q2. 정확도를 높이기 위해 인식 설정을 맞춤화할 수 있나요?**  
A2: 물론입니다! Aspose.OCR은 `RecognitionSettings`를 제공하여 특정 요구 사항에 맞게 OCR 프로세스를 세밀하게 조정할 수 있습니다.

**Q3. 무료 체험판이 있나요?**  
A3: 예, 무료 체험판을 **[여기](https://releases.aspose.com/)**에서 시작할 수 있습니다.

**Q4. Aspose.OCR 임시 라이선스를 어떻게 얻을 수 있나요?**  
A4: 임시 라이선스는 **[여기](https://purchase.aspose.com/temporary-license/)**에서 받을 수 있습니다.

**Q5. 도움을 받거나 커뮤니티와 연결하려면 어디에 가야 하나요?**  
A5: 지원 및 토론을 위해 **[Aspose Forum](https://forum.aspose.com/c/ocr/16)**에서 Aspose.OCR 커뮤니티에 참여하십시오.

---

**마지막 업데이트:** 2026-02-12  
**테스트 환경:** Aspose.OCR 24.11 for .NET  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
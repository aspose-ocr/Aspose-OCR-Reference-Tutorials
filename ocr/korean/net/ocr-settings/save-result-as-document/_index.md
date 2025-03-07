---
title: OCR 이미지 인식에서 결과를 문서로 저장
linktitle: OCR 이미지 인식에서 결과를 문서로 저장
second_title: Aspose.OCR .NET API
description: .NET용 Aspose.OCR의 잠재력을 활용해 보세요. 이미지 속 텍스트를 쉽게 인식하고 결과를 다양한 문서 형식으로 저장합니다.
weight: 10
url: /ko/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 이미지 인식에서 결과를 문서로 저장

## 소개

.NET용 Aspose.OCR을 사용하여 광학 문자 인식(OCR)의 흥미진진한 세계에 오신 것을 환영합니다! 이 포괄적인 튜토리얼에서는 Aspose.OCR을 사용하여 이미지의 텍스트를 인식하고 결과를 다양한 문서 형식으로 저장하는 방법을 보여주는 복잡한 과정을 살펴보겠습니다.

## 전제 조건

이 OCR 여정을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하십시오.

-  .NET용 Aspose.OCR. Aspose.OCR 라이브러리가 설치되어 있는지 확인하세요. 당신은 그것을 다운로드 할 수 있습니다[여기](https://releases.aspose.com/ocr/net/).

-  문서 디렉토리: 문서에 대한 지정된 디렉토리를 갖고 업데이트하십시오.`dataDir` 그에 따라 제공된 코드의 변수.

## 네임스페이스 가져오기

필요한 네임스페이스를 가져오는 것부터 시작하세요. 이는 OCR 기능으로 코드에 힘을 실어주는 구성 요소입니다.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

이제 예제를 여러 단계로 나누어 보겠습니다.

## 1단계: Aspose.OCR 초기화

```csharp
// 문서 디렉터리의 경로입니다.
string dataDir = "Your Document Directory";

// AsposeOcr 인스턴스 초기화
AsposeOcr api = new AsposeOcr();
```

이 단계에서는 Aspose.OCR API를 초기화하여 단계를 설정합니다.

## 2단계: 이미지 인식

```csharp
// 이미지 인식
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

여기서는 Aspose.OCR을 사용하여 지정된 이미지 내의 텍스트를 인식합니다("sample.png"를 이미지 파일로 대체).

## 3단계: 결과를 다른 형식으로 저장

```csharp
// 원하는 형식으로 결과를 저장하세요.
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

필요에 따라 이 단계를 사용자 정의하세요. Aspose.OCR을 사용하면 인식된 텍스트를 DOCX, TXT, PDF, XLSX 등 다양한 문서 형식으로 저장할 수 있습니다.

## 4단계: 성공 메시지 표시

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

문제 없이 프로세스가 완료되었음을 알려주는 간단한 확인 메시지입니다.

다음 단계를 수행하면 이미지 내의 텍스트를 인식하고 결과를 다양한 문서 형식으로 저장하는 데 .NET용 Aspose.OCR의 기능을 성공적으로 활용할 수 있습니다.

## 결론

결론적으로 .NET용 Aspose.OCR은 이미지의 텍스트 인식에 대한 가능성의 세계를 열어줍니다. 데이터를 추출하든 검색 가능한 문서를 생성하든 Aspose.OCR은 직관적인 API를 통해 프로세스를 단순화합니다.

## FAQ

### Q1. Aspose.OCR은 다른 이미지 형식과 호환됩니까?

A1: 예, Aspose.OCR은 다양한 이미지 형식을 지원하여 OCR 작업의 유연성을 보장합니다.

### Q2: 더 나은 정확성을 위해 인식 설정을 사용자 정의할 수 있습니까?

A2: 물론이죠! Aspose.OCR은 특정 요구 사항에 따라 OCR 프로세스를 미세 조정하기 위한 인식 설정을 제공합니다.

### Q3: 무료 평가판이 제공됩니까?

 A3: 예, 무료 평가판으로 시작할 수 있습니다.[여기](https://releases.aspose.com/).

### Q4: Aspose.OCR에 대한 임시 라이선스를 어떻게 얻을 수 있나요?

 A4: 임시 라이센스를 얻을 수 있습니다[여기](https://purchase.aspose.com/temporary-license/).

### 질문 5: 어디에서 도움을 구하거나 커뮤니티와 연결할 수 있나요?

 A5: Aspose.OCR 커뮤니티에 가입하세요.[Aspose 포럼](https://forum.aspose.com/c/ocr/16) 지원과 토론을 위해.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---
title: OCR 이미지 인식에서 폴더를 사용한 OCR 작동
linktitle: OCR 이미지 인식에서 폴더를 사용한 OCR 작동
second_title: Aspose.OCR .NET API
description: Aspose.OCR을 사용하여 .NET에서 OCR 이미지 인식 기능을 활용하세요. 이미지에서 텍스트를 손쉽게 추출해 보세요.
weight: 11
url: /ko/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 이미지 인식에서 폴더를 사용한 OCR 작동

## 소개

.NET용 Aspose.OCR을 사용하는 광학 문자 인식(OCR)의 세계에 오신 것을 환영합니다! .NET 애플리케이션 내에서 이미지에서 텍스트를 원활하게 추출하려는 경우 올바른 위치에 오셨습니다. 이 튜토리얼은 Aspose.OCR의 강력한 기능을 활용하여 폴더를 사용한 OCR 이미지 인식 프로세스를 안내합니다.

## 전제 조건

튜토리얼을 시작하기 전에 다음 전제조건이 충족되었는지 확인하십시오.

- C# 및 .NET 개발에 대한 실무 지식.
- 컴퓨터에 Visual Studio가 설치되어 있습니다.
-  다운로드할 수 있는 .NET 라이브러리용 Aspose.OCR[여기](https://releases.aspose.com/ocr/net/).
- OCR 개념에 대한 기본 이해.

## 네임스페이스 가져오기

C# 코드에서 Aspose.OCR을 사용하는 데 필요한 네임스페이스를 가져와야 합니다. 스크립트 시작 부분에 다음을 포함합니다.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1단계: 문서 디렉터리 설정

```csharp
// ExStart:1
// 문서 디렉터리의 경로입니다.
string dataDir = "Your Document Directory";
```

"문서 디렉토리"를 이미지가 저장된 실제 경로로 바꾸십시오.

## 2단계: Aspose.OCR 초기화

```csharp
// AsposeOcr 인스턴스 초기화
AsposeOcr api = new AsposeOcr();
```

해당 기능을 활용하려면 AsposeOcr 클래스의 인스턴스를 만듭니다.

## 3단계: 이미지 경로 지정

```csharp
//이미지 경로
string fullPath = dataDir + "OCR";
```

이미지가 포함된 특정 폴더와 문서 디렉터리 경로를 연결합니다.

## 4단계: 이미지 인식

```csharp
// 이미지 인식
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //기본값 또는 사용자 정의
});
```

RecognizeMultipleImages 메서드를 활용하여 지정된 폴더 내의 여러 이미지에 대해 OCR을 수행합니다.

## 5단계: 결과 인쇄

```csharp
// 결과 인쇄
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

결과를 반복하고 각 이미지에 대해 인식된 텍스트를 인쇄합니다.

## 6단계: 결론

```csharp
// 연장:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

폴더에 대한 OCR 작업이 성공적으로 실행되었음을 나타내려면 스크립트의 결론에 도달했는지 확인하세요.

## 결론

축하해요! .NET용 Aspose.OCR을 사용하여 폴더로 OCR 이미지 인식을 구현하는 방법을 성공적으로 배웠습니다. 이 강력한 도구는 .NET 애플리케이션의 이미지에서 텍스트를 추출할 수 있는 수많은 가능성을 열어줍니다.

## FAQ

### Q1: 상용 프로젝트에서 .NET용 Aspose.OCR을 사용할 수 있습니까?

 A1: 예, .NET용 Aspose.OCR은 상용 제품입니다. 라이선스 정보를 보려면 다음을 방문하세요.[여기](https://purchase.aspose.com/buy).

### Q2:. 무료 평가판이 제공되나요?

 A2: 예, 무료 평가판을 사용해 볼 수 있습니다.[여기](https://releases.aspose.com/).

### Q3: 문서는 어디서 찾을 수 있나요?

 A3: 문서를 사용할 수 있습니다.[여기](https://reference.aspose.com/ocr/net/).

### Q4: 임시 라이센스는 어떻게 얻을 수 있나요?

 A4: 임시 라이센스를 얻을 수 있습니다[여기](https://purchase.aspose.com/temporary-license/).

### Q5: 지원이 필요하거나 질문이 있나요?

 A5: 다음을 방문하세요.[Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16) 지역 사회 지원을 위해.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

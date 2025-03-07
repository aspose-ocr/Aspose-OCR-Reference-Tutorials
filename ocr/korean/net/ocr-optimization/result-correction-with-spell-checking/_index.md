---
title: OCR 이미지 인식에서 맞춤법 검사를 통한 결과 수정
linktitle: OCR 이미지 인식에서 맞춤법 검사를 통한 결과 수정
second_title: Aspose.OCR .NET API
description: .NET용 Aspose.OCR을 사용하여 OCR 정확도를 향상하세요. 철자를 수정하고, 사전을 사용자 정의하고, 오류 없는 텍스트 인식을 쉽게 달성할 수 있습니다.
weight: 13
url: /ko/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 이미지 인식에서 맞춤법 검사를 통한 결과 수정

## 소개

OCR(광학 문자 인식) 영역에서는 이미지에서 의미 있는 정보를 추출하려면 정확한 결과를 얻는 것이 중요합니다. 일반적인 과제 중 하나는 인식 프로세스에서 철자가 틀린 단어를 처리하는 것입니다. 다행히 .NET용 Aspose.OCR은 맞춤법 검사를 통해 OCR 결과를 향상시키는 강력한 솔루션을 제공합니다.

이 튜토리얼은 .NET용 Aspose.OCR을 사용하여 철자 검사를 통해 결과 수정 과정을 안내합니다. 결국에는 OCR 파생 텍스트의 정확성을 향상시켜 보다 세련되고 오류 없는 출력을 보장할 수 있게 됩니다.

## 전제 조건

맞춤법 검사 마법을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

-  .NET 라이브러리용 Aspose.OCR: 다음에서 Aspose.OCR 라이브러리를 다운로드하고 설치하세요.[릴리스 페이지](https://releases.aspose.com/ocr/net/).

- 문서 디렉터리: 문서에 대해 지정된 디렉터리가 있는지 확인하세요. 코드 조각의 "문서 디렉터리"를 실제 경로로 바꾸세요.

## 네임스페이스 가져오기

.NET 프로젝트에서 필요한 네임스페이스를 가져오는 것부터 시작해 보겠습니다.

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## 1단계: Aspose.OCR 초기화

OCR 프로세스를 시작하려면 Aspose.OCR 인스턴스를 초기화하세요.

```csharp
// 문서 디렉터리의 경로입니다.
string dataDir = "Your Document Directory";

// AsposeOcr 인스턴스 초기화
AsposeOcr api = new AsposeOcr();
```

## 2단계: 이미지 인식

다음으로 Aspose.OCR을 사용하여 이미지 속 텍스트를 인식합니다. 다음은 이 프로세스를 보여주는 스니펫입니다.

```csharp
// 이미지 인식
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## 3단계: 수정 전

수정 전 OCR 결과를 검색하여 수정된 버전과 비교합니다.

```csharp
// 결과 얻기
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## 4단계: 수정 후

올바른 결과를 얻으려면 맞춤법 검사를 적용하세요. 다음 코드 조각은 이 단계를 보여줍니다.

```csharp
// 수정된 결과 얻기
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## 5단계: 철자가 틀린 단어 및 제안

다음 코드를 사용하여 제안된 수정 사항과 함께 철자가 틀린 단어 목록을 가져옵니다.

```csharp
// 추천 단어와 함께 철자가 틀린 단어 목록 가져오기
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## 6단계: 사용자 텍스트 수정

Aspose.OCR 라이브러리를 사용하여 특정 사용자 제공 텍스트를 수정합니다.

```csharp
// 올바른 사용자 텍스트
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## 7단계: 사용자 사전으로 수정

사용자 정의 사용자 사전을 통합하여 수정 기능을 더욱 향상시킵니다.

```csharp
// 사용자 사전으로 수정된 결과 얻기
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## 결론

축하해요! .NET용 Aspose.OCR의 맞춤법 검사 기능을 성공적으로 탐색했습니다. 이 기능을 사용하면 OCR 결과를 구체화하여 정확성을 보장하고 오류를 제거할 수 있습니다.

## FAQ

### Q1: 영어 이외의 언어에도 Aspose.OCR을 사용할 수 있나요?

A1: 예, Aspose.OCR은 여러 언어를 지원합니다. 이에 따라 언어 설정을 조정하십시오.

### Q2: Aspose.OCR을 .NET 프로젝트에 어떻게 통합합니까?

 A2: 다음을 참조하세요.[선적 서류 비치](https://reference.aspose.com/ocr/net/) 자세한 통합 단계를 확인하세요.

### Q3: Aspose.OCR에 사용할 수 있는 평가판이 있습니까?

 A3: 예, 다음을 통해 기능을 탐색할 수 있습니다.[무료 평가판](https://releases.aspose.com/).

### Q4: 맞춤법 검사를 위해 사용자 정의 사전을 업로드할 수 있습니까?

A4: 물론이죠! 이 튜토리얼에서는 사용자가 제공한 사전을 사용하여 수정 기능을 향상시키는 방법을 보여줍니다.

### Q5: Aspose.OCR에 대한 지원은 어디서 구할 수 있나요?

 A5: 다음을 방문하세요.[Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16) 지역 사회의 지원과 지도를 위해.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

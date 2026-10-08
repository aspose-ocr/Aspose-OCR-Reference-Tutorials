---
date: 2026-02-22
description: Aspose.OCR for .NET을 사용하여 이미지에서 텍스트 라인을 인식하고 라인 사각형을 추출함으로써 레이아웃 분석 OCR을
  수행하는 방법을 배웁니다.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: 레이아웃 분석 OCR – 이미지에서 라인 사각형 얻기
url: /ko/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 레이아웃 분석 OCR – 이미지에서 라인 사각형 가져오기

## 소개

이 튜토리얼에서는 Aspose.OCR for .NET을 사용하여 **OCR 라인 사각형을 가져오는 방법**을 알아봅니다. 가이드를 마치면 **이미지에서 텍스트 라인을 인식**하고 **감지된 각 라인의 좌표를 추출**할 수 있게 됩니다—이는 **레이아웃 분석 OCR**, 데이터 추출, 맞춤 렌더링 등 후속 처리에 최적화된 기능입니다.

## 빠른 답변
- **“OCR 라인 사각형을 가져온다”는 무슨 의미인가요?** 이미지에서 감지된 각 텍스트 라인의 경계 상자를 반환합니다.  
- **사용되는 API 메서드는?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **라이선스가 필요한가요?** 개발 단계에서는 무료 체험판으로 가능하지만, 운영 환경에서는 상용 라이선스가 필요합니다.  
- **지원되는 이미지 포맷?** PNG, JPEG, BMP, TIFF 등 다양한 포맷을 지원합니다.  
- **.NET Core에서도 실행할 수 있나요?** 네, Aspose.OCR은 .NET Core 및 .NET 5/6을 완벽히 지원합니다.

## 사전 요구 사항

튜토리얼을 진행하기 전에 다음 요구 사항을 충족했는지 확인하세요:

- C# 및 .NET 개발에 대한 기본 지식.  
- Visual Studio와 같은 통합 개발 환경(IDE).  
- Aspose.OCR for .NET 라이브러리 설치. [여기](https://releases.aspose.com/ocr/net/)에서 다운로드할 수 있습니다.  
- OCR 인식을 위한 텍스트가 포함된 샘플 이미지.

## 네임스페이스 가져오기

프로젝트에 필요한 네임스페이스를 가져와야 합니다. C# 파일 상단에 다음 코드를 추가하세요:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

이제 OCR 이미지 인식에서 라인 사각형을 가져오는 과정을 단계별로 살펴보겠습니다.

## layout analysis ocr – 단계별 가이드

### 단계 1: 문서 디렉터리 설정

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

`"Your Document Directory"`를 실제 샘플 이미지가 들어 있는 폴더 경로로 교체합니다.

### 단계 2: Aspose.OCR 초기화

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

`AsposeOcr` 클래스의 인스턴스를 생성하여 OCR 기능에 접근합니다.

### 단계 3: 이미지 경로 지정

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

OCR을 수행할 이미지의 전체 경로를 정의합니다.

### 단계 4: 이미지 인식 및 사각형 가져오기

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles` 메서드는 `Rectangle` 객체 리스트를 반환하며, 각 객체는 감지된 텍스트 라인의 좌표를 나타냅니다. 이것이 **OCR 라인 사각형을 가져오는** 핵심이며 **레이아웃 분석 OCR**을 가능하게 합니다.

### 단계 5: 결과 출력

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

감지된 영역의 좌표를 콘솔에 출력합니다. 이후 **라인 좌표 추출**을 위한 맞춤 처리에 활용할 수 있는 값을 확인할 수 있습니다.

## Aspose.OCR을 라인 사각형에 사용하는 이유

- **높은 정확도** – 잡음이 많거나 기울어진 이미지에서도 라인을 정밀하게 감지합니다.  
- **크로스 플랫폼** – .NET Framework, .NET Core, .NET 5/6 모두에서 동작합니다.  
- **외부 종속성 없음** – 순수 .NET 라이브러리이며, 별도의 네이티브 DLL이 필요하지 않습니다.  
- **풍부한 출력** – 라인 사각형 외에도 단어, 문자, 신뢰도 점수를 가져올 수 있습니다.

## 일반적인 문제와 해결책

| 문제 | 해결책 |
|-------|----------|
| **사각형이 반환되지 않음** | 이미지에 명확한 가로 텍스트가 있는지 확인하고 `AreasType.LINES`가 지정되었는지 점검하세요. |
| **좌표가 부정확함** | 이미지 DPI를 확인하세요; 저해상도 이미지는 경계가 부정확할 수 있습니다. |
| **대용량 이미지에서 성능 저하** | `GetRectangles` 호출 전에 이미지를 적절한 해상도로 리사이즈하세요. |
| **라이선스 예외** | 테스트용으로는 체험 라이선스를 사용하고, 운영 환경에서는 정식 라이선스를 적용해 평가 제한을 피하세요. |

## 자주 묻는 질문

**Q: 전체 라인 대신 개별 단어를 추출할 수 있나요?**  
A: 네, 동일한 `GetRectangles` 메서드에 `AreasType.WORDS`를 지정하면 단어 수준의 경계 상자를 얻을 수 있습니다.

**Q: API가 다중 페이지 PDF를 지원하나요?**  
A: 각 PDF 페이지를 이미지로 변환한 뒤, 해당 이미지에 대해 `GetRectangles`를 호출하면 됩니다.

**Q: 회전된 텍스트는 어떻게 처리하나요?**  
A: OCR 설정에서 자동 회전 옵션을 활성화하거나, 처리 전에 이미지를 미리 회전시켜 주세요.

**Q: 각 라인에 대한 신뢰도 점수를 얻을 수 있나요?**  
A: 사각형을 얻은 뒤 `api.RecognizeImage(...).Lines`를 호출하면 신뢰도 값을 포함한 라인 객체에 접근할 수 있습니다.

**Q: 지원되는 .NET 버전은 무엇인가요?**  
A: .NET Framework 4.5 이상, .NET Core 3.1 이상, .NET 5/6을 지원합니다.

## 실제 활용 사례

- **문서 레이아웃 분석 OCR** – 라인 사각형을 레이아웃 엔진에 전달해 컬럼 구조를 재구성합니다.  
- **자동 데이터 추출** – 좌표를 활용해 개별 라인을 잘라내어 후속 NLP 파이프라인에 전달합니다.  
- **맞춤 렌더링** – 원본 이미지에 경계 상자를 오버레이하여 시각적 검증이나 UI 오버레이에 활용합니다.  

## 결론

축하합니다! Aspose.OCR for .NET을 사용해 이미지에서 **OCR 라인 사각형을 성공적으로 가져왔**습니다. 이제 경계 상자를 활용해 맞춤 렌더링, 데이터 추출, **레이아웃 분석 OCR** 등 다양한 후속 워크플로에 라인 좌표를 전달할 수 있습니다.

---

**마지막 업데이트:** 2026-02-22  
**테스트 환경:** Aspose.OCR 24.11 for .NET  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
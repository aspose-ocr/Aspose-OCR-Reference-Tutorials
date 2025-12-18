---
date: 2025-12-17
description: Aspose.OCR for .NET을 사용하여 이미지에서 텍스트 라인을 인식하고 라인 좌표를 쉽게 추출하는 방법을 배우고 OCR
  라인 사각형을 얻는 방법을 알아보세요.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: 이미지 텍스트 라인에 대한 OCR 라인 사각형 가져오기
url: /ko/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지 텍스트 라인에 대한 OCR 라인 사각형 가져오기

## 소개

이 튜토리얼에서는 Aspose.OCR for .NET을 사용하여 **OCR 라인 사각형을 가져오는 방법**을 배웁니다. 가이드를 마치면 **이미지에서 텍스트 라인을 인식**하고 감지된 각 라인에 대한 **라인 좌표를 추출**할 수 있게 됩니다—레이아웃 분석, 데이터 추출 또는 사용자 정의 렌더링과 같은 후속 처리에 적합합니다.

## 빠른 답변
- **“OCR 라인 사각형을 가져오기”가 의미하는 것은?** 이미지에서 감지된 각 텍스트 라인의 경계 상자를 반환합니다.  
- **사용되는 API 메서드는?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **라이선스가 필요합니까?** 개발에는 무료 체험판을 사용할 수 있으며, 운영 환경에서는 상용 라이선스가 필요합니다.  
- **지원되는 이미지 형식?** PNG, JPEG, BMP, TIFF 등.  
- **.NET Core에서 실행할 수 있나요?** 예, Aspose.OCR은 .NET Core 및 .NET 5/6을 완벽히 지원합니다.

## 전제 조건

튜토리얼을 시작하기 전에 다음 전제 조건이 준비되어 있는지 확인하십시오:

- C# 및 .NET 개발에 대한 기본 지식.  
- Visual Studio와 같은 통합 개발 환경(IDE).  
- Aspose.OCR for .NET 라이브러리가 설치되어 있어야 합니다. [여기](https://releases.aspose.com/ocr/net/)에서 다운로드할 수 있습니다.  
- OCR 인식을 위한 텍스트가 포함된 샘플 이미지.

## 네임스페이스 가져오기

프로젝트에 필요한 네임스페이스가 가져와졌는지 확인하십시오. C# 파일 상단에 다음 줄을 추가합니다:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

이제 OCR 이미지 인식에서 라인에 대한 사각형을 가져오는 과정을 단계별로 쉽게 설명하겠습니다.

## 단계 1: 문서 디렉터리 설정

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

`"Your Document Directory"`를 샘플 이미지가 들어 있는 폴더의 실제 경로로 교체하십시오.

## 단계 2: Aspose.OCR 초기화

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

OCR 기능에 접근하려면 `AsposeOcr` 클래스의 인스턴스를 생성합니다.

## 단계 3: 이미지 경로 지정

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

OCR을 수행하려는 이미지의 전체 경로를 정의합니다.

## 단계 4: 이미지 인식 및 사각형 가져오기

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles` 메서드는 `Rectangle` 객체 목록을 반환하며, 각 객체는 감지된 텍스트 라인의 좌표를 나타냅니다. 이것이 **OCR 라인 사각형을 가져오는** 핵심입니다.

## 단계 5: 결과 출력

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

감지된 영역의 좌표를 콘솔에 출력합니다. 이후 사용자 정의 처리에 **라인 좌표를 추출**하는 데 사용할 수 있는 값을 확인할 수 있습니다.

## 왜 라인 사각형에 Aspose.OCR을 사용해야 할까요?

- **높은 정확도** – 고급 알고리즘이 노이즈가 있거나 기울어진 이미지에서도 라인을 감지합니다.  
- **크로스 플랫폼** – .NET Framework, .NET Core, .NET 5/6에서 작동합니다.  
- **외부 종속성 없음** – 순수 .NET 라이브러리이며, 배포할 네이티브 DLL이 없습니다.  
- **풍부한 출력** – 라인 사각형 외에도 단어, 문자 및 신뢰도 점수를 가져올 수 있습니다.

## 일반적인 문제 및 해결책

| 문제 | 해결책 |
|-------|----------|
| **사각형이 반환되지 않음** | 이미지가 명확하고 수평인 텍스트를 포함하고 있으며 `AreasType.LINES`가 지정되었는지 확인하십시오. |
| **좌표가 올바르지 않음** | 이미지 DPI를 확인하십시오; 저해상도 이미지는 부정확한 경계를 초래할 수 있습니다. |
| **대용량 이미지에서 성능 병목** | `GetRectangles` 호출 전에 이미지를 적절한 해상도로 리사이즈하십시오. |
| **라이선스 예외** | 테스트용으로 체험 라이선스를 사용하고, 평가 제한을 피하려면 운영 환경에서는 정식 라이선스를 적용하십시오. |

## 자주 묻는 질문

**Q: 전체 라인 대신 개별 단어를 추출할 수 있나요?**  
A: 예, 동일한 `GetRectangles` 메서드와 함께 `AreasType.WORDS`를 사용하면 단어 수준의 경계 상자를 얻을 수 있습니다.

**Q: API가 다중 페이지 PDF를 지원하나요?**  
A: 먼저 각 PDF 페이지를 이미지로 변환한 다음 각 이미지에 `GetRectangles`를 호출하십시오.

**Q: 회전된 텍스트를 어떻게 처리하나요?**  
A: OCR 설정에서 자동 회전 옵션을 활성화하거나 처리 전에 이미지를 미리 회전하십시오.

**Q: 각 라인에 대한 신뢰도 점수를 얻는 방법이 있나요?**  
A: 사각형을 얻은 후 `api.RecognizeImage(...).Lines`를 호출하면 신뢰도 값을 포함한 라인 객체에 접근할 수 있습니다.

**Q: 어떤 .NET 버전과 호환되나요?**  
A: 이 라이브러리는 .NET Framework 4.5 이상, .NET Core 3.1 이상, .NET 5/6과 호환됩니다.

## 결론

축하합니다! Aspose.OCR for .NET을 사용하여 이미지에 대한 **OCR 라인 사각형을 성공적으로 가져왔습니다**. 이제 경계 상자를 활용해 라인 좌표를 사용자 정의 렌더링, 데이터 추출 또는 레이아웃 분석과 같은 후속 워크플로에 전달할 수 있습니다.

---

**마지막 업데이트:** 2025-12-17  
**테스트 환경:** Aspose.OCR 24.11 for .NET  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
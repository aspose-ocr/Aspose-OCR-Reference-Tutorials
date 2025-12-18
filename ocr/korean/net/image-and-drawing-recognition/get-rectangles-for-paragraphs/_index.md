---
date: 2025-12-17
description: Aspose.OCR for .NET을 사용하여 OCR 이미지에서 단락의 사각형을 추출하는 방법을 배우세요 – 사각형을 추출하고
  단락 좌표를 얻는 필수 가이드.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: OCR 이미지 인식에서 단락의 사각형을 추출하는 방법
url: /ko/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 이미지 인식에서 단락을 위한 사각형 추출 방법

## 소개

Aspose.OCR for .NET을 사용한 OCR 이미지 인식에서 **how to extract rectangles**에 대한 포괄적인 가이드에 오신 것을 환영합니다. 문서 처리 파이프라인을 개선하고, 단락 경계를 추출하며, 데이터 추출을 자동화하고자 한다면 이곳이 바로 정답입니다. 환경 설정부터 사각형 좌표 출력까지 모든 단계를 단계별로 안내하므로 OCR 결과를 즉시 활용할 수 있습니다.

## 빠른 답변
- **What does “extract rectangles” mean?** 감지된 텍스트 영역의 경계 상자 (x, y, width, height)를 반환합니다.  
- **Which API method provides the rectangles?** `AsposeOcr.GetRectangles` with `AreasType.PARAGRAPHS`.  
- **Do I need a license for development?** 무료 체험판으로 테스트 가능하지만, 상용 환경에서는 상업용 라이선스가 필요합니다.  
- **Can I process multiple images at once?** 예 — 이미지 목록을 순회하면서 각 파일에 대해 `GetRectangles`를 호출하면 됩니다.  
- **What formats are supported?** PNG, JPEG, TIFF, BMP 등 다양한 포맷을 지원합니다.

## OCR에서 “how to extract rectangles”란 무엇인가요?
OCR 용어에서 사각형 추출은 이미지 내 각 단락 또는 텍스트 라인을 둘러싼 기하학적 경계를 식별하는 것을 의미합니다. 이러한 좌표를 사용하면 스캔된 문서의 특정 영역을 강조, 잘라내기 또는 추가 분석할 수 있습니다.

## 왜 단락 좌표를 추출해야 할까요?
- **Precise post‑processing** – 각 사각형을 다운스트림 워크플로(예: 번역, 가림)로 전달할 수 있습니다.  
- **Improved UI/UX** – 원본 이미지 위에 경계 상자를 오버레이하여 사용자가 텍스트가 발견된 위치를 확인할 수 있습니다.  
- **Batch automation** – 대량 문서 세트에서 단락을 빠르게 찾아 격리할 수 있습니다.

## 전제 조건

- C# 및 .NET 개발에 대한 기본 지식.  
- Aspose.OCR for .NET이 설치된 개발 환경 – [여기](https://releases.aspose.com/ocr/net/)에서 다운로드할 수 있습니다.  
- 이미지 처리 개념과 스캔 파일에서 텍스트를 추출하기 위해 OCR이 왜 중요한지에 대한 이해.

## 네임스페이스 가져오기

C# 파일에서 OCR 클래스를 사용할 수 있도록 필요한 네임스페이스를 가져옵니다:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 단계 1: 문서 디렉터리 설정

분석하려는 이미지가 들어 있는 폴더를 정의합니다:

```csharp
string dataDir = "Your Document Directory";
```

## 단계 2: AsposeOcr 인스턴스 초기화

`AsposeOcr` 객체를 생성합니다 – 이를 통해 모든 OCR 기능에 접근할 수 있습니다:

```csharp
AsposeOcr api = new AsposeOcr();
```

## 단계 3: 이미지 경로 지정

처리하려는 정확한 이미지 파일을 지정합니다:

```csharp
string fullPath = dataDir + "sample.png";
```

## 단계 4: 이미지 인식 및 단락 사각형 가져오기

`GetRectangles` 메서드를 호출합니다. `detect_areas`를 `true`로 설정하면 엔진이 **paragraph** 사각형을 반환합니다:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## 단계 5: 결과 출력

좌표를 출력하여 감지된 **extract paragraph coordinates**를 확인합니다:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## 일반적인 문제 및 해결책

| 문제 | 원인 | 해결 방법 |
|-------|--------|-----|
| No rectangles returned | 이미지 품질이 낮거나 잘못된 `AreasType` 사용 | 이미지가 선명한지 확인하고 `AreasType.PARAGRAPHS`를 사용하세요. |
| Coordinates are off‑by‑one | DPI 스케일링 불일치 | 이미지를 로드할 때 올바른 DPI를 설정하거나 `api.Config.Dpi`를 사용하세요. |
| License exception | 프로덕션 환경에서 유효한 라이선스 없이 실행 | `api.SetLicense`를 통해 임시 또는 영구 라이선스를 적용하세요. |

## 자주 묻는 질문

**Q: Aspose.OCR이 다양한 이미지 포맷을 지원하나요?**  
A: 예, Aspose.OCR은 PNG, JPEG, TIFF, BMP 등 많은 일반 포맷을 지원합니다.

**Q: 여러 이미지를 배치 처리할 수 있나요?**  
A: 물론입니다! 파일 경로 컬렉션을 순회하면서 각 이미지에 `GetRectangles`를 호출하면 됩니다.

**Q: Aspose.OCR for .NET의 무료 체험판이 있나요?**  
A: 예, 무료 체험판을 [여기](https://releases.aspose.com/)에서 확인할 수 있습니다.

**Q: Aspose.OCR의 임시 라이선스를 어떻게 얻을 수 있나요?**  
A: 임시 라이선스를 [여기](https://purchase.aspose.com/temporary-license/)에서 획득할 수 있습니다.

**Q: Aspose.OCR 관련 추가 지원 및 토론을 어디서 찾을 수 있나요?**  
A: 커뮤니티 지원 및 토론을 위해 [Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16)으로 이동하세요.

## 결론

이 튜토리얼에서는 Aspose.OCR for .NET을 사용해 **how to extract rectangles**를 통해 단락 사각형을 추출하는 방법을 보여주고, 각 코드 스니펫을 단계별로 설명했으며 반환된 좌표를 해석하는 방법을 안내했습니다. 이 절차를 애플리케이션에 통합하면 단락 경계를 안정적으로 추출하고 문서 워크플로를 강화하며 보다 스마트한 OCR 기반 솔루션을 구축할 수 있습니다.

---

**마지막 업데이트:** 2025-12-17  
**테스트 환경:** Aspose.OCR 24.11 for .NET  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
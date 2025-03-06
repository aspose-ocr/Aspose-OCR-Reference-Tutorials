---
title: OCR 이미지 인식에서 단락의 직사각형 가져오기
linktitle: OCR 이미지 인식에서 단락의 직사각형 가져오기
second_title: Aspose.OCR .NET API
description: .NET용 Aspose.OCR로 고급 OCR 기능을 잠금 해제하세요. 단락 직사각형을 손쉽게 추출합니다.
weight: 11
url: /ko/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 이미지 인식에서 단락의 직사각형 가져오기

## 소개

.NET용 Aspose.OCR을 활용하여 OCR 이미지 인식에서 단락 직사각형을 추출하는 방법에 대한 포괄적인 가이드에 오신 것을 환영합니다. 문서 처리 기능을 강화하고 .NET 애플리케이션에서 OCR(광학 문자 인식) 기능을 활용하려는 경우 올바른 위치에 오셨습니다.

## 전제 조건

튜토리얼을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

- C# 및 .NET 개발에 대한 기본 지식.
-  .NET용 Aspose.OCR을 사용하여 설정된 개발 환경입니다. 아직 다운로드하지 않았다면 다운로드할 수 있습니다.[여기](https://releases.aspose.com/ocr/net/).
- 이미지 처리 개념과 이미지에서 텍스트를 추출할 때 OCR의 중요성을 이해합니다.

## 네임스페이스 가져오기

C# 코드에서 Aspose.OCR을 효율적으로 사용하기 위해 필요한 네임스페이스를 가져왔는지 확인하세요. 파일 상단에 다음을 포함하세요.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1단계: 문서 디렉토리 설정

OCR 처리를 위한 이미지가 저장되는 문서 디렉터리의 경로를 초기화하는 것부터 시작하세요.

```csharp
string dataDir = "Your Document Directory";
```

## 2단계: AsposeOcr 인스턴스 초기화

OCR 기능에 액세스하려면 AsposeOcr 클래스의 인스턴스를 만듭니다.

```csharp
AsposeOcr api = new AsposeOcr();
```

## 3단계: 이미지 경로 지정

처리하려는 이미지의 전체 경로를 정의합니다.

```csharp
string fullPath = dataDir + "sample.png";
```

## 4단계: 이미지 인식 및 단락 직사각형 가져오기

 호출`GetRectangles` OCR 이미지의 단락에 대한 직사각형을 얻는 방법입니다. 세트`detect_areas` 에게`true` 단락을 추출하려면 다음을 수행하십시오.

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## 5단계: 결과 인쇄

식별된 영역의 좌표를 인쇄합니다.

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## 6단계: 결론

축하해요! .NET용 Aspose.OCR을 사용하여 단락에 대한 직사각형을 얻기 위해 OCR 이미지 인식 프로세스를 성공적으로 실행했습니다.

## 결론

이 튜토리얼에서는 .NET용 Aspose.OCR을 애플리케이션에 통합하여 OCR 처리 이미지에서 단락 직사각형을 추출하는 기본 단계를 살펴보았습니다. Aspose.OCR은 OCR 구현을 단순화하여 문서 처리 및 텍스트 추출을 위한 유용한 도구로 만듭니다.

## FAQ

### Q1: Aspose.OCR은 다른 이미지 형식과 호환됩니까?

A1: 예, Aspose.OCR은 PNG, JPEG, TIFF를 포함한 다양한 이미지 형식을 지원합니다.

### Q2: 여러 이미지의 일괄 처리에 Aspose.OCR을 사용할 수 있습니까?

A2: 물론이죠! Aspose.OCR은 여러 이미지를 원활하게 처리하기 위해 일괄 처리를 용이하게 합니다.

### Q3: .NET용 Aspose.OCR에 대한 무료 평가판이 있습니까?

 A3: 예, 무료 평가판을 사용해 볼 수 있습니다.[여기](https://releases.aspose.com/).

### Q4: Aspose.OCR에 대한 임시 라이선스를 어떻게 얻을 수 있나요?

 A4: 임시 라이센스를 취득할 수 있습니다[여기](https://purchase.aspose.com/temporary-license/).

### Q5: Aspose.OCR과 관련된 추가 지원 및 토론은 어디에서 찾을 수 있습니까?

 A5: 다음으로 가세요.[Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16) 커뮤니티 지원 및 토론을 위해.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

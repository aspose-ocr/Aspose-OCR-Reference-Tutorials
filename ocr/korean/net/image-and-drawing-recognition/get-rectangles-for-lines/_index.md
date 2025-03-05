---
title: OCR 이미지 인식에서 선의 직사각형 가져오기
linktitle: OCR 이미지 인식에서 선의 직사각형 가져오기
second_title: Aspose.OCR .NET API
description: 정확한 OCR 이미지 인식의 핵심인 .NET용 Aspose.OCR을 살펴보세요. 텍스트 추출의 힘을 손쉽게 활용해 보세요.
type: docs
weight: 10
url: /ko/net/image-and-drawing-recognition/get-rectangles-for-lines/
---
## 소개

.NET 애플리케이션에서 광학 문자 인식(OCR)의 잠재력을 활용할 수 있는 강력한 도구인 .NET용 Aspose.OCR의 세계에 오신 것을 환영합니다. 당신이 노련한 개발자이든 호기심 많은 매니아이든 이 가이드는 Aspose.OCR을 사용하여 OCR 이미지 인식에서 선에 대한 직사각형을 얻는 과정을 안내합니다.

## 전제 조건

튜토리얼을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

- C# 및 .NET 개발에 대한 기본 지식.
- Visual Studio와 같은 IDE(통합 개발 환경).
-  .NET 라이브러리용 Aspose.OCR이 설치되었습니다. 당신은 그것을 다운로드 할 수 있습니다[여기](https://releases.aspose.com/ocr/net/).
- OCR 인식을 위한 텍스트가 포함된 샘플 이미지입니다.

## 네임스페이스 가져오기

프로젝트에 필요한 네임스페이스를 가져왔는지 확인하세요. C# 파일 맨 위에 다음 줄을 추가합니다.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

이제 OCR 이미지 인식에서 선의 직사각형을 얻는 과정을 따라하기 쉬운 단계로 나누어 보겠습니다.

## 1단계: 문서 디렉토리 설정

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// 연장:3
```

 바꾸다`"Your Document Directory"` 문서 디렉토리의 실제 경로를 사용하십시오.

## 2단계: Aspose.OCR 초기화

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// 연장:4
```

 인스턴스를 생성합니다.`AsposeOcr` OCR 기능에 액세스하는 클래스입니다.

## 3단계: 이미지 경로 지정

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// 연장:5
```

OCR을 수행하려는 이미지의 전체 경로를 정의합니다.

## 4단계: 이미지 인식 및 직사각형 가져오기

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// 연장:6
```

 활용`GetRectangles` 지정된 이미지의 라인에 대한 직사각형을 검색하는 메소드입니다.

## 5단계: 결과 인쇄

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// 연장:7
```

감지된 영역의 좌표를 콘솔에 인쇄합니다.

## 결론

축하해요! .NET용 Aspose.OCR을 사용하여 OCR 이미지 인식에서 선의 직사각형을 성공적으로 얻었습니다. 이 다재다능한 도구는 애플리케이션에서 텍스트 추출을 위한 가능성의 세계를 열어줍니다.

## FAQ

### Q1: 모든 유형의 이미지에 Aspose.OCR for .NET을 사용할 수 있습니까?

A1: Aspose.OCR은 다양한 이미지 형식을 지원하여 OCR 애플리케이션의 유연성을 보장합니다.

### Q2: OCR 인식은 얼마나 정확합니까?

A2: Aspose.OCR은 높은 정확도를 위해 고급 알고리즘을 활용하므로 다양한 텍스트 인식 시나리오에 적합합니다.

### Q3: 평가판을 사용할 수 있나요?

 A3: 예, 다음을 통해 .NET용 Aspose.OCR의 기능을 탐색할 수 있습니다.[무료 시험판](https://releases.aspose.com/).

### Q4: 포괄적인 문서는 어디에서 찾을 수 있습니까?

 A4: 다음을 참조하세요.[선적 서류 비치](https://reference.aspose.com/ocr/net/) 자세한 정보 및 사용 지침을 확인하세요.

### Q5: 도움이 필요하거나 구체적인 질문이 있습니까?

 A5: 다음을 방문하세요.[Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16) 커뮤니티 지원 및 토론을 위해.
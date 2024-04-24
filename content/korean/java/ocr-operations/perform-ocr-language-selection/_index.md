---
title: Aspose.OCR에서 언어 선택으로 OCR 수행
linktitle: Aspose.OCR에서 언어 선택으로 OCR 수행
second_title: Aspose.OCR 자바 API
description: Java용 Aspose.OCR을 사용하여 이미지에서 정확한 텍스트 추출을 잠금 해제하세요. 언어 선택과 함께 정확한 OCR을 위한 단계별 가이드를 따르세요.
type: docs
weight: 11
url: /ko/java/ocr-operations/perform-ocr-language-selection/
---
## 소개

끊임없이 진화하는 기술 환경에서 광학 문자 인식(OCR)은 이미지에서 의미 있는 정보를 추출하는 데 중추적인 역할을 합니다. Aspose.OCR for Java는 개발자가 OCR 기능을 Java 애플리케이션에 원활하게 통합할 수 있는 강력한 도구입니다. 이 단계별 가이드에서는 Aspose.OCR을 사용하여 언어 선택으로 OCR을 수행하는 방법을 살펴보고 다양한 콘텐츠를 정밀하게 처리할 수 있는 잠재력을 열어줍니다.

## 전제 조건

튜토리얼을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

- Java 개발 환경: 시스템에 Java가 설치되어 있고 개발 환경이 설정되어 있는지 확인하십시오.

-  Aspose.OCR 라이브러리: Java용 Aspose.OCR 라이브러리를 다운로드하고 설치합니다. 라이브러리 및 관련 문서를 찾을 수 있습니다.[여기](https://reference.aspose.com/ocr/java/).

- 이미지 파일: 추출하려는 텍스트가 포함된 이미지 파일을 준비합니다. 예를 들어 "p3.png"라는 파일을 사용해보자.

## 패키지 가져오기

Java 프로젝트에서 Aspose.OCR 기능을 활용하는 데 필요한 패키지를 가져옵니다. Java 파일 시작 부분에 다음 줄을 추가합니다.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 1단계: 문서 디렉터리 설정

```java
// 문서 디렉터리의 경로입니다.
String dataDir = "Your Document Directory";
```

"문서 디렉토리"를 이미지 파일이 있는 디렉토리의 실제 경로로 바꾸십시오.

## 2단계: 이미지 경로 정의

```java
// 이미지 경로
String file = dataDir + "p3.png";
```

특정 이미지 파일을 가리키도록 파일 변수를 조정합니다.

## 3단계: Aspose.OCR API 인스턴스 생성

```java
// API 인스턴스 생성
AsposeOCR api = new AsposeOCR();
```

해당 기능에 액세스하려면 AsposeOCR 개체를 초기화하세요.

## 4단계: 인식 옵션 설정

```java
// 인식 옵션 설정
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

요구 사항에 따라 인식 설정을 사용자 정의하세요. 기울기, 언어, 인식 영역 등의 매개변수를 조정합니다.

## 5단계: OCR 수행 및 결과 검색

```java
// 결과 객체 가져오기
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

지정된 이미지 파일과 설정을 사용하여 OCR 작업을 실행합니다. RecognitionResult 개체에서 결과를 캡처합니다.

## 6단계: 결과 인쇄 및 활용

```java
// 결과 인쇄
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

추출된 텍스트, 인식 영역, JSON 표현, 기울어짐 각도 및 모든 경고를 인쇄합니다. 애플리케이션에서 필요에 따라 결과를 사용하십시오.

## 결론

이 튜토리얼에서는 언어 선택으로 OCR을 수행하기 위해 Java용 Aspose.OCR의 원활한 통합을 살펴보았습니다. 이 강력한 라이브러리는 이미지에서 텍스트를 정확하게 추출하려는 개발자에게 가능성의 세계를 열어줍니다.

## FAQ

### Q1: 단일 인식 프로세스에서 여러 언어에 Aspose.OCR을 사용할 수 있습니까?

A1: 예, RecognitionSettings에서 여러 언어를 설정하여 다국어 콘텐츠에 대한 인식 정확도를 높일 수 있습니다.

### Q2: Aspose.OCR로 다양한 이미지 형식을 어떻게 처리할 수 있나요?

A2: Aspose.OCR은 PNG, JPEG, TIFF를 포함한 다양한 이미지 형식을 지원합니다. 이미지 경로 변수에 올바른 파일 경로를 제공하기만 하면 됩니다.

### Q3: Aspose.OCR이 처리할 수 있는 이미지 크기에 제한이 있나요?

A3: Aspose.OCR은 다양한 크기의 이미지를 처리할 수 있지만 더 큰 이미지에는 더 많은 처리 시간과 리소스가 필요할 수 있습니다.

### Q4: 이미지 내 특정 영역에 대한 인식 설정을 미세 조정할 수 있나요?

A4: 물론이죠. RecognitionAreas 기능을 활용하여 대상 인식을 위해 이미지 내에서 특정 직사각형을 정의합니다.

### Q5: Aspose.OCR은 개인 및 상업 프로젝트 모두에 적합합니까?

A5: 예, Aspose.OCR은 유연한 라이센스 옵션을 제공하므로 개인용 및 상업용 모두에 적합합니다.
---
date: 2026-02-20
description: Aspose.OCR for Java를 사용해 이미지에서 텍스트를 추출하고, 허용 문자 설정 및 임시 라이선스 적용 방법을 배우세요
  – 완전한 Aspose OCR Java 튜토리얼.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR을 사용하여 이미지에서 텍스트 추출 – 허용 문자
url: /ko/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

Now produce final content.

Be careful with dash characters. Keep markdown formatting.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR을 사용한 이미지에서 텍스트 추출 – 허용 문자

## 소개

이미지에서 텍스트를 추출하는 것은 현대 애플리케이션에서 흔히 요구되는 작업입니다—청구서 처리, 영수증 스캔, 인쇄된 문서 디지털화 등 다양한 상황에서 필요합니다. 이 튜토리얼에서는 **aspose ocr java tutorial**을 통해 Aspose.OCR for Java으로 **이미지에서 텍스트를 추출**하고, 허용 문자를 설정하며, 라이브러리를 테스트할 때 임시 라이선스를 적용하는 방법을 단계별로 안내합니다.

## 빠른 답변
- **Aspose.OCR은 무엇을 하나요?** 이미지에서 텍스트를 높은 정확도로 추출하며 사용자 정의 문자 집합을 지원합니다.  
- **라이선스가 필요합니까?** 프로덕션 사용을 위해서는 임시 또는 영구 라이선스가 필요합니다.  
- **지원되는 JDK 버전은?** 최신 JDK 릴리스와 완전하게 호환됩니다.  
- **인식 문자 범위를 제한할 수 있나요?** 예—`setAllowedCharacters` API를 사용하여 출력 문자를 제한할 수 있습니다.  
- **설정에 걸리는 시간은?** 기본 구현의 경우 약 10‑15분 정도 소요됩니다.

## “이미지에서 텍스트 추출”이란?
이미지에서 텍스트를 추출한다는 것은 시각적인 텍스트(예: 인쇄된 텍스트 또는 손글씨)를 기계가 읽을 수 있는 문자열로 변환하는 과정을 의미합니다. 이를 통해 검색, 인덱싱, 데이터 분석 등 하위 작업을 수행할 수 있습니다.

## 왜 Java용 Aspose.OCR을 사용해야 할까요?
- **다중 언어 및 다양한 폰트에 대한 높은 정확도**.  
- **간단한 API**로 모든 Java 프로젝트에 쉽게 통합 가능.  
- **사용자 정의 가능한** 문자 집합, 언어 팩, 이미지 전처리 옵션 제공.  
- **외부 의존성 없음**—라이브러리가 자체적으로 포함되어 있습니다.

## 전제 조건

시작하기 전에 다음 항목이 준비되어 있는지 확인하세요.

### Java Development Kit (JDK)

시스템에 최신 Java Development Kit이 설치되어 있는지 확인하십시오. [여기](https://www.oracle.com/java/technologies/javase-downloads.html)에서 다운로드할 수 있습니다.

### Aspose.OCR for Java Library

[Aspose.OCR for Java 라이브러리 다운로드 링크](https://releases.aspose.com/ocr/java/)에서 라이브러리를 다운로드하고 설치하십시오.

### Aspose.OCR License

Aspose.OCR의 전체 기능을 사용하려면 유효한 라이선스를 획득해야 합니다. [여기](https://purchase.aspose.com/buy)에서 구매하거나, 체험 기간을 위한 [임시 라이선스](https://purchase.aspose.com/temporary-license/)를 확인하십시오.

## 임시 라이선스 적용 방법

제품을 평가하는 동안 임시 라이선스를 사용하면 평가 워터마크가 제거되고 제한된 기간 동안 전체 기능을 사용할 수 있습니다. Aspose 포털에서 라이선스 문자열을 생성한 뒤, 아래 코드 예시와 같이 `AsposeOCR` 생성자에 전달하십시오. 프로덕션 배포 시에는 임시 키를 영구 라이선스로 교체하면 됩니다.

## OCR 이미지 전처리 팁

좋은 이미지 품질은 인식 결과를 크게 향상시킵니다. OCR 엔진을 호출하기 전에 다음을 고려하십시오:

- 이미지를 그레이스케일로 변환합니다.  
- 대비를 높여 문자와 배경을 구분합니다.  
- 바이너리화 필터로 배경 노이즈를 제거합니다.  
- 저해상도 이미지를 최소 300 dpi로 리사이즈합니다.

이러한 단계는 **ocr image preprocessing**의 일부이며, Aspose.OCR을 호출하기 전에 표준 Java 이미지 라이브러리를 사용해 수행할 수 있습니다.

## 패키지 가져오기

전제 조건이 준비되면 Java 프로젝트에 필요한 패키지를 가져옵니다:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## 단계별 가이드

### Step 1: Set Your Document Directory

OCR 처리 결과를 저장할 폴더를 정의합니다. 이 경로는 이후 이미지 파일을 찾는 데 사용됩니다.

```java
String dataDir = "Your Document Directory";
```

### Step 2: Specify the Image Path

분석할 이미지 파일의 경로를 API에 지정합니다.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Step 3: Create an Aspose.OCR Instance

라이선스 키와 함께 OCR 엔진을 인스턴스화합니다. 키는 임시 라이선스 문자열이거나 영구 라이선스 문자열일 수 있습니다.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Step 4: Perform OCR Recognition

`RecognizeLine` 메서드를 호출하여 이미지에서 한 줄의 텍스트를 추출합니다. 결과는 추가 처리하거나 저장할 수 있는 일반 문자열입니다.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** 특정 문자 집합(예: 숫자만)으로 출력을 제한하려면 `RecognizeLine`을 호출하기 전에 `AsposeOCR` 인스턴스의 `setAllowedCharacters` 메서드를 사용하십시오. 이렇게 하면 정의된 집합에 포함되지 않은 문자는 엔진이 무시합니다.

## 일반적인 문제와 해결책

| 문제 | 원인 | 해결책 |
|------|------|--------|
| **출력이 없거나 빈 문자열** | 이미지 경로가 잘못되었거나 지원되지 않는 이미지 형식 | `imagePath`를 확인하고 지원되는 형식(JPEG, PNG, BMP)으로 사용 |
| **인식 오류** | 저해상도 이미지 또는 잡음이 많은 배경 | OCR 전에 이미지 전처리(대비 증가, 바이너리화) 수행 |
| **라이선스가 적용되지 않음** | 라이선스 키 누락 또는 잘못된 형식 | 라이선스 문자열이 정확한지 확인하고 `AsposeOCR` 생성자에 전달 |

## 자주 묻는 질문

**Q: Aspose.OCR의 임시 라이선스는 어떻게 얻나요?**  
A: [임시 라이선스 페이지](https://purchase.aspose.com/temporary-license/)에서 체험 라이선스를 요청하십시오.

**Q: Aspose.OCR에 대한 지원은 어디서 받을 수 있나요?**  
A: [Aspose.OCR 포럼](https://forum.aspose.com/c/ocr/16)에서 커뮤니티에 참여해 도움을 받으세요.

**Q: Aspose.OCR에서 허용 문자를 지정할 수 있나요?**  
A: 예, `setAllowedCharacters` API를 사용해 문자 집합을 사용자 정의할 수 있습니다. 자세한 내용은 공식 문서를 참고하십시오.

**Q: 최신 JDK 버전과 호환되나요?**  
A: 물론입니다—Aspose.OCR은 최신 Java 릴리스와 호환되도록 정기적으로 업데이트됩니다.

**Q: 라인 인식 외에 추가 OCR 기능이 있나요?**  
A: 예, 라이브러리는 블록, 단락, 전체 페이지 인식은 물론 언어 팩 및 이미지 전처리 옵션도 지원합니다.

## 결론

이 **aspose ocr java tutorial**을 따라 하면 **이미지에서 텍스트를 추출**하고 인식할 문자를 제어하는 작업을 구현할 수 있습니다. 고급 기능(다중 언어 지원, 사용자 정의 전처리, 배치 처리 등)을 확인하려면 전체 [문서](https://reference.aspose.com/ocr/java/)를 살펴보세요.

---

**마지막 업데이트:** 2026-02-20  
**테스트 환경:** Aspose.OCR for Java 24.11  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
date: 2026-05-24
description: Aspose.OCR for Java와 함께 OCR을 사용하는 방법을 알아보고, 이미지에서 텍스트를 추출하고, allowed
  characters를 설정하고, 몇 분 안에 temporary license를 적용하는 방법을 확인하세요.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Aspose.OCR에서 Allowed Characters 지정
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: OCR 사용 방법 – Aspose.OCR로 이미지에서 텍스트 추출
url: /ko/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 사용 방법 – Aspose.OCR로 이미지에서 텍스트 추출

현대 Java 애플리케이션에서 **OCR 사용 방법**은 흔한 질문이며, 특히 스캔한 청구서, 영수증 또는 인쇄된 양식을 검색 가능한 텍스트로 변환해야 할 때 그렇습니다. 이 튜토리얼은 **Aspose.OCR for Java** 예제를 전체적으로 안내합니다: 이미지에서 텍스트 추출, 출력 문자열을 사용자 정의 문자 집합으로 제한, 그리고 빠른 평가를 위한 임시 라이선스 적용.

## 빠른 답변
- **Aspose.OCR은 무엇을 하나요?** 이미지에서 텍스트를 높은 정확도로 추출하고 인식된 문자를 제한할 수 있습니다.  
- **라이선스가 필요합니까?** 프로덕션 사용을 위해 임시 또는 영구 라이선스가 필요합니다; 임시 키는 워터마크를 제거합니다.  
- **지원되는 JDK 버전은?** 라이브러리는 최신 JDK 릴리스(JDK 17, 19, 21)와 함께 작동합니다.  
- **인식된 문자를 제한할 수 있나요?** 예—출력을 제한하려면 `setAllowedCharacters` 메서드를 사용하십시오.  
- **설정에 얼마나 걸립니까?** 기본 엔드‑투‑엔드 구현에 대략 10‑15 분 정도 소요됩니다.

## “이미지에서 텍스트 추출”이란?
이미지에서 텍스트를 추출하는 작업은 광학 문자 인식(OCR)이라고도 하며, 인쇄된 것이든 손글씨든 타이핑된 것이든 시각적인 문자를 기계가 읽을 수 있는 문자열로 변환합니다. 이 변환을 통해 애플리케이션은 콘텐츠를 프로그래밍 방식으로 검색, 색인, 편집 및 분석할 수 있게 되며, 청구서 처리, 문서 보관, 데이터 입력 자동화와 같은 워크플로를 지원합니다.

## Java에서 Aspose.OCR을 사용하는 이유
Aspose.OCR은 **60개 이상의 언어**를 지원하고, 전체 파일을 메모리에 로드하지 않고 **10 MB**까지의 이미지를 처리할 수 있으며, 깨끗한 스캔에 대해 **95 % 이상의 정확도**를 제공합니다. 이 라이브러리는 외부 OCR 엔진이 필요 없는 자체 포함형으로, 배포가 간단하고 라이선스 비용을 줄여줍니다.

## 사전 요구 사항

### Java Development Kit (JDK)
최신 Java Development Kit이 설치되어 있는지 확인하십시오. [here](https://www.oracle.com/java/technologies/javase-downloads.html)에서 다운로드할 수 있습니다.

### Aspose.OCR for Java 라이브러리
[download link](https://releases.aspose.com/ocr/java/)에서 Aspose.OCR for Java 라이브러리를 다운로드하고 설치하십시오.

### Aspose.OCR 라이선스
전체 기능을 사용하려면 라이선스를 얻으십시오. [here](https://purchase.aspose.com/buy)에서 구매하거나 체험용으로 [temporary license](https://purchase.aspose.com/temporary-license/)를 요청할 수 있습니다.

## Aspose.OCR for Java를 사용한 OCR 사용 방법?
이미지를 로드하고 OCR 엔진을 구성한 뒤 인식 메서드를 호출하십시오—몇 줄의 간단한 코드만 필요합니다. 이 직접 답변 문단은 정확히 해야 할 일을 알려줍니다: 라이선스 문자열로 `AsposeOCR` 인스턴스를 생성하고, 허용할 문자를 설정한 뒤, 대상 이미지에 `RecognizeLine`을 호출하여 추출된 텍스트를 받습니다. API는 이미지 전처리를 내부적으로 처리하므로 추가 코드 없이도 깨끗한 결과를 얻을 수 있습니다.

### 패키지 가져오기
`AsposeOCR` 클래스는 `com.aspose.ocr` 패키지에 있습니다. 코딩을 시작하기 전에 필요한 클래스를 가져오십시오.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## 단계별 가이드

### 단계 1: 문서 디렉터리 설정
OCR 결과와 임시 파일이 저장될 폴더를 선택하십시오. 이 경로는 나중에 처리하려는 이미지를 찾는 데 사용됩니다.

```java
String dataDir = "Your Document Directory";
```

### 단계 2: 이미지 경로 지정
분석하려는 이미지가 위치한 전체 파일 시스템 경로나 클래스패스 리소스 위치를 제공하십시오.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### 단계 3: Aspose.OCR 인스턴스 생성
`AsposeOCR`는 광학 문자 인식을 수행하는 핵심 엔진입니다. 임시 또는 영구 라이선스 문자열을 사용하여 인스턴스를 생성하십시오.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### 단계 4: OCR 인식 수행
`RecognizeLine`은 제공된 이미지에서 단일 텍스트 라인을 추출하고 일반 Java `String`으로 반환합니다. 다중 라인 문서의 경우 이 메서드를 반복해서 호출할 수 있습니다.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** 출력이 숫자만(예: 청구서 번호)이어야 하는 경우, `RecognizeLine`을 호출하기 전에 `AsposeOCR` 인스턴스에서 `setAllowedCharacters("0123456789")`를 호출하십시오. 이렇게 하면 엔진이 숫자가 아닌 기호를 무시하도록 강제합니다.  
> `setAllowedCharacters`는 `AsposeOCR`의 메서드로, OCR 출력을 지정된 화이트리스트 문자 집합으로 제한합니다.

## 일반적인 문제와 해결책

| Issue | Reason | Fix |
|-------|--------|-----|
| **출력이 없거나 빈 문자열** | 이미지 경로가 잘못되었거나 지원되지 않는 형식 | `imagePath`를 확인하고 지원되는 형식(JPEG, PNG, BMP)을 사용하십시오 |
| **인식 오류** | 저해상도 이미지 또는 노이즈가 많은 배경 | OCR 전에 이미지를 전처리하십시오(대비 증가, 이진화) |
| **라이선스가 적용되지 않음** | 라이선스 키가 없거나 유효하지 않음 | `AsposeOCR` 생성자에 올바른 라이선스 문자열이 전달되었는지 확인하십시오 |

## 자주 묻는 질문

**Q: Aspose.OCR의 임시 라이선스를 어떻게 얻을 수 있나요?**  
A: 평가 워터마크를 제거하는 체험 키를 요청하려면 [temporary license page](https://purchase.aspose.com/temporary-license/)를 방문하십시오.

**Q: Aspose.OCR 지원은 어디에서 받을 수 있나요?**  
A: 도움과 토론을 위해 [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) 커뮤니티에 참여하십시오.

**Q: Aspose.OCR에서 허용 문자 집합을 지정할 수 있나요?**  
A: 예, `setAllowedCharacters` API를 사용하여 사용자 정의 화이트리스트 문자를 정의하십시오. 숫자 전용 필드에 적합합니다.

**Q: Aspose.OCR이 최신 JDK 버전과 호환되나요?**  
A: 물론입니다—Aspose.OCR은 최신 Java 릴리스와 호환되도록 정기적으로 업데이트됩니다.

**Q: 라인 인식 외에 추가 OCR 기능이 있나요?**  
A: 이 라이브러리는 블록, 단락 및 전체 페이지 인식, 언어 팩, 고급 이미지 전처리도 지원합니다.

## 결론

이 **Aspose OCR Java 튜토리얼**을 따라 하면 이제 **OCR 사용 방법**을 알고 이미지에서 텍스트를 추출하고 문자 집합을 제한하며 빠른 테스트를 위해 임시 라이선스를 적용할 수 있습니다. 다중 언어 지원, 배치 처리, 사용자 정의 전처리 파이프라인을 살펴보려면 전체 [documentation](https://reference.aspose.com/ocr/java/)을 확인하십시오.

---

**마지막 업데이트:** 2026-05-24  
**테스트 환경:** Aspose.OCR for Java 24.11  
**작성자:** Aspose  

{{< blocks/products/products-backtop-button >}}

## 관련 튜토리얼

- [Java에서 Aspose.OCR 라이선스 설정 및 확인 방법](/ocr/java/ocr-basics/set-license/)
- [Aspose.OCR BufferedImage를 사용하여 Java에서 이미지를 텍스트로 변환](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose OCR Java 예제 – 이미지에서 라인 인식](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
---
category: general
date: 2026-01-02
description: Aspose OCR을 사용하여 스캔된 이미지 PDF에서 검색 가능한 PDF를 생성합니다. OCR 언어 설정, 텍스트 레이어
  PDF 삽입 및 고압축 PDF 옵션 적용 방법을 배웁니다.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: ko
og_description: 검색 가능한 PDF를 빠르게 만들기. 이 가이드는 스캔된 이미지 PDF를 변환하고, 텍스트 레이어를 삽입하며, OCR
  언어를 설정하고, 고압축 PDF를 활성화하는 방법을 보여줍니다.
og_title: Aspose OCR로 검색 가능한 PDF 만들기 – 완전 가이드
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Aspose OCR로 검색 가능한 PDF 만들기 – 단계별 가이드
url: /ko/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 검색 가능한 PDF 만들기 – 전체 프로그래밍 튜토리얼

스캔한 이미지에서 **검색 가능한 PDF** 파일을 만들어야 하는데 어디서 시작해야 할지 몰라 고민한 적 있나요? 당신만 그런 것이 아닙니다. 문서가 많은 작업 흐름에서는 이미지만 포함된 PDF가 검색 및 색인에 전혀 도움이 되지 않는 경우가 많습니다.  

좋은 소식은 Aspose OCR을 사용하면 **스캔 이미지 PDF**를 몇 줄의 Java 코드만으로 완전한 검색 가능한 문서로 변환할 수 있다는 것입니다. 이 튜토리얼에서는 OCR 엔진 초기화, 고압축 PDF 설정 구성, 숨겨진 텍스트 레이어 삽입, 올바른 OCR 언어 선택까지 모든 단계를 자세히 안내합니다.

이 가이드를 끝까지 따라 하면 검색 가능한 PDF를 생성하는 실행 가능한 프로그램을 얻을 수 있으며, 이 파일을 어떤 검색 엔진이나 문서 관리 시스템에든 문제 없이 넣을 수 있습니다.

---

## 검색 가능한 PDF 만들기 – 개요

코드에 들어가기 전에 “검색 가능한 PDF 만들기”가 정확히 무엇을 의미하는지 명확히 해봅시다. 검색 가능한 PDF는 두 개의 평행 레이어를 가집니다:

1. **시각 레이어** – 원본 스캔 이미지(또는 렌더링된 페이지).  
2. **텍스트 레이어** – OCR을 통해 추출된 보이지 않지만 기계가 읽을 수 있는 문자들.

Adobe Reader에서 텍스트를 선택하면 실제로는 그림이 아니라 숨겨진 텍스트 레이어와 상호작용하게 됩니다. 이 듀얼 레이어 접근 방식이 **텍스트 레이어가 삽입된 PDF** 기능을 가능하게 합니다.

---

## Aspose OCR을 사용한 스캔 이미지 PDF 변환

먼저 PDF로 변환하려는 스캔 이미지(PNG, JPEG, TIFF)가 필요합니다. Aspose OCR은 해당 이미지를 읽고 OCR을 수행한 뒤 결과를 PDF 라이터에 전달합니다.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**작동 원리:**  
- `setCreateSearchablePdf(true)`는 Aspose에게 숨겨진 텍스트 레이어를 생성하도록 지시하여 **텍스트 레이어가 삽입된 PDF** 요구사항을 충족합니다.  
- `setCompressionLevel(9)`는 파일을 **고압축 PDF** 범위로 끌어올려 OCR 정확도를 손상시키지 않으면서 최종 크기를 줄입니다.  
- `RecognitionLanguage.ENGLISH` 인자는 **OCR 언어 설정** 방법을 보여주며, 필요에 따라 프랑스어, 독일어 등으로 교체할 수 있습니다.

---

## 고압축 PDF 설정

대용량 스캔 PDF는 금방 수백 메가바이트까지 커질 수 있습니다. Aspose는 PDF 수준에서 작동하는 간단한 압축 API를 제공합니다. `setCompressionLevel` 메서드는 0 (압축 없음)부터 9 (최대 압축)까지 값을 허용합니다.  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

몇 가지 팁:

- **무손실 이미지 포맷**(PNG)을 텍스트가 많은 스캔에 사용하고, 사진에는 JPEG가 더 적합합니다.  
- 사용자 정의 글꼴을 삽입하는 경우 **글꼴 서브셋팅**을 활성화하세요—검색 가능한 PDF를 만들면 Aspose가 자동으로 처리합니다.  
- **출력 크기를 매번 테스트**하세요; 경우에 따라 레벨 8 압축이 레벨 9에 비해 품질 손실은 거의 없으면서 10 % 정도 크기를 줄일 수 있습니다.

---

## 검색 가능성을 위한 텍스트 레이어 PDF 삽입

`setCreateSearchablePdf(true)` 호출을 생략하면 파일은 겉보기에는 정상이지만 내용 검색이 불가능합니다. 숨겨진 텍스트 레이어는 인식된 각 문자를 페이지상의 위치에 매핑하여 생성됩니다.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**주의할 점:**  

- **다국어 문서** – 언어당 한 번씩 OCR을 실행한 뒤 텍스트 레이어를 병합해야 할 수 있습니다.  
- **복잡한 레이아웃**(표, 다중 컬럼) – Aspose가 꽤 잘 처리하지만, 숨겨진 텍스트를 표시할 수 있는 PDF 뷰어(예: Adobe Acrobat의 “Edit PDF” 모드)로 결과를 반드시 확인하세요.

---

## 정확한 인식을 위한 OCR 언어 설정

OCR 엔진의 정확도는 지정한 언어에 크게 좌우됩니다. Aspose는 기본 제공 언어 세트를 포함하고 있으며, 사용자 정의 언어 팩도 추가할 수 있습니다.  

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**언어를 변경해야 할 때:**  

- 문서에 **비라틴 문자**(키릴 문자, 아라비아 문자 등)가 포함된 경우 적절한 `RecognitionLanguage` 로 전환합니다.  
- 혼합 언어 페이지 – `recognizeImageAndSave` 를 서로 다른 언어로 두 번 호출한 뒤 PDF를 병합하면 됩니다.

---

## 전체 예제 실행

아래는 바로 실행 가능한 전체 프로그램입니다. 자리표시자 경로를 실제 파일 위치로 교체하고, Aspose OCR JAR가 클래스패스에 포함되어 있는지 확인한 뒤 실행하세요.  

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**예상 출력:** 프로그램을 실행하면 콘솔에 다음과 같이 표시됩니다.

```
Searchable PDF created.
```

`searchable.pdf` 를 어떤 PDF 뷰어에서 열고 텍스트를 선택해 보세요. 보이지 않는 레이어가 작동하는 것을 확인할 수 있습니다. 이제 **스캔 이미지에서 검색 가능한 PDF 만들기**에 성공했습니다.

---

![검색 가능한 PDF 예시](image-placeholder.png "검색 가능한 PDF 예시")

*위 스크린샷(자리표시자)은 일반적으로 스캔된 페이지 위에 선택 가능한 텍스트가 표시된 PDF 뷰어를 보여줍니다.*

---

## 결론

Aspose OCR을 사용해 **검색 가능한 PDF** 파일을 만드는 데 필요한 모든 과정을 정리했습니다:

- OCR 엔진 초기화.  
- `recognizeImageAndSave` 로 **스캔 이미지 PDF 변환**.  
- `setCreateSearchablePdf(true)` 로 **텍스트 레이어가 삽입된 PDF** 생성.  
- `setCompressionLevel(9)` 로 **고압축 PDF** 구현, 파일을 가볍게 유지.  
- 최적의 정확도를 위해 적절한 `RecognitionLanguage` 로 **OCR 언어 설정**.

이제 배치 처리, 다양한 언어 적용, 여러 스캔 페이지를 하나의 검색 가능한 PDF로 결합하는 실험을 해볼 수 있습니다. 동일한 패턴을 스페인어, 일본어 등 다른 언어에도 적용하려면 `RecognitionLanguage` 열거형만 교체하면 됩니다.

궁금한 점이 있으면 댓글로 알려 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-02-22
description: Java에서 Aspose OCR을 사용하여 스캔된 PDF에서 검색 가능한 PDF를 생성합니다. 스캔된 PDF를 변환하고, PDF
  이미지를 압축하며, PDF OCR을 효율적으로 인식하는 방법을 배워보세요.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: ko
og_description: Aspose OCR을 사용하여 Java에서 스캔된 PDF를 검색 가능한 PDF로 만들기. 이 단계별 튜토리얼에서는 스캔된
  PDF를 변환하고, PDF 이미지 압축 및 PDF OCR 인식을 수행하는 방법을 보여줍니다.
og_title: 검색 가능한 PDF 만들기 – 스캔된 PDF를 변환하는 Java 가이드
tags:
- Java
- OCR
- PDF
- Aspose
title: 검색 가능한 PDF 만들기 – 스캔한 PDF를 변환하는 Java 가이드
url: /ko/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 검색 가능한 PDF 만들기 – 스캔된 PDF를 변환하는 Java 가이드

스캔한 문서가 많이 있을 때 **검색 가능한 PDF**를 만들어야 했던 적 있나요? 흔한 골칫거리죠—PDF는 보이지만 *Ctrl + F* 로는 아무것도 찾을 수 없습니다. 좋은 소식은? Java와 Aspose OCR 몇 줄만으로 이미지 전용 PDF를 완전한 검색 가능한 파일로 바꿀 수 있고, **스캔된 PDF**를 텍스트로 변환하며, **PDF 이미지 압축**으로 결과 파일 크기도 줄일 수 있습니다.  

이 튜토리얼에서는 완전하고 실행 가능한 예제를 단계별로 살펴보고, 각 설정이 왜 중요한지 설명하며, 다중 페이지 스캔이나 저해상도 이미지와 같은 특수 상황에 맞게 프로세스를 조정하는 방법을 보여드립니다. 끝까지 따라오시면 **recognize pdf ocr**를 안정적으로 수행하고 깔끔한 검색 가능한 문서를 생성할 수 있는 견고한 프로덕션 수준 코드를 얻게 됩니다.

---

## 준비물

- **Java 17** (또는 최신 JDK; API는 JDK에 구애받지 않음)  
- **Aspose.OCR for Java** 라이브러리 – Maven Central(`com.aspose:aspose-ocr`)에서 가져올 수 있습니다  
- 검색 가능하게 만들고 싶은 스캔된 PDF(이미지 전용)  
- 익숙한 IDE 또는 텍스트 편집기(IntelliJ, VS Code, Eclipse 등)

무거운 프레임워크도, 외부 서비스도 필요 없습니다—순수 Java와 단일 서드파티 JAR만 있으면 됩니다.  

---

![검색 가능한 PDF 예시](placeholder-image.png "스캔된 문서에서 만든 검색 가능한 PDF의 일러스트레이션")

*이미지 대체 텍스트:* **검색 가능한 PDF** 일러스트레이션 – 스캔된 PDF가 검색 가능한 텍스트로 변환되기 전후를 보여줍니다.

---

## Step 1 – OCR 엔진 초기화  

먼저 해야 할 일은 `OcrEngine` 인스턴스를 생성하는 것입니다. 이 엔진은 PDF 내부의 각 비트맵을 분석하고 Unicode 문자로 변환해 주는 두뇌 역할을 합니다.  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **팁:** 여러 PDF를 연속으로 처리할 경우 매번 새 `OcrEngine`을 만들기보다 동일 인스턴스를 재사용하세요. 몇 밀리초를 절약하고 메모리 사용량도 감소합니다.

---

## Step 2 – PDF 전용 OCR 옵션 설정  

Aspose는 출력 PDF를 구성하는 방식을 세밀하게 조정할 수 있게 해줍니다. 아래 세 가지 설정은 **compress pdf images**를 수행하면서도 검색 가능성을 유지하는 데 가장 큰 영향을 줍니다.

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi가 적당한 균형점이며, 낮은 값은 속도를 높이지만 작은 글자를 놓칠 수 있습니다.  
- **CompressImages** – 내부적으로 무손실 PNG 압축을 활성화합니다; 검색 가능한 PDF는 선명함을 유지하면서도 파일 크기가 작아집니다.  
- **EmbedOriginalImages** – 이 플래그가 없으면 엔진이 원본 래스터 이미지를 버리고 보이지 않는 텍스트만 남깁니다. 이미지를 유지하면 PDF가 스캔본과 정확히 동일하게 보이므로 많은 컴플라이언스 팀에서 요구합니다.

---

## Step 3 – 스캔된 PDF를 `OcrInput`에 로드  

Aspose는 `OcrInput` 래퍼를 통해 소스 파일을 읽습니다. 여러 파일을 추가할 수 있지만, 이번 데모에서는 단일 **image PDF**에 집중합니다.

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **왜 `File`을 직접 전달하지 않을까?** `OcrInput`을 사용하면 여러 PDF를 연결하거나 이미지 파일(PNG, JPEG)과 혼합해서 OCR을 수행할 수 있는 유연성을 얻습니다. 이는 **convert scanned pdf**가 여러 소스로 나뉘어 있을 때 권장되는 패턴입니다.

---

## Step 4 – OCR 수행 및 검색 가능한 PDF를 바이트 배열로 얻기  

이제 마법이 일어납니다. 엔진은 각 페이지를 분석하고 OCR을 실행한 뒤, 원본 이미지와 숨겨진 텍스트 레이어를 모두 포함하는 새 PDF를 생성합니다.

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

다른 용도로 원시 텍스트가 필요하다면(`예: 인덱싱`) `ocrEngine.recognize(ocrInput)`을 호출해 `String`을 반환받을 수 있습니다. 하지만 **create searchable pdf** 목표라면 바이트 배열을 파일로 저장하면 됩니다.

---

## Step 5 – 검색 가능한 PDF를 디스크에 저장  

마지막으로 바이트 배열을 파일에 씁니다. Java NIO를 사용하면 한 줄 코드로 가능합니다.

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

`searchable_output.pdf`를 Adobe Acrobat이나 최신 뷰어에서 열면 이제 텍스트를 선택·복사·검색할 수 있게 됩니다—바로 **image pdf to text** 변환이 약속하는 결과입니다.

---

## OCR로 스캔된 PDF를 텍스트로 변환 (선택 사항)

때로는 새 PDF가 아니라 추출된 순수 텍스트만 필요할 때가 있습니다. 같은 엔진을 재사용하면 됩니다:

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

이 스니펫은 **recognize pdf ocr**를 활용해 검색 인덱스에 입력하거나 자연어 분석을 수행하는 등 후속 처리에 텍스트를 쉽게 제공하는 방법을 보여줍니다.

---

## 파일 크기를 줄이기 위한 PDF 이미지 압축  

소스 스캔이 대용량(예: 600 dpi 컬러 스캔)이라면, 생성된 검색 가능한 PDF도 여전히 무거울 수 있습니다. `setCompressImages(true)` 플래그 외에도 OCR 전에 직접 DPI를 낮출 수 있습니다:

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

DPI를 낮추면 파일 크기가 대략 절반으로 감소하지만 가독성을 테스트해야 합니다—150 dpi 이하에서는 일부 글꼴이 읽기 어려워질 수 있습니다. **compress pdf images**와 OCR 정확도 사이의 트레이드오프는 저장 용량 제약에 따라 결정하십시오.

---

## Recognize PDF OCR 설정 설명  

| 설정 | 출력에 미치는 영향 | 일반적인 사용 사례 |
|------|-------------------|-------------------|
| `setOutputDpi(int)` | OCR 출력의 래스터 해상도를 제어 | 고품질 아카이브(300 dpi) vs. 가벼운 웹 PDF(150 dpi) |
| `setCompressImages` | PNG 압축 활성화 | 이메일 전송이나 클라우드 저장을 위해 PDF 용량을 줄여야 할 때 |
| `setEmbedOriginalImages` | 원본 스캔 이미지를 유지 | 원본 모양을 그대로 유지해야 하는 법률·컴플라이언스 문서 |
| `setLanguage` (선택) | 언어 모델 강제 지정(예: "eng") | 자동 감지가 부정확할 수 있는 다국어 문서 집합 |

이 옵션들을 이해하면 **recognize pdf ocr**를 보다 스마트하게 활용하고 “흐릿한 텍스트” 함정을 피할 수 있습니다.

---

## Image PDF to Text – 흔히 겪는 문제와 해결 방법  

1. **저해상도 스캔** – 150 dpi 이하에서는 OCR 정확도가 급격히 떨어집니다. 소스를 업샘플링하거나 스캐너에서 더 높은 DPI로 스캔하도록 요청하세요.  
2. **페이지 회전** – 페이지가 옆으로 스캔된 경우 자동 회전을 활성화합니다: `pdfOcrOptions.setAutoRotate(true);`.  
3. **암호화된 PDF** – 엔진은 비밀번호가 설정된 파일을 읽을 수 없습니다; Aspose.PDF의 `PdfDocument`를 사용해 먼저 복호화하세요.  
4. **래스터와 텍스트가 혼합된 경우** – 일부 PDF는 이미 숨겨진 텍스트 레이어를 포함하고 있습니다. 다시 OCR을 수행하면 텍스트가 중복될 수 있습니다. `PdfOcrOptions.setSkipExistingText(true);`를 사용해 기존 레이어를 보존하세요.

위 사항들을 해결하면 **create searchable pdf** 파이프라인을 실제 문서 컬렉션에서도 견고하게 운영할 수 있습니다.

---

## 전체 작업 예제 (한 파일에 모든 단계 포함)

아래는 IDE에 복사‑붙여넣기 할 수 있는 완전한 Java 클래스입니다. `YOUR_DIRECTORY`를 실제 폴더 경로로 바꾸세요.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
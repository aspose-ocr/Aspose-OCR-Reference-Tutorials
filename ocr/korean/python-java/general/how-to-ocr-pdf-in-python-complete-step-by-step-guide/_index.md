---
category: general
date: 2026-06-06
description: Python을 사용하여 PDF를 OCR하고, PDF에서 텍스트를 추출하며, 스캔된 PDF 텍스트를 변환하고, 몇 줄의 코드만으로
  OCR 언어를 변경하는 방법.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: ko
og_description: 'Python으로 PDF OCR하기: PDF에서 텍스트를 추출하고, 스캔된 PDF 텍스트를 변환하며, OCR 언어를 손쉽게
  변경하는 방법을 보여주는 실용 가이드.'
og_title: Python에서 PDF OCR하는 방법 – 전체 프로그래밍 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Python에서 PDF OCR 하는 방법 – 완전 단계별 가이드
url: /ko/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 PDF OCR 하는 방법 – 완전 단계별 가이드

비싼 SaaS 도구에 비용을 지불하지 않고 **PDF를 OCR 하는 방법**이 궁금하셨나요? 당신만 그런 것이 아닙니다. 오래된 책을 디지털화하거나, 청구서에서 데이터를 추출하거나, 스캔된 보고서에서 검색 가능한 텍스트가 필요할 때, Python으로 PDF OCR을 마스터하면 수작업 복사를 몇 시간씩 절약할 수 있습니다.

이 튜토리얼에서는 **PDF에서 텍스트를 추출**하는 간결하고 작동하는 예제를 단계별로 살펴보고, **스캔된 PDF 텍스트를** 편집 가능한 문자열로 변환하는 방법, 그리고 문서가 영어가 아닐 경우 **OCR 언어를 변경**하는 방법을 보여줍니다. 마지막까지 따라오시면 어떤 프로젝트에도 바로 넣어 사용할 수 있는 재사용 가능한 스니펫을 얻게 됩니다.

## 사전 요구 사항 및 설정

시작하기 전에 다음이 준비되어 있는지 확인하세요.

- Python 3.8+ 설치 (코드는 3.9, 3.10 및 최신 버전에서도 작동)
- `OcrEngine` 클래스를 제공하는 `ocr` 패키지 (`pip install ocr-lib` 로 설치 – 실제 사용 중인 패키지 이름으로 교체)
- 처리하려는 PDF 파일; 데모에서는 `YOUR_DIRECTORY` 폴더에 위치한 `high_res_book.pdf` 를 사용합니다.

가상 환경을 사용하고 있다면(강력히 권장) 먼저 활성화하세요:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Pro tip:** PDF 파일은 나중에 경로 문제를 피하기 위해 전용 `data/` 디렉터리 아래에 보관하세요.

## Step 1: OCR 엔진 인스턴스 생성 (How to OCR PDF – Initialization)

**PDF에 OCR을 수행**하려면 가장 먼저 해야 할 일은 엔진을 인스턴스화하는 것입니다. 엔진은 각 페이지를 읽고, 글리프를 해석하고, 순수 텍스트를 반환하는 두뇌와 같습니다.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

왜 중요한가요: 엔진이 없으면 언어 설정, 렌더링 옵션, PDF 처리와 같은 컨텍스트가 없습니다. `OcrEngine` 객체는 이러한 기본값을 보관하고 나중에 조정할 수 있게 해줍니다.

## Step 2: 인식 언어 설정 (Change OCR Language)

대부분의 OCR 라이브러리는 기본값이 영어이지만, 문서가 프랑스어, 독일어, 혹은 일본어라면 어떻게 할까요? 언어를 변경하는 것은 `set_recognition_language` 를 호출하는 것만큼 간단합니다. 이는 **OCR 언어 변경** 요구 사항을 충족시키며 정확도를 높여줍니다.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **왜 필요할 수 있나요:** 다국어 아카이브에는 혼합 언어 페이지가 자주 등장합니다. 실행 중에 언어를 전환하면 “ß”나 “ñ” 같은 문자를 오인식하는 일을 방지할 수 있습니다.

## Step 3: PDF 렌더링 옵션 구성 (Convert Scanned PDF Text Effectively)

스캔된 PDF를 다룰 때 해상도와 색상 모드는 OCR 품질에 큰 영향을 미칩니다. 대부분의 문서에 대해 300 DPI, 그레이스케일 렌더링이 최적의 균형을 이룹니다—세부 사항을 충분히 포착하면서 메모리 사용량은 적당합니다.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

연쇄 호출은 보기엔 화려해 보이지만, 매번 같은 옵션 객체를 반환하는 유창한 API일 뿐입니다. 컬러 다이어그램이 필요하면 `"grayscale"` 을 `"color"` 로 바꾸면 됩니다.

## Step 4: PDF 인식 및 첫 페이지 텍스트 추출 (Extract Text from PDF)

이제 **PDF에 OCR을 수행**하는 핵심 단계가 나옵니다: 엔진에 파일 경로를 전달하고 인식된 텍스트를 받아옵니다. 메서드는 페이지 결과 리스트를 반환하며, 각 결과는 `text` 속성을 포함합니다.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

전체 문서가 필요하면 `results` 를 순회하세요:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### PDF가 암호화된 경우는?

일부 PDF는 비밀번호로 보호됩니다. 이 경우 `recognize_pdf` 에 비밀번호를 전달하면 됩니다:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

엔진이 OCR을 수행하기 전에 즉시 복호화하므로 별도의 단계가 필요 없습니다.

## Step 5: 추출된 텍스트 후처리 (Fine‑Tuning Extract Text from PDF)

원시 OCR 결과물은 줄 바꿈, 불필요한 공백, 혹은 가끔씩 잘못 인식된 문자들을 포함합니다. 간단한 정리 루틴을 적용하면 추출된 문자열을 다운스트림 처리(검색 인덱싱, 데이터베이스 저장 등)에 바로 사용할 수 있습니다.

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

이제 **PDF에서 텍스트를 추출**하고 이를 어떤 NLP 파이프라인, 검색 엔진, 혹은 간단한 `open(...).write()` 작업에 안전하게 전달할 수 있습니다.

## Bonus: 여러 PDF 일괄 처리 (Scaling Perform OCR on PDF)

스캔된 PDF가 가득한 폴더가 있다면 로직을 루프에 감싸면 됩니다:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

이 스니펫은 **PDF에 OCR을 수행**하는 작업을 대량으로 처리하는 방법을 보여주며, 디지털화 프로젝트에서 흔히 요구됩니다.

## Expected Output

단일 페이지 예제(Step 4)를 실행하면 다음과 유사한 출력이 표시됩니다:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

다중 페이지 책을 처리하면 콘솔에 각 페이지의 정제된 텍스트가 출력되고, 배치 스크립트는 각 PDF 옆에 `.txt` 파일을 생성합니다.

## Common Pitfalls & How to Avoid Them

| Issue | Symptoms | Fix |
|-------|----------|-----|
| Low‑resolution source PDF | Garbled characters, missing words | Increase DPI (`set_dpi(400)` or higher) |
| Wrong language set | Many unknown symbols, especially accented characters | Use `engine.set_recognition_language(ocr.Language.FRENCH)` or the appropriate enum |
| Large PDF causing memory error | `MemoryError` or crash after a few pages | Process pages in chunks (`engine.recognize_pdf(..., max_pages=10)`) |
| Missing fonts in the PDF | Blank output for certain pages | Ensure the PDF actually contains raster images; some PDFs are vector‑only and need different handling |

## Image Illustration

아래는 워크플로우를 한눈에 보여주는 간단한 시각 자료입니다. 대체 텍스트는 SEO 친화적으로 작성되었습니다.

![how to ocr pdf workflow diagram showing engine initialization, language setting, rendering options, recognition, and text extraction](/images/ocr-workflow.png)

*다이어그램 자체가 코드 실행에 필수적인 것은 아니지만, 시각 학습자에게 각 단계가 어디에 해당하는지 이해시키는 데 도움이 됩니다.*

## Conclusion

Python에서 **PDF에 OCR을 수행**하는 전체 과정을 다뤘습니다: OCR 엔진 생성, **OCR 언어 변경**, **스캔된 PDF 텍스트 변환**을 위한 렌더링 설정, 그리고 최종적으로 **PDF에서 텍스트 추출**까지. 완전하고 실행 가능한 예제는 어떤 프로젝트에도 바로 삽입할 수 있으며, 선택적인 배치 스크립트는 솔루션을 확장하는 방법을 보여줍니다.

다음 단계로 고려해볼 내용:

- 다국어 아카이브를 위해 언어 리스트를 순회하며 **PDF에 OCR을 수행**하기
- 추출된 텍스트를 Elasticsearch와 연동해 전체 텍스트 검색 구현
- OCR을 사용해 원본 파일에 텍스트 레이어를 삽입해 검색 가능한 PDF 만들기(`save_as_searchable_pdf` 메서드를 제공하는 라이브러리 다수)

실험하고, DPI 설정을 조정하고, 다른 OCR 백엔드로 교체해 보세요. 기본 원리는 동일하며, 이제 튼튼한 기반을 갖추셨습니다.

행복한 코딩 되시고, 스캔된 문서가 마침내 검색 가능해지길 바랍니다!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-26
description: OCR을 사용하여 PDF 텍스트를 추출하는 방법. PDF를 이미지로 로드하고, PDF 텍스트를 인식하며, 간단한 Python
  예제로 PDF에서 텍스트를 추출하는 방법을 배워보세요.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: ko
og_description: OCR을 사용하여 PDF 텍스트를 추출하는 방법. 이 가이드는 PDF를 이미지로 로드하고, PDF 텍스트를 인식하며,
  Python에서 PDF 텍스트를 추출하는 방법을 보여줍니다.
og_title: OCR로 PDF 텍스트 추출하는 방법 – 전체 튜토리얼
tags:
- OCR
- Python
- PDF processing
title: OCR로 PDF 텍스트 추출하는 방법 – 완전 단계별 가이드
url: /ko/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR을 사용해 PDF 텍스트 추출하기 – 완전 단계별 가이드

스캔 이미지뿐인 **PDF 파일을 어떻게 추출할지** 궁금하셨나요? 혼자가 아닙니다—검색 가능한 콘텐츠가 필요하지만 이미지 전용 PDF만 가지고 있는 개발자들이 많이 겪는 문제입니다. 좋은 소식은? 몇 줄의 코드와 강력한 OCR 라이브러리만 있으면 사진‑PDF를 순식간에 일반 텍스트로 바꿀 수 있다는 것입니다.  

이 튜토리얼에서는 **OCR을 사용해** PDF를 이미지로 로드하고, PDF 텍스트를 인식하며, 최종적으로 **PDF에서 텍스트를 추출하는** 방법을 단계별로 살펴봅니다. 끝까지 따라오시면 실행 가능한 스크립트와 각 단계에 대한 명확한 설명, 그리고 흔히 마주치는 함정을 피하는 팁을 얻으실 수 있습니다.

## 준비물

- Python 3.9 이상 (코드는 3.10+에서도 동작)  
- `ocr` Python 패키지 (또는 `OcrEngine`, `OcrEngineMode`, `Imaging.Image`를 제공하는 호환 OCR 라이브러리)  
- 처리하고 싶은 다중 페이지 PDF (예시에서는 `multi_page.pdf`라고 부릅니다)  
- 가상 환경에 대한 기본 지식 (선택 사항이지만 권장)

> **Pro tip:** Windows에서는 Anaconda Prompt를, macOS/Linux에서는 `python -m venv venv && source venv/bin/activate` 한 줄로 환경을 만들면 됩니다.

## Step 1: OCR 라이브러리 설치

먼저 PyPI에서 OCR 패키지를 받아옵니다. 아래 예시는 코드 스니펫에 표시된 API와 동일한 가상의 `ocr` 패키지를 사용하지만, 실제 라이브러리(`pytesseract` + `pdf2image` 등)도 동일한 패턴을 따릅니다.

```bash
pip install ocr
```

다른 엔진을 사용한다면 `ocr`을 해당 이름으로 교체하세요(예: `pip install pytesseract pdf2image`).

## Step 2: OCR 엔진 초기화

엔진 인스턴스를 만드는 것이 **PDF 텍스트를 어떻게 추출할지**의 기본입니다. 엔진은 각 PDF 페이지의 픽셀을 해석하는 두뇌 역할을 합니다.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **왜 중요한가:** `set_engine_mode`를 통해 속도와 정확도 사이를 조정할 수 있습니다. `DEFAULT`는 균형 잡힌 선택이며, 더 높은 정밀도가 필요하면 `HIGH_ACCURACY`(라이브러리 지원 시)로 전환하면 됩니다.

## Step 3: PDF를 이미지 객체로 로드

OCR은 이미지에서 동작하므로 PDF를 이미지 형태로 변환해야 합니다. `Imaging.Image.load` 메서드는 다중 페이지 PDF를 자동으로 처리합니다.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **예외 상황:** 일부 라이브러리는 단일 페이지 이미지만 받습니다. 이 경우 `pdf2image.convert_from_path`를 사용해 페이지별로 루프를 돌려야 합니다. 우리의 `load` 호출은 이를 추상화해 **PDF를 이미지로 로드**하는 과정을 한 줄로 만들었습니다.

## Step 4: 모든 페이지에서 텍스트 인식

이제 **PDF 텍스트 인식**의 핵심 단계입니다. 엔진이 각 페이지를 스캔하고 페이지당 하나씩 결과 객체 리스트를 반환합니다.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

각 `page_result`에는 `get_text()`(평문)와 `get_confidence()`(선택적 품질 지표) 같은 메서드가 포함됩니다.  

> **팁:** 첫 페이지만 필요하다면 다중 페이지 헬퍼 대신 `recognize(pdf_image[0])`를 호출하면 됩니다.

## Step 5: 결과를 순회하며 추출된 텍스트 출력

마지막으로 결과를 순회하면서 각 페이지의 텍스트를 출력합니다. 이렇게 하면 **PDF에서 텍스트를 추출**하는 워크플로가 완성됩니다.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### 예상 출력

`multi_page.pdf`에 “Hello”, “World”, “Python”이라는 단어가 각각의 페이지에 들어 있다면 다음과 같이 표시됩니다.

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

이제 PDF가 완전히 검색 가능해졌으며, 텍스트는 후속 처리(인덱싱, 감성 분석 등)에 바로 사용할 수 있습니다.

## Step 6: 흔히 발생하는 문제 처리

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blank output** | PDF 페이지가 낮은 DPI로 스캔돼 문자 구분이 어려움. | OCR 전에 이미지를 확대: `pdf_image = pdf_image.resize(300)` (300 DPI가 적당). |
| **Garbage characters** | 라틴 문자 외 언어는 별도 언어 팩 필요. | 해당 언어 모델 로드: `ocr_engine.load_language('spa')` (스페인어 등). |
| **Memory blow‑up on huge PDFs** | 모든 페이지를 한 번에 로드하면 RAM 소모가 큼. | 페이지를 청크로 처리: `for img in pdf_image.split(batch=10): …` (의사 코드). |
| **Slow performance** | 대용량 문서에 `DEFAULT` 모드를 쓰면 느려짐. | `FAST` 모드로 전환하거나 `concurrent.futures`로 병렬 OCR 실행. |

## 보너스: 추출된 텍스트를 파일에 저장하기

실제 파이프라인에서는 텍스트를 지속적으로 보관해야 합니다. 아래 작은 헬퍼는 모든 내용을 `output.txt`에 기록합니다.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

이제 `output.txt`를 검색 엔진, 데이터베이스, 혹은 어떤 NLP 모델에도 연결할 수 있습니다.

## 전체 스크립트 한 번에 보기

아래는 완전한 실행 가능한 프로그램입니다. 복사·붙여넣기 후 파일 경로만 조정하면 바로 사용할 수 있습니다.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

실행하기:

```bash
python extract_pdf_ocr.py
```

각 페이지 내용이 콘솔에 출력되고, `extracted_text.txt` 파일이 생성되었다는 확인 메시지가 표시됩니다.

## 결론

이미지 전용 문서에서 OCR 엔진을 이용해 **PDF 텍스트를 추출하는 방법**을 설치부터 다중 페이지 결과 처리, 출력 저장까지 모두 다뤘습니다. 이제 **OCR을 어떻게 사용하는지**, **PDF를 이미지로 로드하는 방법**, **PDF 텍스트를 인식하는 방법**을 확실히 알게 되었습니다.  

다음 단계는? 기본 엔진 모드를 고정밀 모드로 바꾸어 보거나, 다국어 PDF를 위해 언어 팩을 실험해 보세요. 혹은 추출된 텍스트를 Elasticsearch 같은 전체 텍스트 검색 인덱스로 파이프라인에 연결해 보세요. 텍스트 추출 기본기를 마스터했으니 이제 무한한 가능성이 열려 있습니다.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="PDF 추출 워크플로우 다이어그램"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
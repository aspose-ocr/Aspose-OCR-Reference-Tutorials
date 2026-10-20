---
category: general
date: 2026-06-25
description: Python을 사용해 PDF에 OCR을 수행하기—OCR을 위해 PDF를 로드하는 방법, PDF 페이지에서 텍스트를 추출하는
  방법, 그리고 인식된 텍스트를 효율적으로 미리 보는 방법을 배워보세요.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: ko
og_description: Python에서 PDF에 OCR을 수행합니다. 이 가이드는 OCR을 위해 PDF를 로드하고, PDF 페이지에서 텍스트를
  추출하며, 인식된 텍스트를 빠르게 미리 보는 방법을 보여줍니다.
og_title: Python으로 PDF에서 OCR 수행 – 단계별 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Python으로 PDF에서 OCR 수행하기 – 완전 가이드
url: /ko/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF에서 Python으로 OCR 수행 – 완전 가이드

스캔한 계약서가 산더미처럼 쌓여 있거나, 일반 텍스트 추출기로는 읽히지 않는 방대한 핸드북을 다루어야 할 때 **PDF에 OCR을 수행**해야 할 필요를 느낀 적이 있나요? 요컨대, **PDF를 OCR용으로 로드**하고 텍스트를 추출한 뒤, 메모리 사용량을 크게 늘리지 않으면서 빠르게 미리보기를 보고 싶으신 거죠.

바로 여기서 답을 찾으실 수 있습니다. 이번 튜토리얼에서는 **PDF 페이지에서 텍스트를 추출**하는 완전한 파이썬 스크립트를 단계별로 살펴보고, **인식된 텍스트를 미리보기**하는 방법과 **대용량 PDF를 효율적으로 OCR**하는 고전적인 문제까지 다룹니다.

튜토리얼을 마치면 바로 실행 가능한 프로그램을 손에 넣고, 각 설정 옵션을 명확히 이해하며, 초보자들이 흔히 겪는 함정을 피할 수 있는 팁도 얻을 수 있습니다.

---

## 배울 내용

- `aocr` 라이브러리를 사용해 **PDF를 OCR용으로 로드**하는 방법
- **PDF 페이지마다 OCR을 수행**하는 정확한 단계
- 메모리 사용량을 관리하면서 **PDF 페이지에서 텍스트를 추출**하는 방법
- 결과를 검증하기 위해 **인식된 텍스트를 미리보기**하는 방법
- **대용량 PDF**를 RAM을 고갈시키지 않고 처리하는 전략

> **팁:** 이 가이드는 Python 3.9+가 설치되어 있고 가상 환경에 대한 기본적인 이해가 있다고 가정합니다. Python이 처음이라면 먼저 virtualenv를 설정하세요—나중에 겪게 될 골칫거리를 크게 줄여줍니다.

---

## 사전 준비 사항

| Requirement | Why it matters |
|-------------|----------------|
| `aocr` Python 패키지 (또는 호환 가능한 OCR 엔진) | 스크립트 전반에 사용되는 `OcrEngine` 클래스를 제공합니다. |
| `pip` 및 가상 환경 | 시스템 파이썬과 의존성을 분리합니다. |
| 임시 이미지 추출을 위한 충분한 디스크 공간 | 일부 OCR 엔진은 페이지 이미지를 디스크에 저장한 뒤 처리합니다. |
| 선택 사항: 진행 표시줄을 위한 `tqdm` | **대용량 PDF를 OCR**할 때 사용자 경험을 향상시킵니다. |

필수 항목을 설치하려면 다음을 실행하세요:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

PDF가 비밀번호로 보호되어 있다면, 나중에 비밀번호를 제공해야 합니다—“예외 상황” 섹션을 참고하세요.

---

## 1단계: OCR 엔진 설정 – OCR 엔진 인스턴스 만들기

우선 OCR 엔진 인스턴스를 만들어야 합니다. 이는 각 페이지 이미지를 읽고 순수 텍스트로 변환하는 두뇌 역할을 합니다.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **`max_memory_mb`를 설정하는 이유**  
> OCR 엔진은 페이지 이미지를 RAM에 캐시하는 경우가 많습니다. 메모리 상한을 지정하면 500페이지짜리 계약서 같은 대용량 파일에서도 스크립트가 중단되는 일을 방지할 수 있습니다.

---

## 2단계: PDF를 OCR용으로 로드하고 설정 구성하기

이제 실제로 **PDF를 OCR용으로 로드**합니다. 경로는 절대 경로나 상대 경로나 상관없으며, 파일이 존재하는지 확인만 하면 됩니다.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

PDF가 암호화된 경우 `engine.load_pdf`가 예외를 발생시킵니다. 이때는 `engine.load_pdf(pdf_path, password="secret")`와 같이 비밀번호를 전달하면 됩니다—자세한 내용은 뒤에서 다룹니다.

---

## 3단계: PDF 페이지에서 텍스트 추출 – 핵심 루프

여기서 **PDF 페이지마다 OCR을 수행**합니다. 또한 **인식된 텍스트를 미리보기**하여 처음 몇 백 글자를 확인함으로써 정상 동작 여부를 검증합니다.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **프로 팁:** `tqdm` 진행 표시줄은 특히 **대용량 PDF**를 처리할 때 시각적인 힌트를 제공해 줍니다.

---

## 4단계: 전체 합치기 – 바로 실행 가능한 스크립트

아래는 완전한 실행 예시입니다. `pdf_ocr.py`라는 파일명으로 저장한 뒤 `python pdf_ocr.py path/to/your/file.pdf` 명령으로 실행하세요.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### 예상 출력 (일부)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

각 페이지에 대한 짧은 미리보기가 표시되고, 최종적으로 모든 텍스트를 합친 파일이 성공적으로 저장되었다는 확인 메시지가 출력됩니다.

---

## 예외 상황 및 실전 팁

| Situation | What to Do |
|-----------|------------|
| **암호화된 PDF** | 비밀번호를 전달합니다: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **매우 큰 PDF (> 1000 페이지)** | `max_memory_mb` 값을 신중히 늘리거나, 200페이지씩 나누어 처리합니다. |
| **혼합된 콘텐츠(인쇄물 + 손글씨)** | 라이브러리가 지원한다면 `engine.recognition_mode`를 `aocr.RecognitionMode.MIXED`로 전환합니다. |
| **폰트 누락 또는 스캔 품질 저하** | `recognize()` 호출 전에 Pillow 등 이미지 보정 라이브러리로 페이지를 전처리합니다. |
| **메모리 초과 충돌** | `preview_len`을 줄이거나, 모든 텍스트를 리스트에 보관하지 말고 바로 디스크에 기록합니다. |

---

## 대용량 PDF를 효율적으로 OCR하는 방법 – 고급 전략

**대용량 PDF**를 다룰 때는 속도와 안정성이 핵심입니다. 스크립트에 적용할 수 있는 몇 가지 요령을 소개합니다:

1. **페이지 단위 병렬 처리** – OCR 엔진이 스레드 안전하다면 `concurrent.futures.ThreadPoolExecutor`를 활용합니다.  
2. **중간 이미지 캐시** – 일부 엔진은 래스터화된 페이지를 SSD에 저장하도록 지원해 재실행 시 CPU 부하를 크게 줄여줍니다.  
3. **배치 출력 쓰기** – 파이썬 리스트에 누적하는 대신, 출력 파일을 한 번 열어두고 페이지별 텍스트를 바로 기록합니다.  
4. **DPI 조정** – 래스터화 시 DPI를 낮추면 메모리 사용량이 감소하지만 정확도에 영향을 줄 수 있습니다. 보통 200‑300 DPI 사이가 적절합니다.

아래는 OCR 단계를 병렬화하는 간단한 예시입니다(선택 사항, 사용하려면 주석을 해제하세요):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

※ 병렬 처리는 CPU 사용량을 크게 늘릴 수 있으니, 장시간 실행 시 시스템 온도를 모니터링하세요.

---

## 자주 묻는 질문

**Q: 이 스크립트를 Tesseract 같은 다른 OCR 라이브러리와 함께 사용할 수 있나요?**  
A: 물론 가능합니다. `aocr` 호출 부분을 `pytesseract.image_to` 등으로 교체하면 됩니다.

## 다음에 배울 내용은?

다음 튜토리얼들은 이번 가이드에서 다룬 기술을 확장하고, 추가 API 기능을 마스터하거나 대체 구현 방식을 탐구하는 데 도움이 됩니다. 각 자료에는 완전한 코드 예제와 단계별 설명이 포함되어 있습니다.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
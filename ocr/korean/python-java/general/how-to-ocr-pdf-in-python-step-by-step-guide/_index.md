---
category: general
date: 2026-03-28
description: Python으로 PDF를 빠르게 OCR하는 방법을 배워보세요. 이 가이드는 PDF에서 텍스트를 추출하고, PDF의 텍스트를
  인식하며, Aspose OCR을 사용해 스캔된 PDF를 텍스트로 변환하는 방법을 보여줍니다.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: ko
og_description: Python으로 PDF OCR을 마스터하세요. PDF에서 텍스트를 추출하고, PDF의 텍스트를 인식하며, 스캔한 PDF를
  몇 분 안에 텍스트로 변환합니다.
og_title: Python에서 PDF를 OCR하는 방법 – 완전 가이드
tags:
- PDF
- OCR
- Python
- Aspose
title: Python에서 PDF OCR 하는 방법 – 단계별 가이드
url: /ko/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python으로 PDF OCR하기 – 단계별 가이드

PDF 파일이 페이지 사진일 때 **PDF를 OCR하는 방법**이 궁금하셨나요? 당신만 그런 것이 아닙니다. 이번 튜토리얼에서는 PDF 파일을 OCR하고, PDF에서 텍스트를 추출하며, 스캔한 PDF를 검색 가능한 텍스트로 변환하는 정확한 과정을 순서대로 살펴보겠습니다—모두 순수 Python 코드만 사용합니다.

Aspose OCR 라이브러리 설치부터 각 페이지에서 인식된 텍스트를 추출하는 방법까지 모두 다룹니다. 최종적으로 **Python으로 PDF OCR**, **PDF에서 텍스트 추출**, **스캔한 PDF를 텍스트로 변환**하는 방법을 배워서 흩어져 있는 문서를 찾아 헤맬 필요 없이 바로 적용할 수 있습니다. 불필요한 내용은 없으며, 복사‑붙여넣기만 하면 바로 실행 가능한 실용적인 예제입니다.

## 준비물

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* Python 3.8+ (가장 최신 안정 버전 권장)  
* Aspose OCR for Python 라이선스 또는 무료 체험 키 – Aspose 웹사이트에서 받을 수 있습니다.  
* 처리하고자 하는 스캔 PDF 파일 (`input.pdf` 라고 부르겠습니다).  

이미 모두 갖추었다면 바로 시작해도 좋습니다. 아직이라면 패키지 설치가 매우 간단하니 곧 알려드리겠습니다.

## PDF OCR 설정 – 환경 구성

먼저 Aspose OCR 모듈을 로컬에 설치해야 합니다. 패키지 이름은 `aspose-ocr`이며, pip으로 설치할 수 있습니다:

```bash
pip install aspose-ocr
```

> **프로 팁:** 가상 환경(`python -m venv venv`)을 사용하면 의존성을 깔끔하게 관리할 수 있습니다.

패키지가 설치되면 이제 import하고 OCR 엔진을 시작할 준비가 됩니다. 이것이 이후 **python으로 ocr pdf** 워크플로우의 기반이 됩니다.

## Python으로 PDF OCR – Aspose OCR 가져오기

라이브러리를 사용할 수 있게 되었으니 스크립트에 import합니다. 또한 엔진을 *direct PDF mode* 로 설정해 Aspose가 각 페이지를 이미지로 변환하지 않고 PDF 바이트를 바로 읽도록 합니다.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

`PdfMode.DIRECT`를 사용하는 이유는 무엇일까요? 추가적인 래스터화 단계를 건너뛰어 처리 속도가 빨라지고 원본 레이아웃을 그대로 유지하기 때문입니다—특히 **PDF에서 텍스트 인식** 정확도가 중요한 경우에 유용합니다.

## PDF에서 텍스트 인식 – 엔진 실행

엔진이 준비되었으니 스캔한 파일을 지정합니다. `recognize_from_pdf` 메서드가 모든 작업을 수행합니다: 각 페이지를 파싱하고 OCR 알고리즘을 실행한 뒤 `OcrResult` 객체를 반환합니다. 이 객체는 `Page` 객체들의 컬렉션을 포함합니다.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

암호가 설정된 PDF도 동작할까요? 네, `ocr_engine.password = "secret"` 를 `recognize_from_pdf` 호출 전에 지정하면 됩니다. 많은 튜토리얼이 놓치는 부분이지만 실제 파이프라인에서는 유용합니다.

## PDF에서 텍스트 추출 – 페이지 결과 접근

`ocr_result.pages` 리스트에는 페이지당 하나씩 `Page` 객체가 들어 있습니다. 각 `Page` 객체의 `.text` 속성에 스캔된 페이지의 순수 텍스트가 담겨 있습니다. 이제 루프를 돌면서 결과를 출력해 보겠습니다.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

스크립트를 실행하면 다음과 비슷한 출력이 나타납니다:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

이 출력은 **PDF에서 텍스트 추출**과 **PDF에서 텍스트 인식**을 성공적으로 수행했음을 증명합니다. 이제 문자열을 데이터베이스, 검색 인덱스, 혹은 downstream NLP 파이프라인에 전달할 수 있습니다.

![OCR PDF 예시](placeholder-image.png "OCR PDF 예시")

*이미지 대체 텍스트:* **OCR PDF 예시** – 페이지별 인식된 텍스트의 콘솔 출력 예시.

## 스캔 PDF를 텍스트로 변환 – 결과 저장

대부분의 개발자는 콘솔에 출력되는 텍스트만으로는 부족하고, 파일로 저장하고 싶어합니다. 아래는 각 페이지 텍스트를 별도의 `.txt` 파일에 기록하는 작은 헬퍼 코드로, **스캔 PDF를 텍스트로 변환**하는 작업을 `output` 폴더에 수행합니다.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

스크립트가 끝나면 다음과 같은 정돈된 디렉터리를 얻게 됩니다:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

이제 **스캔 PDF를 텍스트로 변환**했으며, 해당 파일들을 검색, 분석, 혹은 간단한 `grep` 등 어떤 downstream 프로세스에도 활용할 수 있습니다.

## 자주 묻는 질문 및 예외 상황

**PDF에 이미지와 실제 텍스트가 혼합돼 있으면 어떻게 하나요?**  
Aspose OCR은 모든 내용을 인식하려 시도하지만, 이미 선택 가능한 텍스트가 포함된 페이지에 대해서는 OCR을 비활성화해 속도를 높일 수 있습니다. `ocr_engine.auto_detect_page_orientation = True` 로 설정하고, 이미 텍스트가 있는 페이지에 대해서는 `ocr_engine.recognize_from_pdf(..., detect_text=False)` 를 호출하세요.

**언어 모델을 제어할 수 있나요?**  
물론입니다. `ocr_engine.language = aocr.Language.English` (또는 지원되는 다른 언어) 로 설정하면 비영어 문서의 정확도가 향상됩니다.

**페이지 수가 많은 대용량 PDF(100페이지 이상)를 어떻게 처리하나요?**  
청크 단위로 처리합니다. `recognize_from_pdf` 메서드는 `page_range` 인자를 받으므로, 예를 들어 `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))` 와 같이 범위를 지정하고 반복하면 메모리 사용량을 낮출 수 있습니다.

## 전체 작업 예제

모든 내용을 하나로 합친 스크립트를 아래에 제공합니다. `ocr_pdf.py` 라는 파일에 저장하고 실행하면 됩니다:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

실행 방법:

```bash
python ocr_pdf.py
```

각 페이지 텍스트와 저장된 `.txt` 파일 위치가 콘솔에 출력될 것입니다.

## 결론

우리는 **Python으로 PDF OCR**하는 방법을 다루었고, 깔끔하게 **python으로 ocr pdf**를 수행하는 방법, **PDF에서 텍스트 추출**, **PDF에서 텍스트 인식** 메커니즘, 그리고 **스캔 PDF를 텍스트로 변환**하는 완전한 예제를 제공했습니다. 전체 과정이 이렇게 정리됩니다.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
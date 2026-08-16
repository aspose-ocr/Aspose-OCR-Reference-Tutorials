---
category: general
date: 2026-03-18
description: 이미지에 OCR을 실행하여 PNG에서 텍스트를 추출하고 검색 가능한 PDF를 생성합니다. 몇 분 안에 텍스트 이미지를 인식하고
  PNG를 PDF로 변환하는 방법을 배워보세요.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: ko
og_description: PNG 이미지에서 텍스트를 추출하기 위해 OCR을 실행하고, 텍스트 이미지를 인식한 뒤 검색 가능한 PDF를 생성합니다.
  이 단계별 가이드를 따라 주세요.
og_title: 이미지에서 OCR 실행 – PNG에서 텍스트를 빠르게 추출
tags:
- OCR
- Python
- Image Processing
title: 이미지에서 OCR 실행 – PNG에서 텍스트를 빠르게 추출
url: /ko/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 OCR 실행 – PNG에서 텍스트 빠르게 추출

이미지 파일에 **OCR을 실행**해야 하는데 어디서 시작해야 할지 몰랐던 적이 있나요? 스캔한 기사 파일이 `article.png`로 저장돼 있고 단순히 텍스트만 원하거나, 보관을 위해 검색 가능한 PDF가 필요할 수도 있습니다. 어느 경우든 올바른 곳에 오셨습니다. 이번 튜토리얼에서는 PNG에서 텍스트를 추출하고, 텍스트 이미지를 인식하며, 그 PNG를 검색 가능한 PDF로 변환하는 과정을 몇 줄의 코드만으로 진행해 보겠습니다.

> **얻을 수 있는 것:** PNG를 로드하고 OCR을 실행하며 hOCR 출력을 저장하고, 필요에 따라 검색 가능한 PDF까지 생성하는 완전한 실행 가능한 스크립트입니다. 누락된 import도 없고, “문서를 참고하세요” 같은 막다른 길도 없습니다—오늘 바로 프로젝트에 넣어 사용할 수 있는 독립형 솔루션입니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- **Python 3.8+** (여기 사용된 문법은 최신 버전에서 모두 동작합니다)
- 사용 중인 **`ocr_engine`** 라이브러리 (예시에서는 `OcrEngine` 클래스를 가정합니다; 필요에 따라 Tesseract, EasyOCR 등으로 교체하세요)
- 처리하고자 하는 PNG 이미지 (예: 프로젝트 폴더에 `article.png`가 위치함)
- 출력 디렉터리에 대한 쓰기 권한

Tesseract를 사용한다면 다음 명령으로 설치합니다:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

그 다음 Python 래퍼를 설치합니다:

```bash
pip install pytesseract Pillow
```

*Pro tip:* OCR 라이브러리를 최신 상태로 유지하세요—새 언어 팩과 성능 개선이 자주 추가됩니다.

## Run OCR on Image – Step‑by‑Step Guide

아래는 **전체 스크립트**입니다. `run_ocr.py`라는 파일에 복사‑붙여넣기하고 `python run_ocr.py`로 실행해 보세요.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### What the script does, in plain English

1. **Instantiate** the OCR engine so you can control its settings.  
   OCR 엔진을 인스턴스화하여 설정을 제어합니다.
2. **Load** the PNG file (`article.png`). The script aborts early if the file isn’t there—no mysterious `NoneType` errors later.  
   PNG 파일(`article.png`)을 로드합니다. 파일이 없으면 스크립트가 바로 중단되어 `NoneType` 오류가 발생하지 않습니다.
3. **Select** `hocr` as the export format. This format keeps the original layout, which is essential for later converting the image into a searchable PDF.  
   `hocr`을 내보내기 형식으로 선택합니다. 이 형식은 원본 레이아웃을 보존하므로 나중에 검색 가능한 PDF로 변환할 때 필수적입니다.
4. **Run** the recognition engine; the heavy lifting happens here.  
   인식 엔진을 실행합니다. 여기서 실제 OCR 작업이 수행됩니다.
5. **Write** the hOCR XML to `article.hocr`. You now have a machine‑readable representation of the text and its coordinates.  
   hOCR XML을 `article.hocr`에 기록합니다. 이제 텍스트와 좌표가 기계가 읽을 수 있는 형태로 저장됩니다.
6. *(Optional)* Switch to `"pdf"` and generate a searchable PDF in one extra step.  
   *(선택 사항)* `"pdf"`로 전환하여 한 단계 더 진행하면 검색 가능한 PDF를 생성합니다.

The **expected output** is a UTF‑8‑encoded `.hocr` file that looks something like this (trimmed for brevity):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

If you uncomment the PDF section, you’ll also end up with `article_searchable.pdf`, which you can open in any PDF viewer and use the **Ctrl + F** search box to locate words instantly.

![이미지에서 OCR 실행 예시 출력](example.png "이미지에서 OCR 실행 – hOCR 및 PDF 결과")

## How to Extract Text from PNG Using OcrEngine

원시 텍스트만 필요하고(레이아웃이나 PDF가 필요 없을 경우) hOCR 단계를 완전히 건너뛰고 싶다면 다음과 같이 하면 됩니다:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Why choose plain text?* It’s lightweight, perfect for indexing, and works great with downstream NLP pipelines.

**왜 순수 텍스트를 선택하나요?** 가볍고 인덱싱에 최적이며, 이후 NLP 파이프라인과도 잘 어울립니다.

## Recognize Text Image and Generate Searchable PDF

검색 가능한 PDF를 만들려면 두 단계가 필요합니다:

1. **Run OCR** with `hocr` (as we did above) to get the layout information.  
   위와 같이 `hocr` 형식으로 OCR을 실행해 레이아웃 정보를 얻습니다.
2. **Combine** the original PNG with the hOCR into a PDF using the engine’s PDF exporter.  
   엔진의 PDF 내보내기 기능을 사용해 원본 PNG와 hOCR을 결합해 PDF를 생성합니다.

Most modern OCR libraries (Tesseract, ABBYY, Google Vision) expose a `pdf` export that does exactly this. The snippet in the *Optional* block of the main script shows the pattern. If your library doesn’t have a built‑in PDF exporter, you can use **`pdf2image`** + **`reportlab`** to stitch the image and hOCR together—just let me know, and I’ll share a quick extra example.

## Convert PNG to PDF with OCR Output

때때로 **검색 레이어가 없는 순수 PDF**만 필요할 때가 있습니다. 이 경우는 훨씬 간단합니다:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

OCR 단계와 결합하면 검색 가능한 버전을 만들 수 있고, 그렇지 않으면 아카이브용으로 시각적으로 정확한 복제본을 유지할 수 있습니다.

## Common Pitfalls & Tips

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blurry or low‑resolution PNG** | OCR accuracy drops dramatically below ~300 DPI. | `Image.resize((width*2, height*2), Image.LANCZOS)` 로 업스케일한 뒤 엔진에 전달합니다. |
| **Wrong language** | Engine defaults to English; non‑English characters become garbled. | `ocr_engine.setLanguage('deu')` (또는 해당 ISO 코드) 를 `recognize()` 전에 호출합니다. |
| **Missing hOCR output** | Some engines default to plain text when `setExportFormat` isn’t called. | `setExportFormat("hocr")` 가 **recognize()** **이전**에 실행되는지 확인합니다. |
| **File permission errors** | Trying to write to a read‑only folder. | 프로젝트 내부 경로나 `os.makedirs(..., exist_ok=True)` 로 디렉터리를 먼저 생성합니다. |
| **Large PDFs cause memory spikes** | PDF exporter keeps the whole image in RAM. | 페이지를 청크 단위로 처리하거나 스트리밍 PDF 라이터를 사용합니다. |

*Pro tip:* always test on a small sample image before scaling to a batch of thousands. It saves hours of debugging.

## Wrap‑Up

이제 **이미지에 OCR을 실행**하는 방법, **PNG에서 텍스트를 추출**하는 방법, **텍스트 이미지를 인식**해 후속 작업에 활용하는 방법, **검색 가능한 PDF를 생성**하는 방법, 그리고 **간단히 PNG를 PDF로 변환**하는 방법을 모두 알게 되었습니다. 제공된 스크립트는 바로 사용할 수 있는 완전한 복사‑붙여넣기 솔루션이며, 선택적 섹션을 통해 필요에 맞게 출력을 조정할 수 있습니다.

### What’s next?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
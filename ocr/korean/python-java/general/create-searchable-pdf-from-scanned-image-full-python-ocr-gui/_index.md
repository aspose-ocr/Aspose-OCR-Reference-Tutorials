---
category: general
date: 2026-07-05
description: Python으로 검색 가능한 PDF 만들기. 스캔한 PNG에 OCR을 적용하고, 스캔 이미지 PDF를 변환하여 몇 분 안에
  검색 가능한 PDF를 얻는 방법을 배워보세요.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: ko
og_description: 검색 가능한 PDF를 빠르게 만들기. 이 가이드는 PNG에 OCR을 적용하고, 스캔된 이미지 PDF를 변환하며, Python을
  사용해 검색 가능한 PDF를 생성하는 방법을 보여줍니다.
og_title: 스캔 이미지에서 검색 가능한 PDF 만들기 – 파이썬 OCR 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: 스캔 이미지에서 검색 가능한 PDF 만들기 – 전체 파이썬 OCR 가이드
url: /ko/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 스캔 이미지에서 검색 가능한 PDF 만들기 – 전체 Python OCR 가이드

고가의 소프트웨어를 구매하지 않고 **검색 가능한 PDF**를 스캔 사진에서 만들고 싶었던 적 있나요? 혼자가 아닙니다. 많은 사무실에서 PDF가 평평한 이미지 형태로 들어와 검색이 어렵고, 복사‑붙여넣기가 불가능하며, 컴플라이언스 감사에 악몽이 됩니다. 좋은 소식은? 몇 줄의 Python 코드만으로 정적인 PNG를 완전한 검색 가능한 PDF로 바꿀 수 있으며, 그 과정은 생각보다 간단합니다.

이 튜토리얼에서는 **OCR 인식 예제**를 전체적으로 살펴보며, 올바른 라이브러리 설치부터 최종 PDF 파일 작성까지 모든 과정을 다룹니다. 끝까지 따라오면 **스캔 이미지 PDF** 파일을 어떻게 **ocr pdf** 로 프로그래밍적으로 변환하는지 정확히 알게 되고, 어떤 프로젝트에도 바로 넣어 사용할 수 있는 재사용 가능한 스크립트를 얻게 됩니다.

## 배울 내용

- Python OCR 라이브러리 설치 및 설정 (`pytesseract`와 `pdf2image` 사용)
- OCR 엔진 초기화 및 언어 설정
- 스캔된 PNG(또는 기타 이미지) 로드 및 OCR 실행
- OCR 결과를 **검색 가능한 PDF**(바이트 배열) 로 변환하고 저장
- 다페이지 문서, 다양한 언어 처리, 흔히 발생하는 문제점에 대한 팁

OCR 경험이 없어도 괜찮습니다—Python 3 환경만 있으면 됩니다.

---

## 검색 가능한 PDF 만들기 – 개요

아래는 구현할 단계들의 고수준 흐름도입니다.  

![검색 가능한 PDF 워크플로우 다이어그램](https://example.com/flowchart.png "검색 가능한 PDF 워크플로우 다이어그램")

*Alt text: 검색 가능한 PDF 워크플로우 다이어그램은 엔진 초기화, 이미지 로드, OCR 인식, PDF 변환, 파일 쓰기 과정을 보여줍니다.*

---

## 1단계: OCR 엔진 초기화 (how to ocr pdf)

왜 엔진을 초기화해야 할까요? OCR 엔진은 픽셀 패턴을 문자로 해석하는 두뇌 역할을 합니다. 엔진 인스턴스를 만들고 언어를 명시적으로 설정하면 라이브러리에게 어떤 알파벳을 기대해야 하는지 알려 주어 정확도가 크게 향상됩니다.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro tip:** 여러 언어의 문서를 OCR해야 한다면 Tesseract용 언어 팩을 설치하고 `ocr_language`에 `"eng+spa"`와 같이 리스트 형태로 전달하세요.

---

## 2단계: 스캔 이미지 로드 (convert scanned image pdf)

다음 퍼즐 조각은 이미지 데이터를 Python으로 가져오는 것입니다. 단일 PNG든 다페이지 TIFF든 `PIL.Image` 클래스로 열 수 있습니다. 이미 스캔 이미지가 포함된 PDF에서 시작한다면 `pdf2image`가 각 페이지를 이미지로 변환해 줍니다.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**왜 중요한가:** 이미지를 Pillow 객체로 로드하면 원시 픽셀 데이터에 접근할 수 있게 되며, 이는 OCR 엔진이 필요로 하는 정보입니다. 이 단계를 건너뛰고 원시 바이트를 직접 전달하면 오류가 발생합니다.

---

## 3단계: 이미지에 OCR 인식 수행 (ocr recognition example)

이제 재미있는 부분—엔진이 텍스트를 읽게 합니다. `pytesseract.image_to_pdf_or_hocr`는 이미 보이지 않는 텍스트 레이어가 포함된 PDF 바이트 스트림을 반환하는데, 바로 **검색 가능한 PDF**에 필요한 형태입니다.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Edge case:** 이미지가 저대비인 경우 OCR 전에 간단한 임계값 적용을 고려하세요:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

이 작은 전처리 단계만으로도 정확도가 크게 향상됩니다.

---

## 4단계: PDF 바이트를 파일에 쓰기 (convert png searchable pdf)

OCR 라이브러리가 바이트 배열을 반환합니다—PDF 파일의 원시 내용이라고 생각하면 됩니다. 이제 해야 할 일은 그 바이트를 디스크에 저장하는 것뿐입니다.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**What you’ll see:** 결과 파일을 PDF 뷰어에서 열고 원본 이미지에 존재하는 단어를 검색해 보세요. 하이라이트가 바로 해당 위치로 이동하여 보이지 않는 텍스트 레이어가 정상 작동함을 확인할 수 있습니다.

---

## 5단계: 다페이지 문서로 확장하기 (convert scanned image pdf)

실제 계약서는 여러 페이지에 걸쳐 있는 경우가 많습니다. 여러 페이지를 **convert scanned image pdf** 파일에서 변환하려면 각 페이지를 순회하면서 OCR을 수행하고 결과 PDF를 연결하면 됩니다.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**왜 병합하나요?** `image_to_pdf_or_hocr` 호출마다 독립적인 PDF가 생성됩니다. 이를 병합하면 최종 문서가 원본 페이지 순서를 유지합니다.

---

## 흔히 겪는 문제와 해결 방법

| 증상 | 가능한 원인 | 해결 방법 |
|---------|--------------|-----|
| PDF를 열었을 때 검색 가능한 텍스트가 없음 | Tesseract가 문자 인식을 못 함(빈 출력) | 이미지 품질 확인, DPI 상승, 전처리 적용(대비, 이진화) |
| 깨진 문자(예: �) | 잘못된 언어 팩 또는 폰트 누락 | 올바른 언어 데이터(`tesseract‑lang‑eng`) 설치 및 `ocr_language` 일치 여부 확인 |
| PDF 파일 크기가 거대함(1페이지 이미지에 10 MB 이상) | 원본으로 손실 없는 PNG 사용; OCR이 고해상도 이미지 포함 | OCR 전에 이미지 축소(`image.thumbnail((1240, 1754))` 등 A4 기준) |
| Windows에서 “tesseract.exe not found” 오류 | Tesseract 실행 파일이 PATH에 없음 | `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` 로 경로 지정(환경에 맞게 조정) |

---

## 전체 실행 가능한 스크립트

전체 흐름을 하나의 파일에 모아 보았습니다. 복사‑붙여넣기 후 바로 실행할 수 있습니다:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

파일명을 `create_searchable_pdf.py` 로 저장하고, 플레이스홀더를 실제 경로로 바꾼 뒤 실행하세요:

```bash
python create_searchable_pdf.py
```

실행하면

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하여 관련 주제를 심도 있게 다룹니다. 각 자료에는 완전한 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
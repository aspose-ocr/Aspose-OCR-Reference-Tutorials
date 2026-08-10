---
category: general
date: 2026-06-19
description: Python OCR을 사용하여 이미지에서 검색 가능한 PDF를 만들기. OCR을 PDF로 변환하고, 이미지에서 텍스트를 추출하며,
  이미지를 빠르게 OCR하는 방법을 배워보세요.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: ko
og_description: Python OCR을 사용하여 이미지에서 검색 가능한 PDF 만들기. 이 가이드는 OCR을 PDF로 변환하고, 이미지에서
  텍스트를 추출하며, 이미지에 OCR을 수행하는 방법을 보여줍니다.
og_title: Python으로 검색 가능한 PDF 만들기 – 전체 프로그래밍 안내
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Python으로 검색 가능한 PDF 만들기 – 완전 단계별 가이드
url: /ko/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 파이썬으로 검색 가능한 PDF 만들기 – 완전 단계별 가이드

스캔한 영수증에서 **create searchable PDF**를 만들어야 할 때, 어디서 시작해야 할지 몰라 고민한 적 있나요? 당신만 그런 것이 아닙니다—많은 개발자들이 텍스트 사진을 실제로 검색 가능한 PDF로 바꾸려 할 때 같은 장벽에 부딪힙니다.  

이 튜토리얼에서는 **perform OCR on image**를 수행하고, OCR 결과를 **searchable PDF**로 변환하며, 필요하다면 원시 텍스트를 추출하는 실용적인 솔루션을 단계별로 안내합니다. 불필요한 내용 없이 바로 프로젝트에 복사‑붙여넣기 할 수 있는 작동 예제만 제공합니다.

## 배울 내용

- Python에서 가벼운 OCR 엔진을 설정하는 방법  
- **convert OCR to PDF**의 정확한 단계와 이를 검색 가능한 문서로 저장하는 방법  
- 후속 분석을 위한 **extract text from image** 방법  
- 이미지 방향 및 대용량 파일과 같은 일반적인 함정을 처리하기 위한 팁  
- 자신의 사용 사례에 맞게 조정할 수 있는 완전하고 실행 가능한 스크립트  

### 사전 요구 사항

- Python 3.8+가 설치된 환경  
- pip 및 가상 환경에 대한 기본적인 이해 (선택 사항이지만 권장)  
- 명확하고 기계가 읽을 수 있는 텍스트가 포함된 이미지 파일(PNG, JPEG 등)  

위 조건을 갖추셨다면, 시작해봅시다.

## 1단계: 필요한 라이브러리 설치

앞서 본 코드 스니펫은 가상의 `ocr` 패키지를 사용했지만, 동일한 아이디어는 **EasyOCR**, **pytesseract**, **pdfminer.six**와 같은 실제 라이브러리에도 적용됩니다. 이 가이드에서는 순수 Python이며 다국어를 지원하고 보조 헬퍼를 통해 편리한 PDF 변환 메서드를 제공하는 **EasyOCR**를 사용합니다.

```bash
pip install easyocr pillow
```

> **Pro tip:** 가상 환경(`python -m venv venv && source venv/bin/activate`) 안에 설치하여 의존성을 깔끔하게 관리하세요.

## 2단계: OCR 엔진 초기화 – Perform OCR on Image

라이브러리가 준비되었으니 OCR 엔진을 생성하고 영어 텍스트를 처리하도록 지정합니다. 여기서 처음으로 **perform OCR on image**를 수행합니다.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

왜 전용 리더 객체가 필요할까요? EasyOCR는 언어 모델을 미리 로드하므로, 여러 이미지에 대해 동일한 `reader`를 재사용하는 것이 매번 다시 초기화하는 것보다 훨씬 효율적입니다.

## 3단계: 이미지 로드 – Extract Text from Image

이미지를 메모리로 불러옵니다. 이 단계가 나중에 **extract text from image**를 수행하는 단계이지만, 우선 이미지를 로드합니다.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

이미지가 뒤집히거나 기울어져 있다면 OCR 엔진에 전달하기 전에 Pillow의 `rotate` 또는 `transpose` 메서드를 사용해 보세요. 간단한 시각적 확인만으로도 나중에 디버깅에 소요되는 시간을 크게 절약할 수 있습니다.

## 4단계: OCR 엔진 실행 및 결과 캡처

프로세스의 핵심—이미지를 OCR 엔진에 전달하고 구조화된 데이터를 반환받는 단계입니다.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

`detail=1` 플래그는 바운딩 박스를 제공하며, 이는 나중에 **convert OCR to PDF**할 때 필요합니다. 순수 문자열만 원한다면 `detail=0`으로 설정하세요.

## 5단계: OCR 결과를 검색 가능한 PDF로 변환 – Convert OCR to PDF

EasyOCR는 직접적인 PDF 작성기를 제공하지 않지만, Pillow와 `reportlab` 라이브러리를 사용해 PDF를 직접 만들 수 있습니다. 튜토리얼을 가볍게 유지하기 위해 원본 이미지를 삽입하고 보이지 않는 텍스트를 오버레이할 수 있는 `fpdf2`를 사용합니다.

```bash
pip install fpdf2
```
```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

무슨 일이 일어난 걸까요? 스캔한 이미지를 보이는 레이어로 배치하고, 인식된 단어들을 흰색 텍스트로 위에 써서 흰 배경과 섞이게 했습니다. 검색 도구는 여전히 숨겨진 레이어를 읽기 때문에, 시각적 모습은 그대로이면서 PDF가 **searchable**하게 됩니다.

## 6단계: PDF 바이트 저장 – Convert Image to PDF

PDF를 메모리에서 처리하고 싶다면(예: API로 전송) 디스크에 직접 쓰는 대신 바이트를 캡처할 수 있습니다.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

해당 코드는 고전적인 **convert image to PDF** 워크플로를 보여줍니다: 이미지로 시작해 OCR을 실행하고, 텍스트를 오버레이한 뒤 최종적으로 PDF 스트림을 출력합니다.

## 7단계: 결과 검증 – 빠른 확인

스크립트를 실행한 뒤, 任意의 PDF 뷰어에서 `receipt_searchable.pdf`를 열고 검색창(Ctrl + F)을 사용해 보세요. 영수증에 있는 단어를 입력했을 때 정확한 위치로 이동한다면 **create searchable pdf**에 성공한 것입니다!  

검색이 실패한다면, 다음을 다시 확인하세요:

1. OCR 신뢰도 점수(`conf` 값). 낮은 신뢰도는 이미지가 흐릿함을 의미할 수 있습니다.  
2. 바운딩 박스 좌표—때때로 EasyOCR가 다른 방향으로 보고할 수 있습니다.  
3. PDF 뷰어가 “이미지 전용” 모드로 설정되어 있지 않은지 확인하세요(드물지만 일부 뷰어에 해당 옵션이 있습니다).

## 전체 작동 스크립트

모든 과정을 종합한 완전하고 바로 실행 가능한 파이썬 파일은 다음과 같습니다:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

`searchable_pdf.py`로 저장하고, `YOUR_DIRECTORY` 자리표시자를 실제 경로로 교체한 뒤 실행하세요:

```bash
python searchable_pdf.py
```

확인 메시지가 표시되고 새로 만든 검색 가능한 PDF가 폴더에 생성될 것입니다.

## 흔히 묻는 질문 및 예외 상황

**이미지가 컬러인 경우는?**  
EasyOCR는 흑백 및 컬러 이미지 모두에서 작동하지만, 그레이스케일(`pil_image.convert("L")`)로 변환하면 잡음이 많은 스캔에서 정확도가 향상될 수 있습니다.

**다중 페이지 PDF를 처리할 수 있나요?**  
네—각 페이지 이미지를 순회하면서 OCR 단계를 수행하고, 각 페이지를 동일한 `FPDF` 객체에 추가하면 됩니다. 새 이미지마다 커서를 초기화(`self.add_page()`)하는 것을 잊지 마세요.

**보이지 않는 흰색 텍스트 대신 원본 텍스트 레이어를 유지할 수 있나요?**  
진정한 “텍스트‑이미지 아래” PDF(예: 접근성을 위해)가 필요하다면 `pdfminer` 또는 `pikepdf`를 사용해 적절한 PDF 태그와 함께 숨겨진 텍스트 레이어를 삽입하는 것을 고려하세요. 좀 더 고급 기술이지만 원리는 동일합니다: 배경 이미지 + 텍스트 오버레이.

**OCR 신뢰도가 낮은 경우는?**  
신뢰도가 낮은 단어를 필터링할 수 있습니다:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## 마무리 – 우리가 달성한 것

우리는 간단한 영수증 이미지를 시작점으로, **perform OCR on image**를 수행하고 인식된 문자열을 추출한 뒤, 최종적으로 **create searchable pdf**를 만들어 전문 스캔 문서와 동일하게 동작하도록 했습니다. 이 과정은 **convert OCR to PDF**, **extract text from image**, **convert image to PDF**, **perform OCR on image**와 같은 모든 보조 키워드를 다루었으므로, 이제 유사한 프로젝트에 재사용 가능한 도구 상자를 갖게 되었습니다.

### 다음 단계

- `easyocr.Reader(['en', 'es'])`와 같이 ISO 코드를 전달해 다른 언어를 실험해 보세요.  
- 완전 오프라인 솔루션이 필요하면 EasyOCR를 Tesseract로 교체하세요; 나머지 파이프라인은 동일합니다.  
- 문제 스캔을 디버깅하기 위해 OCR 신뢰도 시각화(이미지에 바운딩 박스 그리기)를 추가하세요.  

공유하고 싶은 팁이 있나요? 댓글을 남기거나 포크해 주세요

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 숙달하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
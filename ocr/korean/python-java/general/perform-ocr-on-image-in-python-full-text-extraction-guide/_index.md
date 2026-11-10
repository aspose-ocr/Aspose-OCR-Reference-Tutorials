---
category: general
date: 2026-06-19
description: Python의 OCR 라이브러리를 사용하여 이미지에서 OCR을 수행합니다. 이미지에서 텍스트를 감지하고, JPEG에서 텍스트를
  인식하며, 스캔한 이미지에서 텍스트를 효율적으로 추출하는 방법을 배웁니다.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: ko
og_description: Python으로 이미지에 OCR을 수행하고 스캔 파일에서 텍스트를 추출합니다. 이 가이드는 이미지를 로드하고, 기울기를
  보정하며, 텍스트를 단계별로 인식하는 과정을 안내합니다.
og_title: Python에서 이미지 OCR 수행 – 전체 텍스트 추출 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Python에서 이미지 OCR 수행 – 전체 텍스트 추출 가이드
url: /ko/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 OCR 수행 (Python) – 전체 텍스트 추출 가이드

이미지 파일에 **OCR을 수행**하려고 했지만 코드가 난해해서 막혔던 적 있나요? 당신만 그런 것이 아닙니다. 스캔한 영수증을 검색 가능한 PDF로 변환하거나 데이터‑사이언스 프로젝트를 위해 JPEG에서 캡션을 추출하든, JPEG 및 기타 포맷에서 텍스트를 인식하는 능력은 오늘날 모든 개발자에게 필수적인 스킬입니다.

이 튜토리얼에서는 **이미지 파일에서 텍스트를 감지**하고, **스캔한 이미지 문서에서 텍스트를 추출**하며, **OCR용 이미지 로드**까지 몇 줄의 코드만으로 보여주는 완전하고 실행 가능한 예제를 단계별로 살펴봅니다. 끝까지 따라오면, 누락된 import 없이 바로 프로젝트에 삽입할 수 있는 견고하고 프로덕션‑레디 스니펫을 얻게 됩니다.

## 만들게 될 것

- OCR 엔진을 생성하고 자동 디스큐를 활성화하며 JPEG(또는 지원되는 형식)를 로드하고 인식된 텍스트를 출력하는 작은 Python 스크립트
- **왜** 각 설정이 중요한지에 대한 설명과 **어떻게** 입력하는지에 대한 안내
- 다중 페이지 PDF, 비영어권 언어, 흐릿한 스캔과 같은 일반적인 함정에 대한 팁

### 사전 요구 사항

- Python 3.8+ 설치 (예제에서는 `pip install ocr-lib` 로 설치 가능한 `ocr` 패키지를 사용합니다 – 실제 라이브러리 이름으로 교체하세요)
- Python 함수와 가상 환경에 대한 기본 지식
- 처리하고자 하는 이미지 파일(JPEG, PNG, TIFF) – 여기서는 `skewed_page.jpg` 를 예시로 사용합니다

> **프로 팁:** Windows 환경이라면 OCR 라이브러리를 설치할 때 권한 문제를 피하기 위해 터미널을 관리자 권한으로 실행하세요.

---

## 이미지에서 OCR 수행 – 설정 및 구성

가장 먼저 필요한 것은 깨끗한 OCR 엔진 인스턴스입니다. 이는 작업의 두뇌와도 같으며, 올바른 구성이 없으면 가장 선명한 이미지조차도 의미 없는 결과를 반환합니다.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**왜 중요한가:**  
`engine.language` 를 설정하면 OCR 엔진이 기대하는 문자 집합을 제한하여 정확도가 크게 향상됩니다. 이를 생략하면 엔진이 추측하게 되어 간단한 단어조차 잘못 인식할 수 있습니다.

---

## 자동 디스큐 활성화 – 기울어진 스캔 보정

스캔한 페이지는 거의 완벽하게 평평하지 않습니다. 약간의 기울기만 있어도 문자 구분이 흐트러져 “Hello”가 “H3llo”처럼 변할 수 있습니다. `auto_deskew` 플래그가 이 작업을 대신해 줍니다.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**예외 상황:** 이미지가 이미 똑바로 정렬되어 있다는 것을 확신한다면 디스큐를 비활성화하여 처리 시간을 몇 밀리초 절감할 수 있습니다—수천 페이지를 배치 작업으로 처리할 때 유용합니다.

---

## OCR용 이미지 로드 – JPEG, PNG, TIFF 지원

이제 실제로 **OCR용 이미지 로드**를 수행합니다. `ocr.Image.load` 메서드는 유연하며, 지원되는 래스터 포맷이면 어떤 경로든 받아들입니다.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **왜 중요한 단계인가:** 라이브러리는 파일을 내부 비트맵으로 읽어들여 필요한 색 공간 변환을 수행합니다. 이 과정을 건너뛰고 원시 바이트 스트림을 전달하면 `FileNotFoundError`가 발생하거나, 더 나쁘게는 빈 결과가 조용히 반환될 수 있습니다.

특히 **JPEG 파일에서 텍스트를 인식**하려면 파일 확장자가 `.jpeg` 혹은 `.jpg` 인지 확인하면 됩니다. 동일한 호출이 PNG(`.png`)나 TIFF(`.tif`)에도 별도 수정 없이 동작합니다.

---

## 이미지에서 OCR 수행 – 엔진 실행

엔진이 준비되고 이미지가 메모리에 로드되었으니 **이미지에서 OCR 수행**을 할 차례입니다. 아래 한 줄이 전 과정을 담당합니다: 전처리, 세그멘테이션, 분류, 텍스트 조합.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**내부에서 무슨 일이 일어나나요?**  
- 엔진이 디스큐 변환을 적용합니다(활성화된 경우).  
- 신경망 또는 Tesseract 백엔드를 사용해 문자를 식별합니다.  
- 마지막으로 문자를 단어와 줄로 연결해 풍부한 `result` 객체를 반환합니다.

---

## 스캔 이미지에서 텍스트 추출 – 결과 출력

마지막 단계는 **스캔 이미지에서 텍스트 추출**하고 이를 표시하는 것입니다. `result.text` 속성에 순수 텍스트가 들어 있습니다.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

전형적인 출력 예시:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

OCR 엔진이 어떤 문자도 찾지 못하면 `result.text` 는 빈 문자열이 됩니다. 이 경우 이미지 품질을 재검토하거나 `engine.confidence_threshold` 속성을 조정해 보세요(라이브러리에서 지원한다면).

---

## 일반적인 변형 처리

### JPEG vs PNG 텍스트 인식

두 포맷 모두 지원되지만 JPEG 압축은 엔진을 혼란스럽게 하는 아티팩트를 만들 수 있습니다. 오인식이 빈번하다면 JPEG를 먼저 PNG로 변환해 보세요:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### 다중 언어 이미지 텍스트 감지

문서에 영어와 스페인어가 섞여 있다면 다국어 모드를 설정합니다:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

엔진은 이제 두 알파벳을 모두 고려해 인식합니다.

### 스캔 PDF에서 텍스트 추출

PDF의 경우 각 페이지를 먼저 이미지로 래스터화해야 합니다. `pdf2image` 같은 라이브러리를 사용하면 손쉽게 처리할 수 있습니다:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## 전체 작업 예제

아래는 `ocr_demo.py` 파일에 복사‑붙여넣기 할 수 있는 완전한 스크립트입니다. 오류 처리와 실행 시간을 측정하는 작은 헬퍼 함수도 포함되어 있습니다.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**예상 출력**(깨끗한 스캔을 가정):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## 자주 묻는 질문

**Q: 헤드리스 서버에서도 실행할 수 있나요?**  
A: 물론 가능합니다. 라이브러리는 GUI 없이 동작하므로 서버에 필요한 네이티브 바이너리(예: Tesseract)만 설치하면 됩니다.

**Q: 이미지가 흐릿하면 어떻게 해야 하나요?**  
A: `engine.recognize` 전에 샤프닝 필터를 적용해 보세요. 많은 OCR 라이브러리는 `image_preprocessing.sharpen = True` 옵션을 제공하거나 OpenCV의 `cv2.GaussianBlur` 를 역으로 사용해 샤프닝을 구현할 수 있습니다.

**Q: 스크립트가 배치 처리도 지원하나요?**  
A: 예. 파일 경로 리스트에 대해 `perform_ocr` 를 루프 안에서 호출하면 됩니다.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
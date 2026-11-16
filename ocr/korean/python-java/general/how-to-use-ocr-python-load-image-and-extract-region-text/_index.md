---
category: general
date: 2026-06-25
description: Python에서 OCR을 사용하는 방법 – OCR용 이미지 로드, 영역 내 텍스트 인식, 그리고 영역 텍스트를 빠르게 추출하는
  방법을 배워보세요.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: ko
og_description: Python에서 OCR을 사용하는 방법 – 이미지를 로드하고, 특정 영역의 텍스트를 인식하며, 청구서 번호를 추출하는
  단계별 가이드.
og_title: 'OCR 파이썬 사용 방법: 이미지 로드 및 영역 텍스트 추출'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'OCR 파이썬 사용 방법: 이미지 로드 및 영역 텍스트 추출'
url: /ko/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Python 사용 방법: 이미지 로드 및 영역 텍스트 추출

**Python에서 OCR을 사용하는 방법**은 생각보다 간단합니다. 스캔한 청구서를 보고 전체 페이지를 파싱하지 않고 청구서 번호만 추출하고 싶었던 적이 있나요? 처음 OCR을 접하는 개발자라면 흔히 겪는 문제입니다. 이 가이드에서는 OCR을 위해 이미지를 로드하고, 사각형을 정의한 뒤, 해당 영역의 텍스트를 인식하고 최종적으로 영역 텍스트를 추출하는 과정을 단계별로 살펴봅니다. 끝까지 따라오면 필요한 텍스트 조각을 바로 추출할 수 있는 실행 가능한 스크립트를 얻게 됩니다.

> *Pro tip:* PDF를 다룰 경우, 각 페이지를 먼저 이미지로 변환하세요—대부분의 OCR 라이브러리는 PNG/JPEG 포맷을 가장 잘 처리합니다.

## 준비물

- Python 3.8+ (가능하면 최신 안정 버전)  
- `OcrEngine` 클래스를 제공하는 OCR 라이브러리 (예: `pip install ocr-lib` 로 설치하는 **ocr**)  
- 샘플 이미지 — 여기서는 사용자가 제어하는 폴더에 위치한 `invoice.png` 를 사용합니다  
- 사각형 (x, y, width, height) 개념에 대한 기본 이해  

무거운 의존성도 없고 GPU도 필요 없습니다—순수 CPU만으로 동작하므로 휴대성이 뛰어납니다.

---

## OCR 사용 방법: 엔진 초기화 (Step 1)

텍스트를 읽기 전에 OCR 엔진 인스턴스를 생성해야 합니다. 이는 픽셀 패턴을 분석할 “두뇌”와 같습니다.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*왜 중요한가:* 엔진을 초기화하면 언어 모델이 로드되고 기본 설정이 적용됩니다. 이 단계를 건너뛰면 `recognize_region` 호출 시 예외가 발생합니다.

---

## OCR용 이미지 로드 (Step 2)

엔진이 준비되었으니 이제 이미지를 전달합니다. 라이브러리의 `Image.load` 메서드는 일반적인 포맷을 처리하고 비트맵을 정규화합니다.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

파일을 찾을 수 없으면 Python이 `FileNotFoundError` 를 발생시킵니다. 경로가 절대 경로나 스크립트 작업 디렉터리에 상대적인지 확인하세요.  

*예외 상황:* 일부 OCR 엔진은 그레이스케일 이미지를 기대합니다. 정확도가 낮다면 먼저 이미지를 변환해 보세요:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## 영역 내 텍스트 인식 (Step 3)

영역을 정의하면 엔진에게 **어디**를 살펴볼지 알려주는 것입니다. `Rectangle` 은 부동소수점 값을 받아 서브픽셀 정밀도를 제공하므로 고해상도 스캔에 유용합니다.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – 사각형의 좌상단 코너 (픽셀 단위)  
- **width, height** – 박스의 크기  

이 숫자를 어떻게 찾을까요? 이미지 편집기(GIMP, Paint.NET 등)에서 선택 도구를 사용해 좌표를 확인하면 됩니다.  

*왜 전체 페이지를 OCR하지 않을까?* 영역을 제한하면 잡음이 줄어들고 처리 속도가 빨라지며, 청구서 번호와 같은 작은 필드의 정확도가 크게 향상됩니다.

---

## 영역 텍스트 추출 (Step 4)

영역을 설정했으면 엔진에 해당 슬라이스만 인식하도록 요청합니다. 결과 객체에는 원시 텍스트와 신뢰도 점수가 들어 있습니다.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

OCR 엔진이 다국어를 지원한다면 선택적으로 언어 코드를 전달할 수 있습니다:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*흔한 실수:* 일부 엔진은 단일 문자열 대신 단어 리스트를 반환합니다. 이 경우 리스트를 연결해 주세요:

```python
text = " ".join(region_result.words)
```

---

## 추출된 청구서 번호 출력 (Step 5)

마지막으로 추출한 텍스트를 출력하거나 저장합니다. 필요에 따라 문자열에서 불필요한 공백이나 비숫자 문자를 제거하는 후처리도 가능합니다.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

올바르게 정렬된 사각형으로 스크립트를 실행하면 다음과 같은 결과가 나옵니다:

```
Invoice number: 20231578
```

깨진 문자(garbage)가 보이면 사각형 좌표를 다시 확인하거나 이미지 해상도를 높여 보세요.

---

## 전체 작업 예제

모든 단계를 하나로 합친 자체 포함 스크립트는 다음과 같습니다. 복사‑붙여넣기 후 바로 실행할 수 있습니다:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

파일명을 `extract_invoice.py` 로 저장하고, `YOUR_DIRECTORY` 를 실제 폴더 경로로 바꾼 뒤 실행하세요:

```bash
python extract_invoice.py
```

콘솔에 청구서 번호가 출력될 것입니다.

---

## 자주 묻는 질문

**Q: 청구서 번호가 화려한 폰트로 인쇄돼 있으면 어떻게 하나요?**  
A: 최신 OCR 엔진은 다양한 폰트를 지원하지만, 정확도를 높이고 싶다면 커스텀 언어 모델을 학습하거나 이미지 전처리(예: 임계값 필터 적용)를 시도해 보세요.

**Q: 한 번에 여러 필드를 추출할 수 있나요?**  
A: 가능합니다. `Rectangle` 객체 리스트를 정의하고, 각각을 순회하면서 결과를 딕셔너리에 저장하면 됩니다.

**Q: 다중 페이지 PDF에서도 동작하나요?**  
A: 각 페이지를 먼저 이미지로 변환(`pdf2image` 등 사용)한 뒤, 동일한 영역 기반 추출을 페이지별로 적용하면 됩니다.

---

## 마무리

이 튜토리얼에서는 **Python에서 OCR을 사용하는 방법**을 다루었습니다. 이미지를 로드하고, 특정 영역의 텍스트를 인식하며, 해당 영역 텍스트를 추출하는 전체 흐름을 살펴보았습니다. 관심 영역을 분리하면 속도와 정확도가 향상되고 후처리 작업이 줄어듭니다.

다음 단계에 도전해 보세요. 배치 청구서 폴더에서 **OCR용 이미지 로드**를 자동화하거나, **영역 내 텍스트 인식**을 날짜, 합계 등 다른 필드에 적용해 보세요. 패턴은 동일합니다—사각형 좌표만 바꾸면 됩니다.

궁금한 점이나 개선 아이디어가 있으면 아래 댓글에 남겨 주세요. 즐거운 코딩 되시고, OCR 파이프라인이 언제나 정확하길 바랍니다!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하고, 추가 API 기능을 마스터하며, 다양한 구현 방법을 탐구할 수 있도록 구성되었습니다. 각 자료에는 완전한 코드 예제와 단계별 설명이 포함되어 있습니다.

- [이미지에서 텍스트 추출하기 – Aspose OCR 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR에서 사각형을 준비하여 이미지에서 텍스트 추출하기](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [AspOCR 사용법: .NET용 이미지 전처리 OCR 필터](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
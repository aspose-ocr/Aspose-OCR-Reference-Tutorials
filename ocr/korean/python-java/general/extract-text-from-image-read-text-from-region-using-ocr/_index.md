---
category: general
date: 2026-07-05
description: Python OCR을 사용하여 이미지에서 텍스트를 추출합니다. OCR을 위한 이미지 로드 방법, 영역별 텍스트 읽기, 그리고
  몇 줄의 코드만으로 청구서에서 텍스트를 추출하는 방법을 배워보세요.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: ko
og_description: Python OCR로 이미지에서 텍스트를 추출합니다. 이 가이드는 OCR을 위해 이미지를 로드하고, 영역에서 텍스트를
  읽으며, 청구서에서 텍스트를 빠르게 추출하는 방법을 보여줍니다.
og_title: 이미지에서 텍스트 추출 – OCR을 사용하여 영역의 텍스트 읽기
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 이미지에서 텍스트 추출 – OCR을 사용해 영역의 텍스트 읽기
url: /ko/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 추출 – OCR을 사용한 영역별 텍스트 읽기

이미지에서 **extract text from image**가 필요했지만, 특정 부분만 중요한 경우가 있나요—예를 들어 청구서의 총액처럼요. 여러분만 그런 것이 아닙니다. 실제 프로젝트에서는 전체 사진을 파싱하기보다 **read text from region**를 해야 할 때가 많습니다. 다행히 파이썬 몇 줄만으로 OCR용 이미지를 로드하고, 관심 영역(ROI)을 정의하여 필요한 문자만 정확히 추출할 수 있습니다.

이 튜토리얼에서는 **load image for OCR**, ROI 설정, 그리고 최종적으로 **extract text from invoice**하는 방법을 보여주는 완전하고 실행 가능한 예제를 단계별로 살펴보겠습니다. 끝까지 따라오시면 영역 기반 인식을 지원하는 모든 주요 OCR 라이브러리와 함께 사용할 수 있는 바로 적용 가능한 코드를 얻게 됩니다.

---

## 필요 사항

- Python 3.8+ (코드는 3.10에서도 작동합니다)  
- `OcrEngine` 클래스를 제공하는 OCR 패키지 (데모에서는 가상의 `ocr` 모듈을 사용합니다; `pytesseract`, `easyocr` 또는 ROI를 지원하는 다른 라이브러리로 교체하세요)  
- 명확한 인쇄 텍스트가 포함된 샘플 이미지—예: `invoice.png`  
- 파이썬 함수와 클래스에 대한 기본적인 이해 (딥러닝 배경은 필요 없음)

이미 준비되어 있다면 좋습니다—그럼 바로 시작해봅시다. 아직이라면 python.org에서 최신 파이썬을 다운로드하고 `pip install your-ocr-lib` 명령으로 OCR 패키지를 설치하세요.

---

![이미지에서 텍스트 추출 예시](extract-text-from-image.png "이미지에서 텍스트 추출 – 영역 기반 OCR 데모")

*위 그림은 **extract text from image**를 목표로 할 영역(빨간 사각형)을 보여줍니다.*

---

## 단계 1: OCR 라이브러리 설치 및 임포트

먼저, 환경에 OCR 라이브러리가 설치되어 있는지 확인하세요. 아래의 임포트 패턴은 `OcrEngine` 클래스를 제공하는 대부분의 패키지에서 동작합니다.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **팁:** `pytesseract`를 사용하는 경우, Tesseract 바이너리를 별도로 설치하고 `pytesseract.pytesseract.tesseract_cmd`에 해당 경로를 설정해야 합니다.

---

## 단계 2: OCR 엔진 생성 및 언어 설정

엔진 생성은 간단하지만, 언어를 지정하면 정확도가 크게 향상됩니다. 특히 숫자와 영문 단어가 포함된 청구서의 경우에 그렇습니다.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

왜 이렇게 할까요? OCR 엔진은 언어 모델을 사용해 문자를 예측합니다; 영어를 기대하도록 지정하면 “0”을 “O”로 오인식하는 등 잘못된 인식을 줄일 수 있습니다.

---

## 단계 3: OCR용 이미지 로드

이제 실제로 **load image for OCR**합니다. 대부분의 라이브러리는 파일 경로나 Pillow 이미지 객체를 받아들입니다. 여기서는 간단히 라이브러리의 내장 로더를 사용합니다.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

경로가 올바른 디렉터리를 가리키는지 확인하세요; 스크립트가 다른 작업 디렉터리에서 실행될 때 상대 경로를 잊어버리는 경우가 흔한 실수입니다.

---

## 단계 4: 관심 영역(ROI) 정의

ROI 정의는 **read text from region**의 핵심 단계입니다. 청구서에서 총액이 적힌 부분을 둘러싸는 사각형을 그린다고 생각하면 됩니다.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left`와 `top`은 사각형 왼쪽 위 모서리의 X와 Y 좌표를 나타냅니다.  
- `width`와 `height`는 박스의 크기를 설정합니다.  
- 픽셀 좌표를 표시해 주는 이미지 뷰어를 사용해 다양한 값을 실험해 볼 수 있습니다.

> **ROI가 중요한 이유:** 전체 페이지에 OCR을 적용하면 CPU 자원을 낭비하고, 관련 없는 텍스트, 표, 그래픽 등으로 인한 노이즈가 발생합니다. 특정 영역에 집중하면 더 깨끗한 결과와 빠른 처리를 얻을 수 있습니다.

---

## 단계 5: 지정된 영역에서 OCR 수행

모든 설정이 완료되었으니 이제 **extract text from image**를 수행합니다—하지만 정의한 ROI 내부에서만 수행합니다.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

`recognize` 메서드는 일반적으로 원시 문자열, 신뢰도 점수, 경우에 따라 각 단어의 경계 상자를 포함하는 객체를 반환합니다. 여기서는 순수 텍스트만 필요합니다.

---

## 단계 6: 추출된 텍스트 출력

결과를 출력해 보고 어떤 내용이 나오는지 확인해 봅시다. 이 단계는 실제 시나리오에서 **extract text from invoice**를 보여줍니다.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### 예상 출력

```
Text inside ROI:
Total Amount: $1,245.67
```

청구서 레이아웃이 다르면 사각형 안에 있는 텍스트가 출력됩니다—예를 들어 청구서 번호, 날짜, 혹은 PO 참조일 수 있습니다.

---

## 단계 7: 재사용 가능한 함수로 래핑 (선택 사항)

여러 청구서에 재사용할 수 있도록 로직을 함수로 캡슐화합니다. 이는 **ocr on region**을 일반 유틸리티로 보여주는 예시이기도 합니다.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

이제 어떤 청구서든 이 함수를 호출할 수 있습니다:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## 흔히 발생하는 문제와 해결 방법

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **빈 출력** | ROI가 실제 텍스트를 포함하지 않음(좌표 오류). | 이미지 편집기로 픽셀 값을 다시 확인하고, 시각적 디버그 오버레이를 추가하세요. |
| **깨진 문자** | 이미지 해상도가 낮거나 대비가 부족함. | 이미지를 전처리하세요: 그레이스케일 변환 후 임계값 적용(`cv2.threshold`). |
| **잘못된 언어** | 엔진이 필요한 문자 집합이 없는 언어를 기본값으로 사용함. | `ocr_engine.language`를 `ENGLISH` 또는 적절한 로케일로 명시적으로 설정하세요. |
| **성능 지연** | 큰 이미지를 반복적으로 OCR에 사용함. | 로드하기 전에 이미지를 리사이즈하거나, 먼저 ROI를 잘라서 처리하세요. |

---

## 예제 확장: 다중 ROI

청구서에 총액과 청구일 등 여러 필드가 필요할 때가 있습니다—예를 들어 **extract text from invoice**를 두 영역에 적용할 수 있습니다. 사각형 리스트를 순회하면 됩니다:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

이 패턴은 코드를 깔끔하게 유지하고 나중에 더 많은 영역을 추가하기 쉽게 해줍니다.

---

## 결론

우리는 이제 파이썬 OCR을 사용해 **extract text from image**하는 전체 워크플로우를 다루었습니다. **load image for OCR**, **관심 영역 정의**, 엔진 호출을 통해 특정 영역에서 안정적으로 **read text from region**를 할 수 있습니다—청구서의 총액, 영수증의 날짜 등 지역화된 데이터를 추출하는 데 이상적입니다.  
자유롭게 실험해 보세요

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 숙달하고 프로젝트에 적용할 수 있는 다양한 구현 방식을 탐색하도록 돕습니다.

- [Aspose OCR을 사용한 이미지 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [이미지 텍스트 추출 – Aspose.OCR for .NET을 활용한 OCR 최적화](/ocr/english/net/ocr-optimization/)
- [OCR에서 사각형을 준비하여 이미지 텍스트 추출하는 방법](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
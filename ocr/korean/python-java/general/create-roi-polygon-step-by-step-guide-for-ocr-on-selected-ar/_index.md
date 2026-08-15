---
category: general
date: 2026-03-26
description: 선택된 영역에서 OCR을 실행하기 위해 ROI 다각형을 생성합니다. 여러 영역을 정의하고 등록하며, Python OCR 엔진으로
  텍스트를 추출하는 방법을 배웁니다.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: ko
og_description: Python 엔진을 사용하여 ROI 폴리곤을 만들고 선택한 영역에서 OCR을 실행합니다. 전체 코드, 설명 및 팁이 포함되어
  있습니다.
og_title: ROI 폴리곤 만들기 – 선택 영역에 대한 빠른 OCR
tags:
- OCR
- Python
- Image Processing
title: ROI 폴리곤 만들기 – 선택 영역에 대한 OCR 단계별 가이드
url: /ko/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ROI 폴리곤 만들기 – 선택 영역에 대한 OCR 전체 튜토리얼

이미지에서 중요한 부분만 OCR을 실행하려면 **ROI 폴리곤 만들기**가 필요했던 적이 있나요? 영수증을 스캔하면서 총액만 필요하거나, 서명 필드만 읽어야 하는 양식이 있을 수 있습니다. 이런 경우 **선택 영역에 대한 OCR**은 시간을 절약하고 정확성을 높여줍니다.  

이 가이드에서는 두 개의 폴리곤 정의, OCR 엔진에 등록, 인식된 텍스트를 한 번에 추출하는 전체 과정을 단계별로 살펴봅니다. 끝까지 따라오시면 바로 실행 가능한 스크립트와 관심 영역에 집중해야 하는 이유를 명확히 이해하게 됩니다.

## What You’ll Learn

- 일반적인 OCR 라이브러리를 사용해 **ROI 폴리곤** 객체를 만드는 방법
- 단일 영역과 다중 영역을 정의하는 차이점
- `ocr on selected area`가 수행되도록 엔진에 영역을 등록하는 방법
- 예상 출력 및 일반적인 문제점(예: 겹치는 ROI, 빈 결과) 해결 방법

### Prerequisites

- Python 3.8+ 설치
- `Polygon`, `Point`, `add_region_of_interest` 메서드를 제공하는 OCR 라이브러리(예시에서는 가상의 `ocr` 모듈을 사용합니다; 실제 SDK, 예: Tesseract‑Python 래퍼 또는 EasyOCR 로 교체)
- 좌표가 표시된 샘플 이미지 파일(`sample.png`)  

> **Pro tip:** 실제 라이브러리를 사용할 경우 이미지가 동일한 좌표계(좌측 상단이 원점, X는 오른쪽으로 증가, Y는 아래로 증가)로 로드되었는지 확인하세요.  

---  

## Step 1: Import the OCR Module and Load Your Image  

먼저 OCR 패키지를 가져오고 처리할 이미지를 읽어옵니다.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Why this matters:* 엔진은 **ROI 폴리곤**을 연결하기 전에 이미지 데이터를 필요로 합니다. 일부 라이브러리는 나중에 이미지를 전달할 수도 있지만, 초기에 로드해 두면 워크플로가 깔끔해집니다.

## Step 2: Define the First ROI Polygon  

첫 번째 관심 영역을 만듭니다. 테이블 헤더를 둘러싼 사각형을 그린다고 생각하면 됩니다.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Explanation:*  
- `ocr.Point(x, y)`는 픽셀 좌표를 사용합니다.  
- 점 리스트는 시계 방향으로 정렬되어야 하며, 대부분의 엔진이 이 방식을 기대합니다.  
- 불규칙한 형태를 만들고 싶다면 원하는 만큼 점을 추가하면 됩니다; 사각형은 그 중 하나에 불과합니다.

## Step 3: Define Additional ROI Polygons (Optional)  

하나만 만들 필요는 없습니다. 아래는 페이지 하단에 있는 서명 필드를 포착하는 두 번째 폴리곤 예시입니다.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Why add more?* 여러 영역에 대해 **ocr on selected area**를 실행하면 각각을 잘라내어 별도로 처리하는 것보다 한 번에 다양한 데이터를 추출할 수 있어 훨씬 빠릅니다.

## Step 4: Register the ROIs with the OCR Engine  

폴리곤이 준비되었으면 엔진에 어떤 영역을 검사할지 알려줍니다.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Important note:* 엔진을 다른 이미지에 재사용할 경우 새 영역을 추가하기 전에 `clear_regions()` 메서드를 호출해야 하는 SDK도 있습니다.

## Step 5: Run OCR and Retrieve the Text  

마지막으로 인식을 실행합니다. 엔진은 방금 추가한 폴리곤 내부만 살펴봅니다.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Expected output** (예시: `sample.png`에 첫 번째 ROI에 “Invoice Total: $123.45”, 두 번째 ROI에 “Signature: John Doe” 텍스트가 포함된 경우):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

출력이 비어 있다면 좌표가 실제 텍스트와 교차하는지, 이미지 해상도가 좌표계와 일치하는지 다시 확인하세요.

## Edge Cases & Common Pitfalls  

| Situation                               | What to Watch For                               | Fix / Work‑around                              |
|----------------------------------------|--------------------------------------------------|-----------------------------------------------|
| **Overlapping ROIs**                    | 텍스트가 두 번 반환될 수 있음                     | 폴리곤을 겹치지 않게 만들거나 출력 중복 제거 |
| **ROI outside image bounds**           | 엔진이 오류를 발생시키거나 아무 것도 반환하지 않음 | 좌표를 `0 ≤ x < width`, `0 ≤ y < height` 범위 내로 제한 |
| **Very small ROI**                     | 픽셀 수가 부족해 OCR 정확도가 떨어짐               | 폴리곤을 몇 픽셀씩 확대하거나 먼저 이미지를 업스케일 |
| **Non‑rectangular shape**               | 일부 엔진은 볼록 다각형만 지원                     | 복잡한 형태를 여러 개의 볼록 ROI로 분할 |
| **Changing image size**                | 하드코딩된 좌표가 무효화됨                         | 이미지 크기에 비례해 좌표를 계산(예: 백분율) |

## Full Working Example  

아래는 복사‑붙여넣기만 하면 바로 실행 가능한 전체 스크립트입니다(`ocr`를 실제 라이브러리로 교체).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

`python ocr_roi_example.py` 로 실행하면 정의한 두 영역에서 추출된 문자열을 확인할 수 있습니다.

## Next Steps  

- **Dynamic ROI generation:** 좌표를 하드코딩하는 대신 OpenCV 컨투어 검출 등 이미지 처리 기법을 사용해 테이블이나 필드를 자동으로 찾기  
- **Post‑processing:** 공백 제거, 정규식 적용, 숫자를 적절한 데이터 타입으로 변환  
- **Batch processing:** 레이아웃이 일관된 이미지 폴더를 순회하면서 동일한 ROI 정의 재사용  

더 복잡한 문서(예: 다페이지 PDF 또는 스캔된 양식)에서 **ocr on selected area**를 활용하고 싶다면 페이지별 ROI 등록을 지원하는 라이브러리를 살펴보세요.  

---  

### Visual Overview  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="두 개의 ROI 폴리곤이 샘플 이미지에 표시된 예시"}

다이어그램은 두 개의 사각형(파란색 및 초록색)이 기본 이미지에 어떻게 매핑되는지 보여주며, OCR 엔진이 읽게 될 영역을 정확히 나타냅니다.

---  

## Conclusion  

우리는 **ROI 폴리곤** 객체를 만들고, OCR 엔진에 등록한 뒤, `ocr on selected area`를 깔끔하고 재현 가능한 스크립트로 수행했습니다. 관심 영역만 제한함으로써 처리 시간을 단축하고 정확성을 높이며, 이후 데이터 처리도 훨씬 간단해집니다.  

자신만의 이미지로 직접 시도해 보세요—좌표를 조정하고, 폴리곤을 추가하고, 출력 결과를 데이터베이스에 연결해도 좋습니다. 영역 기반 OCR을 마스터하면 가능성은 무한합니다.  

질문이 있거나 멋진 활용 사례를 공유하고 싶다면 아래 댓글에 남겨 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
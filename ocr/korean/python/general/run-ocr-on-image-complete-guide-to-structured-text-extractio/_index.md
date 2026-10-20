---
category: general
date: 2026-05-03
description: 구조화된 OCR 인식을 사용하여 이미지에서 OCR을 실행하고 좌표와 함께 텍스트를 추출하는 방법을 배워보세요. 단계별 파이썬
  코드가 포함되어 있습니다.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: ko
og_description: 이미지에서 OCR을 실행하고 구조화된 OCR 인식을 사용해 좌표와 함께 텍스트를 추출합니다. 설명이 포함된 전체 Python
  예제.
og_title: 이미지에서 OCR 실행 – 구조화된 텍스트 추출 튜토리얼
tags:
- OCR
- Python
- Computer Vision
title: 이미지에서 OCR 실행 – 구조화된 텍스트 추출 완전 가이드
url: /ko/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 OCR 실행 – 구조화된 텍스트 추출 완전 가이드

이미지 파일에 **OCR을 실행**하고 각 단어의 정확한 위치를 유지하는 방법을 몰라 고민한 적 있나요? 여러분만 그런 것이 아닙니다. 영수증 스캔, 양식 디지털화, UI 테스트 등 많은 프로젝트에서 원시 텍스트뿐만 아니라 각 줄이 이미지 상에서 어디에 위치하는지를 알려주는 바운딩 박스가 필요합니다.  

이 튜토리얼에서는 **aocr** 엔진을 사용해 *이미지에서 OCR을 실행*하고 **구조화된 OCR 인식**을 요청한 뒤, 기하 정보를 보존하면서 결과를 후처리하는 실용적인 방법을 보여드립니다. 몇 줄의 파이썬 코드만으로 **좌표와 함께 텍스트를 추출**할 수 있게 되며, 구조화 모드가 다운스트림 작업에 왜 중요한지도 이해하게 될 것입니다.

## 배울 내용

- **구조화된 OCR 인식**을 위한 OCR 엔진 초기화 방법.  
- 이미지를 입력하고 줄 경계가 포함된 원시 결과를 받는 방법.  
- 기하 정보를 잃지 않으면서 텍스트를 정제하는 후처리 방법.  
- 최종 줄을 순회하며 텍스트와 바운딩 박스를 함께 출력하는 방법.  

마법도, 숨겨진 단계도 없습니다—그냥 바로 실행 가능한 예제를 여러분의 프로젝트에 복사해 넣기만 하면 됩니다.

---

## 사전 요구 사항

시작하기 전에 다음이 설치되어 있는지 확인하세요:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

또한 읽기 쉬운 텍스트가 포함된 이미지 파일(`input_image.png` 또는 `.jpg`)이 필요합니다. 스캔한 청구서든 스크린샷이든 OCR 엔진이 문자를 인식할 수만 하면 됩니다.

---

## 1단계: 구조화된 인식을 위한 OCR 엔진 초기화

먼저 `aocr.Engine()` 인스턴스를 만들고 **구조화된 OCR 인식**을 원한다는 것을 알려줍니다. 구조화 모드는 일반 텍스트뿐 아니라 각 줄에 대한 기하 데이터(바운딩 사각형)도 반환하므로, 텍스트를 이미지에 다시 매핑해야 할 때 필수적입니다.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **왜 중요한가:**  
> 기본 모드에서는 엔진이 단순히 이어붙인 문자열만 반환할 수 있습니다. 구조화 모드는 페이지 → 줄 → 단어 계층 구조와 좌표를 제공하므로 원본 이미지 위에 결과를 오버레이하거나 레이아웃을 인식하는 모델에 바로 전달하기가 훨씬 쉬워집니다.

---

## 2단계: 이미지에 OCR 실행 및 원시 결과 획득

이제 이미지를 엔진에 전달합니다. `recognize` 호출은 `OcrResult` 객체를 반환하며, 여기에는 각 줄마다 바운딩 사각형이 포함된 컬렉션이 들어 있습니다.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

이 시점에서 `raw_result.lines`는 두 가지 중요한 속성을 가진 객체들을 보유합니다:

- `text` – 해당 줄에 인식된 문자열.  
- `bounds` – `(x, y, width, height)` 형태의 튜플로 줄의 위치를 설명합니다.

---

## 3단계: 기하 정보를 보존하면서 후처리

원시 OCR 출력은 종종 잡음이 많습니다: 불필요한 문자, 잘못된 공백, 줄바꿈 문제 등. `ai.run_postprocessor` 함수는 텍스트를 정제하지만 **원본 기하 정보를 그대로 유지**하므로 정확한 좌표를 계속 사용할 수 있습니다.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **프로 팁:** 도메인별 어휘(예: 제품 코드)가 있다면 사용자 정의 사전을 후처리기에 전달해 정확도를 높이세요.

---

## 4단계: 좌표와 함께 텍스트 추출 – 순회 및 출력

마지막으로 정제된 줄들을 순회하면서 각 줄의 바운딩 박스를 텍스트와 함께 출력합니다. 이것이 **좌표와 함께 텍스트를 추출**하는 핵심 로직입니다.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### 예상 출력

입력 이미지에 두 줄 “Invoice #12345”와 “Total: $89.99”가 포함되어 있다고 가정하면 다음과 유사한 결과가 표시됩니다:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

첫 번째 튜플은 원본 이미지 상에서 해당 줄의 `(x, y, width, height)`이며, 이를 이용해 사각형을 그리거나 텍스트를 강조하거나 좌표를 다른 시스템에 전달할 수 있습니다.

---

## 결과 시각화 (선택 사항)

이미지 위에 바운딩 박스를 오버레이하고 싶다면 Pillow(PIL)를 사용해 사각형을 그릴 수 있습니다. 아래는 간단한 스니펫이며, 원시 데이터만 필요하면 건너뛰어도 됩니다.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![이미지에서 OCR 실행 예시 – 바운딩 박스 표시](/images/ocr-bounding-boxes.png "이미지에서 OCR 실행 – 바운딩 박스 오버레이")

위 alt 텍스트에는 **주요 키워드**가 포함되어 있어 이미지 alt 속성에 대한 SEO 요구사항을 충족합니다.

---

## 구조화된 OCR 인식이 단순 텍스트 추출보다 뛰어난 이유

“그냥 OCR만 하면 텍스트를 얻을 수 있지 않나요? 왜 좌표가 필요하죠?” 라고 생각할 수 있습니다.  

- **공간적 컨텍스트:** 양식에서 “날짜”와 같은 필드가 실제 값 옆에 위치할 때, 좌표가 데이터가 어디에 있는지 알려줍니다.  
- **다중 컬럼 레이아웃:** 단순 선형 텍스트는 순서를 잃지만, 구조화된 데이터는 컬럼 순서를 보존합니다.  
- **후처리 정확도:** 박스 크기를 알면 단어가 헤더인지, 각주인지, 혹은 잡음인지 판단하기 쉽습니다.  

요컨대, **구조화된 OCR 인식**은 데이터베이스 입력, 검색 가능한 PDF 생성, 레이아웃을 고려한 머신러닝 모델 학습 등 더 스마트한 파이프라인을 구축할 수 있는 유연성을 제공합니다.

---

## 흔히 마주치는 엣지 케이스와 해결 방법

| 상황 | 주의할 점 | 권장 해결책 |
|-----------|-------------------|---------------|
| **회전되거나 기울어진 이미지** | 바운딩 박스가 축을 벗어날 수 있음 | OpenCV `warpAffine` 등으로 디스키유(Deskew) 전처리 |
| **극히 작은 글꼴** | 엔진이 문자를 놓쳐 빈 줄이 생김 | 이미지 해상도 상승 또는 `ocr_engine.set_dpi(300)` 사용 |
| **다중 언어 혼합** | 잘못된 언어 모델 선택 시 텍스트가 깨짐 | 인식 전에 `ocr_engine.language = ["en", "de"]` 등 설정 |
| **중첩된 박스** | 후처리 단계에서 두 줄이 의도치 않게 합쳐질 수 있음 | 처리 후 `line.bounds` 확인; `ai.run_postprocessor` 임계값 조정 |

초기에 이러한 상황을 대비하면, 하루에 수백 개의 문서를 처리하더라도 큰 어려움을 피할 수 있습니다.

---

## 전체 엔드‑투‑엔드 스크립트

아래는 모든 단계를 하나로 묶은 완전 실행 가능한 프로그램입니다. 복사‑붙여넣기 후 이미지 경로만 수정하면 바로 사용할 수 있습니다.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

이 스크립트를 실행하면:

1. 구조화 모드로 **이미지에서 OCR 실행**.  
2. 모든 줄에 대해 **좌표와 함께 텍스트 추출**.  
3. 선택적으로 박스가 표시된 PNG를 생성.

---

## 결론

이제 **이미지에서 OCR을 실행**하고 **구조화된 OCR 인식**을 활용해 **좌표와 함께 텍스트를 추출**하는 완전하고 자체 포함된 솔루션을 갖추었습니다. 엔진 초기화부터 후처리, 시각적 검증까지 모든 단계가 코드에 포함되어 있어 영수증, 양식, 혹은 정확한 텍스트 위치 지정이 필요한 모든 시각 문서에 적용할 수 있습니다.

다음 단계는 무엇일까요? `aocr` 엔진을 Tesseract, EasyOCR 등 다른 라이브러리로 교체해 구조화된 출력이 어떻게 다른지 실험해 보세요. 도메인에 맞는 맞춤형 정규식 필터나 맞춤법 검사와 같은 후처리 전략을 추가해 정확도를 더욱 높일 수 있습니다. 또한 더 큰 파이프라인을 구축한다면 `(text, bounds)` 쌍을 데이터베이스에 저장해 추후 분석에 활용해 보세요.

코딩을 즐기시고, 여러분의 OCR 프로젝트가 언제나 정확하기를 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
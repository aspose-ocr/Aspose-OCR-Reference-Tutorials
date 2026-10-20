---
category: general
date: 2026-03-28
description: 이미지에 OCR을 수행하고 경계 상자 좌표와 함께 정제된 텍스트를 얻습니다. OCR 추출, OCR 정제 및 결과 표시를 단계별로
  배우세요.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: ko
og_description: 이미지에서 OCR을 수행하고, 출력 결과를 정리한 뒤, 간결한 튜토리얼에서 경계 상자 좌표를 표시합니다.
og_title: 이미지에서 OCR 수행 – 깨끗한 결과와 경계 상자
tags:
- OCR
- Computer Vision
- Python
title: 이미지에서 OCR 수행 – 결과 정리 및 바운딩 박스 좌표 표시
url: /ko/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 OCR 수행 – 결과 정리 및 경계 상자 좌표 표시

이미지 파일에 **OCR을 수행**하고 싶지만 텍스트가 엉망이고 각 단어가 사진의 어느 위치에 있는지 모른 적이 있나요? 혼자만 그런 것이 아닙니다. 청구서 디지털화, 영수증 스캔, 간단한 텍스트 추출 등 많은 프로젝트에서 원시 OCR 출력은 첫 번째 장벽에 불과합니다. 좋은 소식은? 그 출력을 정리하고 수많은 보일러플레이트 코드를 작성하지 않고도 각 영역의 경계 상자 좌표를 즉시 확인할 수 있습니다.

이 가이드에서는 **OCR 추출 방법**, **OCR 정리 후처리 방법**, 그리고 최종적으로 **정리된 각 영역의 경계 상자 좌표 표시** 방법을 단계별로 살펴봅니다. 끝까지 따라오면 흐릿한 사진을 깔끔하고 구조화된 텍스트로 변환하는 단일 실행 스크립트를 얻게 됩니다.

## 준비 사항

- Python 3.9+ (아래 구문은 3.8 및 최신 버전에서도 동작)
- `recognize(..., return_structured=True)` 를 지원하는 OCR 엔진 – 예시에서는 가상의 `engine` 라이브러리를 사용합니다. Tesseract, EasyOCR, 혹은 영역 데이터를 반환하는 다른 SDK로 교체하세요.
- Python 함수와 반복문에 대한 기본 지식
- 스캔하려는 이미지 파일 (PNG, JPG 등)

> **Pro tip:** Tesseract를 사용한다면 `pytesseract.image_to_data` 함수가 이미 경계 상자를 제공합니다. 이 결과를 아래 `engine.recognize` API와 동일하게 동작하도록 작은 어댑터로 감싸면 됩니다.

---

![이미지에서 OCR 수행 예시](image-placeholder.png "이미지에서 OCR 수행 예시")

*Alt text: 이미지에서 OCR을 수행하고 경계 상자 좌표를 시각화하는 흐름을 보여주는 다이어그램*

## 1단계 – 이미지에서 OCR 수행 및 구조화된 영역 가져오기

먼저 OCR 엔진에 단순 텍스트가 아니라 구조화된 텍스트 영역 리스트를 반환하도록 요청합니다. 이 리스트는 원시 문자열과 이를 둘러싼 사각형 정보를 포함합니다.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**왜 중요한가:**  
단순 텍스트만 요청하면 공간적 컨텍스트를 잃게 됩니다. 구조화된 데이터는 이후 **경계 상자 좌표를 표시**하거나, 텍스트를 표와 정렬하거나, 정확한 위치 정보를 다운스트림 모델에 전달하는 데 활용할 수 있습니다.

## 2단계 – 후처리기로 OCR 출력 정리하기

OCR 엔진은 문자 인식에 뛰어나지만 종종 불필요한 공백, 줄바꿈 아티팩트, 잘못 인식된 기호 등을 남깁니다. 후처리기는 텍스트를 정규화하고 일반적인 OCR 오류를 수정하며 공백을 제거합니다.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

직접 클리너를 구현한다면 다음을 고려하세요:

- 비 ASCII 문자 제거 (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- 여러 개의 공백을 하나의 공백으로 축소
- `pyspellchecker` 같은 맞춤법 검사기로 명백한 오타 교정

**왜 신경 써야 할까:**  
정돈된 문자열은 검색, 인덱싱, 그리고 다운스트림 NLP 파이프라인의 신뢰성을 크게 높여줍니다. 다시 말해, **OCR 정리 방법**은 사용 가능한 데이터셋과 골칫거리 사이의 차이를 만들곤 합니다.

## 3단계 – 정리된 각 영역의 경계 상자 좌표 표시

텍스트가 정리되었으니 이제 각 영역을 순회하면서 사각형과 정리된 문자열을 출력합니다. 바로 여기서 **경계 상자 좌표를 표시**하게 됩니다.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**샘플 출력**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

이 좌표들을 그림 라이브러리(예: OpenCV)에 전달해 원본 이미지에 박스를 오버레이하거나, 나중에 조회할 수 있도록 데이터베이스에 저장할 수 있습니다.

## 전체 실행 가능한 스크립트

아래는 세 단계를 모두 연결한 완전한 프로그램입니다. 자리표시자 `engine` 호출을 실제 OCR SDK 호출로 교체하면 됩니다.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### 실행 방법

```bash
python perform_ocr.py sample_invoice.jpg
```

위와 같은 샘플 출력이 화면에 표시될 것입니다.

## 자주 묻는 질문 & 엣지 케이스

| 질문 | 답변 |
|----------|--------|
| **OCR 엔진이 `return_structured` 를 지원하지 않으면 어떻게 하나요?** | 엔진의 원시 출력(보통 좌표가 포함된 단어 리스트)을 `text` 와 `bounding_box` 속성을 가진 객체 리스트로 변환하는 얇은 래퍼를 작성합니다. |
| **신뢰도 점수를 얻을 수 있나요?** | 많은 SDK가 영역별 신뢰도 메트릭을 제공합니다. 출력문에 추가하세요: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **회전된 텍스트는 어떻게 처리하나요?** | `recognize` 호출 전에 OpenCV의 `cv2.minAreaRect` 로 이미지의 기울기를 보정합니다. |
| **출력을 JSON 형태로 받고 싶어요.** | `processed_result.regions` 를 `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)` 로 직렬화합니다. |
| **박스를 시각화할 방법이 있나요?** | 루프 안에서 OpenCV를 사용해 `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` 로 그린 뒤 `cv2.imwrite("annotated.jpg", img)` 로 저장합니다. |

## 마무리

이제 **이미지에서 OCR 수행**, 원시 출력 정리, 그리고 **각 영역의 경계 상자 좌표 표시** 방법을 배웠습니다. 인식 → 후처리 → 순회라는 3단계 흐름은 신뢰할 수 있는 텍스트 추출이 필요한 모든 Python 프로젝트에 재사용 가능한 패턴이 됩니다.

### 다음 단계는?

- **다양한 OCR 백엔드**(Tesseract, EasyOCR, Google Vision)를 탐색하고 정확도를 비교해 보세요.
- **데이터베이스와 연동**해 영역 데이터를 저장하고 검색 가능한 아카이브를 구축하세요.
- **언어 감지**를 추가해 각 영역을 적절한 맞춤법 검사기로 라우팅하세요.
- **원본 이미지에 박스 오버레이**를 적용해 시각적으로 검증하세요(위 OpenCV 스니펫 참고).

예상치 못한 문제가 발생하더라도, 가장 큰 성과는 견고한 후처리 단계에서 나온다는 점을 기억하세요. 깨끗한 문자열은 원시 문자 덤프보다 훨씬 다루기 쉽습니다.

행복한 코딩 되시고, OCR 파이프라인이 언제나 깔끔하게 유지되길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
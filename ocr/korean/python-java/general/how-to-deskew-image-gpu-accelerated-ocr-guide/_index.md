---
category: general
date: 2026-01-02
description: 이미지를 교정하고 대비를 높여 빠르게 일반 텍스트를 얻는 방법을 배워보세요. 단계별 파이썬 코드와 텍스트 추출 팁이 포함되어
  있습니다.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: ko
og_description: 이미지를 교정하고 대비를 높여 일반 텍스트를 얻는 방법. 테이블 추출 및 GPU 가속이 포함된 전체 Python 예제.
og_title: 이미지 기울기 보정 방법 – 완전한 GPU OCR 튜토리얼
tags:
- OCR
- Python
- Image Processing
title: 이미지 기울기 보정 방법 – GPU 가속 OCR 가이드
url: /ko/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지 기울기 보정 방법 – GPU‑Accelerated OCR 가이드

영수증이 이상한 각도로 들어올 때 **how to deskew image**가 궁금하셨나요? 혼자가 아닙니다; 기울어진 사진은 완전히 읽을 수 있는 영수증을 뒤죽박죽으로 만들 수 있습니다. 좋은 소식은 몇 줄의 Python 코드만으로 자동 기울기 보정, 대비 향상, 깨끗한 일반 텍스트 추출이 가능하다는 것입니다—수동 Photoshop은 필요 없습니다.  

이 튜토리얼에서는 **how to deskew image**뿐만 아니라 **how to boost contrast**, **get plain text**, 그리고 OCR 엔진이 발견한 표에서 **how to extract text**까지 보여주는 완전한 실행 가능한 예제를 단계별로 살펴보겠습니다. 끝까지 진행하면 어떤 프로젝트에도 넣을 수 있는 독립형 스크립트를 얻게 됩니다.

## 필요 사항

- Python 3.9+가 설치된 환경 (코드가 타입 힌트를 사용하므로 최신 인터프리터가 도움이 됩니다)
- `ocr` 라이브러리로 `OcrEngine`, `EngineMode`, `ImageProcessingOptions`, `OcrResult`를 제공합니다 (`pip install ocr‑sdk` 로 설치 – 사용 중인 실제 패키지 이름으로 교체하세요)
- 속도 향상이 필요하다면 호환 드라이버가 설치된 GPU (선택 사항이지만 권장)
- 조금 회전했거나 대비가 낮은 이미지 파일, 예: `receipt_skewed.jpg`

> **프로 팁:** GPU가 없으면 `EngineMode.GPU`를 `EngineMode.CPU`로 바꾸면 스크립트가 여전히 작동합니다—다소 느려질 뿐입니다.

## 단계별 구현

아래에서는 솔루션을 논리적인 청크로 나눕니다. 각 청크는 주요 키워드 *how to deskew image* 또는 보조 키워드가 포함된 설명적인 **H2**를 가지고 있습니다. 코드는 완전하고 주석이 달려 있으며 바로 실행할 수 있습니다.

### GPU‑Accelerated OCR를 사용한 이미지 기울기 보정 방법

먼저 OCR 엔진에 GPU에서 실행하도록 지정하고 자동 기울기 보정 기능을 활성화합니다. 자동 기울기 보정은 이미지의 기하학을 분석하여 정상적인 방향으로 회전시킵니다.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **왜 중요한가:** GPU 가속은 처리 시간을 초에서 밀리초로 단축시킬 수 있어, 분당 수십 장의 영수증을 처리할 때 매우 중요합니다.

### 더 나은 인식을 위한 이미지 대비 향상

대비가 낮은 영수증은 모든 OCR 시스템에 악몽과 같습니다. 대비를 높이면 엔진이 더 선명한 경계를 인식할 수 있습니다.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **대비를 높이는 방법:** `set_contrast_boost` 메서드는 백분율을 인수로 받습니다; 30 %는 대부분의 스캔된 영수증에 안전한 기본값입니다. 이미지가 매우 어두운 경우 50 %까지 올리거나 실험해 보세요.

### 처리된 이미지에서 일반 텍스트 추출

이미지가 바로잡히고 밝아졌으니, 이를 엔진에 전달하여 일반 텍스트 결과를 요청합니다.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**예상 출력** (간략히 표시):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **일반 텍스트를 얻는 방법:** `get_text()` 메서드는 레이아웃 정보를 모두 제거하고 깨끗한 문자열을 반환합니다. 이를 데이터베이스에 저장하거나 API에 전송하거나 후속 분석에 활용할 수 있습니다.

### 감지된 표에서 텍스트 추출 방법

영수증에는 종종 표 형식의 데이터(항목, 수량, 가격)가 포함됩니다. OCR SDK는 표를 감지하고 행과 셀을 반복 처리할 수 있게 해줍니다.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**샘플 표 출력**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **표를 추출하는 이유:** 구조화된 데이터는 합계 계산, 보고서 생성, 회계 소프트웨어 연동 등을 간단하게 해줍니다.

### 전체 작동 스크립트

모든 것을 합치면, `deskew_and_ocr.py`에 복사‑붙여넣기 할 수 있는 스크립트는 다음과 같습니다:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

다음 명령으로 실행하세요:

```bash
python deskew_and_ocr.py
```

정리된 텍스트와 감지된 표가 콘솔에 출력될 것입니다.

## 일반적인 엣지 케이스 및 처리 방법

| 상황 | 조치 |
|-----------|------------|
| **Image is upside‑down** | SDK에서 지원한다면 `set_rotation_correction(True)`를 추가 호출하여 `set_auto_deskew(True)` 신뢰도를 높이세요. |
| **Contrast boost makes the image too bright** | `set_contrast_boost`에 전달하는 백분율을 낮추세요(예: 15 %). |
| **GPU not available** | `EngineMode.GPU`를 `EngineMode.CPU`로 전환하세요; 파이프라인의 나머지는 그대로 유지됩니다. |
| **Tables are missed** | 해상도를 높인 스캔을 시도하거나 라이브러리가 제공한다면 `set_table_detection(True)`를 활성화하세요. |

## 다음 단계: 일반 텍스트에서 구조화된 데이터로

이제 **how to deskew image**, **how to boost contrast**, **how to get plain text**를 알게 되었으니, 다음과 같이 진행할 수 있습니다:

- 정규 표현식을 사용해 일반 텍스트를 파싱하여 키‑값 쌍(예: `total`, `date`)을 추출합니다.
- 결과를 SQLite 또는 PostgreSQL 데이터베이스에 저장하여 나중에 보고합니다.
- 스크립트를 서버리스 함수(AWS Lambda, Azure Functions)에 연결하여 업로드를 자동으로 처리합니다.

이 모든 확장은 여기서 다룬 동일한 기반 위에 구축됩니다.

## 결론

우리는 GPU 가속 OCR 엔진을 사용한 **how to deskew image** 과정을 살펴보고, 더 선명한 인식을 위한 **how to boost contrast**를 시연했으며, 정확히 **how to get plain text**를 보여주고, 표에서 **how to extract text**까지 다루었습니다. 완전하고 실행 가능한 스크립트가 모든 것을 연결해 주므로, 이를 어떤 Python 프로젝트에든 넣어 바로 기울어지고 대비가 낮은 사진에서 깨끗한 데이터를 추출할 수 있습니다.

자신의 영수증 몇 장으로 시도해 보고, 대비 수준을 조정한 뒤 OCR이 무거운 작업을 수행하도록 해보세요. 문제가 발생하면 위의 엣지 케이스 표를 다시 확인하세요—대부분의 문제는 작은 조정만으로 해결됩니다.

코딩 즐겁게 하시고, 이미지가 언제나 똑바르고 밝게 유지되길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
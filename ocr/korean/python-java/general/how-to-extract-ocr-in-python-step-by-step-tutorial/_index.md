---
category: general
date: 2026-04-26
description: Python을 사용해 이미지에서 OCR을 추출하는 방법 – OCR을 위해 이미지를 로드하고 영수증에서 텍스트를 추출하는 Python
  OCR 예제.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: ko
og_description: Python을 사용해 이미지에서 OCR을 추출하는 방법. 파이썬 OCR 예제를 배우고, OCR용 이미지를 로드하며, 영수증에서
  텍스트를 몇 분 안에 추출하세요.
og_title: Python에서 OCR 추출하는 방법 – 완전 가이드
tags:
- OCR
- Python
- Image Processing
title: Python에서 OCR 추출 방법 – 단계별 튜토리얼
url: /ko/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 OCR 추출 방법 – 완전 가이드

흐릿한 영수증이나 스캔한 청구서에서 **how to extract ocr**가 궁금하셨나요? 당신만 그런 것이 아닙니다—개발자들은 이미지에서 깨끗하고 기계가 읽을 수 있는 텍스트가 필요할 때마다 벽에 부딪히곤 합니다. 좋은 소식은? 몇 줄의 Python 코드만으로 영수증 사진을 고신뢰도, 검색 가능한 텍스트로 변환할 수 있다는 것입니다.

이 튜토리얼에서는 **python ocr example**을 통해 **how to load image for ocr**를 시연하고, 엔진을 실행한 뒤 85 % 신뢰도 임계값을 만족하는 문자만 남기는 과정을 보여드립니다. 끝까지 따라오시면 **extract text from receipt** 이미지를 문서 검색이나 API 파라미터 추측 없이 바로 추출할 수 있게 됩니다.

## What You’ll Need

- Python 3.9 이상 (우리가 사용하는 구문은 3.8+에서도 동작합니다)
- `aocr` 패키지 (또는 `OcrEngine` 클래스를 제공하는 任意 OCR 라이브러리). 다음 명령으로 설치합니다:

```bash
pip install aocr
```

- `receipt.png` 라는 샘플 영수증 이미지가 있는 폴더
- 텍스트 편집기 또는 IDE—VS Code, PyCharm, 혹은 간단한 노트북도 충분합니다.

그게 전부입니다. 무거운 프레임워크도, 외부 서비스도 필요 없고 순수 Python만 있으면 됩니다.

![High‑confidence OCR result – how to extract ocr from a receipt](/images/ocr-high-confidence.png)

*이미지 대체 텍스트: Python OCR을 사용한 how to extract ocr from a receipt*

## Step 1 – Create the OCR Engine Instance (how to extract ocr)

먼저 OCR 엔진을 시작합니다. 이는 픽셀을 읽어줄 두뇌와 같습니다.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Why?** `OcrEngine`을 인스턴스화하면 새로운 설정 객체를 얻게 됩니다. 이후 언어 모델, DPI 설정, 전처리 단계 등을 코어 처리 루프를 건드리지 않고 조정할 수 있습니다.

## Step 2 – Load the Image for OCR

다음으로 엔진이 분석할 이미지를 지정합니다. 여기서 **load image for ocr** 키워드가 등장합니다.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Pro tip:** 이미지가 다른 디렉터리에 있다면 `os.path.join`을 사용해 플랫폼에 독립적인 경로를 만들세요.

**Why load the image this way?** `Image.load` 헬퍼는 파일을 엔진이 이해할 수 있는 형식으로 읽어들여 PNG, JPEG, TIFF 등 일반 포맷을 자동으로 처리합니다. 이 단계를 건너뛰거나 원시 바이트를 직접 전달하면 `ValueError`가 발생합니다.

## Step 3 – Run the OCR Process

이제 실제로 OCR을 실행합니다. `process` 메서드는 인식된 심볼, 신뢰도 점수, 바운딩 박스를 포함한 풍부한 결과 객체를 반환합니다.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**What does `ocr_result` contain?** 대부분의 라이브러리에서 다음과 같은 정보를 제공합니다:

- `text`: 원시 연결 문자열
- `symbol_confidences`: `(char, confidence)` 튜플 리스트
- `boxes`: 각 문자에 대한 좌표 (시각적 디버깅에 유용)

문자별 신뢰도에 접근할 수 있어야 다음 단계가 가능해집니다.

## Step 4 – Keep Only High‑Confidence Symbols (≥ 85 %)

영수증에는 얼룩, 흐릿한 인쇄, 배경 잡음 등이 흔히 존재합니다. 낮은 신뢰도의 심볼을 걸러내면 후속 파싱 정확도가 크게 향상됩니다.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Why 85 %?** 경험적으로 0.85 정도의 임계값이 대부분의 인쇄 영수증에서 재현율과 정밀도의 균형을 맞춥니다. 숫자가 누락되면 임계값을 낮추고, 의미 없는 문자열이 나오면 높이세요.

## Step 5 – Output the High‑Confidence Extracted Text

마지막으로 정제된 문자열을 출력(또는 저장)합니다. 이것이 **extract text from receipt** 워크플로우의 핵심입니다.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

Typical output looks like:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

이제 이 문자열을 CSV 라이터, 데이터베이스, 혹은 다른 분석 파이프라인에 바로 전달할 수 있습니다.

## Full, Ready‑to‑Run Script

아래는 `ocr_receipt.py`에 복사‑붙여넣기만 하면 바로 실행할 수 있는 전체 코드 스니펫입니다.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

파일을 저장하고 `receipt.png`가 존재하는지 확인한 뒤 실행하세요:

```bash
python ocr_receipt.py
```

콘솔에 정리된 영수증 텍스트가 출력될 것입니다.

## Edge Cases & What‑If Scenarios

| Situation | Suggested Fix |
|-----------|----------------|
| **Very low confidence across the board** | 이미지 전처리: 대비 증가, 그레이스케일 변환, 혹은 `cv2.GaussianBlur` 같은 노이즈 제거 필터 적용 |
| **Non‑Latin characters** | `OcrEngine`에 언어 모델 전달 (`ocr_engine.language = "spa"` 등) |
| **Multiple receipts in one image** | 전체 이미지에 OCR을 실행한 뒤 `\n\n+` (두 개 이상의 연속 개행) 정규식을 이용해 결과를 분할 |
| **Need the raw OCR text as well** | 디버깅을 위해 필터링된 버전과 함께 `ocr_result.text`를 보관 |

These variations ensure your **how to use OCR** knowledge scales beyond the simplest case.

## Common Pitfalls (And How to Avoid Them)

- **Forgetting to install the library** – `pip install aocr`가 성공해야 import가 가능합니다.
- **Using the wrong path separator** on Windows (`\` vs `/`). `os.path.join`을 사용하세요.
- **Hard‑coding the confidence threshold** without testing – 몇 개의 영수증으로 빠르게 시각적 검증을 먼저 수행하세요.
- **Ignoring Unicode normalisation** – 일부 영수증에 특수 대시 문자가 포함될 수 있습니다. 출력 저장 전 `unicodedata.normalize('NFKC', text)`를 실행하세요.

## Next Steps – Going Beyond the Basics

이제 **how to extract ocr** 데이터를 단일 영수증에서 추출하는 방법을 알았으니, 다음과 같은 작업을 고려해 보세요:

1. **Batch process a folder of receipts** – 모든 PNG/JPG 파일을 순회하며 각 결과를 CSV에 기록
2. **Integrate with a database** – `high_confidence_text`를 SQLite에 저장해 빠르게 조회
3. **Apply natural‑language parsing** – 정규식이나 `dateutil`을 사용해 날짜, 총액, 세금 등을 추출
4. **Experiment with alternative libraries** – `pytesseract`, `easyocr`, 혹은 클라우드 서비스(Google Vision, Azure OCR)를 활용해 다국어 지원이나 정확도 향상

각 주제는 *python ocr example*, *extract text from receipt*, *load image for ocr*, *how to use OCR* 라는 보조 키워드와 자연스럽게 연결됩니다.

## Conclusion

우리는 **python ocr example**을 통해 영수증 이미지에서 **how to extract ocr** 텍스트를 추출하고, 낮은 신뢰도의 심볼을 필터링한 뒤 깨끗한 결과를 출력하는 전체 과정을 살펴보았습니다. 단계는 간단하고 코드도 독립적이며, 더 큰 프로젝트에 적용하기에도 유연합니다.

직접 영수증으로 시도해 보고, 신뢰도 임계값을 조정한 뒤 배치 처리로 확장해 보세요. 로고가 흐리거나 특이한 폰트와 같은 문제에 직면한다면 위의 예외 상황 팁을 기억하세요. 즐거운 코딩 되시고, OCR 파이프라인이 언제나 정확하기를 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
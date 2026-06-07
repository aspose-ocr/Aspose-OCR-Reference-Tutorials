---
category: general
date: 2026-06-06
description: Python을 사용해 이미지에 OCR을 실행하고 신뢰도 점수를 확인하세요. 낮은 신뢰도의 단어를 필터링하고, 임계값을 설정하며,
  엣지 케이스를 처리하는 방법을 배워보세요.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: ko
og_description: Python에서 이미지에 OCR을 실행하고, 신뢰도 수준을 확인한 뒤 신뢰도가 낮은 단어를 필터링합니다. 이 튜토리얼은
  완전하고 실행 가능한 예제를 단계별로 안내합니다.
og_title: Python으로 이미지에서 OCR 실행 – 전체 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Python으로 이미지에서 OCR 실행 – 완전한 단계별 가이드
url: /ko/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python으로 이미지에서 OCR 실행 – 완전 단계별 가이드

이미지 파일에서 **run OCR on image** 해야 할 때, 신뢰할 수 있는 텍스트를 추출하는 방법을 몰라 고민한 적 있나요? 당신만 그런 것이 아닙니다—많은 개발자들이 추출된 단어가 흐릿하게 보이고 confidence 점수가 이해되지 않아 같은 벽에 부딪히곤 합니다.  

이 가이드에서는 바로 사용할 수 있는 솔루션을 살펴봅니다: **run OCR on image** 하는 방법, 전체 confidence를 읽는 방법, 그리고 수동 검토가 필요할 수 있는 low‑confidence 단어들을 추출하는 방법을 보여드립니다. 끝까지 읽으면 재사용 가능한 스크립트를 얻고, 각 라인이 왜 중요한지 이해하며, 프로젝트에 맞게 confidence threshold를 조정하는 방법을 알게 됩니다.

## 이 튜토리얼에서 다루는 내용

이미지를 로드하는 단계부터 80 % confidence 이하인 단어들을 깔끔하게 보고하는 단계까지 전체 워크플로를 단계별로 살펴보겠습니다. 진행하면서 다음을 논의합니다:

* 견고한 OCR 엔진 선택 (우리는 **EasyOCR**이라는 인기 있는 Python OCR 라이브러리를 사용할 것입니다)  
* 모든 OCR 결과가 반환하는 `confidence` 속성 해석하기  
* 사용자 정의 **OCR confidence threshold** 로 단어 필터링하기  
* 배치 처리 또는 **pytesseract**와 같은 대체 엔진을 위한 스크립트 확장하기  

사전 OCR 경험은 필요 없으며, Python에 대한 기본적인 이해와 작업 환경만 있으면 됩니다 (Python 3.9+ 권장).

흐릿한 스크린샷을 깔끔하고 검색 가능한 텍스트로 바꿀 준비가 되셨나요? 시작해봅시다.

---

## ## Python으로 이미지에서 OCR 실행 방법

튜토리얼의 핵심은 앞서 본 코드를 그대로 반영한 3단계 스니펫입니다. 아래에서 각 라인을 자세히 살펴보고 이유를 설명한 뒤, 완전한 복사‑붙여넣기 가능한 스크립트를 제공하겠습니다.

### Step 1: OCR 엔진 설치 및 임포트

먼저 OCR 라이브러리가 사용 가능한지 확인하세요. **EasyOCR**는 다수의 언어를 바로 지원하며 단어별 confidence 점수를 제공합니다.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Why EasyOCR?* 다양한 데이터셋으로 학습된 딥러닝 모델을 포함하고 있어, 특히 품질이 혼합된 이미지에서 오래된 Tesseract 엔진보다 일반적으로 더 높은 confidence 값을 얻을 수 있습니다.

> **Pro tip:** 제한된 환경(예: 작은 Docker 컨테이너)에서 작업한다면 `pytesseract`가 더 가벼울 수 있지만, EasyOCR가 제공하는 최신 정확도 중 일부를 잃게 됩니다.

### Step 2: 이미지에서 OCR 실행

이제 실제로 **run OCR on image** 를 수행합니다. 원본 예제의 `recognize_image` 메서드는 EasyOCR의 `readtext` 호출로 대체되며, 이는 `(bbox, text, confidence)` 튜플 리스트를 반환합니다.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

`ocr_results`의 각 항목은 다음과 같습니다:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

세 번째 요소(`0.92` 예시)는 0에서 1 사이의 confidence 점수입니다.

### Step 3: 전체 confidence 요약

이전 스니펫이 단일 `confidence` 속성을 출력한 것과 달리, EasyOCR는 단어별 confidence를 제공합니다. 전체적인 감을 잡기 위해 평균을 구해보겠습니다:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Why average?* 빠른 상태 점검을 할 수 있습니다—전체 confidence가 예를 들어 70 % 이하라면 이미지(조명 개선, 전처리 등)를 개선해야 할 가능성이 높습니다.

### Step 4: Low‑Confidence 단어 목록

이제 “confidence가 원하는 임계값 이하인 단어를 나열” 요구사항을 직접 만족시키는 부분입니다. 기본값으로 **OCR confidence threshold** 를 0.80(80 %)으로 설정하지만, 필요에 따라 조정할 수 있습니다.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

루프는 기준에 미달한 각 단어와 해당 confidence 퍼센트를 출력합니다. 이는 원래 `for recognized_word in recognition_result.words` 루프와 정확히 동일하지만, 이제 EasyOCR의 출력 형식에 맞게 동작합니다.

---

## ## OCR confidence 점수 이해하기

Confidence는 마법 같은 숫자가 아니라, 특정 전사에 대해 모델이 얼마나 확신하는지를 추정한 값입니다. 기억해두면 좋은 몇 가지 사항은 다음과 같습니다:

| 상황 | 일반적인 Confidence | 조치 |
|-----------|-------------------|------------|
| 선명하고 고해상도 스캔 | 0.95 – 1.00 | 추가 작업 필요 없음 |
| 약간의 흐림 또는 고르지 않은 조명 | 0.80 – 0.94 | 약간의 전처리(대비 향상) 고려 |
| 많은 노이즈, 회전된 텍스트 | < 0.70 | 이미지 전처리(디스큐, 노이즈 제거) 적용 또는 다른 OCR 엔진으로 전환 |

> **Watch out:** 일부 언어(예: 필기체)에서는 자연스럽게 낮은 점수가 나올 수 있습니다. 그에 맞게 임계값을 조정하세요.

### 엣지 케이스 및 변형

1. **Batch Processing** – 대량으로 **run OCR on image** 파일을 처리해야 한다면, 위 로직을 디렉터리를 순회하는 루프로 감싸세요.  
2. **Multiple Languages** – `easyocr.Reader`에 `['en', 'fr']`와 같은 리스트를 전달하면 엔진이 두 언어를 모두 감지합니다.  
3. **Alternative Engines** – **pytesseract**를 사용해 보고 싶나요? 리더 블록을 다음과 같이 교체하세요:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   그런 다음 문자별 confidence를 단어별 값으로 집계해야 합니다—조금 더 작업이 필요하지만 가능합니다.

4. **Pre‑processing Tricks** – OpenCV 필터(`cv2.threshold`, `cv2.GaussianBlur`)를 적용하면 노이즈가 많은 스캔의 confidence를 높일 수 있습니다.  

---

## ## 완전 실행 가능한 스크립트

아래는 프로젝트에 바로 넣을 수 있는 완전한 Python 파일입니다. `ocr_report.py`로 저장하고 `python ocr_report.py`를 실행하세요. 이미지 경로가 실제 파일을 가리키는지 확인하십시오.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Expected output** (당신의 결과는 다를 수 있습니다):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

모든 단어가 80 % 기준을 통과하면 친절한 “All words meet the confidence threshold.” 메시지가 표시됩니다.

---

## ## 자주 묻는 질문 (FAQ)

**Q: Does this work with PDFs?**  
A: 직접적으로는 지원되지 않습니다. 각 PDF 페이지를 먼저 이미지(PNG/JPEG)로 변환(`pdf2image` 등)한 뒤 스크립트에 전달하세요.

**Q: My confidence numbers are all low—what can I do?**  
A: 이미지 전처리를 시도해 보세요: 대비를 높이고, 배경 노이즈를 제거하거나 이미지를 수평 기준으로 회전합니다. EasyOCR는 조정 가능한 `contrast_ths` 파라미터도 지원합니다.

**Q: Can I export the results to CSV?**  
A: 물론 가능합니다. low‑confidence 루프 이후에 `ocr_results`를 `csv.DictWriter`에 기록하면 각 행에 `text`, `confidence`, 그리고 bounding‑box 좌표가 포함됩니다.

**Q: Is there a GPU‑accelerated version?**  
A: 호환 가능한 GPU와 PyTorch가 설치되어 있으면 EasyOCR가 자동으로 CUDA를 사용합니다. 스크립트를 실행하기 전에 `torch.cuda.is_available()`로 확인하세요.

---

## 결론

우리는 방금 Python을 사용해 **run OCR on image** 를 수행하고, 전체 confidence를 검사했으며, 낮은 confidence를 가진 단어들을 분리했습니다.

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 동작 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움을 줍니다.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
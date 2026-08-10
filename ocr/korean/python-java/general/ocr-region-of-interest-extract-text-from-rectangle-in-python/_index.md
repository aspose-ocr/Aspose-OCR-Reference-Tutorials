---
category: general
date: 2026-05-31
description: OCR 관심 영역을 사용하여 이미지를 로드하고 사각형에서 텍스트를 추출하는 방법을 배우세요. 청구서의 금액을 인식하는 데 완벽합니다.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: ko
og_description: OCR 영역(ROI)을 마스터하여 이미지를 로드하고, 사각형에서 텍스트를 추출하며, 청구서 텍스트를 인식하는 단일 튜토리얼.
og_title: OCR 관심 영역 – 단계별 파이썬 가이드
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR 관심 영역 – 파이썬에서 사각형으로부터 텍스트 추출
url: /ko/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – 사각형에서 텍스트 추출 (Python)

스캔한 청구서의 특정 부분만 OCR에 넣고 전체 페이지를 처리하지 않고도 **ocr region of interest** 하는 방법이 궁금하셨나요? 흐릿한 영수증을 보며 “오른쪽 아래에 있는 금액을 어떻게 추출하지?” 라고 고민한 적이 있다면 당신만이 아닙니다. 좋은 소식은 OCR 라이브러리에게 정확히 어디를 볼지 알려줄 수 있어 속도와 정확성을 크게 높일 수 있다는 점입니다.

이 가이드에서는 **load image for OCR**, **region of interest** 정의, **extract text from rectangle** 수행, 그리고 최종적으로 **recognize text from invoice** 하여 고전적인 “금액을 어떻게 추출하나요?” 질문에 답하는 완전하고 실행 가능한 예제를 단계별로 살펴보겠습니다. 모호한 언급이 아니라 구체적인 코드와 명확한 설명, 그리고 미리 알면 좋을 몇 가지 팁을 제공합니다.

---

## What You’ll Build

이 튜토리얼을 마치면 다음을 수행하는 작은 Python 스크립트를 얻게 됩니다:

1. 디스크에서 청구서 이미지를 로드합니다.  
2. 총액이 위치한 사각형 ROI를 표시합니다.  
3. 해당 ROI 내부에서만 OCR을 실행합니다.  
4. 정제된 금액 문자열을 출력합니다.  

이 모든 과정은 ROI를 지원하는 어떤 OCR 라이브러리와도 동작합니다—여기서는 Tesseract나 EasyOCR와 같은 도구를 모방한 가상의 `SimpleOCR` 패키지를 사용합니다. 필요에 따라 교체해도 개념은 동일합니다.

---

## Prerequisites

- Python 3.8+ 설치 (`python --version` 명령으로 ≥3.8 확인).  
- pip으로 설치 가능한 OCR 패키지 (예: `pip install simpleocr`).  
- 청구서 이미지 (PNG 또는 JPEG) 를 참조 가능한 폴더에 배치.  
- Python 함수와 클래스에 대한 기본 이해 (특별한 지식은 필요 없음).

위 조건을 이미 갖추었다면 바로 시작하세요. 아직이라면 먼저 이미지를 준비해 두세요; 나머지 단계는 파일 내용과 무관합니다.

---

## Step 1: Load Image for OCR

OCR 워크플로우의 첫 단계는 읽을 비트맵이 필요합니다. 대부분의 라이브러리는 파일 경로를 받아들이는 간단한 `load_image` 메서드를 제공합니다. `SimpleOCR` 엔진으로는 다음과 같이 수행합니다:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** 스크립트를 다른 작업 디렉터리에서 실행할 때 “file not found” 오류를 방지하려면 절대 경로나 `os.path.join`을 사용하세요.

---

## Step 2: Define OCR Region of Interest

엔진이 전체 페이지를 스캔하도록 두는 대신, 금액이 정확히 위치한 영역을 지정합니다. 이것이 **ocr region of interest** 단계이며, 특히 문서에 잡음이 많은 헤더나 푸터가 있을 때 신뢰할 수 있는 추출을 위한 핵심입니다.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

왜 이런 숫자인가요? `x`와 `y`는 좌상단 모서리에서의 픽셀 오프셋이며, `width`와 `height`는 박스 크기를 나타냅니다. 확실하지 않다면 이미지 편집기에서 눈금자를 켜고 좌표를 확인하세요. 많은 IDE가 커서를 올릴 때 위치를 표시해 주기도 합니다.

---

## Step 3: Extract Text from Rectangle

ROI가 설정되었으니 이제 엔진에게 **recognize text from invoice** 를 요청하지만, 방금 지정한 사각형 내부에만 제한합니다. 호출 결과는 일반적으로 원시 문자열, 신뢰도 점수, 때로는 경계 상자를 포함하는 객체를 반환합니다.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

내부적으로 `recognize()` 는 각 ROI를 순회하면서 해당 영역을 잘라내고 OCR 모델을 실행한 뒤 결과를 합칩니다. 따라서 **extract text from rectangle** 영역을 꽉 맞게 정의하면 배치 작업에서 처리 시간을 몇 초 단축할 수 있습니다.

---

## Step 4: How to Extract Amount – Clean the Output

OCR은 완벽하지 않으며, 종종 불필요한 공백, 줄 바꿈, 혹은 문자 오인(예: “S”와 “5”)이 섞여 나옵니다. `strip()` 과 짧은 정규식 하나만으로도 금액 값은 대부분 정리됩니다.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** 금액을 데이터베이스나 결제 게이트웨이에 전달하려면 예측 가능한 형식이 필요합니다. 공백을 제거하고 숫자가 아닌 문자를 필터링하면 후속 오류를 방지할 수 있습니다.

---

## Step 5: Recognize Text from Invoice – Full Script

모든 것을 하나로 합치면 다음과 같은 완전한 실행 스크립트가 됩니다. `extract_amount.py` 로 저장하고 `python extract_amount.py` 로 실행하세요.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Expected Output

```
Amount: 1,245.67
```

ROI가 잘못 정렬되면 `Amount: 1245.6S` 와 같이 “S” 같은 잡음이 보일 수 있습니다. 사각형 좌표를 조정하고 다시 실행해 출력이 깔끔해질 때까지 반복하세요.

---

## Common Pitfalls & Edge Cases

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ROI too small** | 금액 텍스트가 잘려서 부분적으로만 인식됩니다. | `width`/`height` 를 약 10‑20 % 확대하고 재시험하세요. |
| **Incorrect DPI** | 저해상도 스캔(≤150 dpi) 은 OCR 정확도를 떨어뜨립니다. | 로드하기 전에 이미지를 300 dpi 로 재샘플링하거나 스캐너에 고해상도를 요청하세요. |
| **Multiple currencies** | 정규식이 첫 번째 숫자 그룹을 잡아 청구서 번호가 선택될 수 있습니다. | 숫자 앞에 통화 기호(`$`, `€`, `£`) 를 찾도록 정규식을 개선하세요. |
| **Rotated invoices** | OCR 엔진은 보통 수평 텍스트를 가정하므로 회전된 페이지는 인식이 깨집니다. | ROI를 추가하기 전에 `ocr_engine.rotate(90)` 로 회전 보정하세요. |
| **Noise in background** | 그림자나 도장이 모델을 혼란시킵니다. | 간단한 임계값(`cv2.threshold`) 처리나 노이즈 제거 필터를 적용하세요. |

초기에 이러한 상황을 해결하면 나중에 디버깅에 드는 시간을 크게 절감할 수 있습니다.

---

## Pro Tips for Real‑World Projects

- **Batch Processing:** 청구서 폴더를 순회하면서 ROI를 동적으로 계산(예: 템플릿 감지 기반)하고 결과를 CSV 로 저장합니다.  
- **Template Matching:** 여러 청구서 레이아웃을 다룰 경우 `template_id → ROI coordinates` 매핑을 JSON 으로 관리하고, 빠른 레이아웃 분류기로 ROI를 전환합니다.  
- **Parallel Execution:** `concurrent.futures.ThreadPoolExecutor` 를 사용해 여러 OCR 인스턴스를 동시에 실행하면 대량 백오피스 파이프라인에 유리합니다.  
- **Confidence Filtering:** 대부분의 OCR 결과에는 신뢰도 점수가 포함됩니다. 85 % 이하 결과는 버리고 수동 검토 대상으로 표시하세요.

---

## Conclusion

우리는 **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, 그리고 최종적으로 **recognize text from invoice** 를 통해 고전적인 **how to extract amount** 질문에 답하는 전체 흐름을 다루었습니다. 스크립트는 작지만 다양한 문서 형식, 언어, OCR 백엔드에 맞게 확장 가능하도록 설계되었습니다.

이제 기본을 마스터했으니 워크플로우를 확장해 보세요: 바코드 스캔 추가, PDF 파서와 연동, 혹은 추출된 금액을 회계 API에 전송 등. ROI를 명확히 정의하면 언제나 더 빠르고 깨끗한 결과를 얻을 수 있습니다.

문제가 발생하면 아래에 댓글을 남겨 주세요—즐거운 OCR 작업 되세요!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## What Should You Learn Next?

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
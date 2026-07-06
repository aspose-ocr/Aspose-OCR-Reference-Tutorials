---
category: general
date: 2026-06-22
description: Python을 사용하여 이미지에서 경계 상자 좌표를 가져옵니다. Aspose OCR과 JSON 파싱을 활용해 몇 분 안에 이미지에서
  텍스트를 추출하는 방법을 배워보세요.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: ko
og_description: Python을 사용하여 이미지에서 경계 상자 좌표를 가져옵니다. 이 가이드는 Aspose OCR로 이미지에서 텍스트를
  추출하고 레이아웃 데이터를 파싱하는 방법을 보여줍니다.
og_title: Python으로 OCR에서 바운딩 박스 좌표 가져오기 – 전체 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Python에서 OCR을 사용해 경계 상자 좌표 얻기 – 완전 가이드
url: /ko/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 OCR을 사용해 바운딩 박스 좌표 가져오기 – 완전 가이드

스캔한 청구서의 모든 단어에 대해 **바운딩 박스 좌표**를 얻어야 했지만 어디서 시작해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다. 많은 자동화 프로젝트에서 텍스트를 이미지 위에 표시하거나 가리거나, 후속 분석에 전달해야 할 때가 있습니다. 좋은 소식은? 몇 줄의 Python 코드와 Aspose.OCR만 있으면 텍스트 **와** 정확한 위치를 한 번에 가져올 수 있다는 것입니다.

이 튜토리얼에서는 **image python** 스타일로 텍스트를 추출하고, JSON 레이아웃 데이터를 파싱해 바운딩 박스를 꺼내는 실습 예제를 단계별로 살펴봅니다. 불필요한 내용 없이 동작하는 스크립트, 각 단계가 왜 중요한지에 대한 설명, 그리고 흔히 발생하는 함정을 피하는 팁을 제공합니다.

---

## 만들게 될 것

이 가이드를 끝까지 따라오면 다음을 수행하는 Python 스크립트를 바로 실행할 수 있습니다:

1. 이미지를 (예: 청구서 PNG) Aspose OCR에 로드합니다.  
2. 엔진을 JSON 레이아웃 정보를 출력하도록 설정합니다.  
3. JSON을 Python 사전(dict)으로 파싱합니다.  
4. 인식된 모든 단어를 순회하면서 텍스트 **와** 바운딩 박스 좌표를 출력합니다.

또한 다페이지 PDF, 다양한 이미지 포맷, 사용자 정의 좌표계에 맞게 코드를 조정하는 방법도 확인할 수 있습니다.

### 사전 요구 사항

- 머신에 Python 3.8+이 설치되어 있어야 합니다.  
- 활성화된 Aspose.OCR for Python 라이선스 또는 무료 체험판(라이선스 없이도 사용 가능하지만 워터마크가 추가됩니다).  
- `pip install aspose-ocr` (PyPI에 등록된 패키지 이름).  
- `invoice.png` 라는 샘플 이미지를 참조 가능한 폴더에 배치합니다.

그게 전부—무거운 프레임워크도, 외부 서비스도 필요 없습니다. 바로 시작해 보세요.

---

## Step 1: 필수 라이브러리 설치 및 임포트

먼저 Aspose OCR 패키지와 내장 `json` 모듈이 사용 가능한지 확인합니다. `json` 모듈은 Python에 기본 포함되어 있으므로 Aspose만 설치하면 됩니다.

```bash
pip install aspose-ocr
```

이제 스크립트에서 임포트합니다:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **왜 중요한가:** `aspose.ocr`를 임포트하면 고성능 OCR 엔진에 접근할 수 있고, `json`을 사용하면 원시 레이아웃 문자열을 Python 사전으로 변환해 쉽게 탐색할 수 있습니다.

---

## Step 2: OCR 엔진 생성 및 이미지 로드

엔진은 전체 프로세스의 핵심입니다. 엔진을 인스턴스화한 뒤 스캔할 이미지 경로를 지정합니다.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **프로 팁:** `"YOUR_DIRECTORY/invoice.png"`을 실제 파일을 가리키는 절대 경로나 상대 경로로 교체하세요. 파일을 찾을 수 없으면 Aspose가 `FileNotFoundError`를 발생시키니 경로 철자를 다시 확인하세요.

---

## Step 3: 엔진을 JSON 레이아웃 데이터 출력하도록 설정

Aspose OCR은 일반 텍스트, OCR‑전용 JSON, 혹은 단어·줄·문자 개별 좌표를 포함한 전체 레이아웃 JSON을 반환할 수 있습니다. **바운딩 박스 좌표**를 얻기 위해서는 레이아웃 JSON이 필요합니다.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **왜 JSON인가?** JSON은 언어에 구애받지 않으며 사람이 읽기 쉽고 Python 사전으로 깔끔하게 매핑됩니다. 레이아웃 JSON에는 각 단어와 `boundingBox` 배열(8개의 숫자, 네 개의 코너 포인트)이 들어 있는 `"words"` 배열이 포함됩니다.

---

## Step 4: 인식 실행 및 원시 JSON 문자열 가져오기

이제 실제 OCR을 수행합니다. `recognize()` 메서드는 `OcrResult` 객체를 반환하고, 여기서 JSON 문자열을 추출할 수 있습니다.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

`layout_json`을 출력하면 다음과 같은 형태가 나타납니다:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **예외 상황:** 이미지에 따라 OCR 엔진이 텍스트를 감지하지 못하면 `"words"` 배열이 비어 있을 수 있습니다. 이 경우 이미지 품질(대비, 해상도)을 확인한 뒤 다시 시도하세요.

---

## Step 5: JSON을 Python 사전으로 파싱

문자열을 직접 다루는 것보다 네이티브 Python 구조를 사용하는 것이 훨씬 쉽습니다. `json.loads()` 함수를 이용해 문자열을 변환합니다.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

이제 `layout_data["words"]`는 각 단어와 바운딩 박스를 나타내는 사전들의 리스트가 됩니다.

---

## Step 6: 단어를 순회하며 **바운딩 박스 좌표 가져오기**

튜토리얼의 핵심 부분입니다. 각 단어를 반복하면서 텍스트를 추출하고 좌표를 출력합니다. 바로 여기서 **바운딩 박스 좌표**를 얻습니다.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**샘플 출력** (이미지에 따라 숫자는 다르게 나타납니다):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **왜 8점 형식인가?** 네 개의 코너(좌상, 우상, 우하, 좌하)를 제공하므로 텍스트가 기울어져 있어도 폴리곤을 그릴 수 있습니다. 단순 사각형만 필요하다면 `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, `height = max(y…) - y_min`와 같이 계산하면 됩니다.

---

## 선택적 확장 기능

### 1. 바운딩 박스를 단순 사각형으로 변환

다운스트림 도구가 `(x, y, width, height)` 형식을 기대한다면 다음 헬퍼 함수를 추가하세요:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. 다페이지 PDF 처리

Aspose OCR은 PDF 스트림을 받아들일 수 있습니다. 이미지 로드 라인을 다음과 같이 교체하세요:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

각 페이지마다 `set_page_number`를 순회하면서 페이지별 좌표를 수집합니다.

### 3. 바운딩 박스 시각화

원본 이미지에 박스를 그려보고 싶다면 Pillow를 사용합니다:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

이제 인식된 모든 단어 주변에 빨간 윤곽선이 표시됩니다—디버깅이나 UI 오버레이에 최적입니다.

---

## 흔히 묻는 질문 및 주의사항

- **JSON이 너무 큰 경우?** 대용량 문서는 JSON을 스트리밍하거나 페이지별로 처리해 메모리 사용량을 낮추세요.  
- **일부 단어가 누락된 이유는?** 대비가 낮거나 손글씨인 경우 OCR 엔진이 인식하기 어렵습니다. 이미지 전처리(대비 증가, 이진화)를 수행한 뒤 다시 시도하세요.  
- **문자 수준 좌표도 가능한가?** 네— `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` 로 설정하면 `"characters"` 배열과 각각의 `boundingBox`를 받을 수 있습니다.  
- **좌표계는 0부터 시작하나요?** 네. (0, 0)은 이미지의 좌상단 코너를 의미합니다.

---

## 전체 스크립트 – 복사·실행 바로 가능

아래는 모든 단계를 하나로 합친 완전 실행 가능한 예제입니다. `extract_bboxes.py` 로 저장하고 `python extract_bboxes.py` 로 실행하세요.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 추가 API 기능을 마스터하고 다양한 구현 방식을 탐색할 수 있도록 단계별 코드 예제를 제공합니다.

- [Aspose OCR으로 이미지에서 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [이미지 인식에서 JSON 결과를 사용하기 위한 Aspose OCR 활용법](/ocr/english/net/text-recognition/get-result-as-json/)
- [OCR에서 사각형을 준비해 이미지에서 텍스트 추출하기](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
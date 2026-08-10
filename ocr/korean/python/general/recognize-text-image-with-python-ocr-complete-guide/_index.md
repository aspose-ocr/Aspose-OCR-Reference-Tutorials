---
category: general
date: 2026-06-28
description: Python OCR을 사용해 텍스트 이미지를 인식하고, 텍스트 PNG 파일을 추출하며, 견고한 오류 처리를 통해 인식된 텍스트를
  출력하는 방법을 배웁니다.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: ko
og_description: Python에서 텍스트 이미지를 인식하고, 텍스트 PNG를 추출하며, 인식된 텍스트를 안전하게 출력하는 단계별 튜토리얼.
og_title: Python OCR로 텍스트 이미지 인식 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python OCR로 텍스트 이미지 인식 – 완전 가이드
url: /ko/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR로 텍스트 이미지 인식 – 완전 가이드

무거운 프레임워크를 도입하지 않고 Python 스크립트에서 **텍스트 이미지 인식**을 할 수 있는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 스크린샷, 스캔한 영수증, 혹은 간단한 PNG와 같은 이미지를 *load image OCR* 하여 텍스트를 빠르게 추출하는 방법을 찾고 있습니다.  

이 튜토리얼에서는 최소한의 OCR 엔진을 연결하고, 커스텀 로거를 첨부한 뒤 **load image OCR**을 수행하고, **process image OCR**을 실행하며, 마지막으로 **print recognized text**를 출력하는 과정을 보여드립니다. 끝까지 따라오시면 필요에 따라 **extract text png** 파일을 추출할 수 있는 독립 실행형 스크립트를 만들 수 있습니다.

## What You’ll Walk Away With

- OCR 엔진을 생성하고, 모든 단계를 로깅하며, 오류를 우아하게 처리하는 완전한 Python 스니펫  
- 각 라인이 왜 중요한지에 대한 명확한 설명 – 이를 통해 Tesseract, EasyOCR 또는 다른 백엔드에 코드를 쉽게 적용 가능  
- 흔히 겪는 함정(폰트 누락, 손상된 PNG)과 디버깅 방법에 대한 팁  

### Prerequisites

- Python 3.8+ 설치  
- `OcrEngine` 클래스를 제공하는 OCR 라이브러리(예시에서는 가상의 API를 사용했으며, 실제로는 `pytesseract`, `easyocr` 등으로 교체)  
- 분석하고자 하는 PNG 이미지, `input.png` 라는 파일명으로 제어 가능한 폴더에 저장  

> **Pro tip:** `pytesseract`를 사용하는 경우 먼저 시스템에 Tesseract 바이너리를 설치(`sudo apt install tesseract-ocr` on Linux)하고, 이후 `pip install pytesseract pillow`를 실행하세요.

---

## ## Recognize Text Image: Setting Up the Logger

좋은 로거는 모든 OCR 파이프라인의 숨은 영웅입니다. 엔진이 언제 시작했는지, 어떤 파일을 열었는지, 왜 실패했는지를 알려줍니다.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Why this matters:*  
로거는 진단 출력을 OCR 핵심 로직과 분리시켜, 로그를 파일, 모니터링 서비스, 혹은 UI 등으로 손쉽게 리다이렉트할 수 있게 해줍니다.  

---

## ## Load Image OCR: Feeding the Engine a PNG

엔진이 **process image OCR**을 수행하기 전에 적절한 이미지 객체가 필요합니다. 대부분의 라이브러리는 Pillow `Image` 인스턴스를 받아들입니다.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Key points:*  

- **load image ocr** – `Image.from_file`은 PNG 디코딩 세부 사항을 추상화합니다.  
- 경로를 설정 가능하게 유지하세요; 하드코딩은 스크립트를 깨지기 쉬워집니다.  
- 로거 호출은 이미지가 성공적으로 읽혔는지 확인해 주며, 파일이 없거나 손상된 경우에 유용합니다.

---

## ## Process Image OCR: Recognizing the Text

이제 본격적인 작업이 시작됩니다. 엔진은 비트맵을 스캔하고, 신경망이나 휴리스틱을 적용해 Unicode 문자열을 반환합니다.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Why we wrap it in `try/except`:*  
OCR은 저해상도 PNG, 지원되지 않는 색 공간, 혹은 언어 데이터 누락 시 오류가 발생할 수 있습니다. `OcrException`을 잡아 **print recognized text**를 실제 텍스트가 존재할 때만 출력하도록 하면, 최종 사용자에게 불필요한 스택 트레이스를 보여주지 않을 수 있습니다.

---

## ## Print Recognized Text & Extract Text PNG

인식이 성공하면 결과를 화면에 표시하고, 원본 PNG 이름과 동일한 `.txt` 파일로 저장할 수 있습니다.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*What you get:*  

- **print recognized text** – 터미널에 즉시 시각적 피드백 제공  
- 원본 PNG와 나란히 생성되는 `.txt` 파일은 **extract text png** 작업을 위한 다운스트림 처리(검색 인덱싱, 데이터 입력 등)에 활용 가능

---

## ## Common Edge Cases & How to Tackle Them

| Situation | Symptom | Fix |
|-----------|---------|-----|
| PNG is grayscale only | OCR returns empty string | 엔진에 전달하기 전에 RGB로 변환 (`Image.convert("RGB")`) |
| Language not supported | `OcrException` with code `LANG_NOT_FOUND` | 해당 언어 팩 설치(예: 프랑스어는 `tesseract‑lang‑fra`) 후 `ocr_engine.language = "fra"` 설정 |
| Very large image ( > 5 MB ) | Slow recognition or memory error | `set_image` 전에 `image.thumbnail((2000, 2000))` 로 다운스케일 |
| Unexpected characters | Garbled output | 파일이 실제 PNG인지 확인; JPEG로 위장된 PNG가 있을 수 있음. `Image.verify()` 로 검증 |

---

## ## Full Working Example (Copy‑Paste Ready)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Expected console output (happy path):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

문제가 발생하면 커스텀 로거 덕분에 이유가 명시된 `[ERROR]` 라인이 표시됩니다.

---

## ## Next Steps & Related Topics

- 배치 처리 시 **extract text png**: 디렉터리 트리를 순회하는 `for` 루프로 스크립트를 감싸기  
- OpenCV를 활용한 전처리(디스큐, 대비 강화) 후 **process image ocr** 수행  
- `OcrEngine` 구현을 교체해 클라우드 OCR 서비스(Google Vision, Azure Read) 사용 – 주변 코드는 그대로 유지  
- `reportlab`을 이용해 **print recognized text**를 PDF로 저장, 자동 보고서 생성  

---

## Conclusion

우리는 Python에서 **recognize text image**를 수행하는 간결하고 프로덕션 수준의 방법을 살펴보았습니다. PNG 로드부터 **print recognized text** 출력 및 결과 저장까지, 작은 로거를 삽입하고 예외를 처리함으로써 빠른 실험과 대규모 파이프라인 모두에 적합한 스크립트를 만들 수 있습니다.

직접 스크린샷을 가지고 실행해 보고, 이미지 전처리를 실험해 보세요. 곧 모든 PNG에서 텍스트를 추출할 수 있게 될 것입니다. 질문이 있으면 댓글을 남겨 주세요—행복한 OCR 생활 되세요!  

![recognize text image example](placeholder.png)


## What Should You Learn Next?


다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하여 관련 주제를 심도 있게 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하므로, 추가 API 기능을 마스터하고 다양한 구현 방식을 프로젝트에 적용하는 데 도움이 됩니다.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-01-12
description: OCR을 빠르고 정확하게 수행하는 방법. 문서에서 OCR을 실행하고, TIFF에서 텍스트를 추출하며, OCR용 이미지를 로드하고,
  Python에서 OCR 언어를 설정하는 방법을 배웁니다.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: ko
og_description: Python에서 OCR을 수행하는 방법. 이 튜토리얼에서는 문서에 OCR을 실행하고, TIFF에서 텍스트를 추출하며,
  OCR을 위한 이미지를 로드하고 OCR 언어를 설정하는 방법을 보여줍니다.
og_title: TIFF 문서에서 OCR 수행 방법 – 완전 가이드
tags:
- OCR
- Python
- Image Processing
title: TIFF 문서에서 OCR 수행 방법 – 단계별 가이드
url: /ko/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF 문서에서 OCR 수행 방법 – 완전 가이드

올바른 라이브러리를 찾느라 시간을 보내지 않고 스캔한 TIFF 파일에서 **OCR 수행 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 특히 성능과 언어 설정이 중요한 경우 tiff 이미지에서 텍스트를 추출해야 할 때 벽에 부딪히곤 합니다.

이 튜토리얼에서는 OCR 패키지 설치, OCR을 위한 이미지 로드, OCR 언어 설정, 그리고 최종적으로 **문서에 OCR 실행**하여 깨끗한 텍스트를 추출하는 모든 과정을 단계별로 안내합니다. 끝까지 진행하면 어떤 프로젝트에든 바로 넣어 사용할 수 있는 실행 가능한 스크립트를 얻게 됩니다.

> **팁:** 예제에서는 일반적인 `ocr` 모듈을 사용하지만, 동일한 개념은 Tesseract, EasyOCR 또는 Python API를 제공하는 최신 OCR 엔진에도 적용됩니다.

---

## 필요한 사항

- Python 3.8+ (최근 버전이면 모두 사용 가능)
- `OcrEngine` 클래스를 제공하는 OCR 라이브러리 (예제에서는 가상의 `ocr` 패키지를 사용합니다; 실제 사용 중인 패키지로 교체하세요)
- 처리하려는 다중 페이지 TIFF 파일 (`big_document.tif` 라고 부르겠습니다)
- 스레드 수를 설정하려면 최소 4개의 CPU 코어를 가진 머신

외부 서비스나 클라우드 키가 필요 없습니다—몇 초 안에 실행되는 로컬 코드만 있습니다.

![TIFF 문서에서 OCR 수행 방법](/images/ocr-example.png "TIFF 문서에서 OCR 수행 방법")

*이미지 대체 텍스트: TIFF 문서에서 OCR 수행 방법 – 추출된 텍스트 미리보기.*

## 단계 1: OCR 라이브러리 설치 및 임포트

먼저, 라이브러리를 머신에 설치합니다. 대부분의 OCR 패키지는 PyPI에 있으므로 간단한 `pip install` 명령으로 설치할 수 있습니다.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

이제 필요한 클래스를 임포트합니다. Tesseract를 사용하는 경우 import 라인이 다르게 보일 수 있지만, 나머지 코드는 동일합니다.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*왜 중요한가:* 올바른 심볼을 미리 임포트하면 나중에 네임스페이스 충돌을 방지하고 스크립트를 더 읽기 쉽게 만들 수 있습니다.

## 단계 2: OCR 엔진 생성 및 구성 (OCR 언어 설정)

엔진을 구성하는 단계에서 정확한 인식을 위해 **OCR 언어를 설정**합니다. 기본은 영어이며, 한 줄로 프랑스어, 독일어 또는 다국어 모드로 전환할 수 있습니다.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **왜 4개의 스레드인가?** 대부분의 최신 노트북은 최소 4개의 코어를 가지고 있으며, 스레드 수를 제한하면 OCR 프로세스가 전체 머신을 독점하는 것을 방지합니다—특히 스크립트가 공유 서버에서 실행될 때 유용합니다.

다른 언어가 필요하면 `ocr.Language.ENGLISH`을 `ocr.Language.FRENCH`, `ocr.Language.SPANISH` 등으로 교체하면 됩니다.

## 단계 3: OCR을 위한 이미지 로드 (Load Image for OCR)

이제 **OCR을 위한 이미지를 로드**합니다. `Image.load` 메서드는 TIFF 파일을 메모리로 읽어 들이며, 다중 페이지 문서를 자동으로 처리합니다.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*예외 상황:* 파일이 매우 크면 RAM이 부족할 수 있습니다. 이 경우 `Image.load_page(page_number)`(라이브러리가 지원한다면)를 사용해 한 페이지씩 로드하는 것을 고려하세요.

## 단계 4: 문서에 OCR 실행

엔진이 준비되고 이미지가 로드되었으니 **문서에 OCR을 실행**할 차례입니다. `process` 메서드는 무거운 작업을 수행하고 결과 객체를 반환합니다.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

엔진은 내부적으로 이미지를 텍스트 블록으로 나누고, 인식 모델을 실행한 뒤 결과를 합칩니다. 이 호출은 블로킹 방식이므로 스크립트가 전체 TIFF가 처리될 때까지 대기합니다—배치 작업에 적합합니다.

## 단계 5: TIFF에서 텍스트 추출 및 출력 확인

마지막으로 결과 객체의 `text` 속성을 통해 **tiff에서 텍스트를 추출**합니다. 빠른 검증을 위해 처음 200자를 출력해 보겠습니다.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**예상 출력 (예시):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

전체 텍스트가 필요하면 `ocr_result.text`를 사용하면 됩니다. 후속 처리용으로 `.txt` 파일에 저장하고 싶다면 다음과 같이 할 수 있습니다:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

## 전체 작업 예시

모두 합치면 바로 실행 가능한 스크립트가 됩니다. 자리표시자 패키지 이름을 실제 설치한 패키지 이름으로 교체하세요.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

스크립트를 다음과 같이 실행합니다:

```bash
python ocr_tiff_example.py
```

콘솔에 미리보기가 출력되고, 전체 전사본이 들어 있는 `extracted_text.txt` 파일이 생성될 것입니다.

## 일반적인 질문 및 예외 상황

- **TIFF에 여러 페이지가 포함되어 있으면 어떻게 하나요?**  
  대부분의 OCR 엔진은 각 페이지를 내부적으로 별개의 이미지로 처리합니다. `ocr_result.text`에는 페이지 사이에 줄바꿈이 포함됩니다. 페이지별 처리가 필요하면 `Image.load_page(page_number)`를 사용해 반복하세요.

- **TIFF 대신 PNG나 JPEG를 처리할 수 있나요?**  
  물론 가능합니다. `Image.load` 메서드는 일반적으로 Pillow 또는 기반 라이브러리가 지원하는 모든 포맷을 받아들입니다. 파일 확장자를 바꾸기만 하면 됩니다.

- **텍스트가 깨져 보입니다—언어를 바꿔야 하나요?**  
  네. `set OCR language` 단계는 비영어 문서에 필수적입니다. 해당 언어 팩이 설치되어 있는지 확인하세요(예: 프랑스어는 `tesseract‑lang‑fra`).

- **메모리가 부족한 경우?**  
  `set_memory_limit`를 낮추거나 페이지를 하나씩 처리하세요. 일부 엔진은 인식 전에 이미지를 다운스케일할 수도 있습니다.

## 결론

이제 Python을 사용해 TIFF 파일에서 **OCR 수행 방법**에 대한 간결하고 완전한 가이드를 확인했습니다. 라이브러리 설치, 엔진 구성(**set OCR language** 포함), **OCR을 위한 이미지 로드**, **문서에 OCR 실행**, 그리고 마지막으로 **tiff에서 텍스트 추출**까지 모든 과정을 다루었습니다.

자유롭게 실험해 보세요: 스레드 수를 조정하고, 언어를 바꾸거나, OCR 결과를 자연어 처리 파이프라인에 연결할 수 있습니다. 기본을 마스터하면 가능성은 무한합니다.

추가 질문이 있나요? 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
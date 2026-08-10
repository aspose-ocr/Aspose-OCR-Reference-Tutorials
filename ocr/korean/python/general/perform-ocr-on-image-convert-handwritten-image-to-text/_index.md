---
category: general
date: 2026-03-18
description: 이미지에 OCR을 수행하고 사진에서 손글씨 텍스트를 추출합니다. 손글씨 이미지를 변환하고, JPG에서 텍스트를 추출하며, 사진에서
  텍스트를 인식하는 방법을 배워보세요.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: ko
og_description: 이미지에서 OCR을 수행하여 사진의 손글씨 텍스트를 추출합니다. 이 튜토리얼에서는 손글씨 이미지를 변환하고 jpg 파일에서
  텍스트를 인식하는 방법을 보여줍니다.
og_title: 이미지에서 OCR 수행 – 손글씨 완전 가이드
tags:
- OCR
- Python
- Handwriting Recognition
title: 이미지에서 OCR 수행 – 손글씨 이미지를 텍스트로 변환
url: /ko/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 OCR 수행 – 전체 스택 손글씨 텍스트 추출

손글씨가 섞인 **이미지에서 OCR을 수행**해야 하는데 엔진이 지저분한 필기를 읽을 수 있을지 고민해 본 적 있나요? 당신만 그런 것이 아닙니다. 실제 앱—예를 들어 영수증 스캐너나 메모 작성 도구—에서는 사진 속 낙서를 일반 텍스트로 변환해야 하는 경우가 많습니다.  

이 가이드에서는 작은 Python‑스타일 라이브러리 `ocr`를 사용해 **손글씨 이미지 파일을 변환**하고, **jpg에서 텍스트를 추출**하며, 심지어 **사진 스트림에서 텍스트를 인식**하는 방법을 보여드립니다. 끝까지 따라오면, 펜이 흔들리더라도 손글씨 메모에서 모든 단어를 추출하는 실행 가능한 스크립트를 얻게 됩니다.

## 준비물

- Python 3.8+ (최근 인터프리터라면 모두 동작)
- 가상의 `ocr` 패키지 – `pip install ocr-lib` 로 설치 (사용 중인 실제 패키지 이름으로 교체)
- `note.jpg` 로 저장된 손글씨 메모 사진 (다른 이미지 포맷도 가능)
- 약간의 호기심—고급 ML 지식은 필요 없습니다

그게 전부입니다. 외부 서비스나 API 키 없이, 로컬 엔진만으로 **이미지에서 OCR을 수행**할 수 있습니다.

![perform OCR on image screenshot](example.png)

*Alt text: OCR 스크립트가 보이는 코드 편집기 화면을 보여주는 이미지.*

## 단계별 구현

아래에서는 과정을 작은 조각으로 나눕니다. 각 헤더에는 키워드가 포함되어 있어 빠르게 스킵할 수 있고, 모든 블록은 **무엇을** 하는지뿐 아니라 **왜** 하는지를 설명합니다.

### 단계 1: OCR 라이브러리 설치 및 확인

**이미지에서 OCR을 수행**하려면 먼저 라이브러리가 환경에 있어야 합니다. 터미널을 열고 다음을 실행하세요:

```bash
pip install ocr-lib
```

> **팁:** 가상 환경(강력히 권장)에서 작업한다면 먼저 활성화하세요. 이렇게 하면 의존성을 깔끔하게 관리하고 버전 충돌을 피할 수 있습니다.

설치가 끝났으면 Python에서 패키지를 임포트할 수 있는지 확인합니다:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

성공 메시지가 보이면 **손글씨 이미지** 데이터를 처리할 준비가 된 것입니다.

### 단계 2: 엔진 인스턴스 생성 및 손글씨 모드 선택

대부분의 OCR 엔진은 기본적으로 인쇄 텍스트 인식을 사용합니다. **손글씨 텍스트를 추출**하려면 모드를 명시적으로 전환해야 합니다. 손글씨는 전처리(예: 획 부드럽게 하기)가 다르게 필요하기 때문에 이 단계가 중요합니다.

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*왜 중요한가:* 손글씨는 크기와 기울기가 크게 변동합니다. `RecognitionMode.HANDWRITTEN`을 설정하면 엔진이 필기 샘플로 학습된 모델을 적용해 정확도가 크게 향상됩니다.

### 단계 3: 분석할 사진 로드

이제 실제로 **이미지에서 OCR을 수행**합니다. `load_image` 메서드는 경로나 파일‑유사 객체를 받습니다. 예시로 JPEG를 로드하지만 PNG, BMP, 심지어 PDF 페이지도 동일하게 호출할 수 있습니다.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

이미지가 클라우드 버킷에 있다면 먼저 다운로드하거나 `BytesIO` 스트림을 전달하면 됩니다—`ocr`는 두 경우 모두 유연하게 처리합니다.

### 단계 4: 인식 프로세스 실행

엔진을 준비하고 이미지가 메모리에 로드되면, 마침내 **이미지에서 OCR을 수행**하고 원시 텍스트를 얻습니다.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

`recognize()` 호출은 일반 Unicode 문자열을 반환합니다. 대부분의 경우 바로 `.txt` 파일에 쓰거나, 자연어 파이프라인에 전달하거나, GUI에 표시하면 됩니다.

### 단계 5: 선택 – 출력 정리 또는 후처리

손글씨 OCR은 완벽하지 않으며, 종종 불필요한 줄바꿈이나 오인식 문자가 나타납니다. 간단한 정리 단계로 후속 결과를 개선할 수 있습니다.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

도메인에 따라 맞춤형 정규식, 언어 모델, 맞춤법 검사기를 연결해 보세요.

### 전체 스크립트 – 복사·붙여넣기용

모든 부분을 합치면 **손글씨 텍스트를 추출**하고 깔끔하게 출력하는 완전한 실행 프로그램이 됩니다.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**예상 출력**(실제 텍스트는 다를 수 있음):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

출력이 엉망이라면 이미지 품질(조명 충분, 흐림 최소)과 `HANDWRITTEN` 모드 설정을 다시 확인하세요. 이 두 요소가 대부분의 인식 오류를 차지합니다.

## 자주 묻는 질문 (FAQ)

| Question | Answer |
|----------|--------|
| **Can I use this to extract text from a PNG?** | Absolutely. `engine.load_image("scan.png")` works the same way. |
| **What if my image is a PDF page?** | Convert the page to an image first (e.g., with `pdf2image`) then feed it to the engine. |
| **Is the library thread‑safe?** | Yes, you can instantiate separate `OcrEngine` objects per thread. |
| **How does this differ from `pytesseract`?** | `ocr` abstracts away the Tesseract binary and includes a built‑in handwritten model, so you don’t need to install external executables. |
| **What if I need to **extract text from JPG** files in bulk?** | Wrap the script in a loop, or use `engine.load_image` on each file and collect results in a list or CSV. |

## 엣지 케이스 및 모범 사례

1. **Low‑contrast photos** – Increase contrast programmatically before loading, or use `engine.apply_preprocessing('contrast', level=2)`.
2. **Mixed printed & handwritten** – Run two passes: first with `HANDWRITTEN`, then with `PRINTED`, and merge the outputs.
3. **Large images** – Downscale to ~1500 px width; OCR engines usually perform faster with smaller buffers without losing accuracy.
4. **Unicode characters** – The library returns UTF‑8 strings, so you can handle emojis, accented letters, or mathematical symbols out of the box.

## 마무리

우리는 **이미지에서 OCR을 수행**하는 구체적인 예시를 살펴보았습니다. `ocr` 패키지를 설치하고, 엔진을 `HANDWRITTEN` 모드로 설정한 뒤, 사진을 로드하고 `recognize()`를 호출하면 **손글씨 이미지** 데이터를 깔끔하고 검색 가능한 텍스트로 변환할 수 있습니다.  

이제 **jpg에서 텍스트를 추출**하는 작업을 대량으로 수행하거나, 메모 앱에 결과를 연동하거나, 접근성을 위해 음성 합성에 연결하는 등 다양한 활용이 가능합니다. 위 코드는 실험을 위한 탄탄한 기반을 제공합니다.

다른 파일 포맷이나 독특한 전처리 팁을 공유하고 싶으신가요? 댓글로 알려 주세요. 계속해서 이야기를 나눠요. 즐거운 코딩 되시고, 낙서를 디지털 금으로 바꾸세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
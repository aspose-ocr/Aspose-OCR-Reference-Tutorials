---
category: general
date: 2026-07-05
description: Python OCR을 사용하여 이미지에서 텍스트를 추출합니다. 이미지에서 텍스트를 인식하고, OCR용 이미지를 로드하며, 몇
  줄만으로 OCR 언어를 설정하는 방법을 배워보세요.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: ko
og_description: Python OCR을 사용하여 이미지에서 텍스트를 추출합니다. 이 가이드는 이미지에서 텍스트를 인식하고, OCR을 위해
  이미지를 로드하며, Python 스타일로 OCR 엔진을 생성하고, OCR 언어를 설정하는 방법을 보여줍니다.
og_title: Python으로 이미지에서 텍스트 추출 – 텍스트를 빠르게 인식
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python으로 이미지에서 텍스트 추출 – 텍스트를 빠르게 인식
url: /ko/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 이미지에서 텍스트 추출 – 빠르게 텍스트 인식

이미지에서 **텍스트를 추출**해야 했지만 어떤 라이브러리를 골라야 할지 몰랐던 적이 있나요? 외부 도구를 사용하지 않고 *이미지에서 텍스트를 인식하는 방법*을 스스로 물어본 적이 있다면, 여기가 바로 맞는 곳입니다. 이 튜토리얼에서는 작은 OCR 엔진을 띄우고, 사진을 가리키며 텍스트를 추출합니다—그것만큼 간단합니다.

우리는 모든 단계를 차근차근 살펴볼 것입니다: **create OCR engine python**, **set OCR language**, **load image for OCR**, 비동기적으로 인식을 실행하고, 마지막으로 결과를 읽습니다. 끝까지 하면 문서 디지털화 도구든 밈을 읽는 챗봇이든 어떤 프로젝트에든 넣을 수 있는 독립 실행형 스크립트를 얻게 됩니다.

## 필요한 환경

- Python 3.8+ (코드는 3.10 및 그 이후 버전에서도 작동합니다)  
- `ocr` 패키지 (Tesseract의 얇은 래퍼 – `pip install ocr` 또는 선호하는 포크로 설치)  
- 읽을 수 있는 텍스트가 포함된 이미지 파일 (`.jpg`, `.png` 등)  
- 비동기 부분을 위한 약간의 인내심 (빠릅니다, 약속합니다)

그게 전부입니다—무거운 의존성도 없고, 네이티브 빌드도 필요 없습니다. 시스템에 Tesseract가 이미 설치되어 있다면 `ocr` 래퍼가 자동으로 찾아줍니다.

## Step 1: OCR 엔진 생성 – 추출의 핵심

먼저 해야 할 일은 기본 OCR 엔진과 통신할 수 있는 엔진 객체를 만드는 것입니다. 이를 나중에 이미지를 처리할 “뇌”라고 생각하면 됩니다.

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*왜 중요한가*: 엔진이 없으면 언어 설정이나 비동기 기능에 대한 컨텍스트가 없습니다. `OcrEngine` 클래스는 Tesseract에 대한 저수준 명령줄 호출을 추상화하여 깔끔한 Python API를 제공합니다.

## Step 2: OCR 언어 설정 – 엔진에 기대하는 언어를 알려주기

문서가 영어라면 기본값을 그대로 두어도 되지만, 명시적으로 설정하는 것이 좋은 습관입니다. 또한 다른 로케일에 대해 **OCR 언어 설정**하는 방법을 보여줍니다.

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **팁**: 다국어 PDF의 경우 `[ocr.Language.ENGLISH, ocr.Language.FRENCH]`와 같은 리스트를 전달할 수 있습니다. 엔진은 두 언어를 자동으로 시도합니다.

## Step 3: OCR용 이미지 로드 – 이미지를 메모리로 가져오기

이제 실제로 **OCR용 이미지를 로드**합니다. 래퍼는 지연 로딩을 지원하므로 엔진이 필요할 때까지 파일을 읽지 않습니다.

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*예외 상황*: 이미지가 매우 크면(5 MB 초과) 인식 속도를 높이기 위해 먼저 크기를 조정하는 것이 좋습니다. Pillow를 사용하면 다음과 같이 할 수 있습니다:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## Step 4: 비동기 인식 시작 – 앱을 차단하지 않기

OCR을 실행하는 데는 특히 큰 스캔일 경우 1~2초 정도 걸릴 수 있습니다. `recognize_async` 메서드는 나중에 폴링할 수 있는 future를 반환하여 **OCR이 백그라운드에서 실행되는 동안 다른 작업을 수행**할 수 있게 합니다.

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

왜 비동기인가? 웹 서버에서는 하나의 요청이 전체 워커 풀을 멈추게 하고 싶지 않습니다. future 객체를 사용하면 제어권을 얻을 수 있습니다: 비동기 코드에서는 `await`하고, 결과가 정말 필요할 때만 차단하면 됩니다.

## Step 5: 결과 가져오기 – 필요할 때만 차단

텍스트가 필요할 때 `future.get()`을 호출합니다. 이 호출은 **여기서만 차단**되므로 OCR이 끝날 때까지 프로그램의 나머지 부분은 응답성을 유지합니다.

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

`asyncio` 루프 안에 있다면 대신 `await future`를 사용할 수 있습니다 – 래퍼는 두 스타일을 모두 지원합니다.

## Step 6: 인식된 텍스트 사용 – 데이터가 준비되었습니다

`result` 객체를 얻었으니 순수 문자열을 추출하는 것은 간단합니다. 이를 출력하고 파일에 저장하는 방법도 보여드리겠습니다.

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**예상 출력** (간략히 표시):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

이미지에 텍스트가 없으면 `result.text`는 빈 문자열이 됩니다—이 경우를 부드럽게 처리하세요.

## 전체 작동 예제 – 한 스크립트에 모든 단계 포함

아래는 완전한 실행 가능한 프로그램입니다. 복사‑붙여넣기하고 `image_path`를 조정하면 바로 사용할 수 있습니다.

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **참고**: `"YOUR_DIRECTORY/large_document.jpg"`를 실제 이미지 경로로 교체하세요. Tesseract가 설치되어 `PATH`에 있으면 스크립트는 Windows, macOS, Linux 모두에서 작동합니다.

## 흔히 발생하는 문제와 해결 방법

| 문제 | 발생 원인 | 해결 방법 |
|------|----------|----------|
| **깨진 문자** | 잘못된 언어 설정 또는 언어 데이터 파일이 없을 때. | `engine.language`가 텍스트와 일치하는지, 그리고 해당 `.traineddata` 파일이 Tesseract의 `tessdata` 폴더에 존재하는지 확인하세요. |
| **큰 이미지에서 느린 성능** | OCR은 대략 픽셀 수에 비례해 처리 시간이 늘어납니다. | 엔진에 전달하기 전에 크기를 조정하거나 다운샘플링하세요 (Pillow 예제를 참고). |
| **Future가 해결되지 않음** | 이미지 파일이 손상되었거나 읽을 수 없습니다. | `future.get()`를 try/except 블록으로 감싸고 인식 전에 `image.is_valid()`를 검증하세요. |
| **Unicode 손실** |  |  |

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 보여준 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색할 수 있도록 돕습니다.

- [Aspose OCR을 사용한 이미지에서 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [이미지를 텍스트로 변환 – URL에서 이미지에 OCR 수행](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [이미지에서 텍스트 추출 – .NET용 Aspose OCR을 이용한 OCR 최적화](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
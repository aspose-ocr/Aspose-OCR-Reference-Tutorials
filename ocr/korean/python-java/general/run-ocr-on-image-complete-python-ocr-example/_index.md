---
category: general
date: 2026-03-18
description: Python으로 이미지를 빠르게 OCR하세요. PNG에서 텍스트를 인식하고, OCR을 위해 이미지를 로드하며, 단계별 가이드에서
  이미지에서 단어를 추출하는 방법을 배웁니다.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: ko
og_description: Python을 사용하여 이미지에서 OCR을 실행합니다. 이 튜토리얼에서는 PNG에서 텍스트를 인식하고, OCR을 위해
  이미지를 로드하며, 전체 코드 예제로 이미지에서 단어를 추출하는 방법을 보여줍니다.
og_title: 이미지에서 OCR 실행 – 파이썬 가이드
tags:
- OCR
- Python
- Image Processing
title: 이미지에서 OCR 실행 – 완전한 파이썬 OCR 예제
url: /ko/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 OCR 실행 – 완전한 Python OCR 예제

이미 **run OCR on image** 파일을 실행해야 했지만 어디서 시작해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다; 많은 개발자들이 스캔된 문서에서 텍스트를 추출하려고 할 때 처음 마주치는 장벽이 바로 이것입니다. 이 튜토리얼에서는 **Python OCR example**을 통해 **recognize text from PNG** 파일을 인식하고, **load image for OCR**을 수행하며, 신뢰도 점수와 함께 **extract words from image**를 몇 줄의 코드만으로 구현하는 방법을 단계별로 살펴보겠습니다.

필요한 라이브러리, 엔진 설정 방법, 각 단계가 왜 중요한지, 그리고 출력 결과가 어떻게 생겼는지를 모두 다룹니다. 끝까지 읽으면 이 스니펫을 자신의 프로젝트에 바로 복사해 넣어 어떤 이미지에서도 즉시 텍스트를 추출할 수 있습니다. 불필요한 내용은 없고, 실용적인 실행 가능한 솔루션만 제공합니다.

## 필요 사항

시작하기 전에 다음을 준비하세요:

- Python 3.8 이상 설치  
- `ocrengine` 패키지(또는 `OcrEngine` 클래스를 제공하는 라이브러리). `pip install ocrengine` 으로 설치할 수 있습니다 – 다른 OCR 라이브러리(`pytesseract` 등)를 사용하는 경우 이름을 조정하세요.  
- 처리하고자 하는 이미지 파일(PNG, JPG 등) – 이 가이드에서는 `invoice.png`를 사용합니다.  

그것만 있으면 됩니다. 무거운 의존성도 없고, 외부 서비스도 필요 없으며, 순수 Python만으로 가능합니다.

![run OCR on image example – scanned invoice being processed](/images/run-ocr-on-image.png)

*Alt text: run OCR on image 예제 – 스캔된 인보이스가 처리되는 모습*

## 단계 1 – OCR 라이브러리 설치 및 임포트

먼저 OCR 엔진을 환경에 설치하고 임포트합니다. 가상의 `ocrengine` 패키지를 사용하는 경우 임포트는 다음과 같습니다:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**왜 중요한가:** 올바른 클래스를 임포트하면 나중에 `setImageFromFile`과 `recognize` 같은 메서드를 사용할 수 있습니다. 이 단계를 건너뛰면 Python이 `ModuleNotFoundError`를 발생시키고, 이미지조차 로드하기 전에 막히게 됩니다.

## 단계 2 – OCR 엔진 인스턴스 생성

라이브러리가 준비되었으니, 인식 프로세스의 설정과 상태를 보관할 엔진 객체가 필요합니다.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*팁:* 일부 OCR 엔진은 이 시점에서 언어 모델이나 DPI 설정을 조정할 수 있습니다. 기본 **python OCR example**에서는 기본값으로 충분하지만, 저해상도 스캔을 다룰 경우 여기서 조정하는 것이 좋습니다.

## 단계 3 – 처리할 이미지 로드

다음 논리적인 단계는 **load image for OCR**입니다. 엔진에 PNG(또는 지원되는 형식)의 파일 경로를 지정하면 됩니다.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**무슨 일이 일어나고 있나요?** 엔진은 픽셀 데이터를 읽어 인식 알고리즘이 이해할 수 있는 형식으로 변환하고 내부에 저장합니다. 파일 경로가 잘못되면 `FileNotFoundError`가 발생하니 이미지가 존재하는지 반드시 확인하세요.

## 단계 4 – 인식 알고리즘 실행

이미지가 로드되었으니 이제 **run OCR on image**를 수행해 텍스트 내용을 추출합니다.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

## 단계 5 – 인식된 단어 반복 및 신뢰도 표시

OCR 워크플로우에서 가장 유용한 부분은 각 추출 토큰에 대한 **the confidence**를 확인하는 것입니다. 엔진이 각 단어에 대해 얼마나 확신하는지 알려주어, 필요에 따라 낮은 신뢰도의 결과를 필터링할 수 있습니다.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**예상 출력** (샘플):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

이제 이미지에서 **what words were extracted from the image**와 각 검출 결과의 신뢰도가 정확히 어떻게 되는지 확인할 수 있습니다. 이는 **extract words from image** 파이프라인의 핵심입니다.

## 일반적인 에지 케이스 처리

### 이미지가 그레이스케일인 경우는?

일부 OCR 엔진은 컬러 이미지에서 더 좋은 성능을 보입니다. 전체적으로 신뢰도가 낮게 나오면 PNG를 대비가 높은 흑백 버전으로 변환한 뒤 엔진에 전달해 보세요. Pillow가 도움이 됩니다:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### 다중 언어 처리

문서에 영어와 스페인어가 모두 포함된 경우, 다국어 모델을 사용해 **recognize text from PNG**를 수행해야 합니다. 대부분의 엔진은 초기화 시 언어 목록을 설정할 수 있습니다:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### 낮은 신뢰도 단어 필터링

때때로 신뢰도가 90 % 이상인 단어만 필요할 때가 있습니다. 간단한 필터는 다음과 같습니다:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## 전체 실행 가능한 스크립트

모든 내용을 하나로 합치면, 바로 복사·붙여넣기해서 실행할 수 있는 단일 스크립트가 됩니다(경로만 자신의 PNG로 교체하면 됩니다).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

다음과 같이 실행합니다:

```bash
python run_ocr_on_image.py
```

콘솔에 단어 목록과 신뢰도 퍼센트가 이전에 보여준 대로 출력될 것입니다.

## 자주 묻는 질문

**Does this work with JPG or TIFF files?**  
Absolutely. The `setImageFromFile` method accepts any format the underlying library can decode, so you can **run OCR on image** files of type JPG, TIFF, BMP, etc.

**Can I process multiple images in a loop?**  
Sure thing. Wrap the loading and recognition steps inside a `for` loop over a list of file paths. Just remember to re‑initialize the engine if the library requires a fresh instance per image.

**What if I need the text in a single string instead of per‑word?**  
Most OCR result objects expose a `getText()` method that returns the whole document. Example:

```python
full_text = ocr_result.getText()
print(full_text)
```

## 다음 단계 및 관련 주제

이제 **run OCR on image** 방법을 알았으니, 다음을 탐색해 보세요:

- **Post‑processing**: 정규식을 사용해 인보이스에서 추출한 날짜, 금액, ID 등을 정리합니다.  
- **Batch processing**: `os.listdir()`와 결합해 스캔된 문서가 들어있는 전체 폴더를 처리합니다.  
- **Alternative libraries**: `pytesseract`는 널리 사용되는 오픈소스 옵션이며, 워크플로우는 유사합니다—엔진 호출만 교체하면 됩니다.  
- **Exporting results**: 추출된 단어와 신뢰도 점수를 CSV로 저장해 후속 분석에 활용합니다.  

이러한 확장은 여기서 만든 기반 위에 직접적으로 쌓이며, 원시 OCR 데이터를 실용적인 정보로 전환할 수 있게 해줍니다.

---

### TL;DR

우리는 **python OCR example**을 통해 **load image for OCR**, **run OCR on image**, 그리고 **extract words from image**를 신뢰도와 함께 보고하는 간결한 예제를 보여주었습니다. 전체 스크립트는 바로 실행할 수 있으며, 이제 **recognize text from PNG**(또는 다른 형식) 작업이 필요한 어떤 프로젝트에도 적용할 수 있는 지식을 갖추었습니다. 한 번 실행해 보고, 신뢰도 임계값을 조정해 보세요. 몇 분 안에 애플리케이션이 텍스트를 인식하도록 만들 수 있습니다. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
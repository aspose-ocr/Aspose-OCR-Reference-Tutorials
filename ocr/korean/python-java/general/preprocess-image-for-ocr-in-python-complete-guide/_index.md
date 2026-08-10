---
category: general
date: 2026-06-25
description: Python을 사용하여 OCR을 위한 이미지 전처리 및 스캔 문서에서 텍스트 인식. 전체 코드를 포함한 단계별 튜토리얼.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: ko
og_description: Python을 사용해 OCR용 이미지 전처리 및 스캔 문서에서 텍스트 인식하기. 자세하고 실행 가능한 튜토리얼을 따라보세요.
og_title: Python에서 OCR을 위한 이미지 전처리 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python에서 OCR을 위한 이미지 전처리 – 완전 가이드
url: /ko/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 OCR을 위한 이미지 전처리 – 완전 가이드

스캔한 페이지가 비뚤어져 있거나 대비가 고르지 않을 때 텍스트가 깨끗하고 신뢰할 수 있게 나오도록 **이미지를 OCR용으로 전처리**하는 방법이 궁금하셨나요? 여러분만 그런 것이 아닙니다—대부분의 개발자가 같은 문제에 부딪힙니다. 좋은 소식은 몇 줄의 Python 코드만으로 그 혼란을 바로잡고, 이미지를 이진화하며, 선명하고 검색 가능한 텍스트를 얻을 수 있다는 점입니다.

이 튜토리얼에서는 **이미지를 OCR용으로 전처리**하고 *스캔한 문서 파일에서 텍스트를 인식*하는 정확한 단계를 살펴봅니다. 끝까지 따라오시면 바로 실행 가능한 스크립트를 얻고, 각 설정이 왜 중요한지 이해하며, 까다로운 경우에 어떻게 조정해야 하는지도 알게 됩니다.

## 준비물

- Python 3.8 이상 (코드는 3.10+에서도 동작)
- `OcrEngine`, `ImagePreProcessingOptions`, `Image` 클래스를 제공하는 OCR 패키지 (예시에서는 가상의 `ocr` 모듈 사용)
- 약간 기울어졌거나 대비가 낮은 스캔 혹은 사진 문서
- 좋아하는 IDE 또는 간단한 터미널—무거운 GUI는 필요 없음

그게 전부입니다. 별도의 바이너리나 Docker 설정도 필요 없습니다. 바로 시작해봅시다.

## OCR용 이미지 전처리 – 단계별 가이드

아래는 핵심 워크플로를 다섯 단계로 나눈 것입니다. 각 단계마다 **왜** 하는지, 정확한 **코드**, 그리고 내부에서 무슨 일이 일어나는지에 대한 짧은 **설명**이 포함됩니다.

### 단계 1: OCR 엔진 인스턴스 생성

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*왜 중요한가:*  
`OcrEngine` 객체는 전체 작업의 두뇌 역할을 합니다. 언어 팩, 신뢰도 임계값, 그리고 가장 중요한 이미지 전처리 플래그와 같은 설정을 보관합니다. 먼저 인스턴스를 만들면 이후에 적용할 트릭들을 깨끗한 상태에서 사용할 수 있습니다.

### 단계 2: 자동 디스큐 및 이진화 활성화

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*왜 중요한가:*  
- **디스큐**는 이미지의 텍스트 라인이 수평이 되도록 회전시킵니다. 기준선이 몇 도 이상 기울어지면 OCR 엔진이 제대로 인식하지 못합니다.  
- **이진화**는 사진을 순수한 흑백으로 변환해 배경 잡음을 제거합니다. 이는 문자 분류기를 혼란스럽게 할 수 있는 요소를 없애줍니다.  
두 옵션 모두 최신 라이브러리에서는 *자동*이지만, 명시적으로 켜야 합니다.

> **팁:** 원본 이미지가 이미 완벽히 정렬돼 있다면 `auto_deskew=False` 로 설정해 처리 시간을 약간 절약할 수 있습니다.

### 단계 3: 처리할 기울어진 이미지 로드

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*왜 중요한가:*  
`Image.load` 메서드는 파일을 메모리로 읽어 OCR 엔진이 이해할 수 있는 객체로 감싸줍니다. 또한 DPI와 같은 메타데이터를 추출하는데, 이는 디스큐 시 기본 스케일링 팩터에 영향을 줄 수 있습니다.

> **예외 상황:** 이미지가 다중 페이지 TIFF인 경우 각 페이지를 순회하거나 `ocr.MultiPageImage.load` 같은 도우미를 사용해야 합니다. 전처리 설정은 모든 페이지에 동일하게 적용됩니다.

### 단계 4: 전처리된 이미지에 OCR 수행

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*왜 중요한가:*  
이 시점에서 엔진은 앞서 활성화한 디스큐와 이진화 단계를 적용한 뒤, 정제된 비트맵에 신경망(또는 고전적인 Tesseract‑스타일 파이프라인)을 실행합니다. 반환된 `result` 객체에는 일반 텍스트, 신뢰도 점수, 경우에 따라 각 단어의 위치 데이터가 포함됩니다.

> **텍스트가 여전히 깨져 보이나요?**  
이미지 해상도를 확인하세요: OCR은 300 dpi 이상에서 가장 잘 동작합니다. 원본 해상도가 낮다면 로드하기 전에 업스케일링을 고려하거나 원본 스캔을 요청하세요.

### 단계 5: 인식된 텍스트 출력

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*왜 중요한가:*  
`result.text`는 엔진이 읽어낸 모든 내용을 담은 일반 문자열입니다. 빠른 디버깅을 위해 콘솔에 출력하는 것이 편리하지만, 실제 애플리케이션에서는 `.txt` 파일, 데이터베이스, 혹은 후속 NLP 파이프라인에 전달하는 것이 일반적입니다.

---

## 스캔 문서에서 텍스트 인식 – 기본을 넘어서는 활용

기본 파이프라인이 동작한다면, 실제 환경에서 **스캔 문서에서 텍스트를 인식**할 때 마주칠 수 있는 몇 가지 흔한 변형을 살펴보겠습니다.

### 1. 다국어 처리

문서에 영어와 프랑스어가 섞여 있다면, 단계 1 전에 엔진을 다음과 같이 설정합니다:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

대부분의 OCR 엔진은 ISO‑639‑2 코드를 사용합니다; 추가 언어 팩을 로드하면 약간의 오버헤드가 발생하지만 다국어 페이지에서 정확도가 크게 향상됩니다.

### 2. 이진화 임계값 미세 조정

자동 이진화가 대부분의 경우에 잘 동작하지만, 오래된 복사본은 사용자 정의 임계값이 필요합니다:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

배경이 사라지면서 희미한 문자까지 지워지지 않도록 120 ~ 220 사이의 값을 실험해 보세요.

### 3. 레이아웃 정보 추출

단순 텍스트뿐 아니라 각 단락이 페이지 어디에 위치하는지 알고 싶을 때가 있습니다. 많은 엔진이 `result.blocks` 컬렉션을 제공합니다:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

표를 재구성하거나 컬럼 순서를 유지하는 데 매우 유용합니다.

### 4. 파일 배치 처리

스캔한 PDF를 JPEG로 변환한 파일이 폴더에 가득 있다면, 전체 흐름을 루프로 감쌀 수 있습니다:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

루프는 동일한 `engine` 인스턴스를 재사용하므로 파일마다 새로 생성하는 것보다 효율적입니다.

### 5. 저해상도 스캔 대응

해상도가 150 dpi 미만인 이미지는 흐릿한 문자를 만들기 쉽습니다. 빠른 해결책은 고품질 알고리즘으로 업스케일링한 뒤 OCR 엔진에 전달하는 것입니다:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

업스케일링이 디테일을 마법처럼 만들지는 않지만, 이진화 단계가 더 선명한 가장자리를 활용할 수 있어 약간의 성능 향상이 있습니다.

---

## 기대 출력

중간 정도로 기울어지고 300 dpi인 스캔에 원본 5단계 스크립트를 실행하면 다음과 같은 결과가 콘솔에 출력됩니다:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

문자가 깨져 보이면 전처리 플래그, 이미지 해상도, 언어 설정을 다시 확인하세요.

---

## 결론

Python을 사용해 **이미지를 OCR용으로 전처리**하고 **스캔 문서에서 텍스트를 인식**하는 데 필요한 모든 과정을 다루었습니다. 새 엔진 인스턴스를 만들고 자동 디스큐와 이진화를 활성화한 뒤, 기울어진 이미지를 로드하고 인식을 수행해 깨끗한 텍스트를 출력했습니다. 또한 다국어 지원, 수동 임계값 조정, 레이아웃 추출, 배치 처리, 저해상도 보정 방법도 살펴보았습니다.

직접 영수증, 손글씨 양식, 오래된 신문 스캔 등으로 스크립트를 실행해 보세요. 익숙해지면 PDF 생성이나 검색 인덱스로 결과를 전달하는 단계까지 확장해 볼 수 있습니다. 가능성은 무한합니다.

**다음 도전 과제가 준비되셨나요?** *“Python으로 스캔 PDF에서 표 추출”* 및 *“TensorFlow로 맞춤 OCR 모델 학습”* 튜토리얼을 확인해 문서 자동화 도구 상자를 더욱 확장해 보세요.

행복한 코딩 되시고, OCR이 언제나 선명하길 바랍니다!


## 다음에 배울 내용은 무엇인가요?


다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하여 밀접하게 연관된 주제를 다룹니다. 각 자료는 단계별 설명과 완전한 코드 예제를 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Aspose OCR으로 이미지에서 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR for .NET을 활용한 OCR 최적화](/ocr/english/net/ocr-optimization/)
- [AspOCR 사용법: .NET용 이미지 전처리 OCR 필터](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
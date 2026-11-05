---
category: general
date: 2026-03-26
description: 이미지를 왜곡 보정하는 방법, 이미지에서 텍스트를 인식하는 방법, 스캔에서 노이즈를 제거하고 스캔된 이미지를 텍스트로 변환하는
  이미지 전처리 파이프라인을 구축하는 방법을 배워보세요.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: ko
og_description: 이미지를 바로잡고 기울어진 스캔을 검색 가능한 텍스트로 변환하는 방법. 이 가이드를 따라 이미지에서 텍스트를 인식하고,
  스캔의 노이즈를 제거하며, 스캔한 이미지를 텍스트로 변환하세요.
og_title: 이미지 기울기 보정 방법 – 단계별 OCR 가이드
tags:
- OCR
- image-processing
- Python
title: 이미지 기울기 보정 방법 – OCR 완전 가이드
url: /ko/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지 기울기 보정 방법 – OCR 완전 가이드

저렴한 스캐너에서 나온 이미지를 **how to deskew image**(이미지 기울기 보정) 해야 할지 궁금했던 적 있나요? 당신만 그런 것이 아닙니다. 구부러진 페이지는 비전문적으로 보이며, 무엇보다도 기울기가 **recognize text from image**(이미지에서 텍스트 인식)하려는 OCR 엔진의 정확도를 떨어뜨릴 수 있습니다.  

이 튜토리얼에서는 스캔을 기울기 보정하고, 이진화하며, 노이즈를 제거하는 전체 **image preprocessing pipeline**(이미지 전처리 파이프라인)을 단계별로 살펴보고, 이를 OCR 엔진에 전달하여 **convert scanned image to text**(스캔 이미지에서 텍스트 변환)를 최소한의 노력으로 수행하는 방법을 안내합니다. 마법이 아니라 순수 파이썬과 무거운 작업을 대신해 주는 작은 라이브러리만 있으면 됩니다.

## 필요 사항

- Python 3.9+ (코드는 3.10 및 최신 버전에서도 작동합니다)
- `ocr` 패키지 (`pip install ocr‑toolkit` 로 설치 – 실제 사용 라이브러리 이름으로 교체하세요)
- 눈에 띄게 기울어진 스캔된 JPEG 또는 PNG 파일 (예: `skewed_scan.jpg`)
- 각 전처리 단계가 왜 중요한지에 대한 약간의 호기심

이것만 있으면 됩니다. 나중에 더 깊이 파고들고 싶지 않은 한 OpenCV 같은 무거운 의존성은 필요하지 않습니다.

## 단계 1: 스캔 이미지 로드

첫 번째 작업은 파일을 메모리로 불러오는 것입니다. 이 단계는 간단하지만 매우 중요합니다—경로가 잘못되면 이후 모든 작업이 실패합니다.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Why?**  
> 이미지를 로드하면 `ocr.ImagePreprocessor`가 작업할 수 있는 조작 가능한 객체를 얻을 수 있습니다. 이 단계를 건너뛰면 파이프라인이 실제 픽셀 데이터를 알 수 없게 됩니다.

## 이미지 기울기 보정 및 OCR 준비 방법

이제 이미지를 가지고 있으니 바로 잡아 보겠습니다. `deskew()` 메서드는 기울기 각도를 추정하고 사진을 수평으로 회전시킵니다.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Pro tip:** 스캔이 **조금만** 기울어져 있다면 (≤ 3°) 기본 알고리즘이 보통 **정확히** 작동합니다. **극단적인** 각도일 경우 내부 파라미터를 조정해야 할 수도 있으니 `max_angle`에 대한 라이브러리 문서를 확인하세요.

## 이미지 이진화 – 흑백 만들기

OCR 엔진은 고대비 입력을 선호합니다. 사진을 이진(흑백) 형태로 변환하면 문자 인식을 방해할 수 있는 미묘한 색조가 사라집니다.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **What’s happening?**  
> 밝기가 128보다 큰 픽셀은 흰색이 되고, 그 외는 모두 검은색이 됩니다. 스캔이 비정상적으로 어둡거나 밝다면 임계값을 조정하세요.

## OCR 전 스캔 노이즈 제거

완벽하게 기울기 보정된 이미지라도 작은 점, 먼지, 압축 아티팩트가 남아 있을 수 있습니다. 이러한 작은 잡음은 OCR 엔진의 적이다.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Why remove noise?**  
> 노이즈는 OCR 엔진이 문자로 오인할 수 있는 잘못된 경계를 만들게 합니다. 대부분의 스캔에서는 작은 반경이 충분하지만, 매우 거친 문서의 경우 반경을 늘려 주세요.

## 이미지 전처리 파이프라인 적용

모든 설정이 완료되었습니다—이제 원본 이미지에 파이프라인을 실행합니다.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Result:** `processed_image`는 텍스트 추출을 위해 준비된, 깨끗하고 직선이며 고대비인 비트맵입니다.

## OCR 엔진으로 이미지에서 텍스트 인식

이제 실제로 텍스트를 읽어볼 차례입니다. OCR 엔진을 초기화하고, 다듬은 이미지를 전달한 뒤 원시 문자열을 요청합니다.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Expected output** (sample):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

문자가 깨져 보이면, 기울기 보정 단계를 다시 확인하거나 다른 `threshold` 값을 실험해 보세요.

## 이미지 전처리 파이프라인 구축 – 전체 스크립트

모든 내용을 하나로 합치면, `.py` 파일에 붙여 실행할 수 있는 단일 스크립트가 됩니다:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Tip:** 여러 파일을 배치 처리하려면 전체 코드를 `def ocr_from_file(path): …` 형태의 함수로 감싸세요.

## 흔히 묻는 질문 및 엣지 케이스

- **이미지가 이미 바로 서 있다면?**  
  `deskew()` 메서드는 거의 0도에 가까운 각도를 감지하고 이미지를 그대로 두므로, 모든 파일에 안전하게 적용할 수 있습니다.

- **스캔이 컬러인데 그대로 두어야 할까요?**  
  대부분의 OCR 작업에서는 색상이 **가치**를 제공하지 않습니다. 이진화 과정에서 색상이 제거되어 처리 속도가 빨라지고 메모리 사용량도 감소합니다.

- **여러 전처리 단계를 연쇄할 수 있나요?**  
  물론 가능합니다. `ImagePreprocessor` 클래스는 파이프라인을 위해 설계되었으며, `apply()`를 호출하기 전에 `sharpen()`, `contrast_enhance()` 또는 사용자 정의 **filters**를 추가할 수 있습니다.

- **OCR 출력에 불필요한 줄 바꿈이 있으면 어떻게 고치나요?**  
  `text.replace("\n", " ").strip()` 로 문자열을 후처리하거나, Tesseract의 `--psm` 모드와 같은 고급 레이아웃 분석 라이브러리를 사용하세요.

## 다음 단계

이제 **how to deskew image**(이미지 기울기 보정) 방법과 견고한 **image preprocessing pipeline**(이미지 전처리 파이프라인)을 알게 되었으니, 다음을 시도해 볼 수 있습니다:

- **recognize text from image**(이미지에서 텍스트 인식)를 Flask API에 통합하여 실시간 문서 업로드를 처리하기
- 역사적 문서의 **remove noise from scan**(스캔 노이즈 제거) 파이프라인을 활용해 보존 작업을 지원하기
- 수천 페이지를 배치 처리하고 `pdfminer` 또는 `PyMuPDF`를 사용해 검색 가능한 PDF로 출력하기

다양한 임계값, 노이즈 제거 반경을 실험하거나, 다국어 지원이 필요하면 OCR 백엔드를 Tesseract로 교체해 보세요. 기본 흐름은 변하지 않습니다: 바로 잡고, 깨끗하게 만들고, 읽어내기.

---

*Happy coding! If you run into trouble, drop a comment below—I'll be glad to help you fine‑tune the pipeline.*  
*코딩 즐겁게! 문제가 발생하면 아래에 댓글을 남겨 주세요—파이프라인을 미세 조정하는 데 기꺼이 도와드리겠습니다.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
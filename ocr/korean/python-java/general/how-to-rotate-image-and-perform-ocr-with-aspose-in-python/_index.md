---
category: general
date: 2026-03-26
description: Python에서 이미지를 회전하고 OCR을 수행하는 방법을 배웁니다. 이 가이드는 OCR을 위한 이미지 전처리 방법과 이미지를
  효율적으로 텍스트로 추출하는 방법도 보여줍니다.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: ko
og_description: Aspose OCR을 사용하여 이미지를 올바르게 회전하고 이미지에서 텍스트를 인식하는 방법. OCR을 위한 이미지 전처리와
  이미지에서 텍스트를 추출하는 단계별 튜토리얼을 따라보세요.
og_title: 이미지를 회전하고 OCR 수행하기 – 완전한 파이썬 가이드
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Python에서 Aspose를 사용하여 이미지 회전 및 OCR 수행 방법
url: /ko/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 Aspose로 이미지 회전 및 OCR 수행 방법

이미지를 **회전**해서 OCR 엔진이 실제로 텍스트를 읽을 수 있게 만든 적 있나요? 양식을 스캔했는데 옆으로 눕혀졌거나, 카메라 촬영이 시계 방향으로 90° 회전된 경우일 수 있습니다. 사람 눈에는 텍스트가 정상적으로 보이지만 OCR 엔진은 엉망이 됩니다. 좋은 소식은, 몇 줄의 Python 코드와 Aspose 라이브러리만으로 방향을 바로잡고, 관심 영역을 잘라낸 뒤 텍스트를 추출하는 것이 아주 간단하다는 것입니다.

이 튜토리얼에서는 전체 워크플로우를 단계별로 살펴봅니다: 회전된 TIFF 로드, 방향 교정, **OCR을 위한 이미지 전처리**, 그리고 최종적으로 **이미지에서 텍스트 인식**까지. 끝까지 따라오면 **OCR 수행 방법**과 **이미지에서 텍스트 추출**을 자신 있게 할 수 있게 됩니다.

## 준비 사항

- Python 3.8+ (최근 버전이면 모두 동작)
- `asposeocrjava` 및 `asposeimaging` 패키지를 `pip`으로 설치
- 회전이 필요한 샘플 이미지 (예: `rotated_form.tif`)
- 이미지 처리에 대한 약간의 호기심

무거운 프레임워크는 필요 없습니다—Aspose 두 패키지와 약간의 Python 로직만 있으면 됩니다.

---

## Step 1: Aspose 패키지 설치 (How to Perform OCR)

**이미지를 회전**하거나 **이미지에서 텍스트를 인식**하기 전에 실제 작업을 수행하는 라이브러리를 설치해야 합니다.

```bash
pip install asposeocrjava asposeimaging
```

> **Pro tip:** 기업 프록시 뒤에 있을 경우 `--proxy http://proxy:port` 옵션을 명령에 추가하세요. 이 패키지는 Aspose .NET/Java 코어를 감싼 순수 Python 래퍼이므로 설치가 거의 즉시 완료됩니다.

---

## Step 2: 원본 파일 로드 및 회전 – 핵심 “How to Rotate Image” 단계

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **왜 회전하나요?** 대부분의 OCR 엔진은 텍스트가 왼쪽‑오른쪽, 위‑아래 순서로 배치된다고 가정합니다. 비트맵이 옆으로 눕혀져 있으면 엔진은 의미 없는 문자열을 반환하거나 아무 것도 반환하지 못합니다. 회전을 통해 픽셀 그리드를 기대하는 읽기 순서에 맞추면 정확도가 크게 향상됩니다.

> **예외 상황:** 이미지가 90°, 180°, 270° 중 어느 각도로 회전해야 할지 모를 경우 `source_image.width`와 `source_image.height`를 비교하거나 `exif` 방향 태그를 확인하세요. Aspose의 `rotate_flip` 메서드는 `ROTATE_180` 및 `ROTATE_270_CLOCKWISE`도 지원합니다.

> **이미지 미리보기 (선택):**  
> ![이미지 회전 예시](/assets/rotate-demo.png "이미지 회전 – 회전 전후 비교")

---

## Step 3: 관심 영역 자르기 – OCR을 위한 이미지 전처리

페이지의 일부분만 필요할 때가 많습니다—예를 들어 서명란이나 숫자 블록 등. 크롭을 하면 잡음이 제거되고 **OCR 수행 방법**이 빨라집니다.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **왜 크롭하나요?** 이미지 크기를 줄이면 OCR 엔진이 탐색해야 할 영역이 감소해 오탐이 줄고 처리 시간이 단축됩니다. 또한 원본 파일에 워터마크나 기타 그래픽이 포함돼 엔진을 혼란스럽게 할 경우에도 도움이 됩니다.

> **팁:** 여러 필드를 다루는 경우 서로 다른 사각형으로 크롭을 반복하고 각각에 대해 OCR을 실행하세요.

---

## Step 4: OCR 엔진 초기화 – “How to Perform OCR” 핵심

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **내부 동작:** Aspose OCR은 Tesseract와 자체 이미지 분석 기술을 결합합니다. 엔진을 한 번 인스턴스화하고 여러 이미지에 재사용하는 것이 매번 새 객체를 만드는 것보다 효율적입니다.

---

## Step 5: 크롭된 이미지 전달 및 텍스트 인식 – How to Extract Text from Image

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### 예상 출력

ROI에 “Invoice #12345 – Paid”라는 문구가 포함되어 있으면 다음과 같은 결과가 나타납니다:

```
Invoice #12345 – Paid
```

OCR이 어려움을 겪는 경우 불필요한 공백이나 잘못 인식된 문자(예: “Invo1ce #I2345 – Pa1d”)가 나올 수 있습니다. 이때 **OCR을 위한 이미지 전처리** 기법—예를 들어 대비 조정이나 이진화 적용—이 도움이 됩니다. Aspose는 단계 5 전에 체인할 수 있는 추가 필터를 제공하지만, 기본 흐름만으로도 대부분의 깨끗한 스캔에 충분합니다.

---

## Step 6: 선택 – OCR 설정 세부 조정 (Advanced “How to Perform OCR”)

특정 언어에 대한 정확도를 높이거나 특정 문자를 무시하고 싶다면 엔진을 조정할 수 있습니다:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **사용 시점:** 문서에 무시해도 되는 장식 기호가 많이 포함된 경우에 활용하세요. 블랙리스트를 지정하면 오탐을 줄일 수 있습니다.

---

## 전체 End‑to‑End 스크립트

모든 단계를 하나로 합치면 **이미지 회전**, **OCR을 위한 이미지 전처리**, 그리고 최종적으로 **이미지에서 텍스트 인식**을 수행하는 실행 가능한 스크립트가 됩니다:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

이 스크립트를 실행하면 인식된 텍스트가 콘솔에 출력되고, 처리된 ROI를 `processed_roi.png` 파일로 저장합니다. 해당 PNG를 열어 회전 및 크롭이 정상적으로 적용됐는지 확인할 수 있습니다.

---

## 흔히 묻는 질문 & 주의사항

| Question | Answer |
|----------|--------|
| **이미지가 이미 올바른 방향이라면 어떻게 하나요?** | 회전 단계는 멱등성을 갖습니다—올바른 방향의 이미지를 90° 회전하면 오히려 깨지므로 `source_image.width`와 `height`를 확인하거나 EXIF 방향 데이터를 사용해 회전을 수행하기 전에 판단해야 합니다. |
| **OCR 결과에 불필요한 줄 바꿈이 포함됩니다.** | `result.get_text().replace("\n", " ").strip()` 로 정리하거나 `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)` 를 활성화하세요. |
| **PDF를 직접 처리할 수 있나요?** | 가능합니다—Aspose Imaging은 PDF 페이지를 이미지(`Image.load("file.pdf")`)로 로드할 수 있으며, 이후 동일한 회전 및 OCR 단계를 적용하면 됩니다. |
| **다수 파일을 배치 처리하려면?** | 디렉터리를 순회하면서 `ocr_rotated_image` 를 호출하거나 Python의 `concurrent.futures` 로 병렬화하면 됩니다. |
| **영어 외 다른 언어를 처리하려면?** | `ocr_engine.get_recognition_settings().set_recognition_language("fr")` 와 같이 인식 언어를 설정하면 프랑스어 등 다른 언어도 지원됩니다. |

---

## 결론

우리는 **이미지 회전**을 정확히 수행하고, **OCR을 위한 이미지 전처리**로 크롭을 적용한 뒤, **이미지에서 텍스트 인식**과 **이미지에서 텍스트 추출**을 Aspose Python 라이브러리로 구현하는 방법을 살펴보았습니다. 완전한 스크립트는 실무에 바로 적용 가능한 워크플로우를 보여주며, 자동화 파이프라인에 쉽게 삽입할 수 있습니다.

다음 단계로 시도해 볼 수 있는 내용:

- OCR 전 **이미지 향상**(대비, 이진화) 적용
- 여러 ROI를 추출해 폼의 여러 필드 처리
- 스캔 문서 전체 폴더에 대한 **배치 처리**
- 추출된 데이터를 데이터베이스 등 **다운스트림 시스템**에 연동

코드를 자신의 상황에 맞게 자유롭게 변형하고, 즐거운 코딩 되세요! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
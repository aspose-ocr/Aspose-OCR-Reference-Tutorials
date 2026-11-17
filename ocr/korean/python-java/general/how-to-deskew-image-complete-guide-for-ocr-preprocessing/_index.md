---
category: general
date: 2026-07-05
description: 이미지를 빠르게 기울기 보정하는 방법. OCR을 위한 이미지 전처리, 이미지 회전 보정, 그리고 Python으로 스캔을 텍스트로
  변환하는 방법을 배워보세요.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: ko
og_description: 이미지를 디스큐하고 OCR을 위한 전처리 방법. 이 가이드는 이미지 회전을 교정하고 Python을 사용해 이미지에서 텍스트를
  추출하는 방법을 보여줍니다.
og_title: 이미지 기울기 보정 방법 – 단계별 OCR 전처리
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: 이미지 기울기 보정 방법 – OCR 전처리를 위한 완벽 가이드
url: /ko/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지 기울기 보정 방법 – OCR 전처리를 위한 완전 가이드

왜곡된 스캐너에서 촬영한 것처럼 보이는 **이미지 기울기 보정 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 실제 프로젝트에서 **이미지에서 텍스트 추출**하기 전에 가장 먼저 해야 할 일은 그 흔들림을 바로 잡는 것입니다.  

이 튜토리얼에서는 **OCR을 위한 이미지 전처리** 예제, 회전 보정, 그리고 Python OCR 라이브러리를 사용해 **스캔을 텍스트로 변환**하는 과정을 손에 잡히게 단계별로 보여드립니다. 모호한 설명 없이 바로 복사‑붙여넣기 할 수 있는 작동 스크립트와 흔히 겪는 함정에 대한 팁을 제공합니다.  

## 달성 목표

이 가이드를 마치면 다음을 할 수 있습니다:

* 조금 기울어진 스캔된 JPEG 또는 PNG 파일을 로드합니다.  
* OCR 정확도를 높이기 위해 기울기 보정 필터와 이진화 단계를 적용합니다.  
* OCR 엔진을 실행하고 **이미지에서 텍스트 추출**을 안정적으로 수행합니다.  
* **올바른 이미지 회전**이 후속 텍스트 추출에 왜 중요한지 이해합니다.  

### 사전 요구 사항

* 머신에 Python 3.9+가 설치되어 있어야 합니다.  
* `ocr` 네임스페이스를 모방하는 pip 설치 가능한 OCR 패키지(예: Tesseract 래퍼).  
* Python 함수와 이미지 처리 개념에 대한 기본적인 이해.  

위 조건을 갖추셨다면, 시작해봅시다.

![이미지 기울기 보정 예시](deskew_before_after.png){alt="이미지 기울기 보정 전후"}

## 단계 1: OCR 엔진 설정 – Python을 사용한 이미지 기울기 보정

먼저 해야 할 일은 문서의 언어를 이해할 수 있는 OCR 엔진을 준비하는 것입니다. 아래 스니펫은 엔진을 생성하고 영어 텍스트를 처리한다는 것을 알려주는 최소 보일러플레이트를 보여줍니다.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*왜 중요한가:* 엔진의 언어 설정은 사용되는 문자 집합과 사전에 영향을 줍니다. 이 단계를 건너뛰면 **이미지 회전 보정** 후에도 OCR이 일반 단어를 오해할 수 있습니다.

## 단계 2: 바로잡을 스캔 이미지 로드

이제 파일을 메모리로 가져옵니다. `"YOUR_DIRECTORY/skewed_scan.jpg"`를 자신의 이미지 경로로 바꾸세요.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

이미지가 이미 NumPy 배열이나 OpenCV `Mat` 형태라면 로더를 그에 맞게 조정하면 됩니다 – 핵심은 이후에 사용할 `apply_filter` 메서드를 제공하는 객체여야 한다는 점입니다.

## 단계 3: OCR을 위한 이미지 전처리 – 기울기 보정 및 이진화

여기서 마법이 일어납니다. 두 개의 필터를 연결합니다:

1. **Deskew** – 텍스트 기준선을 자동으로 감지하고 이미지를 수평으로 회전시킵니다.  
2. **Binarize (Otsu)** – 사진을 순수한 흑백으로 변환해 인식률을 크게 향상시킵니다.  

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Pro tip:* 이진화 후에도 텍스트가 흐릿해 보이면 대비를 조정하거나 다른 임계값 방법을 사용해 보세요. `ocr.Filter` 모듈에는 어려운 경우를 위한 `adaptive_threshold()`가 종종 포함되어 있습니다.

## 단계 4: OCR 실행 – 이미지에서 텍스트 추출

깨끗하고 바로잡힌 캔버스를 엔진에 전달합니다. 결과 객체에는 인식된 문자열, 신뢰도 점수, 필요 시 사용할 수 있는 경계 상자가 포함됩니다.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

일반적인 출력 예시:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

줄 바꿈이 완벽히 맞춰진 것을 보셨나요? 이것이 **올바른 이미지 회전**의 장점입니다 – OCR이 이제 줄 방향을 추측할 필요가 없습니다.

## 단계 5: 전체 합치기 – 스캔을 텍스트로 변환하는 단일 파일 스크립트

아래는 지금까지 논의한 모든 부분을 결합한 완전 실행 가능한 스크립트입니다. `deskew_ocr.py`라는 파일명으로 저장하고 `python deskew_ocr.py`를 실행하세요.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### 작동 원리

* **먼저 Deskew** – 이진화 전에 이미지를 회전하면 임계값 알고리즘이 평평한 지평선 위에서 작동합니다.  
* **Deskew 후 Binarize** – Otsu 방법은 이중 피크 히스토그램을 가정합니다; 기울어진 페이지는 이 가정을 깨뜨립니다.  
* **English language model** – OCR에 기대할 문자들을 알려 주어 오탐을 줄입니다.  

다른 언어를 다루어야 한다면 `ocr.Language.ENGLISH`를 해당 열거형으로 교체하면 됩니다.

## 일반 질문 및 엣지 케이스

| 질문 | 답변 |
|----------|--------|
| *스캔이 뒤집혀 있으면 어떻게 하나요?* | `deskew()` 필터는 일반적으로 180° 회전도 감지합니다. 실패할 경우, 기울기 보정 전에 `apply_filter(ocr.Filter.rotate(180))`를 호출하세요. |
| *문서에 색상 그래픽이 포함되어 있는데, 이진화가 이를 삭제하나요?* | 예. 혼합 콘텐츠의 경우 `ocr.Filter.deskew()`만 사용하고, 컬러 이미지에 OCR을 실행하는 것을 고려하세요. 그래픽을 보존하면서도 텍스트를 추출할 수 있습니다. |
| *파일 배치를 처리할 수 있나요?* | 로직을 루프에 감싸고, 리스트에서 각 파일 경로를 읽어 `result.text`를 별도의 `.txt` 파일에 저장하면 됩니다. |
| *저해상도 스캔의 정확도를 어떻게 향상시킬 수 있나요?* | 기울기 보정 **이전**에 바이큐빅 필터로 이미지를 업스케일한 뒤, 샤프닝 필터를 적용하세요. 픽셀이 많을수록 OCR 엔진에 더 많은 단서가 됩니다. |

## 보너스: 기울기 보정 시각적 검증

전후 모습을 나란히 확인하고 싶다면 간단한 Matplotlib 스니펫을 추가하세요:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

정렬이 바로 잡힌 모습을 보는 것은 특히 까다로운 스캔 배치를 디버깅할 때 큰 안심이 됩니다.

## 결론

우리는 **이미지 기울기 보정 방법**, **OCR을 위한 이미지 전처리**가 왜 필수인지, 그리고 **이미지에서 텍스트 추출**을 통해 최종적으로 **스캔을 텍스트로 변환**하는 전체 흐름을 다루었습니다. 작업 흐름—로드 → 기울기 보정 → 이진화 → 인식—은 OCR이 깨끗하고 평평한 페이지를 보게 하여 정확도를 높이고 수동 교정 작업을 줄여줍니다.

다음 OCR 여정은 무엇인가요? 다음을 시도해 보세요:

* 다른 언어 팩(`ocr.Language.FRENCH` 등) 사용.  
* 컬럼이나 테이블을 감지하는 레이아웃 분석 단계 추가.  
* PDF 라이브러리를 사용해 OCR 결과를 검색 가능한 PDF로 내보내기.  

문제가 발생하거나 특히 까다로운 스캔을 처리하는 자체 팁이 있다면 댓글을 남겨 주세요. 즐거운 코딩 되시고, 이미지가 언제나 완벽히 평평하길 바랍니다!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하여 밀접하게 연관된 주제를 다룹니다. 각 리소스는 완전한 코드 예시와 단계별 설명을 포함해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [AspOCR 사용 방법: .NET용 이미지 OCR 필터 전처리](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Aspose.OCR을 사용한 C# 이미지 텍스트 추출 및 언어 선택](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [이미지 OCR 방법 – OCR 이미지 인식에서 이미지에 OCR 수행](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
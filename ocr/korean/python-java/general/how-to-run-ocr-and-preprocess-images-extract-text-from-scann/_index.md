---
category: general
date: 2026-04-26
description: 스캔한 양식에서 OCR을 실행하는 방법, 노이즈를 줄이기 위해 이미지를 전처리하는 방법을 배우고, 이미지를 빠르게 텍스트로
  추출하는 방법.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: ko
og_description: 스캔한 문서에서 OCR을 실행하고, 이미지를 전처리하며, 노이즈를 줄이고, 텍스트를 효율적으로 추출하는 방법.
og_title: OCR 실행 및 이미지 전처리 방법 – 빠른 가이드
tags:
- OCR
- image processing
- Python
title: OCR 실행 및 이미지 전처리 방법 – 스캔된 양식에서 텍스트 추출
url: /ko/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 실행 방법 – 이미지에서 텍스트 추출을 위한 완전 가이드

지저분한 스캔 양식에서 **OCR을 실행하는 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 많은 실제 프로젝트에서 원본 이미지는 점이 많고, 조명이 고르지 않으며, 기타 특성 때문에 바로 사용할 수 있는 OCR이 제대로 작동하지 못합니다.  

좋은 소식은? 몇 줄의 Python 코드와 스마트한 전처리 파이프라인만 있으면 인식 정확도를 크게 높이고 **노이즈를 감소**시켜 필요한 정확한 단어를 추출할 수 있습니다. 이 튜토리얼에서는 사진을 로드하는 단계부터 최종 문자열을 출력하는 단계까지 모든 과정을 차근차근 살펴보며, 청구서, 영수증 또는 기타 스캔 문서에 적용할 수 있는 바로 사용할 수 있는 스니펫을 제공할 것입니다.

## What You'll Build

- 기본 OCR 라이브러리와 통신하는 `OcrEngine` 인스턴스.  
- 이미지를 **이진화**하고 **중간값 블러**를 적용해 점들을 부드럽게 만드는 전처리 체인.  
- `process()`를 간단히 호출해 `text` 속성으로 추출된 문자열을 반환하는 객체.  

끝까지 진행하면 어떤 이미지 파일이든 실행할 수 있는 독립형 스크립트를 얻으며, 콘솔에서 바로 추출된 텍스트를 확인할 수 있습니다.

## Prerequisites

- Python 3.9+ (여기서 사용된 문법은 최신 안정 버전과 일치합니다).  
- 가상의 `aocr` 패키지 – Tesseract 또는 최신 OCR 엔진을 감싸는 얇은 래퍼라고 생각하면 됩니다. `pip install aocr`로 설치합니다.  
- 참조할 수 있는 폴더에 배치된 스캔 이미지 (`scanned_form.jpg`).  

실제 OCR 라이브러리인 `pytesseract`를 사용한다면 `OcrEngine`을 해당 클래스와 교체하면 됩니다—다른 부분은 동일하게 유지됩니다.

![](how-to-run-ocr-example.png "how to run OCR example showing a scanned form and extracted text")

*Alt text: how to run OCR on a scanned document and view the extracted text.*

---

## Step 1: How to Run OCR – Initialize the Engine

엔진이 어떤 내용도 읽기 전에 인스턴스를 생성해야 합니다. `OcrEngine`을 나중에 시각 데이터를 해석할 뇌라고 생각하면 됩니다.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Why this matters:** 엔진을 인스턴스화하면 내부 모델이 설정되고, 언어 팩이 로드되며, 런타임 환경이 준비됩니다. 이 단계를 건너뛰면 나중에 `process()`를 호출했을 때 `NoneType` 오류가 발생하는 경우가 많습니다.

---

## Step 2: How to Preprocess Image – Load Your Scanned Form

뇌가 준비되었으니 이제 사진을 공급합니다. 이미지는 `aocr.Image`가 지원하는 모든 포맷이면 됩니다.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Pro tip:** 개발 단계에서는 절대 경로를 사용해 “파일을 찾을 수 없음” 오류를 방지하세요. 스크립트가 다른 작업 디렉터리에서 실행될 때 특히 유용합니다.

---

## Step 3: How to Reduce Noise – Apply Binarization & Median Blur

원본 스캔에는 종종 작은 점, 고르지 않은 배경, 흐릿한 그림자가 섞여 있습니다. 두 가지 고전적인 트릭인 **이진화**와 **중간값 블러**를 사용하면 문자 경계를 손상시키지 않으면서 깨끗하게 만들 수 있습니다.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Digging Deeper

- **Binarization**: `threshold=180` 값은 알고리즘에 “밝기가 180보다 밝으면 흰색, 그 외는 검은색”이라고 알려줍니다. 스캔이 너무 어둡거나 밝으면 이 값을 조정하세요.  
- **Median Blur**: 반경 `2`는 필터가 5×5 픽셀 창을 살펴 가운데 픽셀을 중간값으로 교체한다는 의미입니다. 이렇게 하면 글자 획은 유지하면서 고립된 점들을 부드럽게 제거합니다.

> **Edge case:** 문서에 색상 하이라이트가 포함된 경우 단순 이진 임계값이 이를 지워버릴 수 있습니다. 이런 경우 `aocr.ImageFilters.adaptive_threshold()`를 사용해 이미지 전체에 걸쳐 로컬하게 임계값을 적용하도록 고려하세요.

---

## Step 4: How to Extract Text – Run the OCR Process

깨끗한 이미지가 준비되면 이제 엔진에게 마법을 부여합니다.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **What happens under the hood?** 엔진은 픽셀 매트릭스 위에서 신경망(또는 레거시 패턴 매처)을 실행해 각 인식된 글리프를 유니코드 문자로 변환하고, 이를 줄과 단락으로 조합합니다.

---

## Step 5: How to Extract Text – Print the Result

`ocr_result` 객체는 편리한 `text` 속성을 제공합니다. 이제 결과를 확인해 봅시다.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Expected Output

스캔된 양식에 다음과 같은 내용이 포함되어 있다면:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

다음과 비슷한 결과가 출력됩니다:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

전처리 단계가 이전에 “Amount”를 “Am0unt”로 바꾸던 잡다한 점들을 제거한 것을 확인할 수 있습니다. 이것이 **노이즈를 감소**시키는 전처리의 힘입니다.

---

## Common Pitfalls & How to Fix Them

| Symptom | Likely Cause | Quick Fix |
|---------|--------------|-----------|
| 깨진 문자(예: “@#%”) | 이미지가 너무 어둡거나 밝음 | `binarize()`의 `threshold`를 조정하거나 `adaptive_threshold` 사용 |
| 누락된 단어 | 노이즈가 아직 남아 있음 | `median_blur`의 `radius`를 늘리거나 `gaussian_blur` 필터 추가 |
| 잘못된 언어(예: 영어 문자가 중국어로 변환) | 잘못된 언어 팩 로드 | 라이브러리가 지원한다면 `OcrEngine()` 생성 시 `language="eng"` 전달 |
| 큰 파일에서 처리 속도 저하 | 해상도가 높음 | 이진화 전에 `aocr.ImageFilters.resize(width=1200)`으로 이미지 축소 |

---

## Going Further – Next Steps and Related Topics

- **배치 처리**: 위 로직을 루프로 감싸 수십 개 파일을 자동으로 처리합니다.  
- **구조화된 출력**: `ocr_result.text`에 정규식을 적용해 날짜나 금액 같은 필드를 추출합니다.  
- **대체 라이브러리**: `aocr` 대신 `pytesseract`를 사용해 보세요—엔진 초기화 단계만 교체하면 됩니다.  
- **PDF용 이미지 전처리**: 각 PDF 페이지를 이미지로 변환한 뒤 동일한 파이프라인을 적용합니다.  

이러한 확장은 단일 양식에서 엔터프라이즈 급 문서 수집 파이프라인까지 솔루션을 확장할 수 있게 해줍니다.

---

## Conclusion

시작부터 끝까지 **OCR을 실행하는 방법**을 다루었고, **이미지를 전처리해 노이즈를 감소**시키는 방법을 보여주었으며, **이미지에서 텍스트를 추출**하는 깔끔하고 재현 가능한 스크립트를 제공했습니다. 핵심 포인트는 몇 가지 간단한 필터—이진화와 중간값 블러—만으로도 시끄러운 스캔을 신뢰할 수 있는 데이터 소스로 바꿀 수 있다는 점이며, 이는 수작업 정리 시간을 크게 절감합니다.

스크립트를 직접 실행해 보고, 임계값을 조정하며 정확도가 상승하는 모습을 확인해 보세요. 준비가 되면 배치 처리로 확장하거나 데이터베이스에 결과를 저장해 검색 가능한 아카이브를 구축해 보시기 바랍니다. 즐거운 코딩 되세요, 그리고 OCR이 언제나 정확히 작동하길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
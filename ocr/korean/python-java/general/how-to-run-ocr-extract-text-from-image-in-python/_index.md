---
category: general
date: 2026-03-26
description: PNG 파일에서 OCR을 실행하고 사용자 정의 사전을 사용해 이미지에서 텍스트를 추출하여 OCR 정확도를 높이는 방법. OCR을
  빠르게 수행하기 위해 이미지를 로드하는 방법을 배워보세요.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: ko
og_description: PNG 파일에서 OCR을 실행하고 사용자 정의 사전을 사용해 이미지에서 텍스트를 추출하여 OCR 정확도를 향상시키는 방법.
  단계별 가이드.
og_title: OCR 실행 방법 – 파이썬으로 이미지에서 텍스트 추출
tags:
- OCR
- Python
- Image Processing
title: OCR 실행 방법 – 파이썬에서 이미지에서 텍스트 추출
url: /ko/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 실행 방법 – 파이썬에서 이미지에서 텍스트 추출하기

스캔한 청구서나 스크린샷에서 **OCR을 실행하는 방법**을 궁금해 본 적 있나요? 깨끗하고 검색 가능한 텍스트를 얻고 싶으신가요? 당신만 그런 것이 아닙니다. 많은 프로젝트에서 병목 현상은 단순히 OCR용 이미지를 로드하고 엔진이 도메인‑특정 단어를 이해하도록 유도하는 것입니다.  

이 튜토리얼에서는 **이미지에서 텍스트 추출** 파일을 대상으로 완전하고 바로 실행 가능한 예제를 단계별로 살펴보고, **PNG에서 텍스트 인식** 방법을 보여주며, 사용자 정의 사전과 특수 문자를 활용해 **OCR 정확도 향상** 트릭도 시연합니다. 마지막까지 진행하면 어떤 파이썬 코드베이스에도 넣을 수 있는 독립형 스크립트를 얻게 됩니다.

## 필요 사항

- Python 3.8+ (코드는 타입 힌트를 사용하지만 이전 3.x 버전에서도 작동합니다)
- 대상 OCR 엔진에 포함된 `ocr` 라이브러리(`pip install ocr‑engine` 로 설치 – 실제 패키지 이름으로 교체)
- 처리하려는 이미지 파일(`input.png`)
- 선택 사항: 도메인‑특정 단어가 한 줄에 하나씩 들어 있는 일반 텍스트 파일(`invoice_terms.txt`)

무거운 외부 종속성이나 클라우드 API 키가 필요 없으며, 로컬 OCR 엔진만 있으면 됩니다.

---

## 단계 1: OCR 라이브러리 설치 및 임포트

먼저 OCR 패키지가 설치되어 있는지 확인하세요. 가상의 `ocr-engine` 패키지를 사용한다면 다음을 실행합니다:

```bash
pip install ocr-engine
```

이제 필요한 클래스를 임포트합니다:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **전문가 팁:** 가상 환경을 사용 중이라면 설치 전에 활성화하여 전역 파이썬을 깨끗하게 유지하세요.

## 단계 2: OCR 엔진 인스턴스 생성

엔진 객체를 생성하는 것은 모든 OCR 작업의 진입점입니다. 이를 소프트웨어에서 스캐너 하드웨어를 켜는 것이라고 생각하면 됩니다.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

왜 중요한가: 엔진은 언어 팩, 인식 모드, 이후에 연결할 사용자 정의 리소스와 같은 설정을 보관합니다. 이것이 없으면 **OCR용 이미지 로드**를 할 수 없으며 인식 파이프라인을 실행할 수 없습니다.

## 단계 3: 인식할 이미지 로드

여기서는 실제로 **OCR용 이미지 로드**를 수행합니다. `Imaging.Image.load()` 메서드는 파일을 읽어 엔진이 기대하는 내부 비트맵 형식으로 변환합니다.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

JPEG나 TIFF 파일이 있더라도 동일한 메서드가 작동합니다—확장자만 바꾸면 됩니다. 엔진이 자동으로 형식을 감지합니다.

> **예외 상황:** 매우 큰 이미지(5 MP 이상)는 메모리 급증을 일으킬 수 있습니다. 성능 문제가 발생하면 로드하기 전에 Pillow로 다운스케일을 고려하세요.

## 단계 4: 정확도 향상을 위한 사용자 정의 사전 제공

대부분의 OCR 엔진은 일반 언어 모델을 제공합니다. 청구서, 영수증, 법률 문서에서는 종종 단어가 누락됩니다. 사용자 정의 단어 목록을 제공하면 엔진에 “이 용어들은 정상이며, 올바른 것으로 처리하라”고 알려주는 것입니다.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

일반적인 항목은 다음과 같습니다:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

이를 추가하면 **OCR 정확도 향상** 지표가 크게 개선됩니다—특히 비ASCII 기호에 대해.

## 단계 5: 기본 세트에 포함되지 않은 특수 문자 추가

도메인에서 유로 기호(€)나 스칸디나비아 문자 Ø와 같은 기호를 사용한다면, 명시적으로 추가할 수 있습니다:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

엔진은 이제 인식 단계에서 해당 글리프를 유효한 것으로 처리하여 “쓰레기” 출력이 나올 가능성을 줄입니다.

## 단계 6: OCR 프로세스 실행 및 텍스트 추출

마지막으로 인식기를 호출하고 순수 텍스트 결과를 가져옵니다. `recognize()` 호출은 풍부한 객체를 반환하지만, 대부분의 경우 원시 문자열만 필요합니다.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**예상 출력** (간략히 표시):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

출력이 깨져 보이면 사용자 정의 사전과 특수 문자가 올바르게 로드되었는지 다시 확인하세요.

---

## 시각적 개요

![OCR 실행 흐름도](ocr-workflow.png){alt="OCR 실행 흐름도"}

위 다이어그램은 이미지를 로드하여 깨끗한 텍스트를 얻는 흐름을 보여주며, 사용자 정의 사전과 문자 집합을 삽입할 수 있는 위치를 강조합니다.

---

## 자주 묻는 질문 및 주의사항

### 다중 페이지 PDF에서도 작동하나요?

예—각 페이지를 PNG로 변환(`pdf2image` 등 사용)한 뒤 동일한 `ocr_engine` 인스턴스에 순차적으로 전달하면 됩니다. 엔진은 각 이미지를 독립적으로 처리하므로, 연결할 수 있는 문자열 리스트를 얻습니다.

### 이미지가 회전된 경우는 어떻게 하나요?

대부분의 최신 OCR 엔진은 방향을 자동 감지하지만, 다음과 같이 강제로 회전시킬 수 있습니다:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### 영어가 아닌 다른 언어를 처리하려면?

이미지를 로드하기 전에 언어 모델을 교체합니다:

```python
ocr_engine.set_language("de")  # German
```

해당 언어 팩이 설치되어 있는지 확인하세요.

---

## 전체 스크립트 – 복사 및 붙여넣기 준비

아래는 전체 프로그램이며, 자리표시자 경로를 교체하면 바로 실행할 수 있습니다.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

다음 명령으로 실행합니다:

```bash
python run_ocr.py
```

콘솔에 추출된 텍스트가 출력될 것입니다. 이후 파일에 저장하거나 데이터베이스에 넣거나 하위 NLP 파이프라인에 전달할 수 있습니다.

---

## 요약 및 다음 단계

우리는 PNG에서 **OCR 실행 방법**, **이미지에서 텍스트 추출** 방법을 다루었고, 사전과 사용자 정의 문자를 활용해 **PNG에서 텍스트 인식** 및 **OCR 정확도 향상** 실용적인 방법을 보여주었습니다.  

다음과 같이 고려해 보세요:

- **배치 처리:** 이미지 디렉터리를 순회합니다.
- **후처리:** 정규식을 사용해 청구서 번호나 날짜를 추출합니다.
- **통합:** 스크립트를 Flask API에 연결해 필요 시 OCR 서비스를 제공합니다.

더 고급 주제에 관심이 있다면 OpenCV 전처리를 활용한 **OCR용 이미지 로드** 튜토리얼을 확인하거나, LSTM 레이어가 포함된 Tesseract 4+와 같은 딥러닝 기반 OCR 모델을 살펴보세요.

---

### 실험을 계속하세요!

`invoice_terms.txt`를 의료 용어 목록으로 교체하고, 그리스 문자를 추가하거나, 저해상도 사진을 엔진에 입력해 정확도가 얼마나 향상되는지 확인해 보세요. 실험을 많이 할수록 전처리, 사용자 정의 어휘, 엔진 설정 간의 트레이드오프를 더 잘 이해하게 됩니다.

코딩 즐겁게 하시고, OCR 결과가 언제나 선명하길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
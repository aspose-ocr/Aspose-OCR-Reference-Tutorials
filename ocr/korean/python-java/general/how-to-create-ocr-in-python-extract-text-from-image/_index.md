---
category: general
date: 2026-04-26
description: OCR을 빠르고 신뢰성 있게 만드는 방법. 이미지에서 텍스트를 추출하고, OCR을 위해 이미지를 로드하며, 사용자 정의 사전을
  사용해 PNG에 OCR을 실행하는 방법을 배웁니다.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: ko
og_description: Python에서 OCR을 만들고 이미지에서 텍스트를 추출하는 방법. 이 가이드는 OCR을 위해 이미지를 로드하고, PNG에
  대해 OCR을 실행하며, 사용자 정의 사전을 사용하는 방법을 보여줍니다.
og_title: Python으로 OCR 만들기 – 빠른 텍스트 추출
tags:
- OCR
- Python
- Image Processing
title: Python으로 OCR 만들기 – 이미지에서 텍스트 추출
url: /ko/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 OCR 만들기 – 단계별 가이드

스캔한 PDF, 스크린샷, 손글씨 노트를 읽을 수 있는 **OCR을 만드는 방법**이 궁금했나요? 당신만 그런 것이 아닙니다. 실제 프로젝트에서는 *이미지에서 텍스트를 추출*해야 할 때가 많지만, 기본 제공 엔진은 도메인 특화 단어에서 종종 어려움을 겪습니다.

이 튜토리얼에서는 OCR용 이미지를 로드하고, 사용자 정의 사전을 적용하며, 최종적으로 **PNG 파일에서 OCR을 실행**하는 완전한 실행 가능한 예제를 확인할 수 있습니다. 끝까지 따라오면 모든 이미지에서 텍스트를 추출하고 엔진을 자신의 용어에 맞게 조정할 수 있게 됩니다.

## 이 튜토리얼에서 다루는 내용

* 작고 강력한 `aocr` 패키지(또는 호환 가능한 라이브러리) 설치.  
* `aspocorp`나 `licensekey`와 같은 용어를 인식하도록 **사용자 정의 사전**을 구성.  
* PNG, JPEG 또는 스캔한 PDF 페이지 등 **OCR용 이미지 로드**.  
* OCR 프로세스를 실행하고 결과를 출력.  

외부 문서 링크 없이, 오늘 바로 복사‑붙여넣기해서 실행할 수 있는 독립형 솔루션입니다.

### 사전 요구 사항

* Python 3.8 이상 (코드에서 f‑string을 사용).  
* 명령줄에 대한 기본적인 이해 – `pip install` 명령을 몇 번 입력하게 됩니다.  
* 예시에서 사용된 이미지 파일(`technical_doc.png`)을 참조 가능한 위치에 두세요.  

위 세 가지 조건을 충족한다면 바로 시작할 수 있습니다.  

---

## 단계 1: OCR 라이브러리 설치

먼저, 프로그래밍 가능한 설정 객체를 지원하는 OCR 엔진이 필요합니다. `aocr` 패키지는 네이티브 OCR 엔진을 감싸는 가벼운 래퍼이며 데모에 적합합니다.

```bash
# Install the library (run once)
pip install aocr
```

> **Pro tip:** Windows에서 컴파일 오류가 발생하면, 사전 빌드된 휠을 제공하는 `pip install aocr‑binary`를 시도해 보세요.

### 이 라이브러리를 설치해야 하는 이유

`aocr`는 **사용자 정의 사전**을 주입할 수 있는 `config` 객체에 직접 접근할 수 있게 해줍니다. 이는 특수 분야 어휘의 정확도를 높이는 비결입니다.

---

## 단계 2: OCR 엔진 인스턴스 생성 및 사용자 정의 사전 추가

이제 엔진을 시작하고 어떤 단어를 알려진 단어로 처리할지 지정합니다.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### 사용자 정의 사전이 중요한 이유

표준 OCR 모델은 일반 말뭉치로 학습됩니다. 모델이 “aspocorp”를 보면 “aspo corp”로 분리하거나 글자를 완전히 누락할 수 있습니다. 사용자 정의 목록을 제공하면 인식기가 필요한 정확한 철자에 편향되어 후처리 작업을 크게 줄일 수 있습니다.

---

## 단계 3: 처리할 이미지 로드

여기서 **OCR용 이미지 로드**를 수행합니다. `Image.load` 메서드는 경로 문자열을 받아 파일 유형을 자동으로 판단합니다.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Edge case:** 소스가 다중 페이지 PDF인 경우, 각 페이지를 먼저 PNG로 변환(`pdf2image` 등 사용)하고 엔진에 하나씩 전달하세요.

### 이미지 품질 향상을 위한 팁

* 해상도를 최소 300 dpi로 유지하세요.  
* 이미지가 올바른 방향인지 확인하고, 필요하면 `Pillow`로 회전하세요.  
* 컬러 스캔은 잡음을 줄이기 위해 그레이스케일로 변환하세요.

---

## 단계 4: PNG 파일에서 OCR 프로세스 실행

엔진을 설정하고 이미지를 로드했으니, 이제 **PNG에서 OCR을 실행**합니다.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

`process()` 호출은 인식된 텍스트, 신뢰도 점수, 각 단어의 경계 상자를 포함하는 객체를 반환합니다.

---

## 단계 5: 인식된 텍스트 출력

엔진이 찾은 내용을 확인하는 가장 간단한 방법은 `text` 속성을 출력하는 것입니다.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### 예상 출력

`technical_doc.png`에 *“The Aspocorp licensekey expires on 2025‑12‑31.”* 문장이 포함되어 있다면, 콘솔에 다음과 같이 표시됩니다:

```
The Aspocorp licensekey expires on 2025-12-31.
```

사용자 정의 사전 덕분에 브랜드명이 그대로 유지된 것을 확인하세요—일반 OCR이라면 손상될 수 있는 부분입니다.

---

## 전체 작업 예제 (복사‑붙여넣기 준비됨)

아래는 전체 스크립트이며, `run_ocr.py`로 저장할 수 있습니다. 이미지 경로를 실제 위치로 바꾸기만 하면 됩니다.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

터미널에서 실행하세요:

```bash
python run_ocr.py
```

앞 예시와 동일하게 추출된 텍스트가 콘솔에 출력될 것입니다.

---

## 자주 묻는 질문 (FAQ)

| Question | Answer |
|----------|--------|
| **스캔한 PDF에서 텍스트를 추출할 수 있나요?** | 예. 각 페이지를 먼저 PNG(또는 TIFF)로 변환한 뒤, 동일한 스크립트에 이미지를 전달하면 됩니다. |
| **이미지가 PNG가 아니라 JPEG인 경우는 어떻게 하나요?** | `Image.load` 메서드는 JPEG, BMP, TIFF, PNG를 기본적으로 지원합니다. 파일 확장자만 바꾸면 됩니다. |
| **저대비 스캔에서 정확도를 어떻게 높일 수 있나요?** | `Pillow`로 전처리하세요 – 대비를 높이고, 이진화를 적용하거나 `opencv`로 기울기를 보정합니다. |
| **각 단어에 대한 신뢰도 점수를 얻을 수 있나요?** | `ocr_result`에 `words`가 포함되어 있으며, 각 단어는 반복 가능한 `confidence` 속성을 가지고 있습니다. |
| **헤드리스 서버에서도 실행할 수 있나요?** | 물론 가능합니다. `aocr`는 GUI 의존성이 없어 CI 파이프라인에 최적입니다. |

---

## 다음 단계 및 관련 주제

이제 **OCR을 만드는 방법**과 **이미지 파일에서 텍스트를 추출하는 방법**을 알았으니, 다음을 탐색해 보세요:

* **전처리 기법** – `load image for OCR`는 첫 단계일 뿐이며, `opencv`를 사용해 노이즈를 제거하거나 선명하게 할 수 있습니다.  
* **배치 처리** – PNG 디렉터리를 순회하여 검색 가능한 아카이브를 생성합니다.  
* **다국어 지원** – 프랑스어나 독일어 문서를 읽어야 한다면 엔진에 언어 팩을 추가하세요.  
* **Elasticsearch와 통합** – 추출된 텍스트를 색인하여 스캔된 자산 전체에 대한 전체 텍스트 검색을 가능하게 합니다.  

이러한 확장 기능들은 방금 다룬 핵심 패턴을 기반으로 하므로 전환이 매우 쉬울 것입니다.

---

## 마무리

몇 분 안에 **OCR을 만드는 방법**을 다루었으며, 특히 PNG와 같은 **이미지 파일에서 텍스트를 안정적으로 추출**하는 방법을 설명했습니다. 또한 **OCR용 이미지 로드**, **사용자 정의 사전 적용**, **PNG에서 OCR 실행**을 외부 서비스 없이 수행하는 방법을 보여드렸습니다.

스크립트를 실행해 보고, 사전을 자신의 용어에 맞게 조정하면 모든 문서 디지털화 프로젝트를 위한 견고한 기반을 갖게 됩니다.

문제가 발생하면 아래에 댓글을 남겨 주세요—도와드리겠습니다. 그리고 성공 사례를 공유하는 것을 잊지 마세요; 커뮤니티는 실제 사례에서 가장 많이 배웁니다.

**문서 자동화가 준비되셨나요?** 코드를 가져가 수정하고 오늘 바로 픽셀을 검색 가능한 텍스트로 변환해 보세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
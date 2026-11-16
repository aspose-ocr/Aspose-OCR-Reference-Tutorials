---
category: general
date: 2026-06-25
description: Python에서 OCR 엔진을 초기화하여 사용자 정의 사전, 언어 설정 및 영역 타깃팅을 사용해 다중 페이지 PDF에서 텍스트를
  추출합니다.
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: ko
og_description: Python에서 OCR 엔진을 초기화하여 베트남어 PDF를 안정적으로 읽고, 언어 설정, 전처리 및 사용자 정의 사전을
  구성해 정확한 결과를 얻습니다.
og_title: OCR 엔진 초기화 – 단계별 PDF 추출 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: OCR 엔진 초기화 – PDF 텍스트 추출 완전 가이드
url: /ko/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 엔진 초기화 – PDF 텍스트 추출 완전 가이드

베트남어 인보이스 여러 장에 **OCR 엔진을 초기화**해야 하는데 어디서부터 시작해야 할지 몰라 고민한 적 있나요? 당신만 그런 것이 아닙니다. 실제 프로젝트에서 가장 먼저 마주치는 장벽은 OCR 라이브러리를 PDF와 연결하는 일이며, 특히 언어 설정, 전처리, 혹은 커스텀 사전을 조정해야 할 때 더욱 그렇습니다.  

이 가이드에서는 **OCR 엔진을 초기화**하고, 언어를 설정하며, 스마트 이미지 전처리를 활성화하고, 커스텀 사전을 추가한 뒤, 다중 페이지 PDF의 모든 페이지에서 구조화된 데이터를 추출하는 전체 실행 가능한 예제를 단계별로 살펴봅니다. 끝까지 따라오면 프로젝트에 바로 삽입할 수 있는 완전한 스크립트를 얻게 됩니다—빠진 부분 없이, “문서 참고” 같은 우회 없이.

## 배울 내용

- 베트남어 지원으로 **OCR 엔진을 초기화**하는 방법  
- 정확도를 높이는 **OCR 언어 설정**의 중요성  
- 자동 기울기 보정 및 자동 이진화와 같은 **OCR 이미지 전처리** 옵션 사용법  
- 도메인 특화 용어 인식을 강화하는 **OCR 커스텀 사전** 추가 방법  
- **다중 페이지 PDF** 인식 및 특정 영역(예: 총 금액) 추출  
- 원시 결과를 다운스트림 처리에 적합한 깔끔한 JSON‑유사 구조로 변환

### 사전 요구 사항

- Python 3.8+ 설치  
- `OcrEngine` 클래스를 제공하는 OCR 라이브러리(예시에서는 가상의 `ocr` 패키지를 사용; 실제 SDK로 교체)  
- 알려진 디렉터리에 위치한 샘플 다중 페이지 PDF(`sample.pdf`)  
- Python 딕셔너리와 반복문에 대한 기본 이해

위 조건을 갖췄다면 바로 시작합니다.

---

## 1단계: Python에서 OCR 엔진 초기화하기

가장 먼저 해야 할 일은 **OCR 엔진을 초기화**하는 것입니다. 이는 기계를 켜고 어떤 언어를 사용할지 알려주는 과정과 같습니다.

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **왜 중요한가:**  
> 대부분의 OCR 엔진은 기본 언어 팩만 제공합니다. `ocr_engine.language`를 명시적으로 설정하면 엔진이 잘못된 문자를 추측하는 일을 방지할 수 있어, 베트남어에 흔히 사용되는 악센트 문자 인식 오류를 크게 줄일 수 있습니다.

### 팁
동일 실행에서 여러 언어를 지원해야 할 경우, 각 페이지를 처리하기 전에 `ocr_engine.language`를 동적으로 전환하면 됩니다. SDK가 무거운 모델을 재로드해야 한다면 해당 모델을 다시 초기화하는 것을 잊지 마세요.

---

## 2단계: OCR 이미지 전처리 옵션 활성화

스캔본은 거의 완벽하지 않습니다. 페이지가 기울어졌거나 조명이 고르지 않거나 대비가 낮으면 최고의 인식기조차 오류를 일으킬 수 있습니다. 그래서 **OCR 이미지 전처리**를 초기화 직후에 설정합니다.

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

이 두 플래그만으로 대부분의 인보이스 스캔을 깨끗하게 만들 수 있습니다. 원본 PDF가 이미 고품질이라면 페이지당 몇 밀리초를 절약하기 위해 플래그를 끌 수 있습니다.

---

## 3단계: OCR 커스텀 사전 추가

주문 코드, 제품 ID, 법률 약어 등 도메인 특화 용어는 일반 언어 모델에 거의 포함되지 않습니다. **OCR 커스텀 사전**을 제공하면 엔진에 정답지를 주는 효과가 있습니다.

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **내부 동작 원리:**  
> 사전에 포함된 단어와 일치하면 엔진이 해당 단어의 신뢰도 점수를 높여, 다른 단어로 오인식될 가능성을 크게 낮춥니다.

---

## 4단계: 다중 페이지 PDF 인식 – 한 번에 전체 텍스트 가져오기

엔진 설정이 완료되었으니 이제 **다중 페이지 PDF**를 인식할 차례입니다. `recognize_multi_page` 메서드는 각 페이지가 OCR 처리된 결과를 담은 리스트를 반환합니다.

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

수백 페이지에 달하는 대용량 PDF를 다룰 경우, 메모리 사용량을 낮추기 위해 청크 단위로 처리하는 것을 권장합니다. 대부분의 SDK는 스트리밍 API를 제공하니 활용하세요.

---

## 5단계: 모든 페이지에서 특정 영역 추출

대부분의 인보이스는 “총 금액” 필드가 각 페이지의 동일한 위치에 있습니다. 페이지 전체 텍스트를 파싱하는 대신, 엔진에 사각형 영역만 집중하도록 지시할 수 있습니다.

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **왜 영역을 지정하나요?**  
> OCR 범위를 작은 영역으로 제한하면 처리 속도가 빨라지고, 페이지 나머지 부분이 잡음이 많을 때 발생할 수 있는 오인식도 감소합니다.

---

## 6단계: 각 페이지에 대한 JSON‑유사 딕셔너리 구성

원시 텍스트만으로는 충분하지 않으며, 다운스트림 시스템은 보통 구조화된 데이터를 기대합니다. 아래 예시는 페이지 번호, 전체 페이지 텍스트, 추출된 총액, 그리고 신뢰도 점수를 포함한 모든 인식 단어 목록을 담은 깔끔한 딕셔너리를 만드는 과정입니다.

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

스크립트를 실행하면 페이지당 하나씩 딕셔너리가 출력됩니다. 예시는 다음과 같습니다:

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

출력을 파일(`> results.jsonl`)로 리다이렉트하면 배치 처리에 편리합니다.

---

## 전체 작동 예제

전체 흐름을 하나로 합친 완전한 스크립트는 다음과 같습니다. 복사‑붙여넣기 후 바로 실행해 보세요:

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### 예상 출력

3페이지짜리 인보이스 PDF에 대해 스크립트를 실행하면 다음과 같은 결과가 나올 수 있습니다:

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

`jq` 등 JSON 파서에 파이프하면 구조를 손쉽게 확인할 수 있습니다.

---

## 자주 묻는 질문 & 예외 상황

| 질문 | 답변 |
|----------|--------|
| **PDF가 비밀번호로 보호되어 있으면 어떻게 하나요?** | 대부분의 SDK는 `recognize_multi_page` 호출 시 `password` 인자를 받습니다. `password="mySecret"` 를 추가하면 됩니다. |
| **스캔이 회색조이고 흑백이 아니에요.** | `auto_binarize` 옵션이 이를 처리하지만, `recognize_region`에 이미지를 전달하기 전에 `Pillow`로 직접 변환할 수도 있습니다. |
| **총 금액이 좌표가 달라서 나타나요.** | 템플릿 매칭 등으로 사각형을 동적으로 계산하거나, 전체 페이지 OCR 후 정규식 `r'\d{1,3}(,\d{3})* VND'` 로 텍스트를 검색하세요. |
| **500페이지 PDF에서 성능이 느려요.** | 페이지를 배치로 나눠 처리하세요: 50페이지씩 처리하고 결과를 기록한 뒤 `pages` 리스트를 비워 메모리를 해제합니다. 스캔이 이미 바로 서 있다면 `auto_deskew` 를 비활성화하세요. |
| **추후 다른 언어를 지원하려면?** | `ocr_engine.language = ocr.Language.English` (또는 지원되는 다른 enum) 로 변경한 뒤 `recognize_multi_page` 를 호출하면 됩니다. 파이프라인 나머지는 동일하게 유지됩니다. |

---

## 프로덕션 배포 시 팁

1. **예외 처리** – OCR 호출을 `try/except` 로 감싸고, 실패 시 페이지 인덱스를 로그에 남겨 재시도할 수 있게 합니다.  
2. **로깅** – `print` 대신 Python `logging` 모듈을 사용해 가변적인 로그 레벨을 관리합니다.  
3. **병렬 처리** – OCR 라이브러리가 스레드 안전하면 `ThreadPoolExecutor` 로 페이지를 동시에 처리합니다.  
4. **설정 파일** – 언어, 사전, 사각형 좌표 등을 JSON/YAML 파일에 저장해 프로젝트 간 재사용성을 높입니다.  
5. **테스트** – 알려진 PDF를 이용해 작은 테스트 스위트를 만들고, 추출된 `total_amount` 가 기대값과 일치하는지 검증합니다.  

---

## 결론

당신은 이제 **OCR 엔진을 초기화**하고, 언어와 전처리를 설정하며, 커스텀 사전을 적용하고, 다중 페이지 PDF에서 원하는 영역을 추출해 구조화된 JSON‑유사 데이터를 얻는 전체 흐름을 마스터했습니다.

## 다음에 배울 내용

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하고, 추가 API 기능을 마스터하며, 프로젝트에 다양한 구현 방식을 적용할 수 있도록 도와줍니다.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
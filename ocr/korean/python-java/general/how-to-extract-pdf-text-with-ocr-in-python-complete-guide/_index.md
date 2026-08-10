---
category: general
date: 2026-06-19
description: Python에서 OCR을 사용하여 PDF 추출하는 방법 – PDF에서 텍스트 추출, 이미지에서 텍스트 인식, OCR Python
  예제를 포함한 단계별 튜토리얼.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: ko
og_description: Python에서 OCR을 사용해 PDF를 추출하는 방법. PDF에서 텍스트를 추출하고 이미지에서 텍스트를 인식하며, 완전한
  OCR Python 예제를 확인하세요.
og_title: Python에서 OCR을 사용해 PDF 텍스트 추출하는 방법 – 전체 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Python에서 OCR로 PDF 텍스트 추출하는 방법 – 완전 가이드
url: /ko/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 파이썬에서 OCR을 사용해 PDF 텍스트 추출하기 – 완전 가이드

스캔된 이미지일 뿐인 파일에서 **PDF를 추출하는 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 실제 프로젝트에서는 계약서, 청구서, 혹은 역사적 기록과 같이 PDF가 선택 가능한 텍스트를 전혀 포함하지 않을 때가 많습니다. 좋은 소식은? 파이썬 몇 줄만으로 이미지 전용 페이지를 검색 가능하고 편집 가능한 텍스트로 변환할 수 있다는 것입니다.

이 튜토리얼에서는 PDF를 읽고 첫 페이지를 이미지로 렌더링한 뒤 OCR 엔진을 사용해 **PDF에서 텍스트를 추출**하는 실용적인 **OCR 파이썬 예제**를 단계별로 살펴보겠습니다. 마지막까지 하면 **OCR로 PDF 읽기** 방법, 각 단계가 중요한 이유, 그리고 다중 페이지 문서나 다른 언어에 맞게 코드를 정확히 알게 됩니다.

## 배울 내용

- 파이썬용 신뢰할 수 있는 OCR 라이브러리를 설치하고 설정합니다.  
- OCR에 적합한 이미지로 PDF 페이지를 변환합니다.  
- **이미지에서 텍스트 인식**하고 깨끗한 유니코드 문자열을 가져옵니다.  
- 일반적인 함정(저해상도 PDF, 회전된 페이지)과 이를 피하는 방법.  
- 스크립트를 확장하여 다중 페이지 또는 배치 처리에 대응합니다.

**전제 조건**: Python 3.8 이상, pip, 그리고 가상 환경에 대한 기본 이해. 사전 OCR 경험은 필요 없으며, 따라하기만 하면 됩니다.

---

## ## 파이썬에서 OCR을 사용해 PDF 텍스트 추출하기

이 H2 헤더는 주요 키워드를 검색 엔진이 선호하는 위치에 포함하고 있습니다. 바로 코드로 들어가 보겠습니다.

### Step 1 – 필요한 패키지 설치

먼저 OCR 엔진이 필요합니다. 아래 예제는 Tesseract를 감싸는 가벼운 래퍼인 인기 **ocr** 패키지를 사용합니다. 다른 백엔드를 선호한다면 개념은 동일합니다.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **팁:** Linux에서는 Tesseract 바이너리도 필요합니다: `sudo apt-get install tesseract-ocr`. macOS 사용자는 Homebrew를 통해 설치할 수 있습니다: `brew install tesseract`.

### Step 2 – OCR 엔진 초기화 및 언어 설정

이제 엔진을 시작하고 영어 문자를 찾도록 설정합니다. `ocr.Language.English`를 지원되는 다른 언어 코드로 교체할 수 있습니다.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**왜 중요한가:** 언어를 지정하면 엔진이 해당 언어 전용 사전과 문자 모델을 적용할 수 있어 정확도가 크게 향상됩니다.

### Step 3 – PDF 페이지를 이미지로 로드

OCR은 PDF 객체가 아니라 래스터 이미지에서 작동합니다. `ocr.Image.from_pdf` 헬퍼는 선택한 페이지를 비트맵으로 렌더링합니다. 다른 페이지를 사용하려면 `page_number`를 조정하세요(0부터 시작하는 인덱스).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **예외 상황:** PDF에 스캔된 이미지가 아닌 벡터 그래픽이 포함된 경우 선명한 렌더링을 얻을 수 있습니다. 저해상도 스캔의 경우 DPI를 높이는 것을 고려하세요: `ocr.Image.from_pdf(..., dpi=300)`.

### Step 4 – 렌더링된 이미지에서 텍스트 인식

이것이 **ocr 파이썬 예제**의 핵심입니다. 엔진은 비트맵을 처리하고 추출된 문자열을 포함한 객체를 반환합니다.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

`ocr_result.text` 속성은 가능한 경우 줄 바꿈을 유지한 순수 텍스트 출력을 담고 있습니다.

### Step 5 – 추출된 텍스트 출력 또는 저장

마지막으로 결과를 출력합니다. 실제 애플리케이션에서는 파일이나 데이터베이스에 저장할 가능성이 높습니다.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

스크립트를 실행하면 다음과 같은 출력이 나타납니다:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

이것이 OCR을 사용한 완전한 **PDF에서 텍스트 추출** 워크플로우입니다.

---

## ## 이미지에서 텍스트 인식 – 정확도 조정

**이미지에서 텍스트 인식**(예: 영수증 JPEG)만 필요하다면 PDF 변환 단계를 건너뛸 수 있습니다:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

더 나은 결과를 위한 팁:

- **전처리**: 이미지를 그레이스케일로 변환하고, 임계값 적용 또는 기울기 보정(deskew). Pillow를 사용하면 쉽게 할 수 있습니다.
- PDF 렌더링 시 **DPI 증가**: 높은 해상도가 OCR 엔진에 더 많은 세부 정보를 제공합니다.
- 페이지 구분을 위한 OCR 엔진 **설정 활성화** (`ocr_engine.config = "--psm 6"`은 균일 블록용).

## ## OCR로 PDF 읽기 – 다중 페이지 처리

대부분의 계약서는 여러 페이지에 걸쳐 있습니다. 각 페이지를 순회하는 것은 간단합니다:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

이 함수는 **OCR로 PDF를 읽고**, 출력 결과를 연결한 뒤 명확한 페이지 구분자를 삽입합니다. 이후 `full_text`를 검색 인덱스에 넣거나 `.txt` 파일로 저장할 수 있습니다.

## ## 일반적인 함정과 해결 방법

| 증상 | 가능한 원인 | 해결 방법 |
|---------|--------------|-----|
| 문자가 깨지거나 `?`가 많이 표시됨 | 잘못된 언어 설정 또는 언어 데이터 파일 누락 | 올바른 Tesseract 언어 팩(`tesseract-ocr-<lang>`)을 설치하고 `ocr_engine.language`를 설정합니다. |
| 줄이 누락되거나 단어가 잘려 나옴 | DPI가 낮음(150 이하) | PDF를 300 DPI 이상(`dpi=300`)으로 렌더링합니다. |
| 텍스트가 회전되었거나 뒤집혀 있음 | 스캔된 페이지가 올바른 방향이 아님 | 인식 전에 `ocr.Image.deskew(page_image)`를 사용합니다. |
| 대용량 PDF 처리 시 속도가 느림 | 단일 스레드에서 페이지를 순차적으로 처리 | `concurrent.futures.ThreadPoolExecutor`를 사용해 병렬 처리합니다. |

## ## OCR 파이썬 예제 확장

- **PDF/A로 내보내기**: 추출 후 `reportlab` 또는 `pypdf2`를 사용해 텍스트를 검색 가능한 PDF에 다시 삽입할 수 있습니다.
- **언어 감지**: OCR 출력에 `langdetect`를 적용해 `ocr_engine.language`를 동적으로 전환합니다.
- **배치 처리**: `os.listdir`로 디렉터리를 순회하고 `extract_all_pages`를 모든 파일에 적용합니다.

## ## 예상 출력 및 검증

명확한 영어 스캔에 대해 스크립트를 실행하면 적절한 구두점이 포함된 깔끔한 텍스트 블록이 표시됩니다. 검증 방법:

1. 몇 줄을 원본 스캔 이미지와 비교합니다.  
2. 간단한 단어 수(`len(ocr_result.text.split())`)를 실행해 출력이 비어 있지 않은지 확인합니다.  
3. 선택적으로 결과를 `pyspellchecker`와 같은 맞춤법 검사기에 입력해 OCR 오류를 찾아봅니다.

## 결론

전통적인 파싱이 실패할 때 **PDF를 추출하는 방법**을 다루었고, 전체 **ocr 파이썬 예제**를 시연했으며, **이미지에서 텍스트 인식** 및 **OCR로 PDF 읽기**를 단일 페이지와 다중 페이지 상황 모두에 적용하는 방법을 설명했습니다. 위 코드 스니펫을 사용하면 이제 스캔된 PDF를 검색 가능하고 편집 가능한 텍스트로 변환할 수 있어 수동 재입력이 필요 없습니다.

다음 단계는? 언어를 스페인어(`ocr.Language.Spanish`)로 바꾸어 보거나 이미지 전처리 기법을 실험해 정확도를 높여보세요. 문서 관리 시스템을 구축 중이라면 추출된 텍스트를 Elasticsearch에 색인하여 초고속 검색을 구현하는 것을 고려해 보세요.

질문이 있거나 특이한 PDF에 부딪혔다면 댓글을 남겨 주세요. 즐거운 코딩 되세요!  

![파이썬에서 OCR을 사용해 PDF 추출하기](image.png "파이썬에서 OCR을 사용해 PDF 추출하기")

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 완전한 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 숙달하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose OCR을 사용해 이미지에서 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [PDF 텍스트 인식 – Aspose.OCR for Java를 사용한 OCR 작업](/ocr/english/java/ocr-operations/)
- [Aspose.OCR을 사용한 언어 선택이 가능한 C# 이미지 텍스트 추출](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
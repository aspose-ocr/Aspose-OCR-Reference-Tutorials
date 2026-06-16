---
category: general
date: 2026-06-16
description: Python OCR을 사용해 TIFF 파일에서 텍스트를 추출합니다. 단계별로 TIFF를 텍스트로 변환하는 방법을 배우고, 다중
  페이지 문서를 손쉽게 처리하세요.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: ko
og_description: Python OCR로 TIFF 파일에서 텍스트를 추출하세요. 이 가이드를 따라 TIFF를 텍스트로 변환하고, 다중 페이지
  스캔을 처리하며, 깔끔한 결과를 얻으세요.
og_title: TIFF에서 텍스트 추출 – 완전한 파이썬 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: TIFF에서 텍스트 추출 – 완전한 파이썬 가이드
url: /ko/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF에서 텍스트 추출 – 완전한 Python 가이드

TIFF 이미지에서 **텍스트를 추출**해야 하는데 어디서 시작해야 할지 몰라 고민한 적 있나요? 혼자가 아닙니다—스캔된 아카이브나 레거시 문서를 다룰 때 많은 개발자들이 이 문제에 부딪힙니다. 좋은 소식은 몇 줄의 Python 코드만으로 **TIFF를 텍스트로 변환**할 수 있다는 점입니다. 파일에 수십 페이지가 있더라도 순식간에 처리할 수 있습니다.

이 튜토리얼에서는 실제 예제를 통해 다중 페이지 TIFF를 로드하고, OCR 언어를 프랑스어로 설정한 뒤, 각 페이지에서 인식된 텍스트를 추출하는 과정을 단계별로 살펴봅니다. 끝까지 따라오시면 바로 실행 가능한 스크립트를 얻고, 각 단계가 왜 중요한지 이해하며, 다른 언어나 이미지 형식에도 쉽게 적용할 수 있게 됩니다.

## 사전 요구 사항

시작하기 전에 다음을 준비하세요:

- Python 3.8 이상 설치
- `ocr` 패키지(또는 `OcrEngine` 클래스를 제공하는 호환 OCR 라이브러리). `pip install ocr-lib` 로 설치할 수 있습니다—사용 중인 실제 패키지 이름으로 교체하세요.
- 처리하고자 하는 다중 페이지 TIFF 파일(예: `french-scans.tif`)
- Python 스크립팅에 대한 기본 지식

무거운 의존성도, 외부 서비스도 필요 없습니다—순수 Python과 OCR 엔진만 있으면 됩니다.

---

## Step 1: **Extract Text from TIFF**을 위한 OCR 엔진 설정

우선 OCR 엔진 인스턴스를 만들고 사용할 언어를 지정해야 합니다. 여기서는 원본 자료가 프랑스어이므로 언어를 프랑스어로 설정합니다.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**왜 중요한가요:**  
언어 설정은 정확도에 큰 영향을 줍니다. “é”나 “ç” 같은 프랑스어 문자들은 엔진이 기본 영어로 동작하면 일반 기호로 오인될 수 있습니다. 프랑스어를 명시적으로 선택함으로써 올바른 문자 맵을 엔진에 제공하게 됩니다.

> **Pro tip:** 여러 언어가 섞인 문서를 처리할 경우, 각 `recognize()` 호출 전에 `engine.language` 를 동적으로 변경할 수 있습니다.

---

## Step 2: **Convert TIFF to Text**를 위한 다중 페이지 TIFF 로드

TIFF는 여러 프레임을 담을 수 있습니다—각 프레임을 별도의 페이지로 생각하면 됩니다. OCR 라이브러리가 이를 추상화해 주므로 파일 경로만 지정하면 됩니다.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**예외 상황 알림:**  
파일 경로가 잘못되었거나 TIFF가 손상된 경우 `load_from_file` 메서드가 예외를 발생시킵니다. 실제 서비스 코드에서는 `try/except` 블록으로 감싸는 것이 좋습니다:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Step 3: **Extract Text from TIFF** 핵심 – 전체 문서에 OCR 실행

이제 엔진에게 작업을 맡깁니다. `recognize()` 호출은 모든 페이지를 한 번에 처리하고 풍부한 결과 객체를 반환합니다.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**내부에서 무슨 일이 일어나나요?**  
엔진은 각 프레임을 순회하면서 전처리(기울기 보정, 이진화)를 수행하고, 신경망을 실행한 뒤 출력을 집계합니다. `recognize()` 를 한 번만 호출했기 때문에 라이브러리는 페이지 간에 리소스를 공유할 수 있어, 수동 루프보다 빠릅니다.

---

## Step 4: JSON 결과에서 인식된 텍스트 추출 – 페이지별 **Convert TIFF to Text**

결과 객체는 JSON 형태로 직렬화할 수 있습니다. 그 JSON 안에 `pages` 배열이 있으며, 각 요소는 `text` 필드를 가지고 있습니다.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

이제 각 페이지의 OCR 결과가 들어 있는 깔끔한 Python 리스트를 얻었습니다.

---

## Step 5: 각 페이지의 텍스트 출력 또는 저장 – 최종 **Extract Text from TIFF** 단계

페이지를 순회하면서 추출된 텍스트를 화면에 표시해 보겠습니다. 원한다면 각 페이지를 별도의 `.txt` 파일로 저장할 수도 있습니다.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### 예상 출력 (예시)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

OCR이 성공하면 각 페이지마다 깔끔한 프랑스어 문장이 표시됩니다. 문자 깨짐이 보인다면 언어 설정을 다시 확인하거나 OCR 전에 이미지 해상도를 높이는 것을 고려하세요.

---

## **Convert TIFF to Text** 시 흔히 마주치는 문제 처리

| 문제 | 발생 원인 | 빠른 해결책 |
|------|----------|------------|
| **Empty `pages` array** | TIFF가 올바르게 로드되지 않았거나 프레임이 없음 | 파일 경로를 확인하고, TIFF가 단일 페이지 PNG를 가장한 것이 아닌지 확인 |
| **Garbage characters** | 언어 불일치 또는 이미지 품질 저하 | 올바른 `engine.language` 설정 및 이미지 전처리(예: DPI 상승) |
| **Memory blow‑up on huge TIFFs** | 모든 페이지를 한 번에 로드해 RAM 과다 사용 | 청크 단위 처리: 한 프레임을 로드·인식·버린 뒤 다음 프레임으로 이동 |
| **Unicode errors when printing** | 콘솔 인코딩이 억양 문자 지원 안 함 | `print(page["text"].encode('utf-8').decode('utf-8'))` 사용하거나 터미널을 UTF‑8 로 설정 |

---

## 스크립트 확장: **Extract Text from TIFF** → 배치 처리

기본이 탄탄해졌으니 다음 단계도 고려해 보세요:

1. **배치 변환** – 전체 흐름을 `def ocr_tiff(path):` 함수로 감싸고, 디렉터리 내 모든 TIFF 파일을 순회
2. **파일 출력** – 화면에 출력하는 대신 `page_{i}.txt` 로 저장하거나 전체를 하나의 문서로 합치기
3. **대체 OCR 엔진** – 정확도가 필요하면 `ocr.OcrEngine()` 대신 Tesseract(`pytesseract`) 또는 Azure Cognitive Services 로 교체—핵심 로직은 동일하게 유지
4. **후처리** – 맞춤법 검사, 언어 감지, 정규식 정리 등을 적용해 원시 OCR 출력 다듬기

---

## 전체 실행 가능한 스크립트

아래 코드는 복사‑붙여넣기만 하면 바로 사용할 수 있는 완전한 예시입니다. 기본 오류 처리와 각 페이지 텍스트를 별도 파일에 저장하는 옵션을 포함하고 있습니다.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

스크립트를 실행하고 `tiff_file` 변수를 대상 문서 경로로 지정하면 콘솔에 깔끔한 프랑스어 문장이 출력됩니다. `out_folder` 를 지정하면 `page_#.txt` 파일들이 생성되어 후속 처리에 활용할 수 있습니다.

---

## 결론

우리는 간단한 Python OCR 워크플로우를 통해 **TIFF에서 텍스트를 추출**하고, **TIFF를 텍스트로 변환**하는 방법을 살펴보았습니다. 올바른 언어 설정부터 페이지별 JSON 결과를 순회하는 과정까지 각 단계의 이유를 이해했으니, 다른 언어, 이미지 형식, 대용량 배치 작업에도 손쉽게 적용할 수 있습니다.

다음은 무엇을 해볼까요? OCR 백엔드를 Tesseract 로 교체해 보거나, 다양한 언어 팩을 실험하거나, 출력 결과를 검색 가능한 데이터베이스에 연동해 보세요. 스캔된 이미지를 신뢰성 있게 텍스트로 변환할 수 있다면 가능성은 무한합니다.

궁금한 점이나 개선 아이디어가 있으면 언제든 댓글을 남겨 주세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

아래 튜토리얼들은 이번 가이드에서 다룬 기술을 확장하거나 변형하는 데 도움이 되는 관련 주제들입니다. 각 리소스는 완전한 코드 예시와 단계별 설명을 제공하므로, 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 유용합니다.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-06-19
description: OCR을 단계별로 실행하고 일반 텍스트 OCR 기술로 정확도를 향상시키는 방법. 신뢰할 수 있는 텍스트 추출을 위한 빠른 워크플로우를
  배우세요.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: ko
og_description: OCR을 효율적으로 실행하는 방법. 이 튜토리얼은 일반 텍스트 OCR과 AI 후처리를 사용하여 OCR 정확도를 향상시키는
  방법을 보여줍니다.
og_title: Python에서 OCR 실행 방법 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Python에서 OCR을 실행하는 방법 – 완전 가이드
url: /ko/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 파이썬에서 OCR 실행 방법 – 완전 가이드

스캔한 PDF 배치를 대상으로 **OCR을 실행하는 방법**을 고민해 본 적 있나요? 설정을 조정하는 데 시간을 들이지 않아도 됩니다. 많은 프로젝트에서 첫 번째 장애물은 이미지에서 신뢰할 수 있는 텍스트를 추출하는 것이며, 흔들리는 결과와 깔끔한 추출 사이의 차이는 몇 가지 스마트한 단계에 달려 있습니다.

이 가이드에서는 **OCR을 실행**할 뿐만 아니라 **OCR 정확도를 향상**시키는 실용적인 4단계 파이프라인을 살펴봅니다. 빠른 일반 텍스트 패스와 레이아웃 인식 두 번째 패스, 그리고 AI 기반 후처리를 결합합니다. 끝까지 진행하면 바로 실행 가능한 스크립트와 각 단계가 왜 중요한지에 대한 명확한 설명, 다중 컬럼 페이지나 노이즈가 많은 스캔과 같은 엣지 케이스를 처리하는 팁을 얻을 수 있습니다.

---

## 필요한 것들

- **Python 3.9+** – 코드는 타입 힌트와 f‑strings를 사용합니다.
- **Tesseract OCR**이 설치되어 `tesseract` 명령줄을 통해 접근할 수 있어야 합니다. (Ubuntu에서는: `sudo apt install tesseract-ocr`; Windows에서는 공식 저장소에서 설치 프로그램을 다운로드하세요.)
- **pytesseract** 래퍼 (`pip install pytesseract`).
- **AI 후처리 라이브러리** – 이 예시에서는 가벼운 `ai` 모듈이 `run_postprocessor`를 제공한다고 가정합니다. 원한다면 OpenAI의 GPT‑4 API나 로컬 LLM으로 교체하세요.
- 테스트용 샘플 이미지 또는 PDF 몇 개.

그게 전부입니다. 무거운 프레임워크도, Docker 설정도 필요 없습니다. 몇 개의 pip 설치만 하면 바로 시작할 수 있습니다.

---

## 단계 1: 빠른 일반 텍스트 OCR 실행

대부분의 개발자가 간과하는 첫 번째 사실은 *일반 텍스트* OCR 실행이 번개처럼 빠르고 빠른 sanity check를 제공한다는 점입니다. `engine.Recognize()`를 호출해 레이아웃 메타데이터 없이 원시 문자를 추출합니다. 이것이 **일반 텍스트 OCR**을 의미합니다.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*왜 중요한가:*
- **Speed** – 300 dpi 페이지에 대한 일반 패스는 보통 1초 미만에 완료됩니다.
- **Baseline** – 이후 구조화된 출력과 이 기준을 비교하여 명백한 오류를 찾을 수 있습니다.
- **Error‑catching** – 일반 패스가 완전히 실패하면(예: 모든 텍스트가 의미 없을 경우) 이미지 품질이 낮다는 것을 알고 조기에 중단할 수 있습니다.

---

## 단계 2: 상세 레이아웃 인식 OCR 실행

일반 텍스트는 훌륭하지만 각 단어가 페이지 어디에 위치하는지는 버려집니다. 인보이스, 양식, 다중 컬럼 잡지와 같은 경우 좌표, 라인 번호, 경우에 따라 폰트 정보까지 필요합니다. 여기서 `engine.RecognizeStructured()`가 등장합니다.

아래는 Tesseract의 **TSV** 출력을 얇게 래핑한 것으로, 페이지 → 라인 → 단어의 계층 구조를 제공하며 바운딩 박스를 보존합니다.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*왜 이렇게 하는가:*
- **Coordinates**를 사용하면 추출된 텍스트를 원본 이미지에 다시 매핑해 하이라이트하거나 삭제할 수 있습니다.
- **Line grouping**은 원본 레이아웃을 보존하므로 표나 컬럼을 재구성할 때 필수적입니다.
- 이 패스는 일반 패스보다 약간 느리지만 대부분의 문서는 몇 초 안에 완료됩니다.

---

## 단계 3: AI 후처리기로 OCR 오류 수정

최고의 OCR 엔진도 실수를 합니다—예를 들어 “rn”을 “m”으로, 다이아크리티컬을 놓치거나 단어가 분리되는 경우가 있습니다. AI 모델은 원시 문자열과 구조화 데이터를 살펴보고 불일치를 찾아 원래 좌표를 유지하면서 텍스트를 재작성할 수 있습니다.

아래는 **모의** 구현이며, 실제 LLM 호출로 교체하면 됩니다.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*이 단계가 OCR 정확도를 향상시키는 이유:*
- **Contextual fixes** – AI는 주변 단어를 기반으로 “l0ve”가 “love”일 가능성이 높다고 판단할 수 있습니다.
- **Coordinate preservation** – 레이아웃 정보를 유지하므로 PDF 주석과 같은 후속 작업이 정확하게 유지됩니다.
- **Iterative refinement** – 후처리기를 여러 번 실행하여 각 패스마다 더 많은 오류를 정리할 수 있습니다.

---

## 단계 4: 정제된 구조화 출력 반복 처리

이제 정리된 구조가 준비되었으니 최종 텍스트를 추출하는 일은 간단합니다. 아래 예시에서는 각 라인을 출력하지만 CSV로 저장하거나 데이터베이스에 넣거나 검색 가능한 PDF를 생성할 수도 있습니다.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**예상 출력** (단순한 1페이지 인보이스 가정):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

라인 브레이크와 컬럼 순서가 보존되고, AI 단계에서 “$15.00”이 “$15,00”으로 읽히는 일반적인 OCR 오류가 수정된 것을 확인할 수 있습니다.

---

## 이 워크플로우가 **OCR 정확도 향상**에 도움이 되는 방법

| Stage | What it fixes | Why it matters |
|------|---------------|----------------|
| **Plain text OCR** | 읽을 수 없는 페이지를 조기에 감지 | 희망 없는 입력을 건너뛰어 시간을 절약 |
| **Structured OCR** | 레이아웃 및 좌표 캡처 | 하이라이트, 삭제와 같은 후속 작업을 가능하게 함 |
| **AI post‑processor** | 맞춤법 교정, 분할된 단어 병합, 숫자 수정 | 노이즈가 많은 스캔에서 전체 문자 수준 정확도를 ~85 %에서 >95 %로 향상 |
| **Iteration** | 조정된 매개변수로 재실행 가능 | 특정 문서 유형에 맞게 파이프라인을 미세 조정 |

일반 텍스트 OCR, 레이아웃 인식 추출, AI 교정이라는 세 가지 개념을 결합하면 **OCR 정확도를 크게** 향상시킬 수 있습니다. 자체 신경망을 처음부터 만들 필요가 없습니다.

---

## 흔히 발생하는 실수와 전문가 팁

- **Pitfall:** 저해상도 이미지(≤150 dpi)를 Tesseract에 입력하면 깨진 출력이 나옵니다.  
  **Pro tip:** `Pillow`로 전처리하세요—OCR 전에 `Image.convert('L')`와 `Image.filter(ImageFilter.MedianFilter())`를 적용합니다.

- **Pitfall:** AI 후처리기가 도메인 특화 용어(예: “SKU123”)를 실수로 바꿀 수 있습니다.  
  **Pro tip:** 용어 화이트리스트를 구축하고 이를 LLM이나 `pyspellchecker`와 같은 맞춤법 검사 라이브러리에 전달합니다.

- **Pitfall:** 다중 컬럼 페이지가 하나의 라인으로 합쳐집니다.  
  **Pro tip:** Tesseract TSV 출력의 `block_num` 필드를 사용해 컬럼 경계를 감지하고 라인을 적절히 분할합니다.

- **Pitfall:** 대용량 PDF를 한 번에 모두 로드하면 메모리가 폭발합니다.  
  **Pro tip:** 페이지를 순차적으로 처리하세요—`pdf2image.convert_from_path(..., first_page=n, last_page=n)`를 루프에 사용합니다.

---

## 파이프라인 확장

다음 단계에 관심이 있다면 아래와 같은 확장을 고려해 보세요:

1. **Batch processing** – 전체 스크립트를 디렉터리를 순회하는 함수로 감싸고 `concurrent.futures`를 사용해 수천 개 파일을 병렬 처리합니다.
2. **Language models** – 간단한 difflib 휴리스틱을 OpenAI의 `gpt‑4o` 호출이나 로컬에 호스팅된 LLaMA 모델로 교체해 더 풍부한 컨텍스트 교정을 얻습니다.
3. **Export formats** – 정제된 구조를 검색 가능한 PDF로 작성합니다.

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 다룬 기술을 기반으로 하며, 단계별 설명과 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 도와줍니다.

- [Aspose.OCR을 사용한 언어별 이미지 텍스트 OCR 방법](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR for Java 고급 OCR 기술 사용법](/ocr/english/java/advanced-ocr-techniques/)
- [OCR 정확도 향상 – 영역 감지 모드](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-01-02
description: Python을 사용하여 문서에서 표를 추출합니다. PDF에서 표를 읽고 표 행을 반복하는 깔끔하고 재사용 가능한 솔루션을 배워보세요.
draft: false
keywords:
- extract table from document
- how to read tables from pdf
- how to iterate table rows
- pdf table extraction python
- document layout detection
language: ko
og_description: Python으로 문서에서 표 추출하기. 이 가이드는 PDF에서 표를 읽고 신뢰할 수 있는 엔진으로 표 행을 반복하는 방법을
  보여줍니다.
og_title: 문서에서 표 추출 – 완전한 파이썬 튜토리얼
tags:
- Python
- PDF
- Data Extraction
title: 문서에서 표 추출 – 단계별 파이썬 가이드
url: /ko/python/general/extract-table-from-document-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 문서에서 표 추출 – 완전한 파이썬 튜토리얼

문서에서 **표를 추출**해야 했지만 어디서 시작해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다—많은 개발자들이 표 안에 숨겨진 데이터를 포함한 PDF를 다룰 때 같은 장벽에 부딪힙니다. 이 튜토리얼에서는 **PDF에서 표를 읽는 방법**을 보여줄 뿐만 아니라 **표 행을 반복하는 방법**을 시연하는 실용적인 엔드‑투‑엔드 솔루션을 단계별로 안내합니다. 이를 통해 데이터를 원하는 곳으로 파이프할 수 있습니다.

예를 들어 여러 청구서에 각 라인 아이템 요약 표가 있다고 가정해 보세요. 그 행들을 CSV로 추출해 다운스트림 분석에 활용하고 싶을 것입니다. 이 가이드를 끝까지 따라 하면 바로 그런 재사용 가능한 스니펫을 얻을 수 있으며, 흔히 발생하는 함정을 피하는 팁도 몇 가지 제공됩니다.

## 배우게 될 내용

- 레이아웃 엔진을 사용해 문서 레이아웃을 감지합니다.  
- 포스트‑프로세서를 활용해 원시 감지를 정제하고 더 깨끗한 표 구조를 만듭니다.  
- 감지된 표의 각 행을 반복하며 셀 내용을 출력(또는 저장)합니다.  

외부 서비스 없이, 마법 같은 블랙박스 없이—그냥 순수 파이썬과 인기 OCR/레이아웃 라이브러리(예: **pdfplumber**, **pdfminer.six**, 혹은 이미 사용 중인 `engine`)만 있으면 됩니다. `recognize_layout()`와 `run_postprocessor()`를 구현한 `engine` 객체가 이미 있다면 코드를 바로 넣어 사용할 수 있습니다.

> **Pro tip:** 상용 SDK를 사용 중이라면 “table detection” 기능을 반드시 활성화하세요; 그렇지 않으면 원시 레이아웃에서 병합된 셀을 놓칠 수 있습니다.

---

## 1단계: 표 구조 감지 – 문서에서 표 추출

먼저 페이지에서 표가 위치한 곳을 알려주는 원시 레이아웃이 필요합니다. 대부분의 최신 PDF 라이브러리는 `recognize_layout()`와 같은 메서드를 제공하며, 이 메서드는 블록, 라인, 셀의 계층 구조를 반환합니다.

```python
# Step 1 – Detect the document layout using the engine
# ---------------------------------------------------
# `engine` is assumed to be an instantiated object from your PDF library.
# It could be pdfplumber, a custom OCR SDK, or any tool that supports layout detection.
raw_layout = engine.recognize_layout()
```

**왜 중요한가:**  
원시 레이아웃은 모든 텍스트 요소의 좌표를 제공하지만, 종종 잡음(헤더, 푸터, 표에 속하지 않은 문자 등)을 포함합니다. 그래서 다음 단계가 필수적입니다.

> **Common question:** *PDF에 페이지가 여러 개라면 어떻게 하나요?*  
> `recognize_layout()` 호출은 보통 페이지 객체 리스트를 반환합니다. 이를 순회하면서 각 페이지에 동일한 포스트‑프로세싱 로직을 적용하면 됩니다.

---

## 2단계: 감지 정제 – PDF에서 표 읽는 방법

`raw_layout`을 확보한 후에는 이를 정리해야 합니다. 대부분의 엔진은 조각난 셀을 병합하고, 관련 없는 텍스트를 제거하며, 올바른 `Table` 객체를 구축하는 포스트‑프로세서를 제공합니다.

```python
# Step 2 – Refine the detected layout with the post‑processor
# ----------------------------------------------------------
# The post‑processor returns an enhanced layout where tables are
# represented as a list of rows, each row being a list of Cell objects.
enhanced_layout = engine.run_postprocessor(raw_layout)
```

**왜 필요한가:**  
원시 레이아웃은 하나의 표 행을 수십 개의 작은 조각으로 보고할 수 있습니다. 포스트‑프로세서는 이러한 조각을 논리적인 셀로 그룹화해 나중에 행을 쉽게 반복할 수 있게 합니다.

> **Edge case:** 일부 PDF는 보이지 않는 테두리를 사용합니다. 행이 누락된 것이 보이면 엔진에 “detect invisible lines” 플래그를 활성화하세요(가능한 경우).

---

## 3단계: 표 행 반복 – 표 행을 반복하는 방법

이제 `enhanced_layout`이 깔끔해졌으니 데이터 추출은 아주 간단합니다. 아래 예시에서는 각 행을 순회하면서 셀 텍스트를 탭(`\t`)으로 연결해 출력합니다. `print`를 CSV 라이터, 데이터베이스 삽입 등 원하는 저장 로직으로 교체하면 됩니다.

```python
# Step 3 – Print the table contents row by row
# --------------------------------------------
# `enhanced_layout.table` is expected to be an iterable of rows.
# Each `row` is a list of Cell objects with a `.text` attribute.
for row in enhanced_layout.table:
    # Join each cell's text with a tab to align columns
    print("\t".join(cell.text for cell in row))
```

**예시 출력 (예시):**

```
Item	Qty	Price	Total
Widget A	2	$10.00	$20.00
Widget B	1	$15.00	$15.00
Service C	5	$8.00	$40.00
```

탭 구분 대신 CSV가 필요하면 `"\t".join(...)`을 `",".join(...)`으로 바꾸고 파일에 기록하면 됩니다.

---

## 전체 작동 예제

모든 코드를 하나로 합치면 아래와 같은 독립 실행형 스크립트가 됩니다. 사용 중인 라이브러리에 맞게 import와 엔진 초기화를 조정하세요.

```python
# --------------------------------------------------------------
# Full script: extract table from document and iterate rows
# --------------------------------------------------------------
import sys

# -----------------------------------------------------------------
# 1️⃣  Import or instantiate your PDF layout engine.
# Replace the placeholder with the actual library you use.
# -----------------------------------------------------------------
# Example with a fictional `pdf_engine` package:
# from pdf_engine import LayoutEngine
# engine = LayoutEngine(api_key="YOUR_KEY")
# -----------------------------------------------------------------
# For pdfplumber (open‑source) you could do:
# import pdfplumber
# engine = pdfplumber.open("sample.pdf")
# -----------------------------------------------------------------
# We'll keep it generic for the tutorial.
# -----------------------------------------------------------------

def extract_table(engine):
    """
    Detect, refine, and iterate over a table in a PDF document.
    Returns a list of rows, where each row is a list of cell strings.
    """
    # Detect layout
    raw_layout = engine.recognize_layout()

    # Refine layout
    enhanced_layout = engine.run_postprocessor(raw_layout)

    # Collect rows
    rows = []
    for row in enhanced_layout.table:
        rows.append([cell.text for cell in row])
    return rows

def main(pdf_path):
    # Initialise your engine – this will differ per library
    # Below is a stub; replace with real initialization.
    engine = initialize_engine(pdf_path)   # <-- implement this

    try:
        table_rows = extract_table(engine)
        for row in table_rows:
            print("\t".join(row))
    except Exception as e:
        print(f"❌ Extraction failed: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python extract_table.py <path-to-pdf>")
    else:
        main(sys.argv[1])
```

**교체해야 할 부분:**

- `initialize_engine(pdf_path)`: 선택한 라이브러리용 엔진 인스턴스를 생성합니다.  
- `engine.recognize_layout()` / `engine.run_postprocessor()`: 메서드 이름이 다르면 해당 이름을 사용하세요.

`python extract_table.py invoice.pdf` 명령으로 스크립트를 실행하면 탭으로 구분된 표가 깔끔히 출력되어 다운스트림 처리에 바로 사용할 수 있습니다.

---

## 이미지 설명

아래는 감지 파이프라인이 어떻게 구성되는지 보여주는 간단한 도식입니다.  
![extract table from document diagram showing raw layout → post‑processor → clean table]  

*Alt text:* *문서에서 표 추출 흐름도*  

---

## 자주 묻는 질문 및 엣지 케이스

| 질문 | 답변 |
|------|------|
| **PDF에 표가 여러 개 있으면 어떻게 하나요?** | `enhanced_layout.table`은 첫 번째 감지된 표만 포함할 수 있습니다. 라이브러리가 지원한다면 `enhanced_layout.tables`(복수형)를 순회하고 각 표에 동일한 행 반복 로직을 적용하세요. |
| **병합된 셀은 어떻게 처리하나요?** | 포스트‑프로세서는 보통 병합된 셀을 개별 항목으로 확장합니다. 그렇지 않다면 엔진의 `merge_cells` 플래그를 확인하거나 좌표 기반으로 인접 셀을 직접 연결하세요. |
| **스캔된 PDF에서도 표를 추출할 수 있나요?** | 가능합니다. 다만 레이아웃 감지 전에 OCR 단계가 필요합니다. 많은 SDK가 OCR과 레이아웃 감지를 한 번에 수행하도록 (`recognize_layout()`를 스캔 문서에 호출) 지원합니다. |
| **대량 배치 처리 시 성능이 걱정됩니다.** | 페이지를 병렬 처리하세요(예: `concurrent.futures` 사용). 가장 무거운 부분은 OCR이므로, 파일 간에 엔진 인스턴스를 유지해 무거운 모델 재초기화를 피하세요. |
| **추가 의존성을 설치해야 하나요?** | `pdfplumber`를 사용한다면 `pip install pdfplumber`로 설치합니다. 상용 SDK의 경우 공급업체 설치 가이드를 따르세요. |

---

## 결론

우리는 **문서에서 표를 추출**하는 방법을 레이아웃 감지 → 정제 → **표 행을 반복**하는 순서로 보여주었습니다. 데이터 웨어하우스로 전송하든, 보고서를 생성하든, PDF를 CSV로 변환하든 패턴은 동일합니다: 감지 → 정제 → 반복.

다음 단계로 탐색해 볼 내용:

- **PDF에서 표를 읽는 방법**에 스타일 정보(폰트, 색상)까지 포함하기.  
- 분석을 위해 **pandas DataFrame**으로 직접 내보내기.  
- 동일 파이프라인을 사용해 **표를 새 PDF에 다시 쓰기**(역방향 흐름).  

스크립트를 직접 몇 개의 PDF에 적용해 보면서 정적인 표를 어떻게 빠르게 실행 가능한 데이터로 바꿀 수 있는지 확인해 보세요. 즐거운 추출 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
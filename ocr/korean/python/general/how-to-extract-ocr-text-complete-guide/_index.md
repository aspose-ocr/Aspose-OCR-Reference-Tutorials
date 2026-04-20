---
category: general
date: 2026-02-22
description: AI 사후 처리로 OCR 텍스트를 추출하고 OCR 정확도를 향상시키는 방법을 배워보세요. 단계별 예제로 Python에서 OCR
  텍스트를 쉽게 정리할 수 있습니다.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: ko
og_description: 간단한 파이썬 워크플로와 AI 후처리를 사용하여 OCR 텍스트를 추출하고, OCR 정확도를 향상시키며, OCR 텍스트를
  정리하는 방법을 알아보세요.
og_title: OCR 텍스트 추출 방법 – 단계별 가이드
tags:
- OCR
- AI
- Python
title: OCR 텍스트 추출 방법 – 완전 가이드
url: /ko/python/general/how-to-extract-ocr-text-complete-guide/
---

exactly.

Let's craft the final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 텍스트 추출 방법 – 완전 프로그래밍 튜토리얼

스캔한 문서에서 **OCR을 추출하는 방법**을 고민해 본 적 있나요? 오타와 끊어진 줄이 뒤섞인 상태가 되지 않도록 말이죠. 당신만 그런 것이 아닙니다. 실제 프로젝트에서는 OCR 엔진의 원시 출력이 뒤섞인 단락처럼 보이며, 이를 정리하는 것이 큰 골칫거리가 됩니다.  

좋은 소식은? 이 가이드를 따라 하면 구조화된 OCR 데이터를 추출하고 AI 후처리를 실행해 **깨끗한 OCR 텍스트**를 얻을 수 있습니다. 또한 **OCR 정확도 향상** 기술도 다루어 첫 번째 시도부터 신뢰할 수 있는 결과를 얻을 수 있습니다.  

다음 몇 분 안에 필요한 모든 것을 다룰 것입니다: 필수 라이브러리, 전체 실행 가능한 스크립트, 흔히 발생하는 함정들을 피하는 팁. “문서를 참고하세요” 같은 모호한 방법은 없습니다—그냥 복사‑붙여넣기만 하면 바로 실행할 수 있는 완전한 자체 포함 솔루션입니다.

## 필요 사항

- Python 3.9+ (코드에 타입 힌트가 사용되었지만 이전 3.x 버전에서도 동작합니다)
- 구조화된 결과를 반환할 수 있는 OCR 엔진 (예: `pytesseract`와 `--psm 1` 플래그를 사용한 Tesseract, 혹은 블록/라인 메타데이터를 제공하는 상용 API)
- AI 후처리 모델 – 이 예시에서는 간단한 함수로 모킹하지만, OpenAI의 `gpt‑4o-mini`, Claude, 혹은 텍스트를 받아 정제된 출력을 반환하는 모든 LLM으로 교체할 수 있습니다
- 테스트용 샘플 이미지(PNG/JPG) 몇 장

이것들을 준비했다면, 바로 시작해 봅시다.

## OCR 추출 – 초기 가져오기

첫 번째 단계는 OCR 엔진을 호출하고 **구조화된 표현**을 요청하는 것입니다. 구조화된 결과는 블록, 라인, 단어 경계를 보존하므로 이후 정리가 훨씬 쉬워집니다.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **왜 이것이 중요한가:** 블록과 라인을 보존함으로써 단락이 시작되는 위치를 추측할 필요가 없습니다. `recognize_structured` 함수는 나중에 AI 모델에 전달할 수 있는 깔끔한 계층 구조를 제공합니다.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

스니펫을 실행하면 OCR 엔진이 본 첫 번째 라인이 정확히 출력되는데, 여기에는 종종 “OCR” 대신 “0cr”와 같은 인식 오류가 포함됩니다.

## AI 후처리를 통한 OCR 정확도 향상

이제 원시 구조화된 출력이 준비되었으니 AI 후처리기로 넘깁니다. 목표는 일반적인 실수를 교정하고, 구두점을 정규화하며, 필요에 따라 라인을 재구성함으로써 **OCR 정확도 향상**을 이루는 것입니다.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **프로 팁:** LLM 구독이 없으면 호출을 로컬 트랜스포머(예: `sentence‑transformers` + 파인튜닝된 교정 모델)나 규칙 기반 접근법으로 대체할 수 있습니다. 핵심 아이디어는 AI가 각 라인을 독립적으로 보게 하는 것으로, 이는 보통 **OCR 텍스트 정리**에 충분합니다.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

이제 훨씬 더 깔끔한 문장을 확인할 수 있습니다—오타가 교정되고, 불필요한 공백이 제거되며, 구두점이 올바르게 정리됩니다.

## 더 나은 결과를 위한 OCR 텍스트 정리

AI 교정 후에도 최종 정제 단계를 적용하고 싶을 수 있습니다: 비 ASCII 문자 제거, 줄 바꿈 통합, 연속 공백 압축. 이 추가 작업을 통해 출력이 NLP나 데이터베이스 적재와 같은 다운스트림 작업에 바로 사용할 수 있게 됩니다.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

`final_cleanup` 함수는 검색 인덱스, 언어 모델, 혹은 CSV 내보내기에 바로 넣을 수 있는 순수 문자열을 반환합니다. 블록 경계를 유지했기 때문에 단락 구조가 그대로 보존됩니다.

## 엣지 케이스 및 가정 시나리오

- **다중 컬럼 레이아웃:** 소스에 컬럼이 있는 경우 OCR 엔진이 라인을 뒤섞어 반환할 수 있습니다. TSV 출력에서 컬럼 좌표를 감지하고 라인을 재정렬한 뒤 AI에 전달하면 됩니다.
- **비 라틴 스크립트:** 중국어, 아라비아어와 같은 언어의 경우 LLM 프롬프트를 해당 언어에 맞는 교정을 요청하도록 전환하거나, 해당 스크립트에 파인튜닝된 모델을 사용하세요.
- **대용량 문서:** 각 라인을 개별적으로 보내면 속도가 느려질 수 있습니다. 라인을 배치(예: 요청당 10줄)로 묶어 LLM이 정제된 라인 리스트를 반환하도록 하세요. 토큰 제한을 항상 염두에 두세요.
- **블록 누락:** 일부 OCR 엔진은 단어 리스트만 반환합니다. 이 경우 `line_num` 값이 비슷한 단어들을 그룹화해 라인을 재구성하면 됩니다.

## 전체 작업 예시

모든 것을 하나로 합치면, 아래와 같은 단일 파일을 끝‑끝까지 실행할 수 있습니다. 자리표시자를 자신의 API 키와 이미지 경로로 교체하세요.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-04-26
description: OCR 결과를 후처리하고 좌표와 함께 텍스트를 추출하는 방법. 구조화된 출력과 AI 교정을 활용한 단계별 솔루션을 배워보세요.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: ko
og_description: OCR 결과를 후처리하고 좌표와 함께 텍스트를 추출하는 방법. 신뢰할 수 있는 워크플로를 위해 이 포괄적인 튜토리얼을
  따라보세요.
og_title: OCR 후처리 방법 – 완전 가이드
tags:
- OCR
- Python
- AI
- Text Extraction
title: OCR 후처리 방법 – 파이썬으로 좌표와 함께 텍스트 추출
url: /ko/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 후처리 방법 – 파이썬에서 좌표와 함께 텍스트 추출

원시 출력이 잡음이 많거나 정렬이 맞지 않아 **OCR 후처리 방법**이 필요했던 적이 있나요? 당신만 그런 것이 아닙니다. 인보이스 스캔, 영수증 디지털화, 혹은 AR 경험을 보강하는 등 많은 실제 프로젝트에서 OCR 엔진은 원시 단어들을 제공하지만, 여전히 이를 정리하고 각 단어가 페이지의 어느 위치에 있는지 추적해야 합니다. 여기서 구조화된 출력 모드와 AI 기반 후처리기가 결합되면 빛을 발합니다.

이 튜토리얼에서는 이미지에서 **좌표와 함께 텍스트를 추출**하고, AI 기반 교정 단계를 실행하며, 각 단어와 그 (x, y) 위치를 출력하는 완전하고 실행 가능한 파이썬 파이프라인을 단계별로 살펴보겠습니다. 누락된 import 없이, “문서를 참고하세요” 같은 모호한 설명 없이—오늘 바로 프로젝트에 적용할 수 있는 독립형 솔루션입니다.

> **Pro tip:** 다른 OCR 라이브러리를 사용한다면 “structured” 또는 “layout” 모드를 찾아보세요; 개념은 동일합니다.

---

## 사전 요구 사항

시작하기 전에 다음을 확인하세요:

| 요구 사항 | 왜 중요한가 |
|-------------|----------------|
| Python 3.9+ | 최신 구문 및 타입 힌트 |
| `ocr` library that supports `OutputMode.STRUCTURED` (예: 가상의 `myocr`) | 경계 상자 데이터에 필요 |
| AI post‑processing 모듈 (OpenAI, HuggingFace 또는 커스텀 모델 가능) | OCR 후 정확도 향상 |
| 이미지 파일 (`input.png`) (작업 디렉터리 내) | 읽어올 소스 파일 |

위 항목 중 익숙하지 않은 것이 있다면 `pip install myocr ai‑postproc` 로 플레이스홀더 패키지를 설치하면 됩니다. 아래 코드는 실제 라이브러리가 없어도 흐름을 테스트할 수 있도록 대체 스텁을 포함하고 있습니다.

## 단계 1: OCR 엔진에 구조화된 출력 모드 활성화  

첫 번째로 OCR 엔진에 단순 텍스트 이상의 정보를 제공하도록 지시합니다. 구조화된 출력은 각 단어와 해당 경계 상자 및 신뢰도 점수를 반환하며, 이는 이후 **좌표와 함께 텍스트를 추출**하기 위해 필수적입니다.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*왜 중요한가:* 구조화 모드가 없으면 긴 문자열만 얻을 수 있고, 이미지에 텍스트를 오버레이하거나 후속 레이아웃 분석에 필요한 공간 정보를 잃게 됩니다.

---

## 단계 2: 이미지 인식 및 단어, 박스, 신뢰도 캡처  

이제 이미지를 엔진에 전달합니다. 결과는 `text`, `x`, `y`, `width`, `height`, `confidence` 를 제공하는 단어 객체 리스트를 포함하는 객체입니다.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*예외 상황:* 이미지가 비어 있거나 읽을 수 없는 경우 `structured_result.words` 는 빈 리스트가 됩니다. 이를 확인하고 적절히 처리하는 것이 좋은 습관입니다.

---

## 단계 3: 위치를 보존하면서 AI 기반 후처리 실행  

최고의 OCR 엔진도 실수를 합니다—예를 들어 “O”와 “0” 구분이나 결합문자 누락 등. 도메인 특화 텍스트로 학습된 AI 모델은 이러한 오류를 교정할 수 있습니다. 중요한 점은 원래 좌표를 유지하여 공간 레이아웃이 그대로 유지된다는 것입니다.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*좌표를 보존하는 이유:* 많은 후속 작업(예: PDF 생성, AR 라벨링)에서 정확한 위치가 필요합니다. AI는 `text` 필드만 수정하고 `x`, `y`, `width`, `height`는 그대로 둡니다.

---

## 단계 4: 교정된 단어를 순회하며 텍스트와 좌표 표시  

마지막으로 교정된 단어들을 순회하면서 각 단어와 그 좌상단 코너 `(x, y)` 를 출력합니다. 이는 **좌표와 함께 텍스트를 추출** 목표를 달성합니다.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**예상 출력 (예시):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

각 줄은 교정된 단어와 원본 이미지에서의 정확한 위치를 보여줍니다.

## 전체 작동 예제  

아래는 모든 과정을 하나로 연결한 단일 스크립트입니다. 복사‑붙여넣기하고 import 문을 실제 라이브러리에 맞게 조정한 뒤 바로 실행할 수 있습니다.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**스크립트 실행**

```bash
python ocr_postprocess_demo.py
```

실제 라이브러리가 설치되어 있으면 스크립트가 `input.png` 를 처리합니다. 그렇지 않다면 스텁 구현을 통해 외부 의존성 없이 예상 흐름과 출력을 확인할 수 있습니다.

## 자주 묻는 질문 (FAQ)

| 질문 | 답변 |
|----------|--------|
| *Tesseract에서도 작동하나요?* | Tesseract 자체는 구조화된 모드를 기본 제공하지 않지만, `pytesseract.image_to_data` 같은 래퍼는 경계 상자를 반환하므로 동일한 AI 후처리기에 전달할 수 있습니다. |
| *좌상단 대신 우하단 코너가 필요하면 어떻게 하나요?* | 각 단어 객체는 `width`와 `height`도 제공합니다. `x2 = x + width`와 `y2 = y + height`를 계산하면 반대 코너를 얻을 수 있습니다. |
| *여러 이미지를 배치 처리할 수 있나요?* | 물론 가능합니다. `for image_path in Path("folder").glob("*.png"):` 루프로 단계들을 감싸고 파일별로 결과를 수집하면 됩니다. |
| *교정에 사용할 AI 모델은 어떻게 선택하나요?* | 일반 텍스트의 경우 OCR 오류에 대해 미세 조정된 작은 GPT‑2가 작동합니다. 도메인 특화 데이터(예: 의료 처방전)의 경우, 잡음‑깨끗한 쌍 데이터로 시퀀스‑투‑시퀀스 모델을 학습하십시오. |
| *AI 교정 후 신뢰도 점수가 유용한가요?* | 디버깅을 위해 원래 신뢰도를 유지할 수 있지만, 모델이 지원한다면 AI가 자체 신뢰도를 출력할 수도 있습니다. |

## 엣지 케이스 및 모범 사례  

1. **빈 이미지 또는 손상된 이미지** – 진행하기 전에 항상 `structured_result.words` 가 비어 있지 않은지 확인하세요.  
2. **비라틴 문자** – OCR 엔진이 대상 언어에 맞게 설정되어 있는지 확인하고, AI 후처리기도 동일한 스크립트에 대해 학습되어야 합니다.  
3. **성능** – AI 교정은 비용이 많이 들 수 있습니다. 같은 이미지를 재사용한다면 결과를 캐시하거나 AI 단계를 비동기로 실행하세요.  
4. **좌표 시스템** – OCR 라이브러리는 원점이 다를 수 있습니다(좌상단 vs. 좌하단). PDF나 캔버스에 오버레이할 때 이에 맞게 조정하세요.  

## 결론  

이제 **OCR 후처리 방법**과 신뢰할 수 있는 **좌표와 함께 텍스트를 추출**하는 완전한 레시피를 갖추었습니다. 구조화된 출력을 활성화하고 결과를 AI 교정 레이어에 통과시켜 원래 경계 상자를 보존함으로써, 잡음이 많은 OCR 스캔을 PDF 생성, 데이터 입력 자동화, 증강 현실 오버레이와 같은 후속 작업에 사용할 수 있는 깨끗하고 공간 정보를 가진 텍스트로 변환할 수 있습니다.

다음 단계가 준비되셨나요? 스텁 AI를 OpenAI `gpt‑4o‑mini` 호출로 교체하거나 파이프라인을 FastAPI에 통합해 보세요.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
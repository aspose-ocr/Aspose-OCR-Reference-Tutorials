---
category: general
date: 2026-03-18
description: 기본 OCR 파이썬 튜토리얼은 TIFF를 텍스트로 변환하고, 이미지 OCR을 로드하며, GPU 레이어를 설정하고, Aspose
  AI로 선행 0을 수정하는 방법을 보여줍니다.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: ko
og_description: 기본 OCR 파이썬 튜토리얼은 TIFF 파일을 깨끗한 텍스트로 변환하고, 이미지를 로드하며, GPU 레이어를 설정하고,
  앞에 붙은 0을 수정하는 과정을 안내합니다.
og_title: 기본 OCR 파이썬 – TIFF를 텍스트로 변환
tags:
- OCR
- Python
- AI
- Aspose
title: 기본 OCR 파이썬 – TIFF를 텍스트로 변환
url: /ko/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – AI 후처리를 통한 TIFF 텍스트 변환

스캔한 문서에서 **basic ocr python**을 수행할 방법을 찾고 계신가요? 이 가이드에서는 Aspose OCR과 AI 후처리기를 사용해 TIFF 파일을 깔끔하고 검색 가능한 텍스트로 변환하는 과정을 단계별로 살펴봅니다.  

원시 출력에 오타나 이상한 기호가 많이 섞여 있어 **convert TIFF to text**에 어려움을 겪은 적이 있다면 혼자가 아닙니다. 또한 **load image OCR**을 수행하고 엔진을 **set GPU layers**로 조정하는 방법, 그리고 인보이스 번호에 흔히 나타나는 **fix leading zeroes** 방법도 함께 보여드립니다.

## 배울 내용

- 인쇄된 문서용 Aspose OCR 엔진을 초기화하는 방법.  
- TIFF 파일에서 **load image OCR**을 수행하고 원시 텍스트를 얻는 정확한 단계.  
- AI 모델을 구성하고 자동으로 다운로드하며, 빠른 추론을 위해 **set GPU layers**를 설정하는 방법.  
- 내장 맞춤법 검사와 **fix leading zeroes**를 수행하는 사용자 정의 함수를 추가하는 방법.  
- OCR 결과를 정리하고 리소스를 올바르게 해제하는 방법.  

이 튜토리얼을 마치면 어떤 TIFF 파일이든 깔끔하고 검색 가능한 텍스트로 변환하는 재사용 가능한 Python 스크립트를 하나 얻게 됩니다—수동 복사‑붙여넣기는 필요 없습니다.  

### 사전 요구 사항

- Python 3.8+이 머신에 설치되어 있음.  
- `aspose-ocr` 패키지 (`pip install aspose-ocr`).  
- 옵션: **set GPU layers**를 사용하려면 최소 4 GB VRAM을 가진 GPU가 필요합니다; 그렇지 않으면 코드는 자동으로 CPU로 전환됩니다.  

---

## basic ocr python – 이미지 로드 및 텍스트 인식

먼저 **load image OCR**을 수행해 엔진이 픽셀을 읽을 수 있도록 해야 합니다. Aspose의 `OcrEngine`은 다양한 형식을 지원하지만 여기서는 스캔된 인보이스에 가장 흔히 사용되는 TIFF에 초점을 맞춥니다.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** 다중 페이지 TIFF를 다룰 경우, Aspose가 각 페이지를 순차적으로 자동 처리하므로 별도의 루프를 작성할 필요가 없습니다.

이미지가 로드되었으니 이제 기본 인식 과정을 실행해 보겠습니다.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

다음과 같은 결과가 표시됩니다:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

문자 앞에 있는 *zeroes*를 보셨나요? 이는 나중에 정리할 전형적인 OCR 아티팩트입니다.

![basic ocr python 워크플로우](/images/ocr-workflow.png "basic ocr python 워크플로우 다이어그램")

---

## Step 2: TIFF를 텍스트로 변환 – AI 후처리 준비

원시 OCR은 유용하지만 대부분의 프로덕션 파이프라인에서는 다듬어진 버전이 필요합니다. Aspose는 Hugging Face에서 모델을 다운로드하고 GPU에서 실행하며 맞춤법 검사를 자동으로 적용할 수 있는 `AsposeAI` 래퍼를 제공합니다.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### `set GPU layers`가 중요한 이유

`gpu_layers` 파라미터는 하부 GGUF 모델에게 GPU에 유지할 트랜스포머 레이어 수를 알려줍니다. 레이어가 많을수록 추론 속도가 빨라지지만 VRAM 사용량도 증가합니다. 노트북처럼 사양이 제한된 경우 값을 `10`으로 낮추거나 아예 생략해 CPU에서 실행하도록 할 수 있습니다.

---

## Step 3: 맞춤법 검사 적용 및 **fix leading zeroes**

Aspose AI는 대부분의 영어 오타를 잡아주는 내장 맞춤법 검사기를 포함하고 있습니다. 그러나 인보이스 코드와 같이 앞에 `0`이 붙어 있어 `O`로 바꿔야 하는 경우와 같은 도메인 특화 수정은 사용자 정의 후처리가 필요합니다.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Why this works:** 정규식은 단어 경계(`\b`) 뒤에 0이 오고 정확히 세 개의 대문자가 이어지는 패턴을 찾습니다. 그런 다음 0을 문자 “O”로 교체합니다. 다른 특수 케이스(예: `0[0-9]{2}`와 같은 잘못 인식된 숫자)에도 패턴을 확장할 수 있습니다.

---

## Step 4: AI 후처리기로 OCR 결과 정리

이제 모든 요소를 결합합니다: **basic ocr python**에서 얻은 원시 문자열, 맞춤법 검사, 그리고 제로 교정. `run_postprocessor` 메서드는 다운스트림 시스템에서 바로 사용할 수 있는 정제된 버전을 반환합니다.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

후처리 후 전형적인 출력:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

앞에 있던 0가 `O`로 바뀌었고 일반적인 오타가 수정된 것을 확인할 수 있습니다. 이제 텍스트를 검색 엔진에 색인하거나 데이터 추출 파이프라인에 투입하기에 적합합니다.

---

## Step 5: AI 리소스 해제 – GPU를 행복하게 유지

장시간 실행되는 서비스에서 여러 OCR 작업을 수행한다면 작업이 끝난 뒤 모델의 GPU 메모리를 해제하는 것이 좋은 습관입니다.

```python
ocr_ai.free_resources()
```

이 단계를 건너뛰면 특히 **set GPU layers** 값을 높게 설정했을 때 이후 호출에서 “out‑of‑memory” 오류가 발생할 수 있습니다.

---

## 선택적 변형 및 엣지 케이스

| 상황 | 변경 내용 |
|-----------|----------------|
| **Handwritten documents** | `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)`을 사용하고 `PRINTED` 대신 적용합니다. |
| **No GPU available** | `gpu_layers=0`으로 설정하거나 인자를 생략하면 모델이 CPU에서 실행됩니다(속도는 느리지만 안전). |
| **Different language** | Hugging Face 저장소 ID를 언어별 모델로 교체합니다. 예: `microsoft/Florence-2-base`. |
| **Batch processing** | `for file in glob("*.tif"):` 루프로 단계를 감싸고 결과를 리스트나 CSV에 누적합니다. |
| **More complex zero patterns** | `invoice_fix`에 추가 정규식을 넣어 확장합니다. 예: `r"\b0+([A-Z]{2,})\b"`는 다중 선행 제로를 처리합니다. |

---

## 결론

우리는 **basic ocr python** 파이프라인을 완성했습니다. TIFF를 로드하고 원시 텍스트를 추출한 뒤 **set GPU layers**를 활용해 성능을 높인 AI 모델로 정제했습니다. 커스텀 후처리를 통해 **fix leading zeroes**를 수행했으며, 이는 종종 간과되어 다운스트림 분석을 방해하는 작은 디테일입니다.

다양한 실험을 자유롭게 해보세요: 더 높은 정확도를 위한 다른 양자화(`float16`)를 시도하거나, 맞춤법 검사를 도메인 전용 사전으로 교체하거나, 여러 커스텀 교정 함수를 체인처럼 연결해볼 수 있습니다. 패턴은 동일합니다—로드, 인식, AI 설정, 후처리, 정리.

**다음 단계**로 고려해볼 내용:

- 정제된 출력을 데이터베이스나 Elasticsearch 인덱스와 연동하기.  
- 동일한 방식을 사용해 다국어 PDF에 대해 **convert TIFF to text** 수행하기.  
- Flask 또는 FastAPI로 UI를 추가해 비기술 사용자도 파일을 업로드하고 즉시 정제된 텍스트를 받을 수 있게 하기.  

행복한 코딩 되시길 바라며, OCR 결과가 언제나 선명하고 제로‑프리이길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
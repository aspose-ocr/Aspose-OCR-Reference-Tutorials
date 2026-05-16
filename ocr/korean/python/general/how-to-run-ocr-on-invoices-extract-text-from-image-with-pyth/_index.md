---
category: general
date: 2026-01-07
description: 청구서 처리를 위해 OCR을 실행하고 이미지에서 텍스트를 추출하는 방법. OCR 정확도를 향상시키는 방법, OCR을 위한 이미지
  로드, 그리고 청구서 OCR을 효율적으로 처리하는 방법을 배웁니다.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: ko
og_description: 청구서에서 OCR을 단계별로 실행하는 방법. 이미지에서 텍스트를 추출하고, OCR 정확도를 향상시키며, Aspose AI를
  사용해 OCR을 위한 이미지를 로드합니다.
og_title: 청구서에서 OCR 실행 방법 – 완전한 파이썬 가이드
tags:
- OCR
- Python
- Image Processing
title: 청구서에서 OCR 실행 방법 – 파이썬으로 이미지에서 텍스트 추출
url: /ko/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 청구서에서 OCR 실행 방법 – Python으로 이미지에서 텍스트 추출

스캔한 청구서에 **OCR을 실행**하고 깨끗하고 검색 가능한 텍스트를 얻는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 원시 OCR 출력에 맞춤법 오류, 깨진 줄 바꿈, 누락된 구두점 등이 뒤섞여 있는 상황에 부딪히곤 합니다. 이번 튜토리얼에서는 **이미지에서 텍스트를 추출**할 뿐만 아니라 **Aspose AI 모델**을 활용한 후처리로 OCR 정확도를 **향상**시키는 풀스택 솔루션을 단계별로 살펴보겠습니다.

**이미지를 OCR에 로드**하고 내장 엔진을 실행한 뒤, 가벼운 맞춤법 검사기를 적용해 결과를 다운스트림 분석에 바로 사용할 수 있도록 만드는 과정을 보여드립니다. 최종적으로는 어떤 청구서 처리 파이프라인에도 끼워 넣을 수 있는 재사용 가능한 스크립트를 얻게 됩니다.

> **필요한 준비물**  
> * Python 3.9 이상  
> * `aspose-ocr` 및 `aspose-ai` 패키지 (`pip`로 설치)  
> * 청구서 이미지 (PNG, JPEG, 또는 TIFF) – 예시로 `sample_invoice.png` 사용  
> * 선택 사항: 모델 추론 속도를 높이기 위한 최소 4 GB VRAM을 갖춘 GPU (CPU에서도 동작)

---

## Step 1: Install Required Packages and Prepare the Environment

**OCR에 이미지를 로드**하기 전에 필요한 라이브러리가 모두 준비돼 있는지 확인해야 합니다. Aspose OCR 엔진은 간단한 Python 래퍼와 함께 제공되며, AI 후처리는 Hugging Face 양자화 모델에 의존합니다.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Pro tip:** GPU 가속을 사용할 계획이라면 CUDA 지원이 포함된 `torch`를 설치하세요 (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Step 2: Load the Invoice Image

이미지를 로드하는 과정은 간단하지만, 경로를 raw 문자열(`r"..."`)로 명시적으로 지정하는 이유를 언급할 가치가 있습니다. 이는 Windows 경로에서 발생할 수 있는 이스케이프 문자 오류를 방지합니다.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*왜 중요한가:* `ocr.Image.load`를 사용하면 Aspose가 권장하는 기본 전처리(이진화, 기울기 보정)가 자동으로 적용되어 **OCR 정확도가 향상**됩니다. AI 마법이 적용되기 전 단계입니다.

---

## Step 3: Run the Built‑In OCR Engine

이제 실제로 **OCR을 실행**하고 원시 텍스트를 캡처합니다. 이 단계에서는 일반적인 OCR 실행 결과—줄 바꿈이 뒤죽박죽이고 가끔 맞춤법 오류가 섞인—를 확인할 수 있습니다.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Typical raw output** (truncated for brevity):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

“Invoice”가 “Invo1ce”처럼 보이거나 구두점이 누락된 것을 발견할 수 있을 겁니다. 여기서 AI 후처리가 등장합니다.

---

## Step 4: Configure the Aspose AI Model

사용할 AI 모델은 **Qwen2.5‑3B‑Instruct‑GGUF**이며, 중급 GPU에서도 원활히 구동되는 경량 지시‑튜닝 LLM입니다. 아래 설정은 Aspose가 모델을 어디서 가져올지, 몇 개의 레이어를 GPU에 올릴지, 긴 단락을 처리하기 위한 컨텍스트 크기를 지정합니다.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Why this config?**  
> * `gpu_layers=30`은 속도와 메모리 사용의 균형을 맞춥니다—대부분의 추론은 GPU에서 수행되고, 나머지 레이어는 CPU에 남겨 OOM 오류를 방지합니다.  
> * `context_size=4096`은 모델이 청구서 전체를 한 번에 볼 수 있게 하여 중요한 필드가 잘려 나가는 일을 방지합니다.

---

## Step 5: Create a Simple Spell‑Check Post‑Processor

AI 호출을 `simple_spell_check`라는 작은 함수로 감쌀 것입니다. 프롬프트는 의도적으로 간결하게 “Correct spelling and punctuation:” 뒤에 원시 OCR 텍스트를 붙입니다. 모델은 정제된 버전을 반환합니다.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**How it works:** `ai.run_prompt`는 로컬에 로드된 LLM에 프롬프트를 보내고, 맞춤법이 교정되고 구두점이 보완된 단일 문자열을 반환합니다. 또한 보다 자연스러운 줄 바꿈 레이아웃을 제공합니다.

---

## Step 6: Apply the Post‑Processor to the Raw OCR Text

이제 마법이 시작됩니다. 원시 OCR 출력을 후처리 함수에 전달하고 향상된 결과를 출력합니다.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Sample enhanced output**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

수정된 “Invoice” 맞춤법, 올바른 콜론 사용, 일관된 줄 바꿈을 확인할 수 있습니다—신뢰할 수 있는 다운스트림 파싱에 바로 사용할 수 있는 형태입니다.

---

## Step 7: Clean Up Resources

OCR 엔진과 AI 모델 모두 네이티브 리소스를 할당합니다. 특히 장시간 실행되는 서비스에서는 작업이 끝난 뒤 이를 해제하는 것이 좋은 습관입니다.

```python
ai.free_resources()
engine.dispose()
```

---

## Full Script – Ready to Paste

아래는 모든 단계를 하나로 묶은 완전한 실행 가능한 스크립트입니다. `invoice_ocr.py`라는 파일명으로 저장하고, `YOUR_DIRECTORY`를 청구서 이미지가 들어 있는 폴더 경로로 바꾼 뒤 `python invoice_ocr.py`로 실행하세요.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

스크립트를 실행하면 잡음이 많은 원시 OCR 덤프와 정제된 **improved OCR accuracy** 버전이 나란히 표시됩니다.

---

## Frequently Asked Questions & Edge Cases

### 1. What if my invoice image is a multi‑page PDF?

Aspose OCR은 PDF 페이지를 직접 로드할 수 있습니다. 이미지 로드 라인을 다음과 같이 교체하세요:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

`page_index`를 순회하면서 각 페이지를 차례로 처리하면 됩니다.

### 2. My GPU runs out of memory—can I use CPU only?

물론 가능합니다. `AsposeAIModelConfig`에서 `gpu_layers=0`으로 설정하면 모델이 전적으로 CPU에서 실행됩니다. 속도는 느려지지만 저사양 하드웨어에서도 안전하게 동작합니다.

### 3. How do I handle non‑English invoices?

언어‑특화 모델로 모델 레포지토리 ID를 교체하면 됩니다. 예를 들어 다국어 지원을 원한다면 `"mistralai/Mistral-7B-Instruct-v0.2"`를 사용하세요. 파이프라인의 나머지 부분은 그대로 유지됩니다.

### 4. Can I chain multiple post‑processors (e.g., format dates, extract totals)?

가능합니다. `ai.set_post_processor`는 호출 가능한 함수 리스트를 받습니다. 예시:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

출력은 먼저 맞춤법이 교정되고, 그 다음에 총액이 추출되는 순서로 처리됩니다.

---

## Performance Tips & Best Practices

| Tip | Why it Helps |
|-----|---------------|
| **Batch multiple invoices** – load them into a list and process in a loop. | Reduces Python interpreter overhead and keeps the AI model warm in memory. |
| **Cache the model** – avoid calling `initialize` repeatedly in a web service. | Model loading can take ~30 seconds; caching yields instant responses. |
| **Resize large images** to 1500 px width before OCR. | Smaller images speed up both OCR and AI inference without sacrificing accuracy. |
| **Set `allow_auto_download="false"` in production** – ship the model with your deployment. | Guarantees deterministic startup times and avoids network hiccups. |

---

## Conclusion

우리는 **청구서에 OCR을 실행**하는 전체 흐름을 다루었습니다. 이미지 로드부터 AI 기반 맞춤법 검사기로 결과를 다듬는 과정까지. 이 단계를 따르면 **이미지에서 텍스트를 추출**하고 **OCR 정확도를 향상**시켜, 어떤 Python 기반 워크플로에서도 청구서 OCR을 원활히 처리할 수 있습니다.

다양한 청구서 레이아웃—예를 들어 손글씨 영수증이나 스캔된 계약서—으로 직접 실험해 보세요. 동일한 파이프라인이 최소한의 수정만으로도 적용 가능하므로, 잘 구조화된 OCR + AI 조합이 문서 자동화 프로젝트에 얼마나 다재다능한 도구인지 확인할 수 있습니다.

이 가이드가 도움이 되었다면 팀원과 공유하거나 Aspose 패키지를 호스팅하는 레포지토리에 ⭐를 남겨 주세요.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
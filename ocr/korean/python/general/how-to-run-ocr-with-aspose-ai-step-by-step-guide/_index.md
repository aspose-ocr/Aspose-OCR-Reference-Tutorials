---
category: general
date: 2026-02-09
description: Aspose AI와 Hugging Face 모델을 사용하여 OCR을 실행하는 방법 – Hugging Face 모델을 다운로드하고,
  OCR 오류를 수정하며, GPU 메모리를 해제하는 방법을 배웁니다.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: ko
og_description: Aspose AI를 사용한 OCR 실행 방법은 첫 번째 단락에 설명되어 있습니다 – hugging face 모델을 다운로드하고,
  OCR 오류를 수정하며, GPU 메모리를 해제하는 방법을 알아보세요.
og_title: Aspose AI로 OCR 실행하는 방법 – 완전 가이드
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Aspose AI로 OCR 실행하기 – 단계별 가이드
url: /ko/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose AI로 OCR 실행하기 – 완전 가이드

스캔한 청구서에서 **OCR을 실행하는 방법**을 궁금해 본 적이 있나요? 오타를 고치는 데 몇 시간을 들이지 않고도 완벽하게 깨끗한 숫자를 얻고 싶으신가요? 당신만 그런 것이 아닙니다. 많은 실제 프로젝트에서 기존 OCR 엔진이 출력하는 원시 텍스트는 여전히 잡다한 문자, 깨진 통화 기호, 혹은 뒤섞인 숫자를 포함하고 있습니다—특히 원본 이미지가 노이즈가 많을 때 더욱 그렇습니다.  

좋은 소식은 LLM을 Aspose OCR에 연결하고, Hugging Face 모델을 실시간으로 다운로드하여 AI가 출력 결과를 다듬어 줄 수 있다는 것입니다. 이 튜토리얼에서는 모델을 가져오는 단계부터(예, **download hugging face model**을 자동으로 수행하는 방법을 보여드립니다) 작업이 끝난 후 GPU 리소스를 해제하는 과정까지 전체 파이프라인을 단계별로 살펴봅니다. 최종적으로 **corrects OCR errors**를 수행하고, 보통 수준의 GPU에서도 빠르게 실행되며, 사용 후 스스로 정리하여 메모리를 낭비하지 않는 재현 가능한 스크립트를 얻을 수 있습니다.

## 배울 내용

- Aspose AI가 Hugging Face에서 **Qwen2.5‑3B‑Instruct‑GGUF** 모델을 가져오도록 구성합니다.
- 이미지 파일에 대해 표준 Aspose OCR 엔진을 실행합니다.
- 숫자와 통화 기호를 그대로 유지하는 맞춤형 LLM 프롬프트를 사용합니다.
- 내장된 **free gpu memory** 루틴으로 GPU 메모리를 해제합니다.
- 멀티 페이지 PDF나 저사양 GPU와 같은 엣지 케이스에 맞게 워크플로를 조정합니다.

> **Prerequisites** – Python 3.9+, `aspose-ocr` 패키지, 첫 모델 다운로드를 위한 인터넷 접속, 최소 4 GB VRAM을 가진 GPU(선택 사항이지만 권장). GPU가 없을 경우, 스크립트는 남은 레이어를 CPU로 자동 전환합니다.

---

## OCR 실행 및 결과 향상 방법

아래는 완전한 실행 가능한 Python 스크립트입니다. `ocr_with_ai.py`라는 파일명으로 저장하고, 자리표시자 경로를 자신의 파일 경로로 교체하세요.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** `gpu_layers` 매개변수를 사용하면 GPU에 유지할 트랜스포머 레이어 수를 결정할 수 있습니다. 메모리 부족 오류가 발생하면 이 값을 낮추고 나머지는 CPU에서 실행됩니다 – 이후 `ai.free_resources()`로 **free gpu memory**를 여전히 수행할 수 있습니다.

### 예상 출력

샘플 청구서에 스크립트를 실행하면 다음과 같은 결과가 나옵니다:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

AI가 `$1O0.00`의 “O”를 올바른 0으로 교정하고 달러 기호는 그대로 유지한 것을 확인하세요. 이것이 금융 문서에서 **correct OCR errors**의 핵심입니다.

---

## Hugging Face 모델 다운로드 – 내부 동작 원리

`allow_auto_download="true"`를 설정하면 Aspose AI 래퍼가 `directory_model_path`를 확인합니다. 모델 파일이 없으면 Hugging Face Hub에 연결해 `Qwen2.5‑3B‑Instruct‑GGUF`의 **int8‑quantized** 버전을 가져와 로컬에 저장합니다. 이 일회성 다운로드는 보통 2 GB 이하이며, 보통 수준의 SSD에서도 충분히 가능합니다.

> **Why int8?** 8‑bit 양자화는 메모리 사용량을 크게 줄여줍니다—처리 후 **free gpu memory**를 원할 때 필수적입니다. 트레이드오프는 정확도가 약간 감소하는 것이지만, OCR 텍스트 후처리에서는 영향이 거의 없습니다.

모델을 직접 호스팅하고 싶다면 `.gguf` 파일을 `YOUR_DIRECTORY/Models`에 넣기만 하면 Aspose가 다시 인터넷에 접속하지 않고도 해당 파일을 사용합니다.

---

## GPU 해제 방법 – 모범 사례

많은 워크스테이션에서 GPU 자원은 공유 자원입니다. 스크립트가 끝난 뒤 텐서가 남아 있으면 이후 작업에서 “CUDA out of memory” 오류가 발생할 수 있습니다. `ai.free_resources()` 호출은 다음 세 가지 작업을 수행합니다:

1. **Disposes the underlying transformer** – 모든 GPU‑상주 가중치가 해제됩니다.
2. **Clears the PyTorch cache** – 내부적으로 `torch.cuda.empty_cache()`가 호출됩니다.
3. **Deletes temporary files** – 다운로드 중 생성된 디스크 캐시가 삭제됩니다.

Aspose AI와 다른 PyTorch 작업을 혼합하는 경우 `torch.cuda.empty_cache()`를 수동으로 호출할 수도 있지만, 내장 메서드만으로도 보통 충분합니다.

---

## 단계별 워크스루 (보조 키워드 포함 H2)

### Hugging Face 모델 자동 다운로드

`AsposeAIModelConfig` 생성자는 Hugging Face API와의 복잡성을 숨깁니다. 스크립트를 처음 실행할 때 인터넷에 연결되어 있는지 확인하세요. 이후 모델은 `YOUR_DIRECTORY/Models`에 저장되며, 다음 실행부터는 즉시 시작됩니다.

### 추론 후 GPU 메모리 해제

이 코드를 장기 실행 서비스(예: Flask API) 안에서 사용할 경우, 각 요청 후 `ai.free_resources()`를 호출하세요. 이는 메모리 누수를 방지하고 다음 요청이 동일한 GPU를 문제 없이 재사용하도록 보장합니다.

### 맞춤 프롬프트로 OCR 오류 교정

우리의 `financial_prompt` 함수는 `prompt`라는 단일 키를 가진 딕셔너리를 반환합니다. 이를 원하는 도메인에 맞게 조정할 수 있습니다:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

`ai.set_post_processor(...)`에서 함수 이름을 교체하면 의료 기록에 대한 **correct OCR errors** 파이프라인을 얻을 수 있습니다.

### 멀티 페이지 PDF에서 OCR 실행 방법

Aspose OCR은 기본적으로 PDF를 처리할 수 있습니다:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

원시 문자열을 얻은 후, 동일한 LLM 후처리기가 각 페이지 텍스트를 정리합니다. 추가 코드가 필요 없습니다.

### GPU가 없을 때 – GPU 해제 방법 (GPU가 없어도 적용 가능)

CPU 전용 머신에서도 `ai.free_resources()`를 호출해도 무해합니다. 내부 캐시를 정리하여 RAM을 해제할 수 있습니다. 따라서 **how to free gpu** 조언은 보편적으로 적용됩니다: 항상 사용 후 정리하세요.

---

## 흔히 발생하는 문제와 해결 방법

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑Memory on GPU** | `gpu_layers`가 카드에 비해 너무 높게 설정됨 | `gpu_layers`를 10 또는 5로 낮추고 나머지는 CPU에서 실행하도록 합니다. |
| **Model never downloads** | 기업 방화벽이 huggingface.co에 대한 HTTPS를 차단함 | 다른 네트워크에서 모델을 수동으로 다운로드한 뒤 `directory_model_path`를 로컬 폴더로 지정합니다. |
| **Numbers get corrupted** | 프롬프트가 숫자를 유지한다는 내용이 충분히 명시되지 않음 | 프롬프트에 “모든 숫자 값과 통화 기호를 그대로 유지”라는 문구를 추가합니다. |
| **`free_resources` raises an exception** | 구버전 Aspose OCR 사용 | `aspose-ocr` 최신 패키지로 업그레이드 (pip install --upgrade aspose-ocr) |

---

## 전체 예제 요약

다시 한 번 스크립트를 보여드리며, 이번에는 각 라인을 설명하는 인라인 주석을 포함했습니다:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## 결론

우리는 Aspose와 함께 **how to run OCR**를 수행하고, 필요 시 Hugging Face 모델을 다운로드하며, **corrects OCR errors**를 수행하는 프롬프트를 만들고, 마지막으로 **free gpu memory**를 통해 워크스테이션이 반응성을 유지하도록 했습니다. 전체 워크플로는 단일 독립형 Python 파일에 들어가며—외부 스크립트 없이, 모델을 수동으로 다루지 않고, GPU 할당이 남지 않습니다.

다음 단계는? `financial_prompt`를 다른 것으로 교체해 보세요:

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
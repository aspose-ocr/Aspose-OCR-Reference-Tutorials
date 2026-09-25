---
category: general
date: 2026-01-12
description: Aspose OCR와 가벼운 Hugging Face 모델을 사용하여 청구서 이미지에서 OCR을 실행하고 텍스트를 추출하는 방법.
  모델 다운로드, OCR 오류 수정, 이미지에 대한 OCR 수행 방법을 배웁니다.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: ko
og_description: 청구서 이미지에서 OCR을 실행하고 텍스트를 추출하며 Hugging Face LLM으로 오류를 수정하는 방법. 완벽한
  결과를 위한 전체 가이드를 따라보세요.
og_title: 청구서 이미지에 OCR 적용하는 방법 – 전체 튜토리얼
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: 청구서 이미지에서 OCR 실행 방법 – 완전한 단계별 가이드
url: /ko/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 청구서 이미지에서 OCR 수행하기 – 완전 단계별 가이드

스캔한 청구서에서 **OCR을 실행**하고, 수시간 걸리는 정제 없이 깨끗하고 검색 가능한 텍스트를 얻는 방법이 궁금하셨나요? 여러분만 그런 것이 아닙니다. 실제 프로젝트에서는 원시 OCR 결과에 “O”가 “0”으로, “l”이 “1”로 잘못 인식되거나 전체 단어가 뒤섞이는 경우가 흔합니다. 좋은 소식은? 몇 줄의 파이썬 코드만으로 **이미지에서 OCR 수행**은 물론, Hugging Face의 경량 모델을 이용해 자동으로 **OCR 오류를 교정**할 수 있다는 점입니다.

이 튜토리얼에서는 청구서 이미지를 로드하고, 원시 텍스트를 추출하고, 양자화된 모델을 다운로드하고, 결과를 다듬어 최종적으로 다운스트림 처리에 바로 사용할 수 있는 완벽한 전사본을 얻는 전 과정을 단계별로 살펴봅니다. 끝까지 따라오시면 **청구서 PDF 또는 PNG**에서 텍스트를 한 번에 추출하는 재현 가능한 스크립트를 만들 수 있습니다.

## 사전 요구 사항 및 설정

시작하기 전에 다음을 준비하세요:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | 최신 문법 및 타입 힌트 지원 |
| `aspose-ocr` 패키지 | 예제에서 사용하는 `ocr.OcrEngine` 제공 |
| `aspose-ai` 패키지 | `AsposeAI` 후처리기 제공 |
| GPU 접근 권한 (선택) | LLM 레이어 가속; 없으면 CPU에서도 동작 |
| 인터넷 연결 (첫 실행 시) | **Hugging Face 모델 다운로드** 자동 수행 필요 |

필요한 라이브러리는 다음과 같이 설치합니다:

```bash
pip install aspose-ocr aspose-ai
```

> **팁:** GPU에서 LLM을 실행하려면 CUDA 지원 `torch`를 설치하세요 (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

환경이 준비되었으니, 이제 코드를 살펴보겠습니다.

---

## Step 1 – OCR 엔진 초기화 및 청구서 이미지 로드

먼저 Aspose OCR 엔진 인스턴스를 만들고 처리할 파일을 지정합니다. 이 단계가 **이미지에서 OCR 수행**의 기반이 됩니다.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **왜 중요한가:** `load_image`는 PNG, JPEG, TIFF, 심지어 PDF 페이지까지 지원해 형식에 구애받지 않고 **이미지에서 OCR 수행**이 가능합니다.

---

## Step 2 – 기본 OCR 실행으로 원시 텍스트 캡처

이미지가 로드되면 엔진이 원시 전사본을 생성합니다. 이 출력은 보통 잡음이 많아 이후 교정 단계가 필요합니다.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

예시 원시 출력은 다음과 같습니다:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

숫자 “0”이 문자 “O” 자리로 나타나는 것을 보셨나요? 바로 이런 실수를 나중에 수정하게 됩니다.

---

## Step 3 – 경량 LLM을 이용한 AI 후처리기 설정

이제 **Hugging Face 모델 다운로드**를 통해, 저사양 하드웨어에서도 실행 가능하면서도 청구서 언어를 이해할 수 있는 모델을 불러옵니다. 예제에서는 Qwen 2.5 3B‑Instruct GGUF 모델을 `int8` 양자화하여 메모리 사용량을 최소화했습니다.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **왜 이 모델인가?** `int8` 양자화 덕분에 파일 크기가 약 1.2 GB로 줄어 대부분의 노트북에서 실행 가능하며, GPU 레이어가 있으면 추론이 가속되고, GPU가 없을 경우 자동으로 CPU로 전환됩니다.

---

## Step 4 – 원시 OCR 결과에 LLM 기반 교정 적용

모델이 준비되면 원시 텍스트를 후처리기에 전달합니다. LLM이 전사본을 재작성해 일반적인 OCR 오류를 고치고 숫자를 정규화합니다.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

예상 정제된 출력:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

이제 0이 문자 “O”로 바뀌었고, “Am0unt”가 “Amount”로 교정되었습니다. 이것이 **OCR 오류 자동 교정**의 핵심입니다.

---

## Step 5 – 리소스 해제 및 정리

대형 언어 모델은 GPU 메모리를 차지하므로 사용이 끝난 뒤에는 리소스를 해제하는 것이 좋습니다.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

많은 청구서를 배치 처리할 경우, 스크립트 마지막에 한 번만 모델을 해제하도록 하면 효율적입니다.

---

## 전체 작업 예시

모든 코드를 하나로 합치면 다음과 같은 단일 스크립트를 `.py` 파일에 저장해 실행할 수 있습니다:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

스크립트를 실행하면 앞서 보여드린 “AI‑교정” 블록과 유사한 출력이 나타납니다. 이미지 경로만 다른 청구서나 영수증으로 바꾸면 **청구서 파일에서 텍스트 추출**을 대량으로 수행할 수 있습니다.

---

## 자주 묻는 질문 & 예외 상황

### GPU가 없으면 어떻게 하나요?

`gpu_layers` 파라미터는 선택 사항입니다. `0`으로 설정하거나 아예 생략하면 모델이 전적으로 CPU에서 실행됩니다. 추론 속도가 느려져 현대 노트북 기준 페이지당 약 2–3 초가 소요됩니다.

### 청구서가 다페이지 PDF인 경우는?

각 페이지를 별도 이미지로 변환(`pdf2image` 등)한 뒤, 동일 스크립트로 반복 처리하면 됩니다. OCR 엔진은 각 이미지를 독립적으로 처리하고, LLM은 각 텍스트 블록을 개별 교정합니다.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### 방화벽 뒤에서 모델 다운로드가 실패하면?

Hugging Face 모델 허브에서 모델을 수동으로 다운로드하고 압축을 푼 뒤 로컬 폴더에 두세요. 그런 다음 `hugging_face_repo_id`를 로컬 경로로 지정하면 됩니다:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### 교정 정확도는 어느 정도인가요?

일반적인 영문 청구서의 경우 LLM이 95 % 이상의 흔한 OCR 오인식을 수정합니다. 복잡한 손글씨는 여전히 수동 검토가 필요할 수 있습니다.

---

## 프로덕션 사용을 위한 팁 & 트릭

- **배치 처리:** 2‑4 단계를 함수화하고 파일 경로 리스트를 전달하세요. 동일 `AsposeAI` 인스턴스를 재사용하면 모델 재로드를 피할 수 있습니다.
- **로깅:** `print` 대신 Python `logging` 모듈을 사용해 원시 및 교정된 출력 모두를 감사 로그에 기록하세요.
- **예외 처리:** OCR 호출을 `try/except` 블록으로 감싸 이미지가 실패해도 파일명을 로그에 남기고 계속 진행하도록 합니다.
- **성능 튜닝:** `gpu_layers` 값을 실험해 보세요. GPU 레이어를 늘리면 추론 속도가 빨라지지만 VRAM 사용량도 증가합니다.

---

## 결론

시작부터 끝까지 **청구서 이미지에서 OCR 수행** 방법을 다루었으며, **이미지에서 OCR 수행**, **Hugging Face 모델 다운로드**, **OCR 오류 자동 교정**을 보여드렸습니다. 완전한 스크립트는 파이썬 기반 자동화 파이프라인에 바로 적용할 수 있는 실용적인 워크플로우를 제공합니다.

다음 단계는 교정된 텍스트에서 정규표현식을 이용해 **핵심 필드**(청구서 번호, 날짜, 총액) 추출하거나, 정제된 출력을 데이터베이스에 저장해 검색 가능한 레코드로 만드는 것입니다. 필요에 따라 다른 경량 LLM을 시험해 보아도 좋습니다.

코딩 즐겁게, OCR 결과가 언제나 선명하길 바랍니다! 

![청구서 이미지에서 OCR 수행 방법](ocr_invoice_example.png "청구서에서 OCR 수행 방법")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
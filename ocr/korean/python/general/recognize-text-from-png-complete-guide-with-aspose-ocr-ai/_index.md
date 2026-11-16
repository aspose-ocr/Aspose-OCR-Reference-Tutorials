---
category: general
date: 2026-06-22
description: Python에서 Aspose OCR을 사용하여 PNG 파일의 텍스트를 인식합니다. 배치 OCR 이미지 처리 방법을 배우고 빠른
  처리를 위해 GPU 레이어를 설정합니다.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: ko
og_description: Python에서 Aspose OCR을 사용하여 PNG 파일의 텍스트를 인식합니다. 이 가이드는 이미지들을 일괄 OCR
  처리하고 속도를 높이기 위해 GPU 레이어를 설정하는 방법을 보여줍니다.
og_title: png에서 텍스트 인식 – 단계별 Aspose OCR 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: PNG에서 텍스트 인식 – Aspose OCR 및 AI를 활용한 완전 가이드
url: /ko/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# png에서 텍스트 인식 – 전체 기능 Aspose OCR & AI 튜토리얼

png 파일에서 **텍스트를 인식**해야 하는데 설정 과정이 복잡하게 느껴진 적이 있나요? 당신만 그런 것이 아닙니다. 영수증을 디지털화하거나, 양식을 스캔하거나, 스크린샷을 검색 가능한 텍스트로 변환할 때, Python에서 배치 OCR 이미지를 마스터하면 몇 시간을 절약할 수 있습니다.  

이 가이드에서는 **png에서 텍스트를 인식**할 뿐만 아니라 **GPU 레이어 설정**을 통해 눈에 띄는 속도 향상을 얻는 방법을 보여주는 실행 가능한 예제를 단계별로 살펴봅니다. 최종적으로 자체 포함 스크립트, 각 단계에 대한 명확한 설명, 그리고 프로젝트에 바로 복사‑붙여넣기 할 수 있는 실용적인 팁을 제공받게 됩니다.

## 이 튜토리얼에서 다루는 내용

- Aspose OCR 및 Aspose AI Python 패키지 설치  
- Hugging Face에서 자동 다운로드되는 AI 모델 구성  
- 가장 흔한 OCR 오타를 수정하는 작은 후처리기 구현  
- 전체 PNG 폴더에 대해 **batch OCR images** 루프 실행  
- **GPU 레이어 설정** 옵션을 사용해 그래픽 카드 활용  
- 처리 후 안전하게 리소스 정리  

외부 서비스 없이, 숨겨진 마법 없이—그냥 `.py` 파일에 넣어 바로 실행할 수 있는 순수 Python 코드만 제공합니다.

![Diagram of recognize text from png workflow](workflow.png){alt="png에서 텍스트 인식 워크플로우 다이어그램"}

## 사전 요구 사항

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Aspose AI의 휠이 최신 인터프리터를 대상으로 함 |
| CUDA‑compatible GPU (optional) | **GPU 레이어 설정**을 통한 가속을 원할 경우 필요 |
| 첫 실행 시 인터넷 접속 | 모델이 Hugging Face에서 자동 다운로드됨 |
| `pip` 설치 | Aspose 패키지를 가져오기 위해 필요 |

이미 모두 갖추셨다면, 바로 시작할 수 있습니다. 부족한 부분이 있다면 아래 설치 단계에서 안내해 드립니다.

---

## Step 1: Install Aspose OCR and Aspose AI Packages

먼저 PyPI에서 라이브러리를 가져옵니다. 아래 명령은 OCR 엔진과 AI 헬퍼를 한 번에 설치합니다.

```bash
pip install aspose-ocr aspose-ai
```

*Pro tip:* 가상 환경(`python -m venv .venv`)을 사용하면 패키지가 전역 Python 설치와 격리됩니다.

---

## Step 2: Create and Configure the Aspose AI Instance

AI 구성 요소가 OCR 엔진의 “지능형” 모드를 구동합니다. `Qwen/Qwen2.5-3B-Instruct-GGUF` 모델을 지정하고, 없을 경우 자동 다운로드하도록 하며, **GPU 레이어**를 30으로 **set GPU layers**합니다(필요에 따라 조정 가능).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**왜 중요한가:**  
- `allow_auto_download`는 약 2 GB 크기의 모델을 수동으로 가져오는 과정을 없애줍니다.  
- `gpu_layers=30`은 기본 트랜스포머의 처음 30 레이어를 GPU에서 실행하도록 지정해, 호환 GPU가 있을 경우 추론 시간을 크게 단축합니다.  
- `int8` 양자화를 사용하면 메모리 사용량을 낮추면서도 정확도 손실을 최소화합니다.

---

## Step 3: Define a Simple Post‑Processor to Clean Up OCR Mistakes

OCR은 완벽하지 않습니다—특히 저해상도 PNG에서는 더 그렇죠. 빠른 해결책은 자주 오인식되는 문자를 교체하는 것입니다. 아래 함수는 스캔된 청구서에서 흔히 보이는 “0”을 “o”로, “1”을 “l”로 바꿉니다.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

다음 단계에서 AI 인스턴스에 연결해 모든 인식 결과가 자동으로 이 후처리를 거치게 할 것입니다.

---

## Step 4: Bind the Post‑Processor and the OCR Engine

이제 모든 요소를 연결합니다: OCR 엔진, AI 모델, 그리고 후처리기.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**내부 동작 설명:**  
`OcrEngine`은 무거운 작업을 구성한 AI 모델에 위임합니다. 모델이 원시 텍스트를 반환하면 Aspose가 `fix_common_errors`를 호출해 출력을 정리한 뒤 결과를 제공합니다.

---

## Step 5: Batch OCR Images – Process Every PNG in a Folder

튜토리얼의 핵심 부분입니다. 디렉터리를 순회하면서 각 `.png`를 로드하고 OCR을 실행한 뒤 정리된 결과를 출력하는 루프입니다. 이 패턴이 **batch OCR images**를 효율적으로 수행하는 표준 방법입니다.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**예상 출력** (영수증 예시):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

수십 개·수백 개의 파일이 있더라도, 이 루프는 순차적으로 처리하며 동일한 AI 인스턴스를 재사용해 모델 로딩 오버헤드를 피합니다.

---

## Step 6: Clean Up – Free Resources and Dispose the Engine

작업이 끝났다면 GPU 메모리와 기타 네이티브 리소스를 해제하는 것이 좋습니다. Aspose는 이를 위한 명시적 메서드를 제공합니다.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

이 단계를 건너뛰면 GPU 메모리가 남아 다음 실행 시 메모리 부족 오류가 발생할 수 있습니다.

---

## Bonus: Tweaking GPU Layers for Different Hardware

앞서 설정한 `gpu_layers` 값은 대부분의 최신 GPU에 적합한 중간값이지만, 하드웨어에 따라 조정이 필요할 수 있습니다:

| GPU Memory (GB) | Recommended `gpu_layers` |
|-----------------|--------------------------|
| 4 GB 이하       | 10‑15                    |
| 6‑8 GB          | 20‑30                    |
| 12 GB 이상      | 35‑45 (또는 그 이상)      |

GPU 메모리를 초과하면 엔진이 자동으로 남은 레이어를 CPU로 전환하므로 크래시 없이 느려질 뿐입니다. `nvidia‑smi`로 사용량을 모니터링하면서 실험해 보세요.

---

## Common Pitfalls & How to Avoid Them

1. **Model download fails** – `https://huggingface.co`에 접근 가능한지 확인하세요. 기업 프록시가 있다면 `https_proxy` 환경 변수를 설정해야 할 수 있습니다.  
2. **GPU not detected** – 의존성으로 설치된 `torch` 라이브러리가 GPU를 인식하는지 확인: `import torch; print(torch.cuda.is_available())`. `False`가 반환되면 CUDA‑compatible PyTorch 휠을 설치하세요.  
3. **Incorrect image path** – `Path.glob("*.png")`는 Linux에서 대소문자를 구분합니다. 필요에 따라 `*.PNG` 또는 `*.png`를 사용하거나 `pathlib.Path(...).rglob("*.[pP][nN][gG]")`로 안전하게 처리하세요.  
4. **Post‑processor over‑corrects** – 간단한 교체 로직이 실제 “0”을 “o”로 바꿀 수 있습니다. 대표 샘플에서 테스트하고 로직을 조정하세요.

---

## Full Working Example (Copy‑Paste Ready)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

다음 명령으로 실행합니다:

```bash
python recognize_text_from_png_batch.py
```

각 PNG 파일 이름 뒤에 추출된 텍스트가 앞서 보여준 대로 출력될 것입니다.

---

## Conclusion

우리는 Aspose OCR 및 Aspose AI를 사용해 **png에서 텍스트를 인식**하는 완전하고 프로덕션 수준의 워크플로우를 모두 살펴보았습니다. 단계들을 하나의 깔끔한 스크립트로 묶음으로써 **batch OCR images**를 손쉽게 수행할 수 있게 되었으며, `set gpu layers` 옵션 덕분에 성능도 크게 향상되었습니다.

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하고, 추가 API 기능을 마스터하며, 자체 프로젝트에 적용할 수 있는 다양한 구현 방식을 소개합니다.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
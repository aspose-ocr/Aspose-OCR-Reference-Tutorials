---
category: general
date: 2026-05-03
description: Aspose OCR 및 AI 맞춤법 검사를 사용하여 이미지에서 텍스트를 추출합니다. OCR 이미지 방법, OCR을 위한 이미지
  로드, 청구서에서 텍스트 인식 및 GPU 리소스 해제에 대해 배워보세요.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: ko
og_description: Aspose OCR 및 AI 맞춤법 검사를 사용하여 이미지에서 텍스트를 추출합니다. 이미지 OCR 방법, OCR을 위한
  이미지 로드, GPU 리소스 해제 등을 다루는 단계별 가이드.
og_title: 이미지에서 텍스트 추출 – 완전한 OCR 및 맞춤법 검사 가이드
tags:
- OCR
- Aspose
- AI
- Python
title: 이미지에서 텍스트 추출 – Aspose AI 맞춤법 검사와 OCR
url: /ko/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 추출 – 완전 OCR 및 맞춤법 검사 가이드

이미 **이미지에서 텍스트 추출**이 필요했지만 어느 라이브러리가 속도와 정확성을 모두 제공할지 몰랐던 적이 있나요? 여러분만 그런 것이 아닙니다. 실제 프로젝트—예를 들어 청구서 처리, 영수증 디지털화, 계약서 스캔—에서 사진으로부터 깨끗하고 검색 가능한 텍스트를 얻는 것이 첫 번째 관문입니다.

좋은 소식은 Aspose OCR과 가벼운 Aspose AI 모델을 결합하면 몇 줄의 파이썬 코드만으로 이 작업을 처리할 수 있다는 것입니다. 이번 튜토리얼에서는 **이미지 OCR** 방법, 이미지를 올바르게 로드하는 방법, 내장 맞춤법 검사 후처리를 실행하는 방법, 그리고 **GPU 리소스 해제** 방법을 단계별로 살펴보겠습니다.

이 가이드를 마치면 **청구서 이미지에서 텍스트 인식**을 수행하고 일반적인 OCR 오류를 자동으로 교정하며, 다음 배치를 위해 GPU를 깔끔하게 유지할 수 있습니다.

---

## 준비물

- Python 3.9 이상 (코드에 타입 힌트가 사용되었지만 이전 3.x 버전에서도 동작합니다)
- `aspose-ocr` 및 `aspose-ai` 패키지 (`pip install aspose-ocr aspose-ai` 로 설치)
- CUDA 지원 GPU는 선택 사항이며, GPU가 없을 경우 스크립트가 자동으로 CPU로 전환됩니다.
- 예시 이미지, 예: `sample_invoice.png` 를 참조 가능한 폴더에 배치

무거운 ML 프레임워크도, 대용량 모델 다운로드도 필요 없습니다—대부분의 GPU에 편하게 들어가는 작은 Q4‑K‑M 양자화 모델만 있으면 됩니다.

---

## Step 1: Initialise the OCR Engine – extract text from image

먼저 `OcrEngine` 인스턴스를 생성하고 기대하는 언어를 지정합니다. 여기서는 영어를 선택하고 평문 텍스트 출력을 요청합니다. 이는 후속 처리에 이상적입니다.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**왜 중요한가:** 언어를 지정하면 문자 집합이 제한돼 정확도가 향상됩니다. 평문 모드는 레이아웃 정보를 제거하는데, 이는 단순히 **이미지에서 텍스트 추출**만 원할 때 보통 필요하지 않은 정보입니다.

---

## Step 2: Load image for OCR – how to OCR image

이제 엔진에 실제 이미지를 전달합니다. `Image.load` 헬퍼는 일반적인 포맷(PNG, JPEG, TIFF)을 이해하고 파일‑IO quirks를 추상화합니다.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**팁:** 원본 이미지가 크다면 엔진에 전달하기 전에 리사이즈를 고려하세요. 작은 해상도는 GPU 메모리 사용량을 줄이면서 인식 품질에 큰 영향을 주지 않습니다.

---

## Step 3: Configure the Aspose AI Model – recognize text from invoice

Aspose AI는 자동 다운로드 가능한 작은 GGUF 모델을 제공합니다. 예제에서는 `Qwen2.5‑3B‑Instruct‑GGUF` 저장소를 사용하며, `q4_k_m` 로 양자화되었습니다. 또한 런타임에 GPU에 20 레이어를 할당하도록 설정해 속도와 VRAM 사용량의 균형을 맞춥니다.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**내부 동작:** 양자화된 모델은 디스크에 약 1.5 GB 정도이며, 전체 정밀도 모델에 비해 훨씬 작지만 일반적인 OCR 오타를 잡아낼 만큼 충분한 언어적 뉘앙스를 보유하고 있습니다.

---

## Step 4: Initialise AsposeAI and attach the spell‑check post‑processor

Aspose AI에는 즉시 사용할 수 있는 맞춤법 검사 후처리기가 포함되어 있습니다. 이를 연결하면 모든 OCR 결과가 자동으로 정제됩니다.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**왜 후처리기를 사용할까?** OCR 엔진은 종종 “Invoice”를 “Invo1ce” 혹은 “Total”을 “T0tal” 로 오인식합니다. 맞춤법 검사는 가벼운 언어 모델을 원시 문자열에 적용해 이러한 오류를 사용자 정의 사전 없이 교정합니다.

---

## Step 5: Run the spell‑check post‑processor on the OCR result

모든 설정이 끝났다면 한 번의 호출로 교정된 텍스트를 얻을 수 있습니다. 원본과 정제된 두 버전을 모두 출력해 개선된 모습을 확인해 보세요.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

청구서에 대한 일반적인 출력 예시:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

“Invo1ce”가 올바른 단어 “Invoice”로 바뀐 것을 확인할 수 있습니다. 이것이 내장 AI 맞춤법 검사의 힘입니다.

---

## Step 6: Release GPU resources – release gpu resources safely

이 코드를 장시간 실행되는 서비스(예: 분당 수십 개의 청구서를 처리하는 웹 API)에서 사용한다면, 각 배치 후 GPU 컨텍스트를 해제해야 합니다. 그렇지 않으면 메모리 누수가 발생하고 결국 “CUDA out of memory” 오류가 뜹니다.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**프로 팁:** `free_resources()` 를 `finally` 블록이나 컨텍스트 매니저 안에서 호출해 예외가 발생해도 항상 실행되도록 하세요.

---

## Full Working Example

모든 파트를 하나로 합치면 어느 프로젝트에든 넣을 수 있는 독립 실행형 스크립트가 완성됩니다.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

파일을 저장하고 이미지 경로를 조정한 뒤 `python extract_text_from_image.py` 를 실행하세요. 정제된 청구서 텍스트가 콘솔에 출력될 것입니다.

---

## Frequently Asked Questions (FAQ)

**Q: CPU 전용 머신에서도 작동하나요?**  
A: 네. GPU가 감지되지 않으면 Aspose AI가 자동으로 CPU 실행으로 전환되지만 속도는 느려집니다. `model_cfg.gpu_layers = 0` 으로 강제로 CPU만 사용하도록 설정할 수도 있습니다.

**Q: 청구서가 영어가 아닌 다른 언어라면 어떻게 하나요?**  
A: `ocr_engine.language` 를 해당 언어에 맞는 enum 값(e.g., `aocr.Language.Spanish`) 으로 변경하세요. 맞춤법 검사 모델은 다국어를 지원하지만, 언어별 모델을 사용하면 더 좋은 결과를 얻을 수 있습니다.

**Q: 여러 이미지를 반복문으로 처리할 수 있나요?**  
A: 가능합니다. 로드, 인식, 후처리 단계를 `for` 루프 안으로 옮기면 됩니다. 동일한 AI 인스턴스를 재사용한다면 루프 종료 후 혹은 각 배치 후 `ocr_ai.free_resources()` 를 호출하는 것을 잊지 마세요.

**Q: 모델 다운로드 크기는 얼마나 되나요?**  
A: 양자화된 `q4_k_m` 버전은 약 1.5 GB 정도입니다. 최초 실행 시 캐시되며 이후 실행은 즉시 이루어집니다.

---

## Conclusion

이번 튜토리얼에서는 Aspose OCR을 사용해 **이미지에서 텍스트 추출**하는 방법, 작은 AI 모델을 설정하고, 맞춤법 검사 후처리를 적용하며, **GPU 리소스 해제**까지 안전하게 수행하는 전체 흐름을 보여드렸습니다. 이미지 로드부터 정리까지 모든 과정을 포함한 파이프라인으로 **청구서에서 텍스트 인식** 시나리오에 신뢰할 수 있는 솔루션을 제공합니다.

다음 단계는 맞춤형 엔터티 추출 모델로 맞춤법 검사를 교체해 보는 것입니다.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
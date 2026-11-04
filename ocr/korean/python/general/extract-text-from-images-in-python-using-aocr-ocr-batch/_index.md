---
category: general
date: 2026-06-25
description: Python aocr 라이브러리로 이미지에서 텍스트를 추출하세요 – 배치 OCR을 배우고, 인쇄 모드 인식을 설정하며, AI
  후처리기를 추가합니다.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: ko
og_description: Python aocr 라이브러리를 사용하여 이미지에서 텍스트를 추출합니다. 이 튜토리얼에서는 배치 OCR, 인쇄물 인식
  모드 및 선택적인 AI 후처리기를 보여줍니다.
og_title: Python에서 이미지에서 텍스트 추출 – 완전한 aocr 배치 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Python을 사용하여 aocr OCR 배치로 이미지에서 텍스트 추출
url: /ko/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 aocr OCR 배치를 사용해 이미지에서 텍스트 추출하기

이미지에서 **텍스트를 추출**해야 하는데 수십 개의 작은 단계에 압도된 적이 있나요? 당신만 그런 것이 아닙니다. 스캔한 양식을 디지털화하거나 영수증에서 데이터를 추출하거나 검색 가능한 아카이브를 구축할 때, 대규모로 신뢰할 수 있는 OCR 결과를 얻는 일은 가파른 언덕을 오르는 느낌일 수 있습니다.

좋은 소식은? **aocr 라이브러리**만 있으면 몇 줄의 코드로 **Python OCR 배치**를 손쉽게 만들 수 있다는 점입니다. 이 가이드에서는 OCR 배치를 생성하고, 폴더에서 지원되는 모든 이미지를 로드하며, 적절한 **recognition mode printed**를 선택하고, 정확도를 한층 높여줄 **AI postprocessor**까지 연결하는 과정을 단계별로 살펴봅니다. 최종적으로 이미지에서 텍스트를 추출하고 파일당 추출된 문자 수를 알려주는 실행 가능한 스크립트를 얻게 됩니다.

## 배울 내용

- `aocr` 패키지를 설치하고 임포트하는 방법
- 수천 개의 파일을 자동으로 처리하는 `OcrBatch` 설정 방법
- 인쇄된 문서에 최적화된 인식 모드 선택하기
- (선택) AI 후처리기를 연결해 노이즈 결과 정리하기
- 각 파일 경로와 추출된 텍스트 길이 출력하기
- 지원되지 않는 형식이나 빈 페이지와 같은 엣지 케이스 처리 팁

### 사전 요구 사항

- Python 3.8 이상 설치되어 있어야 합니다.  
- Python 스크립팅(반복문, 임포트 등)에 대한 기본 지식이 필요합니다.  
- 스캔 이미지가 들어 있는 폴더(PNG, JPG, TIFF 등) 접근 권한이 있어야 합니다.  

위 조건을 만족한다면, 외부 서비스 없이 바로 시작해 보세요.

## 1단계: aocr 라이브러리 설치

먼저 `aocr` 패키지는 표준 라이브러리에 포함되어 있지 않으므로 PyPI에서 받아야 합니다.

```bash
pip install aocr
```

> **팁:** 가상 환경(`python -m venv .venv`)을 사용하면 의존성을 격리할 수 있습니다.  

설치가 완료되면 핵심 클래스를 임포트합니다.

```python
# core imports
import aocr
```

## 2단계: OCR 배치 인스턴스 만들기

`OcrBatch`는 디렉터리를 탐색하고 모든 이미지 파일을 추적하는 작업의 중심입니다. 마치 이미지들을 OCR 엔진에 공급하는 컨베이어 벨트와 같습니다.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

이 시점에서는 배치가 비어 있지만, 다음 단계에서 채울 예정입니다.

## 3단계: 폴더에서 지원되는 모든 이미지 추가 (재귀적으로)

아마도 클라이언트별 혹은 월별로 하위 폴더가 있는 구조일 것입니다. `add_folder` 메서드는 트리를 순회하면서 읽을 수 있는 모든 이미지를 자동으로 가져옵니다.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

`"YOUR_DIRECTORY/scanned_forms/"`를 실제 경로로 바꾸세요. 이 호출 이후 `ocr_batch.file_paths`에는 절대 파일 경로 리스트가 저장되고, 배치는 처리할 항목 수를 정확히 알게 됩니다.

## 4단계: 인쇄 텍스트용 인식 모드 선택

`aocr` 엔진은 여러 모드(손글씨, 인쇄, 혼합)를 지원합니다. 깨끗한 인쇄 양식을 다루고 있으므로 해당 모드로 설정합니다. 이 작은 플래그 하나가 정확도에 큰 차이를 만들 수 있는데, 엔진이 필기체에 필요한 무거운 휴리스틱을 건너뛰기 때문입니다.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **왜 중요한가:** 인쇄 텍스트는 기준선과 문자 형태가 일관되어 OCR 모델이 더 엄격한 문자 사전을 적용할 수 있습니다. 모드를 “auto”로 두면 저해상도 스캔에서 잡음이 늘어날 수 있습니다.

## 5단계: (선택) AI 후처리기 연결

스캔이 흐리거나 대비가 낮거나 특수 폰트가 사용된 경우, AI 후처리기가 원시 OCR 출력물을 정리해 다운스트림 시스템에 전달하기 전에 품질을 높일 수 있습니다. `set_ai_postprocessor` 메서드는 `process(text: str) -> str` 인터페이스를 구현한 객체를 기대합니다.

아래는 가상의 `SimpleCleaner` 클래스를 이용한 최소 예시입니다. 실제로는 HuggingFace 트랜스포머, 커스텀 언어 모델, 혹은 규칙 기반 맞춤법 검사기를 연결할 수 있습니다.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

이 단계를 건너뛰면 배치는 그대로 원시 OCR 문자열을 반환합니다.

## 6단계: 전체 배치 실행 및 결과 수집

이제 본격적인 작업이 시작됩니다. `run` 메서드는 모든 파일을 순회하면서 OCR 엔진을 실행하고, 선택적인 AI 후처리기를 거쳐 문자열 리스트(이미지당 하나)를 반환합니다.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

메서드가 반환하는 것이 일반 Python 리스트이므로, 다른 컬렉션처럼 저장하거나 CSV로 쓰거나 데이터베이스에 넣어 활용할 수 있습니다.

## 7단계: 각 파일 경로와 추출된 텍스트 길이 출력

간단한 검증 방법으로, 파일별 추출된 문자 수를 출력해 보세요. 페이지가 비어 있거나 OCR이 실패하면 `0`이 표시됩니다.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Typical output looks like:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

`0`이 표시된 파일은 즉시 확인이 필요함을 알려줍니다(손상되었거나 이미지가 아닐 가능성).

## 일반적인 엣지 케이스 처리

### 1. 지원되지 않는 파일 형식

`aocr`는 디코딩할 수 없는 파일을 조용히 건너뜁니다. PDF나 BMP가 섞여 있을 경우 사전에 필터링하세요:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. 대용량 배치와 메모리 사용량

수천 개의 고해상도 스캔을 처리하면 메모리 사용량이 급증할 수 있습니다. 청크 단위로 나누어 처리하면 완화됩니다:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. 빈 페이지 또는 저대비 페이지

한 페이지에서 10자 미만이 추출되면 수동 검토 대상으로 플래그를 달고 싶을 수 있습니다:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## 전체 작업 예시

모두 합친 최종 스크립트입니다. 복사‑붙여넣기 후 바로 실행할 수 있습니다. 파일 이름을 `batch_ocr.py`로 저장하세요.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**예상 출력**(일부만 표시):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

다음 명령으로 실행합니다:

```bash
python batch_ocr.py
```

설정이 올바르게 완료되었다면, 이미지마다 한 줄씩 문자 수가 출력됩니다.

## 자주 묻는 질문

**Q: PDF에서도 동작하나요?**  
A: 기본적으로는 지원되지 않습니다. `aocr`는 래스터 이미지만 처리합니다. PDF를 PNG/TIFF 등으로 변환한 뒤 사용하세요(예: `pdf2image` 활용).

**Q: 인식 모드를 손글씨로 바꿀 수 있나요?**  
A: 가능합니다—`aocr.RecognitionMode.PRINTED` 대신 `aocr.RecognitionMode.HANDWRITTEN`으로 교체하면 됩니다. 실행 시간은 늘어나지만 필기체에 대한 결과가 개선됩니다.

**Q: 다국어 지원은 어떻게 하나요?**  
A: 라이브러리는 언어 팩을 제공합니다. 원하는 언어 모듈을 설치(`pip install aocr-lang-fr` 등)하고 실행 전에 `ocr_batch.language = "fr"`와 같이 설정하면 됩니다.

## 다음 단계 및 관련 주제

- **병렬 처리:** `concurrent.futures.ThreadPoolExecutor`로 배치 실행을 감싸 CPU 코어를 다중 활용합니다.  
- **결과 저장:** `ocr_results`를 CSV나 SQLite 데이터베이스에 기록해 다운스트림 분석에 활용합니다.  
- **클라우드 AI와 통합:** `SimpleCleaner`를 HuggingFace 트랜스포머 모델로 교체해 최신 수준의 맞춤법 교정 기능을 적용합니다.  
- **aocr 미세조정:** 커스텀 폰트 세트가 있다면 `aocr.Trainer`를 사용해 인쇄 모드 정확도를 높이는 방법을 탐색해 보세요.

---

이제 탄탄한 OCR 배치 스크립트를 갖추었습니다.


## 다음에 배워야 할 내용은?


다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하는 주제로, 완전한 코드 예제와 단계별 설명을 포함하고 있어 API 기능을 마스터하고 다양한 구현 방식을 직접 프로젝트에 적용하는 데 도움이 됩니다.

- [Aspose OCR을 사용해 이미지에서 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [폴더에 대한 OCR 작업으로 이미지에서 텍스트 추출](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET에서 리스트를 이용해 이미지 배치 OCR 수행](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
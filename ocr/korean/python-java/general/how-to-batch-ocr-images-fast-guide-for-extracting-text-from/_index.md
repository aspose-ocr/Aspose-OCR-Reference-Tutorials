---
category: general
date: 2026-01-12
description: Python에서 JPEG 파일의 텍스트를 빠르게 추출하고 이미지를 일괄 OCR하는 방법. 완전한 실행 가능한 예제와 함께 단계별
  일괄 처리 방법을 배워보세요.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: ko
og_description: 이미지를 일괄 OCR하고 JPEG 파일에서 텍스트를 추출하는 방법. 이 가이드는 완전하고 바로 실행할 수 있는 파이썬
  솔루션을 단계별로 안내합니다.
og_title: 배치 OCR 이미지 처리 방법 – 빠른 파이썬 튜토리얼
tags:
- OCR
- Python
- image processing
title: 이미지를 일괄 OCR하는 방법 – JPEG 파일에서 텍스트 추출을 위한 빠른 가이드
url: /ko/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지 배치 OCR 방법 – JPEG 파일에서 텍스트 추출을 위한 빠른 가이드

여러 파일마다 별도의 스크립트를 작성하지 않고 **이미지를 배치 OCR하는 방법**이 궁금하셨나요? 당신만 그런 것이 아닙니다. 청구서 스캔, 아카이브 디지털화, 콘텐츠 검열 등 많은 프로젝트에서 한 번에 수십 개에서 수백 개의 JPEG 파일에서 텍스트를 추출해야 합니다. 좋은 소식은 파이썬 몇 줄만으로 이를 수행할 수 있으며, 어떤 파이프라인에도 끼워 넣을 수 있는 재사용 가능한 엔진을 만들 수 있다는 점입니다.

이 튜토리얼에서는 **이미지를 배치 OCR하는 방법**을 정확히 보여드리고, JPEG 파일에서 텍스트를 추출하고, 엣지 케이스를 처리하며, 결과를 검증하는 과정을 단계별로 안내합니다. 끝까지 따라오시면 이미지 폴더 전체에 대해 실행할 수 있는 독립형 스크립트를 얻게 되며, 배치 처리의 성능 및 유지보수 측면에서의 중요성을 이해하게 될 것입니다.

## 배울 내용

- 간단한 OCR 엔진을 설정하고 영어에 맞게 구성하기
- `pathlib`을 사용해 디렉터리 내 모든 JPEG 파일 수집하기
- 한 번의 호출로 전체 배치를 처리하는 OCR 엔진 사용하기
- 각 이미지에 대해 인식된 텍스트 미리보기 표시하기
- 대용량 배치, 다국어 지원, 흔히 발생하는 함정 처리 팁

**전제 조건**: Python 3.8 이상, `ocr` 라이브러리(또는 호환 가능한 래퍼), 분석하려는 JPEG 이미지가 들어 있는 폴더. 외부 서비스는 필요 없으며 모든 작업이 로컬에서 수행됩니다.

---

## Step 1: Initialise the OCR Engine – The Core of How to Batch OCR Images

배치를 OCR하려면 텍스트를 읽을 수 있는 엔진이 필요합니다. 대부분의 라이브러리에서는 엔진 객체를 생성하고, 필요에 따라 언어를 설정한 뒤, 모든 파일에 재사용합니다.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*왜 중요한가*: 엔진을 한 번만 초기화하면 언어 모델을 반복해서 로드하는 오버헤드를 피할 수 있습니다. 또한 DPI, 허용 문자 목록 등 설정을 한 곳에서 조정하면 전체 배치에 적용됩니다.

> **Pro tip**: 다국어 문서를 처리할 계획이라면 `ocr.Language.ENGLISH`를 `ocr.Language.MULTI`로 바꾸거나 배치를 시작하기 전에 여러 언어 팩을 로드하세요.

---

## Step 2: Gather All JPEG Files – The “Extract Text from JPEG Files” Part

엔진이 준비되었으니 이제 어떤 이미지들을 처리할지 알려줘야 합니다. `pathlib`을 사용하면 코드가 플랫폼에 독립적이고 간결해집니다.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*왜 중요한가*: 파일 목록을 먼저 수집하면 전체 컬렉션을 한 번에 OCR 엔진에 전달할 수 있습니다—바로 **이미지를 배치 OCR하는 방법**의 핵심입니다. 하위 폴더가 있다면 `glob("**/*.jpg")`를 재귀 검색으로 바꿀 수 있습니다.

> **Edge case**: 이미지 확장자가 혼합되어 있는 경우(`.jpeg`, `.JPG`) 다음과 같이 glob 패턴을 확장하세요: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## Step 3: Process the Whole Batch in One Call – The Real Power of Batch OCR

대부분의 최신 OCR 라이브러리는 파일 경로 iterable을 받아들이는 `process_batch`(또는 유사 이름) 메서드를 제공합니다. 이것이 **이미지를 배치 OCR하는 방법**을 효율적으로 구현하는 핵심입니다.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*왜 중요한가*: 한 번의 배치 호출은 Python‑to‑C 전환 횟수를 줄이고, 언어 모델을 메모리에 유지하며, 내부 병렬 처리를 가능하게 합니다. 결과는 인식된 텍스트와 신뢰도 점수를 포함한 객체 리스트가 됩니다.

> **Performance note**: 수천 개의 이미지를 처리하는 매우 큰 배치의 경우, 메모리 과다 사용을 방지하기 위해 리스트를 작은 청크(예: 200 파일)로 나누어 처리하는 것을 고려하세요.

---

## Step 4: Show a Preview of the Extracted Text – Quick Validation

배치가 끝난 뒤 각 결과의 앞 몇 글자를 살펴보면 OCR이 실제로 JPEG 파일에서 텍스트를 추출했는지 빠르게 확인할 수 있습니다.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*왜 중요한가*: 짧은 미리보기를 통해 빈 출력이나 깨진 문자와 같은 명백한 실패를 모든 파일을 열지 않고도 발견할 수 있습니다. 체계적인 문제가 보이면 엔진 설정을 조정하고 배치를 다시 실행하면 됩니다.

> **Common pitfall**: 개행 문자를 제거하지 않으면 미리보기가 지저분해 보일 수 있습니다. `replace("\n", " ")` 라인이 이를 정리해 줍니다.

---

## Full Working Example – All Steps Combined

아래는 전체 스크립트이며, 디렉터리 경로만 수정하고 바로 실행할 수 있습니다. **이미지를 배치 OCR하는 방법** 전체 워크플로우를 시작부터 끝까지 보여줍니다.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**예상 출력** (샘플):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

미리보기에 의미 있는 텍스트가 표시되면 **JPEG 파일에서 텍스트를 추출**하는 배치 접근법을 성공적으로 수행한 것입니다.

---

## Handling Large Batches and Advanced Scenarios

### Chunking Large Workloads
수천 개의 이미지를 다룰 때 메모리가 병목이 될 수 있습니다. 리스트를 작은 청크로 나누세요:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Switching Languages
문서에 프랑스어나 스페인어가 포함되어 있다면 배치 전에 언어를 변경합니다:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Saving Results to Disk
출력을 콘솔에 표시하는 대신 각 OCR 결과를 `.txt` 파일로 저장하고 싶을 수 있습니다:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Conclusion

이제 **이미지를 배치 OCR하는 방법**과 **JPEG 파일에서 텍스트를 추출**하는 방법을 컴팩트한 파이썬 스크립트로 확실히 익혔습니다. 엔진을 한 번만 초기화하고, 모든 JPEG 경로를 수집하고, 한 번의 배치 호출로 처리하고, 출력 미리보기를 확인함으로써 속도와 단순성을 동시에 얻을 수 있습니다. 여기서부터는 다국어 지원을 추가하거나, 결과를 데이터베이스에 저장하거나, 스크립트를 더 큰 문서 처리 파이프라인에 통합하는 등 워크플로우를 확장할 수 있습니다.

다음 단계가 준비되셨나요? `ocr` 라이브러리를 Tesseract로 교체해 보거나, 이미지 전처리(임계값 적용, 리사이징)를 실험해 보세요. 추출된 텍스트를 자연어 처리 모델에 넣어 자동 분류까지 진행할 수 있습니다. 가능성은 무한하며, 이제 튼튼한 기반을 갖추었습니다.

행복한 코딩 되시고, OCR 배치가 언제나 오류 없이 작동하길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
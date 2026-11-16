---
category: general
date: 2026-03-18
description: Python과 Aspose OCR을 사용하여 PNG에서 텍스트를 추출합니다. OCR을 위한 이미지 로드 방법, 여러 파일에
  대한 OCR 실행, 그리고 병렬 이미지 인식을 통한 배치 OCR 이미지를 구현하는 방법을 배워보세요.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: ko
og_description: Python에서 Aspose OCR을 사용하여 PNG에서 텍스트를 추출합니다. 이 튜토리얼에서는 OCR을 위한 이미지를
  로드하고, 여러 파일을 OCR 처리하며, 병렬 이미지 인식을 사용하여 배치 OCR 이미지를 실행하는 방법을 보여줍니다.
og_title: PNG에서 텍스트 추출 – 병렬 OCR 가이드
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: PNG에서 텍스트 추출 – 배치 이미지 인식을 위한 병렬 OCR 가이드
url: /ko/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG에서 텍스트 추출 – 배치 이미지 인식을 위한 병렬 OCR 가이드

단일 이미지 처리에 시간이 너무 오래 걸려 **PNG에서 텍스트를 추출**해야 할 때 막히신 적 있나요? 당신만 그런 것이 아닙니다. 인보이스 스캐너, 영수증 디지털화, 아카이브 도구와 같은 실제 프로젝트에서는 속도가 중요하며, PNG를 하나씩 처리하는 방식은 절대 충분하지 않습니다.  

이 가이드에서는 **loads image for OCR**를 수행하고, **ocr multiple files**를 **batch OCR images** 방식으로 실행하며, Python의 `threading` 모듈을 활용한 **parallel image recognition**을 구현하는 완전한 실행 가능한 솔루션을 단계별로 살펴봅니다. 최종적으로 수 초 안에 다수의 PNG에서 텍스트를 추출하는 스크립트를 얻게 됩니다.

## 필요 사항

- Python 3.8 이상 (예시 코드는 3.10+에서도 동작합니다).  
- Aspose OCR for Java/​Python 패키지 (`aspose-ocr`). `pip`으로 설치할 수 있습니다.  
- 처리하고자 하는 PNG 파일이 들어 있는 폴더.  
- 적당한 양의 RAM—각 스레드가 작은 OCR 엔진 인스턴스를 보유하므로 노트북에서도 수십 개의 워커를 실행할 수 있습니다.

외부 서비스, 클라우드 키, 신비한 설정 파일이 전혀 필요 없습니다. 복사‑붙여넣기만 하면 바로 실행할 수 있는 순수 Python 코드입니다.

## 왜 PNG에서 텍스트를 병렬로 추출할까요?

PNG 처리 작업은 CPU‑집약적입니다. OCR 엔진은 픽셀 데이터를 분석하는 일련의 알고리즘을 실행합니다. 이미지가 10개, 20개, 혹은 100개가 되면 전체 실행 시간은 각 이미지별 실행 시간의 합과 같습니다.  

각 파일마다 스레드를 생성하면 운영 체제가 이러한 CPU‑무거운 작업을 동시에 스케줄링합니다. 다코어 머신에서는 종종 실행 시간이 절반, 심지어 1/4까지 단축됩니다. 메모리 사용량이 약간 늘어나는 것이 단점이지만, 대부분의 배치 작업에서는 속도 향상이 충분히 가치 있습니다.

> **Pro tip:** 수백 메가바이트 규모의 이미지를 다룰 경우 `threading` 대신 `concurrent.futures.ProcessPoolExecutor`를 사용하는 것을 고려하세요. 프로세스는 GIL‑제한이 있는 CPython 인터프리터에서 진정한 병렬성을 제공하지만 약간의 오버헤드가 추가됩니다.

## Step 1: Install Aspose OCR for Python

먼저 OCR 라이브러리를 시스템에 설치합니다.

```bash
pip install aspose-ocr
```

위 한 줄로 최신 Aspose OCR 바이너리와 Python 바인딩을 가져옵니다. 권한 오류가 발생하면 `--user` 옵션을 추가하거나 가상 환경을 사용해 보세요.

## Step 2: Load image for OCR – the worker function

이제 각 스레드에서 실행될 핵심 루틴을 정의합니다. 이 함수는 **loads image for OCR**를 수행하고 인식을 실행한 뒤 추출된 텍스트의 미리보기를 출력합니다.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

주의할 점:

- **왜 스레드마다 새로운 `OcrEngine`을 생성할까요?** 엔진은 내부 버퍼를 보유하고 있어 하나의 인스턴스를 공유하면 레이스 컨디션과 깨진 출력이 발생합니다.  
- **왜 줄바꿈을 제거하나요?** 콘솔에 로그를 남길 때 줄을 깔끔하게 유지하기 위해서입니다.  
- **오류 처리는?** 실제 서비스에서는 `try/except`로 감싸고 파일에 로깅하는 것이 일반적이며, 이는 이후에 다룰 예정입니다.

## Step 3: List the PNG files you want to process

리스트를 하드코딩할 수도 있지만, 보다 유연한 방법은 디렉터리를 스캔하는 것입니다. 아래 예시는 명확성을 위해 세 파일을 수동으로 나열했으며, 경로는 자신의 폴더에 맞게 교체하면 됩니다.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

자동으로 파일을 찾아서 처리하고 싶다면:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

이 작은 수정만으로 **extract text from PNG** 파일들을 소스 코드를 매번 수정하지 않고도 대량으로 처리할 수 있습니다.

## Step 4: Set up ocr multiple files with batch OCR images

이제 각 이미지마다 스레드를 생성합니다. 이것이 **batch OCR images** 패턴의 핵심입니다.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

리스트 컴프리헨션을 사용해 코드를 간결하게 유지했으며, 각 `Thread` 객체는 대상 함수와 인수(`image_path`)를 저장합니다.  

> **Side note:** Python의 `threading` 모듈은 네이티브 OS 스레드를 사용하므로 4코어 노트북에서는 보통 동시에 4개의 스레드가 실제로 실행되고, 나머지는 코어가 비게 되면 스케줄됩니다.

## Step 5: Run parallel image recognition

워커를 시작하는 과정은 간단합니다: 리스트를 순회하며 `start()`를 호출합니다. 이후 `join()`을 사용해 모든 스레드가 종료될 때까지 기다립니다.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

스크립트가 끝나면 다음과 같은 라인들이 출력됩니다:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

이 출력은 각 PNG가 처리되었으며 추출된 텍스트가 추가 작업(예: 데이터베이스 저장 또는 NLP 파이프라인 입력)으로 사용될 수 있음을 확인시켜 줍니다.

## Step 6: Verify the results and handle edge cases

### 빈 결과 확인하기

이미지가 너무 노이즈가 많거나 OCR 엔진이 문자를 전혀 감지하지 못할 때가 있습니다. 간단한 검증을 통해 다운스트림 오류를 방지할 수 있습니다.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### 동시 실행 스레드 수 제한하기

작은 VM에서 실행한다면 수백 개의 스레드를 생성하면 스케줄러가 과부하될 수 있습니다. 세마포어를 사용해 동시성을 제한할 수 있습니다:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### 결과를 파일에 저장하기

출력 대신 파일에 CSV 형태로 저장하고 싶을 수 있습니다. 파일명과 추출 텍스트를 한 줄에 기록하는 예시입니다:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

CSV 파일은 **한 번**만 열어 스레드 함수 외부에서 공유하고, `csv` 모듈의 writer는 간단한 쓰기 작업에 대해 스레드‑안전합니다.

## Full Working Example

모든 내용을 하나로 합치면 `batch_ocr.py`라는 파일에 저장하고 바로 실행할 수 있는 스크립트가 됩니다:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
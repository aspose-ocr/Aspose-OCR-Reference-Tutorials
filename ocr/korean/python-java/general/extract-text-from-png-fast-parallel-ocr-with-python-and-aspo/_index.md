---
category: general
date: 2026-03-28
description: Python에서 Aspose OCR을 사용하여 PNG에서 텍스트를 빠르게 추출합니다. 고성능 결과를 위해 병렬 이미지 인식을
  활용한 스캔 페이지 텍스트 변환 방법을 배워보세요.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: ko
og_description: Python에서 Aspose OCR을 사용하여 PNG에서 텍스트를 빠르게 추출합니다. 이 가이드는 병렬 이미지 인식을
  활용한 스캔 페이지 텍스트 변환 방법을 보여주며, 고속 결과를 제공합니다.
og_title: PNG에서 텍스트 추출 – 파이썬을 이용한 빠른 병렬 OCR
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: PNG에서 텍스트 추출 – Python 및 Aspose를 이용한 빠른 병렬 OCR
url: /ko/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG에서 텍스트 추출 – 파이썬을 이용한 빠른 병렬 OCR

PNG 파일에서 **텍스트를 추출**해야 했지만 단일 스레드 OCR이 너무 느려서 고민한 적 있나요? 당신만 그런 것이 아닙니다. 스캔한 영수증을 디지털화하거나 강의 슬라이드를 검색 가능한 PDF로 변환하려 할 때, 병목 현상은 보통 OCR 단계 자체입니다.  

이 튜토리얼에서는 Aspose OCR의 비동기 배치 모드와 파이썬 `ThreadPoolExecutor`를 결합한 **스캔된 페이지 텍스트를 병렬로 변환**하는 완전한 실행 가능한 솔루션을 보여드립니다. 끝까지 따라오면 **image text python** 스타일로 이미지를 인식하고, 단순 루프보다 훨씬 짧은 시간에 수십 개의 이미지를 처리할 수 있게 됩니다.

> **얻을 수 있는 것**  
> * PNG 이미지를 동시에 추출하는 완전한 스크립트.  
> * 비동기 배치 모드가 왜 속도를 높이는지에 대한 이해.  
> * 더 큰 작업량에 대한 확장 팁.

## 필요한 준비물

| 전제 조건 | 이유 |
|--------------|--------|
| Python 3.9+ | 최신 문법과 타입 힌트를 지원합니다. |
| `aspose-ocr` 및 `aspose-storage` 패키지 | OCR 엔진과 이미지 로더를 제공합니다. |
| PNG 파일이 들어 있는 폴더 (예: 스캔한 페이지) | 처리하려는 원본 자료입니다. |
| 파이썬 동시성에 대한 기본 지식 | 있으면 좋지만 필수는 아닙니다; 모든 것을 설명합니다. |

Aspose 라이브러리는 다음 명령으로 설치할 수 있습니다:

```bash
pip install aspose-ocr aspose-storage
```

> **프로 팁:** `pip list --outdated` 로 패키지를 최신 상태로 유지하면 최신 성능 개선을 바로 활용할 수 있습니다.

## Step 1: Aspose OCR 엔진을 비동기 배치 모드로 초기화

먼저 `OcrEngine` 인스턴스를 생성하고 **비동기 배치 모드**로 전환합니다. 이 모드는 내부적으로 인식 요청을 큐에 넣어, 파이썬 스레드를 차단하지 않고 여러 이미지를 동시에 처리할 수 있게 합니다.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*왜 비동기인가?*  
동기 모드에서 `recognize` 를 호출하면 이미지가 완전히 처리될 때까지 호출이 차단됩니다. 비동기 모드에서는 현재 이미지가 디코딩되는 동안 엔진이 다음 이미지를 바로 작업에 착수시킬 수 있어 I/O와 CPU 작업이 겹치게 됩니다.

## Step 2: 처리할 PNG 파일 목록 만들기

여기서는 이미지 컬렉션을 정의합니다. 실제 프로젝트에서는 `glob.glob("*.png")` 와 같이 동적으로 목록을 생성할 수 있지만, 예시를 명시적으로 적어 두면 이해하기 쉽습니다.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **주의:** `YOUR_DIRECTORY` 를 PNG 스캔 파일이 들어 있는 실제 경로로 바꾸세요. 파일이 수백 개라면 `os.listdir` 로 목록을 만든 뒤 `.png` 로 필터링하는 방법을 고려하십시오.

## Step 3: 이미지를 로드하고 텍스트를 반환하는 헬퍼 작성

헬퍼 함수는 **Aspose Storage** 로 파일을 로드하고 OCR 엔진에 전달하는 두 단계 과정을 추상화합니다. 짧은 docstring 을 추가하면 함수가 스스로 문서화되어 향후 유지보수가 쉬워집니다.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*왜 별도 함수인가?*  
스레드 풀 코드를 깔끔하게 유지하고, 다른 곳(예: Flask 엔드포인트)에서도 로직을 재사용할 수 있습니다. 또한 I/O를 분리하면 디버깅이 쉬워집니다—특정 파일이 실패하면 예외 트레이스에 파일명이 표시됩니다.

## Step 4: Thread Pool 로 파이썬 병렬 이미지 인식 실행

이제 `ThreadPoolExecutor` 를 도입합니다. 기본값으로 4개의 워커를 띄우지만, CPU 코어 수와 이미지 규모에 따라 `max_workers` 를 조정할 수 있습니다.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### 어떻게 파이썬 병렬 이미지 인식을 제공하는가

* **ThreadPoolExecutor** 가 워커 스레드 풀을 만들고 각 스레드가 `recognize_image` 를 호출합니다.  
* OCR 엔진이 비동기 배치 모드에 있기 때문에, 각 스레드는 엔진에 작업을 넘기면서도 응답성을 유지합니다.  
* `as_completed` 는 완료된 순서대로 future 를 반환하므로, 결과가 준비되는 즉시 받아볼 수 있어 대용량 배치를 스트리밍하기에 적합합니다.

> **흔한 실수:** `max_workers=1` 로 설정하면 병렬 처리의 의미가 사라집니다. 8코어 머신에서는 `max_workers=8` 이 가장 높은 처리량을 보이지만, 하드웨어에 맞는 최적값을 찾기 위해 몇 가지 값을 테스트해 보세요.

## Step 5: 출력 확인 및 예외 상황 처리

스크립트를 실행하면 각 PNG 파일에 대해 텍스트 블록이 파일명 앞에 붙어 출력됩니다:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

이미지가 손상되었거나 지원되지 않는 형식일 경우, `except` 블록이 전체 배치를 중단하지 않고 유용한 오류 메시지를 출력합니다.

### 솔루션 확장하기

| 시나리오 | 권장 수정 사항 |
|----------|-----------------|
| **수천 페이지** | `ProcessPoolExecutor` 로 전환해 다중 CPU 프로세스를 활용하거나, 리스트를 청크로 나눠 순차적으로 배치 처리합니다. |
| **다른 이미지 형식 (JPG, TIFF)** | `storage.Image.load` 메서드가 자동으로 형식을 감지하므로 파일을 `input_images` 에 추가하기만 하면 됩니다. |
| **결과 저장 필요** | `else` 블록 안에서 `text` 를 `.txt` 파일에 쓰거나 데이터베이스에 삽입합니다. |
| **성능 모니터링** | `recognize_image` 를 타이머(`time.perf_counter`) 로 감싸고 파일당 소요 시간을 로그에 기록합니다. |

## Full Working Example (Copy‑Paste Ready)

아래는 `parallel_ocr.py` 라는 파일에 바로 넣어 실행할 수 있는 전체 스크립트입니다. 빠진 부분 없이 모든 코드가 포함되어 있습니다.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

파일을 저장하고 `YOUR_DIRECTORY` 플레이스홀더를 실제 경로로 바꾼 뒤 실행하세요:

```bash
python parallel_ocr.py
```

콘솔에 각 PNG 에 대한 추출된 텍스트가 앞서 보여드린 대로 표시될 것입니다.

## 결론

우리는 Aspose OCR의 비동기 배치 모드와 파이썬 `ThreadPoolExecutor` 를 결합해 **PNG 파일에서 텍스트를 효율적으로 추출**하는 방법을 시연했습니다. 이 스크립트는 스캔된 페이지 텍스트를 병렬로 변환하여, **recognize image text python** 스타일의 확장 가능한 OCR 처리를 가능하게 합니다.  

다음 단계로 시도해 볼 수 있는 내용:

* 결과를 검색 가능한 SQLite 데이터베이스에 저장하기.  
* OCR 전에 OpenCV 로 이미지 전처리(기울기 보정, 노이즈 제거) 추가하기.  
* Flask 또는 FastAPI 엔드포인트 뒤에 마이크로서비스 형태로 배포하기.

성능 높은 OCR 은 단순히 빠른 엔진만으로 되는 것이 아니라, 엔진에 작업을 공급하는 방식이 동시성을 최대화하도록 설계되는 것이 핵심입니다. 여기서 소개한 패턴을 활용하면 최소한의 코드 변경으로 수십, 수백 개의 PNG 스캔을 손쉽게 처리할 수 있습니다.

행복한 코딩 되세요, 그리고 PDF 가 언제나 검색 가능하길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
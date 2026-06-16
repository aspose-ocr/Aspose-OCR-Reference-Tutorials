---
category: general
date: 2026-03-26
description: Python을 사용해 OCR을 효율적으로 배치 처리하는 방법—이미지와 PDF에서 텍스트를 추출하고 병렬 처리를 통한 OCR
  변환을 배워보세요.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: ko
og_description: 배치 OCR을 효율적으로 수행하는 방법—이미지에서 텍스트 추출, PDF OCR 변환 및 파이썬을 이용한 배치 OCR 처리
  단계별 가이드.
og_title: '배치 OCR 방법: 빠른 병렬 텍스트 추출'
tags:
- OCR
- Python
- Parallel Computing
title: '배치 OCR 방법: 빠른 병렬 텍스트 추출'
url: /ko/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 배치 OCR 방법: 빠른 병렬 텍스트 추출

수십 개의 스캔 페이지, 스크린샷, PDF 파일이 쌓여 있을 때 **배치 OCR**이 궁금하셨나요? 당신만 그런 것이 아닙니다—대부분의 개발자들이 같은 문제에 부딪힙니다: 파일을 하나씩 처리하는 것이 고통스러운 병목 현상이 됩니다.  

좋은 소식은 워커 스레드를 몇 개 띄워 모든 파일을 넣어 주면 OCR 엔진이 배치를 병렬로 처리하는 모습을 볼 수 있다는 것입니다. 이번 튜토리얼에서는 **이미지에서 텍스트 추출**, **PDF OCR 변환**을 수행하고 **병렬 OCR 처리**를 활용해 속도를 높이는 완전한 실행 예제를 단계별로 살펴보겠습니다.

> **얻을 수 있는 것**  
> * PNG, TIFF, PDF, JPG 파일을 한 번에 처리하는 완전한 파이썬 스크립트  
> * 스레드 풀이 I/O‑바운드 OCR 작업을 가속화하는 이유에 대한 이해  
> * 오류 처리, 대용량 PDF, 사용자 정의 스레드 수에 대한 팁  

## Prerequisites

| Requirement | Reason |
|-------------|--------|
| Python 3.8+ | 최신 문법 및 `concurrent.futures` 지원 |
| `ocr` library (or any compatible OCR wrapper) | `OcrBatchProcessor`와 결과 객체 제공 |
| A handful of sample files (PNG, TIFF, PDF, JPG) | **이미지에서 텍스트 추출** 동작을 확인하기 위해 |
| Basic familiarity with threads (optional) | 있으면 좋지만 필수는 아님 |

`ocr` 패키지를 아직 설치하지 않았다면 다음을 실행하세요:

```bash
pip install ocr-lib   # replace with the actual package name
```

이제 환경이 준비되었으니 문제를 나눠 보겠습니다.

## Step 1: Import helpers and instantiate the batch processor

첫 번째로 필요한 것은 모든 OCR 작업을 모아 둘 장소입니다. `OcrBatchProcessor` 클래스가 바로 그 역할을 수행합니다—작업 항목을 큐에 넣고 `Future` 객체 리스트를 반환합니다.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Why this matters*: `as_completed`를 임포트하면 가장 먼저 끝난 작업에 즉시 반응할 수 있어 가장 느린 파일을 기다릴 필요가 없습니다. 이것이 **배치 OCR 처리**의 핵심입니다.

## Step 2: Tune the worker pool for parallel execution

기본 설정에서는 프로세서가 단일 스레드만 사용할 수 있어 배치의 의미가 사라집니다. 여기서는 명시적으로 네 개의 워커를 요청합니다—CPU 코어 수에 맞게 숫자를 늘려도 됩니다.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tip*: OCR과 같은 I/O‑바운드 작업은 `CPU cores * 2`를 초과하면 수익이 급격히 감소합니다. 몇 가지 값을 테스트해 최적점을 찾으세요.

## Step 3: Queue every file you want to OCR

여기서는 이미지와 PDF 파일을 혼합해서 추가합니다. `add` 메서드는 경로만 기록하고 실제 작업은 배치를 제출할 때 시작됩니다.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

전체 폴더를 처리해야 한다면 간단한 `glob` 루프가 도움이 됩니다:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Step 4: Fire off the jobs and collect futures

`submit_all`을 호출하면 프로세서가 작업을 시작합니다. 이 메서드는 `Future` 객체 리스트를 반환하는데, 이는 나중에 결과가 채워질 자리표시자와 같습니다.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

이 시점에서 OCR 엔진은 백그라운드에서 동작 중이며, 각 스레드가 파일을 처리하고 있습니다.

## Step 5: Pull results as soon as they finish

`as_completed`를 사용하면 제출 순서가 아니라 완료 순서대로 `Future`를 순회합니다. 이는 특히 일부 PDF가 단순 PNG보다 오래 걸릴 때 스크립트를 더 반응성 있게 만들어 줍니다.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Expected output** (truncated for brevity):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

각 블록은 원본 파일의 순수 텍스트 표현에 해당합니다. **PDF OCR 변환**을 수행한다면 텍스트에는 각 페이지에서 OCR 엔진이 해석한 모든 내용이 포함됩니다.

## Handling Edge Cases & Common Pitfalls

| Situation | What to watch for | Quick fix |
|-----------|-------------------|-----------|
| A corrupted image | `future.result()` raises `OSError` | `try/except`로 감싸기 (위 코드 참조) |
| Very large PDFs ( > 100 MB ) | 메모리 압박, 스레드 속도 저하 | `thread_count`를 적당히 늘리거나 PDF를 챕터별로 분할 |
| Mixed language documents | 기본 OCR 모델이 언어를 오인식할 수 있음 | 라이브러리가 지원한다면 `OcrBatchProcessor`에 언어 힌트 전달 |
| Need to preserve layout | 일반 `get_text()`는 컬럼을 잃음 | `ocr_result.get_hocr()` 등 레이아웃 인식 메서드 사용 |

### Pro tip: Custom thread count based on file type

대부분이 PDF라면 PDF 전용 스레드를 더 많이 할당하고 작은 PNG는 적게 할당할 수 있습니다. 일부 라이브러리는 작업별 `priority`를 지원하니 활용해 보세요. 지원하지 않으면 이미지용 배치와 PDF용 배치를 별도로 만들어 동시에 실행하면 됩니다.

## Visual Overview (optional)

![배치 OCR 워크플로우 다이어그램](https://example.com/ocr-workflow.png "배치 OCR 워크플로우")

*다이어그램은 파일 탐색 → 배치 생성 → 병렬 실행 → 결과 집계 흐름을 보여줍니다.*

## Full Script You Can Copy‑Paste

아래는 `.py` 파일에 바로 붙여넣을 수 있는 전체 프로그램입니다. 앞서 소개한 모든 스니펫과 디렉터리에서 지원 파일을 자동으로 찾아주는 작은 헬퍼가 포함되어 있습니다.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

`batch_ocr.py`라는 이름으로 저장하고, 스캔 파일이 들어 있는 폴더를 지정하면 콘솔에 추출된 텍스트가 가득 채워지는 것을 확인할 수 있습니다.  

### Why this works

* **Thread pool** – OCR은 주로 디스크 I/O와 외부 엔진 호출을 기다리므로 여러 스레드가 CPU를 효율적으로 활용합니다.  
* **`as_completed`** – 결과가 준비되는 즉시 받아올 수 있어 UI 피드백이나 스트리밍 파이프라인에 이상적입니다.  
* **Error isolation** – 하나의 손상된 파일이 전체 배치를 중단시키지 않으며, `try/except` 블록이 실패를 격리합니다.

## Conclusion

요약하면, 이제 파이썬 `concurrent.futures`와 배치 처리를 지원하는 OCR 라이브러리를 사용해 **배치 OCR**을 수행하는 방법을 알게 되었습니다. 적당한 스레드 풀을 구성하고, 모든 지원 파일을 큐에 넣으며, 완료되는 대로 결과를 받아오면 신뢰성을 해치지 않으면서 빠른 **병렬 OCR 처리**를 달성할 수 있습니다.  

앞으로 할 수 있는 일:

* 추출된 텍스트를 검색 인덱스에 연결해 빠른 문서 검색 구현  
* 각 결과를 원본 파일 옆에 `.txt` 파일로 저장하도록 스크립트 확장  
* OCR 라이브러리가 async API를 제공한다면 내장 스레드 풀을 `asyncio`로 교체  

계속 실험해 보세요—Tesseract, Azure Cognitive Services, Google Vision 등으로 교체해도 동일한 패턴이 적용됩니다. 즐거운 OCR 작업 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-06-19
description: Python OCR을 사용해 이미지에서 텍스트를 추출합니다. 자동 언어 감지, 병렬 처리 및 배치 인식을 간결한 튜토리얼에서
  배워보세요.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: ko
og_description: Python OCR로 이미지에서 텍스트를 추출하세요. 이 가이드는 자동 언어 감지, 병렬 처리 및 배치 인식을 하나의
  튜토리얼에서 보여줍니다.
og_title: Python에서 이미지에서 텍스트 추출 – 전체 OCR 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python에서 이미지에서 텍스트 추출 – 전체 OCR 가이드
url: /ko/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 추출하기 – 전체 OCR 가이드

이미지를 **텍스트로 추출**하는 방법을 고민해 본 적 있나요? 직접 타이핑하지 않아도 되는 편리함을 원한다면 당신만 그런 것이 아닙니다. 오래된 영수증을 디지털화하거나, 검색 가능한 문서 아카이브를 구축하거나, 멋진 AI 트릭을 즐기고 싶을 때, 사진에서 텍스트를 뽑아내는 능력은 오늘날 모든 Python 개발자에게 필수 스킬입니다.

이 튜토리얼에서는 인기 있는 OCR 엔진을 사용해 **이미지에서 텍스트를 추출**하는 완전한 실행 예제를 단계별로 살펴봅니다. 자동 언어 감지, 속도 향상을 위한 병렬 처리, 배치 이미지 인식까지 다루어 수십 개 파일을 몇 초 만에 처리할 수 있습니다. 필요하신 내용인가요? 바로 시작해 보겠습니다.

## 배울 내용

- `ocr.OcrEngine`으로 OCR 엔진 인스턴스 생성하기
- **자동 언어 감지**를 활성화해 엔진이 스스로 언어를 선택하도록 하기
- 커스텀 스레드 풀을 이용한 **병렬 처리 OCR** 설정하기
- 파일 리스트에 대한 **배치 이미지 인식** 실행하기
- 각 이미지에 대해 인식된 텍스트를 출력하고, 저장하거나 색인할 준비하기

외부 문서는 필요 없습니다—여기서 바로 `ocr` 패키지(`pip install ocr`)만 있으면 코드를 바로 실행할 수 있습니다.

## 사전 준비

시작하기 전에 다음을 준비하세요:

1. Python 3.8 이상 설치
2. `ocr` 패키지 (`pip install ocr`)
3. 처리하려는 PNG(또는 JPG) 이미지가 들어 있는 폴더
4. Python 함수와 루프에 대한 기본 지식

그게 전부입니다—무거운 의존성도, GPU도 필요 없고 순수 Python만 있으면 됩니다.

![extract text from images example](https://example.com/ocr-demo.png "Screenshot showing extract text from images output")

*대체 텍스트: extract text from images demo screenshot*

## Step 1 – OCR 엔진 설정하기 (Primary Keyword in Action)

먼저 OCR 엔진 인스턴스를 생성합니다. `ocr.OcrEngine()`은 작업의 두뇌와 같으며, 문자, 줄, 단락을 읽는 방법을 알고 있습니다.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

왜 명시적으로 엔진을 만들어야 할까요? **ocr.OcrEngine 사용**은 언어 설정, 스레딩 등 세부 제어를 가능하게 해 주며, 한 줄 헬퍼보다 **이미지에서 텍스트를 추출**하는 가장 유연한 방법입니다.

## Step 2 – 엔진에 자동 언어 감지 시키기

대부분의 OCR 라이브러리는 어떤 언어를 인식할지 지정해야 합니다. 단일 언어 프로젝트에는 괜찮지만, 혼합 언어 배치에서는 번거롭습니다. 다행히 `ocr` 패키지는 **자동 언어 감지**를 지원합니다.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

`engine.language`를 `ocr.Language.Auto`로 설정하면 엔진이 각 이미지를 살펴보고 적절한 언어 모델을 자동으로 선택합니다. 이 한 줄만으로 국제 문서를 다룰 때 수시간의 수작업 설정을 절감할 수 있습니다.

## Step 3 – 병렬 처리 OCR으로 속도 올리기

CPU 코어가 4개 이상이라면 활용해 보세요. 엔진은 스레드 풀을 생성해 여러 이미지를 동시에 처리할 수 있습니다. 여기서 **병렬 처리 OCR**의 진가가 발휘됩니다.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

머신에 맞게 숫자 `4`를 조정하면 됩니다. 스레드 수가 많을수록 배치 실행이 빨라지지만, 각 스레드가 메모리를 차지하니 환경에 맞는 최적점을 찾아야 합니다.

## Step 4 – 처리할 이미지 모으기

이제 파일 경로 리스트가 필요합니다. 리스트를 직접 작성하거나 CSV에서 읽어오거나 `glob`을 사용할 수 있습니다. 여기서는 간단히 짧은 리스트를 하드코딩합니다:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

`YOUR_DIRECTORY`를 실제 경로로 교체하세요. 파일이 수십 개라면 `glob.glob("*.png")` 같은 한 줄이 작업을 대신해 줍니다.

## Step 5 – 배치 이미지 인식 실행하기

튜토리얼의 핵심 부분입니다. `files`에 있는 모든 이미지를 한 번에 처리하고 결과 객체 리스트를 반환합니다. 바로 **배치 이미지 인식** 기능으로 대규모 OCR이 실용화됩니다.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

엔진은 앞서 설정한 네 개의 워커 스레드에 파일을 분배하고, 동시에 각 이미지에 대해 자동 언어 감지를 수행합니다. 반환된 리스트의 각 요소는 인식된 텍스트와 메타데이터를 담고 있습니다.

## Step 6 – 추출된 텍스트 출력(또는 저장)하기

마지막으로 결과를 순회하며 텍스트를 출력합니다. 실제 프로젝트에서는 데이터베이스나 CSV 파일에 저장하겠지만, 예제는 출력으로 간단히 보여줍니다.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**예상 출력**(요약):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

각 블록은 파일명 뒤에 OCR이 만든 문자열을 보여줍니다. 이미지에 여러 언어가 섞여 있으면 앞서 설정한 **자동 언어 감지** 덕분에 해당 문자들이 올바르게 표시됩니다.

## 팁 & 흔히 겪는 문제

- **이미지 품질** – 흐리거나 대비가 낮은 사진은 쓰레기 결과를 낳습니다. 필요하면 OpenCV(`cv2.threshold`, `cv2.resize`)로 전처리하세요.
- **스레드 수 vs I/O** – 이미지가 느린 네트워크 드라이브에 있다면 스레드 수를 늘려도 도움이 되지 않을 수 있습니다. `top`이나 `Task Manager`로 CPU 사용량을 확인하세요.
- **Unicode 처리** – `result.text`는 Unicode 문자열입니다. 파일에 쓸 때는 `encoding="utf-8"` 옵션을 사용해 `UnicodeEncodeError`를 방지하세요.
- **메모리 사용량** – 큰 PDF를 처리하면 RAM이 많이 잡힐 수 있습니다. `MemoryError`가 발생하면 스레드 풀 크기를 줄이거나 작은 청크로 나눠 처리하세요.

## 전체 작동 스크립트

아래는 지금까지 설명한 모든 단계를 포함한 복사‑붙여넣기용 완전한 스크립트입니다. `batch_ocr.py`라는 파일명으로 저장하고 `python batch_ocr.py`를 실행하세요.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

실행 방법:

```bash
python batch_ocr.py ./my_images 4
```

각 이미지마다 깔끔하게 포맷된 텍스트 블록이 출력되어 **이미지에서 텍스트를 추출**할 수 있음을 확인할 수 있습니다.

## 다음 단계는?

Python으로 **이미지에서 텍스트를 추출**하는 기본을 마스터했으니, 다음 주제들을 탐색해 보세요:

- **후처리**: 정규식이나 자연어 처리 라이브러리로 OCR 결과 정리
- **PDF 변환**: 추출한 문자열을 PDF 생성기로 보내 검색 가능한 PDF 만들기
- **클라우드 OCR 서비스**: 온프레미스 `ocr` 결과를 Google Vision이나 Azure OCR과 비교해 정확도 확인
- **GUI 프론트엔드**: Flask 또는 FastAPI 앱을 만들어 사용자가 이미지를 업로드하고 즉시 텍스트를 확인하도록 구현

이 모든 주제는 방금 설정한 **Python OCR 라이브러리** 기반 위에 쌓이며, 여기서 사용한 **병렬 처리 OCR** 기법도 그대로 활용할 수 있습니다.

---

*코딩 즐겁게! 문제가 생기면 아래 댓글에 남겨 주세요—OCR 트러블슈팅을 언제든 도와드릴게요.*

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 보여준 기술을 확장하는 관련 주제들을 다룹니다. 각 리소스는 완전한 코드 예시와 단계별 설명을 포함해 API 기능을 더 깊이 파고들고, 프로젝트에 적용할 다양한 구현 방식을 탐색할 수 있게 도와줍니다.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
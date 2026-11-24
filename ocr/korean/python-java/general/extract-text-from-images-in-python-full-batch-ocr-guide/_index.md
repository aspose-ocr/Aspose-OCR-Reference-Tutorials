---
category: general
date: 2026-06-19
description: 간단한 OCR 엔진을 사용해 파이썬으로 이미지에서 텍스트를 추출합니다. 스캔한 이미지를 텍스트로 변환하고, 사진에서 텍스트를
  인식하며, 파이썬으로 이미지 파일을 효율적으로 나열하는 방법을 배워보세요.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: ko
og_description: 가벼운 OCR 엔진을 사용해 Python에서 이미지의 텍스트를 추출합니다. 이 가이드는 스캔한 이미지를 텍스트로 변환하고,
  사진에서 텍스트를 인식하며, 몇 단계만에 파이썬으로 이미지 파일을 나열하는 방법을 보여줍니다.
og_title: Python으로 이미지에서 텍스트 추출 – 전체 배치 OCR 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Python으로 이미지에서 텍스트 추출 – 전체 배치 OCR 가이드
url: /ko/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 추출하기 (Python) – 전체 배치 OCR 가이드

이미지를 **텍스트로 추출**해야 하는데 어디서 시작해야 할지 몰라 고민한 적 있나요? 여러분만 그런 것이 아닙니다—개발자들은 스캔한 PDF, 사진으로 찍은 영수증, 스크린샷 등을 검색 가능한 텍스트로 변환하는 문제에 끊임없이 직면합니다. 이번 튜토리얼에서는 **스캔한 이미지를 텍스트로 변환**하고, 사진에서 텍스트를 인식하며, **list image files python** 스타일로 이미지 파일을 나열하는 완전한 실행 예제를 단계별로 살펴보겠습니다. 최종적으로 전체 폴더를 한 번에 처리할 수 있는 재사용 가능한 스크립트를 얻게 됩니다.

필요한 라이브러리, 각 단계가 왜 중요한지, 엣지 케이스 처리, 그리고 약간의 트러블슈팅까지 모두 다룹니다. 외부 문서를 찾아볼 필요 없이 아래 코드는 자체적으로 완전하며, 설명은 “어떻게”와 “왜”를 모두 답합니다. 좋아하는 IDE를 열고 바로 시작해 보세요.

---

## 만들게 될 것

- OCR 엔진 초기화 (`ocr` 패키지를 예시로 사용)
- 디렉터리를 스캔하고 **list image files python** 스타일로 PNG, JPG, TIFF 파일을 필터링
- 찾은 모든 사진에 대해 **배치 OCR** 수행
- 각 파일별로 추출된 텍스트를 명확히 라벨링하여 출력

> **Pro tip:** `ocr` 라이브러리가 설치되어 있지 않다면, 몇 가지 작은 수정만으로 `pytesseract` 로 교체할 수 있습니다—핵심 로직은 동일합니다.

---

## 사전 준비

- Python 3.8+ (스크립트가 f‑string 및 타입 힌트를 사용합니다)
- `OcrEngine` 과 `recognize_batch` 를 제공하는 OCR 라이브러리. 여기서는 가상의 `ocr` 패키지를 가정하지만, 실제 라이브러리에도 동일한 패턴을 적용할 수 있습니다.
- 처리하고자 하는 이미지 파일이 들어 있는 폴더 (`.png`, `.jpg`, `.tif`)

---

## Step 1 – Install & Import Required Modules

먼저 OCR 패키지가 사용 가능한지 확인합니다. 실제 라이브러리(`pytesseract` 등)를 사용할 경우 import 문을 해당 라이브러리로 교체하면 됩니다.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Why this matters:** `os` 를 import 하면 플랫폼에 관계없이 경로를 다룰 수 있고, `typing.List` 는 IDE 자동완성과 향후 확장성을 돕습니다.

---

## Step 2 – **Extract Text from Images**: Initialize the OCR Engine

엔진을 생성하는 것은 모든 OCR 작업의 첫 단계입니다. 여기서는 언어를 자동 감지하도록 설정해 혼합 언어 문서도 처리할 수 있게 합니다.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Explanation:** 엔진 생성을 함수로 캡슐화하면 코드가 모듈화됩니다. 나중에 DPI나 OCR 모드를 조정해야 할 경우 이 한 곳만 수정하면 됩니다.

---

## Step 3 – **List Image Files Python**: Gather Files from a Directory

이제 처리할 모든 사진을 찾아야 합니다. 아래 리스트 컴프리헨션은 흔히 쓰이는 “list image files python” 패턴을 그대로 구현합니다.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Edge case handling:** 이 함수는 하위 폴더를 무시합니다(필요하면 재귀적으로 확장 가능) 그리고 숨김 파일은 지원되는 확장자로 끝나지 않기 때문에 자동으로 필터링됩니다.

---

## Step 4 – **Convert Scanned Images to Text**: Run Batch OCR

대부분의 OCR 라이브러리는 한 번에 여러 이미지를 처리하는 배치 메서드를 제공하며, 개별 처리보다 훨씬 빠릅니다. 아래와 같이 호출합니다.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Why batch?** 모든 이미지를 한 번에 전달하면 모델 로딩 같은 오버헤드가 감소하고 CPU/GPU 활용 효율이 높아집니다.

---

## Step 5 – **Recognize Text from Pictures**: Display the Results

마지막으로 파일명과 OCR 결과를 짝지어 순회하면서 각 이미지마다 깔끔한 헤더를 출력합니다.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Tip:** `strip()` 은 OCR이 자주 추가하는 앞뒤 공백을 제거해 줍니다.

---

## Full Script – Put It All Together

아래는 완전하고 실행 가능한 전체 프로그램입니다. `batch_ocr.py` 로 저장한 뒤 `python batch_ocr.py <your_folder>` 로 실행하세요.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Expected Output

폴더에 `invoice1.png` 와 `receipt.jpg` 가 들어 있다고 가정하면 다음과 같은 출력이 나타날 수 있습니다.

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

각 블록이 명확히 라벨링돼 있어, 이후 데이터베이스 저장 등 다운스트림 처리도 간편합니다.

---

## Handling Common Pitfalls

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **No text appears** | OCR 언어가 감지되지 않았거나 이미지가 저대비인 경우 | 언어를 강제 지정 (`engine.language = ocr.Language.English`)하거나 이미지 전처리(대비 증가)를 수행 |
| **Memory error on large batches** | 엔진이 모든 이미지를 한 번에 로드하려 하기 때문 | `image_files` 를 청크로 나누어 (`batch_size = 20`) `recognize_batch` 를 반복 호출 |
| **Unsupported file format** | `.gif` 혹은 `.bmp` 와 같은 형식을 추가했을 경우 | `supported_exts` 튜플에 형식을 추가하거나 PNG/JPG 로 변환 |
| **Unicode garbling** | OCR이 문자열 대신 바이트를 반환 | OCR 라이브러리가 Unicode 를 출력하도록 설정 (`result.text.decode('utf‑8')` 등) |

---

## Extending the Workflow

이제 **이미지에서 텍스트를 추출**할 수 있게 되었으니, 다음 단계도 고려해 보세요:

- **Export to CSV** – 파일명과 추출된 텍스트를 스프레드시트에 기록해 분석에 활용
- **Parallel processing** – `concurrent.futures.ThreadPoolExecutor` 로 여러 배치를 동시에 처리
- **Integrate with cloud OCR** – 로컬 엔진을 Google Vision 혹은 Azure OCR 로 교체해 복잡한 레이아웃에서도 높은 정확도 확보
- **Add image preprocessing** – Pillow 혹은 OpenCV 로 이미지 기울기 보정, 노이즈 제거, 임계값 적용 등 전처리를 하면 OCR 결과가 크게 개선

위 아이디어들은 모두 앞서 만든 핵심 함수들을 그대로 활용하므로, 처음부터 다시 코딩할 필요가 없습니다.

---

## Conclusion

우리는 Python에서 **이미지에서 텍스트를 추출**하는 전체 솔루션을 단계별로 살펴보았습니다. 여기에는 **list image files python** 부터 **recognize text from pictures**, 그리고 **convert scanned images to text** 까지의 배치 흐름이 포함됩니다. 스크립트는 의도적으로 간단하면서도 확장성을 염두에 두었으니, 영수증 디지털화, 검색 가능한 아카이브 구축, 데이터 추출 파이프라인 등 다양한 프로젝트의 기반으로 활용할 수 있습니다.

코드를 직접 실행해 보고 전처리 단계를 조정해 보면서 OCR 정확도가 어떻게 상승하는지 확인해 보세요. 문제가 발생하면 “Handling Common Pitfalls” 표를 다시 참고하면 대부분 작은 설정 변경만으로 해결됩니다.

다음 도전 과제가 준비됐나요? `pdf2image` 로 PDF‑to‑image 변환 단계를 추가하고, 동일 파이프라인에 바로 연결해 보세요. OCR과 Python 생태계를 결합하면 가능성은 무한합니다.

Happy coding, and may your text be ever legible!

## What Should You Learn Next?

다음 튜토리얼들은 이번 가이드에서 다룬 기술을 확장·심화할 수 있는 관련 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공해 API 기능을 마스터하고 다양한 구현 방식을 탐색하도록 돕습니다.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
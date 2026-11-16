---
category: general
date: 2026-06-28
description: Python에서 배치 OCR 수행 방법—이미지에서 텍스트를 추출하고 스캔한 페이지를 배치 OCR 처리로 텍스트로 변환하기.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: ko
og_description: Python에서 배치 OCR을 수행하고, 이미지에서 텍스트를 추출하며, 효율적인 배치 OCR 처리로 스캔한 페이지를 텍스트로
  변환하는 방법을 배워보세요.
og_title: Python에서 배치 OCR 수행 방법 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python에서 배치 OCR 수행 방법 – 이미지에서 텍스트 추출을 위한 완벽 가이드
url: /ko/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 배치 OCR 수행 방법 – 이미지에서 텍스트 추출 완전 가이드

If you're wondering **how to batch OCR in Python**, you're in the right place. This tutorial shows you a quick way to **extract text from images** and **convert scanned pages to text** using a single OCR engine instance. No more copy‑pasting one file after another—let the code do the heavy lifting.

우리는 필요한 모든 과정을 단계별로 안내합니다: 라이브러리 설치, 전체 스캔 폴더 로드, 배치 OCR 처리 실행, 그리고 결과를 우아하게 처리하기. 끝까지 진행하면 PNG 또는 JPEG 파일 묶음을 몇 초 만에 검색 가능한 텍스트 파일로 변환하는 재사용 가능한 스크립트를 얻게 됩니다.

## 필요 사항

* Python 3.9+가 설치되어 있어야 합니다 (코드는 3.8에서도 동작하지만, 3.9+를 사용하면 최신 타입 기능을 사용할 수 있습니다).
* 최신 OCR 라이브러리—여기서는 **Aspose.OCR for Python via .NET**를 사용하며, 이는 원본 스니펫에 표시된 `OcrEngine` 클래스를 제공합니다.  
  ```bash
  pip install aspose-ocr
  ```
* 스캔된 페이지가 들어 있는 폴더(`page1.png`, `page2.png`, …). Pillow가 열 수 있는 모든 형식이면 되므로 PDF, TIFF, BMP도 사용할 수 있습니다.
* 약간의 호기심—이미지‑텍스트 자동화 경험이 없더라도 배치 OCR이 왜 게임 체인저인지 곧 알게 될 것입니다.

> **Pro tip:** 순수 Python 라이브러리를 선호한다면 `OcrEngine`을 `pytesseract.image_to_string`으로 교체하세요. 주변 로직은 동일하게 유지됩니다.

## Python에서 배치 OCR 수행 – 단계별 가이드

아래는 완전하고 실행 가능한 스크립트입니다. 모든 줄에 주석이 달려 있어 *무엇을* 하는지뿐만 아니라 *왜* 중요한지 확인할 수 있습니다.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### 예상 출력

세 개의 PNG 스캔이 들어 있는 폴더에 대해 스크립트를 실행하면 다음과 같은 결과가 생성됩니다:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

미리보기는 각 페이지의 처음 200자를 보여주며, 전체 텍스트는 `ocr_output` 디렉터리에 저장됩니다.

## 단일 엔진을 사용하여 이미지에서 텍스트 추출

왜 **하나의** `OcrEngine`을 생성하고 재사용할까요? 엔진을 인스턴스화하면 언어 팩과 네이티브 DLL을 로드하므로 비용이 많이 듭니다. 배치 전체에 동일한 인스턴스를 공유하면 다음과 같은 이점이 있습니다:

* **메모리 절약** – 리소스 한 세트만 RAM에 존재합니다.
* **속도 향상** – 엔진이 계속 활성화돼 반복 초기화를 피합니다.
* **일관성 유지** – 동일한 인식 설정이 모든 페이지에 적용되어, 동일한 레이아웃을 가진 **이미지에서 텍스트 추출**이 필요할 때 필수적입니다.

인식 설정을 조정해야 할 경우(예: 맞춤법 검사 활성화 또는 언어 변경) `recognize_batch`를 호출하기 *앞에* 수행하세요. 이후 모든 페이지가 자동으로 해당 설정을 상속합니다.

## 스캔 페이지를 효율적으로 텍스트로 변환

문제의 핵심인 **스캔 페이지를 텍스트로 변환**은 `engine.recognize_batch(images)`로 해결됩니다. 내부적으로 라이브러리는 각 이미지를 백그라운드 스레드 풀에서 처리하므로 다중 코어 머신에서 거의 선형에 가까운 확장성을 얻을 수 있습니다. 몇 가지 유의사항은 다음과 같습니다:

* **이미지 품질 중요** – 300 dpi 이상이 최상의 결과를 제공합니다. 스캔이 저해상도라면 엔진에 전달하기 전에 Pillow로 업샘플링을 고려하세요.
* **컬러 vs. 그레이스케일** – OCR 엔진은 일반적으로 8‑bit 그레이스케일에서 더 빠르게 동작합니다. 전처리 단계를 추가할 수 있습니다:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **언어 지원** – Aspose.OCR은 40개 이상의 언어를 지원합니다. 영어가 아닌 경우 배치 호출 전에 `engine.language = "eng"` 또는 `"fra"`와 같이 설정하세요.

## 배치 OCR 처리 모범 사례

위 코드가 이미 간결하지만, 프로덕션 수준 배치 OCR은 종종 몇 가지 추가 안전장치를 필요로 합니다:

| 우려 사항 | 권장 접근법 |
|----------|-------------|
| **대용량 배치 ( > 500 파일 )** | 메모리 사용량을 적당히 유지하기 위해 100–200 이미지씩 청크로 나눕니다. |
| **손상되었거나 지원되지 않는 파일** | `load_images` 헬퍼가 이미 예외를 잡아 경고를 로그에 남깁니다; 또한 실패 파일을 건너뛰거나 이동하는 대체 로직을 작성할 수 있습니다. |
| **진행 상황 모니터링** | 라이브러리가 이미지별 콜백을 제공한다면 `recognize_batch`를 루프에 감싸서 각 이미지 후에 yield하도록 합니다. |
| **후처리** | 결과 문자열에 맞춤법 검사나 정규식 정리를 수행해 다운스트림 검색 가능성을 향상시킵니다. |
| **병렬 처리** | 멀티 노드 환경이 있다면 폴더를 워커에 분산시키고 마지막에 `.txt` 출력물을 병합합니다. |

이 팁들은 몇 페이지에서 수천 페이지까지 **배치 OCR 처리**를 확장하면서 스크립트가 중단되지 않도록 도와줍니다.

## 자주 묻는 질문

**Q: PDF를 직접 사용할 수 있나요?**  
A: 물론입니다. 각 PDF 페이지를 먼저 이미지로 변환(`pdf2image` 등 사용)한 뒤, 생성된 리스트를 `recognize_batch`에 전달하면 됩니다. 파이프라인의 나머지 부분은 그대로 유지됩니다.

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 자체 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Aspose OCR을 사용한 이미지에서 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [폴더에서 OCR 작업을 사용하여 이미지에서 텍스트 추출](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET을 사용해 ZIP 아카이브에서 텍스트 추출 방법](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-07-05
description: Python에서 OCR을 사용하여 TIFF를 빠르게 텍스트로 변환하는 방법. TIFF 이미지에서 텍스트를 추출하고 Python
  OCR 엔진을 구축하기 위한 OCR 라이브러리 Python 단계들을 배워보세요.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: ko
og_description: Python에서 OCR을 사용하는 방법은? 이 가이드는 파이썬 OCR 엔진과 ocr 라이브러리를 사용하여 TIFF를 텍스트로
  변환하는 과정을 단계별로 보여줍니다.
og_title: Python에서 OCR 사용 방법 – 전체 TIFF 텍스트 추출
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Python에서 OCR 사용 방법 – TIFF에서 텍스트 추출
url: /ko/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 OCR 사용 방법 – TIFF에서 텍스트 추출

스캔한 책을 편집 가능한 텍스트로 변환하기 위해 **Python에서 OCR을 어떻게 사용하는지** 궁금해 본 적 있나요? 여러분만 그런 것이 아닙니다—개발자, 연구자, 취미 개발자 모두 다중 페이지 TIFF 이미지를 다룰 때 이 문제에 부딪힙니다. 좋은 소식은? **ocr library python**을 사용하면 작은 OCR 엔진을 바로 실행하고, TIFF 파일을 지정하여 몇 초 만에 깨끗하고 검색 가능한 텍스트를 얻을 수 있습니다.

이 튜토리얼에서는 필요한 모든 과정을 단계별로 살펴보겠습니다: 올바른 패키지 설치, 다중 페이지 TIFF 로드, OCR 엔진 실행, 그리고 각 페이지의 내용을 출력하기까지. 끝까지 따라오면 **TIFF를 텍스트로 변환**하고 **TIFF에서 텍스트를 추출**하는 방법을 Python 환경을 떠나지 않고도 사용할 수 있게 됩니다.

## 사전 요구 사항

- Python 3.9 이상 (예제는 3.11에서 테스트됨)
- 최신 버전의 `ocr` 라이브러리 (또는 원하는 호환 `python ocr engine`)
- 처리하려는 다중 페이지 TIFF 파일 (`scanned_book.tif`라고 부르겠습니다)
- Python 스크립트와 가상 환경에 대한 기본적인 이해

무거운 외부 도구는 필요 없습니다—pip과 몇 줄의 코드만 있으면 됩니다.

## OCR Library Python 설치

먼저 해야 할 일은 견고한 OCR 백엔드를 준비하는 것입니다. 이 가이드에서는 간단한 고수준 API를 제공하는 가상의 `ocr` 패키지를 사용하지만, 동일한 패턴을 `pytesseract`와 같은 Tesseract 기반 래퍼나 상용 SDK에도 적용할 수 있습니다.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Windows 환경에서 패키지가 네이티브 바이너리에 의존한다면, 해당 Visual C++ 재배포 가능 패키지가 설치되어 있는지 확인하세요. 설치 프로그램은 보통 누락된 항목이 있으면 경고합니다.

## Python에서 OCR 엔진 사용 방법

라이브러리가 준비되었으니 OCR 엔진을 시작하고 TIFF 파일을 지정해 보겠습니다. 아래 스니펫은 엔진 인스턴스를 생성하고, 언어를 영어로 설정한 뒤, 다중 페이지 처리를 위해 준비합니다.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**왜 언어를 설정하나요?**  
대부분의 OCR 엔진은 정확도를 높이기 위해 언어 모델을 사용합니다. 이 단계를 건너뛰면 엔진이 일반 모델로 돌아가 구두점이나 특수 문자를 잘못 인식할 수 있습니다.

## 다중 페이지 TIFF 이미지 로드

다음 단계는 스캔한 문서를 로드하는 것입니다. `ocr.Image.load` 헬퍼는 TIFF 스택을 바로 이해하고, 각 페이지를 내부적으로 나타내는 객체를 반환합니다.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** TIFF에 압축이 적용되어(`CCITT Group 4`, `LZW` 등) 라이브러리에서 오류가 발생한다면, 먼저 ImageMagick으로 압축되지 않은 버전으로 변환해 보세요:  
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## 모든 페이지에 OCR 수행 – TIFF를 텍스트로 변환

이미지 객체가 준비되면 엔진이 한 번에 모든 페이지를 처리할 수 있습니다. 이 메서드는 각 페이지에 대한 OCR 결과를 담은 리스트를 반환합니다.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**내부에서 무슨 일이 일어나나요?**  
`recognize_multi_page` 함수는 각 래스터화된 페이지를 순회하면서 신경망 인식기를 실행하고, 평문 출력과 신뢰도 점수를 함께 패키징합니다. 사실상 수동 루프를 작성할 필요가 없는 배치 작업입니다.

## 결과 반복 – TIFF에서 텍스트 추출

마지막으로 인식된 텍스트를 표시합니다. 출력 결과를 별도의 `.txt` 파일로 저장하거나 데이터베이스에 넣거나 검색 인덱스로 전달하는 등 워크플로에 맞게 활용할 수 있습니다.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### 예상 출력

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

각 `result.text` 문자열에는 해당 페이지의 원시 OCR 출력이 들어 있습니다. 줄바꿈을 유지해야 한다면 대부분의 엔진이 `result.lines`를 문자열 리스트 형태로 제공한다는 점을 기억하세요.

## 대용량 TIFF 파일 처리 – 팁과 요령

500 페이지짜리 TIFF를 처리하면 메모리 사용량이 크게 늘어날 수 있습니다. 아래 전략을 활용해 부드럽게 작업하세요:

1. **페이지를 청크 단위로 처리** – `recognize_multi_page` 대신 `engine.recognize(page)`를 호출하는 제너레이터를 사용해 한 번에 한 페이지씩 처리합니다.
2. **DPI 조정** – 이미지 해상도를 낮추면(예: 300 DPI → 200 DPI) 대부분의 인쇄 텍스트에 대한 정확도 손실이 거의 없으면서 CPU 부하를 줄일 수 있습니다.
3. **병렬 처리** – OCR 엔진이 스레드 안전하다면 `concurrent.futures.ThreadPoolExecutor`를 사용해 여러 페이지를 동시에 인식하도록 합니다.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## 추출된 텍스트를 파일로 저장

실제 파이프라인에서는 영구 저장소가 필요합니다. 아래 코드는 각 페이지 텍스트를 순서대로 별도 파일에 덤프하는 간결한 방법을 보여줍니다.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

이제 인덱싱이나 추가 NLP 처리를 위해 준비된 `.txt` 파일들이 깔끔한 디렉터리에 모여 있습니다.

## 이미지 미리보기 – OCR 결과를 시각적으로 활용하기

원본 이미지 위에 OCR 오버레이를 표시하고 싶다면(디버깅에 유용) 많은 라이브러리가 바운딩 박스를 그릴 수 있습니다. 아래는 Pillow를 이용한 간단한 예시입니다.

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Python에서 OCR 사용 방법 – TIFF 페이지에 OCR 오버레이](ocr_overlay_example.png)

*Alt text:* Python에서 OCR 사용 방법 – TIFF 페이지에 인식된 텍스트를 시각적으로 오버레이한 예시.

## 흔히 발생하는 문제와 해결 방법

| 문제 | 발생 원인 | 해결 방법 |
|------|----------|----------|
| 깨진 문자 | 잘못된 언어 모델 | `engine.language`를 올바른 enum으로 설정 |
| 누락된 페이지 | TIFF 압축이 지원되지 않음 | 먼저 압축되지 않은 TIFF로 변환 |
| 성능 저하 | 높은 DPI와 단일 스레드 처리 | DPI를 낮추거나 멀티스레딩 활성화 |
| 빈 출력 | 이미지가 너무 어둡거나 대비가 낮음 | 대비 스트레칭(`opencv` 또는 `Pillow`)으로 전처리 |

이러한 문제를 초기에 해결하면 나중에 디버깅에 소요되는 시간을 크게 절감할 수 있습니다.

## 다음 단계 – 기본 추출을 넘어선 활용

이제 **Python에서 OCR을 어떻게 사용하는지** 기본을 마스터했으니, 다음과 같은 주제를 탐색해 보세요:

- **PDF 생성** – 추출한 텍스트와 `reportlab`을 결합해 검색 가능한 PDF를 재구성합니다.
- **언어 감지** – `langdetect`를 사용해 `engine.language`를 자동 전환합니다.
- **구조화된 데이터 추출** – 정규식이나 spaCy를 활용해 원시 텍스트에서 날짜, 이름, 표 등을 추출합니다.
- **대체 OCR 백엔드** – 다국어 지원이 필요하면 `ocr` 대신 `pytesseract`나 `easyocr`로 교체합니다.

이러한 주제들은 모두 **ocr library python**, **convert tiff to text**, **extract text from tiff**, **python ocr engine**이라는 보조 키워드와 자연스럽게 연결되어, 보다 고급 프로젝트를 위한 탄탄한 기반을 제공합니다.

---

### 결론

우리는 **Python에서 OCR을 어떻게 사용하는지** 설치부터 다중 페이지 처리까지 전 과정을 다루었으며, 간단한 **python OCR engine**을 이용해 **TIFF를 텍스트로 변환**하고 **TIFF에서 텍스트를 추출**하는 방법을 정확히 보여주었습니다. 위의 완전한 실행 예제는 대부분의 표준 TIFF 파일에 바로 적용될 수 있으며, 제공된 팁을 활용하면 대용량 문서에도 확장하거나 OCR을 더 큰 파이프라인에 통합할 수 있습니다.

직접 스캔한 책, 영수증, 아카이브 이미지를 가지고 시도해 보세요. 그런 다음 “다음 단계” 섹션에 나열된 고급 아이디어를 실험해 보시기 바랍니다. 즐거운 코딩 되시고, OCR 결과가 언제나 정확하기를 바랍니다!

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Aspose OCR로 이미지에서 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR for Java로 tiff에서 텍스트 추출하는 방법](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Aspose OCR을 사용해 스트림에서 이미지 텍스트 추출 수행하기](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
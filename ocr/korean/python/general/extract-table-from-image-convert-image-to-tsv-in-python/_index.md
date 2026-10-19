---
category: general
date: 2026-07-05
description: Python OCR을 사용하여 이미지에서 표를 추출합니다. 표를 추출하고 이미지를 TSV로 변환하는 방법을 배우며, OCR
  표 이미지 파이썬 기술을 마스터하세요.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: ko
og_description: Python OCR을 사용해 이미지에서 표를 추출합니다. 이 가이드는 표를 추출하고, 이미지를 TSV로 변환하며, OCR
  표 이미지 파이썬 도구를 사용하는 방법을 보여줍니다.
og_title: 이미지에서 표 추출 – 파이썬으로 이미지를 TSV로 변환
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: 이미지에서 표 추출 – 파이썬으로 이미지를 TSV로 변환
url: /ko/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 표 추출 – Python으로 이미지 → TSV 변환

이미지에서 표를 추출하는 방법이 궁금했지만 머리를 쥐어뜯을 정도로 복잡하다고 생각하셨나요? 이 튜토리얼에서는 `aocr` 라이브러리를 사용해 사진에서 **표 데이터를 추출**하고, 이를 깔끔한 TSV 파일로 변환하는 과정을 단계별로 안내합니다. 마법은 없으며, 몇 줄의 Python 코드와 AI 기반 후처리만 있으면 됩니다.

스캔한 청구서나 스크린샷에서 표를 복사‑붙여넣기 시도했지만 엉망이 된 경험이 있다면, OCR 기반 접근법을 마스터해야 하는 이유를 이해하실 겁니다. 이 과정을 마치면 표가 포함된 어떤 이미지든 Python에 넣어 깔끔한 탭 구분값(TSV)으로 변환해 스프레드시트나 데이터베이스에 바로 사용할 수 있습니다.

---

## 필요한 준비물

본격적으로 시작하기 전에, 아래 항목들이 준비되어 있는지 확인하세요:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | `aocr` 패키지는 최신 Python 런타임을 대상으로 합니다. |
| `aocr` library (`pip install aocr`) | 우리가 사용할 OCR 엔진과 AI 후처리기를 제공합니다. |
| An image file containing a table (PNG, JPG, etc.) | 추출할 원본 데이터 파일입니다. |
| Optional: a virtual environment | 의존성을 격리하여 관리할 수 있어 강력히 권장됩니다. |

이 항목들을 미리 준비하면 가이드 진행 중에 중단되는 일을 방지할 수 있습니다.

---

## 의존성 설치

먼저 OCR 도구를 설치합니다. 터미널을 열고 다음 명령을 실행하세요:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **프로 팁:** 권한 오류가 발생하면 `pip install` 명령에 `--user` 옵션을 추가하거나 전역 설치를 위해 `pipx`를 사용하세요.

---

## Step 1 – OCR 엔진 초기화

엔진은 전체 프로세스의 핵심입니다. 각 픽셀을 살펴보고 어떤 문자가 어느 위치에 들어가야 하는지 판단하는 “두뇌”라고 생각하면 됩니다.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

왜 단일 함수를 호출하는 대신 엔진을 인스턴스화할까요? 엔진 객체를 사용하면 나중에 커스텀 후처리를 연결할 수 있어 출력에 대한 세밀한 제어가 가능해집니다—특히 **ocr table image python** 정확도가 필요할 때 필수적입니다.

---

## Step 2 – AI 후처리기 연결

`aocr`에는 셀 경계를 유지하면서 원시 OCR 결과를 정리해 주는 가벼운 AI 후처리기가 포함되어 있습니다. 추가 인자가 필요 없으므로 코드가 깔끔합니다.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

이 단계를 건너뛰면 원시 텍스트는 얻을 수 있지만 표 구조가 잡히지 않아 잡음이 많아집니다—마치 모든 셀의 내용이 미스테리인 스프레드시트와 같습니다. 후처리기가 텍스트를 원래 그리드에 맞추는 무거운 작업을 수행합니다.

---

## Step 3 – 표 이미지 로드

이미지는 어느 경로에서든 로드할 수 있지만, 여기서는 예시 디렉터리를 사용합니다. `"YOUR_DIRECTORY/invoice_table.png"`를 실제 파일 경로로 교체하세요.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **참고:** `aocr.Image`는 이미지 형식을 자동으로 감지하고 색 채널을 정규화하므로, 파일이 심하게 손상되지 않은 한 사전 처리할 필요가 없습니다.

---

## Step 4 – 구조화된 OCR 수행

이제 엔진이 이미지를 스캔하고 원시 표 객체를 반환합니다. 이 객체에는 행, 열 및 각 셀의 원시 텍스트가 포함됩니다.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

`recognize` 대신 `recognize_structured`를 사용하는 이유는 무엇일까요? 구조화된 버전은 행/열 경계를 추정하려 시도하여, 나중에 TSV로 변환하기 훨씬 쉬운 행렬 형태의 결과를 제공합니다.

---

## Step 5 – AI 후처리기로 데이터 정리

후처리기를 실행하면 원시 출력이 정제됩니다: 불필요한 문자 제거, 분할된 조각 병합, 각 셀 텍스트가 올바르게 정렬되도록 보장합니다.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

`processed_table.table`을 확인하면 행 리스트를 볼 수 있으며, 각 행은 `Cell` 객체 리스트입니다. 각 `Cell`은 정제된 문자열을 담고 있는 `.text` 속성을 가지고 있습니다.

---

## Step 6 – 표를 TSV로 내보내기

마지막 단계는 정제된 데이터를 탭 구분값(TSV) 파일로 변환하는 것입니다—Excel이나 Google Sheets용 **convert image to TSV**가 필요할 때 바로 사용할 수 있습니다.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

스크립트를 실행하면 각 행을 콘솔에 출력하고(원한다면) 모든 스프레드시트 프로그램에서 열 수 있는 깔끔한 TSV 파일을 작성합니다.

### 빠른 검증

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

다음과 같이 정렬된 열을 확인할 수 있습니다:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

출력이 뒤섞여 보인다면 이미지 품질(선명도, 대비)을 다시 확인하고 OCR 엔진 설정을 조정해 보세요—`engine.set_config(...)`를 사용하면 언어 모델과 신뢰도 임계값을 조정할 수 있습니다.

---

## 일반적인 엣지 케이스 처리

| Situation | Suggested Fix |
|-----------|---------------|
| **Skewed image** | `aocr`에 전달하기 전에 `Pillow`(`Image.rotate`)를 사용해 사전 회전합니다. |
| **Low contrast** | 가독성을 높이기 위해 히스토그램 균등화(`cv2.equalizeHist`)를 적용합니다. |
| **Merged cells** | 알려진 구분자를 기준으로 TSV를 후처리해 셀을 분할하거나, 가능하면 `merge_cells=False` 옵션을 사용합니다. |
| **Multi‑page PDFs** | 각 페이지를 먼저 이미지(`pdf2image`)로 변환한 뒤 파이프라인을 반복 실행합니다. |

이러한 조정으로 다양한 원본 자료에서도 **ocr table image python** 워크플로우를 견고하게 유지할 수 있습니다.

---

## 전체 스크립트 – 원스톱 솔루션

아래는 논의된 모든 단계를 포함한 완전한 실행 가능한 스크립트입니다. `extract_table.py`라는 이름으로 저장하고 `python extract_table.py`를 실행하세요.



## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 보여준 기술을 기반으로 하는 관련 주제를 다룹니다. 각 자료에는 완전한 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
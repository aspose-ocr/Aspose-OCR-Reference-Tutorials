---
category: general
date: 2026-03-26
description: Python OCR을 사용하여 이미지에서 표를 추출하고 이미지를 스프레드시트로 변환합니다. OCR을 위해 이미지를 로드하고,
  표를 읽으며, 표 데이터를 추출하는 방법을 배웁니다.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: ko
og_description: Python OCR을 사용해 이미지에서 표를 추출합니다. 이 가이드는 OCR용 이미지를 로드하고, 표를 읽은 뒤 스프레드시트로
  변환하는 방법을 보여줍니다.
og_title: 이미지에서 표 추출 – 완전 OCR 튜토리얼
tags:
- OCR
- Python
- Data Extraction
title: 이미지에서 표 추출 – 단계별 OCR 가이드
url: /ko/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 표 추출 – 완전 OCR 튜토리얼

이미지에서 **표를 추출**해야 할 때가 있었지만 어디서 시작해야 할지 몰랐나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 PDF나 스크린샷에 표 형태 데이터가 포함되어 있어 이를 편집 가능한 행과 열로 바꿔야 할 때 난관에 부딪히곤 합니다. 좋은 소식은? 몇 줄의 Python 코드와 강력한 OCR 엔진을 결합하면 그 사진을 몇 초 만에 사용할 수 있는 스프레드시트로 변환할 수 있다는 것입니다.

이 튜토리얼에서는 OCR용 이미지를 로드하고, 인식 엔진을 실행한 뒤, 각 표를 행 단위로 추출하는 과정을 단계별로 살펴봅니다. 마지막까지 진행하면 **이미지를 스프레드시트로 변환**할 수 있게 되고, **ocr read tables**와 **ocr extract table data**를 활용해 후속 처리까지 할 수 있게 됩니다. 숨겨진 마법은 없으며, 오늘 바로 프로젝트에 넣어 사용할 수 있는 명확하고 실행 가능한 코드만 제공됩니다.

---

## 필요 사항

- **Python 3.9+** – 최신 안정 버전이 가장 좋습니다.  
- **`ocr`** 라이브러리(또는 `OcrEngine`, `Image`, 표 관련 메서드를 제공하는 호환 OCR SDK). `pip install ocr‑sdk` 로 설치하세요(실제 패키지 이름으로 교체).  
- 명확히 인쇄된 표가 포함된 이미지 파일(`.png`, `.jpg` 등).  
- 선택 사항: **pandas** – 추출한 데이터를 바로 CSV 또는 Excel 파일로 저장하고 싶다면(`pip install pandas`).

모두 준비됐나요? 좋습니다—시작해봅시다.

---

## 단계 1: OCR SDK 가져오기 및 환경 준비

먼저 OCR 클래스를 스크립트에 가져오고, 나중에 원시 표 데이터를 DataFrame으로 변환할 작은 헬퍼를 설정해야 합니다.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**왜 중요한가:** `ocr`를 import하면 `OcrEngine`, `Imaging.Image`, 그리고 반복할 표 객체에 접근할 수 있습니다. `pandas`는 추출에 필수는 아니지만, **이미지를 스프레드시트로 변환**하는 작업을 매우 간단하게 만들어 줍니다.

---

## 단계 2: 처리할 이미지 로드하기

이제 실제로 **load image for OCR**를 수행합니다. SDK는 `Image` 객체를 기대하므로, 파일 경로를 헬퍼 메서드 `Image.load()` 로 감싸면 됩니다.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**팁:** 이미지 파일은 `assets/` 혹은 `data/` 같은 전용 폴더에 보관하고 상대 경로를 사용하세요. 이렇게 하면 스크립트를 다양한 머신에서 포터블하게 유지할 수 있습니다.

---

## 단계 3: 인식 프로세스 실행

이미지가 연결되었으니 이제 엔진에 **ocr read tables**를 요청할 수 있습니다. `recognize()` 호출은 엔진이 발견한 모든 정보를 담은 결과 객체를 반환합니다—텍스트 블록, 라인, 그리고 가장 중요한 표들까지.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**왜 확인하나요:** 일부 이미지가 잡음이 많거나 표 경계가 희미하면 엔진이 표를 놓칠 수 있습니다. 경고 로그를 남기면 스크립트가 중단되지 않고 초기에 피드백을 받을 수 있습니다.

---

## 단계 4: 각 표의 행과 셀 추출

실제 마법이 일어나는 부분입니다. 감지된 모든 표를 순회하면서 각 행을 꺼내고, 다시 각 셀의 텍스트를 추출합니다. 내부 리스트 컴프리헨션으로 코드를 간결하게 유지하면서도 흐름을 설명합니다.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**무슨 일이 일어나나요?**  

- `enumerate(..., start=1)` 은 로그에 친절한 표 번호를 제공합니다.  
- `row_obj.get_cells()` 은 각 셀 객체를 반환하고, `cell.get_text()` 는 OCR이 디코드한 문자열을 가져옵니다.  
- 행 데이터를 `rows_data`에 저장한 뒤 `pandas.DataFrame`에 전달하면 컬럼이 자동 정렬됩니다.  
- `print` 블록은 원본 스니펫에 표시된 **essential output**을 그대로 보여주어 결과를 즉시 확인할 수 있게 합니다.

**예외 상황 처리:** 행마다 셀 개수가 다르면 `pandas`가 누락된 부분을 `NaN`으로 채웁니다. 빈 문자열을 원한다면 `df.fillna('')` 로 나중에 정리할 수 있습니다.

---

## 단계 5: 추출한 표를 스프레드시트에 저장

이제 DataFrame 리스트가 준비됐으니, 이를 Excel 워크북(또는 CSV 파일)으로 변환하는 일은 아주 쉽습니다. 이렇게 하면 **이미지를 스프레드시트로 변환** 목표를 달성할 수 있습니다.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**왜 Excel인가?** 대부분의 비즈니스 사용자는 `.xlsx`를 선호합니다. CSV가 필요하면 루프를 `df.to_csv(f"table_{idx}.csv", index=False)` 로 교체하면 됩니다.

---

## 전체, 바로 실행 가능한 스크립트

모든 코드를 하나로 합치면 다음과 같은 완전한 프로그램이 됩니다. 복사‑붙여넣기만 하면 바로 실행할 수 있습니다.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**예상 콘솔 출력** (간단한 2×3 표 기준):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

스크립트 폴더에 `extracted_tables.xlsx` 파일이 생성되며, 각 표가 별도의 시트에 저장됩니다.

---

## 자주 묻는 질문 & 팁

| Question | Answer |
|----------|--------|
| **다른 OCR 라이브러리를 사용할 수 있나요?** | 물론입니다. 흐름은 동일합니다: 이미지 로드 → 인식 → `get_tables()` 순회. import와 객체 이름만 교체하면 됩니다. |
| **이미지가 잡음이 많으면 어떻게 해야 하나요?** | OCR 엔진에 전달하기 전에 OpenCV로 전처리(임계값 적용, 기울기 보정)하세요. 잡음 감소는 **ocr extract table data** 정확도를 크게 향상시킵니다. |
| **`openpyxl`을 설치해야 하나요?** | 네, `pandas`가 Excel 출력 시 내부적으로 `openpyxl`을 사용합니다. `pip install openpyxl` 로 설치하세요. |
| **병합된 셀은 어떻게 처리하나요?** | 일부 SDK에서는 `cell.is_merged()` 를 제공하므로, 이를 감지해 병합된 범위에 값을 수동으로 복사하면 됩니다. |
| **특정 표만 추출할 수 있나요?** | `table_obj.get_confidence()` 로 필터링하거나, 헤더 키워드를 검사해 원하는 표만 처리하도록 할 수 있습니다. |

---

## 마무리

이제 **이미지에서 표를 추출**하고 결과를 깔끔한 스프레드시트로 변환하며, 하나의 사진에 여러 표가 있더라도 처리할 수 있는 완전한 엔드‑투‑엔드 솔루션을 갖추었습니다. 스크립트는 **load image for OCR**, **ocr read tables**, **ocr extract table data** 를 어떻게 수행하는지 보여주면서 실제 환경에 맞게 유연하게 확장할 수 있습니다.

다음 단계는? OCR 엔진에 PDF 페이지를 이미지로 렌더링해서 입력해 보거나, 다양한 언어와 폰트를 실험해 보세요. DataFrame을 바로 데이터베이스나 보고서 도구에 파이프라인으로 연결할 수도 있습니다—가능성은 무한합니다.

이 가이드가 도움이 되었다면 공유하거나, SDK를 호스팅하는 저장소에 별표를 달고, 여러분만의 팁을 댓글로 남겨 주세요. 즐거운 코딩 되시고, 표가 언제나 완벽히 파싱되길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
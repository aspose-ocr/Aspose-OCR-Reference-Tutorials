---
category: general
date: 2026-04-26
description: Python에서 문서를 일괄 OCR하고 스캔에서 텍스트를 추출하는 방법. OcrEngine을 사용한 단계별 일괄 처리와 JSON
  출력 방법을 배워보세요.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: ko
og_description: 스캔 파일을 일괄 OCR 처리하고 한 스크립트로 스캔에서 텍스트를 추출하는 방법. 전체 코드, 팁, 그리고 예외 상황
  처리.
og_title: 배치 OCR 방법 – 빠른 파이썬 가이드
tags:
- OCR
- Python
- Automation
title: 배치 OCR 방법 – 스캔에서 텍스트를 효율적으로 추출하기
url: /ko/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR – 스캔에서 텍스트 효율적으로 추출하기

스캔한 PDF가 산처럼 쌓여도 **how to batch OCR** 할 수 있을지 궁금하셨나요? 당신만 그런 것이 아닙니다—개발자들은 계속해서 *“스캔에서 텍스트를 한 번에 추출하려면 어떻게 해야 하나요?”* 라고 묻습니다. 좋은 소식은 몇 줄의 Python 코드만으로 그 지루한 작업을 부드럽고 자동화된 파이프라인으로 바꿀 수 있다는 것입니다.

이 튜토리얼에서는 **extracts text from scans**하고, 결과를 JSON으로 저장하며, 마지막에 간단한 정상 여부 확인을 제공하는 완전하고 바로 실행 가능한 솔루션을 단계별로 살펴보겠습니다. 외부 서비스도, 마법도 없습니다—그냥 순수 Python, `OcrEngine` 클래스, 그리고 약간의 폴더 관리만 있으면 됩니다.

## 배울 수 있는 내용

- 이미지 폴더에 대해 **batches OCR**을 수행하는 완전한 기능의 스크립트.
- *why* 각 라인이 존재하는 이유에 대한 명확한 설명, *what* 하는지에 대한 설명만이 아니라.
- 빈 폴더, 이미지가 아닌 파일, 대용량 배치를 처리하기 위한 팁.
- JSON 출력에 실제로 추출된 텍스트가 포함되어 있는지 확인하는 방법.

### 전제 조건 (최소 요구 사항)

| 요구 사항 | 중요한 이유 |
|-------------|----------------|
| Python 3.8+ | 최신 구문 및 타입 힌트 |
| `OcrEngine` library (or a compatible wrapper) | 핵심 OCR 기능 |
| A directory with scanned image files (PNG, JPG, TIFF) | 스캔된 이미지 파일(PNG, JPG, TIFF)이 있는 디렉터리 |
| Write permissions for the output folder | 출력 폴더에 대한 쓰기 권한 |

이미 준비되었다면, 좋습니다—시작해봅시다.

![배치 OCR 워크플로우](image-placeholder.png){alt="배치 OCR 워크플로우"}

## Step 1 – OCR 엔진 초기화 (how to batch OCR)

무엇이든 처리하기 전에 OCR 엔진 인스턴스가 필요합니다. 이를 각 이미지를 읽고 텍스트를 출력하는 “두뇌”라고 생각하면 됩니다. 한 번 초기화하고 전체 배치에서 재사용하는 것이 가장 효율적인 패턴입니다.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **왜 같은 인스턴스를 재사용할까요?**  
> 파일마다 새로운 엔진을 만들면 무거운 모델을 메모리에 반복해서 로드하게 되어 배치 속도가 크게 느려집니다. 하나의 인스턴스는 모델을 RAM에 유지하고 수천 장의 이미지를 눈에 띄는 지연 없이 처리할 수 있게 합니다.

## Step 2 – 스캔 폴더 지정 (extract text from scans)

스캔 파일은 디스크 어딘가에 있습니다. 스크립트에 그 위치를 알려줍시다. 절대 경로를 사용하면 스크립트를 다른 작업 디렉터리에서 실행할 때 발생할 수 있는 “파일을 찾을 수 없음” 오류를 방지할 수 있습니다.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **팁:**  
> Windows 환경이라면, 슬래시(`/`)를 `os.path.abspath`와 함께 그대로 사용해도 문제없으므로 역슬래시를 이스케이프할 필요가 없습니다.

## Step 3 – JSON 결과 저장 위치 선택

OCR 결과를 위한 깔끔한 폴더가 필요할 것입니다. 출력과 원본을 분리하면 나중에 정리하거나 JSON을 다른 파이프라인에 전달하기가 쉬워집니다.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **왜 프로그래밍적으로 폴더를 생성할까요?**  
> 디렉터리가 없을 경우 스크립트가 충돌하는 것을 방지하고, `exist_ok=True` 덕분에 작업이 멱등성을 갖게 되어 스크립트를 여러 번 실행해도 오류가 발생하지 않습니다.

## Step 4 – 배치 프로세스 실행 (how to batch OCR)

이제 핵심 단계입니다: `ocr_engine`에 `input_dir`의 모든 파일을 순회하도록 지시하고, OCR을 실행한 뒤 결과를 `output_dir`에 JSON으로 저장합니다. `format="json"` 플래그는 엔진에게 결과를 구조화된 형태로 직렬화하도록 알려주며, 이는 후속 도구들이 선호합니다.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### 내부에서 무슨 일이 일어나고 있을까요?

1. **File discovery** – 엔진은 `input_folder`를 재귀적으로 스캔하고 숨김 파일은 무시합니다.
2. **File validation** – 지원되는 이미지 확장자(`.png`, `.jpg`, `.tif` 등)만 OCR 모델에 전달됩니다.
3. **OCR execution** – 각 이미지를 OCR 엔진에 전달하고 텍스트, 신뢰도 점수, 레이아웃 데이터를 캡처합니다.
4. **JSON serialization** – 결과를 `output_folder`에 같은 기본 이름이지만 `.json` 확장자를 가진 파일로 저장합니다.

> **예외 상황 처리:**  
> - **Empty folder:** 엔진은 “No files found”를 로그에 남기고 정상적으로 반환합니다.  
> - **Corrupt image:** 파일을 건너뛰고 `batch_errors.log`에 오류 항목을 기록한 뒤 계속 진행합니다.  
> - **Huge batch (10k+ files):** 각 이미지를 독립적으로 처리하므로 메모리 사용량이 낮게 유지됩니다.

## Step 5 – 변환 완료 확인

간단한 `print` 문은 콘솔에 즉시 피드백을 제공합니다. 실제 운영 파이프라인에서는 이를 로깅 호출이나 이메일 알림으로 교체할 수 있습니다.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

해당 문구가 출력되면, `json_output` 폴더를 안전하게 확인할 수 있습니다. 각 JSON 파일은 대략 다음과 같은 형태일 것입니다:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

이제 이러한 JSON 파일을 데이터베이스, 검색 인덱스, 혹은 다른 분석 도구에 전달할 수 있습니다.

## 자주 묻는 질문 (및 빠른 답변)

**Q: 이미지 대신 PDF를 처리해야 하면 어떻게 하나요?**  
A: 각 PDF 페이지를 먼저 이미지로 변환(`pdf2image` 등 사용)하고, 생성된 PNG/JPG 파일을 `input_dir`에 넣습니다. 배치 OCR 로직은 그대로 유지됩니다.

**Q: 출력 형식을 일반 텍스트로 바꿀 수 있나요?**  
A: 물론입니다. `format="json"`을 `format="txt"`로 바꾸면 엔진이 추출된 텍스트만 포함한 `.txt` 파일을 작성합니다.

**Q: 스캔 파일이 여러 하위 폴더에 있는데, 스크립트가 재귀적으로 탐색하나요?**  
A: 네. `batch_process`는 기본적으로 디렉터리 트리를 순회합니다. 평탄한 출력을 원한다면 `flatten=True`(라이브러리가 지원한다면)로 설정하거나 JSON 파일명을 후처리하세요.

**Q: 라틴 문자 이외의 스크립트를 처리하려면 어떻게 해야 하나요?**  
A: `OcrEngine`을 언어 파라미터와 함께 초기화합니다. 예: `OcrEngine(lang="spa+eng")`. 배치 루프 자체는 변경할 필요가 없습니다.

## 전문가 팁 및 흔히 겪는 함정

- **Batch size matters:** CPU 스파이크가 발생하면 파일 사이에 간단히 `time.sleep(0.1)`을 삽입해 처리 속도를 조절하세요.
- **Logging:** `print` 호출을 Python의 `logging` 모듈로 교체하면 타임스탬프와 오류 수준을 기록할 수 있습니다.
- **File naming collisions:** 두 스캔이 같은 기본 이름을 가지고 다른 하위 폴더에 있을 경우 JSON 파일이 서로 덮어씁니다. 충돌을 방지하려면 출력 이름에 상대 경로의 해시를 추가하세요.
- **Memory leaks:** 일부 OCR 백엔드는 네이티브 리소스를 유지합니다. 라이브러리가 정리 메서드를 제공한다면 스크립트 끝에서 `ocr_engine.close()`를 호출하세요.

## 전체 스크립트 – 복사·붙여넣기 바로 사용

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**예상 콘솔 출력**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

`json_output`의 파일을 텍스트 편집기로 열거나 Python에서 로드하여 JSON을 확인할 수 있습니다:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

콘솔에 원시 OCR 추출 텍스트가 출력되는 것을 확인할 수 있을 것입니다.

## 마무리

우리는 **how to batch OCR** 전체 디렉터리의 스캔 이미지들을 처리하고 **extract text from scans**를 깔끔하고 기계가 읽을 수 있는 JSON 파일로 추출하는 방법을 다루었습니다. 접근 방식은 의도적으로 단순합니다: 엔진을 한 번 설정하고 폴더를 지정하면 라이브러리가 무거운 작업을 처리합니다. 이제 다음과 같이 활용할 수 있습니다:

- JSON을 연결

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
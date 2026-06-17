---
category: general
date: 2026-03-18
description: 이미지에서 텍스트를 빠르게 추출하기 위해 OCR을 수행합니다. OCR을 위한 이미지 로드 방법, OCR 엔진 생성 방법, 언어
  옵션을 활용한 OCR 정확도 향상 방법을 배웁니다.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: ko
og_description: 이 상세 가이드를 통해 이미지에 OCR을 수행하세요. OCR을 위한 이미지 로드 방법, OCR 엔진 생성, 그리고 신뢰할
  수 있는 텍스트 추출을 위한 OCR 정확도 향상 방법을 배웁니다.
og_title: 이미지에서 OCR 수행 – 완전한 프로그래밍 튜토리얼
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 이미지에서 OCR 수행 – 단계별 가이드
url: /ko/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 OCR 수행 – 완전 프로그래밍 튜토리얼

이미지에서 OCR을 수행해야 했지만 어떤 라이브러리를 선택해야 할지, 신뢰할 수 있는 결과를 얻는 방법을 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다. 이 가이드에서는 **perform OCR on image**에 필요한 모든 것을, 사진을 로드하고 **extract text from image**까지, 언어 옵션을 조정하여 **improve OCR accuracy**를 단계별로 안내합니다.

우리는 **load image for OCR** 방법과 **create OCR engine** 방법, 그리고 각 설정이 왜 중요한지 다룰 것입니다. 끝까지 하면 인식된 텍스트를 출력하는 바로 실행 가능한 스크립트를 얻게 되고, 각 줄 뒤에 숨은 “왜”를 이해하게 됩니다—모호한 “문서 참고”식 단축키 없이. 시작해봅시다.

## 필요 사항

- Python 3.8+ (코드에서 f‑strings와 타입 힌트를 사용합니다)
- 가상의 `ocr_lib` 패키지 – `pip install ocr_lib` 로 설치
- 선명한 인쇄 텍스트가 포함된 이미지 파일 (예: `lab_report.png`)
- 기본 텍스트 편집기 또는 IDE (VS Code, PyCharm 등)

이미 가지고 있다면, 좋습니다—준비가 끝났습니다. 없으면 python.org에서 Python을 다운로드하고 pip 명령을 실행하세요; 1분이면 충분합니다.

![perform OCR on image 예시](/images/ocr-example.png)

*Alt text: perform OCR on image – 추출된 텍스트를 보여주는 샘플 출력.*

## 1단계: OCR 엔진 생성 – Python에서 **create OCR engine** 방법

인식이 이루어지기 전에, 라이브러리는 구성 및 런타임 상태를 보관하는 엔진 객체가 필요합니다. 엔진을 작업을 제어하는 두뇌라고 생각하면 됩니다.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Why this matters:** 엔진을 미리 인스턴스화하면 나중에 언어 옵션을 연결할 수 있고, 내부 모델을 캐시해 이후 호출을 더 빠르게 할 수 있습니다.

## 2단계: OCR을 위한 이미지 로드 – 올바른 **load image for OCR** 방법

엔진을 확보했으니 이제 읽을 대상을 제공해야 합니다. `setImageFromFile` 메서드는 파일 시스템 경로를 받아들이며, 경로는 절대 경로나 스크립트 작업 디렉터리에 대한 상대 경로일 수 있습니다.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro tip:** 스크립트가 다른 폴더에서 실행될 때 “파일을 찾을 수 없습니다” 오류를 방지하려면 절대 경로나 `os.path.join`을 사용하세요.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## 3단계: OCR 정확도 향상 – **language options**을 조정하여 **improve OCR accuracy**

기본 OCR도 작동하지만, 도메인 특화 어휘(예: 실험실 용어)는 종종 인식을 방해합니다. 사용자 정의 사전과 블랙리스트를 제공하면 “0”과 “O”를 혼동하는 등 오인식을 줄일 수 있습니다.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Why this helps:** 사전은 OCR 모델에 “HPLC”가 유효한 토큰임을 알려 주어 단어가 무의미하게 분해되는 것을 방지합니다. 블랙리스트는 모델에게 모호한 기호를 노이즈로 처리하도록 알려 주어 직접적으로 **improve OCR accuracy**를 향상시킵니다.

## 4단계: 이미지에서 OCR 수행 – 핵심 **perform OCR on image** 호출

엔진이 준비되고 이미지가 연결되면 실제로 텍스트를 인식할 시간입니다. 이 단계는 원시 텍스트, 신뢰도 점수, 경계 상자 등을 조회할 수 있는 `OcrResult` 객체를 반환합니다.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

이미지가 흐릿하면 결과에 낮은 신뢰도 수치가 나타납니다. 이는 엔진에 전달하기 전에 이미지를 전처리(예: 대비 증가)해야 함을 의미합니다.

## 5단계: 이미지에서 텍스트 추출 – 최종 문자열 얻기

마지막으로 `OcrResult`에 텍스트 표현을 요청합니다. `getText()` 메서드는 파일 저장, 데이터베이스 입력 등 후속 처리에 바로 사용할 수 있는 평문 문자열을 반환합니다.

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Expected output:** `lab_report.png`에 간단한 표가 포함되어 있다고 가정하면 다음과 같은 출력이 나올 수 있습니다:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

이렇게 하면 **extract text from image** 부분이 완료됩니다.

## 전체 작업 예제 – 모든 것을 하나로 묶기

아래는 이전 섹션의 조각들을 하나로 연결한 단일 스크립트입니다. `run_ocr.py`에 복사‑붙여넣기하고 `python run_ocr.py`를 실행하면 됩니다.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### 빠른 검증 체크리스트

| ✅ | 항목 |
|---|------|
| ✔️ | Engine is created (`create OCR engine`) |
| ✔️ | Image is loaded (`load image for OCR`) |
| ✔️ | Language options are set (`improve OCR accuracy`) |
| ✔️ | OCR is performed (`perform OCR on image`) |
| ✔️ | Text is extracted (`extract text from image`) |

스크립트를 실행하고 콘솔을 확인하세요. 보고서 내용이 포함된 “OCR Output” 블록이 보이면 **perform OCR on image**를 성공적으로 수행한 것입니다.

## 일반적인 함정 및 회피 방법

| 문제 | 발생 원인 | 해결 방법 |
|------|----------|----------|
| **Blurry input** | OCR 모델이 문자를 구분하지 못함 | OpenCV로 전처리: `cv2.GaussianBlur` 또는 DPI 증가 |
| **Wrong language** | 기본 언어가 영어가 아닌 다른 언어로 설정될 수 있음 | `recognize()` 호출 전에 `engine.setLanguage("eng")` 호출 |
| **Missing dictionary terms** | 도메인 특화 단어가 깨짐 | Step 3에서 보여준 대로 `setDictionary` 로 추가 |
| **Blacklisted characters cause

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
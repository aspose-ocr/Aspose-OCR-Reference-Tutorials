---
category: general
date: 2026-07-05
description: Python을 사용하여 이미지에서 OCR을 수행합니다. 이미지에서 텍스트로 변환하는 방법, OCR을 위한 이미지 로드 및 몇
  분 안에 이미지에서 키릴 문자 텍스트를 추출하는 방법을 배워보세요.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: ko
og_description: Python에서 이미지에 OCR을 수행합니다. 이 가이드는 이미지에서 텍스트를 파이썬으로 변환하고, OCR을 위해 이미지를
  로드하며, 이미지에서 키릴 문자 텍스트를 빠르게 추출하는 방법을 보여줍니다.
og_title: Python으로 이미지 OCR 수행 – 전체 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Python으로 이미지 OCR 수행 – 완전 단계별 가이드
url: /ko/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 OCR 수행하기 (Python) – 완전 단계별 가이드

이미지 파일에 **perform OCR on image** 를 수행하면서 제3자 서비스에 넘기지 않을 수 있을까 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 여권 스캐너, 영수증 디지털화, 아카이브 도구 등 많은 프로젝트에서 사진으로부터 원시 텍스트를 추출하는 것이 첫 번째 장벽입니다.  

이 튜토리얼에서는 **converts image to text python** 스타일의 실용적인 예제를 단계별로 살펴보고, **load image for OCR** 방법을 보여준 뒤, 오픈소스 `aocr` 라이브러리를 사용해 **extract Cyrillic text from image** 를 수행합니다. 마지막까지 따라오시면 어떤 사진이든 **recognize Cyrillic text** 할 수 있게 됩니다.

> **얻을 수 있는 것:** 바로 실행 가능한 스크립트, 각 단계에 대한 명확한 설명, 흐릿한 스캔이나 예상치 못한 폰트와 같은 일반적인 함정에 대한 팁. 외부 API 없이 순수 Python만 사용합니다.

---

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- Python 3.8 이상 설치
- 익숙한 터미널 또는 명령 프롬프트
- `aocr` 패키지 (`pip install aocr` 로 설치 가능)
- 키릴 문자가 포함된 이미지 파일 (예: 스캔한 러시아 여권)

이 중 익숙하지 않은 부분이 있더라도 걱정 마세요—각 항목은 아래에서 간략히 다룹니다.

---

## Step 1: Perform OCR on Image – Setting Up the Environment

먼저 OCR 라이브러리를 설치할 깨끗한 Python 환경이 필요합니다. 가상 환경을 사용하면 의존성을 격리하고 버전 충돌을 방지할 수 있습니다.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Why?**  
전용 환경을 사용하면 `aocr` 패키지와 그 네이티브 바이너리가 다른 프로젝트와 충돌하지 않습니다. 또한 재현성이 뛰어나게 됩니다—다른 사람이 레포를 복제하고 동일한 `pip install -r requirements.txt` 명령을 실행하면 똑같은 환경을 얻을 수 있죠.

> **Pro tip:** `pip freeze > requirements.txt` 로 의존성을 고정해 두면 언제든 정확히 어떤 버전을 사용했는지 알 수 있습니다.

---

## Step 2: Load Image for OCR – Importing and Preparing the File

라이브러리가 준비되었으니 이제 **load image for OCR** 해야 합니다. `aocr.Image.from_file` 메서드는 PNG, JPEG, TIFF 등 대부분의 일반 포맷을 처리합니다. 사용 방법은 다음과 같습니다:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**What’s happening here?**  
`aocr.Image.from_file` 은 바이너리 데이터를 읽어 디코딩하고 OCR 엔진이 이해할 수 있는 객체에 저장합니다. 파일을 찾을 수 없으면 Python 이 `FileNotFoundError` 를 발생시키며, 필요에 따라 나중에 예외 처리를 추가할 수 있습니다.

> **Edge case:** 일부 스캐너는 다중 페이지 TIFF를 출력합니다. 이 경우 먼저 페이지를 분리해야 하는데, `aocr` 은 `Image.from_tiff_pages()` 를 제공하고 있습니다.

---

## Step 3: Configure the OCR Engine – Forcing Cyrillic Recognition

기본적으로 많은 OCR 엔진은 언어를 추측하려고 하는데, 라틴 문자가 아닌 스크립트에서는 결과가 엉망이 될 수 있습니다. **recognize Cyrillic text** 를 안정적으로 수행하려면 언어를 명시적으로 “cyrillic” 으로 설정합니다.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Why force the language?**  
키릴 문자는 라틴 문자와 시각적으로 유사한 경우가 많습니다(예: “A” vs “А”). 엔진에 키릴을 기대하도록 알려 주면 특히 저해상도 스캔에서 오인식이 크게 줄어듭니다.

---

## Step 4: Perform OCR on Image – Running the Recognition

이미지를 로드하고 엔진을 조정했으니 이제 **perform OCR on image** 를 실행합니다. `recognize` 메서드는 추출된 텍스트와 신뢰도 점수를 담은 `OcrResult` 객체를 반환합니다.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**What does `ocr_result` give you?**  
- `text`: 인식된 문자들의 평문 문자열  
- `confidence`: 전체 신뢰도를 나타내는 0‑1 사이 실수  
- `lines`: 세부 제어가 필요할 경우 사용할 수 있는 라인 객체 리스트  

> **Common question:** *텍스트가 뒤집혀 있으면 어떻게 하나요?*  
> `aocr` 은 자동 회전 기능을 제공하므로 `ocr_engine.auto_rotate = True` 로 설정한 뒤 `recognize` 를 호출하면 됩니다.

---

## Step 5: Convert Image to Text Python – Post‑Processing the Output

원시 문자열에는 불필요한 공백이나 줄바꿈이 포함될 수 있습니다. **convert image to text python** 스타일로 깔끔하게 만들기 위해 몇 가지 간단한 정리 작업을 수행합니다:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Why bother?**  
정제된 출력은 데이터베이스 저장, 번역 API 호출, 혹은 여권 번호와 같은 정규식 검색 등 후속 파이프라인에 바로 활용하기가 훨씬 쉽습니다.

---

## Step 6: Extract Cyrillic Text from Image – Putting It All Together

이제 모든 과정을 하나의 재사용 가능한 함수로 묶어 보겠습니다. 이렇게 하면 **extract Cyrillic text from image** 를 여러분 프로젝트에서 한 줄 호출만으로 사용할 수 있습니다.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Result you should see (sample):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

이미지가 선명하고 폰트가 OCR 모델과 일치한다면 거의 완벽에 가까운 전사 결과를 얻을 수 있습니다.

---

## troubleshooting & Tips

| Issue | Likely Cause | Fix |
|-------|--------------|-----|
| Garbled characters | Wrong language setting | Ensure `ocr_engine.language = "cyrillic"` |
| Empty output | Image too dark or low‑resolution | Preprocess with `opencv` to increase contrast |
| Wrong orientation | Image rotated 90° | Set `ocr_engine.auto_rotate = True` |
| Slow performance | Large image ( >5 MP ) | Resize with `aocr.Image.resize(width=1024)` before recognition |

---

![이미지에서 OCR 수행 예시](ocr_example.png "이미지에서 OCR 수행 예시")

*Alt text: “이미지에서 OCR 수행 예시가 Python 코드를 사용해 여권 스캔에서 키릴 텍스트를 추출하는 모습을 보여줍니다.”*

---

## Conclusion

우리는 순수 Python만으로 **perform OCR on image** 파일을 처리하고, **load image for OCR** 방법을 배우며, 엔진에 **recognize Cyrillic text** 를 강제하고, 최종적으로 **extract Cyrillic text from image** 를 깔끔한 헬퍼 함수로 구현했습니다. `aocr` 설치부터 결과 정제까지 전체 파이프라인은 몇 십 줄의 코드로 구성되며, **convert image to text python** 스타일이 필요한 어느 프로젝트에도 쉽게 삽입할 수 있습니다.

---

## What’s Next?

- **Batch processing:** 스캔 폴더를 순회하며 결과를 SQLite에 저장  
- **Language detection:** `langdetect` 와 `aocr` 를 결합해 키릴과 라틴을 자동 전환  
- **Advanced preprocessing:** `opencv` 로 이미지 기울임 보정, 노이즈 제거, 이진화 등 전처리 수행으로 정확도 향상  
- **Integrate with FastAPI:** `extract_cyrillic_text` 함수를 REST 엔드포인트로 노출해 웹 앱에 연결  

언어를 “latin” 으로 바꿔 영어 여권을 처리하거나, 다른 OCR 백엔드로 교체해도 개념은 동일하고 코드는 유연하게 적용됩니다.

행복한 코딩 되세요, 그리고 이미지가 언제나 읽을 수 있기를 바랍니다!

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하여 관련 주제를 심도 있게 다룹니다. 각각 완전한 코드 예제와 단계별 설명을 제공하니, 추가 API 기능을 마스터하고 다양한 구현 방식을 탐구해 보세요.

- [Aspose OCR을 사용한 이미지에서 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [이미지를 텍스트로 변환 – URL에서 이미지에 OCR 수행](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Aspose.OCR을 사용한 언어 선택이 가능한 C# 이미지 텍스트 추출](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
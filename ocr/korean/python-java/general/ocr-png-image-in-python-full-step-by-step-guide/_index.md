---
category: general
date: 2026-06-06
description: Python으로 PNG 이미지 OCR – 이미지에서 텍스트를 추출하는 방법을 배우고, 파이썬 OCR 예제를 실행하며, 고대
  그리스어 텍스트까지 쉽게 읽어보세요.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: ko
og_description: Python에서 OCR PNG 이미지 사용법을 설명합니다. 이 가이드는 이미지에서 텍스트를 추출하고, 파이썬 OCR 예제를
  실행하며, 고대 그리스를 손쉽게 읽는 방법을 보여줍니다.
og_title: Python에서 PNG 이미지 OCR – 완전 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python에서 PNG 이미지 OCR – 전체 단계별 가이드
url: /ko/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 OCR PNG 이미지 – 전체 단계별 가이드

Python 스크립트만으로 **OCR PNG image** 파일을 처리하는 방법이 궁금하셨나요? 스캔한 고대 원고가 가득한 폴더가 있고, **extract text from image** 파일을 일일이 타이핑하지 않고 추출하고 싶을 때가 있죠. 좋은 소식은 컴퓨터 비전 박사 학위가 필요 없다는 겁니다—몇 줄의 코드와 올바른 라이브러리만 있으면 몇 초 만에 고대 그리스를 읽을 수 있습니다.

이 튜토리얼에서는 PNG에서 텍스트를 인식하고, 언어를 Greek polytonic으로 설정한 뒤 결과를 출력하는 **python OCR example**을 단계별로 살펴봅니다. 끝까지 읽으면 **recognize image text** 방법을 정확히 이해하고, 흔히 발생하는 문제들을 해결하며, 다른 언어와 이미지 포맷에 스크립트를 적용하는 방법을 알게 됩니다.

## What You’ll Learn

- Python OCR 라이브러리(pytesseract + Tesseract OCR) 설치 및 설정
- OCR 엔진 인스턴스를 만들고 PNG 파일 로드
- 언어를 Greek polytonic으로 설정하여 **read ancient greek** 가능하게 만들기
- 인식된 텍스트 출력 및 일반적인 문제 해결
- 여러 PNG를 배치 처리하거나 다른 언어로 전환하는 방법 확장

### Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | 현대 문법 및 타입 힌트 |
| `pytesseract` package | Tesseract 엔진을 감싸는 얇은 래퍼 |
| Tesseract OCR binaries (≥ 5.0) | 실제 OCR 엔진 자체 |
| Greek language data (`grc.traineddata`) | **read ancient greek** 를 정확히 인식하기 위해 필요 |
| 분석하려는 PNG 이미지 (예: `ancient_greek.png`) | **ocr png image** 데모의 대상 파일 |

Python 쪽은 다음과 같이 설치할 수 있습니다:

```bash
pip install pytesseract Pillow
```

Ubuntu/macOS에서는 엔진 자체를 추가로 설치합니다:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Greek polytonic 학습 데이터를 다운로드하는 것을 잊지 마세요:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(경로는 시스템에 따라 다를 수 있으니 `TESSDATA_PREFIX` 를 필요에 맞게 조정하세요.)*

---

## OCR PNG Image: Create the Engine Instance

먼저 Tesseract와 통신할 객체가 필요합니다. `pytesseract`에서는 모듈 수준 함수로 엔진에 접근하지만, 명확성을 위해 작은 클래스로 감싸겠습니다. 이는 원본 스니펫에서 보던 “engine” 개념을 그대로 반영합니다.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**왜 래핑하나요?**  
- 시작할 때 사용한 스니펫과 동일한 공개 API를 유지해 마이그레이션이 쉬워집니다.  
- 나중에 로깅이나 오류 처리를 추가해도 메인 흐름을 건드릴 필요가 없습니다.  
- 좋은 OOP 실천을 보여줍니다—시니어 개발자들이 선호하는 방식이죠.

---

## Extract Text from Image: Set the Language to Greek Polytonic

엔진을 만든 뒤에는 어떤 언어를 인식할지 알려줘야 합니다. Greek polytonic은 표준 “greek” 데이터에 포함되지 않은 부호가 있으므로, `grc` 학습 파일을 지정합니다.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

다른 언어로 **extract text from image** 하고 싶다면 `"grc"` 를 `"eng"`(영어), `"fra"`(프랑스어) 등으로 바꾸면 됩니다. 설치된 언어라면 동일한 한 줄로 동작합니다.

---

## Recognize Image Text: Run the OCR on a PNG

언어를 설정했으니 PNG를 엔진에 전달합니다. 원본 예제는 하드코딩된 경로를 사용했지만, 여기서는 `Path` 객체를 활용해 약간 더 유연하게 만들었습니다.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**팁 & 엣지 케이스**

- **File not found** – `try/except FileNotFoundError` 로 감싸 친절한 메시지를 제공하세요.  
- **Low‑resolution PNG** – OCR 전에 Pillow로 리사이징·이진화 같은 전처리를 고려하세요.  
- **Non‑Greek text** – Tesseract가 여전히 시도하지만 정확도가 크게 떨어집니다. 항상 언어를 맞춰 주세요.

---

## Output the Recognized Text

마지막으로 결과를 출력합니다. 실제 프로젝트에서는 데이터베이스, CSV, 혹은 번역 파이프라인에 전달할 수도 있습니다.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

깨끗한 고대 그리스 비문을 스캔한 파일을 실행하면 다음과 비슷한 출력이 나타납니다:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

출력이 깨져 보이면 **greek.traineddata** 파일이 올바른 폴더에 있는지, PNG가 너무 노이즈가 없는지 다시 확인하세요.

---

## Full Working Example (All Steps in One Script)

아래는 완전한 실행 가능한 프로그램 전체입니다. `ocr_greek.py` 로 저장하고 `python ocr_greek.py` 로 실행하세요.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**예상 출력** (일부만 발췌):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

올바른 그리스 문자들이 보이면 축하합니다—Python에서 **ocr png image** 작업을 성공적으로 수행한 것입니다!

---

## Common Questions & Pro Tips

### How do I improve accuracy on a noisy PNG?

- 이미지를 그레이스케일로 변환: `img = img.convert('L')`
- 이진 임계값 적용: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)` 로 확대

이 단계들은 **recognize image text** 를 악몽에서 깨끗한 결과로 바꾸는 데 자주 도움이 됩니다.

### Can I process a whole folder of PNGs?

물론입니다. `recognize_image` 호출을 `Path.glob("*.png")` 로 순회하는 `for` 루프로 감싸면 됩니다. 결과를 딕셔너리에 저장하거나 CSV로 기록해 나중에 분석하세요.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### What if I need to extract numbers only?

`image_to_string` 에 커스텀 **config** 문자열을 전달하면 됩니다:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

이렇게 하면 표, 일련 번호, 타임스탬프 등 숫자만 포함된 **extract text from image** 파일에서도 원하는 결과를 얻을 수 있습니다.

### Is there a way to get confidence scores?

네—`pytesseract.image_to_data` 를 사용하면 단어별 신뢰도 점수가 포함된 TSV를 반환합니다. 최종 문자열을 만들기 전에 낮은 신뢰도의 토큰을 필터링할 수 있습니다.

---

## Extending the Tutorial

기본을 마스터했으니 다음 주제들을 탐구해 보세요:

- **Batch OCR with multiprocessing** – 대량 PNG 코퍼스 처리 속도 향상  
- **Hybrid OCR + NLP pipelines** – 추출한 고대 그리스를 현대 영어로 자동 번역  
- **Alternative engines** – 특정 상황에 맞는 `easyocr` 혹은 `opencv` 기반 방법 시도  
- **Cloud OCR services** – 서버리스 확장을 위한 Google Vision, Azure Computer Vision, AWS Textract 등

이 모든 내용은 방금 다룬 **python ocr example** 을 기반으로 하므로, 더 깊이 파고들어도 자연스럽게 이해할 수 있습니다.

---

## Conclusion

간단한 스니펫을 견고한 **ocr png image** 워크플로우로 확장했습니다. `OcrEngine` 을 만들고, 언어를 Greek polytonic 으로 설정하고, PNG를 입력해 결과를 출력함으로써 이제 **extract text from image** 파일, **recognize image text**, 그리고 **read ancient greek** 를 수행하는 방법을 알게 되었습니다.

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 배운 기술을 확장하는 데 도움이 되는 관련 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하므로, 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있습니다.

- [이미지에서 텍스트 추출 – Aspose OCR 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR 이미지 인식에서 임계값 설정 방법](/ocr/english/net/ocr-settings/set-threshold-value/)
- [다국어를 위한 Aspose OCR 텍스트 인식](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
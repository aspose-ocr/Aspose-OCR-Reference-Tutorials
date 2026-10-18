---
category: general
date: 2026-04-26
description: '파이썬 OCR 방법: 기본 OCR 예제를 사용하여 이미지에서 텍스트를 추출하고 TIFF 파일을 파이썬으로 읽는 방법을 배웁니다.
  빠른 실행 가능한 코드 포함.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: ko
og_description: '파이썬 OCR 방법: 이미지에서 텍스트를 추출하고, 파이썬으로 TIFF 파일을 읽으며, 스캔한 이미지 텍스트를 간단하고
  실행 가능한 스크립트로 변환하는 단계별 가이드.'
og_title: Python으로 OCR하는 방법 – 텍스트 추출을 위한 기본 OCR 예제
tags:
- OCR
- Python
- Image Processing
title: Python으로 OCR 하는 방법 – 텍스트 추출을 위한 기본 OCR 예제
url: /ko/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr python – 텍스트 추출을 위한 기본 OCR 예제

스캔한 TIFF 파일이 책상 위에 놓여 있을 때 **how to ocr python**이 궁금했던 적 있나요? 이미지 파일들을 바라보며 “이 안에서 텍스트를 어떻게 뽑아낼까?”라고 고민하는 당신만은 아닙니다. 올바른 라이브러리와 몇 가지 명확한 단계만 있으면 사진을 순수 텍스트로 바꾸는 일은 식은 죽 먹기입니다.

이 튜토리얼에서는 TIFF 파일을 읽고, 텍스트를 추출한 뒤 콘솔에 출력하는 **기본 OCR 예제**를 단계별로 살펴봅니다. 끝까지 따라오면 **이미지 파일에서 텍스트 추출** 방법, TIFF 포맷의 특이점 처리 방법, 그리고 **스캔한 이미지 텍스트를 변환**할 때 조정해야 할 부분들을 정확히 알게 됩니다. 숨은 마법은 없습니다—오늘 바로 복사‑붙여넣기하고 실행할 수 있는 직관적인 파이썬 코드만 있죠.

## What You’ll Need

시작하기 전에 아래 항목들을 준비하세요:

- Python 3.9+ 설치 (가능하면 최신 안정 버전)
- pip 로 설치 가능한 OCR 라이브러리. 여기서는 인기 도구인 Tesseract 등을 흉내낸 가상의 `aocr` 패키지를 사용합니다; 나중에 `pytesseract` 혹은 `easyocr` 로 교체할 수 있습니다.
- 처리하고 싶은 TIFF 이미지 – 파일명을 `input.tiff` 로 지정하고, 코드에서 참조할 폴더에 넣어두세요.
- 기본적인 커맨드 라인 사용법에 대한 이해 (패키지 설치 정도)

이 정도면 충분합니다. 무거운 의존성도, Docker 컨테이너도 필요 없으며 몇 줄의 코드만 있으면 됩니다.

## Step 1 – Install and Import Dependencies (how to ocr python)

먼저 OCR 패키지를 설치합니다. 터미널을 열고 다음을 실행하세요:

```bash
pip install aocr
```

실제 라이브러리를 사용하고 싶다면 `aocr` 대신 `pytesseract` 로 바꾸고, Tesseract 엔진을 별도로 설치하면 됩니다.

이제 필요한 모듈을 가져옵니다. `pathlib` 의 `Path` 클래스는 운영체제에 관계없이 파일 경로를 깔끔하게 다룰 수 있게 해줍니다.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*왜 `Path`를 사용할까요?* 슬래시(` / ` vs ` \ `) 차이를 추상화해 주어, OS에 구애받지 않고 디렉터리를 결합할 수 있기 때문입니다. 이 작은 디테일이 나중에 CI 서버로 스크립트를 옮길 때 큰 머리통증을 예방해 줍니다.

## Step 2 – Create the OCR Engine Instance (basic ocr example)

다음으로 OCR 엔진을 초기화합니다. `OcrEngine` 은 이미지를 읽고 문자로 변환해 주는 두뇌 역할을 합니다.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

대부분의 OCR 라이브러리는 여기서 언어, DPI, 신뢰도 임계값 등을 조정할 수 있습니다. 이번 **기본 OCR 예제**에서는 기본값을 그대로 사용하지만, 다국어 문서를 다뤄야 한다면 `ocr_engine.config` 를 살펴보세요.

## Step 3 – Load Your TIFF Image (read tiff file python)

이제 **read tiff file python** 단계입니다. TIFF는 다중 페이지를 가질 수 있지만 `Image.load` 는 기본적으로 첫 페이지만 가져오므로 단일 페이지 스캔에 적합합니다.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

`"YOUR_DIRECTORY"` 를 실제 `input.tiff` 가 들어있는 폴더 경로로 바꾸세요. 스크립트가 어느 위치에서 실행되는지 모를 경우 `Path.cwd()` 로 현재 작업 디렉터리를 출력해 보면 경로 문제를 디버깅하는 데 도움이 됩니다.

## Step 4 – Run the OCR Process (extract text from image)

이제 마법이 시작됩니다. `process()` 를 호출하면 이미지가 OCR 파이프라인을 통과하고 결과 객체가 반환됩니다.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

엔진 내부에서는 이미지를 그레이스케일로 변환하고, 임계값을 적용한 뒤 신경망에 전달하는 작업을 수행합니다. 이러한 단계는 라이브러리가 자동으로 처리하므로 직접 관리할 필요가 없습니다.

## Step 5 – Print the Recognized Text (convert scanned image text)

마지막으로 텍스트를 출력합니다. 실제 프로젝트에서는 파일이나 데이터베이스에 저장하겠지만, 여기서는 예시를 간결하게 유지하기 위해 콘솔에 출력합니다.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

스크립트를 실행하면 다음과 비슷한 결과가 나타납니다:

```
Hello, world!
This is a sample scanned document.
```

출력이 깨져 보인다면 원본 이미지가 선명한지, OCR 언어 설정이 텍스트와 일치하는지 다시 확인하세요.

## Full Working Script

전체 코드를 한 번에 모아 보겠습니다. 바로 실행 가능한 프로그램입니다:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Expected Output

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

**스캔한 이미지 텍스트를** 검색 가능한 PDF 로 변환하고 싶다면 `ocr_result.text` 를 `reportlab` 같은 PDF 생성 라이브러리에 파이프하면 됩니다—하지만 그 내용은 또 다른 튜토리얼이 필요합니다.

## Common Pitfalls & Pro Tips

- **저해상도 스캔**: 150 DPI 이하에서는 OCR 정확도가 급격히 떨어집니다. TIFF가 흐릿하면 Pillow(`Image.open(...).resize(...)`) 로 먼저 업샘플링하세요.
- **다중 페이지**: 멀티 페이지 TIFF의 경우 `Image.load_multi_page()`(라이브러리 지원 시)를 순회하면서 결과를 이어 붙이세요.
- **언어 지원**: 대부분 엔진은 기본이 영어입니다. 예를 들어 스페인어는 `ocr_engine.language = "spa"` 로 설정합니다.
- **공백 처리**: OCR 결과에 불필요한 줄바꿈이 포함될 수 있습니다. `str.splitlines()` 나 정규식을 활용해 정리하세요.
- **성능**: 대량 처리 시 파일당 새 `OcrEngine` 을 만들기보다 하나의 인스턴스를 재사용하는 것이 효율적입니다.

## Extending the Example

이제 **how to ocr python** 을 단일 이미지에 적용하는 방법을 익혔으니, 다음 단계들을 고려해 보세요:

1. **배치 처리** – 디렉터리 내 모든 TIFF를 순회하면서 각각을 `.txt` 파일로 저장합니다.
2. **Pandas와 연동** – 추출된 텍스트와 메타데이터를 함께 저장해 빠른 분석이 가능하도록 합니다.
3. **하이브리드 접근** – OCR 결과를 `spaCy` 같은 NLP 라이브러리와 결합해 청구서에서 이름, 날짜, 금액 등 엔터티를 추출합니다.
4. **다른 파일 포맷** – `Image.load` 대신 `Image.from_bytes` 를 사용해 API 혹은 데이터베이스에서 직접 받아오는 이미지를 처리합니다.

이 모든 확장은 **이미지에서 텍스트 추출**과 **스캔한 이미지 텍스트를** 기계가 이해할 수 있는 형태로 변환한다는 핵심 아이디어 위에 세워집니다.

## Conclusion

우리는 **how to ocr python**, **read tiff file python**, **extract text from image** 파일을 몇 줄의 코드만으로 구현하는 **기본 OCR 예제**를 끝까지 살펴보았습니다. 스크립트는 독립형이며 오류 처리를 포함하고 결과를 바로 출력하므로, 스캔 문서를 편집 가능한 텍스트로 변환해야 하는 모든 프로젝트의 견고한 출발점이 됩니다.

OCR 백엔드를 교체하거나 전처리를 조정하거나, 결과를 후속 워크플로에 연결하는 등 자유롭게 실험해 보세요. 신뢰할 수 있게 **스캔한 이미지 텍스트를** 검색 가능하고 활용 가능한 데이터로 변환할 수 있다면 가능성은 무한합니다.

궁금한 점—예외 상황, 언어 팩, 성능 튜닝 등—이 있다면 아래 댓글에 남겨 주세요. 즐거운 코딩 되세요! 

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
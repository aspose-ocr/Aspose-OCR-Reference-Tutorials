---
category: general
date: 2026-03-26
description: Python에서 OCR을 수행하는 방법을 배우고, 간단한 OcrEngine을 사용하여 이미지에서 텍스트를 쉽게 추출하고, 스캔에서
  텍스트를 읽으며, 청구서에서 텍스트를 추출하세요.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: ko
og_description: Python에서 OCR을 수행하는 방법은? 이 가이드는 이미지에서 텍스트를 추출하고, 스캔에서 텍스트를 읽으며, 청구서에서
  텍스트를 몇 분 안에 추출하는 방법을 보여줍니다.
og_title: Python에서 OCR 수행 방법 – 텍스트 빠르게 추출하기
tags:
- OCR
- Python
- Image Processing
title: Python에서 OCR 수행 방법 – 텍스트를 빠르게 추출하기
url: /ko/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 파이썬에서 OCR 수행하기 – 텍스트 빠르게 추출하기

스캔한 영수증이나 흐릿한 PDF에서 **OCR을 어떻게 수행하는지** 궁금하셨나요? 혼자가 아닙니다. 많은 프로젝트에서 **이미지에서 텍스트 추출**이 필요하게 되며, “모두 손으로 입력한다”는 방식은 절대 확장성이 없습니다.  

이 튜토리얼에서는 **OCR을 사용해 스캔에서 텍스트를 읽고**, 청구서에서 데이터를 추출하며, 자동 기울기 보정까지 몇 줄의 파이썬 코드만으로 구현하는 완전한 실행 예제를 보여드립니다.

## 배울 내용

다음 항목들을 차근차근 살펴봅니다:

* 정확한 의존성 및 import 구문
* `OcrEngine` 인스턴스 생성 및 설정 방법
* 동일 엔진을 사용해 **이미지에서 텍스트 추출**, **스캔에서 텍스트 읽기**, **청구서에서 텍스트 추출**하는 방법
* 흔히 겪는 함정(잘못된 언어 설정, 파일 누락, 대용량 이미지)과 회피 방법
* OCR 성공 여부를 확인할 수 있는 기대 출력 예시

외부 문서 링크는 필요 없습니다—코드를 복사‑붙여넣기만 하면 바로 결과를 확인할 수 있습니다.

## 사전 준비

시작하기 전에 다음을 준비하세요:

* Python 3.8+ 설치 ( `ocr` 패키지는 최신 버전과 호환됩니다)
* `ocr` 라이브러리 설치 (`pip install ocr‑engine` – 실제 패키지 이름이 다르면 교체)
* 처리할 이미지 파일 – 데모에서는 `YOUR_DIRECTORY` 폴더에 있는 `invoice.png` 를 사용합니다

준비가 되었다면 바로 시작할 수 있습니다.

## Step 1: OCR 모듈 설치 및 Import

먼저 OCR 라이브러리를 설치해야 합니다. 아직 설치하지 않았다면 터미널에서 다음 명령을 실행하세요:

```bash
pip install ocr-engine
```

이제 스크립트에서 모듈을 import 합니다.

```python
# Step 1: Import the OCR module
import ocr
```

> **팁:** 가상 환경을 깔끔하게 유지하면 나중에 다른 이미지‑처리 패키지를 추가할 때 버전 충돌을 방지할 수 있습니다.

## Step 2: OCR 엔진 생성 및 설정

엔진을 생성하는 것은 생성자를 호출하는 것만큼 간단하지만, 핵심은 올바르게 설정하는 것입니다. 여기서는 언어를 영어로 지정하고 자동 기울기 보정을 켭니다. 이는 스캔된 청구서가 완벽히 정렬되지 않았을 때 필수적입니다.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

왜 `auto_skew`를 켜야 할까요? 많은 스캐너가 이미지를 몇 도 정도 기울인 상태로 저장합니다. 보정이 없으면 엔진이 문자를 놓쳐서 완전한 청구서가 의미 없는 문자열로 변할 수 있습니다.

## Step 3: 대상 이미지에 OCR 수행

이제 이미지 파일을 엔진에 전달합니다. `recognize_image` 메서드는 원시 텍스트와 (라이브러리가 제공한다면) 신뢰도 점수를 포함한 객체를 반환합니다.

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

**스캔에서 텍스트 읽기** 상황이라면, 경로를 PNG 또는 JPEG 로 변환한 스캔 PDF 파일로 바꾸면 됩니다. 기본 호출은 지원하는 모든 이미지 포맷에서 동작합니다.

## Step 4: 추출된 텍스트 확인 및 활용

우선 원시 OCR 출력을 출력해 봅시다. 실제 청구서 처리 파이프라인에서는 이 문자열을 파싱해 항목, 총액, 날짜 등을 추출하지만, 여기서는 OCR이 정상 작동했는지 빠르게 확인하는 정도만 합니다.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**예상 출력 (간략히 표시):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

출력이 깨져 보인다면 이미지가 선명한지, `engine.language`가 문서 언어와 일치하는지 다시 확인하세요.

## Step 5: 흔히 마주치는 Edge Case 처리

### 대용량 이미지

5000 × 5000 픽셀 스캔은 메모리를 많이 소모합니다. 엔진에 전달하기 전에 이미지를 다운스케일하는 간단한 방법은 다음과 같습니다:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### 다중 언어

이미지에 영어와 스페인어가 섞여 있다면, 언어 리스트를 지정할 수 있습니다:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

엔진은 두 언어 집합의 문자를 모두 인식하려 시도합니다.

### 오류 처리

파일 존재 여부를 가정하지 마세요. try‑except 블록으로 감싸 친절한 메시지를 제공하세요:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Visual Reference

아래는 데모에 사용한 샘플 청구서 스크린샷입니다. 약간 기울어져 있는 부분이 `auto_skew`가 바로 잡아주는 부분이죠.

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* 자동 기울기 보정이 적용된 청구서 이미지에서 OCR 수행 예시.

## Full, Runnable Example

모든 내용을 하나로 합친 스크립트입니다. 명령줄에서 실행할 수 있으며, 설치, 설정, 오류 처리 및 추출된 텍스트를 `output.txt` 파일에 저장하는 간단한 후처리 단계까지 포함합니다.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

`python full_ocr_demo.py` 를 실행하면 콘솔에 추출된 텍스트가 출력되고 `output.txt` 에 저장됩니다. 이후 정규식, CSV 작성기 등 원하는 로직을 적용해 **청구서에서 텍스트 추출** 자동화를 진행할 수 있습니다.

## Conclusion

이제 파이썬에서 **OCR을 수행하는 방법**에 대한 완전한 엔드‑투‑엔드 솔루션을 갖추었습니다. `OcrEngine`을 생성하고, 언어와 기울기 보정을 설정하며, 실용적인 Edge Case를 처리함으로써 **이미지에서 텍스트 추출**, **스캔에서 텍스트 읽기**, **청구서에서 텍스트 추출**을 문서화된 자료를 뒤적이지 않아도 신뢰성 있게 구현할 수 있습니다.

다음 단계는? 파일을 배치로 처리하도록 루프에 넣어 보거나, 다른 언어를 실험하거나, 추출 결과를 PDF 생성 라이브러리에 연결해 검색 가능한 PDF를 만들 수 있습니다. 가능성은 무한하며, 방금 본 코드는 견고한 출발점이 될 것입니다.

특정 파일 포맷에 대한 질문이 있거나 신뢰도 임계값 조정이 필요하면 아래 댓글로 알려 주세요—OCR 파이프라인을 미세 조정하는 데 기꺼이 도와드리겠습니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
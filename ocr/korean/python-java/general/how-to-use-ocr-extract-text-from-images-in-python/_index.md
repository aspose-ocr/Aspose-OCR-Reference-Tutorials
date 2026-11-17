---
category: general
date: 2026-03-18
description: OCR을 사용하여 이미지에서 텍스트를 추출하는 방법 – PNG 파일에서 텍스트를 인식하고 OCR을 위해 이미지를 로드하는 빠른
  가이드.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: ko
og_description: OCR를 사용해 이미지에서 텍스트를 추출하는 방법 – PNG에서 텍스트를 인식하고, OCR용 이미지를 로드하며, 간단한
  파이썬 스크립트로 텍스트를 추출하는 방법을 배워보세요.
og_title: 'OCR 사용 방법: 파이썬으로 이미지에서 텍스트 추출'
tags:
- OCR
- Python
- Image Processing
title: 'OCR 사용 방법: 파이썬으로 이미지에서 텍스트 추출'
url: /ko/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 사용 방법: Python에서 이미지에서 텍스트 추출하기

지저분한 스크린샷이나 스캔한 영수증을 보면서 **OCR을 어떻게 사용하는지** 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다—개발자들은 특히 모바일 앱이나 웹 업로드에서 오는 PNG와 같은 이미지에서 읽을 수 있는 텍스트를 추출해야 합니다. 이 튜토리얼에서는 **이미지에서 텍스트 추출** 방법, **PNG에서 텍스트 인식** 방법, 그리고 **OCR을 위한 이미지 로드** 방법을 몇 줄의 Python 코드만으로 보여주는 완전하고 실행 가능한 예제를 단계별로 안내합니다.

올바른 라이브러리 설치부터 다국어 문서 처리까지 모든 과정을 다룰 것이므로, 끝까지 읽으면 어떤 이미지든 엔진에 넣어 **텍스트를 추출하는 방법**을 정확히 알게 됩니다. 애매한 언급 없이 복사‑붙여넣기만 하면 바로 실행할 수 있는 명확한 단계별 솔루션을 제공합니다.

## 배울 내용

1. 가벼운 OCR 엔진을 설정합니다(무거운 종속성 필요 없음).  
2. 이미지 파일—특히 PNG—을 엔진에 로드합니다.  
3. 자동 언어 감지를 활성화하여 엔진이 다국어 콘텐츠를 처리하도록 합니다.  
4. 인식 프로세스를 실행하고 평문 결과를 가져옵니다.  
5. 파일 누락이나 지원되지 않는 형식과 같은 엣지 케이스에 맞게 워크플로를 조정합니다.

기본적인 Python에 익숙하다면 바로 시작할 수 있습니다. 사전 OCR 경험은 필요 없지만, 라이브러리 문서를 한 번 살펴보는 것은 도움이 됩니다.

---

![How to use OCR on a PNG image](placeholder.png "How to use OCR on a PNG image – step-by-step guide")

## OCR 사용 방법 – 이미지 로드 및 텍스트 인식 {#how-to-use-ocr}

### 단계 1: OCR 라이브러리 설치

우선, `OcrEngine` 클래스를 제공하는 Python 패키지가 필요합니다. 이 튜토리얼에서는 가상의 예시이지만 실용적인 **SimpleOCR** 패키지를 사용할 것이며, pip을 통해 설치할 수 있습니다:

```bash
pip install simple-ocr
```

> **팁:** 가상 환경에서 작업하고 있다면(강력히 권장) 설치 명령을 실행하기 전에 환경을 활성화하세요. 이렇게 하면 프로젝트 의존성을 깔끔하게 유지할 수 있습니다.

### 단계 2: 엔진을 임포트하고 인스턴스 생성

엔진을 생성하는 것은 생성자를 호출하는 것만큼 간단합니다. 엔진을 나중에 이미지 처리를 담당할 “두뇌”라고 생각하면 됩니다.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

왜 매번 새로운 인스턴스를 만들까요? 격리 때문입니다. 새 엔진은 이전 실행에서 남은 상태가 현재 인식에 영향을 주지 않도록 보장하며, 배치로 많은 파일을 처리할 때 매우 중요합니다.

### 단계 3: 처리할 이미지 로드

이제 실제로 **OCR을 위한 이미지 로드**를 수행합니다. `setImageFromFile` 메서드는 모든 래스터 이미지 경로를 받아들이며, 여기서는 `mixed_doc.png`라는 PNG 파일을 지정합니다.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

파일을 찾을 수 없으면 `SimpleOCR`는 명확한 `FileNotFoundError`를 발생시킵니다. 이를 잡아 친절한 오류 메시지를 제공할 수 있습니다:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### 단계 4: 자동 언어 감지 활성화

대부분의 최신 OCR 엔진은 언어 팩을 포함합니다. `"multilingual"`을 전달하면 엔진이 텍스트를 분석해 자동으로 적절한 언어 모델을 선택합니다. 예를 들어 PNG에 영어와 스페인어가 혼합되어 있을 때 매우 유용합니다.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

언어를 미리 알고 있다면 `"multilingual"` 대신 `"eng"`나 `"spa"`와 같은 특정 로케일을 지정해 처리 속도를 높일 수 있습니다.

### 단계 5: 인식 프로세스 실행

여기서 핵심 작업이 수행됩니다. `recognize()`는 이미지를 스캔하고, 세그멘테이션을 적용하며, 신경망을 실행하고, 내부적으로 텍스트 버퍼를 구축합니다.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

엔진은 내부적으로 다음을 수행합니다:

- **전처리**(기울기 보정, 이진화)  
- **레이아웃 분석**(열, 표 감지)  
- **문자 분류**(딥러닝 모델 사용)  

이 모든 과정이 추상화되어 있기 때문에 한 줄만 사용하면 됩니다.

### 단계 6: 인식된 텍스트 가져오기 및 출력

마지막으로 결과 객체를 가져와 평문 문자열을 추출합니다. 바로 여기서 **이미지에서 텍스트를 추출**하게 됩니다.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**예상 출력** (간략히 표시):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

이미지에 인식 가능한 문자가 없으면 `text`는 빈 문자열이 됩니다. 이를 방지하려면 다음과 같이 할 수 있습니다:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## 이미지에서 텍스트 추출 – 일반적인 엣지 케이스 처리

### 하나의 파일에 여러 언어가 포함된 경우

문서에 여러 언어가 섞여 있을 때 `"multilingual"` 설정이 보통 올바르게 동작합니다. 하지만 인식 오류가 발생하면 수동으로 대체 목록을 지정할 수 있습니다:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### PNG가 아닌 형식

우리의 초점은 **PNG에서 텍스트 인식**이지만, `SimpleOCR`는 JPEG, BMP, TIFF도 지원합니다. `setImageFromFile`에서 파일 확장자를 바꾸면 됩니다. TIFF 스택의 경우 특정 페이지를 선택해야 할 수도 있습니다:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### 대용량 파일 및 메모리 사용량

기가픽셀 스캔을 처리한다면 OCR 전에 이미지 크기를 조정하는 것을 고려하세요:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

크기 조정은 메모리 부담을 줄이면서도 정확한 인식을 위한 충분한 디테일을 유지합니다.

### 로드 실패 디버깅

때때로 이미지는 눈으로 보기엔 정상인데 내부적으로 손상될 수 있습니다. 엔진이 보는 내용을 확인하려면 자세한 로그를 활성화하세요:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## 완전한 실행 가능한 스크립트

아래는 모든 요소를 결합한 전체 프로그램입니다. `ocr_demo.py`라는 파일에 복사하고, `YOUR_DIRECTORY` 플레이스홀더를 수정한 뒤 `python ocr_demo.py`를 실행하세요.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

이 스크립트를 실행하면 `mixed_doc.png` 안에 있는 내용의 평문 버전이 출력됩니다. 파일을 다른 이미지로 교체해도 **텍스트 추출 방법**은 동일하게 작동합니다.

---

## 결론

우리는 방금 Python에서 **OCR 사용 방법**을 통해 **이미지 파일에서 텍스트를 추출**하는 과정을 살펴보았습니다. 특히 **PNG에서 텍스트 인식**과 **OCR을 위한 이미지 로드** 실용적인 단계에 초점을 맞췄습니다. 위 스니펫은 패키지 설치, 파일 전달, 다국어 감지 활성화, 엔진 실행, 결과 추출까지 모두 포함된 독립적인 솔루션입니다.

앞으로 할 수 있는 일:

- 사용자 업로드를 받는 웹 서비스에 스크립트를 통합하기.  
- PNG로 변환된 PDF 폴더를 일괄 처리하기.  
- 정확도 향상을 위해 후처리(예: 정규식 정리, 맞춤법 검사) 추가하기.

OCR 품질은 이미지 선명도, 적절한 언어 팩, 그리고 때때로 약간의 전처리에 좌우된다는 점을 기억하고, 다양한 실험을 해보세요.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
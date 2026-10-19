---
category: general
date: 2026-03-26
description: Python에서 OCR을 수행하고 이미지 파일의 텍스트를 인식하는 방법을 배워보세요. 이 가이드는 PNG에서 텍스트를 추출하고
  이미지를 빠르게 텍스트로 변환하는 방법을 보여줍니다.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: ko
og_description: Python에서 OCR을 수행하는 방법은? 이 가이드를 따라 이미지에서 텍스트를 인식하고, PNG에서 텍스트를 추출하며,
  이미지를 텍스트로 변환하는 방법을 체험 라이선스로 확인하세요.
og_title: Python에서 OCR 수행 방법 – 완전 튜토리얼
tags:
- OCR
- Python
- Image Processing
title: Python으로 OCR 수행하기 – 완전한 단계별 튜토리얼
url: /ko/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 OCR 수행 방법 – 완전 단계별 튜토리얼  

휴대폰으로 찍은 사진에서 **OCR을 수행하는 방법**이 궁금하셨나요? 여러분만 그런 것이 아닙니다—개발자들은 복잡한 네이티브 라이브러리를 다루지 않고도 이미지 파일에서 텍스트를 인식할 수 있는 신뢰할 수 있는 방법을 필요로 합니다.  

이 튜토리얼에서는 **OCR 수행 방법**, **이미지에서 텍스트 인식**, **PNG에서 텍스트 추출**을 가벼운 Python 래퍼를 사용해 직접 보여줍니다. 마지막까지 따라오시면 몇 줄의 코드만으로 **이미지를 텍스트로 변환**할 수 있게 되며, 내장된 체험판 모드를 사용하기 때문에 라이선스 문제도 걱정하지 않으셔도 됩니다.

## 배울 내용  

* OCR 엔진에 대한 체험판 라이선스 설정 방법 (파일 경로 필요 없음).  
* **이미지에서 텍스트 인식** 객체에 대한 정확한 호출 순서.  
* **PNG 파일에서 텍스트 추출** 방법 및 폰트 누락과 같은 일반적인 함정 처리법.  
* 체험판에서 정식 라이선스로 전환할 때 솔루션을 확장하는 팁.  

**전제 조건** – Python 3.8+와 `ocr` 패키지(`pip install ocr`로 설치 가능)만 있으면 됩니다. 다른 외부 도구는 필요하지 않습니다.

---  

![how to perform OCR example](https://example.com/ocr-demo.png "Python에서 OCR 수행 – 인식된 텍스트 표시")  

*이미지 대체 텍스트: Python에서 OCR 수행 – 샘플 출력*  

## 1단계 – 체험판 라이선스 활성화 (파일 경로 필요 없음)  

엔진이 무엇이든 읽기 전에 유효한 라이선스가 필요합니다. 체험판 모드는 실험 및 소규모 프로젝트에 안성맞춤입니다.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*왜 중요한가:* 라이선스 객체는 OCR 라이브러리에 샌드박스 모드에서 동작하고 있음을 알려줍니다. 이 단계를 건너뛰면 `recognize()` 호출 순간 `LicenseError`가 발생합니다.  

**팁:** 정식 라이선스로 전환할 때는 위 두 줄을 `ocr.License("path/to/your/license.key").apply()` 로 교체하면 됩니다.

## 2단계 – OCR 엔진 인스턴스 생성  

체험판이 활성화되었으니 이제 메인 엔진을 인스턴스화합니다. 이는 이미지를 보고 문자 위치를 판단하는 “두뇌”와 같습니다.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*왜 중요한가:* `OcrEngine`은 언어 팩, DPI 설정 등 구성을 보관합니다. 나중에 조정할 수 있지만 기본값은 대부분의 영어 전용 PNG에 잘 작동합니다.

## 3단계 – 처리할 PNG 로드  

여기서 **이미지에서 텍스트 인식**을 수행합니다. `ocr.Imaging.Image.load()` 메서드는 PNG, JPEG, BMP 등 여러 포맷을 지원합니다.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*예외 상황:* PNG가 인덱스 팔레트를 사용하고 있다면(스크린샷에서 흔함) 로더가 자동으로 24‑bit RGB 버퍼로 변환합니다. 이 변환은 약간의 성능 저하를 일으킬 수 있지만 정확한 OCR 결과를 보장합니다.

## 4단계 – OCR 실행 및 텍스트 추출  

마지막으로 엔진에 작업을 시키고 평문 결과를 받아옵니다.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**예상 출력** (예: “Hello World”가 들어 있는 간단한 이미지):

```
Hello World
```

이미지에 여러 줄이 있으면 출력에 줄 바꿈이 그대로 유지되어 CSV 파서나 NLP 파이프라인 등 후속 처리에 편리합니다.

## 선택 사항: 정확도 향상을 위한 미세 조정  

* **언어 팩:** `ocr_engine.set_language("eng")`(기본) 또는 프랑스어는 `"fra"`  
* **DPI 스케일링:** `ocr_engine.set_dpi(300)`은 저해상도 스캔에서 결과를 개선할 수 있습니다.  
* **전처리:** `ocr.Imaging.Image.threshold()` 로 이진 임계값을 적용한 뒤 `set_image` 하면 잡음이 많은 배경에서도 더 깨끗한 텍스트를 얻을 수 있습니다.

이러한 조정은 빠른 데모에서 **ocr tutorial python** 수준의 프로덕션 급 처리로 전환할 때 유용합니다.

## 전체 스크립트 – 복사·붙여넣기 바로 사용 가능  

아래는 위 단계들을 모두 합친 실행 가능한 전체 스크립트입니다. `run_ocr.py` 로 저장하고 `YOUR_DIRECTORY/sample1.png` 를 실제 PNG 경로로 바꾸세요.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

명령줄에서 실행:

```bash
python run_ocr.py
```

콘솔에 추출된 텍스트가 출력될 것입니다. 빈 문자열이 나오면 이미지에 명확하고 고대비 텍스트가 있는지, 체험판 라이선스가 오류 없이 적용됐는지 다시 확인하세요.

## 흔히 묻는 질문 및 함정  

* **“JPEG도 동작하나요?”** – 물론입니다. `load()` 메서드가 포맷을 자동 감지하므로 코드 수정 없이 PNG를 JPEG로 바꿔도 됩니다.  
* **“이미지가 회전돼 있으면?”** – 엔진이 자동으로 방향을 감지하지만, 최상의 결과를 위해 `set_image` 전에 `input_image.rotate(90)` 로 미리 회전시킬 수 있습니다.  
* **“여러 이미지를 루프에서 처리할 수 있나요?”** – 가능합니다. 로딩과 `recognize()` 호출을 `for` 루프 안으로 옮기면 동일한 `ocr_engine` 인스턴스를 재사용할 수 있어 약간의 오버헤드 절감 효과가 있습니다.  

## 다음 단계 – 데모에서 프로덕션으로  

이제 **OCR 수행 방법**을 알았으니 다음 주제들을 살펴보세요:

* **배치 처리** – `os.listdir()` 와 결합해 **PNG 파일에서 텍스트 추출**을 대량으로 수행합니다.  
* **PDF와 통합** – `pdf2image` 로 PDF 페이지를 PNG로 변환한 뒤 동일 파이프라인에 투입합니다.  
* **후처리** – 정규식이나 퍼지 매칭을 적용해 흔히 발생하는 OCR 오인식(예: “0” vs “O”)을 정리합니다.  

이 모든 내용은 **이미지를 텍스트로 변환**한다는 핵심 아이디어를 기반으로 하며, OCR 워크플로의 활용도를 크게 확장합니다.

---  

### TL;DR  

Python에서 **OCR 수행 방법**에 필요한 모든 것을 다루었습니다: 체험판 라이선스 활성화, 엔진 생성, PNG 로드, 인식 실행, 결과 출력. 몇 줄의 코드만으로 **이미지에서 텍스트 인식**, **PNG에서 텍스트 추출**, **이미지를 텍스트로 변환**할 수 있습니다. DPI나 언어 설정을 조정해 보면서 엔진이 무거운 작업을 대신하도록 하세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
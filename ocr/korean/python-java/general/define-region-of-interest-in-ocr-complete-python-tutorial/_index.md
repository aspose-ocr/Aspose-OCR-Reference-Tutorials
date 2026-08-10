---
category: general
date: 2026-06-16
description: OCR에서 ID 카드의 스페인어 텍스트를 추출하기 위해 관심 영역을 정의합니다. OCR을 위한 이미지를 로드하고 ROI를 효율적으로
  지정하는 방법을 배워보세요.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: ko
og_description: OCR에서 관심 영역을 정의하여 신분증에서 스페인어 텍스트를 추출합니다. 이미지 로드 및 ROI 지정에 대한 단계별 가이드.
og_title: OCR에서 관심 영역 정의 – 완전 파이썬 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: OCR에서 관심 영역 정의 – 완전 파이썬 튜토리얼
url: /ko/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR에서 관심 영역 정의 – 완전한 Python 튜토리얼

이미지에서 실제로 필요한 부분만 읽으려면 **OCR에서 관심 영역을 정의**하는 방법이 궁금하셨나요? 이 튜토리얼에서는 바로 그 방법을 단계별로 안내하고, **OCR용 이미지 로드**와 ID 카드에서 스페인어 텍스트를 몇 줄의 Python 코드만으로 추출하는 방법을 보여드립니다.  

시끄러운 스캔 이미지 앞에서 “이름 필드를 더 깔끔하게 잡아낼 방법이 없을까?”라고 고민한 적이 있다면, 여기서 원하는 답을 찾을 수 있습니다. 끝까지 읽으면 배경 잡음에 방해받지 않고 필요한 ID 카드 텍스트만 추출할 수 있게 됩니다.

## 배울 내용

- OCR을 실행하기 전에 **관심 영역을 정의**해야 하는 이유.  
- 인기 있는 Python OCR 래퍼를 사용해 **OCR용 이미지 로드**하는 정확한 단계.  
- 픽셀 좌표로 **ROI 지정 방법**.  
- 소스 언어가 스페인어일 때도 **ID 카드 텍스트 추출**을 안정적으로 수행하는 방법.  
- 회전된 카드나 저대비 스캔과 같은 엣지 케이스를 처리하는 팁.  

사전 OCR 지식은 필요 없습니다—Python 3 환경과 테스트용 JPEG ID 카드만 있으면 됩니다.

---

![Define region of interest illustration](placeholder.png){alt="관심 영역 예시: ID 카드 이미지에 강조된 사각형을 보여줍니다"}

## 단계 1: OCR 라이브러리 설치 및 임포트

먼저, 앞서 본 `OcrEngine` 클래스를 제공하는 라이브러리가 필요합니다. 이 가이드에서는 가상의 `ocr` 패키지를 사용하지만, `pytesseract`, `easyocr` 혹은 언어와 ROI를 설정할 수 있는 어떤 래퍼에도 동일한 개념이 적용됩니다.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tip:* `pytesseract`를 사용할 경우 `Rectangle` 클래스는 간단한 튜플 `(left, top, width, height)` 형태가 됩니다. 나머지 흐름은 동일합니다.

## 단계 2: OCR용 이미지 로드

이제 **OCR용 이미지 로드**를 수행합니다. 엔진은 `ocr.Image` 객체를 기대하므로, ID 카드가 저장된 파일을 가리키도록 합니다. 경로는 절대 경로나 스크립트 작업 디렉터리 기준 상대 경로여야 합니다.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

이미지가 너무 크면 먼저 리사이즈하는 것을 고려하세요; OCR 엔진은 가로 1500 px 이하 이미지에서 더 빠르게 동작합니다.

## 단계 3: ROI 지정 방법 (관심 영역 정의)

튜토리얼의 핵심: **ROI 지정 방법**입니다. 관심 영역은 OCR 엔진에게 “이 픽셀 범위 안만 살펴라”고 알려주는 사각형일 뿐입니다. ID 카드의 이름 필드 주변에 박스를 그리는 것과 동일합니다.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

왜 이런 숫자인가요? 샘플 이미지에서 이름은 왼쪽 가장자리에서 대략 120 px, 위쪽 가장자리에서 80 px 정도 떨어져 있습니다. 처리하려는 카드 레이아웃에 맞게 값을 조정하세요.  

*엣지 케이스:* 카드가 90° 회전된 경우 `width`와 `height`를 교환하고 `left`/`top`을 적절히 조정하거나, Pillow로 이미지를 미리 회전시킨 후 엔진에 전달합니다.

## 단계 4: ROI 내에서 OCR 수행

ROI가 정의되면 엔진은 사각형 밖의 모든 영역을 무시합니다. 이는 처리 속도를 높일 뿐 아니라 배경 그래픽으로 인한 오탐을 줄여줍니다.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

`recognize()` 호출은 인식된 텍스트, 신뢰도 점수, 각 단어의 경계 상자를 포함하는 객체를 반환합니다.

## 단계 5: ID 카드 텍스트 추출 (스페인어 출력 확인)

마지막으로 **ID 카드 텍스트 추출**을 수행하고 결과를 출력합니다. 앞서 언어를 스페인어로 설정했기 때문에 OCR 엔진은 “ñ”, “á”와 같은 억양 문자를 포함한 스페인어 사전을 적용해 정확도를 높입니다.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### 예상 출력

```
ROI text: JUAN PÉREZ GARCÍA
```

문자가 깨져 보이면 이미지가 실제로 스페인어인지, OCR 라이브러리의 언어 데이터 파일이 올바르게 설치되었는지 다시 확인하세요.

## 흔히 발생하는 문제와 해결 방법

| 증상 | 가능한 원인 | 해결 방법 |
|------|------------|----------|
| 빈 문자열 반환 | ROI가 텍스트와 교차하지 않음 | 이미지 뷰어로 좌표 확인; `engine.debug_draw_roi()` 사용 가능 여부 확인 |
| 잡음 문자 다수 | 잘못된 언어 팩 | 스페인어 언어 데이터를 재설치하거나 `ocr.Language.AUTO`로 전환 |
| 낮은 신뢰도 점수 | 이미지가 흐리거나 저대비 | OpenCV 전처리 – `cv2.GaussianBlur`와 `cv2.threshold` 적용 |
| ROI 지정에도 전체 이미지에 OCR 실행 | 오래된 라이브러리 버전 사용 | 최신 `ocr` 패키지로 업그레이드; 구버전은 ROI를 무시함 |

## 예제 확장: 다중 ROI

때때로 하나 이상의 필드(예: 이름과 ID 번호)를 추출해야 할 때가 있습니다. 패턴은 동일합니다: `engine.region_of_interest`를 변경하고 `recognize()`를 다시 호출합니다.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

라이브러리가 지원한다면 사각형 리스트를 한 번에 배치 처리할 수도 있어 OCR 엔진 호출 횟수를 줄일 수 있습니다.

## 전체 작동 스크립트

모든 내용을 종합한 **관심 영역 정의**, **OCR용 이미지 로드**, **스페인어 텍스트 추출**이 가능한 실행 가능한 스크립트는 다음과 같습니다.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

스크립트를 실행하면 콘솔에 이름이 출력됩니다. 다른 필드를 목표로 하려면 사각형 값을 바꾸면 되며, 이를 통해 어떤 ID‑카드 유형 문서에도 재사용 가능한 유틸리티를 만들 수 있습니다.

## 다음 단계

- **배치 처리:** ID 카드 폴더를 순회하며 각 추출된 이름을 CSV 파일에 저장.  
- **언어 자동 감지:** 사용자가 동적으로 언어를 선택하도록 구현; `ocr.Language.AUTO`가 유용합니다.  
- **후처리:** 정규식 패턴을 적용해 일반적인 OCR 오류(예: 이름에 나타나는 “0”을 “O”로 교체) 정리.  

**관심 영역 정의**를 마스터함으로써 스페인어 문서에서도 **ID 카드 텍스트 추출**을 빠르고 정확하게 수행할 수 있는 강력한 방법을 손에 넣었습니다.

---

### TL;DR

우리는 **OCR에서 관심 영역 정의**, **OCR용 이미지 로드**, **ROI 지정**을 통해 ID 카드에서 **스페인어 텍스트**를 추출하는 방법을 보여주었습니다. 전체 예제는 1분 이내에 실행되며 좌표만 약간 조정하면 어떤 레이아웃에도 적용할 수 있습니다. 직접 시도해 보고 사각형을 조정해 보세요. OCR이 레이저처럼 정확히 초점을 맞출 것입니다.

Happy coding!

## 다음에 배워야 할 내용은?


다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 관련 주제를 깊이 있게 다룹니다. 각 리소스는 단계별 설명과 완전한 코드 예제를 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
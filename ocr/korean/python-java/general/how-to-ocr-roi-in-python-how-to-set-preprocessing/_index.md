---
category: general
date: 2026-03-28
description: Python에서 ROI OCR하기 – 특정 이미지 영역에서 정확한 텍스트 추출을 위한 전처리 옵션 설정 방법을 배우세요.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: ko
og_description: Python에서 ROI OCR하기 – 이 가이드는 정의된 이미지 영역에서 신뢰할 수 있는 텍스트 추출을 위해 전처리를
  설정하는 방법을 보여줍니다.
og_title: Python에서 ROI를 OCR하는 방법 – 전처리 설정 방법
tags:
- OCR
- Python
- Aspose
title: Python에서 ROI OCR하는 방법 – 전처리 설정 방법
url: /ko/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 ROI OCR하기 – 전처리 설정 방법

노이즈가 많은 청구서 이미지에서 전체 페이지를 메모리로 로드하지 않고 **ROI를 OCR하는 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 실제 프로젝트에서는 고객 이름, 주소, 합계와 같은 몇 개의 필드만 필요하기 때문에 전체 문서를 스캔하는 것은 과도합니다.  

좋은 소식은? Aspose OCR을 사용하면 엔진에 정확히 **어디를 볼지** 알려줄 수 있고, 이미지 정리도 먼저 시킬 수 있습니다. 이 튜토리얼에서는 **전처리 설정 방법** 옵션을 살펴보고, 관심 영역(ROIs)을 정의하며, Python 몇 줄만으로 깨끗한 텍스트를 추출하는 과정을 안내합니다.

이 가이드를 끝까지 읽으면 청구서, 영수증 또는 양식에서 특정 블록을 추출하는 바로 실행 가능한 스크립트를 얻게 됩니다. 별도의 도구는 필요 없으며, Aspose OCR과 약간의 Python 로직만 있으면 됩니다.

---

## 필요 사항

- **Python 3.8+** (코드는 최신 버전에서도 작동합니다)  
- **Aspose OCR for Python via .NET** – `pip install aspose-ocr` 로 설치  
- `invoice.png` 와 같은 샘플 이미지(참조 가능한 폴더에 배치)  
- Python 함수와 객체‑지향 구문에 대한 기본적인 이해  

이미 준비되어 있다면, 좋습니다—바로 코드로 넘어가겠습니다.

---

![How to OCR ROI diagram](ocr-roi.png "How to OCR ROI example")

*Alt text: 청구서 이미지에 ROI 상자를 표시한 OCR ROI 다이어그램*

---

## 단계 1 – OCR 엔진 초기화 (How to OCR ROI)

엔진에 *어디를 볼지* 알려주기 전에 OCR 프로세서 인스턴스가 필요합니다. 이 객체는 모든 설정을 보관하고 인식 작업을 수행합니다.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Why this matters*: `OcrEngine` 클래스는 무거운 작업(폰트 감지, 레이아웃 분석 등)을 추상화합니다. 하나의 엔진을 생성하면 이미지마다 무거운 리소스를 재초기화하지 않아 성능이 빠르게 유지됩니다.

---

## 단계 2 – 원본 이미지 로드 (How to OCR ROI)

Aspose Storage를 사용하면 이미지 로드가 간편합니다. 파일 경로를 지정하면 처리 준비가 된 `Image` 객체를 얻을 수 있습니다.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Tip*: 스트림(예: 웹 API를 통해 업로드된 이미지)으로 작업하는 경우 파일 경로 대신 `BytesIO` 객체를 `Image.load`에 전달할 수 있습니다.

---

## 단계 3 – 관심 영역(ROIs) 정의

이제 핵심 질문 **ROI를 OCR하는 방법**에 답합니다: 엔진에 우리가 관심 있는 데이터가 들어 있는 정확한 사각형을 알려줍니다. 각 ROI는 좌상단 좌표(`x`, `y`)와 크기(`width`, `height`)로 정의됩니다.

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*왜 ROIs를 사용하나요?*  
- **속도** – 엔진이 이미지의 관련 없는 부분을 건너뜁니다.  
- **정확도** – 작은 영역에 집중함으로써 다른 곳의 노이즈가 인식기를 혼란스럽게 하지 못합니다.  
- **유연성** – 필요에 따라 원하는 만큼 ROIs를 추가할 수 있으며, 엔진은 동일한 순서로 결과 리스트를 반환합니다.

---

## 단계 4 – 더 나은 OCR 정확도를 위한 전처리 설정 방법

스캐너나 휴대폰에서 바로 얻은 이미지는 종종 기울어짐, 낮은 대비, 고르지 않은 조명 등의 문제를 겪습니다. Aspose OCR은 인식이 실행되기 전에 일반적인 보정을 활성화할 수 있는 `PreprocessingOptions` 객체를 제공합니다.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*이것이 도움이 되는 이유*:  
- **Deskew**: 기울어짐을 제거하여 문자 형태가 모호해지는 것을 방지합니다.  
- **Binarize**: 색상 노이즈를 감소시켜 OCR 엔진에 깨끗한 이진 이미지를 제공합니다.  
- **Contrast**: 옅은 획을 강화하여 특히 색이 바랜 영수증에 유용합니다.

이 플래그들을 실험해 볼 수 있습니다—하나를 끄고 출력이 어떻게 변하는지 확인해 보세요. 이것이 **전처리 설정 방법**을 효과적으로 적용하는 핵심입니다.

---

## 단계 5 – 정의된 ROIs 내에서만 OCR 수행

엔진, 이미지, ROIs, 전처리가 준비되었으니 이제 `recognize`를 호출할 차례입니다. 이 메서드는 `regions` 컬렉션을 포함하는 `OcrResult` 객체를 반환하며, 각 항목은 우리가 제공한 ROI 순서와 일치합니다.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Behind the scenes*: 엔진은 각 ROI를 잘라내고 전처리 파이프라인을 적용한 뒤, 정제된 조각에 인식 모델을 실행합니다. 리스트를 전달했기 때문에 결과는 동일한 순서를 유지해 후처리가 간단합니다.

---

## 단계 6 – 추출된 텍스트 읽고 사용하기 (How to OCR ROI)

마지막으로 `regions` 리스트를 순회하면서 인식된 문자열을 출력하거나 저장합니다. `Region` 객체는 Unicode 결과를 담고 있는 `text` 속성을 제공합니다.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**예상 출력 (예시)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

텍스트가 깨져 보이면 **전처리 설정 방법**을 다시 확인하세요: `contrast`를 높이거나 컬러 로고의 경우 `binarize`를 비활성화해 보세요.

---

## 일반적인 함정 및 전문가 팁

| 문제 | 발생 원인 | 해결 방법 (전처리 설정) |
|------|----------|------------------------|
| 기울어진 텍스트가 의미 없는 문자로 보임 | `deskew` 비활성화 또는 이미지가 너무 회전됨 | `preprocessing_options.deskew = True` 활성화 |
| 숫자가 점이나 잡음으로 변함 | 낮은 대비 또는 과도한 이진화 | `contrast` 낮추기(예: `1.2`) 또는 `binarize = False` 설정 |
| ROI 좌표가 몇 픽셀씩 어긋남 | 다른 DPI 또는 스캐너 스케일링 | 툴(e.g., Paint.NET)로 정확한 픽셀 위치 측정하거나 각 ROI에 작은 여유(`+5` 픽셀)를 추가 |
| 영역에 대한 결과가 비어 있음 | ROI가 이미지 경계 밖에 있음 | 이미지 크기 확인: `source_image.width`, `source_image.height` |

---

## 솔루션 확장 (다양한 시나리오에서 ROI OCR하기)

- **Dynamic ROIs**: 청구서 레이아웃이 가변적인 경우, 먼저 전체 페이지 OCR을 빠르게 실행해 키워드(예: “Customer:”, “Address:”)를 찾은 뒤 ROI를 실시간으로 계산할 수 있습니다.  
- **Batch Processing**: 위 단계를 함수로 감싸고 이미지 폴더를 순회합니다. 메모리 사용량을 낮추려면 동일한 `ocr_engine` 인스턴스를 재사용하세요.  
- **Exporting to JSON**: 출력 대신 딕셔너리를 만든 뒤 `json.dumps` 로 내보내면 ERP 시스템 연동 등 다운스트림 통합이 간단해집니다.

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## 결론

이제 Python에서 **ROI를 OCR하는 방법**을 보여주는 완전한 실행 예제와 **전처리 설정 방법**을 마스터했습니다. 엔진을 정확히 필요한 사각형으로 제한하고 사전에 이미지를 정리하면 더 빠르고 깨끗한 결과를 얻을 수 있어 청구서 자동화, 양식 디지털화, 페이지 일부만 필요한 모든 시나리오에 최적입니다.

다음 단계가 준비되셨나요? 다른 문서 유형에 맞게 ROI 좌표를 조정하거나 `sharpen`, `noise_reduction` 같은 추가 전처리 플래그를 실험해 보세요. Aspose OCR의 유연성 덕분에 거의 모든 이미지 품질에 맞게 파이프라인을 맞춤 설정할 수 있습니다.

문제가 발생하면 콘솔에 빈 영역이 출력되는지 확인하고 전처리 설정을 다시 검토하세요. 즐거운 코딩 되시고, OCR이 언제나 정확하길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
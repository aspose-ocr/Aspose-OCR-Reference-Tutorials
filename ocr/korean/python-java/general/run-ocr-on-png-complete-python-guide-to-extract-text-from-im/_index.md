---
category: general
date: 2026-01-12
description: Python으로 PNG 파일에서 OCR을 빠르게 실행하세요. 이미지와 청구서에서 텍스트를 추출하는 방법을 배우고, Aspose.OCR을
  사용해 OCR용 이미지를 로드하는 방법을 알아보세요.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: ko
og_description: PNG에서 OCR을 즉시 실행합니다. 이 가이드는 이미지와 청구서에서 텍스트를 추출하고, OCR을 위해 이미지를 로드하며,
  결과를 JSON 및 CSV로 저장하는 방법을 보여줍니다.
og_title: PNG에서 OCR 실행 – 전체 파이썬 튜토리얼
tags:
- OCR
- Python
- Image Processing
title: PNG에서 OCR 실행 – 이미지에서 텍스트를 추출하는 완전한 파이썬 가이드
url: /ko/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG에서 OCR 실행 – 이미지에서 텍스트 추출을 위한 완전한 Python 가이드

PNG 파일에 **OCR을 실행**해야 하는데 어떤 라이브러리를 사용해야 깔끔하고 구조화된 결과를 얻을 수 있을지 고민해 본 적 있나요? 여러분만 그런 것이 아닙니다. 실제 프로젝트—예를 들어 청구서 자동화나 영수증 스캔—에서 첫 번째 단계는 **이미지에서 텍스트 추출**하는 것이며, PNG는 손실 없는 품질을 유지하기 때문에 흔히 사용됩니다.

이 튜토리얼에서는 Aspose.OCR Python 패키지를 활용한 실전 예제를 단계별로 살펴봅니다. 가이드를 마치면 **OCR용 이미지 로드**, 모든 텍스트 라인 추출, 데이터를 깔끔한 JSON 객체로 변환, 그리고 CSV로 내보내는 방법을 알게 됩니다. 불필요한 내용 없이 바로 실행 가능한 실용적인 솔루션을 제공합니다.

## 배울 내용

- Aspose.OCR 라이브러리 설치 및 임포트 방법.  
- **PNG에서 OCR 실행** 및 결과 객체 처리 정확한 단계.  
- **청구서에서 텍스트 추출** 방법과 출력 포맷을 JSON 또는 CSV로 변환하는 방법.  
- 저대비 이미지, 다국어 문서, 신뢰도 점수 처리 팁.  
- 오늘 바로 실행할 수 있는 완전한 복사‑붙여넣기 코드 샘플.

> **전제 조건:** Python 3.8+ 및 pip 기본 사용법에 대한 이해. Aspose를 처음 사용한다면 걱정 마세요—이 가이드가 시작에 필요한 모든 것을 다룹니다.

---

## 1단계 – Aspose.OCR 설치 및 환경 준비

**PNG에서 OCR 실행**하기 전에 라이브러리를 시스템에 설치해야 합니다.

```bash
pip install aspose-ocr
```

> **프로 팁:** 가상 환경(`python -m venv venv`)을 사용하면 의존성을 격리할 수 있습니다. 여러 프로젝트를 동시에 다룰 때 버전 충돌을 방지해 줍니다.

설치가 끝났으면 필요한 모듈을 임포트합니다:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

여기서는 무거운 작업을 담당하는 `asposeocr`와 이후 직렬화를 위한 내장 `json` 라이브러리를 가져옵니다.

---

## 2단계 – OCR 엔진 생성 및 언어 설정

OCR 엔진은 실제로 픽셀을 읽는 핵심 구성 요소입니다. 대부분의 영문 청구서에는 영어 언어 팩을 사용합니다:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **왜 중요한가:** 언어를 지정하면 문자 집합이 제한돼 정확도가 높아지고 처리 속도가 빨라집니다. 다국어 청구서를 다뤄야 한다면 `ocr.Language.ENGLISH`를 해당 enum으로 교체하면 됩니다.

---

## 3단계 – OCR용 이미지 로드

이제 **OCR용 이미지 로드**를 수행합니다. `Image.load` 메서드는 파일 경로를 받아들이며 PNG, JPEG, BMP 등 다양한 포맷을 지원합니다.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **예외 상황:** PNG 파일이 5 MB를 초과할 정도로 큰 경우, 메모리 사용량을 줄이기 위해 먼저 리사이즈하는 것이 좋습니다. Pillow를 사용하면 한 줄로 처리할 수 있습니다:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## 4단계 – PNG에서 OCR 실행 및 결과 캡처

엔진이 준비되고 이미지가 로드되었으니 **PNG에서 OCR 실행**하고 구조화된 결과를 가져올 차례입니다.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

`ocr_result` 객체는 `OcrRegion` 항목들의 컬렉션을 포함하며, 각 항목은 인식된 텍스트와 신뢰도 점수(0‑100)를 제공합니다. 여기서 **청구서에서 텍스트 추출**에 필요한 세부 데이터를 얻을 수 있습니다.

---

## 5단계 – 결과를 JSON으로 변환하고 예쁘게 출력

대부분의 다운스트림 시스템은 JSON을 선호하므로 OCR 출력물을 깔끔한 문자열로 변환합니다.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### 샘플 출력

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

각 라인에 신뢰도 메트릭이 포함된 것을 확인할 수 있습니다—자동으로 **청구서에서 텍스트 추출**할 때 신뢰도가 낮은 항목을 필터링하는 데 유용합니다.

---

## 6단계 – OCR 데이터를 CSV로 저장 (텍스트 + 신뢰도 1줄당)

CSV는 스프레드시트나 빠른 데이터 임포트에 이상적입니다. Aspose는 모든 데이터를 CSV 파일로 한 번에 내보내는 원-라이너를 제공합니다.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

생성된 CSV는 다음과 같은 형태입니다:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

이제 Excel, Google Sheets에서 열거나 데이터베이스에 바로 넣을 수 있습니다.

---

## 보너스 – 낮은 신뢰도 텍스트 및 다페이지 PDF 처리

### 신뢰도 기준 필터링

높은 확신도를 가진 라인만 원한다면, JSON을 파일에 쓰기 전에 필터링합니다:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### 다페이지 문서

Aspose.OCR은 다페이지 PNG 또는 PDF의 각 페이지마다 자동으로 새로운 `page` 항목을 생성합니다. `ocr_data["pages"]`를 순회하면 별도 코드 없이 모든 페이지를 처리할 수 있습니다.

---

## 전체 작업 예제

아래는 **전체 스크립트**이며, 복사‑붙여넣기만 하면 바로 실행할 수 있습니다. `YOUR_DIRECTORY`를 PNG 파일이 들어 있는 폴더 경로로 바꾸세요.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

스크립트를 `python run_ocr.py`로 실행하면 콘솔에 JSON 덤프가 표시되고, 디스크에 CSV 파일이 생성되며, 신뢰도가 높은 항목 목록이 필터링되어 출력됩니다.

---

## 자주 묻는 질문

**Q: 영수증을 스캔한 이미지에서 텍스트를 추출하고 싶다면 어떻게 하나요?**  
A: 전혀 문제 없습니다. 동일한 워크플로우를 사용하되 `image_path`를 영수증 PNG 파일로 지정하면 됩니다. 영수증이 다른 언어라면 `engine.language`를 해당 언어로 바꾸세요.

**Q: PNG에 회전된 텍스트가 포함되어 있으면 어떻게 해야 하나요?**  
A: Aspose.OCR은 자동으로 방향을 감지하지만, 복잡한 경우 Pillow로 이미지를 직접 회전한 뒤 엔진에 전달할 수 있습니다.

**Q: Aspose.OCR 사용에 라이선스가 필요합니까?**  
A: 라이브러리는 출력에 워터마크가 붙는 무료 평가 모드를 제공하지만, 프로덕션에서는 라이선스가 필요합니다. 라이선스는 Aspose 웹사이트에서 구매할 수 있습니다.

---

## 결론

Python을 사용해 **PNG에서 OCR 실행**하는 데 필요한 모든 과정을 살펴보았습니다: SDK 설치, 이미지 로드, 구조화된 텍스트 추출, 그리고 결과를 JSON 또는 CSV로 저장하는 방법. 간단한 스크립트에서부터 자동화된 회계 파이프라인까지 **이미지에서 텍스트 추출** 혹은 **청구서에서 텍스트 추출**을 목표로 할 때, 위 단계들은 견고하고 프로덕션에 바로 적용 가능한 기반을 제공합니다.

다음 단계로 고려해볼 내용:

- CSV 출력을 데이터베이스와 연동해 대량 청구서 저장하기.  
- 정규식을 활용해 날짜, 금액, 세금 ID 등 특정 정보를 추출하는 후처리 추가하기.  
- 청구서에 QR 코드가 포함된 경우 `ocr_engine.recognize_barcode` 기능 활용하기.

시도해보고 신뢰도 임계값을 조정해 보세요. 문서 처리 워크플로우가 한결 수월해질 것입니다. 더 궁금한 점이나 멋진 활용 사례가 있으면 아래 댓글로 공유해 주세요—행복한 OCR 작업 되세요!  

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – OCR 결과 시각 예시")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
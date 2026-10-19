---
category: general
date: 2026-06-25
description: Python OCR을 사용하여 이미지에서 텍스트를 추출합니다. OCR을 위한 이미지 로드 방법, Python에서 OCR 수행
  방법, 영수증을 JSON으로 변환하는 간단한 단계들을 배워보세요.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: ko
og_description: Python OCR을 사용하여 이미지에서 텍스트를 추출합니다. 이 튜토리얼은 OCR을 위한 이미지 로드, Python에서
  OCR 수행, 영수증을 JSON으로 변환하는 과정을 단계별로 안내합니다.
og_title: Python으로 이미지에서 텍스트 추출 – 전체 OCR 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Python에서 이미지 텍스트 추출 – 전체 OCR 가이드
url: /ko/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 이미지에서 텍스트 추출 – 전체 OCR 가이드

이미지에서 **텍스트를 추출**해야 했지만 어디서 시작해야 할지 몰랐던 적이 있나요? 이 튜토리얼에서는 **OCR을 위한 이미지 로드**, **Python에서 OCR 수행**, 그리고 **영수증을 JSON으로 변환**하는 방법을 몇 줄의 코드만으로 안내합니다.

영수증 스캔 앱, 비용 추적기 등을 만든 적이 있거나 데이터 입력을 자동화하고 싶다면, 이 흐름을 마스터하는 것이 얼마나 큰 변화를 가져오는지 알게 될 것입니다. 끝까지 따라오면 영수증 사진을 읽어 깔끔한 JSON 페이로드를 생성하는 작동 스크립트를 얻게 됩니다.

## 배울 내용

우리는 `aocr` 라이브러리 설치부터 원시 결과 처리까지 모든 단계를 다룰 것입니다. 구체적으로 다음을 배웁니다:

1. **OCR 엔진 인스턴스 생성** – 모든 인식 작업의 진입점입니다.  
2. **OCR을 위한 이미지 로드** – 엔진에 읽을 파일을 알려줍니다.  
3. **내보내기 형식 선택** – JSON 또는 XML 중에서, 우리는 사용하기 쉬우므로 JSON을 선택합니다.  
4. **인식 실행** – 실제로 Python에서 OCR을 수행합니다.  
5. **결과 출력 또는 저장** – 영수증을 JSON으로 변환하고 출력을 확인합니다.

OCR에 대한 사전 경험은 필요하지 않습니다; 기본적인 Python 환경과 이미지 파일(영수증, 전단지 등)만 있으면 됩니다.  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="Python OCR을 사용한 이미지에서 텍스트 추출 흐름도"}

## 이미지에서 텍스트 추출 – 단계별 Python OCR

아래는 완전하고 바로 실행 가능한 스크립트입니다. `receipt_ocr.py`라는 파일에 복사‑붙여넣기하고 `python receipt_ocr.py`를 실행해 보세요.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### 왜 이렇게 동작할까

- **엔진 인스턴스** – `aocr.OcrEngine()`는 모든 무거운 작업(모델 로드, 전처리 등)을 캡슐화합니다.  
- **이미지 로드** – `engine.load_image()`는 라이브러리에게 정확히 어떤 비트맵을 분석할지 알려줍니다; JPEG, PNG, 혹은 다중 페이지 PDF도 사용할 수 있습니다.  
- **내보내기 형식** – `engine.export_format`을 `aocr.ExportFormat.JSON`으로 설정하면 결과가 구조화된 문자열이 되어 JSON을 기대하는 API에 최적입니다.  
- **인식 호출** – `engine.recognize()`는 백그라운드에서 신경망 추론을 수행하고, 감지된 텍스트 블록, 신뢰도 점수, 레이아웃 정보를 포함한 JSON 문자열을 반환합니다.  

---

## aocr로 OCR을 위한 이미지 로드

이미지에 특별한 전처리가 필요한지 궁금하다면, 짧은 답은 **아니오**입니다—`aocr`가 대부분의 일반적인 경우(대비 조정, 기울기 보정)를 자동으로 처리합니다. 그러나 정확도를 높이려면 다음을 고려하세요:

- 이미지 해상도가 최소 300 dpi인지 확인합니다.  
- 불필요한 테두리를 잘라냅니다.  
- 그레이스케일로 변환 후 입력합니다(선택 사항, `engine.load_image()`가 자동으로 처리합니다).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro tip:* 영수증에 잡음이 많다면 위의 추가 단계가 **Python에서 OCR 수행** 정확도를 눈에 띄게 향상시킬 수 있습니다.

---

## 내보내기 형식 선택 및 영수증을 JSON으로 변환

“그냥 평문 텍스트만 얻으면 안 될까?” 라고 생각할 수 있습니다. JSON은 계층 구조(줄, 단어, 경계 상자)를 보존하므로 나중에 *총액*이나 *날짜*와 같은 필드를 매핑하기가 훨씬 쉽습니다.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

스크립트를 실행하면 `json_result`는 다음과 같은 형태를 가집니다(간결히 표시).

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

이제 **영수증을 JSON으로 변환**한 페이로드를 데이터베이스, REST 엔드포인트, 혹은 머신러닝 모델에 바로 전달할 수 있습니다.

---

## 인식 실행 및 결과 가져오기

마지막 단계—실제로 OCR을 수행하는 것—은 `recognize()`를 호출하는 것만큼 간단합니다. 라이브러리는 내부적으로:

1. 이미지를 사전 학습된 컨볼루션 신경망에 전달합니다.  
2. 네트워크 출력을 읽을 수 있는 문자로 디코딩합니다.  
3. 모든 결과를 선택한 형식(JSON)으로 패키징합니다.

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

출력을 화면에 표시하는 대신 파일에 저장하려면 다음과 같이 작성하면 됩니다:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Edge case:* 일부 영수증에는 비 ASCII 문자(예: “€” )가 포함될 수 있습니다. 위와 같이 UTF‑8 인코딩으로 파일을 열어 텍스트가 깨지는 것을 방지하세요.

---

## 전체 작업 예제 (모든 단계가 하나의 스크립트에 포함)

모든 내용을 하나로 합치면 다음과 같은 최종 스크립트를 얻을 수 있습니다:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

다음 명령으로 실행합니다:

```bash
python receipt_ocr.py
```

실행하면 확인 메시지가 출력되고, 같은 폴더에 구조화된 데이터를 담은 `receipt_output.json` 파일이 생성됩니다.

---

## 결론

이제 Python을 사용해 **이미지에서 텍스트를 추출**하는 방법, **OCR을 위한 이미지 로드**, **Python에서 OCR 수행**, 그리고 **영수증을 JSON으로 변환**하는 방법을 알게 되었습니다. 이 엔드‑투‑엔드 흐름은 가볍고 `aocr` 패키지만 있으면 되며, 어떤 자동화 파이프라인에도 손쉽게 삽입할 수 있습니다.

다음은? 내보내기 형식을 XML로 바꾸어 보거나, 다양한 이미지 전처리 기법을 실험하거나, 업로드된 영수증을 받아 즉시 JSON 페이로드를 반환하는 작은 Flask API를 구축해 보세요. 기본을 잡았다면 가능성은 무한합니다.

궁금한 점이나 문제가 있으면 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [Aspose OCR을 사용한 이미지 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [이미지 텍스트 추출 – Aspose.OCR for .NET을 활용한 OCR 최적화](/ocr/english/net/ocr-optimization/)
- [Aspose.OCR for .NET을 사용해 이미지에서 표 추출하는 방법](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
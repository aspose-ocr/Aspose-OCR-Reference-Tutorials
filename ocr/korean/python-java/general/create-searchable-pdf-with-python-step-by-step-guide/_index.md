---
category: general
date: 2026-05-31
description: Python OCR을 사용하여 스캔된 이미지에서 검색 가능한 PDF를 만들기. 스캔된 이미지 PDF 변환, TIFF를 PDF로
  변환, 그리고 몇 분 안에 OCR 텍스트 레이어를 추가하는 방법을 배우세요.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: ko
og_description: 즉시 검색 가능한 PDF를 만들 수 있습니다. 이 가이드는 OCR을 실행하고, 스캔된 이미지 PDF를 변환하며, 단일
  파이썬 스크립트를 사용해 OCR 텍스트 레이어를 추가하는 방법을 보여줍니다.
og_title: Python으로 검색 가능한 PDF 만들기 – 완전 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Python으로 검색 가능한 PDF 만들기 – 단계별 가이드
url: /ko/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python으로 검색 가능한 PDF 만들기 – 단계별 가이드

스캔한 페이지에서 **검색 가능한 PDF**를 만들기 위해 수많은 도구를 뒤섞어 쓰는 것이 궁금했던 적 있나요? 당신만 그런 것이 아닙니다. 많은 사무 환경에서 스캔한 TIFF나 JPEG 파일이 공유 드라이브에 올라가고, 다음 사용자는 텍스트를 직접 복사‑붙여넣기 해야 합니다—불편하고 오류가 발생하기 쉬우며 시간도 많이 소요됩니다.  

이 튜토리얼에서는 **스캔 이미지 PDF 변환**, **TIFF를 PDF로 변환**, 그리고 **OCR 텍스트 레이어 추가**를 한 번에 수행할 수 있는 깔끔하고 프로그래밍적인 솔루션을 단계별로 살펴보겠습니다. 최종적으로 OCR을 실행하고 숨겨진 텍스트를 삽입한 뒤, 인덱싱·검색·공유가 가능한 검색 가능한 PDF를 출력하는 사용 가능한 스크립트를 얻게 됩니다.

## 필요 사항

- Python 3.9+ (최근 버전이면 모두 사용 가능)
- `aspose-ocr` 및 `aspose-pdf` 패키지 (`pip install aspose-ocr aspose-pdf` 로 설치)
- 스캔 이미지 파일 (`.tif`, `.png`, `.jpg` 또는 이미지만 포함된 PDF 페이지)
- 적당한 양의 RAM (OCR 엔진은 가볍고 노트북에서도 충분히 처리 가능)

> **Pro tip:** Windows 환경이라면 관리자 권한으로 PowerShell을 실행한 뒤 위 명령을 실행하는 것이 가장 간편합니다.

```bash
pip install aspose-ocr aspose-pdf
```

이제 사전 준비가 끝났으니 코드로 들어가 보겠습니다.

## 1단계: OCR 엔진 인스턴스 생성 – *create searchable pdf*

먼저 OCR 엔진을 시작합니다. 모든 픽셀을 읽어 문자로 변환하는 두뇌와 같은 역할을 합니다.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **왜 중요한가:** 엔진을 한 번만 초기화하면 메모리 사용량을 낮게 유지할 수 있습니다. 페이지마다 `OcrEngine()`을 호출하면 금방 자원이 부족해집니다.

## 2단계: 스캔 이미지 로드 – *convert tiff to pdf* & *convert scanned image pdf*

다음으로 처리할 파일을 엔진에 지정합니다. API는 모든 래스터 이미지를 지원하므로 TIFF도 JPEG와 동일하게 사용할 수 있습니다.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

PDF에 스캔 이미지만 포함되어 있는 경우에도 `load_image`를 사용하면 Aspose가 첫 페이지를 자동으로 추출합니다.

## 3단계: PDF 저장 옵션 준비 – *add OCR text layer*

여기서는 최종 PDF의 형태를 설정합니다. 핵심 플래그는 `create_searchable_pdf`이며, 이를 `True`로 설정하면 라이브러리가 시각적 내용과 일치하는 보이지 않는 텍스트 레이어를 삽입합니다.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **텍스트 레이어가 하는 일:** 결과 파일을 Adobe Reader에서 열어 텍스트를 선택하면 숨겨진 문자를 볼 수 있습니다. 검색 엔진도 이를 색인화하므로 컴플라이언스·아카이빙에 최적입니다.

## 4단계: OCR 실행 및 저장 – *how to run OCR* in a single call

이제 마법이 일어납니다. 한 번의 메서드 호출로 인식 엔진을 실행하고 검색 가능한 PDF를 디스크에 기록합니다.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

`recognize` 메서드는 상태 객체를 반환해 오류를 확인할 수 있지만, 대부분의 간단한 시나리오에서는 위 호출만으로 충분합니다.

### 예상 출력

스크립트를 실행하면 다음과 같이 출력됩니다:

```
PDF saved as searchable PDF.
```

`scanned_page_searchable.pdf`를 열면 텍스트를 선택·복사‑붙여넣기 할 수 있고, `Ctrl+F` 검색도 작동합니다. 이것이 **create searchable pdf** 워크플로우의 핵심입니다.

## 전체 작업 스크립트

아래는 완전한 실행 가능한 스크립트입니다. 자리표시자 경로를 실제 파일 위치로 바꾸기만 하면 됩니다.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

`create_searchable_pdf.py`라는 이름으로 저장하고 실행합니다:

```bash
python create_searchable_pdf.py
```

## 흔히 묻는 질문 & 예외 상황

### 1️⃣ 다중 페이지 PDF를 처리할 수 있나요?

네. `ocr_engine.load_image("file.pdf")`를 사용한 뒤 `ocr_engine.recognize(pdf_save_options, page_number)`를 페이지마다 호출하면 됩니다. 라이브러리가 자동으로 다중 페이지 검색 가능한 PDF를 생성합니다.

### 2️⃣ 소스 파일이 고해상도 TIFF(300 dpi 이상)인 경우는?

해상도가 높을수록 OCR 정확도가 향상되지만 메모리 사용량도 커집니다. `MemoryError`가 발생하면 먼저 이미지를 다운스케일하세요:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ OCR 언어를 어떻게 변경하나요?

이미지를 로드하기 전에 엔진의 `language` 속성을 설정하면 됩니다:

```python
ocr_engine.language = "fra"   # French
```

지원되는 언어 코드는 Aspose 문서에 전체 목록이 제공됩니다.

### 4️⃣ 원본 이미지 품질을 유지해야 할 경우는?

`PdfSaveOptions` 클래스의 `compression` 속성을 `PdfCompression.None`으로 설정하면 래스터 데이터를 그대로 보존합니다.

```python
pdf_save_options.compression = "None"
```

## 프로덕션 환경 배포 팁

- **배치 처리:** 핵심 로직을 파일 경로 리스트를 받는 함수로 감싸고, 성공·실패를 CSV에 기록해 감사 로그를 남깁니다.
- **병렬 처리:** `concurrent.futures.ThreadPoolExecutor`를 사용해 여러 코어에서 OCR을 동시에 실행합니다. 단, 각 스레드마다 별도의 `OcrEngine` 인스턴스가 필요합니다.
- **보안:** 민감한 문서를 다룰 경우 스크립트를 샌드박스 환경에서 실행하고, 처리 후 임시 파일을 즉시 삭제하세요.

## 결론

이제 Python 스크립트를 사용해 스캔 이미지에서 **검색 가능한 PDF** 파일을 만드는 방법을 알게 되었습니다. OCR 엔진을 초기화하고, TIFF(또는 기타 래스터)를 로드한 뒤, `PdfSaveOptions`를 **OCR 텍스트 레이어 추가**하도록 설정하고, 마지막으로 `recognize`를 호출하면 **스캔 이미지 PDF 변환** 및 **TIFF를 PDF로 변환** 파이프라인이 단일 명령으로 완성됩니다.

다음 단계는? 파일 감시 프로그램과 연동해 새 스캔이 폴더에 들어올 때마다 자동으로 검색 가능한 PDF로 변환해 보세요. 혹은 다양한 OCR 언어를 적용해 다국어 아카이브를 지원하는 실험도 가능합니다. OCR과 PDF 생성이 결합되면 가능성은 무한합니다.

다른 언어나 프레임워크에서 **how to run OCR**에 대한 질문이 있나요? 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요! 

![스캔 이미지 → OCR 엔진 → 검색 가능한 PDF 흐름 (create searchable pdf)](searchable-pdf-flow.png "검색 가능한 pdf 흐름도")


## 다음에 배울 내용은?

- [Aspose.OCR을 사용한 .NET에서 PDF OCR 처리 방법](/ocr/english/net/text-recognition/recognize-pdf/)
- [C#으로 이미지들을 PDF로 변환 – 다중 페이지 OCR 결과 저장](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Aspose.OCR을 사용해 언어별 이미지 텍스트 OCR 처리 방법](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
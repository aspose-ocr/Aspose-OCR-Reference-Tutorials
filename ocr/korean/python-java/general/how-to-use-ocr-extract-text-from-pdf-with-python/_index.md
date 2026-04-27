---
category: general
date: 2026-04-26
description: 스캔한 PDF에 OCR을 적용하고, PDF에서 텍스트를 추출하며, PDF에 OCR을 실행하고, 스캔한 PDF를 몇 단계만에
  검색 가능한 파일로 변환하는 방법.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: ko
og_description: 'Python에서 OCR 사용 방법: PDF에서 텍스트를 추출하고, PDF에 OCR을 실행하며, 스캔한 PDF를 검색
  가능한 문서로 변환하는 방법을 배워보세요.'
og_title: OCR 사용 방법 – PDF에서 텍스트 추출하기 빠른 가이드
tags:
- OCR
- Python
- PDF
- Text Extraction
title: OCR 사용 방법 – Python으로 PDF에서 텍스트 추출
url: /ko/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 사용 방법 – Python으로 PDF에서 텍스트 추출

스캔한 계약서, 영수증, 전자책에서 텍스트를 추출하기 위해 **OCR 사용 방법**을 궁금해 본 적이 있나요? 당신만 그런 것이 아닙니다. 실제 프로젝트에서 받는 PDF는 종종 이미지일 뿐이며, OCR 없이는 내용을 검색하거나 색인화하거나 분석할 수 없습니다.  

이 튜토리얼에서는 **OCR 사용 방법**, **PDF에서 텍스트 추출** 방법, 그리고 스캔된 PDF 파일을 검색 가능한 문서로 **변환**하고 싶을 때의 이유를 보여주는 완전하고 실행 가능한 예제를 단계별로 살펴봅니다. 또한 OCR 엔진이 각 페이지를 명확히 인식할 수 있도록 **PDF를 이미지로 로드**하는 미묘한 기술도 다룹니다.

> **빠른 미리보기:** 최종적으로 다중 페이지 PDF를 로드하고 각 페이지에 OCR을 실행한 뒤 인식된 텍스트를 출력하는 스크립트를 얻게 됩니다 – 외부 서비스는 전혀 필요하지 않습니다.

## 필요 사항

- Python 3.9+ (최근 버전이면 모두 사용 가능)
- `aocr` 패키지 (또는 `OcrEngine`과 `Image.load`를 제공하는 호환 OCR 라이브러리)
- 처리하려는 스캔된 PDF 파일 (예: `contract.pdf`)
- 적당한 양의 RAM (100 페이지당 약 200 MB 정도면 보통 충분합니다)

OCR 라이브러리를 아직 설치하지 않았다면 다음을 실행하세요:

```bash
pip install aocr
```

> **프로 팁:** 가상 환경을 사용해 의존성을 깔끔하게 관리하세요.

## 1단계: PDF를 이미지로 로드 – 퍼즐의 첫 번째 조각

OCR이 수행되기 전에 PDF는 이미지 형태로 표현되어야 합니다. 여기서 보조 키워드 **load pdf as image**가 등장합니다.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*왜 중요한가:* `aocr.Image.load`는 내부적으로 각 PDF 페이지를 비트맵으로 래스터화하여 OCR 엔진이 이해할 수 있는 형태로 변환합니다. 이 단계를 건너뛰고 원본 PDF를 그대로 전달하면 엔진은 픽셀 데이터가 아니라 벡터 데이터를 받았다고 오류를 발생시킵니다.

> **참고:** 경로는 절대 경로나 상대 경로 모두 가능합니다. 파일이 읽기 가능한지 확인하세요; 그렇지 않으면 `FileNotFoundError`가 발생합니다.

## 2단계: PDF에서 OCR 실행 – 픽셀을 문자로 변환

PDF가 이미지 형태가 되었으니 이제 **run OCR on PDF**를 수행할 수 있습니다. 아래 스니펫은 모든 페이지를 한 번에 처리합니다:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*내부에서 무슨 일이 일어나나요?* `process_all_pages`는 래스터화된 페이지들을 순회하면서 OCR 모델을 적용하고, 페이지당 하나씩 결과 객체 리스트를 반환합니다. 각 결과에는 인식된 텍스트, 신뢰도 점수, 그리고 필요 시 사용할 수 있는 바운딩 박스가 포함됩니다.

## 3단계: PDF에서 텍스트 추출 – 문자열 가져오기

OCR 결과를 얻었으니 이제 순수 텍스트를 추출하는 일은 매우 간단합니다. 페이지를 순회하면서 출력을 프린트하고, 보조 키워드 **extract text from pdf**를 시연합니다.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**예상 출력** (간략히 표시):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

텍스트를 하나의 문자열로 합치고 싶다면 간단히 연결하면 됩니다:

```python
full_text = "\n".join(r.text for r in page_results)
```

이제 OCR을 사용해 **PDF에서 텍스트를 성공적으로 추출**했습니다.

## 4단계: 스캔된 PDF 변환 – 검색 가능하게 만들기

많은 하위 시스템(예: Elasticsearch 또는 SharePoint)은 텍스트 덤프보다 검색 가능한 PDF를 기대합니다. OCR 결과를 원본 PDF에 다시 삽입하면 **convert scanned PDF**를 통해 검색 가능한 버전을 만들 수 있습니다.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*왜 이렇게 할까?* 검색 가능한 PDF는 원본 레이아웃과 이미지를 유지하면서 텍스트 선택 및 색인화를 가능하게 하므로 사람과 기계 모두에게 이득이 됩니다.

## 흔히 발생하는 문제 및 예외 상황

### 메모리보다 큰 다중 페이지 PDF

PDF 페이지가 수백 장에 달한다면 한 번에 모두 로드하면 RAM이 부족해질 수 있습니다. `aocr` 라이브러리는 지연 로딩을 지원합니다:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

그런 다음 페이지를 하나씩 처리합니다:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### 저품질 스캔

흐리거나 대비가 낮은 스캔에서는 OCR 정확도가 크게 떨어집니다. 이미지를 엔진에 전달하기 전에 전처리를 고려하세요:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### 언어 지원

기본적으로 엔진은 영어를 가정합니다. 다른 언어로 **run OCR on PDF**를 수행하려면 언어 코드를 설정하세요:

```python
ocr_engine.language = "spa"  # Spanish
```

해당 언어 모델이 설치되어 있는지 확인하십시오.

## 전체 작업 예시

모든 내용을 합치면 `ocr_pdf.py`라는 파일에 바로 넣어 실행할 수 있는 독립형 스크립트가 됩니다:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

다음과 같이 실행합니다:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

콘솔에 텍스트가 출력되는 것을 확인할 수 있으며, `-o` 옵션을 제공한 경우 원본 파일 옆에 검색 가능한 PDF가 생성됩니다.

## 전문가 팁 및 모범 사례

- **배치 처리:** 수십 개의 PDF를 다룰 때는 위 로직을 루프에 감싸고 각 파일의 성공/실패를 로그에 기록하세요.
- **신뢰도 필터링:** 각 `page_result`에는 신뢰도 메트릭이 포함됩니다. 신뢰도가 낮은 페이지는 수동 검토를 위해 버리거나 플래그를 지정하세요.
- **병렬 처리:** CPU에 코어가 여러 개 있다면 `concurrent.futures`를 사용해 페이지를 병렬로 처리해 보세요—단, 메모리 사용량에 유의하십시오.
- **버전 고정:** `aocr` API는 변할 수 있습니다. `requirements.txt`에 버전을 고정(`aocr==2.3.1` 등)하여 깨지는 변경을 방지하세요.

## 결론

우리는 **OCR 사용 방법**을 통해 **PDF에서 텍스트 추출**, **PDF에서 OCR 실행**, **PDF를 이미지로 로드**, 그리고 **스캔된 PDF를 검색 가능한 형식으로 변환**하는 전체 과정을 살펴보았습니다. 코드는 완전하고 설명은 *무엇을* 그리고 *왜* 하는지를 모두 다루며, 이제 이미지 기반 PDF를 다루는 모든 프로젝트에 재사용 가능한 패턴을 갖추게 되었습니다.

다음은? 추출한 텍스트를 자연어 파이프라인에 넣어 보거나, Elasticsearch로 검색 가능한 PDF를 색인화하거나, Tesseract나 Azure Computer Vision 같은 다른 OCR 백엔드를 실험해 보세요. 가능성은 무한하고, 도구는 이미 여러분 손에 있습니다.

행복한 코딩 되세요, 그리고 여러분의 PDF가 언제나 검색 가능하기를 바랍니다! 

![OCR 사용 예시](/images/ocr_workflow.png "OCR 사용 방법")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
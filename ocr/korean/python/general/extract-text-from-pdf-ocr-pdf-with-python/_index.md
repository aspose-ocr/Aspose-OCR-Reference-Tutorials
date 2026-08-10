---
category: general
date: 2026-04-29
description: Python에서 Aspose OCR을 사용하여 PDF에서 텍스트를 추출합니다. 배치 OCR PDF 처리 방법을 배우고, 스캔된
  PDF 텍스트를 변환하며, 신뢰도가 낮은 페이지를 처리합니다.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: ko
og_description: Python에서 Aspose OCR을 사용하여 PDF에서 텍스트를 추출합니다. 이 가이드는 배치 OCR PDF 처리,
  스캔된 PDF 텍스트 변환 및 낮은 신뢰도 결과 처리를 보여줍니다.
og_title: PDF에서 텍스트 추출 – Python으로 PDF OCR
tags:
- OCR
- Python
- PDF processing
title: PDF에서 텍스트 추출 – Python으로 PDF OCR
url: /ko/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF에서 텍스트 추출 – Python으로 OCR PDF

PDF에서 **텍스트를 추출**해야 하는데 파일이 스캔된 이미지일 때가 있나요? 혼자가 아닙니다—많은 개발자들이 PDF를 검색 가능한 데이터로 변환하려다 이 문제에 부딪힙니다. 좋은 소식은? Aspose OCR for Python을 사용하면 몇 줄의 코드로 스캔된 PDF 텍스트를 변환할 수 있고, 파일이 수십 개일 때는 **배치 OCR PDF 처리**도 실행할 수 있습니다.

이 튜토리얼에서는 전체 워크플로우를 단계별로 살펴보겠습니다: 라이브러리 설정, 단일 PDF에 대한 OCR 실행, 배치로 확장, 그리고 낮은 신뢰도 페이지를 처리하여 언제 수동 검토가 필요한지 알 수 있도록 합니다. 마지막까지 진행하면 스캔된 PDF에서 텍스트를 추출하는 실행 가능한 스크립트를 얻을 수 있으며, 각 단계의 이유도 이해하게 됩니다.

## 필요 사항

시작하기 전에 다음을 준비하세요:

- Python 3.8 이상 (코드가 f‑strings를 사용하므로 3.6+에서도 동작하지만, 3.8+을 권장합니다)
- Aspose OCR for Python 라이선스 또는 무료 체험 키 (Aspose 웹사이트에서 얻을 수 있습니다)
- 처리하려는 하나 이상의 스캔된 PDF가 들어 있는 폴더
- 생성된 *.txt* 보고서를 저장할 충분한 디스크 공간

그게 전부입니다—무거운 외부 종속성도 없고, OpenCV 같은 복잡한 설정도 필요 없습니다. Aspose OCR 엔진이 무거운 작업을 대신 수행합니다.

## 환경 설정

먼저 PyPI에서 Aspose OCR 패키지를 설치합니다:

```bash
pip install aspose-ocr
```

라이선스 파일(`Aspose.OCR.lic`)이 있다면 프로젝트 루트에 두고 다음과 같이 활성화합니다:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Pro tip:** 라이선스 파일을 버전 관리에서 제외하세요; `.gitignore`에 추가하여 실수로 노출되는 것을 방지합니다.

## 단일 PDF에서 OCR 수행

이제 단일 스캔된 PDF에서 텍스트를 추출해 보겠습니다. 핵심 단계는 다음과 같습니다:

1. `OcrEngine` 인스턴스를 생성합니다.
2. PDF 파일을 지정합니다.
3. 각 페이지에 대해 `OcrResult`를 가져옵니다.
4. 평문 텍스트 출력을 디스크에 저장합니다.
5. 엔진을 해제하여 네이티브 리소스를 해제합니다.

전체 실행 가능한 스크립트는 다음과 같습니다:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**예상 출력:** 각 페이지마다 스크립트가 `Page 1: confidence 97.45%`와 같은 정보를 출력합니다. 페이지 신뢰도가 80 % 이하이면 경고가 표시되어 OCR이 문자를 놓쳤을 가능성을 알려줍니다.

### 왜 이렇게 동작하나요

- **`OcrEngine`** 은 네이티브 Aspose OCR 라이브러리의 진입점으로, 이미지 전처리부터 문자 인식까지 모든 작업을 처리합니다.
- **`extract_from_pdf`** 은 각 PDF 페이지를 자동으로 래스터화하므로 직접 이미지를 변환할 필요가 없습니다.
- **Confidence scores** 를 활용하면 품질 검사를 자동화할 수 있습니다—법률 문서나 의료 문서처럼 정확도가 중요한 경우에 필수적입니다.

## Python으로 배치 OCR PDF 처리

실제 프로젝트에서는 파일이 하나 이상인 경우가 대부분입니다. 단일 파일 스크립트를 **배치 OCR PDF 처리** 파이프라인으로 확장해 보겠습니다. 이 파이프라인은 디렉터리를 순회하면서 각 PDF를 처리하고 결과를 일치하는 하위 폴더에 저장합니다.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### 이점

- **Scalability:** 함수가 폴더를 한 번만 순회하면서 각 PDF마다 전용 출력 하위 폴더를 생성합니다. 수십 개의 문서가 있을 때도 정리가 깔끔합니다.
- **Reusability:** `ocr_pdf_file` 은 다른 스크립트(예: 웹 서비스)에서 호출할 수 있는 순수 함수입니다.
- **Error handling:** 입력 폴더가 비어 있으면 친절한 메시지를 출력해 조용히 실패하는 상황을 방지합니다.

## 스캔된 PDF 텍스트 변환 – 엣지 케이스 처리

위 코드는 대부분의 PDF에서 잘 동작하지만, 몇 가지 특수 상황에 부딪힐 수 있습니다:

| Situation | Why It Happens | How to Mitigate |
|-----------|----------------|-----------------|
| **Encrypted PDFs** | PDF가 비밀번호로 보호되어 있습니다. | `extract_from_pdf(pdf_path, password="yourPwd")` 로 비밀번호를 전달합니다. |
| **Multi‑language documents** | Aspose OCR 기본값이 영어이기 때문입니다. | `ocr_engine.language = "spa"` 로 스페인어를 지정하거나, 혼합 언어의 경우 리스트를 제공합니다. |
| **Very large PDFs (>500 pages)** | 각 페이지가 RAM에 로드되면서 메모리 사용량이 급증합니다. | `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` 와 같이 청크 단위로 처리하고 루프를 돌립니다. |
| **Poor scan quality** | 낮은 DPI 또는 노이즈가 많아 신뢰도가 떨어집니다. | `engine.image_preprocessing = True` 로 전처리를 활성화하거나 `engine.dpi = 300` 으로 DPI를 높입니다. |

> **Watch out:** 이미지 전처리를 켜면 CPU 사용 시간이 눈에 띄게 증가할 수 있습니다. 야간 배치를 실행한다면 충분한 시간을 예약하거나 별도의 워커를 띄워 운영하세요.

## 출력 확인

스크립트가 완료되면 다음과 같은 폴더 구조를 확인할 수 있습니다:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

`.txt` 파일을 열면 원본 스캔 내용과 일치하는 깨끗한 UTF‑8 인코딩 텍스트가 표시됩니다. 문자 깨짐이 보이면 PDF의 언어 설정을 다시 확인하고, 머신에 올바른 폰트 팩이 설치되어 있는지 점검하세요.

## 리소스 정리

Aspose OCR은 네이티브 DLL에 의존하므로 작업이 끝난 뒤 `engine.dispose()` 를 호출해 주는 것이 중요합니다. 이 단계를 놓치면 특히 장시간 실행되는 배치 작업에서 메모리 누수가 발생할 수 있습니다.

```python
# Always the last line of your script
engine.dispose()
```

## 전체 엔드‑투‑엔드 예제

모든 내용을 하나로 합치면, 다음과 같은 단일 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
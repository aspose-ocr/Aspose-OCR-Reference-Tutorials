---
category: general
date: 2026-06-06
description: Python OCR을 사용하여 이미지 PDF에서 텍스트를 추출합니다. 비동기 배치 인식을 통해 스캔한 문서를 빠르게 텍스트로
  변환하는 방법을 배워보세요.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: ko
og_description: Python으로 이미지 PDF에서 텍스트 추출하기. 이 단계별 가이드는 비동기 OCR을 사용하여 스캔한 문서를 텍스트로
  변환하는 방법을 보여줍니다.
og_title: 이미지 PDF에서 텍스트 추출 – 파이썬 OCR 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 이미지 PDF에서 텍스트 추출 – 스캔한 문서를 텍스트로 변환하는 파이썬 가이드
url: /ko/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지 PDF에서 텍스트 추출 – 스캔된 문서를 텍스트로 변환하는 Python 가이드

시간을 들여 다시 타이핑하지 않고 **이미지 PDF에서 텍스트를 추출**해야 했던 적이 있나요? 이 가이드에서는 Python에서 간단한 비동기 OCR 워크플로를 사용해 **스캔된 문서를 텍스트로 변환**하는 방법을 보여드립니다.  

스캔된 PDF가 쌓여 있는 모습을 보며 “더 빠른 방법이 없을까?”라고 생각한 적이 있다면, 바로 여기가 맞습니다. 코드 한 줄 한 줄을 자세히 살펴보고, 각 부분이 왜 중요한지 설명하며, 마주칠 수 있는 몇 가지 엣지 케이스까지 다룹니다.

## 배울 내용

- OCR 엔진을 시작하고 인식 언어를 설정하는 방법  
- PNG와 PDF가 섞인 리스트를 배치 인식기로 전달하는 메커니즘  
- 앱이 응답성을 유지하도록 OCR 작업을 비동기적으로 실행하는 방법  
- 결과를 가져와 원본 파일과 매핑하고 깔끔하게 출력하는 방법  

**전제 조건**: Python 3.8 이상, `asyncio` 또는 `concurrent.futures`에 대한 기본 이해, 그리고 예제와 유사한 `OcrEngine` 클래스를 제공하는 OCR 라이브러리(예: Aspose.OCR, Tesseract 래퍼, 혹은 커스텀 래퍼). 별도의 복잡한 설정은 필요 없으며, 라이브러리만 설치하면 바로 시작할 수 있습니다.

![이미지 PDF에서 텍스트 추출](https://example.com/placeholder.png "OCR 출력 스크린샷 – 이미지 PDF에서 텍스트 추출")

## 이미지 PDF에서 텍스트 추출 – OCR 엔진 설정하기

먼저 문서 언어에 맞게 구성된 OCR 엔진 인스턴스가 필요합니다. 여기서는 프랑스어를 사용하지만, 지원되는 언어라면 어떤 것이든 교체할 수 있습니다.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**왜 중요한가**: 언어를 미리 설정하면 정확도가 크게 향상됩니다. 엔진은 언어별 사전과 문자 모델을 사용하므로, 잘못된 언어를 지정하면 출력이 엉망이 되는 흔한 원인입니다.

## 파일 리스트 준비 – 이미지와 PDF를 함께

우리 배치 인식기는 래스터 이미지(`.png`, `.jpg`)와 PDF 컨테이너를 모두 처리할 수 있습니다. 파일 경로를 담은 일반 Python 리스트만 전달하면 됩니다.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**팁**: 리스트는 평평하게 유지하세요; 엔진이 내부적으로 각 PDF 페이지를 이미지로 풀어낸 뒤 인식합니다. 파일 수가 수천 개에 달한다면 메모리 급증을 방지하기 위해 리스트를 작은 배치로 나누는 것을 고려하세요.

## 비동기 배치 인식 시작하기

메인 스레드를 차단하지 않고 OCR 작업을 백그라운드에서 실행합니다. 이 메서드는 결국 `OcrResult` 객체 리스트를 담게 될 `Future`를 반환합니다.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**작동 방식**: 엔진은 내부적으로 스레드 풀(또는 async 태스크)을 생성합니다(구현에 따라 다름). 이를 통해 UI 업데이트, 파일 추가 가져오기, 진행 상황 로깅 등 다른 작업을 동시에 수행할 수 있습니다.

## OCR이 실행되는 동안 유용한 작업 수행하기

많은 사람들이 미래 객체를 빡빡한 루프에서 폴링하며 대기합니다. 대신 전혀 관련 없는 작업을 수행하세요. 예시로 상태 라인을 출력해 보겠습니다.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Future가 완료되면 결과 모으기

OCR 출력을 수집할 준비가 되면 `concurrent.futures`의 `as_completed`를 사용합니다. 이 패턴은 하나의 Future든 여러 개든 동일하게 동작합니다.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**출력 예시**: 각 파일 경로 뒤에 추출된 순수 텍스트가 표시됩니다. PDF의 경우 `result.text`에 모든 페이지 텍스트가 연결되어 들어 있습니다.

### 예상 출력 (예시)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

문자 누락이 보이면 설정한 언어가 문서 언어와 일치하는지 다시 확인하고, 엔진에 전달하기 전에 이미지를 전처리(디스큐, 대비 증가)하는 것을 고려하세요.

## 엣지 케이스 및 흔히 발생하는 함정 처리

| 상황 | 해결 방법 |
|-----------|------------|
| **혼합 언어** | 먼저 언어 감지(pass)를 수행한 뒤, 언어별로 별도 엔진을 인스턴스화합니다. |
| **대용량 PDF (> 100 MB)** | `PyPDF2` 등으로 PDF를 페이지 단위 파일로 분할하고 각각을 별도 엔트리로 전달합니다. |
| **비라틴 문자** | OCR 라이브러리에 해당 언어 팩이 포함되어 있는지 확인합니다; 일부 라이브러리는 추가 데이터 파일을 다운로드해야 합니다. |
| **성능 병목** | 스레드 풀 크기를 늘리세요(`engine.set_thread_pool_size(8)`) 또는 GPU 가속 백엔드가 있으면 전환합니다. |
| **저해상도 이미지에서 텍스트 누락** | OpenCV로 전처리: `cv2.resize`, `cv2.threshold`, `cv2.medianBlur` 등을 사용해 가독성을 높입니다. |

## 전체 작동 예제 (복사‑붙여넣기 가능)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

위 코드를 `extract_text_async.py` 파일로 저장하고, `YOUR_DIRECTORY`를 파일이 있는 경로로 바꾸고, OCR 패키지를 설치(`pip install your-ocr-lib`)한 뒤 `python extract_text_async.py`를 실행하세요. 앞서 보여드린 콘솔 출력이 나타날 것입니다.

## 다음 단계 – 기본 추출을 넘어서는 활용

- **후처리**: 불필요한 공백 제거, 유니코드 정규화(`unicodedata.normalize`), 혹은 맞춤법 검사기로 OCR 노이즈 정리  
- **구조화된 출력**: 결과를 CSV, JSON, 혹은 직접 데이터베이스에 저장해 다운스트림 검색에 활용  
- **병렬 배치**: 수백 개 파일이 있다면 여러 Future를 띄우고 큐를 사용해 CPU를 지속적으로 활용하되 메모리 과부하를 방지  
- **웹 프레임워크와 통합**: Flask 또는 FastAPI 엔드포인트에 스크립트를 연결해 온디맨드 OCR 서비스를 제공  

---

### TL;DR

이제 **이미지 PDF에서 텍스트를 추출**하는 최소한의 Python 스크립트를 사용해 OCR을 비동기적으로 실행하고, **스캔된 문서를 텍스트로 변환**하면서 프로그램이 응답성을 유지하는 방법을 알게 되었습니다. 언어 설정, 배치 크기, 전처리 기법을 조정해 정확도를 최대한 끌어올려 보세요.

특별히 공유하고 싶은 팁—예를 들어 손글씨 노트 OCR이나 클라우드 기반 서비스—이 있다면 댓글로 알려 주세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?


다음 튜토리얼들은 이 가이드에서 소개한 기술을 기반으로 하며, 관련 주제를 깊이 있게 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 도와줍니다.

- [Aspose OCR으로 이미지에서 텍스트 추출 – 단계별 가이드](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [폴더에서 OCR 작업으로 이미지에서 텍스트 추출](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR으로 이미지에서 텍스트 추출 – 허용 문자 지정](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-04-26
description: Python에서 OCR용 이미지를 로드하기 위해 스레딩을 사용하는 방법. 콜백, 백그라운드 스레드 및 이미지 로딩을 활용한
  비동기 OCR 처리를 몇 단계만에 배워보세요.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: ko
og_description: Python에서 OCR을 위해 이미지를 로드할 때 스레딩을 사용하는 방법. 이 가이드는 콜백 및 백그라운드 실행이 포함된
  완전하고 실행 가능한 예제를 보여줍니다.
og_title: OCR를 위해 이미지를 로드할 때 스레딩을 사용하는 방법
tags:
- Python
- Threading
- OCR
- Image Processing
title: OCR을 위해 이미지를 로드할 때 스레딩을 사용하는 방법
url: /ko/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 스레딩을 사용하여 OCR용 이미지 로드하는 방법

앱이 멈추지 않게 **스레딩을 사용하여** OCR용 이미지를 로드하는 방법이 궁금하셨나요? 데스크톱 스캐너를 만들든, 웹 서비스를 구축하든, 대용량 사진을 처리하는 간단한 스크립트를 작성하든 언제든 나타나는 상황입니다. 좋은 소식은? 몇 줄의 Python 코드와 올바른 스레딩 패턴만 있으면 OCR 엔진이 작업을 수행하는 동안 UI를 부드럽게 유지할 수 있다는 것입니다.

이 튜토리얼에서는 전체 엔드‑투‑엔드 예제를 단계별로 살펴봅니다: 큰 PNG 파일을 로드하고, 백그라운드 스레드에서 OCR을 시작하며, 콜백으로 결과를 처리합니다. 끝까지 따라오시면 **스레딩을 사용하는 방법**뿐만 아니라 **OCR용 이미지를 로드하는 방법**을 깔끔하고 재사용 가능한 방식으로 익히게 됩니다.

## 필요 사항

- Python 3.9+ (우리가 사용하는 문법은 최신 버전이면 모두 동작합니다)
- `pillow` 이미지 처리용 (`pip install pillow`)
- `pytesseract` Tesseract OCR의 얇은 래퍼 (`pip install pytesseract`)
- 머신에 설치된 Tesseract OCR 엔진 (다운로드: [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- 처리하려는 큰 이미지 파일 (`large_image.png` 예시)

추가 프레임워크 없이, async/await 없이—클래식 `threading`과 콜백만 사용합니다.

## 단계 1: 백그라운드 실행을 위한 Threading 모듈 가져오기

먼저 `threading` 모듈을 가져옵니다. 이 모듈은 `Thread` 클래스를 제공해, 어떤 함수든 별도의 OS 스레드에서 실행할 수 있게 해줍니다.

```python
import threading
```

*Why this matters*: 메인 스레드에서 OCR을 실행하면 프로그램(특히 GUI)이 OCR이 끝날 때까지 멈춥니다. 작업을 백그라운드 스레드에 위임하면 메인 스레드는 UI 업데이트, 사용자 입력 처리, 혹은 다른 작업을 계속 수행할 수 있습니다.

## 단계 2: OCR이 완료될 때 호출되는 콜백 정의하기

콜백은 작업이 끝났을 때 다른 코드가 호출하는 함수입니다. 여기서는 인식된 텍스트를 출력하지만, 저장하거나 네트워크로 전송하거나 UI 위젯을 업데이트할 수도 있습니다.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Pro tip*: 콜백은 가볍게 유지하세요. 콜백 내부에서 무거운 처리를 하면 스레딩의 의미가 사라집니다. 여전히 콜백을 호출한 스레드(보통 메인 스레드)를 차단하게 되기 때문입니다.

## 단계 3: 처리할 이미지 로드하기

이미지 로드는 OCR과 별개의 작업이지만 전체 워크플로의 일부입니다. Pillow를 사용하면 매우 간단합니다.

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Why we do it here*: 이미지가 거대하면 메인 스레드에서 로드하는 것만으로도 지연이 발생할 수 있습니다. 실제 앱에서는 로딩도 스레드에 넘기지만, 여기서는 이해를 돕기 위해 동기식으로 유지합니다.

## 단계 4: 작은 OCR 엔진 래퍼 만들기

원본 예제는 `engine.process_async`를 사용했습니다. 여기서는 내부에서 스레드를 시작하고 작업이 끝나면 전달된 콜백을 호출하는 작은 클래스로 이를 흉내냅니다.

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Explanation*:  
- `_run_ocr`가 실제 OCR 작업을 수행합니다.  
- `process_async`는 `Thread` 객체를 만들고, 데몬으로 설정(스레드가 아직 실행 중이어도 인터프리터가 종료될 수 있도록)한 뒤 시작합니다.  
- 콜백은 OCR 텍스트 또는 오류 메시지를 받게 됩니다.

## 단계 5: 모든 것을 연결하고 OCR이 실행되는 동안 다른 작업 수행하기

이제 전체 흐름을 조정합니다: 이미지를 로드하고, 엔진을 인스턴스화하고, 비동기 OCR을 시작한 뒤, 메인 스레드에서는 다른 작업(여기서는 메시지 출력)을 수행합니다.

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**예상 출력 (간략히 표시):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

OCR이 실패하면 콜백이 텍스트 대신 오류 메시지를 출력합니다.

---

## 왜 이 접근 방식이 단순 루프보다 더 나은가

- **Responsiveness**: 메인 스레드가 OCR 호출에 절대 블록되지 않으므로, 큰 이미지에 대해 몇 초가 걸리더라도 UI가 멈추지 않습니다.  
- **Scalability**: 여러 `SimpleOcrEngine` 인스턴스를 각각 별도 스레드에서 실행해 이미지 배치를 동시에 처리할 수 있습니다.  
- **Separation of Concerns**: 로딩, 처리, 결과 핸들링이 명확히 분리돼 코드 테스트와 유지보수가 쉬워집니다.

## 흔히 발생하는 실수와 회피 방법

| Pitfall | What Happens | Fix |
|---------|--------------|-----|
| Forgetting to mark the thread as *daemon* | 메인 작업이 끝난 뒤에도 OCR 스레드가 살아 있어 스크립트가 종료되지 않습니다. | `worker.daemon = True` **또는** 종료 전에 `join()` 호출 |
| Using a global variable for the result without locks | 여러 스레드가 동시에 쓰면 데이터가 손상될 수 있는 레이스 컨디션이 발생합니다. | 콜백을 통해 결과 전달(예시와 같이)하거나 `queue.Queue` 같은 스레드‑안전 컨테이너 사용 |
| Loading a massive image on the main thread | 백그라운드 OCR이 시작되기 전 UI가 멈춥니다. | 이미지 로딩도 스레드에 넘기거나 지연 로딩 기법 사용 |
| Not handling exceptions inside the worker thread | 예외가 잡히지 않으면 스레드가 조용히 죽고 결과를 받지 못합니다. | OCR 로직을 `try/except`로 감싸고 오류를 콜백으로 전달 |

## 이 패턴 확장하기

- **Progress Reporting**: 공유 `queue.Queue`를 사용해 OCR 스레드에서 중간 진행률(퍼센트)을 메인 스레드로 푸시합니다.  
- **Thread Pool**: 배치 처리 시 개별 `Thread` 대신 `concurrent.futures.ThreadPoolExecutor`를 사용해 스레드 풀을 구성합니다.  
- **GUI Integration**: Tkinter 또는 PyQt 앱에서는 `after()`(Tkinter) 혹은 `QTimer.singleShot`(Qt)으로 콜백을 스케줄해 UI 업데이트가 메인 스레드에서 이루어지도록 합니다.

## 전체 작동 예제 (복사‑붙여넣기 가능)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
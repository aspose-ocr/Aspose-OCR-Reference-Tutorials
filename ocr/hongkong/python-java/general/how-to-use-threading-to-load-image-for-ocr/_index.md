---
category: general
date: 2026-04-26
description: 如何在 Python 中使用執行緒載入影像以進行 OCR。只需幾個步驟，即可學習使用回呼、背景執行緒和影像載入的非同步 OCR 處理。
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: zh-hant
og_description: 如何在 Python 中使用執行緒載入影像以進行 OCR。本指南展示了一個完整、可執行的範例，包含回呼函式與背景執行。
og_title: 如何使用執行緒載入影像以進行 OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: 如何使用執行緒載入圖像以進行光學字符辨識
url: /zh-hant/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用執行緒載入影像以進行 OCR

有沒有想過 **如何使用執行緒** 來載入影像以進行 OCR，而不會凍結你的應用程式？這種情況無論你是在開發桌面掃描器、網路服務，或是處理大量圖片的簡單腳本，都會出現。好消息是？只要幾行 Python 程式碼加上正確的執行緒模式，就能在 OCR 引擎運作時保持 UI 的流暢。

在本教學中，我們將一步步示範完整的端對端範例：載入大型 PNG、在背景執行緒上啟動 OCR，並以回呼函式處理結果。完成後，你不僅會了解 **如何使用執行緒**，還會掌握 **如何載入影像以進行 OCR** 的乾淨且可重用方式。

## 需要的環境

- Python 3.9+（我們使用的語法在任何近期版本皆可運作）
- `pillow` 用於影像處理（`pip install pillow`）
- `pytesseract` 作為 Tesseract OCR 的輕量封裝（`pip install pytesseract`）
- 在你的機器上安裝 Tesseract OCR 引擎（從 [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract) 下載）
- 一個你想處理的大型影像檔案（本教學中的 `large_image.png`）

不需要額外框架，也不使用 async/await——只要傳統的 `threading` 與回呼函式即可。

## 步驟 1：匯入 Threading 模組（背景執行所必需）

首先，我們匯入 `threading` 模組。它提供了 `Thread` 類別，讓我們能在獨立的作業系統執行緒中執行任意函式。

```python
import threading
```

*為什麼這很重要*：如果在主執行緒上執行 OCR，程式（尤其是 GUI）會在 OCR 完成前凍結。將工作委派給背景執行緒後，主執行緒即可自由更新 UI、處理使用者輸入，或啟動其他任務。

## 步驟 2：定義 OCR 完成時會被呼叫的回呼函式

回呼函式就是在另一段程式碼完成時被呼叫的函式。此處我們會印出辨識出的文字，但你也可以將其儲存、傳送至網路，或更新 UI 元件。

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*小技巧*：保持回呼函式輕量。若在回呼內執行大量處理，會抵消執行緒的效益，因為仍會阻塞呼叫它的執行緒（通常是主執行緒）。

## 步驟 3：載入要處理的影像

載入影像與 OCR 本身是分開的工作，但仍屬於整體流程的一部份。使用 Pillow 可以輕鬆完成。

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

*為什麼在此載入*：若影像非常大，在主執行緒載入可能已經造成卡頓。實務上許多應用會將載入工作也交給執行緒，但為了說明清楚，我們在此保持同步執行。

## 步驟 4：建立簡易的 OCR 引擎包裝類別

原始範例使用 `engine.process_async`。我們將以一個小型類別模擬此行為，內部會啟動執行緒，並在完成時呼叫提供的回呼函式。

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

*說明*：  
- `_run_ocr` 負責執行繁重的 OCR 工作。  
- `process_async` 會建立 `Thread` 物件，將其設為 daemon（即使執行緒仍在執行，直譯器也能正常退出），並啟動它。  
- 回呼函式會收到 OCR 文字或錯誤訊息。

## 步驟 5：將所有步驟串接起來，並在 OCR 執行期間處理其他工作

現在我們把整個流程串起來：載入影像、實例化引擎、觸發非同步 OCR，並讓主執行緒在 OCR 執行期間繼續做其他事（此處僅示範印出訊息）。

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

**預期輸出（為簡潔起見已截斷）**：

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

如果 OCR 失敗，回呼函式會印出錯誤訊息而非文字。

---

## 為什麼此方法較單純迴圈更有效

- **Responsiveness**：主執行緒不會因 OCR 呼叫而阻塞，對於大型影像可能需要數秒的處理時間。
- **Scalability**：可以同時啟動多個 `SimpleOcrEngine` 實例，各自於獨立執行緒處理批次影像。
- **Separation of Concerns**：載入、處理與結果處理明確分離，使程式碼更易測試與維護。

## 常見陷阱與避免方法

| 陷阱 | 會發生什麼 | 解決方法 |
|------|------------|----------|
| 忘記將執行緒標記為 *daemon* | 主工作完成後腳本仍會掛住，因為 OCR 執行緒仍在執行。 | 設定 `worker.daemon = True` **或** 在結束前 `join()` 執行緒。 |
| 使用全域變數儲存結果卻未加鎖 | 多執行緒同時寫入時可能產生競爭條件，導致資料損壞。 | 透過回呼傳遞結果（如本範例），或使用像 `queue.Queue` 這樣的執行緒安全容器。 |
| 在主執行緒載入巨量影像 | UI 在背景 OCR 開始前就已凍結。 | 同樣將載入工作交給執行緒，或使用延遲載入技術。 |
| 未在工作執行緒內處理例外 | 未捕獲的例外會悄悄終止執行緒，導致沒有結果。 | 在 OCR 邏輯外層加上 `try/except`，並將錯誤傳遞給回呼函式。 |

## 擴充此模式

- **進度回報**：使用共享的 `queue.Queue`，將 OCR 執行緒的中間進度百分比推送至主執行緒。
- **執行緒池**：針對批次處理時，將單一 `Thread` 物件改為 `concurrent.futures.ThreadPoolExecutor`。
- **GUI 整合**：在 Tkinter 或 PyQt 應用中，使用 `after()`（Tkinter）或 `QTimer.singleShot`（Qt）排程回呼，以確保 UI 更新發生在主執行緒。

## 完整可執行範例（直接複製貼上）

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
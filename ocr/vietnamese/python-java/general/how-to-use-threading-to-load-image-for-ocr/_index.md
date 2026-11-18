---
category: general
date: 2026-04-26
description: Cách sử dụng threading để tải ảnh cho OCR trong Python. Học xử lý OCR
  bất đồng bộ với callbacks, các luồng nền và tải ảnh chỉ trong vài bước.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: vi
og_description: Cách sử dụng threading để tải ảnh cho OCR trong Python. Hướng dẫn
  này trình bày một ví dụ đầy đủ, có thể chạy được với các callback và thực thi nền.
og_title: Cách sử dụng đa luồng để tải ảnh cho OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: Cách sử dụng đa luồng để tải ảnh cho OCR
url: /vi/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng Threading Để Tải Ảnh Cho OCR

Bạn có bao giờ tự hỏi **cách sử dụng threading** để tải ảnh cho OCR mà không làm treo ứng dụng của mình không? Đây là một tình huống thường gặp dù bạn đang xây dựng một máy quét desktop, một dịch vụ web, hay một script đơn giản xử lý hàng loạt hình ảnh lớn. Tin tốt là gì? Chỉ cần vài dòng Python và mẫu threading phù hợp, giao diện người dùng của bạn sẽ luôn phản hồi nhanh trong khi engine OCR thực hiện công việc của nó.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, từ đầu đến cuối: tải một tệp PNG lớn, khởi chạy OCR trên một luồng nền, và xử lý kết quả bằng một callback. Khi kết thúc, bạn sẽ không chỉ biết **cách sử dụng threading** mà còn biết **cách tải ảnh cho OCR** một cách sạch sẽ và tái sử dụng.

## Những Gì Bạn Cần

- Python 3.9+ (cú pháp chúng tôi dùng hoạt động trên bất kỳ phiên bản mới nào)
- `pillow` để xử lý ảnh (`pip install pillow`)
- `pytesseract` là một wrapper nhẹ quanh Tesseract OCR (`pip install pytesseract`)
- Engine Tesseract OCR được cài đặt trên máy của bạn (tải về từ [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- Một tệp ảnh lớn mà bạn muốn xử lý (`large_image.png` trong hướng dẫn này)

Không cần framework bổ sung, không async/await—chỉ cần `threading` cổ điển và một callback.

## Bước 1: Nhập Module Threading (Cần Thiết Cho Thực Thi Nền)

Điều đầu tiên chúng ta làm là nhập module `threading`. Nó cung cấp lớp `Thread`, cho phép chúng ta chạy bất kỳ hàm nào trong một luồng OS riêng biệt.

```python
import threading
```

*Tại sao điều này quan trọng*: Nếu bạn chạy OCR trên luồng chính, chương trình của bạn (đặc biệt là GUI) sẽ bị treo cho đến khi OCR hoàn thành. Bằng cách giao công việc cho một luồng nền, luồng chính vẫn tự do cập nhật UI, xử lý nhập liệu người dùng, hoặc khởi chạy các tác vụ khác.

## Bước 2: Định Nghĩa Callback Sẽ Được Gọi Khi OCR Hoàn Thành

Callback chỉ đơn giản là một hàm mà một đoạn mã khác gọi khi nó hoàn thành. Ở đây chúng ta sẽ in ra văn bản đã nhận dạng, nhưng bạn cũng có thể lưu nó, gửi qua mạng, hoặc cập nhật một widget UI.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Mẹo chuyên nghiệp*: Giữ callback nhẹ. Xử lý nặng trong callback làm mất mục đích của threading vì nó vẫn sẽ chặn luồng đã gọi (thường là luồng chính).

## Bước 3: Tải Ảnh Bạn Muốn Xử Lý

Việc tải ảnh là một mối quan tâm riêng biệt so với OCR, nhưng vẫn là một phần của quy trình tổng thể. Sử dụng Pillow làm cho việc này trở nên đơn giản.

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

*Tại sao chúng ta làm việc này ở đây*: Nếu ảnh quá lớn, việc tải nó trên luồng chính có thể gây giật. Trong nhiều ứng dụng thực tế, bạn cũng sẽ chuyển tải ảnh sang một luồng, nhưng để rõ ràng chúng ta giữ nó đồng bộ.

## Bước 4: Tạo Một Wrapper Nhỏ Cho Engine OCR

Đoạn mã gốc sử dụng `engine.process_async`. Chúng ta sẽ mô phỏng điều đó bằng một lớp nhỏ khởi tạo một luồng bên trong và gọi callback đã cung cấp khi hoàn thành.

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

*Giải thích*:  
- `_run_ocr` thực hiện công việc nặng.  
- `process_async` tạo một đối tượng `Thread`, đánh dấu nó là daemon (để trình thông dịch có thể thoát ngay cả khi luồng vẫn đang chạy), và khởi chạy nó.  
- Callback nhận hoặc là văn bản OCR hoặc là thông báo lỗi.

## Bước 5: Kết Hợp Tất Cả Và Thực Hiện Các Công Việc Khác Khi OCR Đang Chạy

Bây giờ chúng ta điều phối toàn bộ quy trình: tải ảnh, khởi tạo engine, khởi chạy OCR bất đồng bộ, và giữ luồng chính bận với một việc khác (ở đây chúng ta chỉ in một thông báo).

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

**Kết quả mong đợi (được rút gọn để ngắn gọn):**

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

Nếu OCR thất bại, callback sẽ in ra thông báo lỗi thay vì văn bản.

---

## Tại Sao Cách Tiếp Cận Này Hoạt Động Tốt Hơn So Với Vòng Lặp Đơn Giản

- **Độ phản hồi**: Luồng chính không bao giờ bị chặn khi gọi OCR, việc này có thể mất vài giây đối với ảnh lớn.
- **Khả năng mở rộng**: Bạn có thể khởi tạo nhiều instance của `SimpleOcrEngine`, mỗi cái trên một luồng riêng, để xử lý đồng thời một loạt ảnh.
- **Tách biệt các mối quan tâm**: Việc tải, xử lý và xử lý kết quả được tách biệt rõ ràng, giúp mã dễ kiểm thử và bảo trì hơn.

## Những Cạm Bẫy Thường Gặp và Cách Tránh

| Cạm bẫy | Điều gì xảy ra | Cách khắc phục |
|---------|----------------|----------------|
| Quên đánh dấu luồng là *daemon* | Script bị treo sau khi công việc chính hoàn thành vì luồng OCR vẫn còn hoạt động. | Đặt `worker.daemon = True` **hoặc** `join()` luồng trước khi thoát. |
| Sử dụng biến toàn cục để lưu kết quả mà không có khóa | Các điều kiện race có thể làm hỏng dữ liệu khi nhiều luồng ghi đồng thời. | Truyền kết quả qua callback (như chúng ta làm) hoặc sử dụng các container an toàn với luồng như `queue.Queue`. |
| Tải ảnh khổng lồ trên luồng chính | UI bị treo trước khi OCR nền bắt đầu. | Chuyển tải ảnh sang một luồng khác, hoặc sử dụng kỹ thuật tải lười (lazy loading). |
| Không xử lý ngoại lệ bên trong luồng worker | Các ngoại lệ không được bắt sẽ giết luồng một cách im lặng, khiến bạn không nhận được kết quả. | Bao bọc logic OCR trong `try/except` và chuyển lỗi tới callback. |

## Mở Rộng Mô Hình Này

- **Báo cáo tiến độ**: Sử dụng một `queue.Queue` chia sẻ để đẩy các phần trăm tiến độ trung gian từ luồng OCR tới luồng chính.
- **Thread Pool**: Đối với xử lý batch, thay thế các đối tượng `Thread` riêng lẻ bằng `concurrent.futures.ThreadPoolExecutor`.
- **Tích hợp GUI**: Trong ứng dụng Tkinter hoặc PyQt, lên lịch callback bằng `after()` (Tkinter) hoặc `QTimer.singleShot` (Qt) để đảm bảo cập nhật UI diễn ra trên luồng chính.

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

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
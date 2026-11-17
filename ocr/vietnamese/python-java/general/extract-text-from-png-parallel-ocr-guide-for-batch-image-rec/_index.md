---
category: general
date: 2026-03-18
description: Trích xuất văn bản từ PNG bằng Python và Aspose OCR. Tìm hiểu cách tải
  ảnh cho OCR, chạy OCR trên nhiều tệp và thực hiện OCR hàng loạt ảnh với nhận dạng
  ảnh song song.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: vi
og_description: Trích xuất văn bản từ PNG bằng Aspose OCR trong Python. Hướng dẫn
  này cho thấy cách tải hình ảnh để OCR, xử lý OCR nhiều tệp và chạy OCR hàng loạt
  các hình ảnh bằng nhận dạng hình ảnh song song.
og_title: Trích xuất văn bản từ PNG – Hướng dẫn OCR song song
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Trích xuất văn bản từ PNG – Hướng dẫn OCR song song cho nhận dạng ảnh hàng
  loạt
url: /vi/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ PNG – Hướng dẫn OCR Song song cho Nhận dạng Hình ảnh Hàng loạt

Bạn đã bao giờ cần **trích xuất văn bản từ các tệp PNG** nhưng lại cảm thấy chậm chạp khi một hình ảnh mất rất nhiều thời gian để xử lý? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế—như máy quét hoá đơn, công cụ số hoá biên lai, hoặc các công cụ lưu trữ—tốc độ rất quan trọng, và việc xử lý từng PNG một cách tuần tự sẽ không đáp ứng được nhu cầu.  

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh, sẵn sàng chạy, **tải ảnh để OCR**, thực hiện **ocr multiple files** theo kiểu **batch OCR images**, và tận dụng **parallel image recognition** bằng mô-đun `threading` của Python. Khi hoàn thành, bạn sẽ có một script có thể lấy văn bản từ bất kỳ số lượng PNG nào trong vài giây, chứ không phải phút.

## Những gì bạn cần

- Python 3.8 hoặc mới hơn (cú pháp được hiển thị cũng hoạt động trên 3.10+).  
- Gói Aspose OCR cho Java/​Python (`aspose-ocr`). Bạn có thể cài đặt nó bằng `pip`.  
- Một thư mục chứa một vài tệp PNG mà bạn muốn xử lý.  
- Một lượng RAM vừa phải—mỗi luồng giữ một thể hiện nhỏ của engine OCR, vì vậy ngay cả một laptop cũng có thể khởi chạy hàng chục worker.

Không cần dịch vụ bên ngoài, không cần khóa cloud, và không có tệp cấu hình bí ẩn. Chỉ cần mã Python thuần túy mà bạn có thể sao chép‑dán và chạy.

## Tại sao cần trích xuất văn bản từ PNG một cách song song?

Xử lý một PNG là công việc phụ thuộc vào CPU: engine OCR chạy một loạt thuật toán phân tích ảnh để xử lý dữ liệu pixel. Khi bạn có mười, hai mươi, hoặc một trăm hình ảnh, thời gian chạy tổng cộng thực chất là tổng của mỗi lần chạy riêng lẻ.  

Bằng cách tạo một luồng cho mỗi tệp, chúng ta cho phép hệ điều hành lên lịch các công việc nặng CPU này đồng thời. Trên máy đa nhân, điều này thường giảm một nửa—hoặc thậm chí giảm tới một phần tư—thời gian thực tế. Nhược điểm là mức tiêu thụ bộ nhớ hơi cao hơn, nhưng đối với hầu hết các công việc batch, tốc độ tăng lên đáng giá.

> **Pro tip:** Nếu bạn đang xử lý hàng trăm megabyte ảnh, hãy cân nhắc sử dụng `concurrent.futures.ProcessPoolExecutor` thay vì `threading`. Các process cung cấp khả năng song song thực sự trên trình thông dịch CPython bị ràng buộc bởi GIL, tuy nhiên sẽ tốn thêm một chút overhead.

## Bước 1: Cài đặt Aspose OCR cho Python

Đầu tiên, hãy đưa thư viện OCR vào hệ thống của bạn.

```bash
pip install aspose-ocr
```

Dòng lệnh duy nhất này sẽ tải về các binary mới nhất của Aspose OCR và các binding Python của nó. Nếu gặp lỗi quyền, hãy thử thêm `--user` hoặc sử dụng môi trường ảo.

## Bước 2: Tải ảnh để OCR – hàm worker

Bây giờ chúng ta định nghĩa routine cốt lõi sẽ được thực thi trong mỗi luồng. Nó **tải ảnh để OCR**, chạy nhận dạng, và in ra một bản xem trước của văn bản đã trích xuất.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Một vài lưu ý:

- **Tại sao mỗi luồng lại tạo một `OcrEngine` mới?** Engine giữ các bộ đệm nội bộ; việc chia sẻ một thể hiện sẽ gây ra race condition và kết quả rối loạn.  
- **Tại sao loại bỏ ký tự xuống dòng?** Khi ghi log ra console, việc này giúp dòng chữ gọn gàng.  
- **Xử lý lỗi?** Trong môi trường production, bạn nên bọc phần thân trong một `try/except` và có thể ghi log vào file—điều chúng ta sẽ đề cập sau.

## Bước 3: Liệt kê các tệp PNG bạn muốn xử lý

Bạn có thể hard‑code danh sách, nhưng cách linh hoạt hơn là quét một thư mục. Dưới đây chúng tôi liệt kê thủ công ba tệp để minh họa; hãy thay đổi các đường dẫn thành thư mục của bạn.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Nếu bạn muốn tự động phát hiện:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Thay đổi nhỏ này cho phép bạn **extract text from PNG** hàng loạt mà không cần chỉnh sửa mã nguồn mỗi lần.

## Bước 4: Thiết lập ocr multiple files với batch OCR images

Bây giờ chúng ta tạo một luồng cho mỗi ảnh. Đây là phần cốt lõi của mẫu **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

List comprehension giúp mã ngắn gọn, và mỗi đối tượng `Thread` lưu trữ hàm mục tiêu và đối số (`image_path`).  

> **Side note:** Mô-đun `threading` của Python sử dụng các luồng OS gốc, vì vậy trên một laptop 4‑core bạn thường sẽ thấy tối đa bốn luồng thực sự chạy đồng thời; các luồng còn lại sẽ được lên lịch khi các core trở nên rảnh.

## Bước 5: Chạy nhận dạng ảnh song song

Khởi chạy các worker rất đơn giản: duyệt danh sách và gọi `start()`. Sau đó chúng ta chờ mọi luồng hoàn thành bằng `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Khi script kết thúc, bạn sẽ thấy một loạt các dòng như:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Kết quả này xác nhận mỗi PNG đã được xử lý và văn bản đã trích xuất sẵn sàng cho các bước tiếp theo (ví dụ: lưu vào cơ sở dữ liệu hoặc đưa vào pipeline NLP).

## Bước 6: Kiểm tra kết quả và xử lý các trường hợp đặc biệt

### Kiểm tra kết quả rỗng

Đôi khi ảnh quá nhiễu, hoặc engine OCR không phát hiện được ký tự nào. Một kiểm tra nhanh có thể ngăn ngừa lỗi ở các bước sau.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Giới hạn số luồng đồng thời

Nếu bạn chạy trên một VM tài nguyên hạn chế, việc tạo ra hàng trăm luồng có thể làm quá tải scheduler. Bạn có thể giới hạn độ đồng thời bằng semaphore:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Lưu kết quả vào file

Thay vì in ra console, bạn có thể muốn một file CSV chứa tên tệp và văn bản đã trích xuất:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Hãy chắc chắn mở CSV **một lần** bên ngoài hàm worker để tránh race condition; đối tượng writer của mô-đun `csv` là thread‑safe cho các ghi đơn giản.

## Ví dụ Hoạt động Đầy đủ

Kết hợp mọi thứ lại, dưới đây là một script duy nhất mà bạn có thể lưu thành file `batch_ocr.py` và chạy:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
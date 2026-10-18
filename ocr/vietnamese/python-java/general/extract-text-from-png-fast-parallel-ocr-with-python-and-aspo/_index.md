---
category: general
date: 2026-03-28
description: Trích xuất văn bản từ PNG nhanh chóng bằng Aspose OCR trong Python. Học
  cách chuyển đổi văn bản của các trang quét bằng nhận dạng hình ảnh song song trong
  Python để đạt hiệu suất cao.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: vi
og_description: Trích xuất văn bản từ PNG nhanh chóng bằng Aspose OCR trong Python.
  Hướng dẫn này cho thấy cách chuyển đổi văn bản của các trang quét bằng nhận dạng
  hình ảnh song song trong Python, mang lại kết quả tốc độ cao.
og_title: Trích xuất văn bản từ PNG – OCR nhanh song song bằng Python
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Trích xuất văn bản từ PNG – OCR song song nhanh bằng Python và Aspose
url: /vi/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ PNG – OCR Song song Nhanh với Python

Bạn đã bao giờ cần **extract text from PNG** nhưng lại thấy OCR đơn luồng chậm chạp? Bạn không phải là người duy nhất. Dù bạn đang số hoá một đống biên lai đã quét hoặc chuyển các slide bài giảng thành PDF có thể tìm kiếm, nút thắt thường là bước OCR itself.  

Trong hướng dẫn này, chúng tôi sẽ cho bạn thấy một giải pháp hoàn chỉnh, sẵn sàng chạy mà **converts scanned pages text** song song, sử dụng chế độ batch bất đồng bộ của Aspose OCR cùng với `ThreadPoolExecutor` của Python. Khi kết thúc, bạn sẽ có thể **recognize image text python**‑style, xử lý hàng chục hình ảnh trong một phần nhỏ thời gian so với một vòng lặp đơn giản.

> **Bạn sẽ nhận được**  
> * Một script hoạt động đầy đủ có thể trích xuất văn bản từ ảnh PNG một cách đồng thời.  
> * Hiểu vì sao chế độ batch bất đồng bộ tăng tốc.  
> * Mẹo để mở rộng giải pháp cho khối lượng công việc lớn hơn.

## Những gì bạn cần

| Yêu cầu | Lý do |
|--------------|--------|
| Python 3.9+ | Cú pháp hiện đại và gợi ý kiểu. |
| `aspose-ocr` and `aspose-storage` packages | Cung cấp engine OCR và bộ tải ảnh. |
| A folder of PNG files (e.g., scanned pages) | Thư mục chứa các tệp PNG (ví dụ: các trang đã quét) |
| Basic knowledge of Python concurrency | Kiến thức cơ bản về đồng thời trong Python; có ích nhưng không bắt buộc; chúng tôi sẽ giải thích mọi thứ. |

Bạn có thể cài đặt các thư viện Aspose bằng:

```bash
pip install aspose-ocr aspose-storage
```

> **Mẹo chuyên nghiệp:** Giữ các gói của bạn luôn cập nhật (`pip list --outdated`) để hưởng lợi từ các cải tiến hiệu năng mới nhất.

## Bước 1: Khởi tạo Engine Aspose OCR ở chế độ Batch Bất đồng bộ

Điều đầu tiên chúng ta làm là tạo một thể hiện `OcrEngine` và chuyển nó sang **asynchronous batch mode**. Chế độ này xếp hàng các yêu cầu nhận dạng nội bộ, cho phép engine xử lý nhiều hình ảnh mà không chặn luồng Python của bạn.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Tại sao async?*  
Khi bạn gọi `recognize` ở chế độ đồng bộ, lời gọi sẽ chặn cho đến khi hình ảnh được xử lý hoàn toàn. Trong chế độ async, engine có thể bắt đầu làm việc với hình ảnh tiếp theo trong khi hình ảnh hiện tại vẫn đang được giải mã, thực hiện việc chồng chéo I/O và công việc CPU.

## Bước 2: Liệt kê các tệp PNG bạn muốn xử lý

Ở đây chúng ta định nghĩa tập hợp các hình ảnh. Trong một dự án thực tế, bạn có thể tạo danh sách này một cách động (ví dụ, `glob.glob("*.png")`), nhưng việc giữ nó rõ ràng giúp ví dụ dễ theo dõi.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Lưu ý:** Thay `YOUR_DIRECTORY` bằng đường dẫn thực tế nơi các bản quét PNG của bạn nằm. Nếu bạn có hàng trăm tệp, hãy cân nhắc sử dụng `os.listdir` và lọc các tệp `.png`.

## Bước 3: Viết một hàm trợ giúp để tải ảnh và trả về văn bản của nó

Hàm trợ giúp trừu tượng hoá quá trình hai bước tải tệp qua **Aspose Storage** và sau đó đưa nó vào engine OCR. Thêm một docstring nhỏ giúp hàm tự mô tả—hữu ích cho việc bảo trì sau này.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Tại sao lại có một hàm riêng?*  
Nó giữ cho mã thread‑pool sạch sẽ và cho phép chúng ta tái sử dụng logic ở nơi khác (ví dụ, trong một endpoint Flask). Ngoài ra, tách I/O ra giúp việc gỡ lỗi dễ dàng hơn—nếu một tệp cụ thể gặp lỗi, bạn sẽ thấy tên tệp trong trace của ngoại lệ.

## Bước 4: Chạy Nhận dạng Hình ảnh Song song Python với Thread Pool

Bây giờ chúng ta đưa vào `ThreadPoolExecutor`. Mặc định chúng ta khởi tạo bốn worker, nhưng bạn có thể điều chỉnh `max_workers` dựa trên số lõi CPU và kích thước tập hợp hình ảnh.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Cách thức điều này cung cấp Nhận dạng Hình ảnh Song song Python

* **ThreadPoolExecutor** tạo một pool các luồng worker, mỗi luồng gọi `recognize_image`.  
* Vì engine OCR đang ở chế độ batch bất đồng bộ, mỗi luồng có thể chuyển công việc cho engine trong khi vẫn phản hồi nhanh.  
* `as_completed` trả về các future theo thứ tự hoàn thành, vì vậy bạn nhận được kết quả ngay khi chúng sẵn sàng—lý tưởng cho việc stream các batch lớn.

> **Cạm bẫy phổ biến:** Sử dụng `max_workers=1` làm mất mục đích của song song. Trên máy 8‑core, `max_workers=8` thường cho thông lượng tốt nhất, nhưng hãy thử một vài giá trị để tìm điểm cân bằng cho phần cứng của bạn.

## Bước 5: Xác minh Đầu ra và Xử lý Các Trường hợp Đặc biệt

Khi bạn chạy script, bạn sẽ thấy một khối văn bản cho mỗi PNG, kèm tiền tố là tên tệp của nó:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Nếu bất kỳ hình ảnh nào thất bại (tệp hỏng, định dạng không hỗ trợ), khối `except` sẽ in ra thông báo lỗi hữu ích thay vì làm sập toàn bộ batch.

### Mở rộng Giải pháp

| Kịch bản | Điều chỉnh đề xuất |
|----------|-----------------|
| **Hàng nghìn trang** | Chuyển sang `ProcessPoolExecutor` để tận dụng nhiều tiến trình CPU, hoặc chia danh sách thành các khối và xử lý batch tuần tự. |
| **Các định dạng ảnh khác nhau (JPG, TIFF)** | Phương thức `storage.Image.load` tự động phát hiện định dạng, vì vậy chỉ cần thêm các tệp vào `input_images`. |
| **Cần lưu kết quả** | Ghi `text` vào tệp `.txt` hoặc chèn vào cơ sở dữ liệu trong khối `else`. |
| **Giám sát hiệu năng** | Bao quanh `recognize_image` bằng một bộ hẹn giờ (`time.perf_counter`) và ghi lại thời gian mỗi tệp. |

## Ví dụ Hoạt động Đầy đủ (Sẵn sàng Sao chép‑Dán)

Dưới đây là script hoàn chỉnh, sẵn sàng đưa vào một tệp có tên `parallel_ocr.py`. Không có phần nào bị thiếu—mọi thứ bạn cần đều có ở đây.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Lưu tệp, điều chỉnh placeholder `YOUR_DIRECTORY`, và chạy:

```bash
python parallel_ocr.py
```

Bạn sẽ thấy văn bản đã trích xuất cho mỗi PNG xuất hiện trong console, giống như đã hiển thị trước đó.

## Kết luận

Chúng tôi vừa trình diễn cách **extract text from PNG** một cách hiệu quả bằng cách kết hợp chế độ batch bất đồng bộ của Aspose OCR với `ThreadPoolExecutor` của Python. Script chuyển đổi văn bản các trang đã quét song song, cung cấp cho bạn một cách mở rộng để **recognize image text python**‑style mà không cần viết thread‑pool tùy chỉnh từ đầu.  

Nếu bạn sẵn sàng tiến xa hơn, hãy thử:

* Lưu kết quả vào cơ sở dữ liệu SQLite có thể tìm kiếm.  
* Thêm tiền xử lý ảnh (điều chỉnh góc, giảm nhiễu) với OpenCV trước OCR.  
* Triển khai script như một microservice phía sau endpoint Flask hoặc FastAPI.

Hãy nhớ, chìa khóa để OCR hiệu năng cao không chỉ là một engine nhanh hơn—mà còn là cách cung cấp công việc cho engine sao cho tối đa hoá tính đồng thời. Với mẫu đã trình bày ở đây, bạn có thể xử lý hàng chục hoặc thậm chí hàng trăm bản quét PNG với ít thay đổi mã.

Chúc lập trình vui vẻ, và chúc các PDF của bạn luôn có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-26
description: cách thực hiện OCR hàng loạt hiệu quả bằng Python—học cách trích xuất
  văn bản từ hình ảnh và chuyển đổi OCR PDF với xử lý song song.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: vi
og_description: cách thực hiện OCR hàng loạt hiệu quả—hướng dẫn từng bước để trích
  xuất văn bản từ hình ảnh, chuyển đổi OCR PDF và xử lý OCR hàng loạt bằng Python.
og_title: 'cách thực hiện OCR hàng loạt: trích xuất văn bản nhanh song song'
tags:
- OCR
- Python
- Parallel Computing
title: 'Cách thực hiện OCR hàng loạt: trích xuất văn bản nhanh song song'
url: /vi/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách thực hiện batch ocr: trích xuất văn bản nhanh song song

Bạn đã bao giờ tự hỏi **cách thực hiện batch ocr** khi có hàng chục trang quét, ảnh chụp màn hình và PDF nằm rải rác chưa? Bạn không phải là người duy nhất—hầu hết các nhà phát triển đều gặp cùng một rào cản: xử lý từng tệp một cách tuần tự trở thành một nút thắt gây đau đầu.  

Tin tốt là bạn có thể khởi động một vài luồng worker, đưa tất cả các tệp của mình vào và để engine OCR xử lý batch một cách song song. Trong tutorial này chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho thấy **trích xuất văn bản từ hình ảnh**, thực hiện **pdf ocr conversion**, và tận dụng **parallel ocr processing** để tăng tốc.

> **Bạn sẽ nhận được gì**  
> * Một script Python hoạt động đầy đủ, xử lý danh sách hỗn hợp các tệp PNG, TIFF, PDF và JPG trong một lần chạy.  
> * Hiểu tại sao một thread pool lại tăng tốc các tác vụ OCR phụ thuộc I/O.  
> * Các mẹo xử lý lỗi, PDF lớn, và số lượng thread tùy chỉnh.  

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

| Requirement | Reason |
|-------------|--------|
| Python 3.8+ | Cú pháp hiện đại & `concurrent.futures` |
| `ocr` library (hoặc bất kỳ wrapper OCR tương thích nào) | Cung cấp `OcrBatchProcessor` và các đối tượng kết quả |
| Một vài tệp mẫu (PNG, TIFF, PDF, JPG) | Để xem **extract text from images** hoạt động |
| Kiến thức cơ bản về threads (tùy chọn) | Hữu ích nhưng không bắt buộc |

Nếu bạn chưa cài đặt gói `ocr`, chạy:

```bash
pip install ocr-lib   # replace with the actual package name
```

Bây giờ môi trường đã sẵn sàng, hãy phân tích vấn đề.

## Step 1: Import helpers and instantiate the batch processor

Điều đầu tiên chúng ta cần là một nơi để thu thập tất cả các job OCR. Lớp `OcrBatchProcessor` làm đúng điều này—nó xếp hàng các mục công việc và trả lại cho bạn một danh sách các đối tượng `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Lý do quan trọng*: Việc import `as_completed` cho phép chúng ta phản hồi ngay khi mỗi job hoàn thành, thay vì chờ tệp chậm nhất. Đây là cốt lõi của **batch ocr processing**.

## Step 2: Tune the worker pool for parallel execution

Mặc định processor có thể chỉ dùng một thread, điều này làm mất mục đích của batching. Chúng ta sẽ yêu cầu bốn worker—có thể tăng số này lên tới số core CPU mà bạn có.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Mẹo chuyên nghiệp*: Đối với các tác vụ I/O‑bound như OCR, bạn thường thấy hiệu suất giảm sau `CPU cores * 2`. Hãy thử một vài giá trị và chọn điểm cân bằng tốt nhất.

## Step 3: Queue every file you want to OCR

Ở đây chúng ta thêm một tập hợp hỗn hợp các tệp ảnh và PDF. Phương thức `add` chỉ ghi lại đường dẫn; công việc thực tế sẽ không bắt đầu cho đến khi chúng ta submit batch.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Nếu bạn cần xử lý toàn bộ thư mục, một vòng lặp `glob` nhanh sẽ làm công việc:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Step 4: Fire off the jobs and collect futures

Gọi `submit_all` sẽ bật “đèn xanh” cho processor. Nó trả về một danh sách các đối tượng `Future`—giống như các placeholder cho kết quả sẽ xuất hiện sau.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

Lúc này engine OCR đang làm việc ở nền, mỗi thread đang “nhai” một tệp.

## Step 5: Pull results as soon as they finish

Sử dụng `as_completed` chúng ta lặp qua các future theo thứ tự hoàn thành, không phải thứ tự submit. Điều này giúp script phản hồi nhanh, đặc biệt khi một số PDF mất thời gian lâu hơn các PNG đơn giản.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Kết quả mong đợi** (rút gọn để ngắn gọn):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Mỗi khối tương ứng với bản đại diện plain‑text của tệp gốc. Nếu bạn đang thực hiện **pdf ocr conversion**, văn bản sẽ bao gồm mọi thứ mà engine OCR có thể giải mã từ mỗi trang.

## Handling Edge Cases & Common Pitfalls

| Situation | What to watch for | Quick fix |
|-----------|-------------------|-----------|
| Ảnh bị hỏng | `future.result()` gây ra `OSError` | Bao bọc trong `try/except` (xem code ở trên) |
| PDF rất lớn ( > 100 MB ) | Áp lực bộ nhớ, thread chậm hơn | Tăng `thread_count` một cách vừa phải hoặc chia PDF thành các chương trước |
| Tài liệu đa ngôn ngữ | Mô hình OCR mặc định có thể nhận dạng sai | Truyền gợi ý ngôn ngữ cho `OcrBatchProcessor` nếu thư viện hỗ trợ |
| Cần giữ bố cục | `get_text()` thông thường mất cột | Dùng `ocr_result.get_hocr()` hoặc phương pháp nhận dạng bố cục tương tự |

### Pro tip: Custom thread count based on file type

Nếu bạn biết phần lớn khối lượng công việc là PDF, bạn có thể cấp nhiều thread hơn cho chúng và ít hơn cho các PNG nhỏ. Một số thư viện cho phép truyền `priority` cho từng job; nếu không, bạn có thể tạo hai batch riêng—một cho ảnh, một cho PDF—and chạy chúng đồng thời.

## Visual Overview (optional)

![how to batch ocr workflow diagram](https://example.com/ocr-workflow.png "how to batch ocr workflow")

*Biểu đồ minh họa luồng từ việc khám phá tệp → tạo batch → thực thi song song → tổng hợp kết quả.*

## Full Script You Can Copy‑Paste

Dưới đây là toàn bộ chương trình, sẵn sàng sao chép vào file `.py`. Nó bao gồm tất cả các đoạn code ở trên, cộng thêm một helper nhỏ tự động khám phá các tệp hỗ trợ trong một thư mục.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Lưu lại dưới tên `batch_ocr.py`, chỉ định thư mục chứa các bản scan của bạn, và xem console hiện ra văn bản đã trích xuất.  

### Why this works

* **Thread pool** – OCR chủ yếu chờ I/O đĩa và các lời gọi engine bên ngoài, vì vậy nhiều thread giúp CPU luôn bận.  
* **`as_completed`** – Bạn nhận được kết quả ngay khi chúng sẵn sàng, lý tưởng cho phản hồi UI hoặc pipeline streaming.  
* **Error isolation** – Một tệp hỏng sẽ không làm sập toàn bộ batch; khối `try/except` cô lập các lỗi.

## Conclusion

Tóm lại, bạn đã biết **cách thực hiện batch ocr** bằng Python `concurrent.futures` kết hợp với một thư viện OCR hỗ trợ batch processing. Bằng cách cấu hình một thread pool vừa phải, xếp hàng mọi tệp hỗ trợ, và lấy kết quả khi chúng hoàn thành, bạn đạt được **parallel ocr processing** nhanh chóng mà không mất độ tin cậy.  

Từ đây bạn có thể:

* Kết nối đầu ra vào một chỉ mục tìm kiếm để truy xuất tài liệu nhanh.  
* Mở rộng script để ghi mỗi kết quả vào file `.txt` bên cạnh tệp gốc.  
* Thay thế thread pool tích hợp bằng `asyncio` nếu thư viện OCR của bạn cung cấp API async.  

Tiếp tục thử nghiệm—thay thế bằng Tesseract, Azure Cognitive Services, hoặc Google Vision, và bạn sẽ thấy cùng một mẫu áp dụng. Chúc bạn OCR vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
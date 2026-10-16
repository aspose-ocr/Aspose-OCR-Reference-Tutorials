---
category: general
date: 2026-06-25
description: Xử lý OCR hàng loạt trong Python trở nên dễ dàng. Học cách trích xuất
  văn bản từ một loạt ảnh và làm chủ việc trích xuất văn bản từ ảnh hàng loạt bằng
  các luồng song song.
draft: false
keywords:
- batch OCR processing
- extract text from image batch
- batch image text extraction
language: vi
og_description: Xử lý OCR hàng loạt trong Python cho phép bạn trích xuất văn bản từ
  các hình ảnh nhanh chóng. Hướng dẫn này sẽ đưa bạn qua quá trình OCR song song với
  các ví dụ mã rõ ràng.
og_title: Xử lý OCR hàng loạt bằng Python – Hướng dẫn toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  headline: Batch OCR Processing in Python – Complete Programming Guide
  type: TechArticle
- description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  name: Batch OCR Processing in Python – Complete Programming Guide
  steps:
  - name: Missing or Corrupt Images
    text: If an image can’t be opened, most OCR libraries raise an exception that
      aborts the whole batch. Wrap the call in a `try/except` inside the batch function
      or filter out problematic files beforehand (see the sanity check in Step 1).
  - name: Language & DPI Settings
    text: For multilingual documents, pass a `langs` parameter (e.g., `langs=['en',
      'de']`). If your scans are low‑resolution, consider pre‑processing with `Pillow`
      to upscale to 300 DPI before OCR—this often boosts accuracy.
  - name: Memory Constraints
    text: 'Eight threads can eat RAM, especially with large images. If you hit memory
      errors, lower `max_threads` or process the list in smaller chunks:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Xử lý OCR hàng loạt trong Python – Hướng dẫn lập trình toàn diện
url: /vi/python-java/general/batch-ocr-processing-in-python-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xử lý OCR Hàng loạt trong Python – Hướng dẫn Lập trình Toàn diện

Bạn đã bao giờ cần **xử lý OCR hàng loạt** nhưng không chắc làm sao chạy hiệu quả trên hàng chục trang quét? Bạn không phải là người duy nhất—các nhà phát triển thường gặp khó khăn khi cố gắng trích xuất văn bản từ một loạt ảnh mà không làm quá tải CPU.  

Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn một cách đơn giản để **trích xuất văn bản từ loạt ảnh** bằng công cụ OCR của Python, chạy công việc trên tối đa tám luồng, và cuối cùng xem mỗi ảnh đã đóng góp bao nhiêu ký tự. Khi kết thúc, bạn sẽ có một script có thể tái sử dụng để xử lý **trích xuất văn bản ảnh hàng loạt** như một chuyên gia.

## Nội Dung Hướng Dẫn

Chúng ta sẽ đi qua ba bước thực tiễn:

1. Xây dựng danh sách các tệp ảnh mà bạn muốn nhận dạng.  
2. Khởi chạy công cụ OCR song song với `max_threads=8`.  
3. Duyệt qua kết quả và in ra một bản tóm tắt ngắn gọn.

Không cần dịch vụ bên ngoài, không cần thư viện lạ—chỉ cần Python thuần và một wrapper OCR tiêu chuẩn (ví dụ, `ocr` từ `easyocr` hoặc một wrapper tùy chỉnh). Nếu bạn đã có Python 3.8+ và đã cài đặt gói OCR, bạn đã sẵn sàng sao chép‑dán và chạy.

---

## Bước 1: Chuẩn Bị Danh Sách Các Tệp Ảnh cho Xử Lý OCR Hàng Loạt

Điều đầu tiên bạn cần là một tập hợp các đường dẫn ảnh. Hãy nghĩ nó như một danh sách mua sắm cho công cụ OCR; mỗi mục trỏ tới một tệp PNG, JPEG hoặc TIFF chứa văn bản bạn muốn đọc.

```python
# Step 1: Prepare a list of image files to be recognized
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png",
    "YOUR_DIRECTORY/page4.png",
    "YOUR_DIRECTORY/page5.png"
]

# Quick sanity check – make sure the files exist
import os
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"These files are missing: {missing}")
```

**Tại sao điều này quan trọng:**  
Tạo danh sách từ trước cho phép công cụ OCR hoạt động ở chế độ batch thực sự. Nó cũng cung cấp cho bạn một vị trí duy nhất để thêm hoặc loại bỏ tệp mà không cần chạm vào logic xử lý sau này. Kiểm tra tính hợp lệ ngăn ngừa lỗi “file not found” gây sập giữa chừng trong một lần chạy dài.

---

## Bước 2: Chạy OCR trên Batch với Các Luồng Song Song (Extract Text from Image Batch)

Bây giờ chúng ta truyền danh sách cho công cụ OCR. Hầu hết các wrapper OCR hiện đại đều cung cấp phương thức `recognize_batch` nhận đối số `max_threads`. Khi đặt giá trị `8` chúng ta yêu cầu thư viện khởi tạo tám luồng làm việc, điều này trên CPU quad‑core có hyper‑threading có thể giảm đáng kể thời gian xử lý.

```python
# Step 2: Run OCR on the batch, allowing up to 8 parallel threads
# Assuming `ocr` is a module that provides OcrEngine with recognize_batch()
import ocr

batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# batch_results is a list of Result objects, each with a .text attribute
```

**Tại sao song song hữu ích:**  
OCR tiêu tốn nhiều CPU; mỗi ảnh được đưa qua một mạng nơ‑ron hoặc một engine cũ. Chạy chúng tuần tự có thể rất chậm, đặc biệt với các bản quét độ phân giải cao. Các luồng song song giữ cho mọi lõi đều bận, biến một công việc 5‑phút thành 1‑phút trên phần cứng thông thường.

**Mẹo:** Nếu bạn đang dùng `easyocr`, lời gọi trông giống `reader.readtext(image_path, detail=0)` trong một vòng lặp. Trừu tượng `recognize_batch` của chúng tôi ẩn đi sự phức tạp này, nhưng bạn luôn có thể thay thế bằng `ThreadPoolExecutor` của riêng mình nếu thư viện không hỗ trợ batch.

---

## Bước 3: Duyệt Qua Kết Quả và Tổng Hợp Trích Xuất Văn Bản Ảnh Hàng Loạt

Sau khi OCR hoàn tất, bạn sẽ có một danh sách các đối tượng kết quả. Hãy zip các đường dẫn tệp gốc với đầu ra OCR tương ứng và in ra một dòng gọn cho mỗi ảnh, cho biết bao nhiêu ký tự đã được nhận dạng.

```python
# Step 3: Iterate through the results and display character counts
for file_path, result in zip(image_files, batch_results):
    # result.text holds the raw extracted string
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Bạn sẽ thấy:**  

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

**Tại sao bước này hữu ích:**  
Đếm nhanh số ký tự cho phép bạn ngay lập tức biết một ảnh có được xử lý đúng hay không. Một số ký tự bất ngờ thấp có thể là dấu hiệu của bản quét mờ, cài đặt ngôn ngữ sai, hoặc tệp bị hỏng—những vấn đề bạn có thể khắc phục trước khi chuyển sang phân tích tiếp theo.

---

## Bonus: Xử Lý Các Trường Hợp Cạnh và Những Cạm Bẫy Thường Gặp

### Ảnh Thiếu hoặc Hỏng  
Nếu một ảnh không mở được, hầu hết các thư viện OCR sẽ ném ra ngoại lệ làm dừng toàn bộ batch. Hãy bao bọc lời gọi trong `try/except` bên trong hàm batch hoặc lọc ra các tệp có vấn đề trước (xem kiểm tra tính hợp lệ ở Bước 1).

### Cài Đặt Ngôn Ngữ & DPI  
Đối với tài liệu đa ngôn ngữ, truyền tham số `langs` (ví dụ, `langs=['en', 'de']`). Nếu bản quét của bạn có độ phân giải thấp, cân nhắc tiền xử lý bằng `Pillow` để nâng lên 300 DPI trước khi OCR—thường cải thiện độ chính xác.

### Hạn Chế Bộ Nhớ  
Tám luồng có thể tiêu tốn RAM, đặc biệt với ảnh lớn. Nếu gặp lỗi bộ nhớ, giảm `max_threads` hoặc xử lý danh sách thành các khối nhỏ hơn:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(image_files, 3):  # process three images at a time
    results = ocr.OcrEngine.recognize_batch(chunk, max_threads=3)
    # handle results...
```

---

## Script Hoàn Chỉnh

Kết hợp mọi thứ lại, dưới đây là một ví dụ đầy đủ, sẵn sàng chạy. Thay `"YOUR_DIRECTORY"` bằng đường dẫn chứa các tệp PNG của bạn và đảm bảo mô-đun `ocr` đã được cài đặt.

```python
#!/usr/bin/env python3
"""
Batch OCR Processing Script
Extracts text from an image batch using parallel threads and prints character counts.
"""

import os
import ocr  # Replace with your OCR library import, e.g., from easyocr import Reader

# -------------------------------------------------
# Step 1: Define the list of image files
# -------------------------------------------------
image_dir = "YOUR_DIRECTORY"
image_files = [
    os.path.join(image_dir, f"page{i}.png") for i in range(1, 6)
]

# Verify that all files exist
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"Missing image files: {missing}")

# -------------------------------------------------
# Step 2: Run OCR in parallel (max 8 threads)
# -------------------------------------------------
# The OcrEngine is a placeholder – adapt to your library's API
batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# -------------------------------------------------
# Step 3: Report how many characters each image yielded
# -------------------------------------------------
for file_path, result in zip(image_files, batch_results):
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Kết quả mong đợi** (số liệu của bạn sẽ khác):

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

Chạy script bằng `python batch_ocr.py` và quan sát terminal hiện ra các thống kê ngắn gọn.

---

## Tổng Quan Hình Ảnh

![Sơ đồ quy trình xử lý OCR hàng loạt](image-placeholder.png "Sơ đồ minh họa các bước xử lý OCR hàng loạt")

*Văn bản thay thế ảnh:* *Sơ đồ quy trình xử lý OCR hàng loạt cho thấy việc tạo danh sách tệp, thực thi OCR song song, và tổng hợp kết quả.*

---

## Kết Luận

Bây giờ bạn đã có nền tảng vững chắc cho **xử lý OCR hàng loạt** trong Python. Bằng cách chuẩn bị danh sách ảnh sạch sẽ, tận dụng các luồng song song để **trích xuất văn bản từ loạt ảnh**, và tổng hợp kết quả, bạn có thể biến một công việc thủ công tẻ nhạt thành một pipeline nhanh chóng và có thể lặp lại.  

Từ đây bạn có thể:

- Lưu mỗi `result.text` vào tệp `.txt` để xử lý NLP tiếp theo.  
- Kết hợp số ký tự với điểm tin cậy để lọc các trang chất lượng thấp.  
- Tích hợp script vào quy trình nhập tài liệu lớn hơn, có thể đưa dữ liệu vào một chỉ mục tìm kiếm.

Dù bạn đang số hoá tài liệu lưu trữ, xây dựng ứng dụng quét biên lai, hay chuẩn bị dữ liệu đào tạo cho mô hình ngôn ngữ, các khái niệm ở đây có thể mở rộng lên hàng trăm hoặc hàng nghìn tệp với ít thay đổi.

Có câu hỏi về cài đặt ngôn ngữ, tiền xử lý ảnh, hoặc triển khai trên đám mây? Hãy để lại bình luận hoặc xem các hướng dẫn liên quan về *Tiền xử lý ảnh Python* và *OCR bất đồng bộ với asyncio*. Chúc bạn lập trình vui!

## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ, kèm theo giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
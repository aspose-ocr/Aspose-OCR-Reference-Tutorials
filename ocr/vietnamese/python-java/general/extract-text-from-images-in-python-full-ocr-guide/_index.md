---
category: general
date: 2026-06-19
description: Trích xuất văn bản từ hình ảnh bằng Python OCR. Học cách phát hiện ngôn
  ngữ tự động, xử lý song song và nhận dạng hàng loạt trong một hướng dẫn ngắn gọn.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Python OCR. Bài hướng dẫn này
  trình bày việc phát hiện ngôn ngữ tự động, xử lý song song và nhận dạng hàng loạt
  trong một hướng dẫn duy nhất.
og_title: Trích xuất văn bản từ hình ảnh trong Python – Hướng dẫn OCR đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Trích xuất văn bản từ hình ảnh bằng Python – Hướng dẫn OCR đầy đủ
url: /vi/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# trích xuất văn bản từ hình ảnh trong Python – Hướng dẫn OCR toàn diện

Bạn đã bao giờ tự hỏi làm sao **trích xuất văn bản từ hình ảnh** mà không phải gõ lại từng từ chưa? Bạn không phải là người duy nhất. Dù bạn đang số hoá các hoá đơn cũ, xây dựng một kho lưu trữ tài liệu có thể tìm kiếm, hay chỉ đơn giản là thử nghiệm các thủ thuật AI thú vị, khả năng lấy văn bản từ ảnh là kỹ năng cần có cho bất kỳ lập trình viên Python nào ngày nay.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy ngay, **trích xuất văn bản từ hình ảnh** bằng một engine OCR phổ biến. Chúng ta sẽ đề cập đến phát hiện ngôn ngữ tự động, xử lý song song để tăng tốc, và nhận dạng ảnh theo lô để bạn có thể xử lý hàng chục tệp trong vài giây. Nghe có vẻ phù hợp? Hãy bắt đầu.

## Những gì bạn sẽ học

- Cách khởi tạo engine OCR với `ocr.OcrEngine`.
- Kích hoạt **phát hiện ngôn ngữ tự động** để engine tự chọn ngôn ngữ phù hợp.
- Cấu hình **OCR xử lý song song** với một thread pool tùy chỉnh.
- Thực hiện **nhận dạng ảnh theo lô** trên danh sách tệp.
- In ra văn bản đã nhận dạng cho mỗi ảnh, sẵn sàng để lưu hoặc lập chỉ mục.

Không cần tài liệu bên ngoài—tất cả những gì bạn cần đều có ở đây, và mã hoạt động ngay với package `ocr` (cài đặt bằng `pip install ocr`).

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy chắc chắn bạn đã có:

1. Python 3.8 hoặc mới hơn được cài đặt.
2. Package `ocr` (`pip install ocr`).
3. Một thư mục chứa các ảnh PNG (hoặc JPG) bạn muốn xử lý.
4. Kiến thức cơ bản về hàm và vòng lặp trong Python.

Đó là tất cả—không có phụ thuộc nặng, không cần GPU, chỉ cần Python thuần.

![trích xuất văn bản từ hình ảnh ví dụ](https://example.com/ocr-demo.png "Ảnh chụp màn hình hiển thị kết quả trích xuất văn bản từ hình ảnh")

*Alt text: ảnh chụp màn hình demo trích xuất văn bản từ hình ảnh*

## Bước 1 – Thiết lập Engine OCR (Từ khóa chính trong hành động)

Điều đầu tiên cần làm: tạo một instance của engine OCR. Hãy nghĩ `ocr.OcrEngine()` như bộ não của toàn bộ quá trình; nó biết cách đọc ký tự, dòng và đoạn văn.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Tại sao chúng ta cần một engine rõ ràng? Bởi vì **sử dụng ocr.OcrEngine** cho phép bạn kiểm soát chi tiết các thiết lập ngôn ngữ, luồng xử lý và hơn thế nữa. Đây là cách linh hoạt nhất để **trích xuất văn bản từ hình ảnh** so với các helper một dòng.

## Bước 2 – Để Engine Tự Động Phát Hiện Ngôn Ngữ

Hầu hết các thư viện OCR yêu cầu bạn chỉ định ngôn ngữ cần tìm. Điều này ổn với dự án một ngôn ngữ, nhưng gây phiền toái khi xử lý lô đa ngôn ngữ. May mắn là package `ocr` hỗ trợ **phát hiện ngôn ngữ tự động**.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

Đặt `engine.language` thành `ocr.Language.Auto` sẽ khiến engine tự sniff mỗi ảnh và chọn mô hình ngôn ngữ phù hợp. Dòng lệnh ngắn này tiết kiệm cho bạn hàng giờ cấu hình thủ công khi làm việc với tài liệu quốc tế.

## Bước 3 – Tăng Tốc Độ với OCR Xử Lý Song Song

Nếu máy bạn có bốn lõi CPU trở lên, tại sao không tận dụng chúng? Engine có thể khởi tạo một thread pool, cho phép xử lý nhiều ảnh đồng thời. Đây là lúc **OCR xử lý song song** tỏa sáng.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

Bạn có thể điều chỉnh số `4` tùy theo máy. Nhiều thread → chạy lô nhanh hơn, nhưng nhớ mỗi thread tiêu tốn bộ nhớ, vì vậy hãy tìm điểm cân bằng phù hợp với môi trường của bạn.

## Bước 4 – Thu Thập Các Ảnh Cần Xử Lý

Bây giờ chúng ta cần một danh sách các đường dẫn tệp. Bạn có thể tạo danh sách này thủ công, đọc từ CSV, hoặc dùng `glob`. Để minh bạch, chúng ta sẽ hard‑code một danh sách ngắn:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

Thay `YOUR_DIRECTORY` bằng đường dẫn thực tế trên hệ thống của bạn. Nếu có hàng chục tệp, một lệnh nhanh `glob.glob("*.png")` sẽ làm phần việc nặng.

## Bước 5 – Thực Hiện Nhận Dạng Ảnh Theo Lô

Đây là phần cốt lõi của tutorial: một lời gọi duy nhất xử lý mọi ảnh trong `files` và trả về danh sách các đối tượng kết quả. Đây là tính năng **nhận dạng ảnh theo lô** giúp OCR quy mô lớn trở nên thực tiễn.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

Ở phía sau, engine phân phối mỗi tệp cho bốn worker thread mà chúng ta đã cấu hình trước, đồng thời tự động phát hiện ngôn ngữ cho từng ảnh. Phương thức trả về một danh sách, mỗi phần tử chứa văn bản đã nhận dạng và siêu dữ liệu liên quan.

## Bước 6 – In (hoặc Lưu) Văn Bản Đã Trích Xuất

Cuối cùng, chúng ta lặp qua các kết quả và in ra văn bản. Trong dự án thực tế, bạn có thể ghi chúng vào cơ sở dữ liệu hoặc file CSV, nhưng việc in ra giúp ví dụ đơn giản hơn.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**Kết quả mong đợi** (rút gọn để ngắn gọn):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

Mỗi khối hiển thị tên tệp theo sau là chuỗi ký tự được OCR tạo ra. Nếu một ảnh chứa nhiều ngôn ngữ, bạn sẽ thấy các ký tự tương ứng xuất hiện nhờ bước **phát hiện ngôn ngữ tự động** ở trên.

## Mẹo chuyên nghiệp & Những lỗi thường gặp

- **Chất lượng ảnh quan trọng** – ảnh mờ hoặc độ tương phản thấp sẽ cho ra kết quả rác. Hãy tiền xử lý bằng OpenCV (`cv2.threshold`, `cv2.resize`) nếu cần.
- **Số lượng thread vs. I/O** – Nếu ảnh của bạn nằm trên ổ mạng chậm, việc tăng thread có thể không giúp gì. Theo dõi mức sử dụng CPU bằng `top` hoặc `Task Manager`.
- **Xử lý Unicode** – `result.text` là chuỗi Unicode. Khi ghi ra file, mở chúng với `encoding="utf‑8"` để tránh lỗi `UnicodeEncodeError`.
- **Tiêu thụ bộ nhớ** – PDF lớn có thể tiêu tốn nhiều RAM. Nếu gặp `MemoryError`, giảm kích thước thread pool hoặc xử lý ảnh theo các khối nhỏ hơn.

## Script Hoàn Chỉnh

Dưới đây là script đầy đủ, sẵn sàng copy‑paste, tích hợp mọi bước chúng ta đã thảo luận. Lưu lại dưới tên `batch_ocr.py` và chạy `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

Chạy như sau:

```bash
python batch_ocr.py ./my_images 4
```

Bạn sẽ thấy một khối văn bản được định dạng đẹp cho mỗi ảnh, chứng minh rằng bạn có thể **trích xuất văn bản từ hình ảnh** ở quy mô lớn.

## Tiếp Theo?

Sau khi đã nắm vững các kiến thức cơ bản về **trích xuất văn bản từ hình ảnh** bằng Python, bạn có thể khám phá:

- **Xử lý hậu kỳ**: làm sạch đầu ra OCR bằng regex hoặc các thư viện ngôn ngữ tự nhiên.
- **Chuyển PDF**: đưa các chuỗi đã trích xuất vào công cụ tạo PDF để có PDF có thể tìm kiếm.
- **Dịch vụ OCR đám mây**: so sánh kết quả `ocr` nội bộ với Google Vision hoặc Azure OCR để đạt độ chính xác cao hơn trong các trường hợp đặc biệt.
- **Giao diện GUI**: xây dựng một ứng dụng Flask hoặc FastAPI nhỏ cho phép người dùng tải ảnh lên và ngay lập tức xem văn bản đã trích xuất.

Mỗi chủ đề này đều dựa trên nền tảng **thư viện OCR Python** mà bạn vừa thiết lập, và đều hưởng lợi từ các thủ thuật **OCR xử lý song song** mà chúng ta đã dùng.

---

*Chúc bạn lập trình vui! Nếu gặp bất kỳ khó khăn nào, hãy để lại bình luận bên dưới—tôi luôn sẵn sàng hỗ trợ giải quyết các vấn đề liên quan đến OCR.*

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn hoạt động đầy đủ cùng các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
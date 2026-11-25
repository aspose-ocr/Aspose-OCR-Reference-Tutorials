---
category: general
date: 2026-06-19
description: Trích xuất văn bản từ hình ảnh trong Python bằng một công cụ OCR đơn
  giản. Tìm hiểu cách chuyển đổi hình ảnh đã quét thành văn bản, nhận dạng văn bản
  từ ảnh, và liệt kê các tệp hình ảnh trong Python một cách hiệu quả.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: vi
og_description: Trích xuất văn bản từ hình ảnh trong Python bằng một công cụ OCR nhẹ.
  Hướng dẫn này chỉ cho bạn cách chuyển đổi hình ảnh đã quét thành văn bản, nhận dạng
  văn bản từ ảnh, và liệt kê các tệp hình ảnh trong Python chỉ trong vài bước.
og_title: Trích xuất văn bản từ hình ảnh bằng Python – Hướng dẫn OCR toàn bộ theo
  lô
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Trích xuất văn bản từ hình ảnh trong Python – Hướng dẫn OCR hàng loạt đầy đủ
url: /vi/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ hình ảnh trong Python – Hướng dẫn OCR hàng loạt đầy đủ

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng không biết bắt đầu từ đâu? Bạn không đơn độc—các nhà phát triển luôn phải đối mặt với thách thức chuyển đổi các tệp PDF đã quét, biên lai chụp ảnh, hoặc ảnh chụp màn hình thành văn bản có thể tìm kiếm. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho thấy cách **chuyển đổi hình ảnh đã quét thành văn bản**, nhận dạng văn bản từ ảnh, và thậm chí **liệt kê các tệp hình ảnh theo kiểu python**. Khi kết thúc, bạn sẽ có một script có thể tái sử dụng để xử lý toàn bộ thư mục chỉ trong một lần.

Chúng tôi sẽ bao phủ mọi thứ bạn cần: các thư viện bắt buộc, lý do mỗi bước quan trọng, xử lý các trường hợp biên, và một chút khắc phục sự cố. Không cần phải chạy theo tài liệu bên ngoài; mã dưới đây là tự chứa, và các giải thích trả lời cả “cách làm” *và* “tại sao”. Hãy mở IDE yêu thích của bạn, và bắt đầu thôi.

---

## Những gì bạn sẽ xây dựng

- Khởi tạo một engine OCR (chúng tôi sẽ dùng gói `ocr` để minh họa).
- Quét một thư mục và **liệt kê các tệp hình ảnh theo kiểu python**, lọc PNG, JPG và TIFF.
- Thực hiện một thao tác **OCR hàng loạt** trên tất cả các ảnh đã tìm được.
- In ra văn bản đã trích xuất cho mỗi tệp, được gắn nhãn rõ ràng.

> **Mẹo chuyên nghiệp:** Nếu bạn chưa cài đặt thư viện `ocr`, bạn có thể thay thế bằng `pytesseract` với một vài thay đổi nhỏ—logic cốt lõi vẫn giữ nguyên.

---

## Yêu cầu trước

- Python 3.8+ (script sử dụng f‑strings và type hints).
- Một thư viện OCR cung cấp một `OcrEngine` với `recognize_batch`. Trong hướng dẫn này chúng tôi giả định một gói `ocr` hư cấu, nhưng mẫu này hoạt động với các thư viện thực.
- Một thư mục chứa các tệp hình ảnh bạn muốn xử lý (`.png`, `.jpg`, `.tif`).

---

## Bước 1 – Cài đặt & Nhập các mô-đun cần thiết

Đầu tiên, hãy chắc chắn rằng gói OCR đã sẵn sàng. Nếu bạn đang dùng một thư viện thực như `pytesseract`, hãy thay đổi phần import cho phù hợp.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Tại sao điều này quan trọng:** Việc import `os` cung cấp khả năng xử lý đường dẫn đa nền tảng, trong khi `typing.List` giúp IDE tự hoàn thành và chuẩn bị cho tương lai.

---

## Bước 2 – **Extract Text from Images**: Khởi tạo Engine OCR

Việc tạo engine là bước đầu tiên cho bất kỳ công việc OCR nào. Chúng tôi cũng đặt ngôn ngữ tự động phát hiện để engine có thể xử lý tài liệu đa ngôn ngữ.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Giải thích:** Bằng cách đóng gói việc tạo engine trong một hàm, chúng ta giữ cho mã có tính mô-đun. Nếu sau này bạn cần tinh chỉnh DPI hoặc chế độ OCR, chỉ cần chỉnh sửa một chỗ duy nhất.

---

## Bước 3 – **List Image Files Python**: Thu thập tệp từ một thư mục

Bây giờ chúng ta cần xác định mọi ảnh muốn xử lý. List comprehension dưới đây phản ánh một mẫu “list image files python” phổ biến.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Xử lý trường hợp biên:** Hàm này bỏ qua các thư mục con (bạn có thể thêm đệ quy sau) và tự động lọc các tệp ẩn vì chúng thường không kết thúc bằng các phần mở rộng được hỗ trợ.

---

## Bước 4 – **Convert Scanned Images to Text**: Chạy OCR hàng loạt

Hầu hết các thư viện OCR cung cấp một phương thức batch nhanh hơn rất nhiều so với xử lý từng ảnh một. Đây là cách chúng ta gọi nó.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Tại sao batch?** Gửi tất cả ảnh cùng một lúc giảm tải (ví dụ: tải lại mô hình OCR nhiều lần) và thường mang lại hiệu suất CPU/GPU tốt hơn.

---

## Bước 5 – **Recognize Text from Pictures**: Hiển thị kết quả

Cuối cùng, chúng ta lặp qua các cặp tên tệp và kết quả OCR, in ra tiêu đề sạch sẽ cho mỗi ảnh.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Mẹo:** `strip()` loại bỏ khoảng trắng đầu/cuối mà OCR thường thêm vào.

---

## Script đầy đủ – Kết hợp tất cả lại

Dưới đây là chương trình hoàn chỉnh, có thể chạy được. Lưu lại dưới tên `batch_ocr.py` và chạy `python batch_ocr.py <your_folder>`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Kết quả mong đợi

Giả sử thư mục chứa `invoice1.png` và `receipt.jpg`, bạn có thể thấy:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Mỗi khối đều được gắn nhãn rõ ràng, giúp việc xử lý tiếp theo (ví dụ: lưu vào cơ sở dữ liệu) trở nên đơn giản.

---

## Xử lý các vấn đề thường gặp

| Vấn đề | Tại sao xảy ra | Giải pháp nhanh |
|-------|----------------|-----------------|
| **Không xuất hiện văn bản** | Ngôn ngữ OCR không được phát hiện hoặc ảnh có độ tương phản quá thấp. | Buộc ngôn ngữ (`engine.language = ocr.Language.English`) hoặc tiền xử lý ảnh (tăng độ tương phản). |
| **Lỗi bộ nhớ khi batch lớn** | Engine cố gắng tải tất cả ảnh cùng lúc. | Chia `image_files` thành các khối (`batch_size = 20`) và gọi `recognize_batch` liên tục. |
| **Định dạng tệp không được hỗ trợ** | Bạn đã thêm `.gif` hoặc `.bmp`. | Mở rộng tuple `supported_exts` hoặc chuyển đổi ảnh sang PNG/JPG trước. |
| **Ký tự Unicode bị lỗi** | OCR trả về bytes thay vì string. | Đảm bảo thư viện OCR xuất Unicode (`result.text.decode('utf‑8')` nếu cần). |

---

## Mở rộng quy trình làm việc

Bây giờ bạn đã có thể **trích xuất văn bản từ hình ảnh**, hãy xem xét các bước tiếp theo:

- **Xuất ra CSV** – Ghi mỗi tên tệp và văn bản đã trích xuất vào bảng tính để phân tích.
- **Xử lý song song** – Sử dụng `concurrent.futures.ThreadPoolExecutor` để xử lý nhiều batch đồng thời.
- **Tích hợp OCR đám mây** – Thay engine cục bộ bằng Google Vision hoặc Azure OCR để đạt độ chính xác cao hơn trên các bố cục phức tạp.
- **Thêm tiền xử lý ảnh** – Các thư viện như Pillow hoặc OpenCV có thể chỉnh góc, giảm nhiễu, hoặc ngưỡng ảnh trước khi OCR, nâng cao kết quả.

Tất cả các ý tưởng này đều sử dụng cùng các hàm cốt lõi mà chúng ta đã xây dựng, vì vậy bạn không cần bắt đầu từ đầu.

---

## Kết luận

Chúng tôi vừa đi qua một giải pháp hoàn chỉnh để **trích xuất văn bản từ hình ảnh** trong Python, bao phủ mọi thứ từ **list image files python** đến **recognize text from pictures** và cuối cùng là **convert scanned images to text** trong một batch gọn gàng. Script được thiết kế đơn giản nhưng đủ linh hoạt để làm nền tảng cho các dự án lớn hơn—cho dù bạn đang số hoá biên lai, xây dựng kho lưu trữ có thể tìm kiếm, hay vận hành một pipeline trích xuất dữ liệu.

Hãy thử chạy, tinh chỉnh các bước tiền xử lý, và quan sát độ chính xác OCR của bạn tăng lên. Nếu gặp khó khăn, hãy quay lại bảng “Xử lý các vấn đề thường gặp”; hầu hết các vấn đề đều được giải quyết bằng một thay đổi cấu hình nhỏ.

Sẵn sàng cho thử thách tiếp theo? Hãy thêm bước chuyển PDF sang ảnh bằng `pdf2image`, rồi đưa các ảnh này trực tiếp vào cùng pipeline. Khi kết hợp OCR với hệ sinh thái phong phú của Python, không gì là không thể.

Chúc lập trình vui vẻ, và hy vọng văn bản của bạn luôn rõ ràng!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, kèm theo giải thích từng bước để giúp bạn thành thạo các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất văn bản từ hình ảnh với Aspose OCR – Hướng dẫn chi tiết](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Trích xuất văn bản từ hình ảnh – Cơ bản OCR với Aspose.OCR cho Java](/ocr/english/java/ocr-basics/)
- [Cách trích xuất văn bản từ hình ảnh qua URL bằng Aspose.OCR cho Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
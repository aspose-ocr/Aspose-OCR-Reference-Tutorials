---
category: general
date: 2026-01-12
description: Trích xuất văn bản từ PDF bằng công cụ OCR Python – học cách đọc PDF
  với OCR, tải hình ảnh cho OCR và nhận kết quả có cấu trúc.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: vi
og_description: Trích xuất văn bản từ PDF bằng công cụ OCR Python. Hướng dẫn này cho
  thấy cách đọc PDF với OCR, tải ảnh cho OCR và sử dụng công cụ OCR Python để có kết
  quả đáng tin cậy.
og_title: Trích xuất văn bản từ PDF bằng công cụ OCR Python – Hướng dẫn đầy đủ
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Trích xuất văn bản từ PDF bằng công cụ OCR Python – Hướng dẫn từng bước
url: /vi/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ PDF bằng Động cơ OCR Python – Hướng dẫn đầy đủ

Bạn đã bao giờ cần **trích xuất văn bản từ PDF** nhưng tệp chỉ là một hình ảnh được quét chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, PDF bạn nhận được không có văn bản có thể chọn, vì vậy cách duy nhất là **đọc PDF bằng OCR**.  

Trong hướng dẫn này, chúng tôi sẽ đi qua một giải pháp thực tế, từ đầu đến cuối, cho thấy chính xác cách **tải hình ảnh cho OCR**, khởi động **OCR engine Python**, và trích xuất văn bản có cấu trúc mà bạn có thể đưa vào các pipeline downstream. Không có tham chiếu mơ hồ, chỉ có một ví dụ hoàn chỉnh, có thể chạy được mà bạn có thể sao chép‑dán ngay hôm nay.

## Những gì bạn sẽ học

- Cách cài đặt và import thư viện OCR Python mà bạn cần.  
- Các bước chính xác để **tải hình ảnh cho OCR** từ tệp PDF.  
- Cách gọi phương thức `recognize_structured()` của engine và lặp qua các block, line và word.  
- Mẹo xử lý kết quả có độ tin cậy thấp và các PDF đa trang.  

Khi kết thúc hướng dẫn này, bạn sẽ có một script có thể **trích xuất văn bản từ PDF** một cách đáng tin cậy, bất kể tài liệu có một trang hay một trăm trang.

---

![Sơ đồ cho thấy động cơ OCR xử lý PDF và xuất ra văn bản có cấu trúc.](images/ocr_flow.png "sơ đồ trích xuất văn bản từ pdf")

*Văn bản thay thế hình ảnh: sơ đồ trích xuất văn bản từ pdf mô tả các bước xử lý OCR.*

## Yêu cầu trước

- Python 3.9 trở lên (code sử dụng f‑strings và type hints).  
- Gói OCR có thể cài đặt qua pip, cung cấp lớp `OcrEngine` (ví dụ, thư viện giả tưởng `pyocr`).  
- Tệp PDF bạn muốn xử lý, lưu cục bộ (ví dụ, `form.pdf`).  

Nếu bạn chưa có thư viện OCR, hãy cài đặt bằng:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Bước 1: Trích xuất Văn bản từ PDF – Cài đặt OCR Engine

Trước khi chúng ta có thể **đọc PDF bằng OCR**, chúng ta cần một thể hiện của engine. Hãy nghĩ engine như bộ não nhìn vào từng pixel và quyết định ký tự nào nó đại diện.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Tại sao điều này quan trọng:** Khởi tạo engine một lần cho phép bạn tái sử dụng các gói ngôn ngữ đã tải cho nhiều tệp, tiết kiệm thời gian và bộ nhớ.

---

## Bước 2: Tải hình ảnh cho OCR – Chuẩn bị PDF của bạn

PDF không phải là một hình ảnh thô, vì vậy thư viện thường cung cấp một công cụ hỗ trợ để chuyển trang đầu tiên (hoặc tất cả các trang) thành hình ảnh mà OCR engine có thể hiểu.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Mẹo:** Nếu PDF của bạn có nhiều trang, nhiều thư viện OCR cho phép bạn truyền `page=2` hoặc lặp qua `engine.load_image(pdf_path, page=n)`. Đối với tài liệu lớn, hãy xem xét xử lý các trang theo lô để tránh tăng đột biến bộ nhớ.

---

## Bước 3: Sử dụng OCR Engine Python – Nhận dạng Văn bản có Cấu trúc

Bây giờ công việc nặng nề diễn ra. Lệnh `recognize_structured()` trả về một cấu trúc phân cấp của các block → line → word, mỗi phần được chú thích với ngôn ngữ, độ tin cậy và hộp bao.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **Bạn nhận được:**  
> - `structured_result.blocks` – các container cấp cao nhất (thường là đoạn văn hoặc cột).  
> - Mỗi block chứa `lines`, và mỗi line chứa `words`.  
> - Điểm tin cậy cho phép bạn lọc các kết quả đáng ngờ.

---

## Bước 4: Lặp qua Kết quả – Truy cập Blocks, Lines và Words

Dưới đây là một vòng lặp ngắn gọn in ra thông tin hữu ích nhất. Bạn có thể mở rộng để ghi JSON, CSV, hoặc đưa vào cơ sở dữ liệu.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Kết quả Dự kiến

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Lý do bạn sẽ thích điều này:** Cấu trúc phản ánh cách con người đọc một trang, giúp dễ dàng tái tạo lại các bảng hoặc bố cục cột sau này.

---

## Bước 5: Xử lý Các Trường hợp Cạnh – Độ Tin Cậy Thấp & PDF Đa Trang

### Từ có Độ Tin Cậy Thấp

Nếu độ tin cậy của một từ giảm xuống dưới, ví dụ, `0.70`, bạn có thể muốn đánh dấu nó để kiểm tra thủ công:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Xử lý Tất cả Các Trang

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Mẹo chuyên nghiệp:** Lưu cache các hình ảnh trung gian dưới dạng PNG nếu thư viện OCR của bạn vẽ lại chúng mỗi lần—điều này có thể giảm vài giây cho các lô lớn.

---

## Script Hoàn chỉnh Hoạt động

Kết hợp mọi thứ lại, đây là một tệp duy nhất bạn có thể chạy ngay lập tức:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Save this as `extract_pdf_ocr.py` and run:

```bash
python extract_pdf_ocr.py
```

Bạn sẽ thấy chi tiết cấp block được in ra console, cùng với bất kỳ cảnh báo độ tin cậy thấp nào.

---

## Kết luận

Chúng tôi vừa trình bày một cách hoàn chỉnh, sẵn sàng cho sản xuất để **trích xuất văn bản từ PDF** bằng **OCR engine Python**. Bắt đầu từ việc cài đặt thư viện, qua **tải hình ảnh cho OCR**, đến **đọc PDF bằng OCR** và cuối cùng lặp qua kết quả có cấu trúc, bạn giờ đã có một script có thể tái sử dụng và điều chỉnh cho bất kỳ dự án nào.

- Xuất cấu trúc ra JSON cho các pipeline NLP downstream.  
- Thêm phát hiện ngôn ngữ để chuyển đổi mô hình OCR một cách linh hoạt.  
- Tích hợp với `pdf2image` để tiền xử lý các PDF có bố cục phức tạp.  

Hãy thử trên một lô hoá đơn đa trang, điều chỉnh ngưỡng độ tin cậy, và xem bạn có thể nhanh chóng chuyển các PDF đã quét thành văn bản có thể tìm kiếm, chỉnh sửa như thế nào. Nếu gặp bất kỳ khó khăn nào, hãy để lại bình luận bên dưới—chúc bạn OCR vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
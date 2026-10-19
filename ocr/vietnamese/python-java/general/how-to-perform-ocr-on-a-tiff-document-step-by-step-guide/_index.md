---
category: general
date: 2026-01-12
description: Cách thực hiện OCR nhanh chóng và chính xác. Học cách chạy OCR trên tài
  liệu, trích xuất văn bản từ tiff, tải hình ảnh cho OCR và thiết lập ngôn ngữ OCR
  trong Python.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: vi
og_description: Cách thực hiện OCR trong Python. Hướng dẫn này cho bạn biết cách chạy
  OCR trên tài liệu, trích xuất văn bản từ tiff, tải hình ảnh để OCR và thiết lập
  ngôn ngữ OCR.
og_title: Cách thực hiện OCR trên tài liệu TIFF – Hướng dẫn chi tiết
tags:
- OCR
- Python
- Image Processing
title: Cách thực hiện OCR trên tài liệu TIFF – Hướng dẫn từng bước
url: /vi/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện OCR trên Tài Liệu TIFF – Hướng Dẫn Đầy Đủ

Bạn đã bao giờ tự hỏi **cách thực hiện OCR** trên một tệp TIFF đã quét mà không phải mất hàng giờ tìm kiếm thư viện phù hợp chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần trích xuất văn bản từ ảnh TIFF, đặc biệt khi hiệu năng và cài đặt ngôn ngữ quan trọng.

Trong tutorial này chúng ta sẽ đi qua mọi thứ bạn cần biết: từ cài đặt gói OCR, tải ảnh để OCR, thiết lập ngôn ngữ OCR, cho tới **chạy OCR trên tài liệu** và lấy ra văn bản sạch. Khi hoàn thành, bạn sẽ có một script sẵn sàng chạy mà có thể đưa vào bất kỳ dự án nào.

> **Mẹo chuyên nghiệp:** Mặc dù ví dụ sử dụng mô-đun `ocr` chung, cùng một khái niệm áp dụng cho Tesseract, EasyOCR, hoặc bất kỳ engine OCR hiện đại nào cung cấp API Python.

---

## Những Gì Bạn Cần Chuẩn Bị

- Python 3.8+ (bất kỳ phiên bản gần đây nào đều được)
- Thư viện OCR cung cấp lớp `OcrEngine` (ví dụ mẫu dùng gói `ocr` giả tưởng; hãy thay bằng gói thực tế của bạn)
- Một tệp TIFF đa trang mà bạn muốn xử lý (chúng ta sẽ gọi nó là `big_document.tif`)
- Một máy có ít nhất 4 lõi CPU nếu bạn dự định thiết lập số lượng luồng

Không cần dịch vụ bên ngoài, không cần khóa cloud—chỉ cần code chạy cục bộ trong vài giây.

---

![ví dụ cách thực hiện OCR](/images/ocr-example.png "cách thực hiện OCR trên tài liệu TIFF")

*Văn bản thay thế ảnh: cách thực hiện OCR trên tài liệu TIFF – xem trước văn bản đã trích xuất.*

---

## Bước 1: Cài Đặt và Nhập Thư Viện OCR

Đầu tiên, hãy cài đặt thư viện vào máy của bạn. Hầu hết các gói OCR có trên PyPI, vì vậy một lệnh `pip install` đơn giản là đủ.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Bây giờ nhập các lớp bạn sẽ cần. Nếu bạn dùng Tesseract, dòng import sẽ khác, nhưng phần còn lại của code vẫn giữ nguyên.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Lý do quan trọng:* Nhập đúng các ký hiệu ngay từ đầu giúp tránh xung đột namespace sau này và làm cho script dễ đọc hơn.

---

## Bước 2: Tạo và Cấu Hình Engine OCR (Thiết Lập Ngôn Ngữ OCR)

Cấu hình engine là nơi bạn **thiết lập ngôn ngữ OCR** để nhận dạng chính xác. Tiếng Anh là mặc định, nhưng bạn có thể chuyển sang tiếng Pháp, tiếng Đức, hoặc chế độ đa ngôn ngữ chỉ với một dòng.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Tại sao lại dùng 4 luồng?** Hầu hết laptop hiện đại có ít nhất bốn lõi, và giới hạn số luồng giúp quá trình OCR không chiếm hết tài nguyên máy—đặc biệt hữu ích khi script chạy trên server chia sẻ.

Nếu cần ngôn ngữ khác, chỉ cần thay `ocr.Language.ENGLISH` bằng `ocr.Language.FRENCH`, `ocr.Language.SPANISH`, v.v.

---

## Bước 3: Tải Ảnh Để OCR (Load Image for OCR)

Bây giờ chúng ta **tải ảnh để OCR**. Phương thức `Image.load` đọc tệp TIFF vào bộ nhớ, tự động xử lý tài liệu đa trang.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Trường hợp đặc biệt:* Nếu tệp quá lớn, bạn có thể hết RAM. Khi đó, hãy cân nhắc tải từng trang một bằng `Image.load_page(page_number)` (nếu thư viện hỗ trợ).

---

## Bước 4: Chạy OCR Trên Tài Liệu

Với engine đã sẵn sàng và ảnh đã được tải, đã đến lúc **chạy OCR trên tài liệu**. Phương thức `process` thực hiện công việc nặng và trả về một đối tượng kết quả.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Bên trong, engine sẽ chia ảnh thành các khối văn bản, chạy mô hình nhận dạng, và ghép các kết quả lại với nhau. Lệnh này là blocking, nghĩa là script sẽ chờ cho đến khi toàn bộ TIFF được xử lý—rất phù hợp cho các job batch.

---

## Bước 5: Trích Xuất Văn Bản Từ TIFF và Kiểm Tra Kết Quả

Cuối cùng, chúng ta **trích xuất văn bản từ TIFF** bằng cách truy cập thuộc tính `text` của kết quả. Hãy in ra 200 ký tự đầu tiên để kiểm tra nhanh.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Kết quả mong đợi (ví dụ):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Nếu bạn cần toàn bộ văn bản, chỉ cần dùng `ocr_result.text`. Đối với các bước xử lý tiếp theo, bạn có thể ghi nó vào file `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Ví Dụ Hoàn Chỉnh

Kết hợp tất cả lại, đây là một script sẵn sàng chạy. Thay tên gói placeholder bằng gói bạn đã cài đặt thực tế.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Chạy script bằng:

```bash
python ocr_tiff_example.py
```

Bạn sẽ thấy một đoạn preview được in ra console và một file có tên `extracted_text.txt` chứa toàn bộ bản sao.

---

## Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

- **Nếu TIFF chứa nhiều trang thì sao?**  
  Hầu hết các engine OCR xử lý mỗi trang như một ảnh riêng biệt. Thuộc tính `ocr_result.text` sẽ chứa ký tự xuống dòng giữa các trang. Nếu bạn cần xử lý từng trang, hãy lặp lại với `Image.load_page(page_number)`.

- **Có thể xử lý PNG hoặc JPEG thay vì TIFF không?**  
  Chắc chắn rồi. Phương thức `Image.load` thường chấp nhận bất kỳ định dạng nào mà Pillow hoặc thư viện nền hỗ trợ. Chỉ cần đổi phần mở rộng file.

- **Văn bản bị rối—có nên thay đổi ngôn ngữ không?**  
  Có. Bước **thiết lập ngôn ngữ OCR** rất quan trọng với tài liệu không phải tiếng Anh. Đảm bảo đã cài đặt gói ngôn ngữ (ví dụ, `tesseract‑lang‑fra` cho tiếng Pháp).

- **Hết bộ nhớ?**  
  Giảm `set_memory_limit` hoặc xử lý từng trang một. Một số engine còn cho phép giảm kích thước ảnh trước khi nhận dạng.

---

## Kết Luận

Vậy là bạn đã có một hướng dẫn ngắn gọn, đầy đủ về **cách thực hiện OCR** trên tệp TIFF bằng Python. Chúng ta đã đi qua mọi bước: cài đặt thư viện, cấu hình engine (bao gồm **thiết lập ngôn ngữ OCR**), **tải ảnh để OCR**, **chạy OCR trên tài liệu**, và cuối cùng **trích xuất văn bản từ TIFF**.  

Hãy thoải mái thử nghiệm: điều chỉnh số luồng, chuyển đổi ngôn ngữ, hoặc đưa đầu ra OCR vào pipeline xử lý ngôn ngữ tự nhiên. Khi đã nắm vững nền tảng, bạn có thể mở rộng vô hạn.

Có câu hỏi thêm? Hãy để lại bình luận bên dưới, chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
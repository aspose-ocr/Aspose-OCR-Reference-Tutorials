---
category: general
date: 2026-03-26
description: Cách trích xuất văn bản PDF bằng OCR. Tìm hiểu cách tải PDF dưới dạng
  hình ảnh, nhận dạng văn bản PDF và trích xuất văn bản từ PDF với một ví dụ Python
  đơn giản.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: vi
og_description: Cách trích xuất văn bản PDF bằng OCR. Hướng dẫn này cho bạn biết cách
  tải PDF dưới dạng hình ảnh, nhận dạng văn bản PDF và trích xuất văn bản từ PDF bằng
  Python.
og_title: Cách Trích Xuất Văn Bản PDF bằng OCR – Hướng Dẫn Toàn Diện
tags:
- OCR
- Python
- PDF processing
title: Cách Trích Xuất Văn Bản PDF Bằng OCR – Hướng Dẫn Chi Tiết Từng Bước
url: /vi/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Trích Xuất Văn Bản PDF bằng OCR – Hướng Dẫn Chi Tiết Từng Bước

Bạn đã bao giờ tự hỏi **cách trích xuất PDF** mà thực chất chỉ là các hình ảnh quét chưa? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn này khi họ cần nội dung có thể tìm kiếm nhưng chỉ có các PDF chỉ chứa hình ảnh. Tin tốt là gì? Chỉ với vài dòng mã và một thư viện OCR mạnh mẽ, bạn có thể biến những PDF dạng ảnh đó thành văn bản thuần trong chớp mắt.  

Trong hướng dẫn này, chúng ta sẽ đi qua **cách sử dụng OCR** để tải một PDF dưới dạng hình ảnh, nhận dạng văn bản PDF, và cuối cùng **trích xuất văn bản từ PDF** bất kỳ độ dài nào. Khi kết thúc, bạn sẽ có một script có thể chạy được, giải thích rõ ràng từng bước, và một vài mẹo để tránh những khó khăn thường gặp.

## Những Điều Cần Chuẩn Bị

- Python 3.9 hoặc mới hơn (mã cũng chạy trên 3.10+)  
- Gói Python `ocr` (hoặc bất kỳ thư viện OCR tương thích nào cung cấp `OcrEngine`, `OcrEngineMode`, và `Imaging.Image`)  
- Một file PDF đa trang bạn muốn xử lý (trong ví dụ chúng ta sẽ gọi nó là `multi_page.pdf`)  
- Kiến thức cơ bản về môi trường ảo (không bắt buộc nhưng được khuyến nghị)

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Windows, hãy cân nhắc sử dụng Anaconda Prompt; trên macOS/Linux, một lệnh đơn giản `python -m venv venv && source venv/bin/activate` sẽ thực hiện công việc.

## Bước 1: Cài Đặt Thư Viện OCR

Đầu tiên, tải gói OCR từ PyPI. Ví dụ dưới đây sử dụng một gói `ocr` giả tưởng mô phỏng API được hiển thị trong đoạn mã, nhưng hầu hết các thư viện thực tế (như `pytesseract` + `pdf2image`) cũng tuân theo cùng một mẫu.

```bash
pip install ocr
```

Nếu bạn đang dùng một engine khác, hãy thay `ocr` bằng tên phù hợp (ví dụ, `pip install pytesseract pdf2image`).

## Bước 2: Khởi Tạo Engine OCR

Tạo một thể hiện engine là nền tảng của **cách trích xuất PDF**. Hãy nghĩ engine như bộ não sẽ giải mã các pixel trong mỗi trang PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Tại sao điều này quan trọng:** `set_engine_mode` cho phép bạn cân bằng giữa tốc độ và độ chính xác. `DEFAULT` là lựa chọn cân đối; nếu bạn cần độ chính xác cao hơn, chuyển sang `HIGH_ACCURACY` (nếu thư viện hỗ trợ).

## Bước 3: Tải PDF dưới dạng Đối Tượng Hình Ảnh

OCR hoạt động trên hình ảnh, không phải trên container PDF, vì vậy chúng ta phải chuyển đổi PDF thành dạng hình ảnh trước. Phương thức `Imaging.Image.load` tự động xử lý các PDF đa trang.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Trường hợp đặc biệt:** Một số thư viện chỉ chấp nhận hình ảnh một trang. Trong trường hợp đó, bạn sẽ lặp qua từng trang bằng `pdf2image.convert_from_path`. Lệnh `load` của chúng tôi trừu tượng hoá việc này, biến **load pdf as image** thành một dòng lệnh.

## Bước 4: Nhận Dạng Văn Bản trên Tất Cả Các Trang

Bây giờ là phần cốt lõi của **nhận dạng văn bản PDF**. Engine quét mọi trang, trả về một danh sách các đối tượng kết quả—một cho mỗi trang.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Mỗi `page_result` chứa các phương thức như `get_text()` (văn bản thuần) và `get_confidence()` (chỉ số chất lượng tùy chọn).  

> **Mẹo:** Nếu bạn chỉ cần trang đầu tiên, gọi `recognize(pdf_image[0])` thay vì dùng trợ giúp đa trang.

## Bước 5: Duyệt Kết Quả và Xuất Văn Bản Đã Trích Xuất

Cuối cùng, chúng ta lặp qua các kết quả, in ra văn bản của mỗi trang. Điều này hoàn thành quy trình **trích xuất văn bản từ PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Kết Quả Dự Kiến

Nếu `multi_page.pdf` chứa ba trang với các từ “Hello”, “World”, và “Python”, bạn sẽ thấy:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Xong—PDF của bạn giờ đã có thể tìm kiếm được hoàn toàn và văn bản sẵn sàng cho các quy trình tiếp theo (đánh chỉ mục, phân tích cảm xúc, bất kỳ gì bạn muốn).

## Bước 6: Xử Lý Các Rủi Ro Thông Thường

| Vấn Đề | Nguyên Nhân | Giải Pháp Nhanh |
|-------|-------------|-----------------|
| **Kết quả trống** | Các trang PDF được quét ở DPI thấp, khiến ký tự không thể phân biệt. | Tăng độ phân giải ảnh trước khi OCR: `pdf_image = pdf_image.resize(300)` (300 DPI là mức phù hợp). |
| **Ký tự rác** | Các bảng chữ cái không phải Latin cần gói ngôn ngữ. | Tải mô hình ngôn ngữ phù hợp: `ocr_engine.load_language('spa')` cho tiếng Tây Ban Nha, v.v. |
| **Bùng RAM khi PDF lớn** | Tải tất cả các trang cùng lúc tiêu tốn RAM. | Xử lý các trang theo lô: `for img in pdf_image.split(batch=10): …` (mã giả). |
| **Hiệu năng chậm** | Dùng `DEFAULT` trên tài liệu lớn có thể chậm. | Chuyển sang chế độ `FAST` hoặc chạy OCR song song bằng `concurrent.futures`. |

## Thêm: Lưu Văn Bản Đã Trích Xuất vào Tập Tin

Hầu hết các pipeline thực tế cần lưu trữ văn bản. Dưới đây là một hàm trợ giúp nhỏ ghi mọi thứ vào `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Bây giờ bạn có thể đưa `output.txt` vào công cụ tìm kiếm, cơ sở dữ liệu, hoặc bất kỳ mô hình NLP nào.

## Tổng Hợp – Script Hoàn Chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng chạy. Sao chép, dán, điều chỉnh đường dẫn file, và bạn đã sẵn sàng.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Chạy nó:

```bash
python extract_pdf_ocr.py
```

Bạn sẽ thấy nội dung mỗi trang được in ra console, tiếp theo là xác nhận rằng file `extracted_text.txt` đã được tạo.

## Kết Luận

Chúng ta đã đề cập **cách trích xuất PDF** văn bản từ các tài liệu chỉ chứa hình ảnh bằng một engine OCR, từ việc cài đặt thư viện đến xử lý kết quả đa trang và lưu đầu ra. Bây giờ bạn đã biết **cách sử dụng OCR**, cách **tải PDF dưới dạng hình ảnh**, và cách **nhận dạng văn bản PDF** một cách đáng tin cậy.  

Bước tiếp theo? Hãy thử đổi chế độ engine mặc định sang cài đặt độ chính xác cao, thử nghiệm các gói ngôn ngữ cho PDF đa ngôn ngữ, hoặc đưa văn bản đã trích xuất vào chỉ mục tìm kiếm toàn văn như Elasticsearch. Khi đã nắm vững các nguyên tắc cơ bản của việc trích xuất văn bản từ file PDF, bạn có thể làm bất cứ điều gì.

---

![ví dụ cách trích xuất pdf](images/ocr_flowchart.png){alt="lưu đồ quy trình trích xuất pdf"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
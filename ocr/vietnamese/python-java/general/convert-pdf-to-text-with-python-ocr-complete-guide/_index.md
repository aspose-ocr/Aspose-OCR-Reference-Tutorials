---
category: general
date: 2026-07-05
description: Chuyển đổi PDF sang văn bản bằng Python OCR. Tìm hiểu cách trích xuất
  văn bản từ PDF, thực hiện xử lý OCR hàng loạt và tải PDF để OCR trong vài bước đơn
  giản.
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: vi
og_description: Chuyển đổi PDF sang văn bản nhanh chóng. Hướng dẫn này cho thấy cách
  trích xuất văn bản từ PDF, thực hiện xử lý OCR hàng loạt và nhận dạng các tệp PDF
  đã quét bằng Python.
og_title: Chuyển PDF sang Văn bản bằng OCR Python – Hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Chuyển đổi PDF sang Văn bản bằng OCR Python – Hướng dẫn toàn diện
url: /vi/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi PDF sang Văn bản với Python OCR – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **convert PDF to text** mà không gặp khó khăn? Có thể bạn có một đống các hợp đồng, hoá đơn hoặc bài báo được quét và cần phiên bản văn bản thuần để lập chỉ mục hoặc phân tích. Tin tốt là chỉ vài dòng Python có thể thực hiện công việc nặng cho bạn.

Trong hướng dẫn này, chúng tôi sẽ đi qua một giải pháp thực tế không chỉ **convert pdf to text**, mà còn cho bạn cách **extract text from pdf**, thiết lập **batch OCR processing**, và đúng cách **load pdf for OCR**. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy có thể **recognize scanned pdf** các trang trong một lần.

## Những gì bạn sẽ học

- Cài đặt và cấu hình một thư viện Python OCR (chúng tôi sẽ sử dụng một gói `ocr` chung để minh họa).  
- Tải một PDF đa trang và đưa nó vào engine OCR.  
- Lặp qua các kết quả để in hoặc lưu văn bản đã trích xuất.  
- Xử lý các trường hợp đặc biệt thường gặp như tệp lớn, PDF được mã hoá, và tài liệu đa ngôn ngữ.  

Không có công cụ GUI nặng, không cần sao chép thủ công—chỉ là mã thuần mà bạn có thể đưa vào pipeline CI hoặc tiện ích desktop.

![Convert PDF to Text using Python OCR](https://example.com/images/convert-pdf-to-text.png "Convert PDF to Text using Python OCR")

## Yêu cầu trước

Trước khi chúng ta bắt đầu, hãy chắc chắn rằng bạn đã có:

| Yêu cầu | Tại sao quan trọng |
|---------|--------------------|
| Python 3.9+ | Cú pháp hiện đại, gợi ý kiểu, và hiệu năng tốt hơn. |
| `ocr` library (or a wrapper around Tesseract) | Cung cấp các lớp `OcrEngine`, `Language`, và `Image` được sử dụng trong ví dụ. |
| A multi‑page scanned PDF (e.g., `contract.pdf`) | Đây là nguồn mà bạn sẽ **load pdf for OCR**. |
| Basic command‑line familiarity | Để cài đặt các gói và chạy script. |

Nếu bạn đang sử dụng Tesseract ở mức độ thấp, hãy cài đặt nó qua trình quản lý gói OS của bạn (`apt-get install tesseract-ocr` trên Linux, `brew install tesseract` trên macOS). Sau đó thêm wrapper Python:

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## Bước 1: Tạo OCR Engine và Đặt Ngôn ngữ Nhận dạng

Đầu tiên, chúng ta cần một thể hiện OCR engine. Đặt ngôn ngữ thành tiếng Anh là mặc định phổ biến, nhưng bạn có thể chuyển sang các ngôn ngữ hỗ trợ khác sau.

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**Tại sao điều này quan trọng:** Engine là bộ não giải mã dữ liệu pixel. Bằng cách xác định rõ `engine.language`, bạn tránh được chi phí phát hiện ngôn ngữ trên mỗi trang, giúp tăng tốc **batch OCR processing** đáng kể.

## Bước 2: Tải tài liệu PDF cho OCR

Bây giờ chúng ta đưa PDF vào bộ nhớ. Phương thức `ocr.Image.load` có thể nhận một đường dẫn tệp và trả về một đối tượng mà engine hiểu.

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**Mẹo chuyên nghiệp:** Nếu PDF của bạn được bảo vệ bằng mật khẩu, hầu hết các thư viện cho phép bạn truyền tham số `password`. Xử lý sớm sẽ ngăn ngừa lỗi “cannot open file” khó hiểu sau này.

## Bước 3: Chạy OCR trên Tất cả Các Trang – Recognize Scanned PDF trong Một Lần

Chạy OCR từng trang một có thể chậm, đặc biệt với tài liệu lớn. Phương thức `recognize_multi_page` thực hiện **batch OCR processing** nội bộ, sử dụng đa luồng khi có thể.

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**Điều gì đang diễn ra phía sau?** Engine truyền từng trang tới engine OCR nền (như Tesseract), thu thập văn bản và đóng gói trong một `OcrResult`. Cách tiếp cận này giảm tải I/O và cung cấp cho bạn cách sạch sẽ để **extract text from pdf** sau này.

## Bước 4: Lặp qua Kết quả và Xuất Văn bản Được Nhận dạng

Cuối cùng, chúng ta lặp qua mỗi `OcrResult` và in ra văn bản. Bạn cũng có thể ghi mỗi trang vào một tệp `.txt` riêng hoặc nối chúng thành một tài liệu duy nhất.

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**Tại sao dùng enumerate?** Sử dụng `enumerate(..., start=1)` cung cấp số trang dễ đọc cho con người, hữu ích khi bạn cần tham chiếu tới một phần cụ thể của PDF gốc.

### Kết quả Dự kiến

Chạy script với một hợp đồng 3 trang có thể tạo ra:

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

Nếu một trang không chứa văn bản nhận dạng được, `result.text` tương ứng sẽ là một chuỗi rỗng—lý tưởng để phát hiện các trang trống hoặc chỉ có hình ảnh.

## Xử lý PDF lớn và Giới hạn Bộ nhớ

Xử lý một PDF 500 trang có thể làm cạn kiệt RAM nếu bạn tải toàn bộ cùng một lúc. Dưới đây là hai chiến lược:

1. **Chunked Loading** – Một số thư viện cho phép bạn tải một dải trang:

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **Streaming to Disk** – Ghi trực tiếp văn bản của mỗi trang vào tệp thay vì giữ toàn bộ danh sách trong bộ nhớ.

Cả hai kỹ thuật đều giữ cho quy trình **convert pdf to text** của bạn có khả năng mở rộng.

## Xử lý Lỗi và Các Trường hợp Đặc biệt

- **Encrypted PDFs** – Truyền mật khẩu vào `Image.load`:

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **Mixed Languages** – Chuyển ngôn ngữ cho mỗi trang nếu bạn phát hiện một script khác:

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **Low‑Resolution Scans** – Tiền xử lý ảnh bằng thư viện như `Pillow` để tăng độ tương phản trước OCR. Điều này có thể cải thiện đáng kể chất lượng bước **recognize scanned pdf**.

## Script Đầy đủ: Convert PDF to Text trong Một Lần

Dưới đây là script hoàn chỉnh, sẵn sàng thực thi, kết nối mọi thứ lại với nhau. Lưu lại dưới tên `pdf_to_text.py` và chạy `python pdf_to_text.py`.

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**Chạy script** sẽ tạo một thư mục `output` chứa `page_1.txt`, `page_2.txt`, v.v., thực hiện **extract text from pdf** một cách có cấu trúc.

## Kiểm tra Giải pháp

1. **Sanity Check** – Mở tệp `.txt` đã tạo và xác minh rằng vài dòng đầu khớp với tiêu đề của tài liệu gốc.  
2. **Performance Test** – Đo thời gian chạy script trên PDF 100 trang bằng lệnh `time`. Nếu mất thời gian lâu hơn mong đợi, hãy cân nhắc bật cờ đa luồng của thư viện (thường là `engine.set_threads(4)`).  
3. **Quality Assurance** – So sánh đầu ra OCR với đoạn văn được gõ thủ công bằng công cụ diff. Nhắm tới độ chính xác ký tự >95 % cho các bản quét sạch.

## Các Bước Tiếp Theo và Chủ đề Liên quan

- **Improve Accuracy**: Thử nghiệm với `engine.dpi = 300` hoặc áp dụng tiền xử lý ảnh (deskew, denoise) trước OCR.  
- **Searchable PDFs**: Sử dụng thư viện PDF (như `PyPDF2` hoặc `pdfplumber`) để nhúng văn bản đã trích xuất trở lại PDF gốc, làm cho nó có thể tìm kiếm.  
- **Natural Language Processing**: Đưa văn bản đã trích xuất vào spaCy hoặc NLTK để trích xuất thực thể, phân tích cảm xúc, hoặc gắn thẻ từ khóa.  
- **Automation Pipelines**: Kết hợp script này với `watchdog` để giám sát một thư mục và tự động **convert pdf to text** mỗi khi có tệp mới xuất hiện.

Bằng cách nắm vững các mẫu này, bạn sẽ có thể

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
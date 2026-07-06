---
category: general
date: 2026-06-22
description: Học cách OCR tệp PDF trong Python, trích xuất văn bản từ PDF và chuyển
  PDF sang văn bản bằng phương pháp dựa trên luồng. Các bước đơn giản để xử lý PDF
  đã quét.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: vi
og_description: Cách OCR tệp PDF trong Python? Hãy làm theo hướng dẫn này để trích
  xuất văn bản từ PDF, chuyển PDF sang văn bản và xử lý PDF đã quét bằng luồng.
og_title: Cách OCR PDF trong Python – Hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Cách OCR PDF trong Python – Hướng dẫn toàn diện để trích xuất văn bản từ PDF
url: /vi/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách OCR PDF trong Python – Hướng Dẫn Toàn Diện để Trích Xuất Văn Bản từ PDF

Bạn đã bao giờ tự hỏi **cách OCR PDF** như thế nào mà không phải vật lộn với các công cụ desktop nặng nề? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế—như tự động hoá hoá đơn hoặc số hoá các bản quét lưu trữ—bạn cần một cách đáng tin cậy để chuyển một PDF đã quét thành văn bản có thể tìm kiếm và chỉnh sửa.

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ sạch sẽ, từ đầu đến cuối mà **trích xuất văn bản từ PDF** các trang bằng một engine OCR Python nhẹ. Khi kết thúc, bạn sẽ biết chính xác cách **chuyển PDF sang văn bản**, cách **tải PDF từ luồng**, và cách **xử lý PDF đã quét** một cách hiệu quả. Không có phép màu, chỉ là mã Python thuần túy mà bạn có thể đưa vào dự án ngay hôm nay.

## Những Điều Bạn Sẽ Học

- Cài đặt và cấu hình một thư viện OCR Python có khả năng hiểu đầu vào PDF.  
- Bật chế độ nhận dạng PDF và đặt định dạng đầu ra là văn bản thuần.  
- Tải một PDF đa trang từ luồng tệp (mẫu “load pdf from stream” cổ điển).  
- Chạy OCR trên tất cả các trang và lấy nội dung văn bản.  
- In hoặc lưu kết quả để xử lý tiếp theo.

**Yêu cầu trước**  
- Python 3.8+ đã được cài đặt trên máy của bạn.  
- Kiến thức cơ bản về pip và môi trường ảo.  
- Một tệp PDF đã quét (có tên `multipage.pdf` trong ví dụ) được đặt trong một thư mục đã biết.

Nếu bất kỳ điều nào trong số này nghe lạ, đừng lo—mỗi bước đều được giải thích bằng ngôn ngữ đơn giản, và chúng tôi sẽ cung cấp các lệnh chính xác mà bạn cần.

---

## Bước 1: Cài Đặt Engine OCR (cách OCR PDF)

Đầu tiên—bạn cần một engine OCR có thể xử lý đầu vào PDF. Trong hướng dẫn này, chúng tôi sẽ sử dụng gói `ocr` giả định (API của nó phản chiếu các SDK thương mại phổ biến, nhưng mẫu tương tự cũng hoạt động với Tesseract‑OCR, ABBYY, hoặc Google Vision khi được bọc phù hợp).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Mẹo:** Nếu bạn đang dùng Windows và gặp lỗi quyền, hãy thử `pip install --user ocr` thay vì.

Sau khi gói được cài đặt, bạn có thể import nó trong script và khởi tạo một instance của engine—đây là phần cốt lõi của **cách OCR PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Đối tượng `OcrEngine` chứa tất cả các cài đặt mà chúng ta sẽ điều chỉnh sau, như ngôn ngữ, DPI, và—đặc biệt—chế độ PDF.

## Bước 2: Bật Nhận Dạng PDF và Chọn Đầu Ra (trích xuất văn bản từ PDF)

Mặc định, nhiều SDK OCR cho rằng bạn đang cung cấp cho chúng các hình ảnh. Để engine xử lý luồng đến như một PDF, chúng ta bật cờ nhận dạng PDF và yêu cầu đầu ra dạng văn bản thuần.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

Tại sao phải chỉ định định dạng đầu ra? Bởi vì một số engine có thể trả về PDF với lớp văn bản ẩn, PDF có thể tìm kiếm, hoặc JSON kèm bounding box. Đối với hầu hết các pipeline trích xuất dữ liệu, **trích xuất văn bản từ PDF** dưới dạng chuỗi thuần là định dạng downstream sạch nhất.

## Bước 3: Tải PDF từ Luồng Tệp (load PDF from stream)

Tải PDF từ một luồng là mẫu tiết kiệm bộ nhớ—bạn tránh việc tải toàn bộ tệp vào RAM một lúc. Điều này đặc biệt hữu ích khi xử lý các tài liệu đa trang lớn.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **Nếu tệp nằm trên S3 hoặc một bucket đám mây khác thì sao?**  
> Chỉ cần thay thế `from_file` bằng một phương thức chấp nhận bộ đệm byte (ví dụ, `ImageStream.from_bytes(s3_object.read())`). Phần còn lại của pipeline vẫn giữ nguyên.

## Bước 4: Chạy OCR trên Tất Cả Các Trang (xử lý PDF đã quét)

Bây giờ công việc nặng nề bắt đầu. Engine sẽ lặp qua từng trang, chạy engine nhận dạng, và trả về một danh sách các đối tượng trang—mỗi đối tượng cung cấp nội dung văn bản của nó.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

Trong hậu trường, thư viện OCR giải nén mỗi trang PDF, raster hoá nó ở DPI đã cấu hình, và đưa bitmap qua mô hình mạng nơ-ron của nó. Kết quả? Một tập hợp các đối tượng `Page` sẵn sàng để trích xuất.

## Bước 5: Lấy và Hiển Thị Văn Bản Được Nhận Dạng (chuyển PDF sang văn bản)

Cuối cùng, chúng ta lặp qua các trang đã trả về và in ra văn bản đã nhận dạng. Đây là thời điểm **chuyển PDF sang văn bản** thực sự diễn ra.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Kết Quả Dự Kiến

Nếu `multipage.pdf` chứa ba trang đã quét, bạn sẽ thấy gì đó giống như:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Lưu ý sự tách biệt rõ ràng giữa các trang—hữu ích nếu bạn cần lưu văn bản của mỗi trang vào cơ sở dữ liệu hoặc đưa nó vào mô hình NLP downstream.

## Xử Lý Các Trường Hợp Cạnh Thường Gặp

### 1. PDF có Lớp Hình Ảnh và Văn Bản Hỗn Hợp

Một số PDF đã chứa lớp văn bản ẩn (ví dụ, xuất từ Word). Nếu bạn muốn engine OCR **bỏ qua văn bản hiện có** và xử lý lại hình ảnh, hãy đặt:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Tệp Lớn Vượt Quá Giới Hạn Bộ Nhớ

Khi làm việc với các PDF có kích thước gigabyte, hãy cân nhắc xử lý theo từng khối:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Hỗ Trợ Ngôn Ngữ và Phông Chữ

Nếu tài liệu đã quét của bạn bằng tiếng Pháp hoặc chứa ký tự đặc biệt, hãy cho engine biết mô hình ngôn ngữ nào sẽ dùng:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## Toàn Bộ Script – Sẵn Sàng Chạy

Dưới đây là ví dụ hoàn chỉnh, có thể chạy được, kết nối tất cả các phần lại với nhau. Lưu lại dưới tên `ocr_pdf.py` và thực thi `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Chạy script** sẽ in văn bản của mỗi trang ra console, chính xác như trong phần “Kết Quả Dự Kiến”. Từ đây bạn có thể chuyển hướng đầu ra tới một tệp:

```bash
python ocr_pdf.py > extracted_text.txt
```

## Kết Luận

Chúng tôi vừa trình bày **cách OCR PDF** trong Python từ đầu đến cuối. Bằng cách cấu hình engine, tải tài liệu qua luồng, và lặp qua mỗi trang đã nhận dạng, bạn có thể **trích xuất văn bản từ PDF**, **chuyển PDF sang văn bản**, và **xử lý PDF đã quét** chỉ với vài dòng mã. Cách tiếp cận này mở rộng từ các hoá đơn hai trang nhỏ tới các kho lưu trữ hàng trăm trang khổng lồ.

Tiếp theo? Hãy thử đưa các chuỗi đã trích xuất vào một chỉ mục tìm kiếm, một bộ tóm tắt mô hình ngôn ngữ, hoặc một pipeline kiểm tra dữ liệu. Bạn cũng có thể thử nghiệm các định dạng đầu ra như JSON để giữ lại siêu dữ liệu vị trí cho phân tích tài liệu nâng cao.

Có câu hỏi về việc xử lý PDF được mã hoá hoặc tích hợp với lưu trữ đám mây? Hãy để lại bình luận bên dưới—chúc bạn lập trình vui!

![Sơ đồ mô tả quy trình OCR PDF – cách OCR PDF, tải PDF từ luồng, nhận dạng các trang và trích xuất văn bản](ocr-pdf-workflow.png "sơ đồ quy trình OCR PDF")

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách OCR PDF trong .NET với Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cách Trích Xuất Văn Bản từ Hình Ảnh Sử Dụng Aspose.OCR cho .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Cách Trích Xuất Văn Bản từ Các Tệp ZIP Sử Dụng Aspose.OCR cho .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
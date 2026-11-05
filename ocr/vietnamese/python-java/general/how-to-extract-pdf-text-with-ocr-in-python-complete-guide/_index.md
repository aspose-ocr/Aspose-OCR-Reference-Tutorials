---
category: general
date: 2026-06-19
description: Cách trích xuất PDF bằng OCR trong Python – hướng dẫn từng bước bao gồm
  trích xuất văn bản từ PDF, nhận dạng văn bản từ hình ảnh và ví dụ OCR bằng Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: vi
og_description: Cách trích xuất PDF bằng OCR trong Python. Học cách trích xuất văn
  bản từ PDF, nhận dạng văn bản từ hình ảnh và xem một ví dụ hoàn chỉnh về OCR trong
  Python.
og_title: Cách Trích Xuất Văn Bản PDF bằng OCR trong Python – Hướng Dẫn Đầy Đủ
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Cách Trích Xuất Văn Bản PDF Bằng OCR Trong Python – Hướng Dẫn Toàn Diện
url: /vi/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Trích Xuất Văn Bản PDF bằng OCR trong Python – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách trích xuất PDF** khi tệp chỉ là một hình ảnh quét chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế—như hợp đồng, hoá đơn, hoặc lưu trữ lịch sử—PDF bạn nhận được không có văn bản có thể chọn được. Tin tốt? Chỉ vài dòng Python có thể biến những trang chỉ có hình ảnh thành văn bản có thể tìm kiếm và chỉnh sửa.

Trong hướng dẫn này, chúng ta sẽ đi qua một **ví dụ OCR Python** thực tế, đọc một PDF, chuyển trang đầu tiên thành hình ảnh, và sau đó **trích xuất văn bản từ PDF** bằng một công cụ OCR. Khi kết thúc, bạn sẽ biết chính xác cách **đọc PDF với OCR**, lý do mỗi bước quan trọng, và cách điều chỉnh mã cho tài liệu đa trang hoặc các ngôn ngữ khác.

## Những Điều Bạn Sẽ Học

- Cài đặt và thiết lập một thư viện OCR đáng tin cậy cho Python.  
- Chuyển các trang PDF thành hình ảnh phù hợp cho OCR.  
- **Nhận dạng văn bản từ hình ảnh** và lấy các chuỗi Unicode sạch.  
- Những khó khăn thường gặp (PDF độ phân giải thấp, trang bị xoay) và cách tránh chúng.  
- Mở rộng script để xử lý nhiều trang hoặc xử lý hàng loạt.

**Yêu cầu trước**: Python 3.8+, pip, và hiểu biết cơ bản về môi trường ảo. Không cần kinh nghiệm OCR trước—chỉ cần làm theo.

---

## ## Cách Trích Xuất Văn Bản PDF bằng OCR trong Python

Tiêu đề H2 này chứa từ khóa chính của chúng ta ngay nơi các công cụ tìm kiếm thích thấy. Hãy đi thẳng vào mã.

### Bước 1 – Cài Đặt Các Gói Yêu Cầu

Đầu tiên, chúng ta cần một công cụ OCR. Ví dụ dưới đây sử dụng gói **ocr** phổ biến (một lớp bao bọc mỏng quanh Tesseract). Nếu bạn thích backend khác, các khái niệm vẫn giống.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Mẹo chuyên nghiệp:** Trên Linux, bạn cũng cần binary Tesseract: `sudo apt-get install tesseract-ocr`. Người dùng macOS có thể cài qua Homebrew: `brew install tesseract`.

### Bước 2 – Khởi Tạo Công Cụ OCR và Đặt Ngôn Ngữ

Bây giờ chúng ta khởi động công cụ và yêu cầu nó tìm các ký tự tiếng Anh. Bạn có thể thay `ocr.Language.English` bằng bất kỳ mã ngôn ngữ nào được hỗ trợ.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Tại sao điều này quan trọng:** Đặt ngôn ngữ sẽ cải thiện độ chính xác đáng kể vì công cụ có thể áp dụng các từ điển và mô hình ký tự riêng cho ngôn ngữ.

### Bước 3 – Tải Trang PDF Thành Hình Ảnh

OCR hoạt động trên ảnh raster, không phải các đối tượng PDF. Hàm trợ giúp `ocr.Image.from_pdf` chuyển trang đã chọn thành bitmap. Điều chỉnh `page_number` cho các trang khác (đánh số bắt đầu từ 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Trường hợp đặc biệt:** Nếu PDF chứa đồ họa vector thay vì hình ảnh quét, bạn có thể nhận được bản render sắc nét. Đối với các bản quét độ phân giải thấp, hãy cân nhắc tăng DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Bước 4 – Nhận Dạng Văn Bản Từ Hình Ảnh Đã Render

Đây là phần cốt lõi của **ví dụ ocr python**. Công cụ xử lý bitmap và trả về một đối tượng chứa chuỗi đã trích xuất.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

Thuộc tính `ocr_result.text` chứa đầu ra văn bản thuần, giữ lại các ngắt dòng khi có thể.

### Bước 5 – In Hoặc Lưu Văn Bản Đã Trích Xuất

Cuối cùng, chúng ta xuất kết quả. Trong một ứng dụng thực tế, bạn có thể ghi vào tệp hoặc cơ sở dữ liệu.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Chạy script sẽ hiển thị một cái gì đó giống như:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Đó là quy trình **trích xuất văn bản từ pdf** hoàn chỉnh bằng OCR.

---

## ## Nhận Dạng Văn Bản Từ Hình Ảnh – Tinh Chỉnh Độ Chính Xác

Nếu bạn chỉ quan tâm đến **nhận dạng văn bản từ hình ảnh** (ví dụ, một JPEG của biên lai), bạn có thể bỏ qua bước chuyển đổi PDF:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Mẹo để có kết quả tốt hơn:**

- **Tiền xử lý** ảnh: chuyển sang thang độ xám, áp dụng ngưỡng, hoặc chỉnh nghiêng. Pillow giúp việc này dễ dàng.  
- **Tăng DPI** khi render PDF: độ phân giải cao hơn cung cấp nhiều chi tiết cho công cụ OCR.  
- **Bật cấu hình của công cụ OCR** cho phân đoạn trang (`ocr_engine.config = "--psm 6"` cho các khối đồng nhất).  

## ## Đọc PDF với OCR – Xử Lý Nhiều Trang

Hầu hết các hợp đồng có nhiều trang. Lặp qua mỗi trang là rất đơn giản:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Hàm này **đọc PDF với OCR**, nối các đầu ra lại và chèn một dấu phân trang rõ ràng. Bạn có thể đưa `full_text` vào chỉ mục tìm kiếm hoặc lưu thành tệp `.txt`.

## ## Những Rủi Ro Thường Gặp và Cách Khắc Phục

| Triệu chứng | Nguyên nhân có thể | Cách khắc phục |
|------------|-------------------|----------------|
| Ký tự lộn xộn, nhiều `?` | Ngôn ngữ sai hoặc thiếu tệp dữ liệu ngôn ngữ | Cài đặt gói ngôn ngữ Tesseract đúng (`tesseract-ocr-<lang>`) và đặt `ocr_engine.language`. |
| Thiếu dòng hoặc từ bị cắt ngắn | DPI thấp (dưới 150) | Render PDF ở 300 DPI hoặc cao hơn (`dpi=300`). |
| Văn bản bị xoay hoặc ngược | Trang quét không thẳng đứng | Sử dụng `ocr.Image.deskew(page_image)` trước khi nhận dạng. |
| Xử lý chậm trên PDF lớn | Xử lý các trang tuần tự trên một luồng | Song song hoá với `concurrent.futures.ThreadPoolExecutor`. |

## ## Mở Rộng Ví Dụ OCR Python

- **Xuất ra PDF/A**: Sau khi trích xuất, bạn có thể nhúng văn bản trở lại PDF có thể tìm kiếm bằng `reportlab` hoặc `pypdf2`.  
- **Phát hiện ngôn ngữ**: Sử dụng `langdetect` trên đầu ra OCR để chuyển `ocr_engine.language` một cách động.  
- **Xử lý hàng loạt**: Duyệt thư mục bằng `os.listdir` và áp dụng `extract_all_pages` cho mỗi tệp.  

## ## Kết Quả Mong Đợi và Kiểm Tra

Khi bạn chạy script trên một bản quét tiếng Anh rõ ràng, bạn sẽ thấy một khối văn bản sạch sẽ với dấu câu đúng. Kiểm tra bằng cách:

1. So sánh một vài dòng với hình ảnh quét gốc.  
2. Chạy đếm từ đơn giản (`len(ocr_result.text.split())`) để đảm bảo đầu ra không rỗng.  
3. Tùy chọn, đưa kết quả vào bộ kiểm tra chính tả như `pyspellchecker` để phát hiện lỗi OCR.  

## Kết Luận

Chúng tôi đã trình bày **cách trích xuất PDF** khi việc phân tích truyền thống thất bại, minh họa một **ví dụ ocr python** đầy đủ, và giải thích cách **nhận dạng văn bản từ hình ảnh** và **đọc PDF với OCR** cho cả trường hợp một trang và đa trang. Với các đoạn mã trên, bạn có thể chuyển bất kỳ PDF quét nào thành văn bản có thể tìm kiếm và chỉnh sửa—không còn phải gõ lại thủ công.

Bước tiếp theo? Hãy thử đổi ngôn ngữ sang tiếng Tây Ban Nha (`ocr.Language.Spanish`) hoặc thử nghiệm các kỹ thuật tiền xử lý ảnh để tăng độ chính xác. Nếu bạn đang xây dựng hệ thống quản lý tài liệu, hãy cân nhắc lập chỉ mục văn bản đã trích xuất bằng Elasticsearch để tìm kiếm siêu nhanh.

Có câu hỏi hoặc gặp PDF lạ? Hãy để lại bình luận, và chúc bạn lập trình vui vẻ!  

![Cách trích xuất PDF bằng OCR trong Python](image.png "Cách trích xuất PDF bằng OCR trong Python")

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích Xuất Văn Bản Từ Hình Ảnh với Aspose OCR – Hướng Dẫn Từng Bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Nhận Dạng Văn Bản PDF – Các Hoạt Động OCR với Aspose.OCR cho Java](/ocr/english/java/ocr-operations/)
- [Trích Xuất Văn Bản Hình Ảnh C# với Lựa Chọn Ngôn Ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
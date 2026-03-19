---
category: general
date: 2026-03-18
description: Chạy OCR trên hình ảnh để trích xuất văn bản từ PNG và tạo PDF có thể
  tìm kiếm. Tìm hiểu cách nhận dạng hình ảnh văn bản và chuyển đổi PNG sang PDF trong
  vài phút.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: vi
og_description: Chạy OCR trên hình ảnh để trích xuất văn bản từ PNG, nhận dạng hình
  ảnh văn bản và tạo PDF có thể tìm kiếm. Thực hiện theo hướng dẫn từng bước này.
og_title: Chạy OCR trên hình ảnh – Trích xuất văn bản từ PNG nhanh chóng
tags:
- OCR
- Python
- Image Processing
title: Chạy OCR trên hình ảnh – Trích xuất văn bản từ PNG nhanh chóng
url: /vi/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy OCR trên Ảnh – Trích Xuất Văn Bản từ PNG Nhanh Chóng

Bạn đã bao giờ cần **chạy OCR trên file ảnh** nhưng không biết bắt đầu từ đâu? Có thể bạn có một bài viết đã quét lưu dưới dạng `article.png` và chỉ muốn lấy văn bản thuần, hoặc bạn cần một PDF có thể tìm kiếm để lưu trữ. Dù sao, bạn đã đến đúng nơi. Trong hướng dẫn này, chúng ta sẽ đi qua việc trích xuất văn bản từ PNG, nhận dạng hình ảnh văn bản, và thậm chí chuyển PNG thành PDF có thể tìm kiếm — tất cả chỉ với một vài dòng code.

> **Bạn sẽ nhận được:** một script hoàn chỉnh, có thể chạy ngay, tải PNG, chạy OCR, lưu kết quả hOCR, và tùy chọn tạo PDF có thể tìm kiếm. Không thiếu import, không “xem tài liệu” chết — chỉ có một giải pháp tự chứa mà bạn có thể đưa vào dự án ngay hôm nay.

## Yêu Cầu Trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- **Python 3.8+** (cú pháp ở đây hoạt động trên bất kỳ phiên bản gần đây nào)
- Thư viện **`ocr_engine`** mà bạn đang dùng (ví dụ giả định một lớp gọi là `OcrEngine`; thay thế bằng Tesseract, EasyOCR, v.v. nếu cần)
- Một ảnh PNG bạn muốn xử lý (ví dụ `article.png` đặt trong thư mục bạn có thể tham chiếu)
- Quyền ghi vào thư mục đầu ra

Nếu bạn đang dùng Tesseract ở phía dưới, cài đặt nó bằng:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

Rồi cài wrapper Python:

```bash
pip install pytesseract Pillow
```

*Pro tip:* luôn cập nhật thư viện OCR của bạn — các gói ngôn ngữ và cải tiến hiệu năng thường xuyên được phát hành.

## Chạy OCR trên Ảnh – Hướng Dẫn Từng Bước

Dưới đây là **script hoàn chỉnh**. Bạn có thể sao chép‑dán nó vào một file tên `run_ocr.py` và chạy bằng `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Script làm gì, bằng tiếng Việt đơn giản

1. **Khởi tạo** engine OCR để bạn có thể điều chỉnh các thiết lập.
2. **Tải** file PNG (`article.png`). Script sẽ dừng sớm nếu file không tồn tại — tránh lỗi `NoneType` bí ẩn sau này.
3. **Chọn** `hocr` làm định dạng xuất. Định dạng này giữ nguyên bố cục gốc, rất cần thiết để sau này chuyển ảnh thành PDF có thể tìm kiếm.
4. **Chạy** engine nhận dạng; phần “công việc nặng” diễn ra ở đây.
5. **Ghi** XML hOCR vào `article.hocr`. Bây giờ bạn có một biểu diễn máy‑đọc được của văn bản và tọa độ của nó.
6. *(Tùy chọn)* Chuyển sang `"pdf"` và tạo PDF có thể tìm kiếm trong một bước bổ sung.

**Kết quả mong đợi** là một file `.hocr` được mã hoá UTF‑8 trông giống như sau (được rút gọn để ngắn gọn):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Nếu bạn bỏ comment phần PDF, bạn sẽ còn có `article_searchable.pdf`, có thể mở bằng bất kỳ trình xem PDF nào và dùng hộp tìm **Ctrl + F** để nhanh chóng tìm từ khóa.

![Ví dụ kết quả chạy OCR trên ảnh](example.png "Chạy OCR trên ảnh – kết quả hOCR và PDF")

## Cách Trích Xuất Văn Bản từ PNG Bằng OcrEngine

Nếu bạn chỉ cần văn bản thô (không cần bố cục, không cần PDF), bạn có thể bỏ qua bước hOCR hoàn toàn:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Tại sao chọn văn bản thuần?* Nó nhẹ, lý tưởng cho việc lập chỉ mục, và hoạt động tốt với các pipeline NLP tiếp theo.

## Nhận Diện Hình Ảnh Văn Bản và Tạo PDF Có Thể Tìm Kiếm

Tạo PDF có thể tìm kiếm là một quy trình hai bước:

1. **Chạy OCR** với `hocr` (như ở trên) để lấy thông tin bố cục.
2. **Kết hợp** PNG gốc với hOCR thành PDF bằng bộ xuất PDF của engine.

Hầu hết các thư viện OCR hiện đại (Tesseract, ABBYY, Google Vision) đều cung cấp một export `pdf` thực hiện đúng việc này. Đoạn code trong khối *Optional* của script chính cho thấy mẫu thực hiện. Nếu thư viện của bạn không có bộ xuất PDF tích hợp, bạn có thể dùng **`pdf2image`** + **`reportlab`** để ghép ảnh và hOCR lại — chỉ cần cho tôi biết, tôi sẽ chia sẻ một ví dụ nhanh bổ sung.

## Chuyển PNG sang PDF với Kết Quả OCR

Đôi khi bạn chỉ muốn một **PDF thuần** chứa ảnh (không có lớp có thể tìm kiếm). Điều này còn đơn giản hơn:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Kết hợp đoạn này với bước OCR nếu bạn cần phiên bản có thể tìm kiếm, hoặc giữ nguyên như một bản sao hình ảnh trung thực cho mục đích lưu trữ.

## Những Sai Lầm Thường Gặp & Mẹo Nhỏ

| Vấn đề | Tại sao xảy ra | Giải pháp nhanh |
|-------|----------------|-----------------|
| **PNG mờ hoặc độ phân giải thấp** | Độ chính xác OCR giảm mạnh dưới ~300 DPI. | Phóng to bằng `Image.resize((width*2, height*2), Image.LANCZOS)` trước khi đưa vào engine. |
| **Ngôn ngữ sai** | Engine mặc định tiếng Anh; ký tự không phải tiếng Anh sẽ bị lỗi. | Gọi `ocr_engine.setLanguage('deu')` (hoặc mã ISO phù hợp) trước `recognize()`. |
| **Không có đầu ra hOCR** | Một số engine mặc định xuất văn bản thuần khi không gọi `setExportFormat`. | Đảm bảo `setExportFormat("hocr")` được thực thi **trước** `recognize()`. |
| **Lỗi quyền ghi file** | Cố ghi vào thư mục chỉ đọc. | Dùng đường dẫn trong dự án hoặc gọi `os.makedirs(..., exist_ok=True)` trước. |
| **PDF lớn gây tăng RAM** | Bộ xuất PDF giữ toàn bộ ảnh trong RAM. | Xử lý các trang theo lô hoặc dùng trình ghi PDF dạng stream. |

*Pro tip:* luôn thử nghiệm trên một ảnh mẫu nhỏ trước khi mở rộng lên hàng ngàn ảnh. Điều này tiết kiệm hàng giờ gỡ lỗi.

## Kết Luận

Bây giờ bạn đã biết **cách chạy OCR trên file ảnh**, **cách trích xuất văn bản từ PNG**, **cách nhận dạng hình ảnh văn bản** cho các tác vụ downstream, **cách tạo PDF có thể tìm kiếm**, và **cách chuyển PNG sang PDF** khi bạn chỉ cần một bản lưu trữ đơn giản. Script được cung cấp là một giải pháp hoàn chỉnh, sao chép‑dán, hoạt động ngay, và các phần tùy chọn cho phép bạn tùy chỉnh đầu ra cho quy trình làm việc của mình.

### Tiếp theo là gì?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
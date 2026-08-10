---
category: general
date: 2026-06-06
description: Cách OCR PDF và tạo các tệp PDF có thể tìm kiếm từ hình ảnh bằng Python.
  Học cách thêm văn bản có thể tìm kiếm và chuyển đổi hình ảnh sang PDF/A trong vài
  phút.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: vi
og_description: Cách OCR PDF từng bước. Học cách thêm văn bản có thể tìm kiếm và chuyển
  đổi hình ảnh sang PDF/A bằng một script Python đơn giản.
og_title: Cách OCR PDF – Hướng dẫn nhanh tạo PDF có thể tìm kiếm
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Cách OCR PDF trong Python – Tạo PDF có thể tìm kiếm từ hình ảnh
url: /vi/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách OCR PDF – Chuyển Hình Ảnh Quét Thành PDF Có Thể Tìm Kiếm

Bạn đã bao giờ tự hỏi **cách OCR PDF** khi bạn chỉ có một hình ảnh quét của hoá đơn hoặc biên lai chưa? Bạn không phải là người duy nhất. Ở nhiều văn phòng, tài liệu đến dưới dạng PNG hoặc JPEG phẳng, và bước tiếp theo—làm cho nội dung có thể tìm kiếm—cảm giác như một hộp đen.  

Tin tốt? Chỉ với vài dòng Python, bạn có thể **tạo PDF có thể tìm kiếm**, **thêm văn bản có thể tìm kiếm**, và thậm chí **chuyển đổi hình ảnh sang PDF/A** để lưu trữ lâu dài. Trong hướng dẫn này, chúng tôi sẽ đi qua từng bước, giải thích tại sao chúng quan trọng, và cung cấp cho bạn một script sẵn sàng chạy mà bạn có thể đưa vào bất kỳ dự án nào.

> **Mẹo chuyên nghiệp:** Cùng một cách tiếp cận cũng hoạt động cho các bản quét đa trang; chỉ cần lặp qua các tệp và engine sẽ thực hiện phần công việc nặng.

---

## Những Gì Bạn Cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có những thứ sau trên máy của mình:

| Yêu cầu | Tại sao quan trọng |
|-------------|----------------|
| Python 3.9 hoặc mới hơn | Cú pháp hiện đại và hỗ trợ thư viện tốt hơn |
| Engine OCR dựa trên `pdfium` (ví dụ, `pdfocr` hoặc SDK thương mại) | Xử lý cả nhận dạng hình ảnh và tạo PDF/A |
| Tệp hình ảnh (PNG, JPEG, TIFF) bạn muốn chuyển thành PDF có thể tìm kiếm | Nguồn của văn bản |
| Quyền ghi vào thư mục đầu ra | Để script có thể lưu PDF mới |

Nếu bạn chưa cài đặt SDK OCR, chạy:

```bash
pip install pdfocr   # replace with your vendor's package name
```

Xong rồi—không có phụ thuộc hệ thống phức tạp, chỉ cần một lệnh pip install.

---

## Cách OCR PDF – Tổng Quan

Ở mức cao, quy trình bao gồm ba hành động đơn giản:

1. **Nhận diện** văn bản trong hình ảnh đồng thời giữ nguyên đồ họa gốc.  
2. **Xuất** kết quả OCR cùng với hình ảnh gốc thành một **PDF/A có thể tìm kiếm** (phiên bản PDF thân thiện lưu trữ lâu dài).  
3. **Xác thực** rằng tệp kết quả chứa văn bản có thể chọn, có thể tìm kiếm được đặt lên trên ảnh gốc.

Dưới đây bạn sẽ thấy từng bước trong mã, kèm giải thích *tại sao* phía sau các lệnh.

---

## Bước 1: Nhận Diện Văn Bản Từ Hình Ảnh

Đầu tiên chúng ta yêu cầu engine OCR đọc các pixel và trả về một đối tượng kết quả chứa cả hình ảnh thô và văn bản đã trích xuất. Hãy nghĩ nó như engine “đọc” hoá đơn cho bạn.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Tại sao điều này quan trọng

- **Giữ nguyên đồ họa** có nghĩa là bố cục trực quan (bảng, logo, con dấu) vẫn giữ nguyên như khi máy quét chụp.  
- Đối tượng `result` thường chứa một lớp văn bản ẩn mà chúng ta sẽ nhúng vào PDF sau.  
- Sử dụng `recognize_image` thay vì `recognize_pdf` tránh một bước chuyển đổi thêm, giúp tăng tốc xử lý cho ảnh một trang.

#### Các biến thể phổ biến

- Nếu bạn có **TIFF đa trang**, truyền đường dẫn tệp trực tiếp; hầu hết các engine sẽ coi mỗi trang là một hình ảnh riêng.  
- Đối với các PDF đã chứa hình ảnh, bạn có thể gọi `engine.recognize_pdf("file.pdf")` và bỏ qua bước này hoàn toàn.

---

## Bước 2: Xuất Kết Quả OCR Thành PDF/A Có Thể Tìm Kiếm

Bây giờ chúng ta lấy `result` từ bước 1 và yêu cầu engine ghi một tệp mới. Cờ quan trọng ở đây là *PDF/A*—phiên bản PDF chuẩn ISO được thiết kế cho việc bảo quản lâu dài.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Tại sao điều này quan trọng

- **PDF có thể tìm kiếm**: Tệp đầu ra chứa một lớp văn bản ẩn, có thể chọn. Bạn có thể dùng Ctrl + F để tìm trong tài liệu.  
- **Tuân thủ PDF/A**: Một số tổ chức (pháp lý, tài chính) yêu cầu PDF/A cho hồ sơ kiểm toán; bước này tự động đáp ứng yêu cầu.  
- Phương pháp cũng **thêm văn bản có thể tìm kiếm** mà không làm phẳng hình ảnh, vì vậy độ trung thực hình ảnh vẫn hoàn hảo.

#### Trường hợp đặc biệt: Cần PDF thường thay vì PDF/A?

Nếu bạn không quan tâm đến PDF/A, thay `save_as_pdfa` bằng `save_as_pdf`. Phần còn lại của quy trình vẫn giữ nguyên.

---

## Bước 3: Xác Thực PDF Có Thể Tìm Kiếm

Kiểm tra nhanh giúp bạn tránh các lỗi bí ẩn sau này. Mở tệp đã tạo trong bất kỳ trình xem PDF nào, thử chọn một từ và sử dụng chức năng tìm kiếm.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Kết quả mong đợi

Khi bạn chạy script, console sẽ in:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Mở tệp, bạn sẽ thấy hình ảnh hoá đơn gốc với một lớp văn bản mờ, vô hình. Khi bạn tô sáng bất kỳ từ nào, sẽ thấy nó có thể chọn—**đó là văn bản có thể tìm kiếm** mà bạn vừa thêm.

---

## Thêm Văn Bản Có Thể Tìm Kiếm Vào PDF Đã Tồn Tại (Bonus)

Đôi khi bạn đã có một PDF nhưng cần **thêm văn bản có thể tìm kiếm** vào đó. Cùng engine có thể phủ kết quả OCR lên một PDF hiện có:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Ở đây `apply_to` hợp nhất lớp ẩn với các trang gốc, cho phép bạn **tạo PDF có thể tìm kiếm** mà không cần quét lại.

---

## Cạm Bẫy và Mẹo

| Cạm bẫy | Cách tránh |
|---------|------------|
| **Hình ảnh nguồn độ phân giải thấp** (< 150 dpi) | Tăng độ phân giải hoặc yêu cầu bản quét độ phân giải cao hơn; độ chính xác OCR giảm đáng kể dưới 150 dpi. |
| **Thiếu dữ liệu ngôn ngữ** | Cài đặt các gói ngôn ngữ phù hợp cho engine OCR (`pip install pdfocr[eng,spa]`). |
| **Thư mục đầu ra không thể ghi** | Chạy script với quyền đủ hoặc chọn thư mục khác. |
| **Xác thực PDF/A thất bại** | Đảm bảo bạn không nhúng phông chữ không hỗ trợ hoặc JavaScript; hầu hết SDK sẽ tự động xử lý khi bạn dùng `save_as_pdfa`. |

---

## Script Đầy Đủ – Giải Pháp Một Tệp

Dưới đây là một script tự chứa, kết nối mọi thứ lại với nhau. Sao chép‑dán, thay đổi các đường dẫn placeholder, và bạn đã sẵn sàng **chuyển đổi hình ảnh sang PDF/A** trong vài giây.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**Script này làm gì:**  
1. Tải engine OCR.  
2. Đọc hình ảnh đã chọn và trích xuất văn bản.  
3. Ghi một **PDF/A có thể tìm kiếm** mà bạn có thể ngay lập tức phân phối hoặc lưu trữ.  

Bạn có thể gói logic `main` vào một hàm xử lý toàn bộ thư mục—chỉ cần lặp qua `os.listdir()` và lặp lại ba bước cho mỗi tệp.

---

## Các Bước Tiếp Theo & Chủ Đề Liên Quan

Bây giờ bạn đã nắm vững **cách OCR PDF**, hãy xem xét khám phá các ý tưởng sau:

- **Xử lý hàng loạt:** Sử dụng `concurrent.futures` để OCR hàng chục hoá đơn đồng thời.  
- **Chèn metadata:** Thêm ngày tạo hoặc số hoá đơn vào metadata của PDF để dễ lập chỉ mục hơn.  
- **PDF hỗn hợp:** Kết hợp văn bản có thể tìm kiếm với hình ảnh gốc được nhúng để tạo “bản sao kỹ thuật số” của tài liệu giấy.  
- **Đầu ra thay thế:** Xuất ra **DOCX** hoặc **HTML** nếu hệ thống downstream cần định dạng có thể chỉnh sửa.

Mỗi mục trên đều dựa trên các khái niệm cốt lõi bạn vừa học—nhận diện, xuất, xác thực.

---

## Wrap‑Up

Tóm lại, bạn giờ đã biết **cách OCR PDF** bằng cách biến một hình ảnh đơn giản thành **PDF/A có thể tìm kiếm** chỉ với ba dòng Python. Script thực hiện phần công việc nặng, giữ nguyên đồ họa gốc, và cung cấp cho bạn một tài liệu tuân chuẩn mà bạn có thể tìm kiếm, lưu trữ hoặc chia sẻ.  

Hãy thử với hoá đơn, biên lai hoặc hợp đồng đã quét của bạn. Nếu gặp khó khăn, để lại bình luận bên dưới hoặc kiểm tra tài liệu chính thức của SDK—thường chứa nhiều ví dụ bổ sung. Chúc bạn lập trình vui vẻ, và tận hưởng khả năng mới giúp bất kỳ hình ảnh nào ngay lập tức có thể tìm kiếm!

![Ví dụ cách OCR PDF hiển thị hình ảnh gốc và lớp PDF có thể tìm kiếm](placeholder.png "Ví dụ cách OCR PDF")

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách OCR PDF trong .NET với Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Nhận dạng Văn bản PDF – Các thao tác OCR với Aspose.OCR cho Java](/ocr/english/java/ocr-operations/)
- [Chuyển Đổi Hình Ảnh sang PDF C# – Lưu Kết Quả OCR Đa Trang](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-31
description: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét bằng Python OCR. Học cách
  chuyển đổi PDF hình ảnh đã quét, chuyển đổi TIFF sang PDF và thêm lớp văn bản OCR
  trong vài phút.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: vi
og_description: Tạo PDF có thể tìm kiếm ngay lập tức. Hướng dẫn này chỉ cách chạy
  OCR, chuyển đổi PDF ảnh quét và thêm lớp văn bản OCR bằng một script Python duy
  nhất.
og_title: Tạo PDF có thể tìm kiếm bằng Python – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Tạo PDF có thể tìm kiếm bằng Python – Hướng dẫn từng bước
url: /vi/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm bằng Python – Hướng dẫn từng bước

Bạn đã bao giờ tự hỏi làm thế nào để **tạo PDF có thể tìm kiếm** từ một trang đã quét mà không phải dùng hàng chục công cụ? Bạn không phải là người duy nhất. Trong nhiều quy trình văn phòng, một tệp TIFF hoặc JPEG đã quét được lưu vào ổ chia sẻ, và người tiếp theo phải sao chép‑dán văn bản thủ công—đau đầu, dễ gây lỗi và tốn thời gian.  

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp lập trình sạch sẽ cho phép bạn **chuyển đổi PDF ảnh đã quét**, **chuyển đổi TIFF sang PDF**, và **thêm lớp văn bản OCR** trong một lần. Khi kết thúc, bạn sẽ có một script sẵn sàng sử dụng, chạy OCR, nhúng văn bản ẩn, và tạo ra một PDF có thể tìm kiếm mà bạn có thể lập chỉ mục, tìm kiếm hoặc chia sẻ một cách tự tin.

## Những gì bạn cần

- Python 3.9+ (bất kỳ phiên bản mới nào cũng hoạt động)
- `aspose-ocr` và `aspose-pdf` packages (cài đặt bằng `pip install aspose-ocr aspose-pdf`)
- Một tệp ảnh đã quét (`.tif`, `.png`, `.jpg`, hoặc thậm chí một trang PDF chỉ chứa hình ảnh)
- Một lượng RAM vừa đủ (engine OCR nhẹ; ngay cả laptop cũng xử lý được)

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Windows, cách dễ nhất để lấy các gói là chạy lệnh trong cửa sổ PowerShell được nâng quyền.

```bash
pip install aspose-ocr aspose-pdf
```

Bây giờ các điều kiện tiên quyết đã được giải quyết, chúng ta hãy đi sâu vào mã.

## Bước 1: Tạo một thể hiện OCR Engine – *create searchable pdf*

Điều đầu tiên chúng ta làm là khởi động OCR engine. Hãy nghĩ nó như bộ não sẽ đọc từng pixel và chuyển chúng thành ký tự.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Tại sao điều này quan trọng:** Khởi tạo engine chỉ một lần giúp giảm mức sử dụng bộ nhớ. Nếu bạn gọi `OcrEngine()` trong một vòng lặp cho mỗi trang, bạn sẽ nhanh chóng hết tài nguyên.

## Bước 2: Tải ảnh đã quét – *convert tiff to pdf* & *convert scanned image pdf*

Tiếp theo, chỉ định engine tới tệp bạn muốn xử lý. API chấp nhận bất kỳ hình ảnh raster nào, vì vậy TIFF hoạt động tốt như JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Nếu bạn có một PDF chỉ chứa ảnh đã quét, bạn vẫn có thể sử dụng `load_image` vì Aspose sẽ tự động trích xuất trang đầu tiên.

## Bước 3: Chuẩn bị tùy chọn lưu PDF – *add OCR text layer*

Ở đây chúng ta cấu hình cách PDF cuối cùng sẽ hiển thị. Cờ quan trọng là `create_searchable_pdf`; đặt nó thành `True` sẽ yêu cầu thư viện nhúng một lớp văn bản vô hình phản ánh nội dung hình ảnh.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Chức năng của lớp văn bản:** Khi bạn mở tệp kết quả trong Adobe Reader và cố gắng chọn văn bản, bạn sẽ thấy các ký tự ẩn. Các công cụ tìm kiếm cũng có thể lập chỉ mục chúng—hoàn hảo cho việc tuân thủ hoặc lưu trữ.

## Bước 4: Chạy OCR và Lưu – *how to run OCR* trong một lần gọi

Bây giờ phép màu xảy ra. Một lần gọi phương thức sẽ chạy engine nhận dạng và ghi PDF có thể tìm kiếm vào đĩa.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

Phương thức `recognize` trả về một đối tượng trạng thái mà bạn có thể kiểm tra lỗi, nhưng đối với hầu hết các kịch bản đơn giản, lời gọi đơn giản ở trên là đủ.

### Kết quả mong đợi

Chạy script sẽ in ra:

```
PDF saved as searchable PDF.
```

Nếu bạn mở `scanned_page_searchable.pdf` bạn sẽ thấy có thể chọn văn bản, sao chép‑dán, và thậm chí thực hiện tìm kiếm `Ctrl+F`. Đó là dấu hiệu của quy trình **create searchable pdf**.

## Script Hoàn chỉnh

Dưới đây là script hoàn chỉnh, sẵn sàng chạy. Chỉ cần thay thế các đường dẫn placeholder bằng vị trí tệp thực tế của bạn.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Lưu lại dưới tên `create_searchable_pdf.py` và thực thi:

```bash
python create_searchable_pdf.py
```

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

### 1️⃣ Tôi có thể xử lý PDF đa trang không?

Có. Sử dụng `ocr_engine.load_image("file.pdf")` và sau đó lặp qua mỗi trang bằng `ocr_engine.recognize(pdf_save_options, page_number)`. Thư viện sẽ tự động tạo một PDF có thể tìm kiếm đa trang.

### 2️⃣ Nếu tệp nguồn của tôi là TIFF độ phân giải cao (300 dpi+)?

DPI cao hơn cho độ chính xác OCR tốt hơn nhưng cũng tiêu tốn bộ nhớ lớn hơn. Nếu bạn gặp `MemoryError`, hãy giảm kích thước ảnh trước:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Làm thế nào để thay đổi ngôn ngữ của OCR?

Đặt thuộc tính `language` trên engine trước khi tải ảnh:

```python
ocr_engine.language = "fra"   # French
```

Danh sách đầy đủ các mã ngôn ngữ được hỗ trợ có trong tài liệu Aspose.

### 4️⃣ Nếu tôi cần giữ nguyên chất lượng ảnh gốc thì sao?

Lớp `PdfSaveOptions` có thuộc tính `compression`. Đặt nó thành `PdfCompression.None` để giữ nguyên dữ liệu raster như ban đầu.

```python
pdf_save_options.compression = "None"
```

## Mẹo cho Triển khai Sẵn sàng Sản xuất

- **Xử lý hàng loạt:** Đóng gói logic cốt lõi trong một hàm nhận danh sách đường dẫn tệp. Ghi lại mỗi lần thành công/ thất bại vào file CSV để theo dõi kiểm toán.
- **Song song:** Sử dụng `concurrent.futures.ThreadPoolExecutor` để chạy OCR trên nhiều lõi. Chỉ cần nhớ mỗi luồng cần một thể hiện `OcrEngine` riêng.
- **Bảo mật:** Nếu bạn xử lý tài liệu nhạy cảm, chạy script trong môi trường sandbox và xóa ngay các tệp tạm sau khi xử lý.

## Kết luận

Bây giờ bạn đã biết cách **tạo PDF có thể tìm kiếm** từ các ảnh đã quét bằng một script Python ngắn gọn. Bằng cách khởi tạo OCR engine, tải một TIFF (hoặc bất kỳ raster nào), cấu hình `PdfSaveOptions` để **thêm lớp văn bản OCR**, và cuối cùng gọi `recognize`, toàn bộ quy trình **convert scanned image pdf** và **convert TIFF to PDF** trở thành một lệnh duy nhất, có thể lặp lại.

Bước tiếp theo? Hãy thử nối script này với một file‑watcher để bất kỳ bản quét mới nào được thả vào thư mục sẽ tự động trở thành có thể tìm kiếm. Hoặc thử nghiệm các ngôn ngữ OCR khác nhau để hỗ trợ lưu trữ đa ngôn ngữ. Không giới hạn khi bạn kết hợp OCR với việc tạo PDF.

Có thêm câu hỏi về **cách chạy OCR** trong các ngôn ngữ hoặc framework khác? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ! 

![Sơ đồ hiển thị luồng từ ảnh đã quét → OCR engine → PDF có thể tìm kiếm (create searchable pdf)](searchable-pdf-flow.png "Create searchable pdf flow diagram")


## Bạn nên học gì tiếp theo?

- [Cách OCR PDF trong .NET với Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Chuyển đổi hình ảnh sang PDF C# – Lưu kết quả OCR đa trang](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Cách OCR văn bản hình ảnh với ngôn ngữ bằng Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
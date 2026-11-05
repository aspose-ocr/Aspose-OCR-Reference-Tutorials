---
category: general
date: 2026-06-19
description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Python OCR. Học cách chuyển
  OCR sang PDF, trích xuất văn bản từ hình ảnh và thực hiện OCR trên hình ảnh nhanh
  chóng.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: vi
og_description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Python OCR. Hướng dẫn này
  chỉ cách chuyển OCR sang PDF, trích xuất văn bản từ hình ảnh và thực hiện OCR trên
  hình ảnh.
og_title: Tạo PDF có thể tìm kiếm trong Python – Hướng dẫn lập trình đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Tạo PDF có thể tìm kiếm bằng Python – Hướng dẫn chi tiết từng bước
url: /vi/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm trong Python – Hướng dẫn đầy đủ từng bước

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một biên lai đã quét nhưng không biết bắt đầu từ đâu chưa? Bạn không đơn độc—nhiều nhà phát triển gặp cùng một rào cản khi họ lần đầu cố gắng chuyển một bức ảnh chứa văn bản thành một PDF mà bạn thực sự có thể tìm kiếm.  

Trong tutorial này chúng ta sẽ đi qua một giải pháp thực tế cho phép bạn **thực hiện OCR trên hình ảnh**, chuyển kết quả OCR thành **PDF có thể tìm kiếm**, và thậm chí trích xuất văn bản thô nếu bạn cần xử lý tiếp. Không có phần thừa, chỉ có một ví dụ hoạt động mà bạn có thể sao chép‑dán vào dự án ngay hôm nay.

## Những gì bạn sẽ học

- Cách thiết lập một engine OCR nhẹ trong Python  
- Các bước chính xác để **chuyển đổi OCR sang PDF** và lưu nó dưới dạng tài liệu có thể tìm kiếm  
- Các cách để **trích xuất văn bản từ hình ảnh** cho phân tích downstream  
- Mẹo xử lý các vấn đề thường gặp như hướng ảnh và tệp lớn  
- Một script hoàn chỉnh, có thể chạy được mà bạn có thể tùy chỉnh cho trường hợp sử dụng của mình

### Yêu cầu trước

- Python 3.8+ đã được cài đặt trên máy của bạn  
- Kiến thức cơ bản về pip và môi trường ảo (tùy chọn nhưng được khuyến nghị)  
- Một tệp hình ảnh (PNG, JPEG, v.v.) chứa văn bản rõ ràng, có thể máy đọc được  

Nếu bạn đã có những thứ trên, hãy bắt đầu ngay.

## Bước 1: Cài đặt Thư viện Yêu cầu

Đoạn mã mẫu bạn đã thấy trước đó sử dụng một gói `ocr` giả tưởng, nhưng cùng một ý tưởng cũng áp dụng cho các thư viện thực tế như **EasyOCR**, **pytesseract**, hoặc **pdfminer.six**. Trong hướng dẫn này chúng ta sẽ dùng **EasyOCR** vì nó thuần Python, hỗ trợ nhiều ngôn ngữ, và cung cấp một phương pháp chuyển PDF tiện lợi thông qua một helper phụ trợ.

```bash
pip install easyocr pillow
```

> **Pro tip:** Cài đặt trong môi trường ảo (`python -m venv venv && source venv/bin/activate`) để giữ các phụ thuộc gọn gàng.

## Bước 2: Khởi tạo Engine OCR – Thực hiện OCR trên hình ảnh

Bây giờ thư viện đã sẵn sàng, chúng ta tạo một engine OCR và chỉ định nó làm việc với văn bản tiếng Anh. Đây là nơi đầu tiên chúng ta **thực hiện OCR trên hình ảnh**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Tại sao chúng ta cần một đối tượng reader riêng? EasyOCR tải trước các mô hình ngôn ngữ, vì vậy việc tái sử dụng cùng một `reader` cho nhiều hình ảnh sẽ hiệu quả hơn rất nhiều so với việc khởi tạo lại mỗi lần.

## Bước 3: Tải hình ảnh – Trích xuất văn bản từ hình ảnh

Hãy đưa bức ảnh vào bộ nhớ. Bước này là nơi chúng ta **trích xuất văn bản từ hình ảnh** sau này, nhưng trước tiên chúng ta chỉ tải nó lên.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Nếu ảnh của bạn bị lộn ngược hoặc nghiêng, hãy cân nhắc sử dụng các phương thức `rotate` hoặc `transpose` của Pillow trước khi đưa vào engine OCR. Một kiểm tra nhanh bằng mắt có thể tiết kiệm cho bạn hàng giờ gỡ lỗi sau này.

## Bước 4: Chạy Engine OCR và Ghi nhận Kết quả

Đây là phần cốt lõi của quy trình—gửi ảnh tới engine OCR và nhận lại dữ liệu có cấu trúc.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

Cờ `detail=1` cung cấp cho chúng ta các bounding box, mà chúng ta sẽ cần khi sau này **chuyển đổi OCR sang PDF**. Nếu bạn chỉ quan tâm tới chuỗi thô, hãy đặt `detail=0`.

## Bước 5: Chuyển đổi Kết quả OCR thành PDF có thể tìm kiếm – Chuyển đổi OCR sang PDF

EasyOCR không cung cấp một trình ghi PDF trực tiếp, nhưng chúng ta có thể tự ghép PDF bằng Pillow và thư viện `reportlab`. Để tutorial nhẹ, chúng ta sẽ dùng `fpdf2`, cho phép nhúng ảnh gốc và phủ lên văn bản vô hình.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Điều gì vừa xảy ra? Chúng ta đặt ảnh đã quét làm lớp hiển thị, sau đó viết các từ đã nhận dạng lên trên bằng văn bản màu trắng hòa vào nền trắng. Các công cụ tìm kiếm vẫn đọc được lớp ẩn, vì vậy PDF trở nên **có thể tìm kiếm** mà không thay đổi giao diện hình ảnh.

## Bước 6: Lưu Dữ liệu PDF – Chuyển đổi Hình ảnh sang PDF

Nếu bạn muốn xử lý PDF trong bộ nhớ (ví dụ, gửi qua API), bạn có thể lấy dữ liệu byte thay vì ghi trực tiếp ra đĩa.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Dòng này minh họa quy trình truyền thống **chuyển đổi hình ảnh sang PDF**: bạn bắt đầu với một ảnh, chạy OCR, phủ văn bản, và cuối cùng xuất ra một luồng PDF.

## Bước 7: Xác minh Kết quả – Kiểm tra Nhanh

Sau khi chạy script, mở `receipt_searchable.pdf` trong bất kỳ trình xem PDF nào và thử hộp tìm kiếm (Ctrl + F). Gõ một từ bạn biết có trong biên lai—nếu nó nhảy đến vị trí đúng, bạn đã **tạo PDF có thể tìm kiếm** thành công!  

Nếu tìm kiếm thất bại, hãy kiểm tra lại:

1. Điểm tin cậy OCR (`conf`). Điểm thấp có thể nghĩa là ảnh mờ.  
2. Tọa độ bounding box—đôi khi EasyOCR báo chúng theo hướng khác.  
3. Trình xem PDF không được đặt ở chế độ “chỉ ảnh” (hiếm, nhưng một số trình có tùy chọn này).

## Kịch bản Hoạt động Đầy đủ

Kết hợp mọi thứ lại, đây là file Python hoàn chỉnh, sẵn sàng chạy:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Lưu file này dưới tên `searchable_pdf.py`, thay thế các placeholder `YOUR_DIRECTORY` bằng đường dẫn thực tế, và chạy:

```bash
python searchable_pdf.py
```

Bạn sẽ thấy thông báo xác nhận và một PDF có thể tìm kiếm mới xuất hiện trong thư mục của mình.

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

**Nếu ảnh là màu thì sao?**  
EasyOCR hoạt động với cả ảnh xám và màu, nhưng chuyển sang xám (`pil_image.convert("L")`) đôi khi cải thiện độ chính xác trên các bản quét nhiễu.

**Tôi có thể xử lý PDF đa trang không?**  
Có—lặp qua mỗi ảnh trang, chạy các bước OCR, và thêm mỗi trang vào cùng một đối tượng `FPDF`. Chỉ cần nhớ đặt lại con trỏ (`self.add_page()`) cho mỗi ảnh mới.

**Có cách nào giữ lớp văn bản gốc thay vì văn bản trắng vô hình không?**  
Nếu bạn cần một PDF “văn bản‑dưới‑ảnh” thực sự (ví dụ, cho khả năng truy cập), hãy cân nhắc dùng `pdfminer` hoặc `pikepdf` để nhúng lớp văn bản ẩn với các thẻ PDF thích hợp. Đây là kỹ thuật nâng cao, nhưng nguyên tắc vẫn giống: ảnh nền + phủ văn bản.

**Nếu độ tin cậy OCR thấp thì sao?**  
Bạn có thể lọc bỏ các từ có độ tin cậy thấp:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Tổng kết – Những gì chúng ta đã đạt được

Chúng ta bắt đầu với một ảnh biên lai đơn giản, **thực hiện OCR trên hình ảnh**, trích xuất các chuỗi đã nhận dạng, và cuối cùng **tạo PDF có thể tìm kiếm** hoạt động như bất kỳ tài liệu quét chuyên nghiệp nào. Quy trình đã bao phủ mọi từ khóa phụ—**chuyển đổi OCR sang PDF**, **trích xuất văn bản từ hình ảnh**, **chuyển đổi hình ảnh sang PDF**, và **thực hiện OCR trên hình ảnh**—do đó bạn giờ có một bộ công cụ tái sử dụng cho bất kỳ dự án tương tự nào.

### Các bước Tiếp theo

- Thử nghiệm với các ngôn ngữ khác bằng cách truyền mã ISO của chúng vào `easyocr.Reader(['en', 'es'])`.  
- Thay EasyOCR bằng Tesseract nếu bạn cần một giải pháp hoàn toàn offline; phần còn lại của pipeline vẫn giữ nguyên.  
- Thêm trực quan hoá độ tin cậy OCR (vẽ bounding box lên ảnh) để gỡ lỗi các bản quét có vấn đề.  

Bạn có một cách tiếp cận mới muốn chia sẻ? Hãy để lại bình luận, fork

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn Từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Chuyển Đổi Hình ảnh sang PDF C# – Lưu Kết quả OCR Đa Trang](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Cách OCR Hình ảnh – Thực hiện OCR trên Hình ảnh trong Nhận dạng Ảnh OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
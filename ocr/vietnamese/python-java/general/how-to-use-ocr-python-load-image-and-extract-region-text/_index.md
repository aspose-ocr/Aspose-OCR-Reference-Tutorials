---
category: general
date: 2026-06-25
description: Cách sử dụng OCR trong Python – học cách tải ảnh cho OCR, nhận dạng văn
  bản trong vùng và trích xuất nhanh văn bản vùng.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: vi
og_description: Cách sử dụng OCR trong Python – hướng dẫn từng bước để tải ảnh, nhận
  dạng văn bản trong một khu vực cụ thể và trích xuất số hóa đơn.
og_title: 'Cách sử dụng OCR Python: Tải ảnh và trích xuất văn bản vùng'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Cách sử dụng OCR Python: Tải ảnh và trích xuất văn bản vùng'
url: /vi/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR Python: Tải Ảnh và Trích Xuất Văn Bản Vùng

**Cách sử dụng OCR trong Python** đơn giản hơn bạn nghĩ. Đã bao giờ bạn nhìn vào một hoá đơn đã quét và tự hỏi làm sao lấy được chỉ số hoá đơn mà không phải phân tích toàn bộ trang? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn này khi mới bắt đầu với nhận dạng ký tự quang học. Trong hướng dẫn này, chúng ta sẽ đi qua các bước tải ảnh cho OCR, định nghĩa một hình chữ nhật, nhận dạng văn bản trong vùng đó, và cuối cùng trích xuất văn bản vùng. Khi hoàn thành, bạn sẽ có một script sẵn sàng chạy để cô lập bất kỳ đoạn văn bản nào bạn cần.

> *Mẹo chuyên nghiệp:* Nếu bạn làm việc với PDF, hãy chuyển mỗi trang thành ảnh trước—hầu hết các thư viện OCR xử lý PNG/JPEG tốt nhất.

## Những Gì Bạn Cần Chuẩn Bị

- Python 3.8+ (khuyến nghị dùng phiên bản ổn định mới nhất)  
- Thư viện OCR cung cấp lớp `OcrEngine` (ví dụ: **ocr** từ `pip install ocr-lib`)  
- Một ảnh mẫu—ở đây chúng ta sẽ dùng `invoice.png` đặt trong thư mục bạn quản lý  
- Kiến thức cơ bản về hình chữ nhật (x, y, width, height)  

Không có phụ thuộc nặng, không cần GPU—chỉ dùng CPU thông thường, giúp dự án di động hơn.

---

## Cách Sử Dụng OCR: Khởi Tạo Engine (Bước 1)

Trước khi bất kỳ văn bản nào có thể được đọc, bạn cần một thể hiện của engine OCR. Hãy nghĩ nó như bộ não sẽ phân tích các mẫu pixel.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Lý do quan trọng:* Khởi tạo engine sẽ tải các mô hình ngôn ngữ và thiết lập cấu hình mặc định. Bỏ qua bước này sẽ gây ra ngoại lệ ngay khi bạn gọi `recognize_region`.

---

## Tải Ảnh cho OCR (Bước 2)

Khi engine đã sẵn sàng, chúng ta cung cấp cho nó một ảnh. Phương thức `Image.load` của thư viện xử lý các định dạng phổ biến và chuẩn hoá bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Nếu tệp không tồn tại, Python sẽ ném ra `FileNotFoundError`. Đảm bảo đường dẫn là tuyệt đối hoặc tương đối so với thư mục làm việc của script.  

*Trường hợp đặc biệt:* Một số engine OCR yêu cầu ảnh ở dạng grayscale. Nếu bạn nhận thấy độ chính xác kém, hãy chuyển ảnh sang grayscale trước:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Nhận Dạng Văn Bản Trong Vùng (Bước 3)

Định nghĩa vùng là nơi bạn chỉ định cho engine *đâu* cần tìm kiếm. Lớp `Rectangle` nhận các giá trị kiểu floating‑point để đạt độ chính xác sub‑pixel, rất hữu ích khi làm việc với ảnh quét độ phân giải cao.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – tọa độ góc trên‑trái của hình chữ nhật (đơn vị pixel)  
- **width, height** – kích thước của hộp  

Bạn có thể tự hỏi làm sao tìm các số này. Cách nhanh là mở ảnh trong bất kỳ trình chỉnh sửa nào (ví dụ: GIMP hoặc Paint.NET) và dùng công cụ chọn để đọc tọa độ.  

*Vì sao không OCR toàn bộ trang?* Giới hạn khu vực sẽ giảm nhiễu, tăng tốc xử lý, và cải thiện đáng kể độ chính xác cho các trường nhỏ như số hoá đơn.

---

## Cách Trích Xuất Văn Bản Vùng (Bước 4)

Khi đã đặt vùng, yêu cầu engine chỉ nhận dạng phần đó. Đối tượng kết quả chứa văn bản thô và điểm tin cậy.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Nếu engine OCR hỗ trợ đa ngôn ngữ, bạn có thể truyền thêm mã ngôn ngữ tùy chọn:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Nhầm lẫn thường gặp:* Một số engine trả về danh sách các từ thay vì một chuỗi duy nhất. Trong trường hợp này, hãy nối chúng lại:

```python
text = " ".join(region_result.words)
```

---

## Xuất Số Hoá Đơn Đã Trích Xuất (Bước 5)

Cuối cùng, in ra—hoặc lưu—văn bản đã trích xuất. Bạn cũng có thể xử lý hậu kỳ chuỗi để loại bỏ khoảng trắng thừa hoặc ký tự không phải số.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Chạy script với một hình chữ nhật đã căn chỉnh đúng sẽ cho kết quả giống như:

```
Invoice number: 20231578
```

Nếu bạn nhận được ký tự rác, hãy kiểm tra lại tọa độ hình chữ nhật hoặc cân nhắc tăng độ phân giải ảnh.

---

## Ví Dụ Hoạt Động Đầy Đủ

Kết hợp tất cả lại, đây là một script tự chứa mà bạn có thể sao chép‑dán và chạy:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Lưu file dưới tên `extract_invoice.py`, thay `YOUR_DIRECTORY` bằng thư mục thực tế, và chạy:

```bash
python extract_invoice.py
```

Bạn sẽ thấy số hoá đơn được in ra console.

---

## Câu Hỏi Thường Gặp

**Hỏi: Nếu số hoá đơn được in bằng phông chữ fancy thì sao?**  
Đáp: Hầu hết các engine OCR hiện đại hỗ trợ đa dạng phông chữ, nhưng bạn có thể tăng độ chính xác bằng cách đào tạo mô hình ngôn ngữ tùy chỉnh hoặc tiền xử lý ảnh (ví dụ: áp dụng bộ lọc ngưỡng).

**Hỏi: Tôi có thể trích xuất nhiều trường cùng lúc không?**  
Đáp: Chắc chắn. Định nghĩa một danh sách các đối tượng `Rectangle`—mỗi trường một hình chữ nhật—và lặp qua chúng, lưu mỗi kết quả vào một dictionary.

**Hỏi: Điều này có hoạt động với PDF đa trang không?**  
Đáp: Chuyển mỗi trang thành ảnh trước (sử dụng `pdf2image` hoặc tương tự), sau đó áp dụng cùng một quy trình trích xuất dựa trên vùng cho từng trang.

---

## Kết Luận

Trong tutorial này, chúng ta đã tìm hiểu **cách sử dụng OCR** trong Python để tải ảnh, nhận dạng văn bản trong một vùng cụ thể, và trích xuất văn bản của vùng đó—rất phù hợp để lấy số hoá đơn, ID đơn hàng, hoặc bất kỳ đoạn dữ liệu nhỏ nào từ tài liệu đã quét. Bằng cách cô lập khu vực quan tâm, bạn sẽ có tốc độ, độ chính xác cao hơn và giảm bớt công việc hậu xử lý.

Sẵn sàng cho bước tiếp theo? Hãy thử mở rộng script để **tải ảnh cho OCR** từ một thư mục chứa nhiều hoá đơn, hoặc thử **nhận dạng văn bản trong vùng** cho các trường khác như ngày và tổng tiền. Mẫu code vẫn giống nhau—chỉ cần thay đổi tọa độ hình chữ nhật.

Nếu bạn gặp khó khăn hoặc có ý tưởng cải tiến, hãy để lại bình luận bên dưới. Chúc lập trình vui vẻ, và chúc các pipeline OCR của bạn luôn chính xác!

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
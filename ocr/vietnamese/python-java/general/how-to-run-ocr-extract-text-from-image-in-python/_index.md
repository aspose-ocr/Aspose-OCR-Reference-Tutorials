---
category: general
date: 2026-03-26
description: Cách chạy OCR trên tệp PNG và trích xuất văn bản từ hình ảnh bằng từ
  điển tùy chỉnh để cải thiện độ chính xác của OCR. Tìm hiểu cách tải hình ảnh cho
  OCR nhanh chóng.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: vi
og_description: Cách chạy OCR trên tệp PNG và trích xuất văn bản từ hình ảnh với từ
  điển tùy chỉnh để cải thiện độ chính xác của OCR. Hướng dẫn từng bước.
og_title: Cách chạy OCR – Trích xuất văn bản từ hình ảnh trong Python
tags:
- OCR
- Python
- Image Processing
title: Cách chạy OCR – Trích xuất văn bản từ hình ảnh trong Python
url: /vi/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Chạy OCR – Trích Xuất Văn Bản Từ Hình Ảnh trong Python

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một hoá đơn đã quét hoặc một ảnh chụp màn hình và nhận được văn bản sạch, có thể tìm kiếm chưa? Bạn không phải là người duy nhất. Trong nhiều dự án, nút thắt chỉ là việc tải ảnh lên để OCR và sau đó thuyết phục engine hiểu các từ ngữ chuyên ngành.  

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, **trích xuất văn bản từ các tệp hình ảnh**, cho bạn thấy cách **nhận dạng văn bản từ PNG**, và thậm chí trình bày các mẹo để **cải thiện độ chính xác OCR** bằng từ điển tùy chỉnh và ký tự đặc biệt. Khi kết thúc, bạn sẽ có một script độc lập mà bạn có thể đưa vào bất kỳ codebase Python nào.

## Những Gì Bạn Cần Chuẩn Bị

- Python 3.8+ (code sử dụng type hints nhưng vẫn chạy trên các phiên bản 3.x cũ hơn)
- Thư viện `ocr` đi kèm với engine OCR bạn đang nhắm tới (cài đặt qua `pip install ocr‑engine` – thay bằng tên gói thực tế)
- Một tệp hình ảnh (`input.png`) mà bạn muốn xử lý
- Tùy chọn: một tệp văn bản thuần (`invoice_terms.txt`) chứa các từ ngữ chuyên ngành, mỗi từ một dòng

Không có phụ thuộc bên ngoài nặng, không cần khóa API đám mây, chỉ cần một engine OCR cục bộ.

---

## Bước 1: Cài Đặt và Nhập Thư Viện OCR

Đầu tiên, chắc chắn rằng gói OCR đã được cài đặt. Nếu bạn đang dùng gói giả định `ocr-engine`, chạy:

```bash
pip install ocr-engine
```

Bây giờ nhập các lớp bạn sẽ cần:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng môi trường ảo, hãy kích hoạt nó trước khi cài đặt để giữ Python toàn cục của bạn sạch sẽ.

## Bước 2: Tạo Một Instance của Engine OCR

Việc tạo một đối tượng engine là điểm khởi đầu cho mọi nhiệm vụ OCR. Hãy nghĩ nó như việc bật phần cứng máy quét trong phần mềm.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Tại sao điều này quan trọng: engine giữ các cấu hình như gói ngôn ngữ, chế độ nhận dạng, và bất kỳ tài nguyên tùy chỉnh nào bạn sẽ gắn sau này. Không có nó, bạn không thể **load image for OCR** hay chạy pipeline nhận dạng.

## Bước 3: Tải Ảnh Bạn Muốn Nhận Diện

Ở đây chúng ta thực sự **load image for OCR**. Phương thức `Imaging.Image.load()` đọc tệp và chuyển đổi nó thành định dạng bitmap nội bộ mà engine mong đợi.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Nếu bạn có JPEG hoặc TIFF, cùng một phương thức vẫn hoạt động—chỉ cần đổi phần mở rộng. Engine sẽ tự động phát hiện định dạng.

> **Trường hợp đặc biệt:** Các ảnh rất lớn (hơn 5 MP) có thể gây tăng đột biến bộ nhớ. Hãy cân nhắc giảm kích thước bằng Pillow trước khi tải nếu gặp vấn đề hiệu năng.

## Bước 4: Cung Cấp Từ Điển Tùy Chỉnh Để Tăng Độ Chính Xác

Hầu hết các engine OCR đi kèm với mô hình ngôn ngữ chung. Đối với hoá đơn, biên lai, hoặc tài liệu pháp lý, bạn thường sẽ thấy các từ bị bỏ lỡ. Cung cấp danh sách từ tùy chỉnh cho engine biết “các thuật ngữ này là hợp lệ, coi chúng là đúng”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Các mục điển hình có thể là:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Thêm chúng sẽ cải thiện **improve OCR accuracy** một cách đáng kể—đặc biệt với các ký hiệu không phải ASCII.

## Bước 5: Thêm Các Ký Tự Đặc Biệt Không Có Trong Bộ Mặc Định

Nếu lĩnh vực của bạn sử dụng các ký hiệu như dấu Euro (€) hoặc ký tự Scandinavia Ø, bạn có thể thêm chúng một cách rõ ràng:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Engine bây giờ sẽ coi những glyph này là hợp lệ trong giai đoạn nhận dạng, giảm khả năng xuất hiện “rác” trong kết quả.

## Bước 6: Chạy Quy Trình OCR và Lấy Văn Bản

Cuối cùng, gọi bộ nhận dạng và lấy kết quả văn bản thuần. Lệnh `recognize()` trả về một đối tượng phong phú; chúng ta chỉ cần chuỗi thô cho hầu hết các trường hợp sử dụng.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Kết quả mong đợi** (được rút gọn để ngắn gọn):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Nếu đầu ra trông rối mắt, hãy kiểm tra lại rằng từ điển tùy chỉnh và ký tự đặc biệt đã được tải đúng.

---

## Tổng Quan Trực Quan

![sơ đồ cách chạy OCR](ocr-workflow.png){alt="sơ đồ cách chạy OCR"}

Sơ đồ trên minh họa luồng từ việc tải ảnh đến việc nhận được văn bản sạch, nhấn mạnh nơi bạn có thể chèn từ điển tùy chỉnh và bộ ký tự.

---

## Các Câu Hỏi Thường Gặp & Những Cạm Bẫy

### Có hoạt động với PDF đa trang không?

Có—chỉ cần chuyển mỗi trang thành PNG (sử dụng `pdf2image` hoặc tương tự) và đưa chúng tuần tự vào cùng một instance `ocr_engine`. Engine sẽ xử lý mỗi ảnh độc lập, vì vậy bạn sẽ nhận được một danh sách các chuỗi mà bạn có thể nối lại.

### Nếu ảnh bị xoay thì sao?

Hầu hết các engine OCR hiện đại tự động phát hiện hướng, nhưng bạn có thể ép buộc xoay bằng:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Làm sao xử lý các ngôn ngữ không phải tiếng Anh?

Thay đổi mô hình ngôn ngữ trước khi tải ảnh:

```python
ocr_engine.set_language("de")  # German
```

Đảm bảo rằng gói ngôn ngữ tương ứng đã được cài đặt.

---

## Toàn Bộ Script – Sẵn Sàng Sao Chép & Dán

Dưới đây là toàn bộ chương trình, sẵn sàng chạy sau khi bạn thay thế các đường dẫn placeholder.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Chạy nó bằng:

```bash
python run_ocr.py
```

Bạn sẽ thấy văn bản đã trích xuất được in ra console. Từ đó bạn có thể ghi vào tệp, đưa vào cơ sở dữ liệu, hoặc truyền cho các pipeline NLP tiếp theo.

---

## Tóm Tắt & Các Bước Tiếp Theo

Chúng ta đã bao quát **cách chạy OCR** trên PNG, cách **trích xuất văn bản từ hình ảnh**, và trình bày các cách thực tiễn để **nhận dạng văn bản từ PNG** đồng thời **cải thiện độ chính xác OCR** bằng từ điển và ký tự tùy chỉnh.  

Tiếp theo, hãy cân nhắc:

- **Xử lý hàng loạt:** Lặp qua một thư mục các ảnh.
- **Hậu xử lý:** Dùng regex để lấy số hoá đơn hoặc ngày tháng.
- **Tích hợp:** Kết nối script vào một API Flask để cung cấp dịch vụ OCR theo yêu cầu.

Nếu bạn muốn khám phá các chủ đề nâng cao hơn, hãy xem các tutorial về **load image for OCR** với tiền xử lý OpenCV, hoặc tìm hiểu các mô hình OCR dựa trên deep‑learning như Tesseract 4+ với các lớp LSTM.

---

### Tiếp Tục Thử Nghiệm!

Hãy thử thay `invoice_terms.txt` bằng danh sách thuật ngữ y tế, thêm ký tự Hy Lạp, hoặc đưa engine một bức ảnh độ phân giải thấp để xem độ chính xác có thể đạt tới mức nào. Bạn càng tinkering, bạn sẽ càng hiểu rõ các đánh đổi giữa tiền xử lý, từ vựng tùy chỉnh, và các thiết lập engine.

Chúc lập trình vui vẻ, và hy vọng kết quả OCR của bạn luôn sắc nét!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
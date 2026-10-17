---
category: general
date: 2026-06-22
description: Thực hiện OCR trên hình ảnh bằng Python chỉ trong vài dòng. Tìm hiểu
  cách tải hình ảnh cho OCR, nhận dạng văn bản từ PNG và sử dụng engine OCR một cách
  hiệu quả.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: vi
og_description: Thực hiện OCR trên hình ảnh nhanh chóng với Python. Hướng dẫn này
  cho thấy cách tải hình ảnh để OCR, nhận dạng văn bản từ PNG và sử dụng công cụ OCR
  với độ tin cậy.
og_title: Thực hiện OCR trên hình ảnh bằng Python – Hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Thực hiện OCR trên ảnh trong Python – Hướng dẫn đầy đủ
url: /vi/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên hình ảnh trong Python – Hướng dẫn đầy đủ

Bạn đã bao giờ cần **perform OCR on image** nhưng lại gặp khó khăn ngay từ dòng lệnh đầu tiên? Bạn không phải là người duy nhất. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **load image for OCR**, thiết lập một **OCR engine** nhẹ, và cuối cùng **recognize text from PNG** chỉ với một vài lệnh.

Chúng tôi sẽ bao phủ mọi thứ từ cài đặt thư viện đến điều chỉnh whitelist sao cho chỉ có chữ số và chữ hoa được nhận dạng. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy mà bạn có thể đưa vào bất kỳ dự án nào—không có bí ẩn, không có phần thừa.

## Những gì bạn sẽ học

- Cách **use OCR engine** một cách lập trình trong Python.  
- Các bước chính xác để **load image for OCR** từ thư mục cục bộ.  
- Tại sao và cách hạn chế nhận dạng chỉ với một bộ ký tự tùy chỉnh.  
- Cách **recognize text from PNG** và xử lý kết quả một cách an toàn.  

**Prerequisites:** Python 3.7+ đã được cài đặt, một terminal mà bạn thoải mái sử dụng, và một hình ảnh (ví dụ, `serial-number.png`) bạn muốn đọc. Không yêu cầu kinh nghiệm OCR trước.

---

## Thực hiện OCR trên hình ảnh – Khởi tạo OCR Engine

Điều đầu tiên bạn phải làm là tạo một thể hiện của OCR engine. Hãy nghĩ engine như bộ não sẽ phân tích các pixel và chuyển chúng thành ký tự.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* Không có engine thì không có gì để xử lý hình ảnh. Lớp `OcrEngine` gói gọn tất cả các công việc nặng—pre‑processing, segmentation, và character classification—vào một đối tượng duy nhất mà bạn có thể tái sử dụng.

---

## Tải hình ảnh cho OCR – Cung cấp tệp PNG

Bây giờ engine đã tồn tại, bạn cần cung cấp cho nó hình ảnh bạn muốn đọc. Thư viện yêu cầu một đối tượng `ImageStream`, mà bạn có thể tạo trực tiếp từ đường dẫn tệp.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Pro tip:* Giữ hình ảnh ở định dạng độ tương phản cao (văn bản đen trên nền trắng) và tránh các artefact nén; chúng có thể làm rối thuật toán OCR.

---

## Hạn chế ký tự – Whitelist chữ số và chữ hoa

Thường bạn chỉ quan tâm đến một tập con các ký tự—ví dụ, một số serial chỉ chứa A‑Z và 0‑9. Bằng cách thiết lập whitelist, bạn yêu cầu engine bỏ qua mọi thứ khác, điều này cải thiện độ chính xác đáng kể.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*What’s happening under the hood?* Engine tạo một bộ lọc loại bỏ bất kỳ glyph nào không có trong whitelist trước bước phân loại cuối cùng. Điều này đặc biệt hữu ích khi hình ảnh chứa nhiễu hoặc văn bản trang trí mà bạn không cần.

---

## Nhận dạng văn bản từ PNG – Chạy quy trình OCR

Với engine đã sẵn sàng và hình ảnh đã được tải, cuối cùng bạn có thể **perform OCR on image**. Lệnh `recognize()` chạy toàn bộ pipeline và trả về một đối tượng kết quả.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Nếu bạn tò mò về hiệu năng, phương pháp này thường hoàn thành trong vài trăm miligiây cho một PNG 300 × 200 px trên laptop hiện đại.

---

## Xuất và Xác minh – Lấy văn bản đã nhận dạng

Bước cuối cùng là trích xuất văn bản thuần từ đối tượng kết quả. Bất kỳ ký tự nào không khớp với whitelist sẽ tự động bị loại bỏ, vì vậy bạn nhận được một chuỗi sạch sẵn sàng cho các xử lý tiếp theo.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typical output:* `AB12C3D4E5` (giả sử hình ảnh chứa đúng số serial đó).  

Nếu đầu ra rỗng hoặc bị lỗi, hãy kiểm tra lại chất lượng hình ảnh và whitelist; một lỗi thường gặp là vô tình bỏ sót các ký tự cần thiết.

---

## Trường hợp góc cạnh & Những lỗi thường gặp

| Situation | What to Check | Suggested Fix |
|-----------|---------------|---------------|
| **File not found** | Sai đường dẫn hoặc tệp tin bị thiếu | Sử dụng `os.path.abspath` để xác minh đường dẫn đầy đủ trước khi gọi `set_image`. |
| **Low contrast image** | Văn bản hòa lẫn với nền | Áp dụng ngưỡng đơn giản (`Pillow` hoặc `OpenCV`) trước khi đưa hình ảnh vào engine. |
| **Unexpected characters** | Whitelist quá hạn chế | Thêm các ký tự thiếu vào chuỗi whitelist. |
| **Large images** | Nhận dạng chậm | Thay đổi kích thước hình ảnh tối đa 1024 px chiều rộng; chất lượng OCR thường vẫn cao. |

---

## Script đầy đủ – Sẵn sàng chạy

Dưới đây là script hoàn chỉnh, tự chứa, kết nối tất cả các phần lại với nhau. Lưu lại dưới tên `ocr_demo.py`, thay thế `YOUR_DIRECTORY` bằng thư mục thực tế, và chạy `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Expected console output* (khi PNG chứa `SN12345`):

```
Recognized text: SN12345
```

---

## Kết luận

Bây giờ bạn đã biết chính xác cách **perform OCR on image** trong Python, từ **loading image for OCR** đến **recognize text from PNG** và cuối cùng trích xuất kết quả sạch bằng một **OCR engine** có thể tùy chỉnh. Cách tiếp cận này đơn giản, mở rộng được, và hoạt động ngay lập tức cho hầu hết các quét kiểu số serial.

Tiếp theo? Hãy thử thay đổi whitelist sang chữ thường, thử nghiệm với các định dạng hình ảnh khác (JPEG, BMP), hoặc tích hợp script vào quy trình xử lý hàng loạt. Mẫu tương tự—engine → image → settings → recognize → output—áp dụng cho hầu hết mọi nhiệm vụ OCR mà bạn sẽ gặp.

Có câu hỏi hoặc hình ảnh lạ khiến bạn gặp khó khăn? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ! 

![Diagram illustrating the steps to perform OCR on image using Python](https://example.com/ocr-flow.png "Diagram showing how to perform OCR on image with a Python OCR engine")

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Chuyển đổi hình ảnh thành văn bản – Thực hiện OCR trên hình ảnh từ URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Cách sử dụng AspOCR: Tiền xử lý bộ lọc OCR cho hình ảnh trong .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Cách trích xuất văn bản từ hình ảnh bằng cách chuẩn bị các hình chữ nhật trong OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
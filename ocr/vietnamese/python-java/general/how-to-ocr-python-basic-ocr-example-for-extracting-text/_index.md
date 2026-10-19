---
category: general
date: 2026-04-26
description: 'cách sử dụng OCR trong Python: Học cách trích xuất văn bản từ hình ảnh
  và đọc tệp TIFF bằng Python bằng một ví dụ OCR cơ bản. Bao gồm mã nhanh, có thể
  chạy ngay.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: vi
og_description: 'cách sử dụng OCR trong Python: Hướng dẫn từng bước cho thấy cách
  trích xuất văn bản từ hình ảnh, đọc tệp TIFF bằng Python và chuyển đổi văn bản từ
  ảnh đã quét bằng một script đơn giản, có thể chạy được.'
og_title: Cách sử dụng OCR trong Python – Ví dụ OCR cơ bản để trích xuất văn bản
tags:
- OCR
- Python
- Image Processing
title: cách sử dụng OCR trong Python – Ví dụ OCR cơ bản để trích xuất văn bản
url: /vi/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách ocr python – Ví dụ OCR Cơ bản để Trích xuất Văn bản

Bạn đã bao giờ tự hỏi **cách ocr python** khi có một tệp TIFF đã quét nằm trên bàn làm việc chưa? Bạn không phải là người duy nhất đang nhìn vào một loạt các tệp ảnh và hỏi, “Làm sao tôi lấy được chữ từ đây?” Tin tốt là việc biến một bức ảnh thành văn bản thuần túy trở nên cực kỳ dễ dàng với thư viện phù hợp và một vài bước rõ ràng.

Trong tutorial này, chúng ta sẽ đi qua một **ví dụ OCR cơ bản** đọc tệp TIFF, trích xuất văn bản và in ra console. Khi kết thúc, bạn sẽ biết chính xác cách **trích xuất văn bản từ ảnh**, cách xử lý các đặc thù của định dạng TIFF, và những gì cần điều chỉnh nếu bạn muốn **chuyển đổi văn bản ảnh đã quét** thành dạng hữu ích hơn. Không có phép thuật ẩn – chỉ là Python đơn giản mà bạn có thể sao chép‑dán và chạy ngay hôm nay.

## Những gì bạn cần

- Python 3.9+ đã được cài đặt (phiên bản ổn định mới nhất là tốt nhất).
- Thư viện OCR có thể cài đặt qua pip. Trong hướng dẫn này chúng tôi sẽ sử dụng gói giả lập `aocr` mô phỏng các công cụ phổ biến như Tesseract; bạn có thể thay thế bằng `pytesseract` hoặc `easyocr` sau.
- Một ảnh TIFF bạn muốn xử lý – đặt tên là `input.tiff` và đặt vào thư mục mà bạn sẽ tham chiếu trong mã.
- Kiến thức cơ bản về dòng lệnh (chỉ để cài đặt gói).

Đó là tất cả. Không có phụ thuộc nặng, không có container Docker, chỉ một vài dòng mã.

## Bước 1 – Cài đặt và Nhập các phụ thuộc (how to ocr python)

Đầu tiên, lấy gói OCR. Mở terminal và chạy:

```bash
pip install aocr
```

Nếu bạn muốn một thư viện thực tế, thay `aocr` bằng `pytesseract` và cài đặt engine Tesseract riêng.

Bây giờ nhập những gì chúng ta cần. Lớp `Path` từ `pathlib` cung cấp cách sạch sẽ để làm việc với đường dẫn tệp trên mọi hệ điều hành.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Tại sao dùng `Path`?* Vì nó trừu tượng hoá các dấu gạch chéo (`/` vs `\`) và cho phép bạn nối thư mục mà không lo về hệ điều hành nền. Chi tiết nhỏ này thường cứu bạn khỏi những rắc rối khi chuyển script sang máy CI.

## Bước 2 – Tạo Instance cho Engine OCR (basic ocr example)

Tiếp theo, khởi động engine OCR. Hãy nghĩ `OcrEngine` như bộ não sẽ đọc ảnh và đưa ra các ký tự.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

Hầu hết các thư viện OCR cho phép bạn tinh chỉnh ngôn ngữ, DPI, hoặc ngưỡng confidence ở đây. Đối với **ví dụ OCR cơ bản** này, chúng ta sẽ dùng các giá trị mặc định, nhưng bạn có thể khám phá `ocr_engine.config` sau nếu cần xử lý tài liệu đa ngôn ngữ.

## Bước 3 – Tải ảnh TIFF của bạn (read tiff file python)

Đây là nơi phần **read tiff file python** xuất hiện. TIFF có thể có nhiều trang, nhưng `Image.load` sẽ lấy trang đầu tiên theo mặc định — hoàn hảo cho một bản quét một trang.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Thay `"YOUR_DIRECTORY"` bằng thư mục thực tế chứa `input.tiff`. Nếu bạn không chắc script chạy ở đâu, `Path.cwd()` sẽ in ra thư mục làm việc hiện tại — rất hữu ích để debug vấn đề đường dẫn.

## Bước 4 – Chạy quy trình OCR (extract text from image)

Bây giờ phép màu xảy ra. Gọi `process()` sẽ đưa ảnh qua pipeline OCR và trả về một đối tượng kết quả.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Ở phía sau, engine có thể đang chuyển ảnh sang grayscale, áp dụng threshold, và đưa vào mạng nơ‑ron. Bạn không cần quản lý các bước này; thư viện đã trừu tượng hoá chúng.

## Bước 5 – In ra Văn bản đã Nhận dạng (convert scanned image text)

Cuối cùng, xuất ra văn bản. Trong các dự án thực tế, bạn có thể ghi vào file hoặc cơ sở dữ liệu, nhưng việc in ra giúp ví dụ gọn gàng.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Khi bạn chạy script, bạn sẽ thấy một kết quả giống như:

```
Hello, world!
This is a sample scanned document.
```

Nếu đầu ra bị rối, hãy kiểm tra lại ảnh nguồn có rõ ràng không và ngôn ngữ OCR có khớp với văn bản không.

## Script Hoàn chỉnh

Kết hợp tất cả lại, đây là chương trình hoàn chỉnh, sẵn sàng chạy:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Kết quả Dự kiến

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Nếu bạn cần **chuyển đổi văn bản ảnh đã quét** thành PDF có thể tìm kiếm, bạn có thể truyền `ocr_result.text` vào một trình tạo PDF như `reportlab` — nhưng đó là một tutorial riêng.

## Những Cạm Bẫy Thường Gặp & Mẹo Chuyên Nghiệp

- **Quét độ phân giải thấp**: OCR gặp khó khăn dưới 150 DPI. Nếu TIFF của bạn mờ, hãy tăng độ phân giải trước bằng Pillow (`Image.open(...).resize(...)`).
- **Nhiều trang**: Đối với TIFF đa trang, lặp qua `Image.load_multi_page()` (nếu thư viện hỗ trợ) và nối các kết quả lại.
- **Hỗ trợ ngôn ngữ**: Nhiều engine mặc định là tiếng Anh. Đặt `ocr_engine.language = "spa"` cho tiếng Tây Ban Nha, ví dụ.
- **Xử lý khoảng trắng**: OCR thường thêm các ngắt dòng không mong muốn. Sử dụng `str.splitlines()` hoặc biểu thức chính quy để làm sạch kết quả.
- **Hiệu năng**: Khi xử lý hàng loạt, tái sử dụng một instance `OcrEngine` duy nhất thay vì tạo mới cho mỗi tệp.

## Mở rộng Ví dụ

Bây giờ bạn đã thành thạo **cách ocr python** cho một ảnh đơn, hãy xem các bước tiếp theo:

1. **Xử lý hàng loạt** – Lặp qua một thư mục chứa các TIFF và ghi mỗi kết quả vào tệp `.txt`.
2. **Tích hợp với Pandas** – Lưu trữ văn bản đã trích xuất cùng với siêu dữ liệu để phân tích nhanh.
3. **Phương pháp kết hợp** – Kết hợp OCR với các thư viện NLP như `spaCy` để trích xuất thực thể (tên, ngày, số tiền) từ hoá đơn quét.
4. **Định dạng tệp thay thế** – Thay `Image.load` bằng `Image.from_bytes` để xử lý ảnh đến từ API hoặc cơ sở dữ liệu.

Tất cả những điều này dựa trên ý tưởng cốt lõi của **trích xuất văn bản từ ảnh** và **chuyển đổi văn bản ảnh đã quét** thành thứ mà máy móc có thể hiểu.

## Kết luận

Chúng ta đã đi qua một **ví dụ OCR cơ bản** rõ ràng, từ đầu đến cuối, cho thấy **cách ocr python**, cách **đọc tệp tiff bằng python**, và cách **trích xuất văn bản từ ảnh** chỉ với vài dòng mã. Script tự chứa, bao gồm xử lý lỗi, và in kết quả trực tiếp, tạo nền tảng vững chắc cho bất kỳ dự án nào cần biến tài liệu quét thành văn bản có thể chỉnh sửa.

Hãy thoải mái thử nghiệm — thay đổi backend OCR, tinh chỉnh tiền xử lý, hoặc kết nối đầu ra vào quy trình downstream. Khi bạn có thể tin cậy **chuyển đổi văn bản ảnh đã quét** thành dữ liệu có thể tìm kiếm, mọi khả năng đều mở ra.

Có câu hỏi về các trường hợp đặc biệt, gói ngôn ngữ, hay tối ưu hiệu năng? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ! 

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
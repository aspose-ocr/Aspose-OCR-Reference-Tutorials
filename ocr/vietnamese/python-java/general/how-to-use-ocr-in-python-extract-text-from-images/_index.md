---
category: general
date: 2026-06-16
description: Cách sử dụng OCR trong Python để trích xuất văn bản từ các tệp hình ảnh
  như PNG. Tìm hiểu quy trình chuyển đổi hình ảnh sang văn bản từng bước với Aspose
  OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: vi
og_description: Cách sử dụng OCR trong Python để trích xuất văn bản từ hình ảnh. Hướng
  dẫn này sẽ chỉ cho bạn cách chuyển đổi các tệp PNG thành văn bản có thể tìm kiếm
  bằng Aspose OCR.
og_title: Cách sử dụng OCR trong Python – Trích xuất văn bản từ hình ảnh
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: Cách sử dụng OCR trong Python – Trích xuất văn bản từ hình ảnh
url: /vi/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong Python – Trích Xuất Văn Bản từ Hình Ảnh

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** trong một dự án Python chưa? Bạn không phải là người duy nhất. Dù bạn đang xây dựng một công cụ quét biên lai, một hệ thống lưu trữ tài liệu, hay chỉ đơn giản là tò mò về cách chuyển ảnh chụp màn hình thành văn bản có thể chỉnh sửa, khả năng **trích xuất văn bản từ hình ảnh** là một bước đột phá.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình — từ cài đặt thư viện Aspose OCR đến việc đọc văn bản từ tệp PNG — để bạn có thể **chuyển đổi hình ảnh thành văn bản** chỉ với vài dòng code. Khi hoàn thành, bạn sẽ biết chính xác cách **đọc văn bản từ PNG** và thậm chí tự động xử lý nội dung đa ngôn ngữ.

> **Mẹo chuyên nghiệp:** Tính năng tự động phát hiện ngôn ngữ của Aspose OCR có nghĩa là bạn không cần phải đoán trước ngôn ngữ — hoàn hảo cho các ứng dụng toàn cầu.

## Những Điều Cần Chuẩn Bị

- Python 3.8+ (phiên bản ổn định mới nhất cũng được)
- Tệp giấy phép Aspose OCR hợp lệ (`Aspose.OCR.lic`). Bản dùng thử miễn phí đủ cho việc thử nghiệm, nhưng giấy phép chính thức sẽ loại bỏ các giới hạn đánh giá.
- Gói Aspose OCR được cài đặt qua `pip`:

```bash
pip install aspose-ocr
```

- Tệp hình ảnh bạn muốn xử lý — chúng ta sẽ dùng `sample-multi-lang.png` làm ví dụ.

Có sẵn các yêu cầu trên sẽ giúp quá trình diễn ra suôn sẻ và tránh các lỗi “module not found” bất ngờ sau này.

![Quy trình sử dụng OCR trong Python](https://example.com/ocr-workflow.png "Cách sử dụng OCR trong Python – minh họa từng bước")

*Văn bản thay thế hình ảnh: Sơ đồ mô tả cách sử dụng OCR trong Python để trích xuất văn bản từ một hình ảnh.*

## Bước 1: Áp Dụng Giấy Phép Aspose OCR của Bạn (Cần Thiết Một Lần cho Mỗi Ứng Dụng)

Điều đầu tiên mà bất kỳ dự án OCR nghiêm túc nào làm là tải giấy phép. Nếu không, Aspose sẽ đưa ra cảnh báo và giới hạn số trang bạn có thể xử lý.

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **Tại sao điều này quan trọng:** Tải giấy phép ngay từ đầu đảm bảo rằng engine **ocr image to text python** hoạt động ở tốc độ tối đa và không có watermark. Hãy nghĩ nó như việc mở khóa các tính năng cao cấp trước khi bạn bắt đầu chuyển đổi.

## Bước 2: Tạo Engine OCR và Bật Tự Động Phát Hiện Ngôn Ngữ

Bây giờ chúng ta khởi tạo engine cốt lõi. Bật `language_auto_detect` là rất quan trọng khi bạn không biết hình ảnh chứa tiếng Anh, tiếng Tây Ban Nha, tiếng Trung hay hỗn hợp các ngôn ngữ nào.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

Nếu bạn *biết* ngôn ngữ từ trước, bạn có thể đặt `ocr_engine.language = "English"` (hoặc bất kỳ mã ISO nào được hỗ trợ) để tăng tốc một chút. Nhưng đối với tiện ích “đọc văn bản từ PNG” chung, tự động phát hiện là lựa chọn an toàn nhất.

## Bước 3: Tải Hình Ảnh Bạn Muốn Xử Lý

Aspose OCR hỗ trợ nhiều định dạng — PNG, JPEG, BMP, TIFF, v.v. Hãy tải một tệp PNG chứa nhiều ngôn ngữ.

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **Trường hợp đặc biệt:** Nếu hình ảnh quá lớn (hơn vài megabyte), bạn có thể muốn giảm kích thước trước để cải thiện hiệu năng. Aspose cung cấp `ocr_image.resize(width, height)` cho mục đích này.

## Bước 4: Thực Hiện Nhận Diện OCR

Khi mọi thứ đã được kết nối, việc trích xuất văn bản thực tế chỉ là một lời gọi phương thức duy nhất. Đối tượng kết quả sẽ cung cấp cho bạn cả văn bản đã nhận dạng và ngôn ngữ được phát hiện.

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

Trong nền, Aspose chạy các mạng nơ-ron tinh vi và thuật toán khớp mẫu để chuyển mỗi cụm pixel thành ký tự. Tất cả công việc nặng được thực hiện bằng mã gốc, vì vậy bạn nhận được **OCR nhanh, chính xác** ngay cả trên phần cứng vừa phải.

## Bước 5: Hiển Thị Ngôn Ngữ Được Phát Hiện và Văn Bản Đã Nhận Dạng

Cuối cùng, hãy in ra những gì chúng ta nhận được. Thuộc tính `detected_language` cho bạn biết Aspose đã đoán ngôn ngữ nào, và `text` chứa toàn bộ bản sao.

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### Kết Quả Dự Kiến

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

Nếu bạn chạy script trên một hình ảnh chứa cả tiếng Anh và tiếng Nhật, bạn sẽ thấy ngôn ngữ tự động chuyển đổi — nhờ tính năng tự động phát hiện mà chúng ta đã bật ở trên.

## Xử Lý Các Trường Hợp Gặp Phải Thông Thường

### 1. Không Tìm Thấy Giấy Phép

Nếu bạn gặp lỗi như `License file not found`, hãy kiểm tra lại đường dẫn bạn truyền cho `set_license`. Sử dụng chuỗi thô (`r"..."`) giúp tránh các lỗi ký tự escape trên Windows.

### 2. Kết Quả Trống

Một `ocr_result.text` trống thường có nghĩa là hình ảnh quá nhiễu hoặc văn bản quá mờ. Hãy thử tăng độ tương phản của hình ảnh:

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. Phát Hiện Ngôn Ngữ Sai

Nếu tính năng tự động phát hiện chọn sai ngôn ngữ, bạn có thể buộc một ngôn ngữ cụ thể:

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## Mở Rộng Ví Dụ: Xử Lý Hàng Loạt Nhiều Tệp PNG

Thường bạn sẽ muốn **chuyển đổi hình ảnh thành văn bản** cho toàn bộ thư mục, không chỉ một tệp duy nhất. Dưới đây là một vòng lặp nhanh xử lý mọi PNG trong một thư mục:

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

Đoạn mã này minh họa cách thực tế để **trích xuất văn bản từ hình ảnh** hàng loạt, một yêu cầu phổ biến cho các quy trình số hoá tài liệu.

## Script Hoàn Chỉnh Hoạt Động

Kết hợp tất cả lại, đây là một tệp duy nhất bạn có thể chạy từ đầu đến cuối:

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

Lưu lại dưới tên `ocr_demo.py`, chạy `python ocr_demo.py`, và bạn sẽ thấy ngôn ngữ và văn bản được in ra console.

## Kết Luận

Chúng tôi đã trình bày **cách sử dụng OCR** trong Python từ đầu đến cuối, cho bạn thấy cách **trích xuất văn bản từ hình ảnh**, **đọc văn bản từ PNG**, và nói chung **chuyển đổi hình ảnh thành văn bản** bằng engine mạnh mẽ của Aspose. Bằng cách tải giấy phép, bật tự động phát hiện ngôn ngữ, và đưa một hình ảnh vào `OcrEngine`, bạn sẽ có được văn bản sạch, có thể tìm kiếm trong vài giây.

Tiếp theo là gì? Hãy thử thay Aspose bằng một giải pháp mã nguồn mở như Tesseract để so sánh độ chính xác, thử nghiệm với đầu vào PDF, hoặc tích hợp bước OCR vào một API Flask để xử lý hình ảnh ngay lập tức. Không gì là không thể khi bạn nắm vững các kiến thức cơ bản của **ocr image to text python**.

Có câu hỏi nào về việc xử lý phông chữ khó, tối ưu hiệu năng, hoặc giấy phép? Hãy để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ code hoàn chỉnh kèm giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích Xuất Văn Bản từ Hình Ảnh với Aspose OCR – Hướng Dẫn Từng Bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Trích Xuất Văn Bản từ Hình Ảnh – Tối Ưu Hóa OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)
- [Trích Xuất Văn Bản Hình Ảnh C# với Lựa Chọn Ngôn Ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
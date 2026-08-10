---
category: general
date: 2026-01-12
description: Cách thực hiện OCR và chuyển đổi hình ảnh thành văn bản nhanh chóng.
  Tìm hiểu cách nhận dạng ký tự đặc biệt, trích xuất văn bản từ hình ảnh và tải hình
  ảnh cho OCR với một ví dụ Python đầy đủ.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: vi
og_description: Cách thực hiện OCR trong Python, chuyển đổi hình ảnh thành văn bản
  và nhận dạng ký tự đặc biệt. Hãy theo dõi hướng dẫn thực hành này để trích xuất
  văn bản từ hình ảnh.
og_title: Cách thực hiện OCR trong Python – Hướng dẫn đầy đủ
tags:
- OCR
- Python
- Image Processing
title: Cách thực hiện OCR trong Python – Hướng dẫn từng bước
url: /vi/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện OCR trong Python – Hướng Dẫn Từng Bước

Bạn đã bao giờ cần **perform OCR** trên một ảnh chụp màn hình chứa cả ký tự Latin và Cyrillic chưa? Bạn không phải là người duy nhất. Trong nhiều dự án—cho dù là số hoá biên lai, lập chỉ mục tài liệu đa ngôn ngữ, hay xây dựng một kho lưu trữ có thể tìm kiếm—**how to perform OCR** nhanh chóng trở thành câu hỏi quan trọng nhất.  

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho bạn thấy cách **convert image to text**, **recognize special characters**, và **extract text from image** bằng một thư viện Python đơn giản. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy, tải một hình ảnh để OCR, xử lý nội dung đa ngôn ngữ, và in kết quả.

## Những Điều Cần Chuẩn Bị

- Python 3.8+ được cài đặt trên máy của bạn.  
- Gói `ocr` (hoặc bất kỳ thư viện OCR tương thích nào) được cài đặt qua `pip install ocr`.  
- Tệp hình ảnh (`multilingual.png`) chứa cả glyph Latin và Cyrillic.  
- Một trình soạn thảo văn bản cơ bản hoặc IDE—VS Code, PyCharm, hoặc thậm chí Notepad đơn giản cũng được.  

Nếu bạn không có gói `ocr`, bạn có thể thay thế bằng `pytesseract` với một vài thay đổi nhỏ; các khái niệm cốt lõi vẫn giữ nguyên.

## Bước 1: Cài Đặt và Nhập Thư Viện OCR

Đầu tiên, chúng ta hãy chuẩn bị engine OCR. Chúng ta sẽ nhập thư viện, tạo một thể hiện engine, và cấu hình nó để hỗ trợ đa ngôn ngữ.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Tại sao điều này quan trọng:**  
Creating the engine is the foundation—without it you can’t **load image for OCR** later. Enabling language packs ensures the engine can correctly identify characters like “Ŀ”, “Ҕ”, and “Ǣ”. If you skip this step, you’ll end up with garbled output for non‑Latin scripts.

## Bước 2: Tải Hình Ảnh Chứa Văn Bản Đa Ngôn Ngữ

Bây giờ chúng ta chỉ định engine tới tệp mà chúng ta muốn xử lý. Đường dẫn có thể là tuyệt đối hoặc tương đối; chỉ cần chắc chắn rằng nó trỏ tới một hình ảnh có thể đọc được.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![ví dụ cách thực hiện OCR](/images/ocr-example.png "cách thực hiện OCR trên một hình ảnh đa ngôn ngữ")

**Tại sao điều này quan trọng:**  
Lệnh `load_image` đọc dữ liệu pixel vào bộ nhớ, chuẩn bị cho thuật toán OCR. Nếu hình ảnh lớn, engine có thể tự động giảm độ phân giải; bạn có thể tinh chỉnh sau bằng `engine.set_max_resolution(3000)` cho các quét độ phân giải cao.

## Bước 3: Chạy Quy Trình Nhận Dạng

Với engine đã sẵn sàng và hình ảnh đã được tải, cuối cùng chúng ta có thể trích xuất nội dung văn bản.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Tại sao điều này quan trọng:**  
`recognize()` runs the heavy‑lifting neural network behind the scenes. It returns an object that holds the raw text, confidence scores, and even bounding boxes if you need them for visual debugging.

## Bước 4: Xuất Văn Bản Được Nhận Dạng

Hãy xem engine đã tìm thấy gì. Chúng ta sẽ in văn bản ra console, nhưng bạn cũng có thể ghi nó vào tệp hoặc cơ sở dữ liệu.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Kết Quả Dự Kiến

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Nếu bạn thấy kết quả tương tự, chúc mừng—bạn đã thành công **convert image to text** và **recognize special characters**.

## Xử Lý Các Rủi Ro Thường Gặp

Ngay cả với một script đơn giản, bạn vẫn có thể gặp một vài trục trặc. Dưới đây là một số mẹo thực tế từ kinh nghiệm của tôi.

### 1. Thiếu Gói Ngôn Ngữ

Nếu bạn nhận được dấu hỏi (`?`) thay vì các chữ Cyrillic, hãy kiểm tra lại rằng các gói ngôn ngữ đã được cài đặt. Đối với nhiều engine OCR, bạn cần tải xuống các tệp `.traineddata` tương ứng và đặt chúng vào thư mục `tessdata` của engine.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Chất Lượng Hình Ảnh Thấp

Hình ảnh mờ hoặc độ tương phản thấp tạo ra điểm tin cậy thấp. Tiền xử lý hình ảnh bằng OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Tập Tin Lớn và Sử Dụng Bộ Nhớ

Xử lý một bức ảnh 10 MB có thể làm tăng đột biến bộ nhớ. Sử dụng `engine.set_max_image_size(2000)` để giới hạn độ phân giải, hoặc chia hình ảnh thành các ô và OCR từng ô riêng biệt.

### 4. Ghi Nhận Các Hộp Bao

Nếu bạn cần làm nổi bật vị trí của mỗi từ (hữu ích cho lớp phủ UI), truy cập `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Toàn Bộ Script – Thực Thi Một‑Nhấp

Kết hợp mọi thứ lại, đây là một tệp duy nhất bạn có thể chạy bằng `python ocr_demo.py`. Nó bao gồm xử lý lỗi, tiền xử lý tùy chọn, và các chú thích để rõ ràng.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Chạy nó bằng:

```bash
python ocr_demo.py path/to/multilingual.png
```

Bạn sẽ thấy cùng một kết quả như trên, xác nhận rằng bạn đã **extract text from image** thành công.

## Kết Luận

Chúng tôi đã bao phủ **how to perform OCR** trong Python từ đầu đến cuối: cài đặt thư viện, tải hình ảnh, nhận dạng nội dung đa ngôn ngữ, và xử lý các trường hợp biên phổ biến nhất. Bằng cách làm theo hướng dẫn này, bạn giờ có thể **convert image to text**, **recognize special characters**, và **extract text from image** trong các dự án của mình—không còn cần sao chép thủ công.

Tiếp theo? Hãy thử nghiệm với:

- Thêm nhiều gói ngôn ngữ hơn (ví dụ, `spa` cho tiếng Tây Ban Nha).  
- Xuất kết quả ra JSON để xử lý tiếp theo.  
- Tích hợp bước OCR vào một Flask API để các dịch vụ khác có thể gọi nó.  

Nếu bạn gặp bất kỳ vấn đề nào, cộng đồng xung quanh hầu hết các thư viện OCR rất năng động—tìm kiếm “ocr library language pack installation” hoặc để lại bình luận bên dưới. Chúc lập trình vui vẻ, và tận hưởng việc biến hình ảnh thành văn bản có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
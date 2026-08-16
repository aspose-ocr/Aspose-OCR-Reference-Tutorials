---
category: general
date: 2026-03-18
description: Tìm hiểu cách trích xuất văn bản từ hình ảnh và chuyển đổi văn bản của
  ảnh quét thành chuỗi có thể chỉnh sửa bằng Aspose OCR trong Python. Bao gồm mã từng
  bước.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR trong Python. Hướng
  dẫn này cho thấy cách chuyển đổi văn bản từ hình ảnh đã quét chỉ trong vài dòng
  mã.
og_title: Trích xuất văn bản từ hình ảnh bằng Aspose OCR – Hướng dẫn Python
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Trích xuất văn bản từ hình ảnh bằng Aspose OCR – Hướng dẫn Python
url: /vi/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ hình ảnh bằng Aspose OCR – Hướng dẫn Python

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng không biết bắt đầu từ đâu chưa? Bạn không phải là người duy nhất—các nhà phát triển luôn phải đối mặt với việc chuyển đổi các tệp PDF đã quét, ảnh chụp màn hình nhiễu, hoặc biên lai chụp ảnh thành các chuỗi có thể tìm kiếm và chỉnh sửa.  

Tin tốt là gì? Với Aspose OCR cho Python, bạn có thể **chuyển đổi văn bản trong ảnh đã quét** hàng loạt, mà không cần rời khỏi IDE. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho bạn thấy cách thực hiện, lý do mỗi bước quan trọng, và những lưu ý cần chú ý.

## Những gì bạn sẽ học

- Cài đặt thư viện Aspose OCR trong môi trường Python.  
- Chuẩn bị danh sách các tệp hình ảnh (PNG, JPG, TIFF, v.v.).  
- Thực hiện OCR hàng loạt chỉ với một lời gọi phương thức.  
- Truy cập và hiển thị văn bản đã trích xuất cho mỗi tệp.  
- Xử lý các vấn đề phổ biến như định dạng không được hỗ trợ và việc sử dụng bộ nhớ cho tệp lớn.  

Khi hoàn thành, bạn sẽ có một script có thể **trích xuất văn bản từ hình ảnh** theo yêu cầu—hoàn hảo để tự động hoá nhập liệu, lập chỉ mục tài liệu, hoặc cung cấp dữ liệu cho các pipeline NLP downstream.

---

![Extract text from images example](/images/ocr-extract-text.png "extract text from images")

*Image alt text: “extract text from images using Aspose OCR in Python”*

## Yêu cầu trước

- Python 3.8 hoặc mới hơn (code sử dụng f‑strings).  
- Giấy phép Aspose OCR cho Python hợp lệ hoặc khóa dùng thử miễn phí.  
- Các hình ảnh bạn muốn xử lý đã được lưu cục bộ (bất kỳ sự kết hợp nào của PNG, JPG, hoặc TIFF).  

Nếu bạn đã có môi trường ảo, tuyệt vời—nếu chưa, hãy tạo một môi trường mới với:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

Bây giờ bạn đã sẵn sàng cài đặt SDK.

## Bước 1: Cài đặt Aspose OCR SDK

Aspose phân phối engine OCR qua PyPI, vì vậy một lệnh `pip` duy nhất là đủ:

```bash
pip install aspose-ocr
```

> **Mẹo chuyên nghiệp:** Ghim phiên bản (ví dụ, `aspose-ocr==22.12`) để tránh các thay đổi gây lỗi không mong muốn sau này.

## Bước 2: Nhập lớp Engine OCR

Lớp cốt lõi bạn sẽ làm việc là `OcrEngine`. Nhập nó ở đầu script của bạn:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *Tại sao lại quan trọng:* Chỉ nhập những gì cần thiết giúp thời gian khởi động thấp, đặc biệt khi bạn nhúng script này vào một ứng dụng lớn hơn.

## Bước 3: Định nghĩa các tệp hình ảnh cần xử lý

Tạo một danh sách Python chứa đường dẫn đầy đủ tới mỗi hình ảnh bạn muốn quét. Thay `YOUR_DIRECTORY` bằng đường dẫn thư mục thực tế.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Trường hợp đặc biệt:** Nếu bạn có hàng trăm tệp, hãy cân nhắc tạo danh sách này một cách tự động bằng `glob.glob('*.png')` để tránh việc chỉnh sửa thủ công.

## Bước 4: Chạy OCR trên tất cả hình ảnh cùng lúc

Aspose OCR cung cấp phương thức tiện lợi `processMultiple` trả về một danh sách các đối tượng `OcrResult`—một đối tượng cho mỗi tệp đầu vào.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *Tại sao lại dùng xử lý batch?* Gửi từng hình ảnh riêng lẻ sẽ gây thêm overhead (khởi tạo engine, tải thư viện gốc). Lời gọi batch giảm tải CPU và tăng tốc độ công việc tổng thể.

### Xử lý lỗi một cách nhẹ nhàng

Nếu một hình ảnh không thể đọc được (tệp hỏng, định dạng không hỗ trợ), `processMultiple` sẽ ném ra ngoại lệ. Bao bọc lời gọi trong khối `try/except` để script vẫn chạy:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## Bước 5: Xuất văn bản đã trích xuất cho mỗi tệp

Duyệt qua các kết quả, ghép mỗi `OcrResult` với tên tệp gốc của nó. Phương thức `getText()` trả về chuỗi đã nhận dạng.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### Kết quả mong đợi

Chạy toàn bộ script trên ba ảnh chụp màn hình đơn giản có thể cho ra kết quả như sau:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

Nếu một hình ảnh không chứa ký tự nào có thể nhận dạng, bạn sẽ thấy một chuỗi rỗng—không có lỗi, và bạn có thể quyết định có đánh dấu tệp đó để kiểm tra thủ công hay không.

## Bonus: Tinh chỉnh độ chính xác OCR

Aspose OCR cung cấp một số cài đặt tùy chọn mà bạn có thể thử:

| Cài đặt | Chức năng | Khi nào nên dùng |
|---------|-----------|-------------------|
| `ocr_engine.setLanguage('eng')` | Buộc sử dụng mô hình ngôn ngữ tiếng Anh (giảm false positives). | Chủ yếu là tài liệu tiếng Anh. |
| `ocr_engine.setResolution(300)` | Cải thiện độ chính xác trên các bản quét DPI thấp. | Các bản quét dưới 200 dpi. |
| `ocr_engine.setPageSegMode('single_block')` | Xem toàn bộ ảnh như một khối văn bản duy nhất. | Biên lai đơn giản hoặc thẻ ID. |

Bạn có thể thêm các dòng này ngay sau khi tạo `ocr_engine`:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## Những cạm bẫy thường gặp & Cách tránh

1. **Stack TIFF lớn** – Một tệp TIFF đa trang có thể tiêu tốn gigabyte RAM khi tải toàn bộ cùng lúc. Hãy chia tệp thành các ảnh một trang trước khi đưa vào `processMultiple`.  
2. **Kịch bản không phải Latin** – Nếu bạn cần **trích xuất văn bản từ hình ảnh** chứa ký tự Cyrillic, Arabic, hoặc Chinese, hãy thay đổi mã ngôn ngữ tương ứng (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **Đường dẫn tệp có khoảng trắng** – Đường dẫn Windows có khoảng trắng có thể gây `FileNotFoundError`. Bao bọc mỗi đường dẫn trong raw string (`r"C:\My Folder\image.png"`) hoặc dùng `os.path.abspath`.  

Giải quyết những vấn đề này từ đầu sẽ giúp bạn tránh các lỗi runtime khó hiểu sau này.

---

## Ví dụ hoàn chỉnh

Dưới đây là script đầy đủ mà bạn có thể sao chép‑dán vào một tệp có tên `batch_ocr.py`. Nó bao gồm tất cả các tinh chỉnh thực tiễn đã được thảo luận ở trên.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

Lưu lại, kích hoạt môi trường ảo của bạn, và chạy:

```bash
python batch_ocr.py
```

Bạn sẽ thấy các chuỗi đã trích xuất được in ra console, sẵn sàng cho các bước xử lý tiếp theo (ví dụ: lưu vào cơ sở dữ liệu hoặc đưa vào mô hình ngôn ngữ tự nhiên).

---

## Kết luận

Trong hướng dẫn này, chúng tôi đã chỉ cho bạn cách **trích xuất văn bản từ hình ảnh** bằng Aspose OCR cho Python, bao gồm mọi thứ từ cài đặt đến xử lý batch và quản lý lỗi. Script ngắn gọn, đầy đủ chức năng, và dễ mở rộng—dù bạn muốn **chuyển đổi văn bản trong ảnh đã quét** thành file CSV, đưa vào chỉ mục tìm kiếm, hay tự động hoá nhập liệu.

Sẵn sàng cho bước tiếp theo? Hãy cân nhắc kết hợp pipeline OCR này với một công cụ gộp PDF để tạo PDF có thể tìm kiếm, hoặc kết nối nó với trigger lưu trữ đám mây để mỗi bản quét được tải lên đều được xử lý ngay lập tức. Bầu trời là giới hạn, và bạn đã có nền tảng vững chắc để xây dựng.

Có câu hỏi hoặc ý tưởng cải tiến? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-01-02
description: Học cách chỉnh nghiêng ảnh và tăng độ tương phản ảnh để nhanh chóng lấy
  văn bản thuần. Bao gồm mã Python từng bước và các mẹo để trích xuất văn bản.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: vi
og_description: Cách chỉnh nghiêng ảnh và tăng độ tương phản để lấy văn bản thuần.
  Ví dụ Python đầy đủ với trích xuất bảng và tăng tốc GPU.
og_title: Cách chỉnh nghiêng ảnh – Hướng dẫn OCR GPU toàn diện
tags:
- OCR
- Python
- Image Processing
title: Cách chỉnh nghiêng ảnh – Hướng dẫn OCR tăng tốc bằng GPU
url: /vi/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Khôi Hình Ảnh – Hướng Dẫn OCR Tăng Tốc GPU

Bạn đã bao giờ tự hỏi **how to deskew image** khi các biên lai của bạn xuất hiện ở góc kỳ lạ chưa? Bạn không phải là người duy nhất; một bức ảnh nghiêng có thể biến một biên lai dễ đọc thành một mớ hỗn độn. Tin tốt là với vài dòng Python, bạn có thể tự động định khôi, tăng độ tương phản và trích xuất văn bản thuần – không cần Photoshop thủ công.  

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy ngay, không chỉ **how to deskew image** mà còn cho thấy **how to boost contrast**, **how to get plain text**, và thậm chí **how to extract text** từ các bảng mà engine OCR phát hiện. Khi kết thúc, bạn sẽ có một script tự chứa mà bạn có thể đưa vào bất kỳ dự án nào.

## Những Gì Bạn Cần Chuẩn Bị

- Python 3.9+ đã được cài đặt (code sử dụng type hints, vì vậy một trình thông dịch mới sẽ hữu ích)
- Thư viện `ocr` cung cấp `OcrEngine`, `EngineMode`, `ImageProcessingOptions`, và `OcrResult` (cài đặt qua `pip install ocr‑sdk` – thay thế bằng tên gói thực tế bạn dùng)
- Một GPU có driver tương thích nếu bạn muốn tăng tốc (không bắt buộc nhưng được khuyến nghị)
- Một file ảnh hơi xoay hoặc độ tương phản thấp, ví dụ `receipt_skewed.jpg`

> **Mẹo chuyên nghiệp:** Nếu bạn không có GPU, chỉ cần đổi `EngineMode.GPU` thành `EngineMode.CPU` và script vẫn chạy — chỉ chậm hơn một chút.

## Triển Khai Từng Bước

Dưới đây chúng ta chia giải pháp thành các khối logic. Mỗi khối có một tiêu đề **H2** mô tả từ khóa chính *how to deskew image* hoặc một trong các từ khóa phụ. Code đầy đủ, có chú thích và sẵn sàng chạy.

### How to Deskew Image with GPU‑Accelerated OCR

Điều đầu tiên chúng ta làm là chỉ định engine OCR chạy trên GPU và bật tính năng auto‑deskew. Auto‑deskew phân tích hình học của ảnh và xoay lại cho thẳng đứng.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Tại sao lại quan trọng:** Tăng tốc GPU có thể rút thời gian xử lý từ vài giây xuống mili giây, điều này rất quan trọng khi bạn xử lý hàng chục biên lai mỗi phút.

### Boost Image Contrast for Better Recognition

Một biên lai có độ tương phản thấp là cơn ác mộng đối với bất kỳ hệ thống OCR nào. Bằng cách tăng độ tương phản, chúng ta cung cấp cho engine các cạnh rõ ràng hơn để làm việc.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Cách tăng độ tương phản:** Phương thức `set_contrast_boost` nhận phần trăm; 30 % là giá trị mặc định an toàn cho hầu hết các biên lai đã quét. Nếu ảnh của bạn quá tối, hãy tăng lên 50 % hoặc thử nghiệm.

### Get Plain Text from the Processed Image

Bây giờ ảnh đã thẳng và sáng, chúng ta đưa nó vào engine và yêu cầu kết quả dạng văn bản thuần.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Kết quả mong đợi** (rút gọn để tiện):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Cách lấy plain text:** Phương thức `get_text()` loại bỏ mọi thông tin bố cục và trả về một chuỗi sạch, bạn có thể lưu vào cơ sở dữ liệu, gửi tới API, hoặc đưa vào các phân tích tiếp theo.

### How to Extract Text from Detected Tables

Thường thì biên lai chứa dữ liệu dạng bảng (mặt hàng, số lượng, giá). SDK OCR có thể phát hiện bảng và cho phép bạn lặp qua các hàng và ô.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Ví dụ đầu ra bảng**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Tại sao cần trích xuất bảng:** Dữ liệu có cấu trúc giúp tính tổng nhanh chóng, tạo báo cáo, hoặc đưa vào phần mềm kế toán.

### Full Working Script

Kết hợp mọi thứ lại, đây là script bạn có thể sao chép‑dán vào `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Chạy nó bằng:

```bash
python deskew_and_ocr.py
```

Bạn sẽ thấy văn bản đã được làm sạch và bất kỳ bảng nào được phát hiện được in ra console.

## Các Trường Hợp Cạnh Thường Gặp & Cách Xử Lý

| Tình Huống | Cách Giải Quyết |
|-----------|-----------------|
| **Ảnh bị lộn ngược** | Tăng độ tin cậy của `set_auto_deskew(True)` bằng cách cũng gọi `set_rotation_correction(True)` nếu SDK hỗ trợ. |
| **Tăng độ tương phản làm ảnh quá sáng** | Giảm phần trăm truyền vào `set_contrast_boost` (ví dụ, 15 %). |
| **GPU không khả dụng** | Đổi `EngineMode.GPU` thành `EngineMode.CPU`; phần còn lại của pipeline không thay đổi. |
| **Bảng bị bỏ lỡ** | Thử quét với độ phân giải cao hơn hoặc bật `set_table_detection(True)` nếu thư viện cung cấp. |

## Bước Tiếp Theo: Từ Plain Text Đến Dữ Liệu Có Cấu Trúc

Bây giờ bạn đã biết **how to deskew image**, **how to boost contrast**, và **how to get plain text**, bạn có thể muốn:

- Phân tích plain text bằng biểu thức chính quy để trích xuất các cặp key‑value (ví dụ, `total`, `date`).
- Lưu kết quả vào cơ sở dữ liệu SQLite hoặc PostgreSQL để báo cáo sau này.
- Kết nối script với một hàm serverless (AWS Lambda, Azure Functions) để tự động xử lý các tệp tải lên.

Tất cả các mở rộng này dựa trên nền tảng chúng ta đã đề cập ở trên.

## Kết Luận

Chúng ta đã đi qua **how to deskew image** bằng một engine OCR tăng tốc GPU, trình bày **how to boost contrast** để nhận dạng sắc nét hơn, chỉ ra **how to get plain text**, và thậm chí **how to extract text** từ các bảng. Script hoàn chỉnh, có thể chạy ngay, gộp mọi thứ lại, cho phép bạn đưa nó vào bất kỳ dự án Python nào và bắt đầu trích xuất dữ liệu sạch từ các ảnh nghiêng, độ tương phản thấp ngay lập tức.

Hãy thử với một vài biên lai của bạn, điều chỉnh mức độ tương phản, và để OCR làm phần việc nặng. Nếu gặp khó khăn, hãy xem lại bảng các trường hợp cạnh trên — hầu hết vấn đề chỉ cần một chút tinh chỉnh.

Chúc lập trình vui vẻ, và mong rằng ảnh của bạn luôn thẳng và sáng!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
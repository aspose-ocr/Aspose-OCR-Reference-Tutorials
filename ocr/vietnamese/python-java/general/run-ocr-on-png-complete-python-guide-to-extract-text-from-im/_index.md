---
category: general
date: 2026-01-12
description: Chạy OCR trên các tệp PNG nhanh chóng với Python. Tìm hiểu cách trích
  xuất văn bản từ hình ảnh và hoá đơn, và tải hình ảnh để OCR bằng Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: vi
og_description: Chạy OCR trên PNG ngay lập tức. Hướng dẫn này chỉ cách trích xuất
  văn bản từ hình ảnh và hoá đơn, tải hình ảnh để OCR, và lưu kết quả dưới dạng JSON
  và CSV.
og_title: Chạy OCR trên PNG – Hướng dẫn Python đầy đủ
tags:
- OCR
- Python
- Image Processing
title: Chạy OCR trên PNG – Hướng dẫn Python toàn diện để trích xuất văn bản từ hình
  ảnh
url: /vi/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy OCR trên PNG – Hướng Dẫn Python Đầy Đủ Để Trích Xuất Văn Bản Từ Hình Ảnh

Bạn đã bao giờ cần **run OCR on PNG** nhưng không chắc thư viện nào sẽ cho kết quả sạch sẽ, có cấu trúc? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế—như tự động hoá hoá đơn hoặc quét biên lai—bước đầu tiên là **extract text from image** và PNG là định dạng phổ biến vì nó giữ chất lượng không mất dữ liệu.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ thực hành sử dụng gói Aspose.OCR cho Python. Khi kết thúc, bạn sẽ biết cách **load image for OCR**, lấy ra từng dòng văn bản, chuyển dữ liệu thành một đối tượng JSON gọn gàng, và thậm chí xuất ra CSV để xử lý tiếp theo. Không có phần thừa, chỉ có giải pháp thực tế, sẵn sàng chạy.

## Những Điều Bạn Sẽ Học

- Cách cài đặt và import thư viện Aspose.OCR.  
- Các bước chính xác để **run OCR on PNG** và xử lý đối tượng kết quả.  
- Cách **extract text from invoice** và định dạng đầu ra dưới dạng JSON hoặc CSV.  
- Mẹo xử lý ảnh độ tương phản thấp, tài liệu đa ngôn ngữ và điểm tin cậy.  
- Một mẫu mã hoàn chỉnh, sao chép‑dán mà bạn có thể chạy ngay hôm nay.

> **Prerequisite:** Python 3.8+ và kiến thức cơ bản về pip. Nếu bạn chưa từng dùng Aspose, đừng lo—hướng dẫn này bao gồm mọi thứ bạn cần để bắt đầu.

---

## Bước 1 – Cài Đặt Aspose.OCR và Chuẩn Bị Môi Trường

Trước khi chúng ta có thể **run OCR on PNG**, thư viện cần phải được cài đặt trên hệ thống của bạn.

```bash
pip install aspose-ocr
```

> **Pro tip:** Sử dụng môi trường ảo (`python -m venv venv`) để cô lập các phụ thuộc. Điều này ngăn xung đột phiên bản khi bạn làm việc với nhiều dự án.

Sau khi cài đặt, import các module chúng ta sẽ cần:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

## Bước 2 – Tạo Engine OCR và Đặt Ngôn Ngữ

The OCR engine is the core component that actually reads the pixels. For most English invoices, you’ll want the English language pack:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Why this matters:** Việc chỉ định ngôn ngữ sẽ thu hẹp bộ ký tự, tăng độ chính xác và tốc độ xử lý. Nếu bạn cần xử lý hoá đơn đa ngôn ngữ, chỉ cần thay `ocr.Language.ENGLISH` bằng enum phù hợp.

## Bước 3 – Tải Ảnh Để OCR

Now we’ll **load image for OCR**. The `Image.load` method accepts a file path, and it works with PNG, JPEG, BMP, and more.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** Nếu PNG quá lớn (hơn 5 MB), hãy cân nhắc giảm kích thước trước để giữ mức sử dụng bộ nhớ hợp lý. Pillow có thể thực hiện việc này trong một dòng:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

## Bước 4 – Thực Hiện OCR trên PNG và Lấy Kết Quả

With the engine ready and the image loaded, it’s time to **run OCR on PNG** and retrieve the structured result.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

`ocr_result` chứa một tập hợp các mục `OcrRegion`, mỗi mục có văn bản đã nhận dạng và điểm tin cậy (0‑100). Đây là nơi bạn có được dữ liệu chi tiết cần để **extract text from invoice**.

## Bước 5 – Chuyển Kết Quả Sang JSON và In Đẹp

Most downstream systems love JSON, so we’ll turn the OCR output into a nicely formatted string.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Kết Quả Mẫu

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Chú ý mỗi dòng đều có chỉ số tin cậy—rất phù hợp để lọc các mục có tin cậy thấp nếu bạn muốn **extract text from invoice** tự động.

## Bước 6 – Lưu Dữ Liệu OCR Dưới Dạng CSV (Mỗi Dòng Một Văn Bản + Tin Cậy)

CSV is ideal for spreadsheets or quick data imports. Aspose offers a one‑liner to dump everything into a CSV file.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

The generated CSV will look like this:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Bây giờ bạn có thể mở nó trong Excel, Google Sheets, hoặc nhập vào cơ sở dữ liệu.

## Bonus – Xử Lý Văn Bản Tin Cậy Thấp và PDF Đa Trang

### Lọc Theo Tin Cậy

If you only want high‑certainty lines, filter the JSON before you write it out:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Tài Liệu Đa Trang

Aspose.OCR tự động tạo một mục `page` mới cho mỗi trang trong PNG hoặc PDF đa trang. Lặp qua `ocr_data["pages"]` để xử lý tất cả—không cần mã bổ sung.

## Ví Dụ Hoàn Chỉnh Hoạt Động

Below is the **complete script** you can copy, paste, and run immediately. Replace `YOUR_DIRECTORY` with the folder that holds your PNG file.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Chạy script bằng `python run_ocr.py` và bạn sẽ thấy JSON được in ra console, một file CSV trên đĩa, và danh sách đã lọc các mục tin cậy cao.

## Câu Hỏi Thường Gặp

**Q: Tôi có thể dùng cách này để trích xuất văn bản từ biên lai quét thay vì hoá đơn không?**  
A: Chắc chắn. Quy trình giống nhau—chỉ cần trỏ `image_path` tới file PNG biên lai của bạn. Nếu biên lai dùng ngôn ngữ khác, hãy đổi `engine.language` cho phù hợp.

**Q: Nếu PNG của tôi chứa văn bản bị xoay thì sao?**  
A: Aspose.OCR tự động phát hiện hướng, nhưng trong những trường hợp khó, bạn có thể tự quay ảnh bằng Pillow trước khi đưa vào engine.

**Q: Tôi có cần giấy phép trả phí cho Aspose.OCR không?**  
A: Thư viện cung cấp chế độ đánh giá miễn phí với watermark trên kết quả. Đối với sử dụng sản xuất, bạn sẽ cần giấy phép, có thể lấy từ trang web Aspose.

## Kết Luận

Chúng tôi đã bao quát mọi thứ bạn cần để **run OCR on PNG** bằng Python: cài đặt SDK, tải ảnh, trích xuất văn bản có cấu trúc, và lưu kết quả dưới dạng JSON hoặc CSV. Dù bạn muốn **extract text from image** cho một script đơn giản hay **extract text from invoice** cho quy trình kế toán tự động, các bước trên cung cấp nền tảng vững chắc, sẵn sàng cho sản xuất.

Next, you might explore:

- Kết hợp đầu ra CSV với cơ sở dữ liệu để lưu trữ hoá đơn hàng loạt.  
- Thêm xử lý hậu kỳ bằng biểu thức chính quy để lấy ngày, số tiền, hoặc mã số thuế.  
- Sử dụng tính năng `ocr_engine.recognize_barcode` nếu hoá đơn của bạn có mã QR.

Hãy thử, điều chỉnh ngưỡng tin cậy, và xem quy trình xử lý tài liệu của bạn trở nên nhẹ nhàng. Có thêm câu hỏi hoặc trường hợp sử dụng thú vị? Để lại bình luận bên dưới—chúc OCR vui vẻ!  

![ví dụ chạy OCR trên PNG](run-ocr-on-png.png "run OCR on PNG – ví dụ hình ảnh kết quả OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
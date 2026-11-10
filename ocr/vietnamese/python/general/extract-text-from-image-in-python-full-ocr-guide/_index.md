---
category: general
date: 2026-06-25
description: Trích xuất văn bản từ hình ảnh bằng Python OCR. Tìm hiểu cách tải hình
  ảnh cho OCR, thực hiện OCR trong Python và chuyển đổi biên lai sang JSON trong vài
  bước đơn giản.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng OCR Python. Hướng dẫn này sẽ chỉ
  cho bạn cách tải hình ảnh để OCR, thực hiện OCR trong Python và chuyển đổi biên
  lai sang JSON.
og_title: Trích xuất văn bản từ hình ảnh trong Python – Hướng dẫn OCR đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Trích xuất văn bản từ hình ảnh bằng Python – Hướng dẫn OCR đầy đủ
url: /vi/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh trong Python – Hướng dẫn OCR toàn diện

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng không biết bắt đầu từ đâu? Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **tải hình ảnh để OCR**, **thực hiện OCR trong Python**, và **chuyển đổi biên lai sang JSON**—tất cả chỉ với một vài dòng mã.

Nếu bạn từng xây dựng một ứng dụng quét biên lai, một công cụ theo dõi chi phí, hoặc chỉ muốn tự động hoá việc nhập dữ liệu, bạn sẽ thấy việc nắm vững quy trình này thực sự thay đổi cuộc chơi. Khi kết thúc, bạn sẽ có một script hoạt động, đọc ảnh biên lai và xuất ra một payload JSON sạch sẽ, sẵn sàng cho các dịch vụ downstream.

## Những gì bạn sẽ học

Chúng ta sẽ đi qua mọi bước từ cài đặt thư viện `aocr` đến xử lý kết quả thô. Cụ thể, bạn sẽ học cách:

1. **Tạo một thể hiện OCR engine** – điểm vào cho mọi công việc nhận dạng.  
2. **Tải hình ảnh cho OCR** – chỉ định cho engine file nào cần đọc.  
3. **Chọn định dạng xuất** – JSON hoặc XML, chúng ta sẽ chọn JSON vì dễ tiêu thụ hơn.  
4. **Chạy nhận dạng** – thực hiện OCR trong Python.  
5. **In hoặc lưu kết quả** – chuyển đổi biên lai sang JSON và xem đầu ra.

Không cần kinh nghiệm trước về OCR; chỉ cần một môi trường Python cơ bản và một file hình ảnh (biên lai, tờ rơi, bất kỳ gì bạn muốn).  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="lưu đồ trích xuất văn bản từ hình ảnh bằng OCR Python"}

## Trích xuất Văn bản từ Hình ảnh – Hướng dẫn OCR Python Từng Bước

Dưới đây là script hoàn chỉnh, sẵn sàng chạy. Bạn có thể sao chép‑dán nó vào một file tên `receipt_ocr.py` và chạy `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Tại sao cách này hoạt động

- **Thể hiện engine** – `aocr.OcrEngine()` bao gói mọi công việc nặng (tải mô hình, tiền xử lý, v.v.).  
- **Tải hình ảnh** – `engine.load_image()` cho thư viện biết chính xác bitmap nào cần phân tích; bạn có thể đưa JPEG, PNG, hoặc thậm chí PDF đa trang.  
- **Định dạng xuất** – Đặt `engine.export_format` thành `aocr.ExportFormat.JSON` sẽ cho kết quả dưới dạng chuỗi có cấu trúc, hoàn hảo cho các API mong đợi JSON.  
- **Gọi nhận dạng** – `engine.recognize()` thực hiện suy luận mạng nơ‑ron phía sau; nó trả về một chuỗi JSON chứa các khối văn bản được phát hiện, điểm tin cậy và thông tin bố cục.  

---

## Tải Hình ảnh cho OCR với aocr

Nếu bạn thắc mắc liệu hình ảnh có cần tiền xử lý đặc biệt không, câu trả lời ngắn gọn là **không**—`aocr` tự động xử lý hầu hết các trường hợp phổ biến (điều chỉnh độ tương phản, cân chỉnh). Tuy nhiên, bạn có thể cải thiện độ chính xác bằng cách:

- Đảm bảo hình ảnh có độ phân giải ít nhất 300 dpi.  
- Cắt bỏ các viền không liên quan.  
- Chuyển sang ảnh xám trước khi đưa vào (tùy chọn, `engine.load_image()` sẽ tự làm cho bạn).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro tip:* Nếu biên lai có nhiều nhiễu, bước bổ sung trên có thể tăng **perform OCR in Python** đáng kể.

---

## Chọn Định dạng Xuất và Chuyển đổi Biên lai sang JSON

Bạn có thể tự hỏi, “Tại sao không chỉ lấy văn bản thuần?” Bởi vì JSON giữ lại cấu trúc phân cấp (dòng, từ, hộp bao). Điều này giúp việc ánh xạ các trường như *tổng tiền* hoặc *ngày* trở nên dễ dàng hơn rất nhiều.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Khi chạy script, `json_result` sẽ trông giống như sau (được rút gọn để ngắn gọn):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Bây giờ bạn đã có một payload **convert receipt to JSON** có thể đưa thẳng vào cơ sở dữ liệu, endpoint REST, hoặc mô hình machine‑learning.

---

## Chạy Nhận dạng và Lấy Kết quả

Bước cuối cùng—thực sự thực hiện OCR—chỉ cần gọi `recognize()`. Ở phía sau, thư viện:

1. Gửi hình ảnh qua một mạng nơ‑ron tích chập đã được huấn luyện trước.  
2. Giải mã đầu ra của mạng thành các ký tự có thể đọc được.  
3. Đóng gói mọi thứ vào định dạng đã chọn (JSON trong trường hợp này).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Nếu bạn muốn lưu kết quả thay vì in ra, chỉ cần ghi nó vào một file:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Trường hợp đặc biệt:* Một số biên lai chứa ký tự không phải ASCII (ví dụ, “€”). Hãy chắc chắn mở file với mã hoá UTF‑8 như trong ví dụ trên, để tránh văn bản bị lỗi.

---

## Ví dụ Hoàn chỉnh (Tất cả các Bước trong Một Script)

Kết hợp mọi thứ lại, đây là script cuối cùng bạn có thể chạy từ đầu tới cuối:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Chạy nó bằng:

```bash
python receipt_ocr.py
```

Bạn sẽ thấy một dòng xác nhận và, trong cùng thư mục, một file `receipt_output.json` chứa dữ liệu có cấu trúc.

---

## Kết luận

Bây giờ bạn đã biết **cách trích xuất văn bản từ hình ảnh** bằng Python, **cách tải hình ảnh cho OCR**, **cách thực hiện OCR trong Python**, và **cách chuyển đổi biên lai sang JSON** cho các hệ thống downstream. Quy trình end‑to‑end này nhẹ, chỉ yêu cầu gói `aocr`, và có thể tích hợp vào bất kỳ pipeline tự động nào.

Tiếp theo bạn sẽ làm gì? Thử đổi định dạng xuất sang XML, thử nghiệm các kỹ thuật tiền xử lý hình ảnh khác nhau, hoặc xây dựng một API Flask nhỏ nhận biên lai tải lên và trả về payload JSON ngay lập tức. Khi đã nắm vững nền tảng, bạn có thể bay cao hơn nữa.

Có câu hỏi hoặc gặp khó khăn? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ cùng các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
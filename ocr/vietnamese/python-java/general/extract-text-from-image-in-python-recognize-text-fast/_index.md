---
category: general
date: 2026-07-05
description: Trích xuất văn bản từ hình ảnh bằng Python OCR. Tìm hiểu cách nhận dạng
  văn bản từ hình ảnh, tải hình ảnh cho OCR và thiết lập ngôn ngữ OCR chỉ trong vài
  dòng.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Python OCR. Hướng dẫn này chỉ
  cách nhận dạng văn bản từ hình ảnh, tải hình ảnh cho OCR, tạo công cụ OCR theo phong
  cách Python và thiết lập ngôn ngữ OCR.
og_title: Trích xuất văn bản từ hình ảnh trong Python – Nhận dạng văn bản nhanh
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Trích xuất văn bản từ hình ảnh trong Python – Nhận dạng văn bản nhanh
url: /vi/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ hình ảnh trong Python – Nhận dạng văn bản nhanh

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng không biết nên chọn thư viện nào? Nếu bạn từng tự hỏi *cách nhận dạng văn bản từ hình ảnh* mà không phải dùng các công cụ bên ngoài, bạn đang ở đúng nơi. Trong hướng dẫn này, chúng ta sẽ khởi động một công cụ OCR nhỏ, chỉ vào một bức ảnh và lấy văn bản ra—không hơn, không kém.

Chúng ta sẽ đi qua từng bước: **create OCR engine python**, **set OCR language**, **load image for OCR**, kích hoạt nhận dạng một cách bất đồng bộ, và cuối cùng đọc kết quả. Khi kết thúc, bạn sẽ có một script tự chứa mà bạn có thể đưa vào bất kỳ dự án nào, dù là một công cụ số hoá tài liệu hay một chatbot đọc meme.

## Những gì bạn cần

- Python 3.8+ (mã chạy trên 3.10 và các phiên bản mới hơn)  
- Gói `ocr` (một lớp bao bọc nhẹ quanh Tesseract – cài đặt bằng `pip install ocr` hoặc fork mà bạn thích)  
- Tệp hình ảnh (`.jpg`, `.png`, v.v.) chứa văn bản có thể đọc được  
- Một chút kiên nhẫn cho phần async (nó nhanh, hứa)

Chỉ vậy—không có phụ thuộc nặng, không cần biên dịch gốc. Nếu bạn đã có Tesseract trên hệ thống, lớp bao bọc `ocr` sẽ tự động tìm thấy nó.

## Bước 1: Tạo OCR Engine – trái tim của việc trích xuất

Điều đầu tiên cần làm: bạn cần một đối tượng engine biết cách giao tiếp với engine OCR bên dưới. Hãy nghĩ nó như “bộ não” sẽ xử lý hình ảnh sau này.

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*Tại sao điều này quan trọng*: nếu không có engine, bạn sẽ không có ngữ cảnh cho cài đặt ngôn ngữ hay khả năng async. Lớp `OcrEngine` trừu tượng hoá các lệnh dòng lệnh cấp thấp tới Tesseract, cung cấp cho bạn một API Python sạch sẽ.

## Bước 2: Đặt ngôn ngữ OCR – cho engine biết gì sẽ nhận dạng

Nếu tài liệu của bạn là tiếng Anh, bạn có thể để mặc định, nhưng tốt hơn là đặt rõ ràng. Điều này cũng cho thấy cách **set OCR language** cho các ngôn ngữ khác.

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **Mẹo chuyên nghiệp**: Đối với PDF đa ngôn ngữ, bạn có thể truyền một danh sách như `[ocr.Language.ENGLISH, ocr.Language.FRENCH]`. Engine sẽ tự động thử cả hai ngôn ngữ.

## Bước 3: Tải hình ảnh cho OCR – đưa ảnh vào bộ nhớ

Bây giờ chúng ta thực sự **load image for OCR**. Lớp bao bọc hỗ trợ tải lười, vì vậy tệp không được đọc cho đến khi engine cần.

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*Trường hợp đặc biệt*: Nếu hình ảnh quá lớn (hơn 5 MB), hãy cân nhắc thay đổi kích thước trước để tăng tốc nhận dạng. Bạn có thể làm điều này bằng Pillow:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## Bước 4: Khởi động nhận dạng bất đồng bộ – không chặn ứng dụng của bạn

Chạy OCR có thể mất một hoặc hai giây, đặc biệt với các bản quét lớn. Phương thức `recognize_async` trả về một future mà bạn có thể kiểm tra sau, cho phép bạn **thực hiện công việc khác trong khi OCR chạy ở nền**.

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

Tại sao lại async? Trong một máy chủ web, bạn không muốn một yêu cầu duy nhất làm chậm toàn bộ pool worker. Đối tượng future cho bạn quyền kiểm soát: bạn có thể `await` nó trong mã async hoặc chỉ chặn khi thực sự cần kết quả.

## Bước 5: Lấy kết quả – chỉ chặn khi cần thiết

Khi cuối cùng bạn cần văn bản, gọi `future.get()`. Lệnh này **chỉ chặn tại đây**, nghĩa là phần còn lại của chương trình vẫn phản hồi cho tới khi OCR hoàn thành.

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

Nếu bạn đang trong vòng lặp `asyncio`, bạn có thể thay thế bằng `await future` – lớp bao bọc hỗ trợ cả hai kiểu.

## Bước 6: Sử dụng văn bản đã nhận dạng – dữ liệu của bạn đã sẵn sàng

Bây giờ bạn đã có một đối tượng `result`, việc lấy chuỗi thuần là đơn giản. Hãy in nó ra và cũng cho thấy cách bạn có thể ghi vào tệp.

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Kết quả mong đợi** (rút gọn để ngắn gọn):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Nếu hình ảnh không chứa văn bản, `result.text` sẽ là một chuỗi rỗng—hãy xử lý trường hợp này một cách nhẹ nhàng.

## Ví dụ hoàn chỉnh – Tất cả các bước trong một script

Dưới đây là chương trình đầy đủ, sẵn sàng chạy. Sao chép‑dán, điều chỉnh `image_path`, và bạn đã sẵn sàng.

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **Lưu ý**: Thay `"YOUR_DIRECTORY/large_document.jpg"` bằng đường dẫn thực tế tới hình ảnh của bạn. Script hoạt động trên Windows, macOS và Linux miễn là Tesseract đã được cài đặt và có thể truy cập trong `PATH` của bạn.

## Những lỗi thường gặp & Cách tránh

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Ký tự rác** | Ngôn ngữ sai hoặc thiếu các tệp dữ liệu ngôn ngữ. | Đảm bảo `engine.language` khớp với văn bản và tệp `.traineddata` tương ứng tồn tại trong thư mục `tessdata` của Tesseract. |
| **Hiệu suất chậm trên ảnh lớn** | OCR tăng thời gian xử lý tương ứng với số pixel. | Thay đổi kích thước hoặc giảm mẫu trước khi đưa vào engine (xem đoạn mã Pillow). |
| **Future không bao giờ hoàn thành** | Tệp ảnh bị hỏng hoặc không đọc được. | Bao bọc `future.get()` trong khối try/except và xác thực `image.is_valid()` trước khi nhận dạng. |
| **Mất Unicode** | | |

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất văn bản từ hình ảnh với Aspose OCR – Hướng dẫn từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Chuyển đổi hình ảnh thành văn bản – Thực hiện OCR trên hình ảnh từ URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Trích xuất văn bản từ hình ảnh – Tối ưu hóa OCR với Aspose OCR cho .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
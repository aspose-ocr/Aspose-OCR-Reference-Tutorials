---
category: general
date: 2026-06-28
description: Học cách nhận dạng hình ảnh văn bản bằng OCR Python, trích xuất các tệp
  PNG chứa văn bản và in ra văn bản đã nhận dạng với xử lý lỗi mạnh mẽ.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: vi
og_description: Hướng dẫn từng bước để nhận dạng ảnh văn bản trong Python, trích xuất
  văn bản PNG và in văn bản đã nhận dạng một cách an toàn.
og_title: Nhận dạng hình ảnh văn bản bằng Python OCR – Hướng dẫn toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Nhận dạng hình ảnh văn bản bằng Python OCR – Hướng dẫn đầy đủ
url: /vi/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nhận dạng văn bản trong hình ảnh bằng Python OCR – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **recognize text image** trong một script Python mà không cần kéo vào một framework nặng? Bạn không phải là người duy nhất. Nhiều nhà phát triển cần một cách nhanh chóng để *load image OCR* một ảnh chụp màn hình, một biên lai đã quét, hoặc một file PNG đơn giản và lấy lại văn bản.

Trong hướng dẫn này, chúng ta sẽ kết nối một engine OCR tối thiểu, gắn một logger tùy chỉnh, **load image OCR**, chạy **process image OCR**, và cuối cùng **print recognized text**. Khi kết thúc, bạn sẽ có một script tự chứa có thể **extract text png** các file khi cần.

## Những gì bạn sẽ nhận được

- Một đoạn mã Python hoàn chỉnh tạo ra một OCR engine, ghi lại mọi bước, và xử lý lỗi một cách nhẹ nhàng.  
- Giải thích rõ ràng về *tại sao* mỗi dòng lại quan trọng—để bạn có thể điều chỉnh mã cho Tesseract, EasyOCR, hoặc bất kỳ backend nào khác.  
- Mẹo cho các vấn đề thường gặp (thiếu font, PNG hỏng) và cách debug chúng.  

### Yêu cầu trước

- Python 3.8+ đã được cài đặt  
- Thư viện OCR cung cấp một lớp `OcrEngine` (ví dụ sử dụng một API giả tưởng nhưng điển hình; thay thế bằng `pytesseract`, `easyocr`, v.v.).  
- Một ảnh PNG bạn muốn phân tích, lưu dưới tên `input.png` trong một thư mục bạn kiểm soát.  

> **Mẹo:** Nếu bạn đang sử dụng `pytesseract`, hãy cài đặt binary Tesseract của hệ thống trước (`sudo apt install tesseract-ocr` trên Linux) và sau đó `pip install pytesseract pillow`.

---

## ## Nhận dạng Văn bản trong Hình ảnh: Cài đặt Logger

Một logger tốt là người hùng thầm lặng của bất kỳ pipeline OCR nào. Nó cho bạn biết *khi nào* engine bắt đầu, *tệp nào* nó mở, và *tại sao* nó có thể thất bại.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*​Tại sao điều này quan trọng:*  
Logger tách riêng đầu ra chẩn đoán khỏi lõi OCR, giúp dễ dàng chuyển hướng log tới file, dịch vụ giám sát, hoặc thậm chí UI sau này.

---

## ## Load Image OCR: Cung cấp Engine một PNG

Trước khi engine có thể **process image OCR**, nó cần một đối tượng ảnh hợp lệ. Hầu hết các thư viện chấp nhận một instance `Image` của Pillow.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*​Các điểm chính:*  

- **load image ocr** – `Image.from_file` ẩn đi chi tiết giải mã PNG.  
- Giữ đường dẫn có thể cấu hình; hard‑coding làm script dễ gãy.  
- Lệnh logger xác nhận ảnh đã được đọc thành công, hữu ích khi tệp bị thiếu hoặc hỏng.

---

## ## Process Image OCR: Nhận dạng Văn bản

Bây giờ công việc nặng nhọc bắt đầu. Engine quét bitmap, áp dụng mạng nơ-ron hoặc heuristics, và trả về một chuỗi Unicode.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*​Tại sao chúng ta bọc nó trong `try/except`:*  
OCR có thể gặp lỗi với PNG độ phân giải thấp, không hỗ trợ không gian màu, hoặc thiếu dữ liệu ngôn ngữ. Bắt `OcrException` cho phép bạn **print recognized text** chỉ khi nó thực sự tồn tại, tránh các stack trace khó hiểu cho người dùng cuối.

---

## ## Print Recognized Text & Extract Text PNG

Nếu việc nhận dạng thành công, chúng ta hiển thị kết quả và tùy chọn ghi nó vào file `.txt` có tên trùng với PNG gốc.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*​Bạn nhận được:*  

- **print recognized text** – phản hồi trực quan ngay trong terminal.  
- Một file `.txt` song song giúp **extract text png** cho các quy trình tiếp theo (đánh chỉ mục tìm kiếm, nhập dữ liệu, v.v.).

---

## ## Các trường hợp góc cạnh phổ biến & Cách giải quyết

| Tình huống | Triệu chứng | Cách khắc phục |
|-----------|-------------|----------------|
| PNG chỉ có màu xám | OCR trả về chuỗi rỗng | Chuyển sang RGB (`Image.convert("RGB")`) trước khi cung cấp cho engine. |
| Ngôn ngữ không được hỗ trợ | `OcrException` với mã `LANG_NOT_FOUND` | Cài đặt gói ngôn ngữ (ví dụ, `tesseract‑lang‑fra` cho tiếng Pháp) và đặt `ocr_engine.language = "fra"`. |
| Ảnh rất lớn ( > 5 MB ) | Nhận dạng chậm hoặc lỗi bộ nhớ | Giảm kích thước bằng `image.thumbnail((2000, 2000))` trước `set_image`. |
| Ký tự không mong muốn | Kết quả rối | Đảm bảo ảnh thực sự là PNG; một số tệp giả dạng PNG nhưng thực chất là JPEG. Sử dụng `Image.verify()` để xác thực. |

---

## ## Ví dụ Hoạt động đầy đủ (Sẵn sàng Sao chép‑Dán)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Kết quả console mong đợi (đường thành công):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

Nếu có gì sai, bạn sẽ thấy dòng `[ERROR]` rõ ràng kèm lý do, nhờ logger tùy chỉnh.

---

## ## Các bước tiếp theo & Chủ đề liên quan

- **extract text png** từ các batch: bọc script trong một vòng `for` duyệt cây thư mục.  
- **process image ocr** với tiền xử lý (điều chỉnh góc, tăng độ tương phản) bằng OpenCV trước khi cung cấp cho engine.  
- Chuyển sang dịch vụ OCR đám mây (Google Vision, Azure Read) bằng cách thay đổi triển khai `OcrEngine`—code xung quanh vẫn giữ nguyên.  
- Tìm hiểu cách **print recognized text** vào PDF bằng `reportlab` để tự động tạo báo cáo.  

---

## Kết luận

Chúng ta vừa đi qua một cách gọn gàng, sẵn sàng cho sản xuất để **recognize text image** trong Python, từ việc tải PNG đến **print recognized text** và lưu kết quả. Bằng cách chèn một logger nhỏ, xử lý ngoại lệ, và tùy chọn lưu kết quả, script sẵn sàng cho cả các thí nghiệm nhanh và tích hợp vào pipeline lớn hơn.

Hãy thử với các screenshot của bạn, chơi với tiền xử lý ảnh, và bạn sẽ sớm trích xuất văn bản từ bất kỳ PNG nào. Có câu hỏi? Để lại bình luận—chúc bạn OCR vui vẻ!  

![ví dụ nhận dạng văn bản trong hình ảnh](placeholder.png)


## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cách thực hiện Trích xuất Văn bản từ Hình ảnh từ Stream bằng Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Chuyển Đổi Hình ảnh sang Văn bản – Thực hiện OCR trên Hình ảnh từ URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
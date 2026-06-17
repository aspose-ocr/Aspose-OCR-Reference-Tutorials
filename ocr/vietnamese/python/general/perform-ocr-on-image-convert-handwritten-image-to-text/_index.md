---
category: general
date: 2026-03-18
description: Thực hiện OCR trên hình ảnh và trích xuất văn bản viết tay từ một bức
  ảnh. Tìm hiểu cách chuyển đổi hình ảnh viết tay, trích xuất văn bản từ file jpg
  và nhận dạng văn bản từ ảnh.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: vi
og_description: Thực hiện OCR trên hình ảnh để trích xuất văn bản viết tay từ một
  bức ảnh. Hướng dẫn này cho thấy cách chuyển đổi hình ảnh viết tay và nhận dạng văn
  bản từ các tệp jpg.
og_title: Thực hiện OCR trên ảnh – Hướng dẫn toàn diện về văn bản viết tay
tags:
- OCR
- Python
- Handwriting Recognition
title: Thực hiện OCR trên hình ảnh – Chuyển đổi hình ảnh viết tay thành văn bản
url: /vi/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên Hình ảnh – Trích xuất Văn bản Viết tay Toàn Stack

Bạn đã bao giờ cần **perform OCR on image** các tệp nhưng không chắc liệu engine có thể đọc được chữ viết tay lộn xộn không? Bạn không phải là người duy nhất. Trong nhiều ứng dụng thực tế—như máy quét biên lai chi phí hoặc công cụ ghi chú—bạn sẽ gặp phải những bức ảnh chứa các nét vẽ cần được chuyển thành văn bản thuần.  

Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **convert handwritten image** các tệp, **extract text from jpg**, và thậm chí **recognize text from photo** các luồng ảnh bằng một thư viện kiểu Python nhỏ gọi là `ocr`. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy để lấy ra mọi từ trong một ghi chú viết tay, bất kể bút có run rẩy như thế nào.

## Những gì bạn cần

- Python 3.8+ (mã chạy trên bất kỳ trình thông dịch hiện đại nào)
- Gói `ocr` giả định – cài đặt bằng `pip install ocr-lib` (thay bằng tên gói thực tế bạn dùng)
- Một bức ảnh rõ nét của ghi chú viết tay được lưu dưới dạng `note.jpg` (hoặc bất kỳ định dạng ảnh nào khác)
- Một chút tò mò—không yêu cầu kiến thức ML nâng cao

Chỉ vậy thôi. Không có dịch vụ bên ngoài, không có khóa API, chỉ một engine cục bộ có thể **perform OCR on image** dữ liệu.

![ảnh chụp màn hình perform OCR on image hiển thị trình soạn thảo mã với script OCR](example.png)

*Alt text: ảnh chụp màn hình perform OCR on image hiển thị trình soạn thảo mã với script OCR.*

## Triển khai từng bước

Dưới đây chúng tôi chia quy trình thành các phần nhỏ. Mỗi tiêu đề bao gồm một từ khóa để bạn có thể lướt nhanh, và mỗi khối giải thích **why** chúng ta làm gì—không chỉ **what**.

### Bước 1: Cài đặt và Xác minh Thư viện OCR

Trước khi bạn có thể **perform OCR on image** các tệp, thư viện phải có trong môi trường của bạn. Mở terminal và chạy:

```bash
pip install ocr-lib
```

> **Mẹo:** Nếu bạn làm việc trong môi trường ảo (rất được khuyến nghị), hãy kích hoạt nó trước. Điều này giữ cho các phụ thuộc của bạn gọn gàng và tránh xung đột phiên bản.

Sau khi cài đặt, hãy chắc chắn Python có thể import gói:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

Nếu bạn thấy thông báo thành công, bạn đã sẵn sàng **convert handwritten image** dữ liệu.

### Bước 2: Tạo một Instance Engine và Chọn Chế độ Handwritten

Hầu hết các engine OCR mặc định nhận dạng văn bản in. Vì chúng ta muốn **extract handwritten text**, chúng ta cần chuyển chế độ một cách rõ ràng. Bước này quan trọng vì chữ viết tay thường yêu cầu tiền xử lý khác (như làm mịn nét).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Tại sao điều này quan trọng:* Các ký tự viết tay có thể thay đổi mạnh về kích thước và góc nghiêng. Bằng cách đặt `RecognitionMode.HANDWRITTEN`, engine áp dụng mô hình đã được huấn luyện trên các mẫu chữ viết liền, tăng độ chính xác đáng kể.

### Bước 3: Tải ảnh bạn muốn phân tích

Bây giờ chúng ta thực sự **perform OCR on image** nội dung. Phương thức `load_image` chấp nhận một đường dẫn hoặc một đối tượng giống file. Để minh họa, chúng ta sẽ tải một JPEG, nhưng cùng một lệnh cũng hoạt động với PNG, BMP, hoặc thậm chí các trang PDF.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

Nếu ảnh của bạn nằm trong bucket đám mây, chỉ cần tải xuống trước hoặc truyền một luồng `BytesIO`—`ocr` đủ linh hoạt để xử lý cả hai.

### Bước 4: Chạy quy trình Nhận dạng

Với engine đã sẵn sàng và ảnh trong bộ nhớ, cuối cùng chúng ta **perform OCR on image** và lấy về văn bản thô.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

Lệnh `recognize()` trả về một chuỗi Unicode thuần. Đối với hầu hết các trường hợp sử dụng, bạn có thể ghi trực tiếp vào tệp `.txt`, đưa vào pipeline ngôn ngữ tự nhiên, hoặc hiển thị trong GUI.

### Bước 5: Tùy chọn – Dọn dẹp hoặc Xử lý hậu kỳ Kết quả

OCR chữ viết tay không hoàn hảo; bạn thường sẽ thấy các dấu ngắt dòng lẻ hoặc ký tự nhận sai. Một bước dọn dẹp nhanh có thể cải thiện kết quả downstream.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

Bạn có thể tự do tích hợp bộ kiểm tra chính tả, mô hình ngôn ngữ, hoặc regex tùy chỉnh tùy theo lĩnh vực của mình.

### Toàn bộ Script – Sẵn sàng Sao chép & Dán

Kết hợp mọi thứ lại, đây là chương trình đầy đủ, có thể chạy được mà **extracts handwritten text** từ một JPEG và in ra kết quả gọn gàng.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Kết quả mong đợi** (văn bản thực tế của bạn sẽ khác, tất nhiên):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

Nếu bạn thấy kết quả rối rắm, hãy kiểm tra lại chất lượng ảnh (ánh sáng tốt, ít mờ) và chắc chắn bạn đang ở chế độ `HANDWRITTEN`. Hai yếu tố này chiếm phần lớn lỗi nhận dạng.

## Câu hỏi Thường gặp (FAQ)

| Question | Answer |
|----------|--------|
| **Tôi có thể dùng điều này để trích xuất văn bản từ PNG không?** | Chắc chắn. `engine.load_image("scan.png")` hoạt động tương tự. |
| **Nếu ảnh của tôi là một trang PDF thì sao?** | Đầu tiên chuyển trang thành ảnh (ví dụ, bằng `pdf2image`) rồi đưa vào engine. |
| **Thư viện có an toàn với đa luồng không?** | Có, bạn có thể tạo các đối tượng `OcrEngine` riêng cho mỗi luồng. |
| **Điểm khác biệt so với `pytesseract` là gì?** | `ocr` ẩn đi binary Tesseract và bao gồm một mô hình viết tay tích hợp, vì vậy bạn không cần cài đặt các thực thi bên ngoài. |
| **Nếu tôi cần **extract text from JPG** các tệp hàng loạt thì sao?** | Bao bọc script trong một vòng lặp, hoặc dùng `engine.load_image` cho mỗi tệp và thu thập kết quả vào danh sách hoặc CSV. |

## Các Trường hợp Cạnh & Thực hành Tốt nhất

1. **Low‑contrast photos** – Tăng độ tương phản bằng lập trình trước khi tải, hoặc sử dụng `engine.apply_preprocessing('contrast', level=2)`.
2. **Mixed printed & handwritten** – Thực hiện hai lần: đầu tiên với `HANDWRITTEN`, sau đó với `PRINTED`, và hợp nhất các kết quả.
3. **Large images** – Thu nhỏ xuống khoảng ~1500 px chiều rộng; các engine OCR thường chạy nhanh hơn với bộ nhớ đệm nhỏ hơn mà không mất độ chính xác.
4. **Unicode characters** – Thư viện trả về chuỗi UTF‑8, vì vậy bạn có thể xử lý emoji, ký tự có dấu, hoặc ký hiệu toán học ngay từ đầu.

## Tổng kết

Chúng tôi vừa đi qua một ví dụ thực tế về cách **perform OCR on image** các tệp, đặc biệt nhắm vào các ghi chú viết tay. Bằng cách cài đặt gói `ocr`, cấu hình engine ở chế độ `HANDWRITTEN`, tải ảnh, và gọi `recognize()`, bạn có thể **convert handwritten image** dữ liệu thành văn bản sạch, có thể tìm kiếm.  

Từ đây bạn có thể **extract text from jpg** các tệp hàng loạt, đưa kết quả vào ứng dụng ghi chú, hoặc kết hợp với tổng hợp giọng nói để tăng khả năng tiếp cận. Không giới hạn, và đoạn mã trên cung cấp nền tảng vững chắc để thử nghiệm.

Có một cách tiếp cận bạn muốn chia sẻ—có thể là định dạng tệp khác hoặc một thủ thuật tiền xử lý độc đáo? Hãy để lại bình luận, và chúng ta sẽ tiếp tục trao đổi. Chúc bạn lập trình vui vẻ, và tận hưởng việc biến những nét vẽ thành vàng kỹ thuật số!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
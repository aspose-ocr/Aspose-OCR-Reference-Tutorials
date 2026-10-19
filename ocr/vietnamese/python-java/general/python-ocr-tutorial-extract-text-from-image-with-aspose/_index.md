---
category: general
date: 2026-03-26
description: 'Hướng dẫn OCR Python: học cách trích xuất văn bản từ hình ảnh, tải hình
  ảnh cho OCR và nhận dạng văn bản từ biên lai bằng Aspose OCR chỉ trong vài bước.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: vi
og_description: 'Hướng dẫn OCR Python: nhanh chóng học cách trích xuất văn bản từ
  hình ảnh, tải hình ảnh cho OCR và nhận dạng văn bản từ biên lai bằng Aspise OCR.'
og_title: Hướng dẫn OCR bằng Python – Trích xuất văn bản từ hình ảnh
tags:
- OCR
- Aspose
- Python
title: Hướng dẫn OCR bằng Python – Trích xuất văn bản từ hình ảnh với Aspose
url: /vi/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng dẫn OCR Python – Trích xuất Văn bản từ Hình ảnh với Aspose

Bạn đã bao giờ tự hỏi làm sao để lấy văn bản ra từ một hoá đơn mờ hoặc một mẫu quét mà không phải tốn hàng giờ viết các biểu thức chính quy tùy chỉnh? Bạn không đơn độc. Trong **python ocr tutorial** này, chúng ta sẽ đi qua các bước tải ảnh để OCR, thực hiện OCR trong Python, và cuối cùng nhận dạng văn bản từ các tệp hoá đơn bằng thư viện Aspose OCR.  

Khi hoàn thành hướng dẫn này, bạn sẽ có một script sẵn sàng chạy, có thể đọc bất kỳ định dạng ảnh nào được hỗ trợ, trích xuất nội dung văn bản và in ra console. Không cần dịch vụ bên ngoài, không cần khóa API — chỉ cần Python thuần và một engine OCR mạnh mẽ.  

## Những gì bạn cần

- Python 3.8 hoặc mới hơn (code sử dụng type hints, vì vậy phiên bản interpreter mới nhất là tốt nhất)
- Gói `asposeocrjava` được cài đặt qua `pip install aspose-ocr`
- Một ảnh mẫu — ví dụ `receipt_noisy.jpg` chứa một hoá đơn cửa hàng điển hình
- (Tùy chọn) Môi trường ảo để quản lý các phụ thuộc một cách gọn gàng

Nếu bạn đã có đầy đủ các mục trên, chúng ta có thể ngay lập tức chuyển sang phần code.  

## Bước 1: Cài đặt và Import các lớp Aspose OCR

Đầu tiên, đảm bảo gói Aspose OCR đã sẵn sàng. Sau đó import các lớp cần thiết.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Tại sao lại quan trọng:** Chỉ import những ký hiệu cần thiết giúp giữ namespace sạch sẽ và thông báo cho interpreter những phần nào của thư viện chúng ta thực sự sử dụng. Nó cũng làm ngắn hơn các dòng code sau, giúp tutorial dễ theo dõi hơn.

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Jupyter notebook, hãy đặt dấu `!` trước dòng cài đặt để chạy trong‑cell.

## Bước 2: Tạo Engine OCR và Bật chế độ Deep‑Learning

Aspose cung cấp một số chế độ engine. Đối với hầu hết các hoá đơn thực tế, mô hình deep‑learning mang lại độ chính xác cao nhất, đặc biệt với các bản quét nhiễu.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Tại sao lại là deep‑learning?** OCR dựa trên quy tắc truyền thống có thể gặp khó khăn với các ký tự có độ tương phản thấp hoặc bị biến dạng. Mô hình deep‑learning, được huấn luyện trên hàng triệu glyph, thích nghi tốt hơn với các biến thể — chính xác những gì bạn cần khi *perform OCR in Python* trên các hoá đơn chụp bằng điện thoại.

## Bước 3: Tải Ảnh để OCR

Bây giờ chúng ta thực sự **load image for OCR**. Aspose.Imaging hỗ trợ PNG, JPEG, BMP, TIFF và nhiều định dạng khác, vì vậy bạn có thể chỉ tới hầu như bất kỳ bức ảnh tài liệu nào.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Cạm bẫy thường gặp:** Quên gọi `set_image` trên engine sẽ gây ra `NullReferenceException` khi chạy. Luôn luôn gọi `set_image` sau khi đã tải file.

## Bước 4: Thực hiện OCR và Trích xuất Văn bản

Với engine đã sẵn sàng và ảnh đã được gắn, chúng ta cuối cùng có thể **perform OCR in Python** và lấy kết quả văn bản.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

Phương thức `recognize()` trả về một đối tượng `OcrResult` chứa không chỉ văn bản thô mà còn các điểm tin cậy, bounding box và thông tin ngôn ngữ. Đối với trường hợp **extract text from image** nhanh chóng, chúng ta chỉ cần `get_text()`.

## Bước 5: Hiển thị Văn bản Được Nhận dạng

Hãy xem engine thực sự đã đọc gì từ hoá đơn.

```python
print("Recognized text:\n", recognized_text)
```

Kết quả điển hình trông như sau:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Nếu kết quả chứa các ký tự lộn xộn, hãy cân nhắc tiền xử lý ảnh (ví dụ: tăng độ tương phản hoặc áp dụng bộ lọc deskew) trước khi tải vào engine OCR. Aspose.Imaging cung cấp một bộ công cụ nâng cao ảnh đầy đủ mà bạn có thể xâu chuỗi lại với nhau.

## Xử lý Các Trường hợp Cạnh & Mẹo để Cải thiện Độ chính xác

### 1. Xử lý các Hoá đơn Rất Nhiễu
Nếu hoá đơn bị nhòe mạnh, bạn có thể chuyển sang chế độ `OcrEngineMode.HIGH_SPEED` để thực hiện một lượt nhanh, dù độ chính xác thấp hơn, sau đó chạy một lượt thứ hai ở chế độ `DEEP_LEARNING` trên ảnh đã được làm sạch.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Chỉ định Ngôn ngữ
Mặc định Aspose sẽ tự động phát hiện ngôn ngữ. Đối với hoá đơn tiếng Anh, bạn có thể khóa ngôn ngữ như sau:

```python
ocr_engine.set_language("eng")
```

### 3. Quản lý Bộ nhớ
Khi xử lý nhiều ảnh trong một vòng lặp, hãy giải phóng tài nguyên một cách rõ ràng:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. Lưu Kết quả OCR vào File
Đôi khi bạn cần lưu văn bản đã trích xuất để phân tích sau.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Ví dụ Hoàn chỉnh

Dưới đây là script đầy đủ kết nối mọi thành phần. Sao chép‑dán nó vào file có tên `receipt_ocr.py`, điều chỉnh đường dẫn ảnh, và chạy `python receipt_ocr.py`.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

Chạy script sẽ hiển thị nội dung hoá đơn trong console và đồng thời tạo file `receipt_output.txt` với cùng dữ liệu.

![Hướng dẫn OCR Python – mẫu kết quả biên lai](https://example.com/receipt_output.png "ví dụ hướng dẫn OCR python")

*Văn bản thay thế hình ảnh:* **hướng dẫn OCR python – mẫu kết quả biên lai**

## Tổng kết & Các Bước Tiếp Theo

Chúng ta vừa đi qua một **python ocr tutorial** cho thấy cách **load image for OCR**, **perform OCR in Python**, và cuối cùng **recognize text from receipt** bằng Aspose. Những điểm chính cần nhớ là:

- Chọn chế độ engine phù hợp (deep‑learning cho độ chính xác)
- Luôn gắn ảnh trước khi gọi `recognize()`
- Sử dụng đối tượng `OcrResult` để lấy văn bản sạch, sau đó lưu hoặc xử lý theo nhu cầu

Tiếp theo bạn có thể: kết hợp các bộ lọc Aspose Imaging để cải thiện các bản quét độ tương phản thấp, hoặc tích hợp script vào một API Flask để cho phép tải lên hoá đơn qua biểu mẫu web. Bạn cũng có thể khám phá việc xuất dữ liệu OCR ra CSV để tự động hoá kế toán.

Có câu hỏi về xử lý PDF đa trang hoặc các script không phải Latin? Hãy để lại bình luận — mình sẵn sàng hỗ trợ!  

**Sẵn sàng nâng tầm tự động hoá tài liệu?** Lấy code, thử nghiệm với các ảnh khác nhau, và để engine OCR làm phần việc nặng. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
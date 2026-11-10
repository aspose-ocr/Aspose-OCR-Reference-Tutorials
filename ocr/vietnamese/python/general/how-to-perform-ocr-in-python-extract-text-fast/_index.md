---
category: general
date: 2026-03-26
description: Học cách thực hiện OCR trong Python và dễ dàng trích xuất văn bản từ
  hình ảnh, đọc văn bản từ bản quét, hoặc trích xuất văn bản từ hoá đơn bằng OcrEngine
  đơn giản.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: vi
og_description: Cách thực hiện OCR trong Python? Hướng dẫn này cho bạn biết cách trích
  xuất văn bản từ hình ảnh, đọc văn bản từ bản quét và trích xuất văn bản từ hoá đơn
  trong vài phút.
og_title: Cách thực hiện OCR trong Python – Trích xuất văn bản nhanh
tags:
- OCR
- Python
- Image Processing
title: Cách thực hiện OCR trong Python – Trích xuất văn bản nhanh
url: /vi/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện OCR trong Python – Trích Xuất Văn Bản Nhanh Chóng

Bạn đã bao giờ tự hỏi **cách thực hiện OCR** trên một biên lai đã quét hoặc một tệp PDF mờ chưa? Bạn không phải là người duy nhất. Trong nhiều dự án, nhu cầu **trích xuất văn bản từ hình ảnh** xuất hiện sớm hơn dự kiến, và cách tiếp cận “gõ tay mọi thứ” thông thường không thể mở rộng.  

Trong hướng dẫn này, bạn sẽ thấy một ví dụ hoàn chỉnh, sẵn sàng chạy, cho thấy **cách sử dụng OCR** để đọc văn bản từ bản quét, lấy dữ liệu từ hoá đơn, và thậm chí xử lý tự động việc chỉnh độ nghiêng—tất cả chỉ với vài dòng Python.

## Những Điều Bạn Sẽ Học

Chúng tôi sẽ đi qua mọi thứ bạn cần biết:

* Các phụ thuộc và import cần thiết.
* Cách tạo và cấu hình một thể hiện `OcrEngine`.
* Các cách **trích xuất văn bản từ hình ảnh**, **đọc văn bản từ bản quét**, và **trích xuất văn bản từ hoá đơn** bằng cùng một engine.
* Những bẫy thường gặp (ngôn ngữ sai, thiếu tệp, hình ảnh lớn) và cách tránh chúng.
* Kết quả mong đợi để bạn có thể xác minh OCR đã thành công.

Không cần liên kết tài liệu bên ngoài—mọi thứ đều tự chứa, vì vậy bạn có thể sao chép‑dán mã và thấy kết quả ngay lập tức.

## Yêu Cầu Trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* Python 3.8+ đã được cài đặt (gói `ocr` hoạt động với bất kỳ phiên bản mới nào).
* Thư viện `ocr` có sẵn (`pip install ocr‑engine` – thay thế bằng tên gói thực tế nếu khác).
* Một tệp hình ảnh bạn muốn xử lý – trong bản demo chúng ta sẽ dùng `invoice.png` nằm trong thư mục có tên `YOUR_DIRECTORY`.

Xong rồi. Nếu bạn đã có những thứ này, bạn đã sẵn sàng.

## Bước 1: Cài Đặt và Import Module OCR

Đầu tiên: chúng ta cần thư viện OCR. Nếu bạn chưa cài đặt, hãy chạy lệnh sau trong terminal:

```bash
pip install ocr-engine
```

Bây giờ chúng ta import module vào script.

```python
# Step 1: Import the OCR module
import ocr
```

> **Mẹo:** Giữ môi trường ảo của bạn gọn gàng; nó ngăn ngừa xung đột phiên bản khi bạn sau này thêm các gói xử lý ảnh khác.

## Bước 2: Tạo và Cấu Hình Engine OCR

Việc tạo engine đơn giản như gọi constructor của nó, nhưng sức mạnh thực sự nằm ở việc cấu hình đúng. Chúng ta sẽ đặt ngôn ngữ là tiếng Anh và bật tính năng tự động chỉnh độ nghiêng, điều này rất quan trọng khi xử lý các hoá đơn đã quét không được căn chỉnh hoàn hảo.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Tại sao bật `auto_skew`? Nhiều máy quét tạo ra hình ảnh lệch vài độ. Nếu không chỉnh sửa, engine có thể bỏ sót ký tự, biến một hoá đơn đọc được thành mớ hỗn độn.

## Bước 3: Thực Hiện OCR trên Hình Ảnh Mục Tiêu

Bây giờ chúng ta đưa tệp hình ảnh vào engine. Phương thức `recognize_image` trả về một đối tượng chứa văn bản thô cũng như điểm tin cậy (nếu thư viện cung cấp).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Nếu bạn đang làm việc với trường hợp **đọc văn bản từ bản quét**, chỉ cần thay đổi đường dẫn thành PDF đã quét được chuyển đổi sang PNG hoặc JPEG. Lệnh gọi này hoạt động với bất kỳ định dạng ảnh nào mà thư viện nền hỗ trợ.

## Bước 4: Kiểm Tra và Sử Dụng Văn Bản Đã Trích Xuất

Hãy in ra kết quả OCR thô. Trong một quy trình xử lý hoá đơn thực tế, bạn có thể sẽ phân tích chuỗi này, trích xuất các mục, tổng tiền và ngày tháng, nhưng hiện tại một cái nhìn nhanh sẽ xác nhận OCR đã thành công.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Kết quả mong đợi (rút gọn để ngắn gọn):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Nếu kết quả trông rối mắt, hãy kiểm tra lại hình ảnh có rõ ràng không và `engine.language` có khớp với ngôn ngữ của tài liệu không.

## Bước 5: Xử Lý Các Trường Hợp Cạnh Thường Gặp

### Hình Ảnh Lớn

Xử lý một bản quét 5000 × 5000 pixel có thể tốn nhiều bộ nhớ. Cách nhanh để giảm thiểu là thu nhỏ hình ảnh trước khi gửi tới engine:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Nhiều Ngôn Ngữ

Nếu bạn cần **trích xuất văn bản từ hình ảnh** chứa cả tiếng Anh và tiếng Tây Ban Nha, bạn có thể đặt danh sách ngôn ngữ:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Engine sẽ cố gắng nhận dạng ký tự từ cả hai bộ.

### Xử Lý Lỗi

Không bao giờ giả định tệp tồn tại. Bao bọc lời gọi trong khối try‑except để đưa ra thông báo thân thiện:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Tham Khảo Hình Ảnh

Dưới đây là ảnh chụp màn hình của mẫu hoá đơn chúng tôi dùng trong bản demo. Lưu ý độ nghiêng nhẹ—đó chính là thứ mà `auto_skew` sửa chữa.

![cách thực hiện OCR trên một hoá đơn](/images/ocr-example.png)

*Alt text:* cách thực hiện OCR trên hình ảnh hoá đơn, hiển thị việc tự động chỉnh độ nghiêng.

## Ví Dụ Đầy Đủ, Có Thể Chạy

Kết hợp mọi thứ lại, đây là một script đơn lẻ bạn có thể chạy từ dòng lệnh. Nó bao gồm cài đặt, cấu hình, xử lý lỗi, và một bước hậu xử lý đơn giản ghi văn bản đã trích xuất vào tệp có tên `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Chạy `python full_ocr_demo.py` sẽ in văn bản đã trích xuất ra console và lưu vào `output.txt`. Từ đó bạn có thể áp dụng biểu thức chính quy, ghi CSV, hoặc bất kỳ logic nào khác bạn cần cho việc tự động **trích xuất văn bản từ hoá đơn**.

## Kết Luận

Bây giờ bạn đã có một giải pháp toàn diện, đầu‑tới‑cuối cho **cách thực hiện OCR** trong Python. Bằng cách tạo một `OcrEngine`, cấu hình ngôn ngữ và chỉnh độ nghiêng, và xử lý một vài trường hợp cạnh thực tế, bạn có thể một cách đáng tin cậy **trích xuất văn bản từ hình ảnh**, **đọc văn bản từ bản quét**, và **trích xuất văn bản từ hoá đơn** mà không phải lục lọi tài liệu rải rác.

Tiếp theo là gì? Hãy thử đưa một loạt tệp vào vòng lặp, thử nghiệm với các ngôn ngữ khác nhau, hoặc kết nối đầu ra với thư viện tạo PDF để tạo PDF có thể tìm kiếm. Không gì là không thể, và đoạn mã bạn vừa thấy là một bệ phóng vững chắc.

Có câu hỏi về định dạng tệp cụ thể hoặc cần trợ giúp điều chỉnh ngưỡng tin cậy? Hãy để lại bình luận bên dưới—rất vui được giúp bạn tinh chỉnh quy trình OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
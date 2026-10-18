---
category: general
date: 2026-03-26
description: Học cách thực hiện OCR trong Python và nhận dạng văn bản từ các tệp hình
  ảnh. Hướng dẫn này cho thấy cách trích xuất văn bản từ PNG và chuyển đổi hình ảnh
  thành văn bản một cách nhanh chóng.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: vi
og_description: Cách thực hiện OCR trong Python? Hãy theo hướng dẫn này để nhận dạng
  văn bản từ hình ảnh, trích xuất văn bản từ PNG và chuyển đổi hình ảnh thành văn
  bản với giấy phép dùng thử.
og_title: Cách thực hiện OCR trong Python – Hướng dẫn đầy đủ
tags:
- OCR
- Python
- Image Processing
title: Cách thực hiện OCR trong Python – Hướng dẫn chi tiết từng bước
url: /vi/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện OCR trong Python – Hướng Dẫn Bước‑đầu Hoàn Chỉnh  

Bạn đã bao giờ tự hỏi **cách thực hiện OCR** trên một bức ảnh bạn vừa chụp bằng điện thoại chưa? Bạn không đơn độc—các nhà phát triển trên toàn thế giới cần một cách đáng tin cậy để nhận dạng văn bản từ các tệp hình ảnh mà không phải vật lộn với các thư viện gốc phức tạp.  

Trong tutorial này chúng ta sẽ đi qua một ví dụ thực hành cho thấy **cách thực hiện OCR**, **nhận dạng văn bản từ hình ảnh**, và **trích xuất văn bản từ PNG** bằng một wrapper Python nhẹ. Khi kết thúc, bạn sẽ có thể **chuyển đổi hình ảnh thành văn bản** chỉ trong vài dòng code, và bạn sẽ không phải lo lắng về các vấn đề giấy phép vì chúng ta sẽ sử dụng chế độ dùng thử tích hợp.

## Những Điều Bạn Sẽ Học  

* Cách thiết lập giấy phép dùng thử cho engine OCR (không cần đường dẫn tệp).  
* Trình tự chính xác các lời gọi để **nhận dạng văn bản từ hình ảnh**.  
* Các cách **trích xuất văn bản từ PNG** và xử lý các vấn đề thường gặp như thiếu phông chữ.  
* Mẹo mở rộng giải pháp khi bạn chuyển từ giấy phép dùng thử sang giấy phép sản xuất.  

**Prerequisites** – bạn cần Python 3.8+ và gói `ocr` (có thể cài đặt bằng `pip install ocr`). Không cần công cụ bên ngoài nào khác.

---  

![ví dụ cách thực hiện OCR](https://example.com/ocr-demo.png "cách thực hiện OCR trong Python – văn bản đã nhận dạng hiển thị")  

*Văn bản thay thế hình ảnh: cách thực hiện OCR trong Python – mẫu kết quả*  

## Bước 1 – Kích Hoạt Giấy Phép Dùng Thử (Không Cần Đường Dẫn Tệp)  

Trước khi engine có thể đọc bất kỳ thứ gì, nó cần một giấy phép hợp lệ. Chế độ dùng thử là lựa chọn hoàn hảo cho các thí nghiệm và dự án nhỏ.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Why this matters:* Đối tượng license thông báo cho thư viện OCR rằng bạn đang hoạt động trong môi trường sandbox. Nếu bỏ qua bước này, engine sẽ ném ra `LicenseError` ngay khi bạn gọi `recognize()`.  

**Pro tip:** Khi bạn chuyển sang giấy phép trả phí, thay thế hai dòng trên bằng `ocr.License("path/to/your/license.key").apply()`.

## Bước 2 – Tạo Instance của Engine OCR  

Bây giờ giấy phép dùng thử đã được kích hoạt, chúng ta khởi tạo engine chính. Hãy nghĩ nó như “bộ não” sẽ nhìn vào hình ảnh và quyết định ký tự nào nằm ở đâu.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Why this matters:* `OcrEngine` chứa các cấu hình như gói ngôn ngữ và thiết lập DPI. Bạn có thể điều chỉnh chúng sau, nhưng mặc định đã hoạt động tốt cho hầu hết các PNG chỉ có tiếng Anh.

## Bước 3 – Tải PNG Bạn Muốn Xử Lý  

Đây là nơi chúng ta **nhận dạng văn bản từ hình ảnh**. Phương thức `ocr.Imaging.Image.load()` hỗ trợ PNG, JPEG, BMP và một vài định dạng khác.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Edge case:* Nếu PNG của bạn sử dụng bảng màu chỉ mục (thường gặp trong ảnh chụp màn hình), bộ tải sẽ tự động chuyển đổi nó sang bộ đệm RGB 24‑bit. Việc chuyển đổi này có thể gây một chút giảm hiệu năng, nhưng nó đảm bảo kết quả OCR chính xác.

## Bước 4 – Chạy OCR và Lấy Văn Bản  

Cuối cùng, chúng ta yêu cầu engine thực hiện công việc và sau đó lấy kết quả dạng plain‑text.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Expected output** (ví dụ cho một hình ảnh đơn giản chứa “Hello World”):

```
Hello World
```

Nếu hình ảnh chứa nhiều dòng, đầu ra sẽ giữ nguyên các ký tự xuống dòng, giúp dễ dàng đưa vào các quy trình tiếp theo như bộ phân tích CSV hoặc pipeline NLP.

## Tùy Chọn: Tinh Chỉnh Để Độ Chính Xác Cao Hơn  

* **Language packs:** `ocr_engine.set_language("eng")` (mặc định) hoặc `"fra"` cho tiếng Pháp.  
* **DPI scaling:** `ocr_engine.set_dpi(300)` có thể cải thiện kết quả trên các bản quét độ phân giải thấp.  
* **Pre‑processing:** Áp dụng ngưỡng nhị phân (`ocr.Imaging.Image.threshold()`) trước `set_image` thường cho ra văn bản sạch hơn trên nền nhiễu.

Những điều chỉnh này hữu ích khi bạn chuyển từ một demo nhanh sang một **ocr tutorial python** cấp sản xuất xử lý hàng trăm tệp mỗi ngày.

## Toàn Bộ Script – Sẵn Sàng Sao Chép & Dán  

Dưới đây là script hoàn chỉnh, có thể chạy được, kết hợp tất cả các bước ở trên. Lưu lại dưới tên `run_ocr.py` và thay thế `YOUR_DIRECTORY/sample1.png` bằng đường dẫn tới PNG của bạn.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Chạy nó từ dòng lệnh:

```bash
python run_ocr.py
```

Bạn sẽ thấy văn bản đã trích xuất được in ra console. Nếu nhận được một chuỗi rỗng, hãy kiểm tra lại rằng hình ảnh thực sự chứa văn bản rõ ràng, độ tương phản cao và giấy phép dùng thử đã được áp dụng mà không có lỗi.

## Câu Hỏi Thường Gặp & Những Trường Hợp Gây Nhầm Lẫn  

* **“Does this work with JPEG?”** – Hoàn toàn có thể. Phương thức `load()` tự động phát hiện định dạng, vì vậy bạn có thể thay PNG bằng JPEG mà không cần thay đổi code.  
* **“What if the image is rotated?”** – Engine có thể tự động phát hiện hướng, nhưng để có kết quả tốt nhất bạn có thể quay trước bằng `input_image.rotate(90)` trước khi gọi `set_image`.  
* **“Can I process multiple images in a loop?”** – Có. Chỉ cần đưa các lời gọi load và `recognize()` vào trong một vòng `for`; cùng một instance `ocr_engine` có thể được tái sử dụng, giúp giảm một chút overhead.

## Các Bước Tiếp Theo – Từ Demo Đến Sản Xuất  

Bây giờ bạn đã biết **cách thực hiện OCR**, hãy xem xét các chủ đề tiếp theo:

* **Batch processing** – Kết hợp script này với `os.listdir()` để **trích xuất văn bản từ PNG** hàng loạt.  
* **Integrate with PDF** – Sử dụng `pdf2image` để chuyển các trang PDF sang PNG, sau đó đưa chúng vào cùng một pipeline.  
* **Post‑processing** – Áp dụng regex hoặc fuzzy matching để làm sạch các lỗi nhận dạng thường gặp của OCR (ví dụ, “0” vs “O”).  

Mỗi mục trên đều dựa trên ý tưởng cốt lõi **chuyển đổi hình ảnh thành văn bản** và mở rộng tính hữu dụng của quy trình OCR của bạn.

---  

### TL;DR  

Chúng tôi đã bao phủ mọi thứ bạn cần biết để **cách thực hiện OCR** trong Python: kích hoạt giấy phép dùng thử, tạo engine, tải PNG, chạy nhận dạng và in kết quả. Chỉ với một vài dòng code, bạn có thể **nhận dạng văn bản từ hình ảnh**, **trích xuất văn bản từ PNG**, và **chuyển đổi hình ảnh thành văn bản** cho bất kỳ ứng dụng downstream nào.  

Hãy thử ngay, điều chỉnh DPI hoặc cài đặt ngôn ngữ, và để engine thực hiện phần công việc nặng. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
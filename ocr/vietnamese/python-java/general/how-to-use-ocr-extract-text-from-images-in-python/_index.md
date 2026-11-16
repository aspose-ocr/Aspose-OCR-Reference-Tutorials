---
category: general
date: 2026-03-18
description: Cách sử dụng OCR để trích xuất văn bản từ hình ảnh – hướng dẫn nhanh
  về nhận dạng văn bản từ các tệp PNG và tải hình ảnh cho OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: vi
og_description: Cách sử dụng OCR để trích xuất văn bản từ hình ảnh – học cách nhận
  dạng văn bản từ PNG, tải hình ảnh cho OCR và trích xuất văn bản bằng một script
  Python đơn giản.
og_title: 'Cách sử dụng OCR: Trích xuất văn bản từ hình ảnh trong Python'
tags:
- OCR
- Python
- Image Processing
title: 'Cách sử dụng OCR: Trích xuất văn bản từ hình ảnh trong Python'
url: /vi/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR: Trích Xuất Văn Bản Từ Hình Ảnh trong Python

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** khi có một ảnh chụp màn hình lộn xộn hoặc một biên lai đã quét chưa? Bạn không phải là người duy nhất—các nhà phát triển luôn cần lấy văn bản có thể đọc được từ hình ảnh, đặc biệt là các PNG xuất phát từ ứng dụng di động hoặc tải lên web. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ đầy đủ, có thể chạy được, cho bạn thấy cách **trích xuất văn bản từ hình ảnh** files, **nhận dạng văn bản từ PNG** assets, và thậm chí **tải hình ảnh cho OCR** chỉ với vài dòng Python.

Chúng tôi sẽ bao phủ mọi thứ từ cài đặt thư viện phù hợp đến xử lý tài liệu đa ngôn ngữ, vì vậy vào cuối bạn sẽ biết chính xác *cách trích xuất văn bản* từ bất kỳ hình ảnh nào bạn đưa vào công cụ. Không có tham chiếu mơ hồ, chỉ có một giải pháp rõ ràng, từng bước mà bạn có thể sao chép‑dán và chạy.

## Những Điều Bạn Sẽ Học

1. Cài đặt một engine OCR nhẹ (không cần các phụ thuộc nặng).  
2. Tải một tệp hình ảnh—cụ thể là PNG—vào engine.  
3. Bật phát hiện ngôn ngữ tự động để engine có thể xử lý nội dung đa ngôn ngữ.  
4. Chạy quá trình nhận dạng và lấy kết quả văn bản thuần.  
5. Tinh chỉnh quy trình cho các trường hợp biên như tệp bị thiếu hoặc định dạng không được hỗ trợ.

Nếu bạn đã quen với Python cơ bản, bạn đã sẵn sàng. Không cần kinh nghiệm OCR trước, mặc dù việc xem nhanh tài liệu của thư viện cũng không hại gì.

![Cách sử dụng OCR trên hình ảnh PNG](placeholder.png "Cách sử dụng OCR trên hình ảnh PNG – hướng dẫn từng bước")

## Cách Sử Dụng OCR – Tải Hình Ảnh và Nhận Dạng Văn Bản {#how-to-use-ocr}

### Bước 1: Cài đặt thư viện OCR

Đầu tiên, bạn cần một gói Python cung cấp lớp `OcrEngine`. Đối với mục đích của hướng dẫn này, chúng tôi sẽ sử dụng gói **SimpleOCR** giả tưởng nhưng minh họa, mà bạn có thể cài đặt qua pip:

```bash
pip install simple-ocr
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang làm việc trong môi trường ảo (rất được khuyến nghị), hãy kích hoạt nó trước khi chạy lệnh cài đặt. Điều này giữ cho các phụ thuộc dự án của bạn gọn gàng.

### Bước 2: Nhập engine và tạo một thể hiện

Tạo engine dễ dàng như việc gọi constructor của nó. Hãy nghĩ engine như “bộ não” sẽ xử lý hình ảnh bạn cung cấp sau này.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Tại sao chúng ta tạo một thể hiện mới mỗi lần? Để cô lập. Một engine mới đảm bảo không có trạng thái còn lại từ lần chạy trước làm ảnh hưởng đến nhận dạng hiện tại, điều này rất quan trọng khi bạn xử lý nhiều tệp trong một lô.

### Bước 3: Tải hình ảnh bạn muốn xử lý

Bây giờ chúng ta thực sự **tải hình ảnh cho OCR**. Phương thức `setImageFromFile` chấp nhận đường dẫn tới bất kỳ hình ảnh raster nào; chúng ta sẽ chỉ đến một PNG có tên `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Nếu tệp không được tìm thấy, `SimpleOCR` sẽ ném ra một `FileNotFoundError` rõ ràng. Bạn có thể bắt nó để cung cấp thông báo lỗi thân thiện:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Bước 4: Bật phát hiện ngôn ngữ tự động

Hầu hết các engine OCR hiện đại đi kèm với các gói ngôn ngữ. Bằng cách truyền `"multilingual"` chúng ta nói cho engine dò tìm văn bản và tự động chọn mô hình ngôn ngữ phù hợp. Điều này đặc biệt hữu ích khi PNG của bạn chứa hỗn hợp tiếng Anh và tiếng Tây Ban Nha, ví dụ.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Nếu bạn biết ngôn ngữ trước, bạn có thể thay thế `"multilingual"` bằng một locale cụ thể như `"eng"` hoặc `"spa"` để tăng tốc xử lý.

### Bước 5: Chạy quá trình nhận dạng

Công việc nặng nhất diễn ra ở đây. `recognize()` quét hình ảnh, áp dụng phân đoạn, chạy mạng nơ-ron, và xây dựng bộ đệm văn bản nội bộ.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Trong hậu trường, engine thực hiện:

- **Tiền xử lý** (điều chỉnh góc, nhị phân hoá)  
- **Phân tích bố cục** (phát hiện cột, bảng)  
- **Phân loại ký tự** (sử dụng mô hình deep‑learning)  

Tất cả những điều đó được trừu tượng hoá, vì vậy bạn chỉ cần một dòng.

### Bước 6: Lấy và in văn bản đã nhận dạng

Cuối cùng, chúng ta lấy đối tượng kết quả và trích xuất chuỗi thuần. Đây là phần mà bạn thực sự **trích xuất văn bản từ hình ảnh**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Kết quả mong đợi** (được rút gọn để ngắn gọn):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Nếu hình ảnh không chứa ký tự nào có thể nhận dạng, `text` sẽ là một chuỗi rỗng. Bạn có thể bảo vệ trước trường hợp này:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

## Trích Xuất Văn Bản Từ Hình Ảnh – Xử Lý Các Trường Hợp Cạnh Thông Thường

### Nhiều ngôn ngữ trong một tệp

Khi một tài liệu pha trộn các ngôn ngữ, cài đặt `"multilingual"` thường hoạt động đúng. Tuy nhiên, nếu bạn nhận thấy nhận dạng sai, bạn có thể tự chỉ định một danh sách dự phòng:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Định dạng không phải PNG

Mặc dù chúng ta tập trung vào **nhận dạng văn bản từ PNG**, `SimpleOCR` cũng chấp nhận JPEG, BMP và TIFF. Chỉ cần thay đổi phần mở rộng tệp trong `setImageFromFile`. Đối với các stack TIFF, bạn có thể cần chọn một trang cụ thể:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Tệp lớn và sử dụng bộ nhớ

Nếu bạn đang xử lý các bản quét gigapixel, hãy cân nhắc thay đổi kích thước trước khi OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Thay đổi kích thước giảm áp lực bộ nhớ trong khi vẫn giữ đủ chi tiết cho việc nhận dạng chính xác.

### Gỡ lỗi khi tải thất bại

Đôi khi một hình ảnh trông ổn với mắt nhưng bị hỏng bên trong. Bật ghi log chi tiết để xem engine nhìn thấy gì:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

## Script Hoàn Chỉnh, Sẵn Sàng Chạy

Dưới đây là chương trình đầy đủ kết hợp tất cả các phần lại với nhau. Sao chép nó vào một tệp có tên `ocr_demo.py`, điều chỉnh placeholder `YOUR_DIRECTORY`, và chạy `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Chạy script này sẽ xuất ra phiên bản văn bản thuần của bất kỳ nội dung nào trong `mixed_doc.png`. Bạn có thể tự do thay đổi tệp bằng bất kỳ hình ảnh nào khác—**cách trích xuất văn bản** hoạt động tương tự.

## Kết Luận

Chúng tôi vừa đi qua **cách sử dụng OCR** trong Python để **trích xuất văn bản từ hình ảnh** files, đặc biệt tập trung vào **nhận dạng văn bản từ PNG** assets và các bước thực tế để **tải hình ảnh cho OCR**. Đoạn mã trên là một giải pháp tự chứa: cài đặt gói, cung cấp tệp, bật phát hiện đa ngôn ngữ, chạy engine, và lấy kết quả.

Từ đây bạn có thể:

- Tích hợp script vào dịch vụ web nhận tải lên của người dùng.  
- Xử lý hàng loạt một thư mục các PDF đã chuyển thành PNG.  
- Thêm xử lý hậu kỳ (ví dụ: làm sạch regex, kiểm tra chính tả) để cải thiện độ chính xác.

Hãy nhớ, chất lượng OCR phụ thuộc vào độ rõ của hình ảnh, các gói ngôn ngữ phù hợp, và đôi khi một chút tiền xử lý—vì vậy hãy thử nghiệm

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
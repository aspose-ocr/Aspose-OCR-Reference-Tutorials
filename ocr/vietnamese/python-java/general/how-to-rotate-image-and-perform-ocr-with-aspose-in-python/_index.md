---
category: general
date: 2026-03-26
description: Học cách xoay ảnh và thực hiện OCR trong Python. Hướng dẫn này cũng chỉ
  cách tiền xử lý ảnh cho OCR và trích xuất văn bản từ ảnh một cách hiệu quả.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: vi
og_description: Cách xoay ảnh đúng cách và sau đó nhận dạng văn bản từ ảnh bằng Aspose
  OCR. Hãy làm theo hướng dẫn từng bước này để tiền xử lý ảnh cho OCR và trích xuất
  văn bản từ ảnh.
og_title: Cách Xoay Hình Ảnh và Thực Hiện OCR – Hướng Dẫn Python Đầy Đủ
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Cách Xoay Hình Ảnh và Thực Hiện OCR với Aspose trong Python
url: /vi/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Xoay Hình Ảnh và Thực Hiện OCR với Aspose trong Python

Bạn đã bao giờ tự hỏi **cách xoay hình ảnh** sao cho một công cụ OCR thực sự có thể đọc được văn bản? Có thể bạn đã quét một mẫu biểu và nó bị nghiêng, hoặc ảnh chụp bằng camera bị quay 90° theo chiều kim đồng hồ. Trong trường hợp đó, văn bản trông ổn với mắt người, nhưng công cụ OCR lại thấy hỗn loạn. Tin tốt? Việc chỉnh sửa hướng, cắt vùng bạn quan tâm, và sau đó trích xuất văn bản—tất cả chỉ với vài dòng Python và các thư viện Aspose—rất đơn giản.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: từ tải một tệp TIFF đã xoay, chỉnh sửa hướng, **tiền xử lý hình ảnh cho OCR**, và cuối cùng **nhận dạng văn bản từ hình ảnh**. Khi kết thúc, bạn sẽ biết **cách thực hiện OCR** trên bất kỳ hình ảnh nào và có thể **trích xuất văn bản từ hình ảnh** một cách tự tin.

## Những Gì Bạn Cần

- Python 3.8+ (mã chạy được với bất kỳ phiên bản mới nào)
- Các gói `asposeocrjava` và `asposeimaging` được cài đặt qua `pip`
- Một hình ảnh mẫu cần xoay (ví dụ: `rotated_form.tif`)
- Một chút tò mò về xử lý ảnh

Không cần các khung công tác nặng—chỉ cần hai gói Aspose và một chút logic Python.

---

## Bước 1: Cài Đặt Các Gói Aspose (Cách Thực Hiện OCR)

Trước khi chúng ta có thể **xoay hình ảnh** hoặc **nhận dạng văn bản từ hình ảnh**, chúng ta cần các thư viện thực hiện công việc nặng.

```bash
pip install asposeocrjava asposeimaging
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang ở sau proxy của công ty, thêm `--proxy http://proxy:port` vào lệnh. Các gói là các wrapper Python thuần cho lõi Aspose .NET/Java, vì vậy việc cài đặt thường ngay lập tức.

---

## Bước 2: Tải Tệp Nguồn và Xoay Nó – Bước Cốt Lõi “Cách Xoay Hình Ảnh”

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Tại sao phải xoay?** Hầu hết các công cụ OCR giả định văn bản đọc từ trái sang phải và từ trên xuống dưới. Nếu bitmap bị quay sang bên, công cụ sẽ trả về ký tự rác hoặc không trả gì cả. Việc xoay căn chỉnh lưới pixel với thứ tự đọc mong đợi, cải thiện độ chính xác đáng kể.

> **Trường hợp đặc biệt:** Nếu bạn không chắc hình ảnh cần quay 90°, 180° hay 270°, bạn có thể kiểm tra `source_image.width` so với `source_image.height` hoặc sử dụng thẻ định hướng `exif`. Phương thức `rotate_flip` của Aspose cũng hỗ trợ `ROTATE_180` và `ROTATE_270_CLOCKWISE`.

> **Xem trước hình ảnh (tùy chọn):**  
> ![how to rotate image example](/assets/rotate-demo.png "How to rotate image – before and after rotation")

---

## Bước 3: Cắt Vùng Quan Tâm – Tiền Xử Lý Hình Ảnh cho OCR

Thường bạn chỉ cần một phần nhỏ của trang—ví dụ, trường chữ ký hoặc một khối số. Việc cắt bỏ nhiễu và tăng tốc **cách thực hiện OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Tại sao phải cắt?** Giảm kích thước hình ảnh giới hạn không gian tìm kiếm của công cụ OCR, giảm các kết quả sai và rút ngắn thời gian xử lý. Nó cũng hữu ích nếu tệp nguồn chứa watermark hoặc đồ họa khác có thể gây nhầm lẫn cho công cụ.

> **Mẹo:** Nếu bạn đang xử lý nhiều trường, lặp lại bước cắt với các hình chữ nhật khác nhau và chạy OCR trên từng phần riêng biệt.

---

## Bước 4: Khởi Tạo Engine OCR – Cốt Lõi “Cách Thực Hiện OCR”

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Phía sau:** Aspose OCR sử dụng kết hợp Tesseract và phân tích ảnh độc quyền. Khởi tạo engine một lần và tái sử dụng cho nhiều hình ảnh hiệu quả hơn so với việc tạo đối tượng mới mỗi lần.

---

## Bước 5: Cung Cấp Hình Ảnh Đã Cắt và Nhận Dạng Văn Bản – Cách Trích Xuất Văn Bản từ Hình Ảnh

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Kết Quả Dự Kiến

Nếu ROI chứa cụm từ “Invoice #12345 – Paid”, bạn sẽ thấy gì đó như:

```
Invoice #12345 – Paid
```

Nếu OCR gặp khó khăn, bạn có thể nhận được các khoảng trắng thừa hoặc ký tự đọc sai (ví dụ, “Invo1ce #I2345 – Pa1d”). Đó là lúc các mẹo **tiền xử lý hình ảnh cho OCR**—như điều chỉnh độ tương phản hoặc áp dụng nhị phân hoá—được áp dụng. Aspose cung cấp các bộ lọc bổ sung mà bạn có thể xâu chuỗi trước bước 5, nhưng luồng cơ bản trên hoạt động với hầu hết các bản quét sạch.

---

## Bước 6: Tùy Chọn – Tinh Chỉnh Cài Đặt OCR (Nâng Cao “Cách Thực Hiện OCR”)

Nếu bạn cần độ chính xác cao hơn cho một ngôn ngữ cụ thể hoặc muốn bỏ qua một số ký tự, bạn có thể điều chỉnh engine:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Khi nào sử dụng:** Dùng khi tài liệu chứa nhiều ký hiệu trang trí mà bạn không quan tâm. Danh sách đen giảm các phát hiện sai.

---

## Kịch Bản Toàn Bộ Từ Đầu Đến Cuối

Kết hợp mọi thứ lại, đây là một script sẵn sàng chạy mà **cách xoay hình ảnh**, **tiền xử lý hình ảnh cho OCR**, và cuối cùng **nhận dạng văn bản từ hình ảnh**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Chạy script này sẽ in văn bản đã nhận dạng ra console và lưu hình ảnh trực quan của ROI đã xử lý dưới dạng `processed_roi.png`. Bạn có thể mở PNG đó để xác nhận việc xoay và cắt đã hoạt động như mong đợi.

---

## Câu Hỏi Thường Gặp & Lưu Ý

| Question | Answer |
|----------|--------|
| **Nếu hình ảnh đã thẳng đứng rồi thì sao?** | Bước xoay là idempotent—xoay một hình ảnh đã đúng hướng 90° sẽ chắc chắn làm hỏng nó, vì vậy bạn nên kiểm tra `source_image.width` so với `height` hoặc sử dụng dữ liệu định hướng EXIF trước khi gọi `rotate_flip`. |
| **Kết quả OCR của tôi chứa các ngắt dòng thừa.** | Sử dụng `result.get_text().replace("\n", " ").strip()` để làm sạch, hoặc bật `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Tôi có thể xử lý PDF trực tiếp không?** | Có—Aspose Imaging có thể tải các trang PDF dưới dạng hình ảnh (`Image.load("file.pdf")`), sau đó bạn thực hiện các bước xoay và OCR tương tự. |
| **Có cách nào để xử lý hàng loạt nhiều tệp không?** | Bao bọc `ocr_rotated_image` trong một vòng lặp qua thư mục, hoặc dùng `concurrent.futures` của Python để song song hoá. |
| **Làm thế nào để xử lý các ngôn ngữ khác ngoài tiếng Anh?** | Đặt ngôn ngữ nhận dạng bằng `ocr_engine.get_recognition_settings().set_recognition_language("fr")` cho tiếng Pháp, v.v. |

---

## Kết Luận

Chúng ta đã đề cập **cách xoay hình ảnh** đúng cách, **tiền xử lý hình ảnh cho OCR** bằng cách cắt, và cuối cùng **cách thực hiện OCR** để **nhận dạng văn bản từ hình ảnh** và **trích xuất văn bản từ hình ảnh** bằng các thư viện Python của Aspose. Script hoàn chỉnh minh họa một quy trình thực tế, sẵn sàng cho sản xuất mà bạn có thể tích hợp vào bất kỳ pipeline tự động nào.

Nếu bạn đã sẵn sàng tiến xa hơn, hãy thử nghiệm với:

- **Cải thiện hình ảnh** (độ tương phản, nhị phân hoá) trước OCR
- **Trích xuất nhiều ROI** cho các mẫu có nhiều trường
- **Xử lý hàng loạt** toàn bộ thư mục tài liệu đã quét
- **Tích hợp** với các hệ thống hạ nguồn (ví dụ, đưa dữ liệu đã trích xuất vào cơ sở dữ liệu)

Hãy tự do điều chỉnh mã cho trường hợp sử dụng của bạn, và chúc lập trình vui vẻ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
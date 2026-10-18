---
category: general
date: 2026-03-26
description: Nhận dạng văn bản từ hình ảnh nhanh chóng bằng cách học cách tải hình
  ảnh cho OCR và trích xuất dữ liệu từ một khu vực cụ thể. Hãy theo dõi hướng dẫn
  thực hành này.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: vi
og_description: Nhận dạng văn bản từ hình ảnh trong Python bằng cách tải hình ảnh
  để OCR, xác định vùng quan tâm và trích xuất văn bản sạch. Tìm hiểu quy trình đầy
  đủ.
og_title: Nhận dạng văn bản từ hình ảnh – Hướng dẫn toàn diện OCR bằng Python
tags:
- OCR
- Python
- Image Processing
title: Nhận dạng văn bản từ hình ảnh – Hướng dẫn OCR Python từng bước
url: /vi/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhận dạng văn bản từ hình ảnh – Hướng dẫn Python OCR toàn diện

Bạn đã bao giờ cần **recognize text from image** nhưng không chắc bắt đầu từ đâu chưa? Có thể bạn có một mẫu quét, một biên lai, hoặc một ảnh chụp màn hình và chỉ muốn lấy các từ bên trong một hộp cụ thể. Tin tốt là chỉ với vài dòng Python, bạn có thể **load image for OCR**, tập trung vào một vùng duy nhất và trích xuất chính xác văn bản bạn cần—không cần sao chép thủ công.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: **load image for OCR**, xác định một vùng quan tâm (ROI), chạy engine OCR, và in kết quả. Khi kết thúc, bạn sẽ có thể nhúng đoạn mã này vào bất kỳ dự án nào cần trích xuất văn bản từ một phần cụ thể của hình ảnh. Không có các pipeline xử lý ảnh nặng, chỉ có mã sạch, dễ đọc và hoạt động ngay hôm nay.

## Yêu cầu trước

- Python 3.8+ đã được cài đặt  
- Gói `ocr` (hoặc bất kỳ thư viện OCR tương thích nào) – cài đặt bằng `pip install ocr-lib` (thay thế bằng tên gói thực tế bạn sử dụng)  
- Một ảnh PNG/JPEG chứa mẫu bạn muốn đọc  
- Kiến thức cơ bản về hàm và lớp trong Python  

Nếu bạn đã quen thuộc với những yêu cầu này, tuyệt vời—bạn có thể bỏ qua. Nếu chưa, hãy uống một tách cà phê nhanh và đảm bảo các mục trên đã sẵn sàng; các bước tiếp theo giả định chúng đã có.

## Bước 1: Tạo một Instance của Engine OCR – Lõi “recognize text from image”

Điều đầu tiên chúng ta cần là một đối tượng biết cách giao tiếp với engine OCR. Hãy nghĩ nó như bộ não sẽ sau này **recognize text from image** dữ liệu.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Tại sao điều này quan trọng:** Khởi tạo engine một lần cho phép bạn tái sử dụng các cài đặt (như gói ngôn ngữ) cho nhiều hình ảnh, giúp cải thiện hiệu suất và giữ cho mã gọn gàng.

## Bước 2: **Load Image for OCR** – Đưa hình ảnh vào bộ nhớ

Bây giờ chúng ta thực sự **load image for OCR**. Thư viện cung cấp một phương thức tĩnh tiện lợi để đọc tệp và trả về một đối tượng mà engine có thể hiểu.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Mẹo chuyên nghiệp:** Nếu hình ảnh của bạn lớn, hãy cân nhắc thay đổi kích thước trước khi tải. Hình ảnh nhỏ hơn giúp OCR nhanh hơn mà không làm giảm độ chính xác đối với hầu hết văn bản in.

## Bước 3: Xác định **OCR Region of Interest (ROI)**

Thường bạn không cần toàn bộ trang—chỉ một hộp cụ thể nơi người dùng nhập dữ liệu. Định nghĩa một **OCR region of interest** cho engine biết bỏ qua phần còn lại, giảm nhiễu và tăng tốc xử lý.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **Tại sao tập trung vào ROI?**  
> - **Tốc độ:** Engine quét ít pixel hơn.  
> - **Độ chính xác:** Đồ họa nền ngoài ROI có thể gây nhầm lẫn cho việc nhận dạng ký tự.  
> - **Đơn giản:** Bạn nhận được một chuỗi sạch khớp chính xác với trường bạn quan tâm.

## Bước 4: Chạy quy trình OCR – Giây phút quyết định

Với mọi thứ đã sẵn sàng, cuối cùng chúng ta **recognize text from image** trong ROI đã định nghĩa.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

Nếu engine hỗ trợ nhiều vùng, `ocr_result` sẽ chứa một danh sách; trong trường hợp ROI đơn của chúng ta, nó là một đối tượng đơn giản với phương thức `get_text()`.

## Bước 5: Trích xuất và In Văn bản – Nhận Kết quả Cuối cùng

Bây giờ chúng ta lấy chuỗi thuần từ đối tượng kết quả và hiển thị nó. Đây là nơi bạn có thể đưa đầu ra vào cơ sở dữ liệu, tệp CSV, hoặc bất kỳ logic nào tiếp theo.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Kết quả mong đợi** (ví dụ cho trường tên đã điền):

```
Text inside ROI:
 John Doe
```

Nếu engine OCR trả về khoảng trắng thừa hoặc ngắt dòng, bạn có thể làm sạch bằng `.strip()` hoặc một biểu thức chính quy.

## Xử lý các trường hợp góc phổ biến

| Situation                              | What to Do                                                               |
|----------------------------------------|--------------------------------------------------------------------------|
| **Low‑resolution image**               | Phóng to bằng `Pillow` (`Image.resize`) trước khi tải.                  |
| **Skewed or rotated text**             | Áp dụng chỉnh sửa xoay (`ocr.Imaging.Image.rotate`).               |
| **Multiple languages**                | Đặt gói ngôn ngữ cho engine: `ocr_engine.set_language('eng+spa')`. |
| **No ROI defined**                     | Bỏ qua `add_region_of_interest`; engine sẽ xử lý toàn bộ hình ảnh. |
| **Unexpected characters (e.g., commas)** | Xử lý hậu kỳ chuỗi: `extracted_text.replace(',', '')`.            |

Những mẹo này giúp pipeline **load image for OCR** của bạn vững chắc ngay cả khi tài liệu nguồn không hoàn hảo.

## Ví dụ Hoạt động đầy đủ – Sao chép, Dán, Chạy

Dưới đây là script hoàn chỉnh bạn có thể đặt vào tệp `.py` và chạy. Nó bao gồm tất cả các import, xử lý lỗi, và một trợ giúp nhỏ để kiểm tra ảnh tồn tại.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

Chạy script này sẽ in ra chuỗi đã được làm sạch từ ROI, cung cấp cho bạn một dữ liệu sẵn sàng sử dụng.

## Kết luận

Bây giờ bạn đã có một phương pháp rõ ràng, từ đầu đến cuối để **recognize text from image** bằng cách đầu tiên **load image for OCR**, xác định một **OCR region of interest** chính xác, và cuối cùng trích xuất văn bản sạch. Cách tiếp cận này hoạt động với bất kỳ thư viện OCR Python nào tuân theo mẫu trên, và bạn có thể dễ dàng mở rộng để xử lý nhiều ROI, ngôn ngữ khác nhau, hoặc các bước tiền xử lý.

Tiếp theo, bạn có thể khám phá:

- **image preprocessing for OCR** (thresholding, denoising) để tăng độ chính xác trên các bản quét nhiễu.  
- Sử dụng kết quả **extract text from ROI** để điền vào pandas DataFrame cho phân tích dữ liệu hàng loạt.  
- Chuyển sang dịch vụ OCR dựa trên đám mây (Google Vision, Azure Computer Vision) khi bạn cần độ tin cậy cao hơn ở quy mô lớn.

Hãy thử nghiệm, điều chỉnh tọa độ hình chữ nhật để phù hợp với mẫu của bạn, và xem tự động hoá diễn ra. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
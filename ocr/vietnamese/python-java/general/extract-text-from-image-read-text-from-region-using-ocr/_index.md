---
category: general
date: 2026-07-05
description: Trích xuất văn bản từ hình ảnh bằng Python OCR. Tìm hiểu cách tải hình
  ảnh cho OCR, đọc văn bản từ vùng, và trích xuất văn bản từ hoá đơn chỉ với vài dòng
  mã.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Python OCR. Hướng dẫn này chỉ
  cách tải hình ảnh cho OCR, đọc văn bản từ vùng và nhanh chóng trích xuất văn bản
  từ hoá đơn.
og_title: Trích xuất văn bản từ hình ảnh – Đọc văn bản từ khu vực bằng OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Trích xuất văn bản từ hình ảnh – Đọc văn bản từ vùng bằng OCR
url: /vi/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh – Đọc Văn bản từ Vùng bằng OCR

Bạn đã bao giờ cần **extract text from image** nhưng chỉ một phần cụ thể mới quan trọng—như tổng số tiền trên hoá đơn? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, bạn sẽ gặp phải việc cần **read text from region** thay vì phân tích toàn bộ hình ảnh. May mắn là, chỉ với vài dòng Python, bạn có thể tải hình ảnh cho OCR, xác định một vùng quan tâm (ROI), và lấy ra chính xác các ký tự bạn cần.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy cách **load image for OCR**, thiết lập ROI, và cuối cùng **extract text from invoice**. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng để sử dụng với bất kỳ thư viện OCR phổ biến nào hỗ trợ nhận dạng dựa trên vùng.

---

## Những gì bạn cần

- Python 3.8+ (mã chạy trên 3.10 cũng được)  
- Một gói OCR cung cấp lớp `OcrEngine` (đối với bản demo chúng ta sẽ dùng mô-đun giả `ocr`; thay thế bằng `pytesseract`, `easyocr`, hoặc bất kỳ thư viện nào hỗ trợ ROI)  
- Một hình ảnh mẫu—ví dụ, `invoice.png`—chứa văn bản in rõ ràng  
- Kiến thức cơ bản về hàm và lớp trong Python (không yêu cầu nền tảng học sâu)

Nếu bạn đã có những thứ này, tuyệt vời—hãy bắt đầu. Nếu chưa, tải Python mới nhất từ python.org và cài đặt gói OCR bằng `pip install your-ocr-lib`.

![Ví dụ trích xuất văn bản từ hình ảnh](extract-text-from-image.png "Trích xuất văn bản từ hình ảnh – demo OCR dựa trên vùng")

*Hình ảnh trên minh họa vùng (hình chữ nhật màu đỏ) mà chúng ta sẽ nhắm tới để **extract text from image**.*

## Bước 1: Cài đặt và Nhập Thư viện OCR

Đầu tiên, hãy chắc chắn rằng thư viện OCR có sẵn trong môi trường của bạn. Mẫu import dưới đây hoạt động với hầu hết các gói cung cấp lớp `OcrEngine` cấp cao.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro tip:** Nếu bạn đang sử dụng `pytesseract`, bạn sẽ cần cài đặt binary Tesseract riêng và đặt `pytesseract.pytesseract.tesseract_cmd` tới đường dẫn của nó.

## Bước 2: Tạo Engine OCR và Đặt Ngôn ngữ

Tạo engine rất đơn giản, nhưng việc chỉ định ngôn ngữ sẽ cải thiện độ chính xác đáng kể, đặc biệt đối với hoá đơn chứa số và từ tiếng Anh.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Tại sao chúng ta làm như vậy? Engine OCR sử dụng mô hình ngôn ngữ để dự đoán ký tự; việc cho nó biết sẽ nhận tiếng Anh giúp giảm các kết quả sai như nhầm “0” thành “O”.

## Bước 3: Tải Hình ảnh cho OCR

Bây giờ chúng ta thực sự **load image for OCR**. Hầu hết các thư viện chấp nhận đường dẫn tệp hoặc đối tượng ảnh Pillow. Ở đây chúng ta sử dụng bộ tải tích hợp của thư viện để đơn giản.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Đảm bảo đường dẫn trỏ tới thư mục đúng; lỗi thường gặp là quên đường dẫn tương đối khi script chạy từ thư mục làm việc khác.

## Bước 4: Xác định Vùng Quan tâm (ROI)

Xác định ROI là trọng tâm của **read text from region**. Hãy tưởng tượng như vẽ một hình chữ nhật quanh phần hoá đơn chứa tổng số tiền.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` và `top` đại diện cho tọa độ X và Y của góc trên‑trái của hình chữ nhật.  
- `width` và `height` xác định kích thước của khung.  
- Bạn có thể thử nghiệm các giá trị khác nhau bằng một trình xem ảnh hiển thị tọa độ pixel.

> **Tại sao ROI quan trọng:** Chạy OCR trên toàn trang lãng phí tài nguyên CPU và thường gây nhiễu từ văn bản, bảng hoặc đồ họa không liên quan. Bằng cách tập trung vào một vùng, bạn sẽ có kết quả sạch hơn và xử lý nhanh hơn.

## Bước 5: Thực hiện OCR trên Vùng Đã Chỉ Định

Với mọi thứ đã được thiết lập, cuối cùng chúng ta **extract text from image**—nhưng chỉ trong ROI mà chúng ta đã định nghĩa.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

Phương thức `recognize` trả về một đối tượng thường chứa chuỗi thô, điểm tin cậy, và đôi khi hộp bao cho mỗi từ. Đối với mục đích của chúng ta, chỉ cần văn bản thuần.

## Bước 6: Xuất Văn bản Đã Trích xuất

Hãy in kết quả và xem chúng ta nhận được gì. Bước này minh họa **extract text from invoice** trong một kịch bản thực tế.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Kết quả Dự kiến

```
Text inside ROI:
Total Amount: $1,245.67
```

Nếu hoá đơn của bạn có bố cục khác, bạn sẽ thấy bất kỳ văn bản nào nằm trong hình chữ nhật—có thể là số hoá đơn, ngày, hoặc tham chiếu PO.

## Bước 7: Đóng Gói Thành Hàm Có Thể Tái Sử Dụng (Tùy chọn)

Để giải pháp có thể tái sử dụng cho nhiều hoá đơn, hãy đóng gói logic vào một hàm. Điều này cũng minh họa **ocr on region** như một tiện ích chung.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Bây giờ bạn có thể gọi hàm với bất kỳ hoá đơn nào:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

## Những Cạm Bẫy Thường Gặp & Cách Tránh

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Kết quả trống** | ROI không thực sự bao phủ bất kỳ văn bản nào (tọa độ sai). | Kiểm tra lại giá trị pixel bằng trình chỉnh sửa ảnh; thêm lớp debug trực quan. |
| **Ký tự rác** | Độ phân giải ảnh thấp hoặc độ tương phản kém. | Tiền xử lý ảnh: chuyển sang thang độ xám, áp dụng ngưỡng (`cv2.threshold`). |
| **Ngôn ngữ sai** | Engine mặc định một ngôn ngữ không có bộ ký tự cần thiết. | Đặt rõ `ocr_engine.language` thành `ENGLISH` hoặc locale phù hợp. |
| **Độ trễ hiệu năng** | Chạy OCR trên các ảnh lớn liên tục. | Thu nhỏ ảnh trước khi tải, hoặc chỉ xử lý ROI bằng cách cắt trước. |

## Mở Rộng Ví dụ: Nhiều ROI

Đôi khi một hoá đơn chứa nhiều trường bạn cần—như **extract text from invoice** cho cả tổng số tiền và ngày hoá đơn. Bạn có thể lặp qua danh sách các hình chữ nhật:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Mẫu này giữ cho mã của bạn sạch sẽ và dễ dàng thêm nhiều vùng sau này.

## Kết luận

Chúng ta vừa hoàn thành một quy trình toàn diện, đầu‑tới‑cuối để **extract text from image** bằng OCR Python, tập trung vào một vùng cụ thể. Bằng cách **loading image for OCR**, xác định **region of interest**, và gọi engine, bạn có thể đáng tin cậy **read text from region**—lý tưởng để lấy tổng tiền từ hoá đơn, ngày từ biên lai, hoặc bất kỳ dữ liệu cục bộ nào khác.  

Hãy thoải mái thử nghiệm

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao quát các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, hoạt động với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn Từng Bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Trích xuất Văn bản từ Hình ảnh – Tối ưu hóa OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)
- [Cách Trích xuất Văn bản từ Hình ảnh bằng cách Chuẩn bị Các Hình chữ nhật trong OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
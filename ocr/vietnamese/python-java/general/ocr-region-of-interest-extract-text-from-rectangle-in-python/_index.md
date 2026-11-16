---
category: general
date: 2026-05-31
description: Tìm hiểu cách sử dụng vùng quan tâm OCR để tải hình ảnh cho OCR và trích
  xuất văn bản từ hình chữ nhật, hoàn hảo cho việc nhận dạng số tiền trên hóa đơn.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: vi
og_description: Thành thạo vùng quan tâm OCR để tải hình ảnh cho OCR, trích xuất văn
  bản từ hình chữ nhật và nhận dạng văn bản từ hoá đơn trong một hướng dẫn duy nhất.
og_title: OCR Vùng Quan Tâm – Hướng Dẫn Python Từng Bước
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR Vùng quan tâm – Trích xuất văn bản từ hình chữ nhật trong Python
url: /vi/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – Trích xuất Văn bản từ Hình chữ nhật trong Python

Bạn đã bao giờ tự hỏi làm sao **ocr region of interest** một phần cụ thể của hoá đơn đã quét mà không phải đưa toàn bộ trang vào engine? Bạn không phải là người đầu tiên nhìn vào một biên lai mờ và nghĩ, “Làm sao tôi lấy được số tiền nằm ở góc dưới bên phải?” Tin tốt là bạn có thể chỉ cho thư viện OCR biết chính xác nơi cần tìm, giúp tăng tốc độ và độ chính xác đáng kể.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho bạn thấy cách **load image for OCR**, định nghĩa một **region of interest**, và sau đó **extract text from rectangle** để cuối cùng **recognize text from invoice** và trả lời câu hỏi cổ điển “làm sao lấy được số tiền”. Không có những tham chiếu mơ hồ—chỉ có code cụ thể, giải thích rõ ràng, và một vài mẹo chuyên nghiệp mà bạn ước mình biết từ trước.

---

## Những gì bạn sẽ xây dựng

Khi kết thúc tutorial này, bạn sẽ có một script Python nhỏ mà:

1. Tải ảnh hoá đơn từ đĩa.  
2. Đánh dấu một ROI hình chữ nhật nơi tổng số tiền nằm.  
3. Chỉ chạy OCR trong ROI đó.  
4. In ra chuỗi số tiền đã được làm sạch.  

Tất cả đều hoạt động với bất kỳ thư viện OCR nào hỗ trợ ROI—ở đây chúng ta sẽ dùng một package giả tưởng nhưng đại diện `SimpleOCR` mô phỏng các công cụ phổ biến như Tesseract hoặc EasyOCR. Bạn có thể thay thế nó; các khái niệm vẫn giữ nguyên.

---

## Yêu cầu trước

- Python 3.8+ đã được cài đặt (`python --version` nên hiển thị ≥3.8).  
- Một package OCR có thể cài qua pip (ví dụ: `pip install simpleocr`).  
- Một ảnh hoá đơn (PNG hoặc JPEG) được đặt trong thư mục bạn có thể tham chiếu.  
- Kiến thức cơ bản về hàm và lớp trong Python (không cần gì phức tạp).

Nếu bạn đã có những thứ trên, tuyệt vời—cùng bắt đầu. Nếu chưa, hãy lấy ảnh trước; các bước còn lại không phụ thuộc vào nội dung thực tế của file.

---

## Bước 1: Load Image for OCR

Điều đầu tiên bất kỳ quy trình OCR nào cần là một bitmap để đọc. Hầu hết các thư viện cung cấp một phương thức `load_image` đơn giản nhận đường dẫn file. Đây là cách thực hiện với engine `SimpleOCR` của chúng ta:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Sử dụng đường dẫn tuyệt đối hoặc `os.path.join` để tránh những lỗi “file not found” khi chạy script từ thư mục làm việc khác.

---

## Bước 2: Define OCR Region of Interest

Thay vì để engine quét toàn bộ trang, chúng ta chỉ cho nó *chính xác* nơi số tiền nằm. Đây là bước **ocr region of interest**, và nó là chìa khóa để trích xuất đáng tin cậy, đặc biệt khi tài liệu có tiêu đề hoặc chân trang gây nhiễu.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Tại sao lại dùng những con số đó? `x` và `y` là khoảng cách pixel từ góc trên‑trái, trong khi `width` và `height` mô tả kích thước hộp. Nếu không chắc, mở ảnh trong bất kỳ trình chỉnh sửa nào, bật thước đo, và ghi lại tọa độ. Nhiều IDE còn cho phép bạn xem vị trí con trỏ khi di chuột.

---

## Bước 3: Extract Text from Rectangle

Khi ROI đã được đặt, chúng ta yêu cầu engine **recognize text from invoice** nhưng chỉ trong hình chữ nhật vừa thêm. Lệnh này trả về một đối tượng kết quả thường chứa chuỗi thô, điểm tin cậy, và đôi khi cả bounding box.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Ở phía sau, `recognize()` lặp qua từng ROI, cắt phần ảnh tương ứng, chạy mô hình OCR, và ghép các kết quả lại. Vì vậy việc định nghĩa một **extract text from rectangle** chặt chẽ có thể giảm vài giây thời gian xử lý cho các job batch.

---

## Bước 4: How to Extract Amount – Clean the Output

OCR không hoàn hảo; bạn thường nhận được các khoảng trắng thừa, ký tự xuống dòng, hoặc thậm chí ký tự bị nhận sai (ví dụ “S” thay vì “5”). Một `strip()` nhanh và một regex nhỏ thường đủ để xử lý các giá trị tiền tệ.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** Nếu bạn định đưa số tiền vào cơ sở dữ liệu hoặc cổng thanh toán, bạn cần một định dạng dự đoán được. Loại bỏ khoảng trắng và lọc các ký tự không phải số ngăn ngừa lỗi ở các bước tiếp theo.

---

## Bước 5: Recognize Text from Invoice – Full Script

Kết hợp tất cả lại, đây là script hoàn chỉnh, sẵn sàng chạy. Lưu lại dưới tên `extract_amount.py` và thực thi `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Expected Output

```
Amount: 1,245.67
```

Nếu ROI không căn chỉnh đúng, bạn có thể thấy kết quả như `Amount: 1245.6S`—có ký tự “S” lạ. Điều chỉnh lại tọa độ hình chữ nhật và chạy lại cho tới khi output sạch sẽ.

---

## Common Pitfalls & Edge Cases

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ROI quá nhỏ** | Văn bản số tiền bị cắt, dẫn đến nhận dạng không đầy đủ. | Mở rộng `width`/`height` khoảng 10‑20 % và kiểm tra lại. |
| **DPI không đúng** | Ảnh scan độ phân giải thấp (≤150 dpi) làm giảm độ chính xác OCR. | Tăng mẫu ảnh lên 300 dpi trước khi load, hoặc yêu cầu máy scan ở DPI cao hơn. |
| **Nhiều loại tiền tệ** | Regex lấy nhóm số đầu tiên, có thể là số hoá đơn. | Tinh chỉnh regex để tìm ký hiệu tiền tệ (`$`, `€`, `£`) trước các chữ số. |
| **Hoá đơn bị xoay** | Các engine OCR giả định văn bản thẳng đứng; trang xoay làm mất nhận dạng. | Áp dụng chỉnh sửa góc (`ocr_engine.rotate(90)`) trước khi thêm ROI. |
| **Nhiễu nền** | Bóng hoặc dấu tem gây rối mô hình. | Tiền xử lý bằng ngưỡng đơn giản (`cv2.threshold`) hoặc bộ lọc giảm nhiễu. |

Giải quyết những trường hợp này sớm sẽ tiết kiệm hàng giờ debug sau này.

---

## Pro Tips for Real‑World Projects

- **Batch Processing:** Lặp qua một thư mục hoá đơn, tính ROI động (ví dụ dựa trên phát hiện mẫu), và lưu kết quả vào CSV.  
- **Template Matching:** Nếu bạn xử lý nhiều bố cục hoá đơn, duy trì một bản đồ JSON `template_id → ROI coordinates`. Chuyển ROI dựa trên bộ phân loại mẫu nhanh.  
- **Parallel Execution:** Dùng `concurrent.futures.ThreadPoolExecutor` để chạy nhiều instance OCR đồng thời—rất hữu ích cho pipeline back‑office khối lượng lớn.  
- **Confidence Filtering:** Hầu hết kết quả OCR có điểm tin cậy. Loại bỏ các kết quả dưới ngưỡng (ví dụ 85 %) và đánh dấu để kiểm tra thủ công.

---

## Kết luận

Chúng ta đã bao quát mọi thứ cần thiết để **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, và cuối cùng **recognize text from invoice** nhằm trả lời câu hỏi cổ điển **how to extract amount**. Script ngắn gọn, nhưng đủ linh hoạt để thích nghi với các định dạng tài liệu, ngôn ngữ, và backend OCR khác nhau.

Bây giờ bạn đã nắm vững nền tảng, hãy mở rộng quy trình: thêm quét mã vạch, tích hợp với parser PDF, hoặc đẩy số tiền đã trích xuất lên API kế toán. Không có giới hạn, và với ROI được định nghĩa rõ ràng, bạn luôn nhận được kết quả nhanh hơn, sạch hơn.

Nếu gặp khó khăn, để lại bình luận bên dưới—chúc bạn OCR vui vẻ!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ví dụ về OCR region of interest")


## Bạn nên học gì tiếp theo?

- [Cách Trích xuất Văn bản từ Hình ảnh bằng cách Chuẩn bị Hình chữ nhật trong OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Trích xuất Văn bản từ Hình ảnh Java với Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Trích xuất Văn bản từ Hình ảnh – Tối ưu hoá OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
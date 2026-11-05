---
category: general
date: 2026-03-26
description: Tạo đa giác ROI để chạy OCR trên khu vực đã chọn. Tìm hiểu cách định
  nghĩa nhiều vùng, đăng ký chúng và trích xuất văn bản bằng công cụ OCR Python.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: vi
og_description: Tạo đa giác ROI và chạy OCR trên khu vực đã chọn bằng công cụ Python.
  Bao gồm đầy đủ mã nguồn, giải thích và mẹo.
og_title: Tạo đa giác ROI – OCR nhanh trên khu vực đã chọn
tags:
- OCR
- Python
- Image Processing
title: Tạo đa giác ROI – Hướng dẫn từng bước cho OCR trên khu vực đã chọn
url: /vi/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo ROI Polygon – Hướng Dẫn Toàn Diện cho OCR trên Vùng Chọn

Bạn đã bao giờ cần **create ROI polygon** để có thể chạy OCR chỉ trên phần ảnh quan trọng chưa? Có thể bạn đang quét biên lai và chỉ cần tổng tiền, hoặc bạn có một mẫu đơn mà chỉ trường chữ ký cần được đọc. Trong những trường hợp đó, **ocr on selected area** giúp tiết kiệm thời gian và tăng độ chính xác.  

Trong hướng dẫn này, chúng tôi sẽ đi qua mọi thứ bạn cần: từ việc định nghĩa hai polygon, đăng ký chúng với engine OCR, đến việc lấy văn bản đã nhận dạng ra trong một lời gọi duy nhất. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy và hiểu rõ lý do tại sao việc tập trung vào các vùng quan tâm lại quan trọng.

## Bạn Sẽ Học Được

- Cách **create ROI polygon** bằng cách sử dụng một thư viện OCR tiêu chuẩn.  
- Sự khác biệt giữa việc định nghĩa một vùng duy nhất và nhiều vùng.  
- Cách đăng ký các vùng này với engine để thực hiện `ocr on selected area`.  
- Kết quả mong đợi và cách khắc phục các vấn đề thường gặp (ví dụ: ROI chồng lấn, kết quả rỗng).

### Yêu Cầu Trước

- Python 3.8+ đã được cài đặt.  
- Một thư viện OCR cung cấp các phương thức `Polygon`, `Point`, và `add_region_of_interest` (ví dụ trong tài liệu này dùng module giả `ocr`; hãy thay thế bằng SDK thực tế của bạn, như wrapper Tesseract‑Python hoặc EasyOCR).  
- Một file ảnh mẫu (`sample.png`) chứa văn bản trong các tọa độ được hiển thị bên dưới.

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng một thư viện thực, hãy chắc chắn rằng ảnh được tải trong cùng không gian tọa độ (gốc ở góc trên‑trái, X tăng sang phải, Y tăng xuống).  

---  

## Bước 1: Nhập Module OCR và Tải Ảnh Của Bạn  

Đầu tiên, đưa gói OCR vào phạm vi và đọc ảnh bạn muốn xử lý.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Lý do quan trọng:* Engine cần dữ liệu ảnh trước khi bạn có thể gắn bất kỳ **ROI polygon** nào. Một số thư viện cũng cho phép bạn truyền ảnh sau, nhưng khởi tạo sớm giúp quy trình gọn gàng hơn.

## Bước 2: Định Nghĩa ROI Polygon Đầu Tiên  

Bây giờ chúng ta tạo vùng quan tâm đầu tiên. Hãy tưởng tượng như đang vẽ một hình chữ nhật quanh tiêu đề bảng.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Giải thích:*  
- `ocr.Point(x, y)` sử dụng tọa độ pixel.  
- Danh sách các điểm được sắp xếp theo chiều kim đồng hồ, như hầu hết các engine mong đợi.  
- Bạn có thể thêm bao nhiêu điểm tùy thích để tạo hình dạng bất thường; một hình chữ nhật chỉ là một trường hợp đặc biệt.

## Bước 3: Định Nghĩa Thêm ROI Polygons (Tùy Chọn)  

Bạn không cần dừng lại ở một polygon. Dưới đây là một polygon thứ hai để bắt trường chữ ký ở phía dưới trang.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Tại sao thêm nhiều?* Thực hiện **ocr on selected area** cho nhiều vùng cho phép bạn trích xuất các mẩu dữ liệu rời rạc trong một lần chạy, nhanh hơn rất nhiều so với việc cắt và xử lý từng phần riêng lẻ.

## Bước 4: Đăng Ký Các ROI Với Engine OCR  

Khi các polygon đã sẵn sàng, hãy thông báo cho engine biết những khu vực nào cần kiểm tra.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Lưu ý quan trọng:* Một số SDK yêu cầu bạn gọi phương thức `clear_regions()` trước khi thêm mới nếu bạn tái sử dụng engine cho ảnh khác.

## Bước 5: Chạy OCR và Lấy Văn Bản  

Cuối cùng, thực hiện nhận dạng. Engine sẽ chỉ tìm kiếm bên trong các polygon chúng ta vừa thêm.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Kết quả mong đợi** (giả sử `sample.png` chứa các từ “Invoice Total: $123.45” trong ROI đầu tiên và “Signature: John Doe” trong ROI thứ hai):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Nếu kết quả rỗng, hãy kiểm tra lại các tọa độ có thực sự cắt qua văn bản và độ phân giải ảnh có khớp với hệ thống tọa độ hay không.

## Trường Hợp Đặc Biệt & Những Cạm Bẫy Thường Gặp  

| Tình Huống                               | Điều Cần Lưu Ý                                 | Cách Khắc Phục / Giải Pháp                     |
|----------------------------------------|------------------------------------------------|-----------------------------------------------|
| **ROI chồng lấn**                       | Văn bản có thể được trả về hai lần.            | Giữ các polygon không giao nhau hoặc loại bỏ trùng lặp trong kết quả. |
| **ROI nằm ngoài giới hạn ảnh**          | Engine có thể ném lỗi hoặc trả về rỗng.       | Giới hạn tọa độ trong khoảng `0 ≤ x < width`, `0 ≤ y < height`. |
| **ROI quá nhỏ**                         | Độ chính xác OCR giảm do thiếu pixel.          | Mở rộng polygon vài pixel hoặc tăng độ phân giải ảnh trước. |
| **Hình dạng không phải hình chữ nhật**  | Một số engine chỉ hỗ trợ polygon lồi.          | Chia các hình dạng phức tạp thành nhiều ROI lồi. |
| **Thay đổi kích thước ảnh**             | Các tọa độ cứng sẽ không còn hợp lệ.           | Tính toán tọa độ ROI dựa trên kích thước ảnh (ví dụ: phần trăm). |

## Ví Dụ Hoàn Chỉnh  

Dưới đây là script đầy đủ mà bạn có thể sao chép‑dán và chạy (thay `ocr` bằng thư viện thực tế của bạn).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Chạy bằng `python ocr_roi_example.py` và bạn sẽ thấy các chuỗi đã trích xuất từ hai vùng đã định nghĩa.

## Các Bước Tiếp Theo  

- **Tạo ROI động:** Thay vì mã hoá tọa độ, sử dụng xử lý ảnh (ví dụ: phát hiện contour bằng OpenCV) để tự động xác định bảng hoặc trường.  
- **Xử lý hậu kỳ:** Loại bỏ khoảng trắng, áp dụng regex, hoặc chuyển đổi số sang kiểu dữ liệu phù hợp.  
- **Xử lý hàng loạt:** Lặp qua một thư mục ảnh, tái sử dụng cùng một định nghĩa ROI nếu bố cục đồng nhất.  

Nếu bạn quan tâm đến **ocr on selected area** cho các tài liệu phức tạp hơn—như PDF đa trang hoặc mẫu đơn quét—hãy tìm hiểu các thư viện hỗ trợ đăng ký ROI theo trang.  

---  

### Tổng Quan Hình Ảnh  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="ví dụ tạo roi polygon hiển thị hai vùng được chọn"}

Sơ đồ minh họa cách hai hình chữ nhật (màu xanh và màu xanh lá) được bố trí trên ảnh nền, chỉ ra chính xác những gì engine OCR sẽ đọc.

---  

## Kết Luận  

Chúng ta vừa **created ROI polygon** objects, đăng ký chúng với một engine OCR, và thực hiện `ocr on selected area` trong một script sạch sẽ, có thể tái tạo. Bằng cách giới hạn engine vào những khu vực bạn quan tâm, bạn giảm thời gian xử lý, cải thiện độ chính xác, và làm cho việc xử lý dữ liệu sau này trở nên đơn giản hơn rất nhiều.  

Hãy thử với ảnh của bạn—điều chỉnh tọa độ, thêm nhiều polygon, hoặc kết nối đầu ra với cơ sở dữ liệu. Khi bạn thành thạo OCR dựa trên vùng, khả năng của bạn sẽ không có giới hạn.  

Có câu hỏi hoặc muốn chia sẻ một trường hợp sử dụng thú vị? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
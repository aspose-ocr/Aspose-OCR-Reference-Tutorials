---
category: general
date: 2026-03-28
description: Cách OCR ROI trong Python – Tìm hiểu cách thiết lập các tùy chọn tiền
  xử lý để trích xuất văn bản chính xác từ các vùng ảnh cụ thể.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: vi
og_description: Cách OCR ROI trong Python – Hướng dẫn này chỉ cách thiết lập tiền
  xử lý để trích xuất văn bản đáng tin cậy từ các vùng ảnh đã định nghĩa.
og_title: Cách OCR ROI trong Python – Cách thiết lập tiền xử lý
tags:
- OCR
- Python
- Aspose
title: Cách OCR ROI trong Python – Cách thiết lập tiền xử lý
url: /vi/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách OCR ROI trong Python – Cách thiết lập tiền xử lý

Bạn đã bao giờ tự hỏi **cách OCR ROI** trong một hình ảnh hoá đơn nhiễu mà không cần tải toàn bộ trang vào bộ nhớ chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, chúng ta chỉ cần một vài trường—tên khách hàng, địa chỉ, tổng tiền—nên việc quét toàn bộ tài liệu là quá mức.

Tin tốt là gì? Với Aspose OCR, bạn có thể chỉ cho engine **đúng nơi cần tìm** và thậm chí yêu cầu nó làm sạch hình ảnh trước. Trong hướng dẫn này, chúng ta sẽ đi qua **cách thiết lập tiền xử lý**, định nghĩa các Vùng Quan Tâm (ROIs), và trích xuất văn bản sạch chỉ trong vài dòng Python.

Kết thúc hướng dẫn, bạn sẽ có một script sẵn sàng chạy để trích xuất các khối cụ thể từ bất kỳ hoá đơn, biên lai, hoặc mẫu đơn nào. Không cần công cụ bổ sung, chỉ cần Aspose OCR và một chút logic Python.

---

## Những gì bạn cần

- **Python 3.8+** (code hoạt động trên bất kỳ phiên bản gần đây nào)  
- **Aspose OCR for Python via .NET** – cài đặt bằng `pip install aspose-ocr`  
- Một hình ảnh mẫu (ví dụ: `invoice.png`) đặt trong thư mục bạn có thể tham chiếu  
- Kiến thức cơ bản về hàm Python và cú pháp hướng đối tượng  

Nếu bạn đã có những thứ này, tuyệt vời—hãy chuyển ngay sang phần code.

---

![Sơ đồ cách OCR ROI](ocr-roi.png "Ví dụ cách OCR ROI")

*Văn bản thay thế: sơ đồ cách OCR ROI hiển thị các hộp ROI trên hình ảnh hoá đơn*

---

## Bước 1 – Khởi tạo Engine OCR (Cách OCR ROI)

Trước khi chúng ta có thể chỉ cho engine *đâu* cần tìm, chúng ta cần một thể hiện của bộ xử lý OCR. Đối tượng này chứa tất cả cấu hình và thực hiện quá trình nhận dạng.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Lý do quan trọng*: Lớp `OcrEngine` trừu tượng hoá các công việc nặng (phát hiện phông chữ, phân tích bố cục, v.v.). Bằng cách tạo một engine duy nhất, bạn tránh việc khởi tạo lại các tài nguyên nặng cho mỗi hình ảnh, giúp hiệu năng luôn nhanh.

---

## Bước 2 – Tải hình ảnh nguồn của bạn (Cách OCR ROI)

Aspose Storage giúp việc tải hình ảnh trở nên đơn giản. Chỉ cần chỉ tới đường dẫn tệp, và bạn sẽ nhận được một đối tượng `Image` sẵn sàng để xử lý.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Mẹo*: Nếu bạn làm việc với stream (ví dụ, hình ảnh được tải lên qua API web), bạn có thể truyền một đối tượng `BytesIO` cho `Image.load` thay vì đường dẫn tệp.

---

## Bước 3 – Định nghĩa Các Vùng Quan Tâm (ROIs)

Bây giờ chúng ta trả lời câu hỏi cốt lõi **cách OCR ROI**: chúng ta chỉ cho engine các hình chữ nhật chính xác chứa dữ liệu mà chúng ta quan tâm. Mỗi ROI được xác định bằng góc trên‑trái (`x`, `y`) và kích thước (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Tại sao nên dùng ROIs?*  
- **Tốc độ** – Engine bỏ qua các phần không liên quan của hình ảnh.  
- **Độ chính xác** – Khi tập trung vào một khu vực nhỏ, nhiễu ở những nơi khác sẽ không làm rối bộ nhận dạng.  
- **Linh hoạt** – Bạn có thể thêm bao nhiêu ROI tùy thích; engine sẽ trả về danh sách kết quả theo cùng thứ tự.

---

## Bước 4 – Cách thiết lập tiền xử lý để cải thiện độ chính xác OCR

Hình ảnh lấy trực tiếp từ máy quét hoặc điện thoại thường gặp vấn đề nghiêng, độ tương phản thấp, hoặc ánh sáng không đồng đều. Aspose OCR cung cấp một đối tượng `PreprocessingOptions` cho phép bạn bật các sửa chữa phổ biến trước khi nhận dạng.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Cách nó giúp*:  
- **Deskew** loại bỏ độ nghiêng khiến các ký tự trở nên mơ hồ.  
- **Binarize** giảm nhiễu màu, cung cấp cho engine OCR một hình ảnh nhị phân sạch.  
- **Contrast** tăng cường các nét mờ, đặc biệt hữu ích cho biên lai đã phai màu.

Bạn có thể thử nghiệm các cờ này—tắt một cờ và xem kết quả có thay đổi không. Đó là cách **cách thiết lập tiền xử lý** một cách hiệu quả.

---

## Bước 5 – Thực hiện OCR chỉ trong các ROI đã định nghĩa

Với engine, hình ảnh, ROIs và tiền xử lý đã sẵn sàng, đã đến lúc gọi `recognize`. Phương thức này trả về một đối tượng `OcrResult` chứa một collection `regions`—mỗi mục tương ứng với thứ tự ROI mà chúng ta đã cung cấp.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Bên trong*: Engine cắt mỗi ROI, áp dụng pipeline tiền xử lý, và chạy mô hình nhận dạng trên đoạn đã làm sạch. Vì chúng ta truyền một danh sách, kết quả giữ nguyên thứ tự, giúp việc hậu xử lý trở nên đơn giản.

---

## Bước 6 – Đọc và sử dụng Văn bản Đã Trích xuất (Cách OCR ROI)

Cuối cùng, lặp qua danh sách `regions` và in ra—hoặc lưu—các chuỗi đã nhận dạng. Đối tượng `Region` cung cấp thuộc tính `text` chứa kết quả Unicode.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Kết quả mong đợi (ví dụ)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Nếu văn bản bị rối, hãy quay lại **cách thiết lập tiền xử lý**: có thể tăng `contrast` hoặc tắt `binarize` cho các logo màu.

---

## Những Cạm Bẫy Thường Gặp và Mẹo Chuyên Nghiệp

| Vấn đề | Nguyên nhân | Giải pháp (Cách thiết lập tiền xử lý) |
|--------|--------------|---------------------------------------|
| Văn bản nghiêng xuất hiện thành mớ hỗn độn | `deskew` bị tắt hoặc hình ảnh quá xoay | Bật `preprocessing_options.deskew = True` |
| Số bị biến thành chấm hoặc dấu lạ | Độ tương phản thấp hoặc binarization quá mạnh | Giảm `contrast` (ví dụ, `1.2`) hoặc đặt `binarize = False` |
| Tọa độ ROI lệch vài pixel | DPI khác nhau hoặc tỷ lệ máy quét | Dùng công cụ (ví dụ, Paint.NET) đo vị trí pixel chính xác, hoặc thêm một khoảng lề nhỏ (`+5` pixel) cho mỗi ROI |
| Kết quả rỗng cho một vùng | ROI nằm ngoài giới hạn hình ảnh | Kiểm tra kích thước ảnh: `source_image.width`, `source_image.height` |

---

## Mở Rộng Giải Pháp (Cách OCR ROI trong Các Tình Huống Khác)

- **ROIs động**: Nếu hoá đơn của bạn có bố cục thay đổi, bạn có thể chạy một OCR nhanh toàn trang để tìm các từ khóa (“Customer:”, “Address:”) rồi tính toán ROI ngay lập tức.  
- **Xử lý hàng loạt**: Đóng gói các bước trên vào một hàm và lặp qua một thư mục hình ảnh. Hãy nhớ tái sử dụng cùng một thể hiện `ocr_engine` để giảm tiêu thụ bộ nhớ.  
- **Xuất ra JSON**: Thay vì in, xây dựng một dictionary và dump bằng `json.dumps`; việc này giúp tích hợp downstream (ví dụ, đưa vào hệ thống ERP) trở nên đơn giản.

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Kết luận

Bạn đã có một ví dụ hoàn chỉnh, có thể chạy được, cho thấy **cách OCR ROI** trong Python đồng thời nắm vững **cách thiết lập tiền xử lý** để đạt độ chính xác tối ưu. Bằng cách giới hạn engine chỉ vào các hình chữ nhật bạn quan tâm và làm sạch hình ảnh trước, bạn sẽ nhận được kết quả nhanh hơn, sạch hơn—hoàn hảo cho tự động hoá hoá đơn, số hoá mẫu đơn, hoặc bất kỳ trường hợp nào chỉ cần một phần của trang.

Sẵn sàng cho bước tiếp theo? Hãy thử điều chỉnh tọa độ ROI cho loại tài liệu khác, hoặc thử các cờ tiền xử lý bổ sung như `sharpen` hoặc `noise_reduction`. Tính linh hoạt của Aspose OCR cho phép bạn tùy chỉnh pipeline cho hầu hết mọi chất lượng hình ảnh.

Nếu gặp khó khăn, kiểm tra đầu ra console để tìm các vùng rỗng và xem lại cài đặt tiền xử lý. Chúc lập trình vui vẻ, và chúc OCR của bạn luôn chính xác!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
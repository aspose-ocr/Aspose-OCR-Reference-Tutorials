---
category: general
date: 2026-04-26
description: Cách chạy OCR trên mẫu quét, học cách tiền xử lý hình ảnh để giảm nhiễu
  và trích xuất văn bản từ hình ảnh một cách nhanh chóng.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: vi
og_description: Cách chạy OCR trên tài liệu đã quét, tiền xử lý hình ảnh, giảm nhiễu
  và trích xuất văn bản một cách hiệu quả.
og_title: Cách chạy OCR và tiền xử lý hình ảnh – Hướng dẫn nhanh
tags:
- OCR
- image processing
- Python
title: Cách chạy OCR và tiền xử lý hình ảnh – Trích xuất văn bản từ biểu mẫu đã quét
url: /vi/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Chạy OCR – Hướng Dẫn Toàn Diện để Trích Xuất Văn Bản từ Hình Ảnh

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một mẫu quét lộn xộn và nhận được văn bản sạch, có thể tìm kiếm chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, hình ảnh thô đầy các đốm, ánh sáng không đồng đều và những khuyết điểm khác khiến OCR “ra khỏi hộp” gặp khó khăn.  

Tin tốt là gì? Chỉ với vài dòng Python và một pipeline tiền xử lý thông minh, bạn có thể tăng đáng kể độ chính xác nhận dạng, **giảm nhiễu**, và lấy ra đúng những từ bạn cần. Trong tutorial này, chúng ta sẽ đi qua từng bước — từ tải ảnh đến in chuỗi kết quả — để bạn có một đoạn mã sẵn sàng sử dụng cho hoá đơn, biên lai hoặc bất kỳ tài liệu quét nào.

## Những gì bạn sẽ xây dựng

- Một thể hiện `OcrEngine` giao tiếp với thư viện OCR bên dưới.  
- Một chuỗi tiền xử lý **binarize** (nhị phân hoá) ảnh và áp dụng **median blur** (làm mờ trung vị) để làm sạch các đốm.  
- Một lời gọi đơn giản tới `process()` trả về một đối tượng cung cấp `text`, chuỗi đã trích xuất.  

Khi hoàn thành, bạn sẽ có một script tự chứa mà bạn có thể chạy trên bất kỳ tệp ảnh nào và ngay lập tức xem văn bản đã trích xuất trong console.

## Yêu cầu trước

- Python 3.9+ (cú pháp ở đây phù hợp với phiên bản ổn định mới nhất).  
- Gói giả lập `aocr` – tưởng tượng nó là một lớp bao bọc mỏng quanh Tesseract hoặc bất kỳ engine OCR hiện đại nào. Cài đặt bằng `pip install aocr`.  
- Một ảnh quét (`scanned_form.jpg`) được đặt trong thư mục bạn có thể tham chiếu.  

Nếu bạn đang dùng một thư viện OCR thực tế như `pytesseract`, bạn có thể thay `OcrEngine` bằng lớp thích hợp — mọi thứ còn lại vẫn giữ nguyên.

![](how-to-run-ocr-example.png "ví dụ cách chạy OCR hiển thị một mẫu quét và văn bản đã trích xuất")

*Alt text: cách chạy OCR trên một tài liệu quét và xem văn bản đã trích xuất.*

---

## Bước 1: Cách Chạy OCR – Khởi Tạo Engine

Trước khi engine có thể đọc bất kỳ thứ gì, chúng ta cần tạo một thể hiện. Hãy nghĩ `OcrEngine` như bộ não sẽ sau này giải thích dữ liệu hình ảnh.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Tại sao điều này quan trọng:** Việc khởi tạo engine thiết lập các mô hình nội bộ, tải các gói ngôn ngữ và chuẩn bị môi trường chạy. Bỏ qua bước này thường dẫn đến lỗi `NoneType` khi bạn gọi `process()` sau này.

---

## Bước 2: Cách Tiền Xử Lý Ảnh – Tải Mẫu Quét Của Bạn

Bây giờ bộ não đã sẵn sàng, chúng ta cung cấp cho nó một bức ảnh. Ảnh có thể ở bất kỳ định dạng nào được `aocr.Image` hỗ trợ.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Mẹo chuyên nghiệp:** Sử dụng đường dẫn tuyệt đối trong quá trình phát triển để tránh những bất ngờ “file không tìm thấy” khi script chạy từ thư mục làm việc khác.

---

## Bước 3: Cách Giảm Nhiễu – Áp Dụng Binarization & Median Blur

Các bản quét thô thường chứa các đốm lẻ, nền không đồng đều hoặc bóng mờ nhẹ. Hai thủ thuật cổ điển — **binarization** và **median blur** — làm sạch ảnh mà không làm mất các cạnh quan trọng của ký tự.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Đi sâu hơn

- **Binarization**: Giá trị `threshold=180` nói với thuật toán: “Bất cứ gì sáng hơn 180 sẽ trở thành trắng; mọi thứ còn lại sẽ trở thành đen.” Điều chỉnh con số này nếu bản quét của bạn quá tối hoặc quá sáng.  
- **Median Blur**: Bán kính `2` có nghĩa bộ lọc xem một cửa sổ 5×5 pixel và thay thế pixel trung tâm bằng giá trị trung vị. Điều này làm mờ các đốm lẻ trong khi giữ nguyên nét chữ.

> **Trường hợp đặc biệt:** Nếu tài liệu của bạn có các vùng tô màu, một ngưỡng nhị phân đơn giản có thể xóa chúng. Trong trường hợp đó, hãy cân nhắc dùng `aocr.ImageFilters.adaptive_threshold()` — nó sẽ điều chỉnh ngưỡng một cách cục bộ trên toàn ảnh.

---

## Bước 4: Cách Trích Xuất Văn Bản – Chạy Quy Trình OCR

Với một ảnh đã được làm sạch, cuối cùng chúng ta để engine thực hiện phép màu của nó.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Bên trong engine đang làm gì?** Engine chạy một mạng nơ-ron (hoặc bộ khớp mẫu cũ) trên ma trận pixel, dịch mỗi glyph đã nhận dạng thành ký tự Unicode, và ghép chúng lại thành các dòng và đoạn văn.

---

## Bước 5: Cách Trích Xuất Văn Bản – In Kết Quả

Đối tượng `ocr_result` cung cấp thuộc tính tiện lợi `text`. Hãy xem chúng ta nhận được gì.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Đầu ra dự kiến

Nếu mẫu quét chứa:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Bạn sẽ thấy một thứ gì đó như:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Chú ý cách bước tiền xử lý đã loại bỏ các đốm lẻ khiến “Amount” trước đây bị hiển thị thành “Am0unt”. Đó là sức mạnh của **cách giảm nhiễu** trước khi OCR.

---

## Những Sai Lầm Thường Gặp & Cách Khắc Phục

| Triệu chứng | Nguyên nhân có thể | Giải pháp nhanh |
|------------|-------------------|-----------------|
| Ký tự lộn xộn (ví dụ “@#%”) | Ảnh quá tối hoặc quá sáng | Điều chỉnh `threshold` trong `binarize()`; thử `adaptive_threshold`. |
| Thiếu từ | Nhiễu vẫn còn | Tăng `radius` cho `median_blur` hoặc thêm bộ lọc `gaussian_blur`. |
| Ngôn ngữ sai (ví dụ chữ Anh thành chữ Trung) | Gói ngôn ngữ không đúng | Đưa `language="eng"` khi tạo `OcrEngine()` nếu thư viện hỗ trợ. |
| Xử lý chậm trên tệp lớn | Độ phân giải cao | Thu nhỏ ảnh trước: `aocr.ImageFilters.resize(width=1200)` trước khi binarization. |

---

## Tiến Xa Hơn – Các Bước Tiếp Theo và Chủ Đề Liên Quan

- **Xử lý hàng loạt**: Đóng gói logic trên vào một vòng lặp để tự động xử lý hàng chục tệp.  
- **Kết quả có cấu trúc**: Dùng biểu thức chính quy trên `ocr_result.text` để lấy các trường như ngày tháng hoặc số tiền.  
- **Thư viện thay thế**: Thay `aocr` bằng `pytesseract` — chỉ cần thay đổi đoạn khởi tạo engine.  
- **Cách tiền xử lý ảnh cho PDF**: Chuyển mỗi trang PDF thành ảnh, rồi áp dụng cùng pipeline.  

Những mở rộng này cho phép bạn mở rộng giải pháp từ một mẫu đơn lẻ lên một pipeline nhập liệu tài liệu cấp doanh nghiệp.

---

## Kết Luận

Chúng ta đã bao quát **cách chạy OCR** từ đầu đến cuối, trình bày **cách tiền xử lý ảnh** để **giảm nhiễu**, và minh họa **cách trích xuất văn bản từ ảnh** bằng một script sạch, có thể tái sử dụng. Bài học chính? Một vài bộ lọc đơn giản — binarization và median blur — có thể biến một bản quét nhiễu thành nguồn dữ liệu đáng tin cậy, giúp bạn tiết kiệm hàng giờ công việc dọn dẹp thủ công.

Hãy chạy script với tài liệu của riêng bạn, tinh chỉnh các ngưỡng, và quan sát độ chính xác tăng lên. Khi đã sẵn sàng, khám phá xử lý hàng loạt hoặc tích hợp kết quả vào cơ sở dữ liệu để lưu trữ có thể tìm kiếm. Chúc lập trình vui vẻ, và mong OCR của bạn luôn chính xác!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
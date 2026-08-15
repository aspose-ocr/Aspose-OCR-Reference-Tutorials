---
category: general
date: 2026-03-26
description: Học cách chỉnh nghiêng ảnh, nhận dạng văn bản từ ảnh và xây dựng quy
  trình tiền xử lý ảnh để loại bỏ nhiễu trong bản quét và chuyển ảnh đã quét thành
  văn bản.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: vi
og_description: Cách chỉnh nghiêng ảnh và biến một bản scan lệch thành văn bản có
  thể tìm kiếm. Hãy làm theo hướng dẫn này để nhận dạng văn bản từ ảnh, loại bỏ nhiễu
  trong bản scan và chuyển ảnh đã quét thành văn bản.
og_title: Cách chỉnh nghiêng ảnh – Hướng dẫn OCR từng bước
tags:
- OCR
- image-processing
- Python
title: Cách chỉnh nghiêng ảnh – Hướng dẫn toàn diện với OCR
url: /vi/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Thẳng Ảnh – Hướng Dẫn Đầy Đủ Với OCR

Bạn đã bao giờ tự hỏi **cách định thẳng ảnh** xuất từ một máy quét rẻ tiền chưa? Bạn không phải là người duy nhất. Một trang lệch trông không chuyên nghiệp, và quan trọng hơn, độ nghiêng có thể làm rối bất kỳ engine OCR nào đang cố **nhận dạng văn bản từ ảnh**.  

Trong hướng dẫn này, chúng ta sẽ đi qua một **pipeline tiền xử lý ảnh** đầy đủ, bao gồm việc định thẳng, nhị phân hoá và giảm nhiễu một bản quét, sau đó chuyển nó cho một engine OCR để bạn có thể **chuyển ảnh quét sang văn bản** một cách dễ dàng. Không có ma thuật, chỉ là Python thuần và một thư viện nhỏ thực hiện phần công việc nặng.

## Những Gì Bạn Cần Chuẩn Bị

- Python 3.9+ (mã chạy trên 3.10 và mới hơn)
- Gói `ocr` (cài đặt bằng `pip install ocr‑toolkit` – thay bằng tên thư viện thực tế của bạn)
- Một file JPEG hoặc PNG đã quét và có độ nghiêng rõ rệt (ví dụ, `skewed_scan.jpg`)
- Một chút tò mò về lý do mỗi bước tiền xử lý quan trọng

Đó là tất cả. Không cần các phụ thuộc nặng như OpenCV trừ khi bạn muốn đào sâu hơn sau này.

## Bước 1: Tải Ảnh Đã Quét

Điều đầu tiên là đưa file vào bộ nhớ. Bước này đơn giản nhưng quan trọng—nếu đường dẫn sai, mọi thứ sẽ bị lỗi.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Tại sao?**  
> Tải ảnh cho chúng ta một đối tượng có thể thao tác mà `ocr.ImagePreprocessor` có thể làm việc. Bỏ qua bước này sẽ khiến pipeline không có dữ liệu pixel thực tế.

## Cách Định Thẳng Ảnh và Chuẩn Bị Cho OCR

Bây giờ chúng ta đã có ảnh, hãy đưa nó thẳng lại. Phương thức `deskew()` ước tính góc nghiêng và xoay ảnh trở lại vị trí ngang.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Mẹo chuyên nghiệp:** Nếu các bản quét của bạn chỉ hơi lệch (≤ 3°), thuật toán mặc định thường là chính xác. Đối với góc nghiêng lớn, bạn có thể cần điều chỉnh các tham số nội bộ—xem tài liệu thư viện cho `max_angle`.

## Nhị Phân Hoá Ảnh – Chuyển Thành Đen‑Trắng

Các engine OCR thích đầu vào có độ tương phản cao. Chuyển ảnh sang dạng nhị phân (đen‑trắng) loại bỏ các sắc thái mờ mà có thể làm rối việc nhận dạng ký tự.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Đang xảy ra gì?**  
> Các pixel sáng hơn 128 trở thành trắng; phần còn lại trở thành đen. Điều chỉnh ngưỡng nếu bản quét của bạn quá tối hoặc quá sáng.

## Loại Bỏ Nhiễu Trước Khi OCR

Ngay cả khi ảnh đã được định thẳng hoàn hảo, vẫn có thể chứa các đốm, bụi hoặc artefact nén. Những chấm nhỏ này là kẻ thù của bất kỳ engine OCR nào.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Tại sao phải loại bỏ nhiễu?**  
> Nhiễu tạo ra các cạnh giả mà engine OCR có thể hiểu nhầm thành ký tự. Bán kính nhỏ phù hợp với hầu hết các bản quét; tăng lên nếu tài liệu rất nhiễu.

## Áp Dụng Pipeline Tiền Xử Lý Ảnh

Tất cả cấu hình đã sẵn sàng—bây giờ chúng ta chạy pipeline trên ảnh gốc.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Kết quả:** `processed_image` là một bitmap đã được làm sạch, thẳng và có độ tương phản cao, sẵn sàng cho việc trích xuất văn bản.

## Nhận Dạng Văn Bản Từ Ảnh Bằng Engine OCR

Đến lúc thực sự đọc văn bản. Chúng ta khởi tạo engine OCR, đưa vào ảnh đã được tinh chỉnh, và yêu cầu chuỗi kết quả thô.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Kết quả mong đợi** (ví dụ):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Nếu bạn thấy các ký tự lộn xộn, hãy kiểm tra lại bước định thẳng hoặc thử nghiệm với giá trị `threshold` khác.

## Xây Dựng Pipeline Tiền Xử Lý Ảnh – Script Đầy Đủ

Kết hợp mọi thứ lại, đây là một script đơn, có thể chạy được mà bạn có thể lưu vào file `.py` và thực thi:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Mẹo:** Đặt toàn bộ quá trình trong một hàm (`def ocr_from_file(path): …`) nếu bạn dự định xử lý nhiều file theo lô.

## Câu Hỏi Thường Gặp & Các Trường Hợp Cực Đặc

- **Nếu ảnh đã thẳng đứng rồi thì sao?**  
  Phương thức `deskew()` sẽ phát hiện góc gần bằng 0 và không thay đổi ảnh, vì vậy bạn có thể an tâm chạy nó trên mọi file.

- **Bản quét của tôi là màu—có nên giữ lại không?**  
  Màu không mang lại giá trị cho hầu hết các tác vụ OCR. Nhị phân hoá sẽ loại bỏ màu, giúp tăng tốc xử lý và giảm tiêu thụ bộ nhớ.

- **Tôi có thể nối chuỗi nhiều bước tiền xử lý không?**  
  Chắc chắn. Lớp `ImagePreprocessor` được thiết kế cho các pipeline; bạn có thể thêm `sharpen()`, `contrast_enhance()` hoặc các bộ lọc tùy chỉnh trước khi gọi `apply()`.

- **Kết quả OCR có các ngắt dòng lẻ loi—làm sao khắc phục?**  
  Hậu xử lý chuỗi bằng `text.replace("\n", " ").strip()` hoặc dùng thư viện phân tích bố cục nâng cao như chế độ `--psm` của Tesseract.

## Bước Tiếp Theo

Bây giờ bạn đã biết **cách định thẳng ảnh** và có một **pipeline tiền xử lý ảnh** vững chắc, bạn có thể khám phá:

- Tích hợp **nhận dạng văn bản từ ảnh** vào một API Flask để tải tài liệu ngay lập tức.
- Sử dụng pipeline để **loại bỏ nhiễu từ bản quét** các tài liệu lịch sử, nơi việc bảo tồn là quan trọng.
- Mở rộng để xử lý hàng ngàn trang và xuất PDF có thể tìm kiếm bằng `pdfminer` hoặc `PyMuPDF`.

Hãy thoải mái thử nghiệm các ngưỡng, bán kính giảm nhiễu khác nhau, hoặc thậm chí thay đổi backend OCR sang Tesseract nếu bạn cần hỗ trợ đa ngôn ngữ. Các nguyên tắc cơ bản vẫn không thay đổi: đưa thẳng, làm sạch, rồi đọc.

---

*Chúc lập trình vui vẻ! Nếu gặp khó khăn, hãy để lại bình luận bên dưới—tôi sẽ sẵn sàng giúp bạn tinh chỉnh pipeline.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
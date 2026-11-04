---
category: general
date: 2026-06-06
description: Cách tiền xử lý hình ảnh cho OCR bằng Python. Học cách nhị phân hoá hình
  ảnh bằng Otsu, cách chỉnh nghiêng tài liệu đã quét và cải thiện độ chính xác OCR
  cho văn bản tiếng Đức.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: vi
og_description: Cách tiền xử lý hình ảnh cho OCR trong Python. Hướng dẫn này cho thấy
  cách nhị phân hoá hình ảnh bằng Otsu, cách chỉnh nghiêng tài liệu đã quét, và cách
  cải thiện độ chính xác OCR cho hình ảnh tiếng Đức.
og_title: Cách Tiền Xử Lý Hình Ảnh cho OCR – Hướng Dẫn Python Toàn Diện
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: Cách Tiền Xử Lý Hình Ảnh cho OCR – Hướng Dẫn Python Toàn Diện
url: /vi/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tiền Xử Lý Ảnh Cho OCR – Hướng Dẫn Python Đầy Đủ

Bạn đã bao giờ tự hỏi **cách tiền xử lý ảnh cho OCR** để văn bản trở nên trong suốt? Bạn không phải là người duy nhất. Các tài liệu được quét—đặc biệt là những trang tiếng Đức nhiễu—có thể là cơn ác mộng đối với bất kỳ công cụ OCR nào. Tin tốt? Một vài bước tiền xử lý thông minh có thể biến một bản quét mờ, bị vệt thành một hình ảnh sạch, có thể đọc được bởi máy.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ thực tế cho thấy **cách tiền xử lý ảnh cho OCR** bằng Python. Bạn sẽ học cách **binarize image using Otsu**, **how to deskew scanned documents**, và tổng thể **how to improve OCR accuracy** khi cần **extract text from German image**. Không có phần thừa, chỉ có một script hoạt động mà bạn có thể sao chép‑dán ngay hôm nay.

## Những Gì Bạn Cần Chuẩn Bị

- **Python 3.9+** (bất kỳ phiên bản mới nào cũng được)
- Thư viện OCR cung cấp lớp `OcrEngine` – trong ví dụ chúng ta sẽ giả định một gói `ocr` chung. Cài đặt bằng `pip install ocr-lib`.
- Một bản quét tiếng Đức nhiễu (`noisy_german_scan.tif`) mà bạn muốn thử.
- Kiến thức cơ bản về hàm Python (nếu bạn đã viết một `def` trước đây, bạn đã sẵn sàng).

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng một SDK OCR khác (ví dụ, Tesseract qua `pytesseract`), các khái niệm vẫn giữ nguyên—chỉ cần điều chỉnh tên phương thức.

## Tổng Quan Về Giải Pháp

1. **Tạo một thể hiện OCR engine.**  
2. **Đặt ngôn ngữ nhận dạng thành tiếng Đức.**  
3. **Xây dựng một pipeline tiền xử lý tùy chỉnh** bao gồm deskew, denoise, binarization (Otsu) và contrast stretching.  
4. **Gắn pipeline vào engine** để mọi ảnh đều tự động đi qua.  
5. **Chạy OCR** trên bản quét tiếng Đức nhiễu.  
6. **In ra văn bản đã trích xuất** để kiểm chứng kết quả.

Dưới đây chúng ta sẽ phân tích từng bước, giải thích **tại sao** chúng quan trọng, và hiển thị đoạn code chính xác mà bạn cần.

![how to preprocess images for OCR example](image.png "how to preprocess images for OCR example")

## Bước 1: Tạo Một Thể Hiện OCR Engine

Đầu tiên—không có engine, không có gì xảy ra. Đối tượng `OcrEngine` là điểm vào điều phối tất cả các xử lý sau này.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Lý do quan trọng:* Khởi tạo engine thiết lập các tài nguyên nội bộ (như mô hình ngôn ngữ) và cung cấp cho bạn một nền tảng sạch để gắn pipeline tùy chỉnh sau này.

## Bước 2: Đặt Ngôn Ngữ Nhận Dạng Thành Tiếng Đức

Độ chính xác OCR phụ thuộc mạnh vào ngôn ngữ. Khi bạn thông báo cho engine rằng sẽ xử lý tiếng Đức, bạn kích hoạt bộ ký tự và mô hình ngôn ngữ phù hợp.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

Nếu bỏ qua bước này, engine có thể mặc định tiếng Anh, gây lỗi nhận dạng các ký tự umlaut (ä, ö, ü) và ký tự ß—điểm yếu thường gặp khi làm việc với tài liệu tiếng Đức.

## Bước 3: Xây Dựng Pipeline Tiền Xử Lý Tùy Chỉnh

Đây là phần cốt lõi của **cách tiền xử lý ảnh cho OCR**. Chúng ta sẽ nối bốn biến đổi:

| Transformation | What it does | Why it helps |
|----------------|--------------|--------------|
| **Deskew** | Rotates the image back to horizontal (max 5°) | Scans are rarely perfectly aligned; deskewing removes slant that confuses character segmentation. |
| **Denoise** | Reduces random speckles (strength 0.7) | Noise creates false edges that the OCR engine may interpret as characters. |
| **Binarize (Otsu)** | Converts to black‑and‑white using Otsu’s method | A clean binary image gives the engine a sharp contrast between foreground (text) and background. |
| **Contrast Stretch** | Expands the dynamic range | Improves readability of faint strokes, especially on old documents. |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### Cách Deskew Các Tài Liệu Được Quét

Lệnh `deskew` ở trên là câu trả lời cụ thể cho **how to deskew scanned documents**. Nội bộ, nó ước tính góc dòng văn bản chủ đạo bằng biến đổi Hough và xoay ảnh trở lại. Nếu tài liệu của bạn bị quay hơn 5°, tăng `max_angle` lên, nhưng hãy cẩn thận với các hiện tượng artefact do xoay quá mức.

### Binarize Image Using Otsu

Dòng `binarize(method="otsu")` trả lời trực tiếp truy vấn **binarize image using otsu**. Thuật toán Otsu tính ngưỡng tối thiểu phương sai trong‑lớp, rất phù hợp cho các tài liệu có biểu đồ histogram nhị phân (văn bản đậm vs. nền sáng).

## Bước 4: Gắn Pipeline Vào Engine

Bây giờ chúng ta chỉ định cho OCR engine chạy mọi ảnh đầu vào qua pipeline vừa xây dựng.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Lý do quan trọng:* Nếu không đăng ký, engine sẽ xử lý bản quét thô, bỏ qua toàn bộ việc làm sạch mà chúng ta đã cấu hình. Bước này đảm bảo **cách cải thiện độ chính xác OCR** bằng cách áp dụng cùng một tiền xử lý một cách nhất quán.

## Bước 5: Nhận Dạng Văn Bản Từ Bản Quét Tiếng Đức Nhiễu

Đến lúc lắp ráp mọi thứ. Chúng ta đưa engine một ảnh tiếng Đức nhiễu và để nó thực hiện công việc nặng nhọc.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

Nếu bạn muốn biết thời gian thực hiện, có thể đo thời gian gọi hàm:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## Bước 6: Xuất Văn Bản Đã Nhận Dạng

Cuối cùng, chúng ta in ra chuỗi đã trích xuất. Đây là câu trả lời trực tiếp cho **extract text from german image**.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Kết Quả Dự Kiến

Giả sử bản quét mẫu chứa câu “Die schnelle braune Füchsin springt über den faulen Hund.” bạn sẽ thấy kết quả tương tự:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

Nếu đầu ra vẫn còn ký tự lộn xộn, hãy cân nhắc điều chỉnh độ mạnh `denoise` hoặc tăng `max_angle` cho deskew.

## Những Sai Lầm Thường Gặp & Cách Khắc Phục

- **Thiếu mô hình ngôn ngữ:** Quên `set_recognition_language(Language.GERMAN)` thường dẫn đến mất các ký tự umlaut. Kiểm tra lại lời gọi này.
- **Denoise quá mức:** Giá trị mạnh hơn 0.9 có thể xóa bỏ các nét mảnh, đặc biệt trong phông chữ cũ. Giữ trong khoảng 0.5‑0.7 cho hầu hết trường hợp.
- **Định dạng tệp không đúng:** Một số engine OCR không hỗ trợ TIFF đa trang. Nếu bạn có tài liệu đa trang, hãy chia thành các tệp một trang trước.
- **Thứ tự pipeline:** Thứ tự được hiển thị (deskew → denoise → binarize → contrast) là có chủ đích. Binarize trước khi denoise có thể “khóa” nhiễu; luôn denoise trước.

## Mở Rộng Pipeline (Tiếp Theo?)

Giờ bạn đã có một nền tảng vững chắc, có thể muốn:

- **Thêm một phép mở hình thái** để làm sạch các đốm nhỏ (`.morph_open(kernel=3)`).
- **Tích hợp mô hình ngôn ngữ** để sửa lỗi sau khi nhận dạng (`ocr_engine.apply_spellcheck()`).
- **Song song hoá xử lý batch** cho tập dữ liệu lớn bằng `concurrent.futures`.

Tất cả những mở rộng này vẫn giữ nguyên ý tưởng **cách tiền xử lý ảnh cho OCR** trong khi tăng cường **cách cải thiện độ chính xác OCR** hơn nữa.

## Kết Luận

Chúng ta vừa hoàn thành **cách tiền xử lý ảnh cho OCR** từ đầu đến cuối: tạo engine, đặt ngôn ngữ tiếng Đức, xây dựng pipeline **binarize image using Otsu**, **how to deskew scanned documents**, và cuối cùng **extract text from german image** với độ tin cậy cao hơn. Thực hiện sáu bước trên, bạn sẽ thấy chất lượng nhận dạng tăng đáng kể—không còn phải sửa tay vô tận.

Hãy thử script với các bản quét của bạn, điều chỉnh các tham số, và để kết quả tự nói lên câu chuyện. Có câu hỏi về một tweak tiền xử lý cụ thể? Để lại bình luận, chúng tôi sẽ cùng bạn khám phá sâu hơn.

Chúc lập trình vui vẻ, và chúc OCR của bạn luôn chính xác!

## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ cùng giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất văn bản ảnh C# với lựa chọn ngôn ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cách Đặt Giá Trị Ngưỡng Trong Nhận Diện Ảnh OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Cách OCR Ảnh – Thực Hiện OCR Trên Ảnh Trong Nhận Diện Ảnh OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
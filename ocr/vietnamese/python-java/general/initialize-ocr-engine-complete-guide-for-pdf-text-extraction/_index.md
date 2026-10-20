---
category: general
date: 2026-06-25
description: Khởi tạo công cụ OCR trong Python để trích xuất văn bản từ các tệp PDF
  đa trang bằng cách sử dụng từ điển tùy chỉnh, cài đặt ngôn ngữ và mục tiêu vùng.
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: vi
og_description: Khởi tạo công cụ OCR trong Python để đọc PDF tiếng Việt một cách đáng
  tin cậy, cấu hình ngôn ngữ, tiền xử lý và từ điển tùy chỉnh để đạt kết quả chính
  xác.
og_title: Khởi tạo Engine OCR – Hướng dẫn trích xuất PDF từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Khởi tạo Engine OCR – Hướng dẫn toàn diện để trích xuất văn bản từ PDF
url: /vi/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Khởi tạo Engine OCR – Hướng dẫn đầy đủ để trích xuất văn bản PDF

Bạn đã bao giờ cần **khởi tạo engine OCR** cho một loạt hoá đơn tiếng Việt nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, rào cản đầu tiên là làm cho thư viện OCR giao tiếp với các file PDF của bạn, đặc biệt khi bạn phải điều chỉnh ngôn ngữ, tiền xử lý hoặc từ điển tùy chỉnh.

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ đầy đủ, có thể chạy được, cho thấy cách **khởi tạo engine OCR**, cấu hình ngôn ngữ, bật tiền xử lý hình ảnh thông minh, thêm từ điển tùy chỉnh và cuối cùng trích xuất dữ liệu có cấu trúc từ mỗi trang của một file PDF đa trang. Khi hoàn thành, bạn sẽ có một script tự chứa mà bạn có thể đưa vào dự án của mình—không thiếu bất kỳ phần nào, không có các “xem tài liệu” rút gọn.

## Những gì bạn sẽ học

- Cách **khởi tạo engine OCR** với hỗ trợ ngôn ngữ tiếng Việt.  
- Tại sao **cấu hình ngôn ngữ OCR** lại quan trọng đối với độ chính xác.  
- Sử dụng các tùy chọn **tiền xử lý hình ảnh OCR** như tự động chỉnh nghiêng và tự động nhị phân hoá.  
- Thêm **từ điển tùy chỉnh OCR** để cải thiện việc nhận dạng các thuật ngữ chuyên ngành.  
- **Nhận dạng file PDF đa trang** và trích xuất một vùng cụ thể (ví dụ: tổng số tiền).  
- Chuyển đổi kết quả thô thành cấu trúc JSON‑giống sạch sẽ cho quá trình xử lý tiếp theo.

### Yêu cầu trước

- Python 3.8+ đã được cài đặt.  
- Thư viện OCR cung cấp lớp `OcrEngine` (ví dụ sử dụng gói `ocr` giả định; thay thế bằng SDK thực tế của bạn).  
- Một file PDF đa trang mẫu (`sample.pdf`) được đặt trong thư mục đã biết.  
- Kiến thức cơ bản về từ điển và vòng lặp trong Python.

Nếu bạn đã có những thứ này, hãy bắt đầu.

---

## Bước 1: Cách khởi tạo Engine OCR trong Python

Điều đầu tiên bạn phải làm là **khởi tạo engine OCR**. Hãy nghĩ nó như việc bật một máy và cho nó biết ngôn ngữ bạn sẽ cung cấp.

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **Tại sao điều này quan trọng:**  
> Hầu hết các engine OCR đi kèm với các gói ngôn ngữ chung. Bằng cách đặt rõ ràng `ocr_engine.language` bạn tránh việc engine đoán sai ký tự, điều này giảm đáng kể các lỗi nhận dạng các dấu phụ thường gặp trong tiếng Việt.

### Mẹo chuyên nghiệp
Nếu bạn cần hỗ trợ nhiều ngôn ngữ trong cùng một lần chạy, bạn có thể chuyển `ocr_engine.language` một cách linh hoạt trước khi xử lý mỗi trang. Chỉ cần nhớ khởi tạo lại bất kỳ mô hình nặng nào nếu SDK yêu cầu.

---

## Bước 2: Bật các tùy chọn Tiền xử lý Hình ảnh OCR

Các bản scan thô hiếm khi hoàn hảo. Các trang lệch, ánh sáng không đồng đều hoặc độ tương phản thấp có thể làm rối ngay cả những bộ nhận dạng tốt nhất. Đó là lý do chúng ta **cấu hình tiền xử lý hình ảnh OCR** ngay sau khi khởi tạo.

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

Hai cờ này thường đủ để làm sạch hầu hết các hoá đơn đã scan. Nếu các PDF nguồn của bạn đã có chất lượng cao, bạn có thể tắt chúng để tiết kiệm vài mili giây cho mỗi trang.

---

## Bước 3: Thêm Từ điển Tùy chỉnh OCR

Các thuật ngữ chuyên ngành—như mã đơn hàng, ID sản phẩm, hoặc viết tắt pháp lý—hiếm khi xuất hiện trong các mô hình ngôn ngữ chung. Bằng cách cung cấp một **từ điển tùy chỉnh OCR**, bạn đưa cho engine một bản cheat sheet.

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **Điều gì đang diễn ra phía sau?**  
> Engine sẽ tăng điểm tin cậy cho bất kỳ từ nào khớp với mục trong danh sách này, làm cho khả năng nó bị nhận sai thành một thứ khác giảm đáng kể.

---

## Bước 4: Nhận dạng PDF Đa Trang – Trích xuất toàn bộ Văn bản một Lần

Bây giờ engine đã được cấu hình đầy đủ, chúng ta có thể **nhận dạng PDF đa trang**. Phương thức `recognize_multi_page` trả về một danh sách, trong đó mỗi phần tử đại diện cho một trang đã được OCR.

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

Nếu bạn đang xử lý các PDF khổng lồ (hàng trăm trang), hãy cân nhắc xử lý chúng theo từng khối để giữ mức sử dụng bộ nhớ thấp. SDK thường cung cấp một API streaming cho trường hợp này.

---

## Bước 5: Trích xuất Vùng Cụ thể từ Mỗi Trang

Hầu hết các hoá đơn có trường “Tổng cộng” nằm ở cùng một vị trí trên mỗi trang. Thay vì phân tích toàn bộ văn bản trang, chúng ta có thể yêu cầu engine tập trung vào một hình chữ nhật.

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **Tại sao lại nhắm vào một vùng?**  
> Giới hạn OCR trong một khu vực nhỏ giúp tăng tốc xử lý và giảm các kết quả dương tính sai, đặc biệt khi phần còn lại của trang có nhiều nhiễu.

---

## Bước 6: Tạo một Từ điển Kiểu JSON cho Mỗi Trang

Có được văn bản thô là tuyệt vời, nhưng các hệ thống downstream thường mong đợi dữ liệu có cấu trúc. Dưới đây chúng ta xây dựng một từ điển sạch sẽ chứa số trang, toàn bộ văn bản trang, tổng đã trích xuất, và danh sách tất cả các từ đã nhận dạng cùng điểm tin cậy.

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

Chạy script sẽ xuất ra một loạt các từ điển—một cho mỗi trang—trông giống như sau:

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

Bạn có thể dễ dàng chuyển hướng đầu ra tới một file (`> results.jsonl`) để xử lý hàng loạt sau này.

---

## Ví dụ Hoạt động Đầy đủ

Kết hợp tất cả lại, đây là script hoàn chỉnh mà bạn có thể sao chép‑dán và chạy:

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### Kết quả Dự kiến

Chạy script với một file PDF hoá đơn ba trang có thể tạo ra:

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

Bạn có thể tự do pipe kết quả này vào `jq` hoặc bất kỳ trình phân tích JSON nào để xác nhận cấu trúc.

---

## Các Câu hỏi Thường gặp & Trường hợp Cạnh

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu PDF của tôi được bảo vệ bằng mật khẩu thì sao?** | Hầu hết các SDK cho phép bạn truyền tham số `password` vào `recognize_multi_page`. Chỉ cần thêm `password="mySecret"` vào lời gọi. |
| **Các bản scan của tôi là ảnh xám, không phải đen‑trắng.** | Tùy chọn `auto_binarize` sẽ xử lý việc này, nhưng bạn cũng có thể tự chuyển đổi bằng `Pillow` trước khi đưa ảnh vào `recognize_region`. |
| **Tổng tiền đôi khi xuất hiện ở tọa độ khác.** | Hoặc tính toán hình chữ nhật một cách động (ví dụ: qua template matching) hoặc chạy OCR toàn trang rồi tìm kiếm văn bản bằng regex như `r'\d{1,3}(,\d{3})* VND'`. |
| **Hiệu năng chậm trên PDF 500 trang.** | Xử lý theo lô: xử lý 50 trang, ghi kết quả, sau đó xóa danh sách `pages` để giải phóng bộ nhớ. Ngoài ra, tắt `auto_deskew` nếu các bản scan đã thẳng. |
| **Làm sao để hỗ trợ các ngôn ngữ khác sau này?** | Chỉ cần thay đổi `ocr_engine.language = ocr.Language.English` (hoặc bất kỳ enum nào được hỗ trợ) trước khi gọi `recognize_multi_page`. Các phần còn lại của quy trình vẫn giữ nguyên. |

---

## Mẹo cho Triển khai Sản xuất

1. **Xử lý lỗi** – Bao bọc các lời gọi OCR trong khối `try/except`; ghi lại chỉ mục trang khi gặp lỗi để có thể thử lại sau.  
2. **Ghi log** – Sử dụng mô-đun `logging` của Python thay vì `print` để linh hoạt trong việc điều chỉnh mức độ chi tiết.  
3. **Song song** – Nếu thư viện OCR của bạn hỗ trợ đa luồng, khởi tạo một `ThreadPoolExecutor` để xử lý các trang đồng thời.  
4. **File cấu hình** – Lưu ngôn ngữ, từ điển và tọa độ hình chữ nhật trong file JSON/YAML; giúp script tái sử dụng dễ dàng cho các dự án khác nhau.  
5. **Kiểm thử** – Tạo một bộ kiểm thử nhỏ với các PDF đã biết và xác nhận rằng `total_amount` được trích xuất khớp với giá trị mong đợi.  

---

## Kết luận

Bạn vừa học được **

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao quát các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm các ví dụ code hoàn chỉnh cùng giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Nhận dạng văn bản PDF – Các thao tác OCR với Aspose.OCR cho Java](/ocr/english/java/ocr-operations/)
- [Nhận dạng hình ảnh văn bản với Aspose OCR cho nhiều ngôn ngữ](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Trích xuất văn bản từ hình ảnh – Tối ưu hóa OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-01-12
description: Hướng dẫn OCR Python cho thấy cách trích xuất văn bản bảng từ hình ảnh.
  Học cách đọc bảng từ hình ảnh và trích xuất văn bản đã chọn bằng Aspose OCR.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: vi
og_description: Hướng dẫn OCR Python dạy bạn cách trích xuất văn bản bảng từ hình
  ảnh, đọc bảng từ hình ảnh và trích xuất văn bản đã chọn bằng Aspose OCR.
og_title: 'Hướng dẫn OCR Python: Trích xuất văn bản bảng từ hình ảnh'
tags:
- OCR
- Python
- AsposeOCR
title: 'Hướng dẫn OCR Python: Trích xuất văn bản bảng từ hình ảnh'
url: /vi/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng Dẫn Python OCR: Trích Xuất Văn Bản Bảng Từ Hình Ảnh

Bạn đã bao giờ cần một **python ocr tutorial** thực sự chỉ cho bạn cách lấy một bảng ra từ mẫu quét chưa? Bạn không phải là người duy nhất. Hầu hết các hướng dẫn chỉ dừng lại ở việc trích xuất văn bản chung, để bạn phải đoán cách tách lưới dữ liệu gọn gàng mà bạn quan tâm.  

Trong hướng dẫn này, chúng ta sẽ đi qua một kịch bản thực tế: đọc một bảng từ hình ảnh, trích xuất chỉ văn bản đã chọn mà bạn cần, và cuối cùng in ra kết quả. Trong quá trình này, chúng tôi sẽ cung cấp các mẹo về **how to extract table** một cách đáng tin cậy, để bạn không phải tự phát triển lại mỗi lần.

## Những Điều Bạn Sẽ Học

- Cách cài đặt Aspose OCR cho Python.
- Cách định nghĩa một vùng hình chữ nhật chứa bảng.
- Các bước chính xác để **extract table text** và **read table from image**.
- Mẹo xử lý đa ngôn ngữ hoặc bố cục bảng không đều.
- Một script hoàn chỉnh, có thể chạy được mà bạn có thể đưa vào dự án ngay hôm nay.

**Yêu cầu trước**  
- Python 3.8 hoặc mới hơn.  
- Hiểu biết cơ bản về các khái niệm OCR (không cần chuyên môn sâu).  
- Một hình ảnh PNG hoặc JPEG chứa bảng rõ ràng (chúng tôi sẽ gọi nó là `form_with_table.png`).  

Nếu bạn đã có những thứ này, hãy bắt đầu—không có phần thừa, chỉ có mã thực tế.

![python ocr tutorial example of table region](table_region_example.png){alt="ví dụ tutorial python ocr hiển thị vùng bảng"}

## Bước 1: Cài Đặt và Nhập Aspose OCR

Đầu tiên: bạn cần thư viện Aspose OCR. Gói này có trên PyPI, vì vậy một lệnh `pip` duy nhất sẽ thực hiện công việc.

```bash
pip install aspose-ocr
```

Bây giờ nhập mô-đun và bất kỳ trợ giúp nào bạn cần.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Mẹo chuyên nghiệp:* Giữ các phụ thuộc của bạn trong tệp `requirements.txt`. Điều này giúp tái tạo môi trường một cách dễ dàng.

## Bước 2: Khởi Tạo Engine OCR (Python OCR Tutorial Core)

Tạo engine là trung tâm của bất kỳ **python ocr tutorial** nào. Ở đây chúng tôi cũng đặt ngôn ngữ mặc định là tiếng Anh—bạn có thể thay đổi sau.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Tại sao phải đặt ngôn ngữ? Độ chính xác OCR có thể tăng đáng kể khi engine biết các ký tự nào sẽ xuất hiện. Nếu bạn đang xử lý các mẫu đa ngôn ngữ, bạn có thể đặt danh sách ngôn ngữ hoặc ghi đè theo vùng (xem phần sau).

## Bước 3: Tải Hình Ảnh Của Bạn

Aspose OCR hoạt động với hầu hết các định dạng ảnh phổ biến. Chỉ cần chỉ đến đường dẫn tệp, và bạn sẽ có một đối tượng `Image` sẵn sàng để xử lý.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Trường hợp đặc biệt:* Ảnh lớn (hơn 5 MB) có thể làm chậm quá trình xử lý. Hãy cân nhắc thay đổi kích thước hoặc nén chúng trước khi OCR nếu hiệu năng trở thành vấn đề.

## Bước 4: Định Nghĩa Vùng Bảng (Read Table from Image)

Bây giờ là phần thú vị: cho engine biết *ở đâu* bảng nằm. Bạn cung cấp một `OcrRegion` với một `Rectangle` (x, y, width, height). Các tọa độ dựa trên pixel, vì vậy bạn có thể cần thử nghiệm một chút.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Tại sao lại dùng vùng? Bằng cách giới hạn OCR chỉ trong khu vực bảng, chúng ta **extract selected text** nhanh hơn và tránh nhiễu từ các nhãn hoặc đồ họa xung quanh. Điều này cũng cải thiện độ chính xác vì engine có thể tập trung vào bố cục đồng nhất.

## Bước 5: Chạy OCR trên Vùng Đã Định Nghĩa

Với vùng đã thiết lập, chúng ta gọi `process_region`. Phương thức này trả về một đối tượng `OcrResult` chứa văn bản thô, điểm tin cậy, và thậm chí các hộp bao nếu bạn cần sau này.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

Nếu bạn cần trích xuất nhiều bảng, chỉ cần lặp lại Các Bước 4‑5 với các hình chữ nhật khác nhau.

## Bước 6: Xuất Văn Bản Bảng Đã Trích Xuất

Cuối cùng, in—hoặc lưu—đại diện văn bản của bảng. Aspose OCR trả về văn bản thuần với các ngắt dòng thường phù hợp với các hàng, giúp xử lý sau trở nên đơn giản.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Kết quả mong đợi** (ví dụ):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

Bây giờ bạn có thể đưa chuỗi này vào các bộ phân tích `csv`, pandas DataFrames, hoặc bất kỳ pipeline phân tích nào phía sau.

## Ví Dụ Hoạt Động Đầy Đủ

Kết hợp tất cả lại, đây là script hoàn chỉnh bạn có thể chạy ngay. Thay thế `YOUR_DIRECTORY/form_with_table.png` bằng đường dẫn thực tế tới hình ảnh của bạn.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Chạy script bằng `python extract_table.py`. Nếu mọi thứ khớp, bạn sẽ thấy bảng được in ra console.

## Câu Hỏi Thường Gặp & Xử Lý Trường Hợp Đặc Biệt

**Nếu bảng không phải là hình chữ nhật hoàn hảo?**  
Bạn có thể chia bảng thành nhiều vùng chồng lên nhau hoặc dùng một hình chữ nhật lớn hơn bao phủ toàn bộ khu vực và sau đó xử lý văn bản (ví dụ, tách theo ngắt dòng).

**Tôi có thể trích xuất chỉ các cột cụ thể không?**  
Sau khi có toàn bộ văn bản bảng, sử dụng `csv` hoặc `pandas` của Python để cắt ra các cột bạn quan tâm. Bước OCR tự nó trả về mọi thứ trong hình chữ nhật.

**Làm thế nào để làm việc với các bảng không phải tiếng Anh?**  
Đặt `ocr_engine.language` (hoặc `region.language`) thành enum phù hợp, chẳng hạn `ocr.Language.FRENCH` hoặc kết hợp nhiều ngôn ngữ bằng `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**Có cách nào để lấy hộp bao cho mỗi ô không?**  
Aspose OCR có thể trả về `region_result.words` trong đó mỗi từ có một hộp bao. Bạn sẽ cần ánh xạ các hộp này lại thành lưới—hữu ích cho phân tích bố cục nâng cao.

## Mẹo Để Độ Chính Xác Tốt Hơn

- **Làm sạch hình ảnh**: Nhị phân hoá hoặc tăng độ tương phản trước khi đưa vào OCR. Các thư viện như Pillow có thể giúp.
- **Tránh các artefact nén**: Lưu bản quét dưới dạng PNG khi có thể.
- **Chú ý DPI**: 300 dpi là mức lý tưởng; giá trị thấp hơn có thể gây mất ký tự.
- **Thử các kích thước hình chữ nhật khác nhau**: Hình chữ nhật hơi lớn hơn thường bắt được các ký tự lẻ tẻ thuộc bảng.

## Các Bước Tiếp Theo

Bây giờ bạn đã thành thạo **how to extract table** dữ liệu với Aspose OCR, bạn có thể khám phá:

- Chuyển đổi văn bản đã trích xuất thành tệp CSV bằng mô-đun `csv` của Python.
- Đưa dữ liệu vào **pandas** DataFrame để phân tích.
- Sử dụng OCR để đọc các mẫu viết tay (cần engine khác hoặc đào tạo thêm).
- Tự động xử lý hàng loạt hàng chục mẫu quét bằng một vòng lặp `for` đơn giản.

Mỗi phần mở rộng này dựa trên các khái niệm cốt lõi trong **python ocr tutorial** này, vì vậy bạn đã sẵn sàng để mở rộng.

*Chúc lập trình vui vẻ! Nếu gặp bất kỳ khó khăn nào, hãy để lại bình luận bên dưới—tôi sẽ sẵn sàng giúp bạn tinh chỉnh quá trình trích xuất.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
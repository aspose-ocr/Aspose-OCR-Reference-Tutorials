---
category: general
date: 2026-03-26
description: Trích xuất bảng từ hình ảnh và chuyển đổi hình ảnh thành bảng tính bằng
  Python OCR. Tìm hiểu cách tải hình ảnh cho OCR, đọc bảng và trích xuất dữ liệu bảng.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: vi
og_description: Trích xuất bảng từ hình ảnh bằng Python OCR. Hướng dẫn này cho thấy
  cách tải hình ảnh cho OCR, đọc các bảng và chuyển chúng thành bảng tính.
og_title: Trích xuất bảng từ hình ảnh – Hướng dẫn OCR toàn diện
tags:
- OCR
- Python
- Data Extraction
title: Trích xuất bảng từ hình ảnh – Hướng dẫn OCR từng bước
url: /vi/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất bảng từ hình ảnh – Hướng dẫn OCR đầy đủ

Bạn đã bao giờ cần **trích xuất bảng từ hình ảnh** nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi một file PDF hoặc ảnh chụp màn hình chứa dữ liệu dạng bảng cần chuyển thành các hàng và cột có thể chỉnh sửa. Tin tốt là gì? Chỉ với vài dòng Python, kết hợp với một engine OCR mạnh, bạn có thể biến bức ảnh thành bảng tính dùng được trong vài giây.

Trong hướng dẫn này, chúng ta sẽ đi qua các bước tải ảnh để OCR, chạy engine nhận dạng, và lấy ra từng bảng hàng‑hàng. Khi hoàn thành, bạn sẽ có thể **chuyển đổi hình ảnh thành bảng tính**, đồng thời biết cách **ocr read tables** và **ocr extract table data** để xử lý tiếp. Không có phép màu ẩn, chỉ có mã nguồn rõ ràng, chạy được mà bạn có thể đưa vào dự án ngay hôm nay.

---

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã chuẩn bị sẵn:

- **Python 3.9+** – phiên bản ổn định mới nhất hoạt động tốt nhất.  
- Thư viện **`ocr`** (hoặc bất kỳ SDK OCR tương thích nào cung cấp `OcrEngine`, `Image`, và các phương thức liên quan tới bảng). Cài đặt bằng `pip install ocr‑sdk` (thay bằng tên gói thực tế).  
- Một file ảnh (`.png`, `.jpg`, …) chứa bảng được in rõ ràng.  
- Tùy chọn: **pandas** nếu bạn muốn ghi dữ liệu đã trích xuất trực tiếp vào file CSV hoặc Excel (`pip install pandas`).

Mọi thứ đã sẵn sàng? Tuyệt vời—bắt đầu nào.

---

## Bước 1: Nhập SDK OCR và chuẩn bị môi trường

Đầu tiên, chúng ta cần import các lớp OCR vào script và tạo một helper nhỏ sẽ chuyển dữ liệu bảng thô thành DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Tại sao lại quan trọng:** Import `ocr` cho phép chúng ta truy cập `OcrEngine`, `Imaging.Image`, và các đối tượng bảng mà chúng ta sẽ duyệt. `pandas` không bắt buộc để trích xuất, nhưng nó làm cho phần **chuyển đổi hình ảnh thành bảng tính** trở nên đơn giản.

---

## Bước 2: Tải ảnh bạn muốn xử lý

Bây giờ chúng ta thực sự **load image for OCR**. SDK yêu cầu một đối tượng `Image`, vì vậy chúng ta sẽ bọc đường dẫn file bằng phương thức helper `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Mẹo:** Đặt các file ảnh trong một thư mục riêng (`assets/` hoặc `data/`) và dùng đường dẫn tương đối. Như vậy script sẽ dễ di chuyển giữa các máy.

---

## Bước 3: Chạy quá trình nhận dạng

Khi ảnh đã được gắn, chúng ta cuối cùng có thể yêu cầu engine **ocr read tables**. Lệnh `recognize()` trả về một đối tượng kết quả chứa mọi thứ engine phát hiện — các khối văn bản, dòng, và quan trọng nhất là các bảng.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Tại sao cần kiểm tra:** Một số ảnh có thể bị nhiễu hoặc viền bảng mờ, khiến engine bỏ lỡ. Ghi cảnh báo sẽ cung cấp phản hồi sớm mà không làm script bị dừng.

---

## Bước 4: Trích xuất các hàng và ô của từng bảng

Đây là phần “phép màu” thực sự. Chúng ta sẽ duyệt qua mọi bảng được phát hiện, lấy từng hàng, rồi từng ô văn bản. List comprehension bên trong giúp code ngắn gọn, nhưng chúng ta vẫn sẽ giải thích luồng hoạt động.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**Điều gì đang diễn ra?**  

- `enumerate(..., start=1)` cung cấp số bảng thân thiện để log.  
- `row_obj.get_cells()` trả về mỗi đối tượng ô; `cell.get_text()` lấy chuỗi đã giải mã bởi OCR.  
- Chúng ta lưu các hàng vào `rows_data`, sau đó truyền cho `pandas.DataFrame` để tự động căn chỉnh cột.  
- Khối `print` phản ánh **kết quả thiết yếu** như trong đoạn code gốc, giúp bạn kiểm tra ngay lập tức.

**Xử lý trường hợp đặc biệt:** Nếu một hàng có số ô khác với các hàng khác, `pandas` sẽ tự động chèn `NaN`. Bạn có thể làm sạch DataFrame sau này bằng `df.fillna('')` nếu muốn thay bằng chuỗi rỗng.

---

## Bước 5: Lưu các bảng đã trích xuất vào bảng tính

Bây giờ chúng ta đã có danh sách các DataFrame, việc chuyển chúng thành một workbook Excel (hoặc file CSV) là chuyện nhẹ. Điều này đáp ứng mục tiêu “convert image to spreadsheet”.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Tại sao lại là Excel?** Hầu hết người dùng doanh nghiệp thích `.xlsx`. Nếu bạn muốn CSV, thay vòng lặp bằng `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Script đầy đủ, sẵn sàng chạy

Kết hợp mọi thứ lại, đây là chương trình hoàn chỉnh bạn có thể sao chép‑dán và thực thi.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Kết quả console dự kiến** (giả sử bảng đơn giản 2×3):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Và bạn sẽ thấy file `extracted_tables.xlsx` trong thư mục chứa script, mỗi bảng trên một sheet riêng.

---

## Câu hỏi thường gặp & Mẹo

| Câu hỏi | Trả lời |
|----------|--------|
| **Có thể dùng thư viện OCR khác không?** | Chắc chắn. Quy trình vẫn giống: load image → recognize → iterate over `get_tables()`. Chỉ cần thay đổi import và tên đối tượng. |
| **Nếu ảnh của tôi bị nhiễu thì sao?** | Tiền xử lý bằng OpenCV (thresholding, deskew) trước khi đưa vào engine OCR. Giảm nhiễu thường cải thiện độ chính xác của **ocr extract table data**. |
| **Có cần cài đặt `openpyxl` không?** | Có, `pandas` sử dụng nó ngầm để xuất Excel. Cài đặt bằng `pip install openpyxl`. |
| **Làm sao xử lý các ô hợp nhất?** | Một số SDK cung cấp `cell.is_merged()`; bạn có thể phát hiện và sao chép giá trị sang các ô hợp nhất một cách thủ công. |
| **Có cách chỉ trích xuất các bảng cụ thể không?** | Lọc bằng `table_obj.get_confidence()` hoặc kiểm tra từ khóa tiêu đề trước khi xử lý. |

---

## Kết luận

Bạn đã có một giải pháp hoàn chỉnh, từ đầu đến cuối, để **extract tables from image**, chuyển kết quả thành bảng tính gọn gàng, và thậm chí xử lý nhiều bảng trong một ảnh duy nhất. Script này minh họa cách **load image for OCR**, **ocr read tables**, và **ocr extract table data** đồng thời vẫn đủ linh hoạt cho các biến thể thực tế.

Tiếp theo bạn muốn làm gì? Hãy thử đưa một trang PDF đã được render thành ảnh vào engine OCR, hoặc thử nghiệm với các ngôn ngữ và phông chữ khác nhau. Bạn cũng có thể truyền DataFrame trực tiếp vào cơ sở dữ liệu hoặc công cụ báo cáo — giới hạn chỉ là trí tưởng tượng của bạn.

Nếu bạn thấy hướng dẫn này hữu ích, hãy chia sẻ, star repository chứa SDK, hoặc để lại bình luận với các mẹo của mình. Chúc bạn lập trình vui vẻ, và hy vọng các bảng của bạn luôn được phân tích một cách hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
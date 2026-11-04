---
category: general
date: 2026-04-26
description: Cách thực hiện OCR hàng loạt cho tài liệu và trích xuất văn bản từ các
  bản quét bằng Python. Học quy trình xử lý hàng loạt từng bước với OcrEngine để xuất
  ra định dạng JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: vi
og_description: Cách thực hiện OCR hàng loạt cho các tệp đã quét và trích xuất văn
  bản từ các bản quét trong một script duy nhất. Mã hoàn chỉnh, mẹo và xử lý các trường
  hợp đặc biệt.
og_title: Cách thực hiện OCR hàng loạt – Hướng dẫn Python nhanh
tags:
- OCR
- Python
- Automation
title: Cách thực hiện OCR hàng loạt – Trích xuất văn bản từ ảnh quét một cách hiệu
  quả
url: /vi/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện Batch OCR – Trích Xuất Văn Bản Từ Các Tập Tin Quét Hiệu Quả

Bạn đã bao giờ tự hỏi **cách batch OCR** một đống tài liệu PDF đã quét mà không mất trí không? Bạn không phải là người duy nhất—các nhà phát triển liên tục hỏi, *“Làm sao tôi có thể trích xuất văn bản từ các tập tin quét trong một lần?”* Tin tốt là chỉ với vài dòng Python, công việc tẻ nhạt đó có thể biến thành một quy trình tự động mượt mà.

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh, sẵn sàng chạy mà **trích xuất văn bản từ các tập tin quét**, lưu kết quả dưới dạng JSON, và cung cấp cho bạn một kiểm tra nhanh cuối cùng. Không có dịch vụ bên ngoài, không có phép thuật—chỉ Python thuần, lớp `OcrEngine`, và một chút xử lý thư mục.

## Những Điều Bạn Sẽ Nhận Được

- Một script hoạt động đầy đủ có thể **batch OCR** trên bất kỳ thư mục ảnh nào.
- Giải thích rõ ràng *tại sao* mỗi dòng tồn tại, không chỉ *cái gì* nó làm.
- Mẹo xử lý các thư mục trống, tệp không phải ảnh, và các batch lớn.
- Cách xác minh rằng đầu ra JSON thực sự chứa văn bản đã trích xuất.

### Yêu Cầu Cơ Bản (tối thiểu nhất)

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| Python 3.8+ | Cú pháp hiện đại & gợi ý kiểu |
| `OcrEngine` library (or a compatible wrapper) | Chức năng OCR cốt lõi |
| A directory with scanned image files (PNG, JPG, TIFF) | Thư mục chứa các tệp ảnh đã quét (PNG, JPG, TIFF) |
| Write permissions for the output folder | Quyền ghi cho thư mục đầu ra |

Nếu bạn đã có những thứ này, tuyệt vời—hãy bắt đầu.

![how to batch OCR workflow](image-placeholder.png){alt="luồng công việc batch OCR"}

## Bước 1 – Khởi Tạo Engine OCR (cách batch OCR)

Trước khi chúng ta có thể xử lý bất kỳ thứ gì, chúng ta cần một thể hiện của engine OCR. Hãy nghĩ nó như “bộ não” sẽ đọc mỗi ảnh và xuất ra văn bản. Khởi tạo một lần và tái sử dụng nó cho toàn bộ batch là mẫu hiệu quả nhất.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Tại sao lại tái sử dụng cùng một thể hiện?**  
> Tạo một engine mới cho mỗi tệp sẽ liên tục tải các mô hình nặng vào bộ nhớ, làm chậm batch đáng kể. Một thể hiện duy nhất giữ mô hình trong RAM và cho phép bạn xử lý hàng nghìn ảnh mà không gặp sự chậm lại đáng chú ý.

## Bước 2 – Chỉ Định Thư Mục Chứa Các Tập Tin Quét (trích xuất văn bản từ các tập tin quét)

Các tập tin quét của bạn nằm ở đâu đó trên đĩa. Hãy cho script biết nơi chúng nằm. Sử dụng đường dẫn tuyệt đối tránh những bất ngờ “không tìm thấy tệp” khi script được chạy từ thư mục làm việc khác.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Mẹo chuyên nghiệp:**  
> Nếu bạn đang dùng Windows, dấu gạch chéo (`/`) hoạt động tốt với `os.path.abspath`, vì vậy bạn không cần escape dấu gạch ngược.

## Bước 3 – Chọn Địa Điểm Lưu Kết Quả JSON

Bạn có lẽ muốn một thư mục gọn gàng cho kết quả OCR. Giữ đầu ra riêng biệt với nguồn giúp việc dọn dẹp sau này dễ dàng hơn hoặc đưa JSON vào một pipeline khác.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Tại sao tạo thư mục bằng chương trình?**  
> Điều này đảm bảo script sẽ không bị crash nếu thư mục chưa tồn tại, và `exist_ok=True` làm cho thao tác trở nên idempotent—chạy script nhiều lần mà không gặp lỗi.

## Bước 4 – Chạy Quá Trình Batch (cách batch OCR)

Bây giờ là phần cốt lõi: yêu cầu `ocr_engine` duyệt qua mọi tệp trong `input_dir`, thực hiện OCR, và ghi JSON vào `output_dir`. Tham số `format="json"` báo cho engine tuần tự hoá kết quả theo cách có cấu trúc mà các công cụ downstream yêu thích.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Điều gì đang diễn ra bên trong?

1. **Khám phá tệp** – Engine quét `input_folder` một cách đệ quy, bỏ qua các tệp ẩn.  
2. **Xác thực tệp** – Chỉ các phần mở rộng ảnh được hỗ trợ (`.png`, `.jpg`, `.tif`, v.v.) mới được đưa vào mô hình OCR.  
3. **Thực thi OCR** – Mỗi ảnh được gửi tới engine OCR; văn bản, điểm tin cậy và dữ liệu bố cục được ghi lại.  
4. **Tuần tự hoá JSON** – Kết quả được ghi vào một tệp có cùng tên cơ sở nhưng có phần mở rộng `.json` trong `output_folder`.

> **Xử lý các trường hợp đặc biệt:**  
> - **Thư mục trống:** Engine ghi log “No files found” và trả về một cách êm ái.  
> - **Ảnh hỏng:** Bỏ qua tệp, ghi một mục lỗi vào `batch_errors.log`, và tiếp tục.  
> - **Batch lớn (hơn 10k tệp):** Việc sử dụng bộ nhớ vẫn thấp vì mỗi ảnh được xử lý độc lập.

## Bước 5 – Xác Nhận Quá Trình Chuyển Đổi Hoàn Thành

Một câu lệnh `print` đơn giản cung cấp phản hồi ngay lập tức trong console. Đối với các pipeline sản xuất, bạn có thể thay thế bằng lời gọi logging hoặc thông báo email.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Khi bạn thấy dòng này, bạn có thể an toàn kiểm tra thư mục `json_output`. Mỗi tệp JSON sẽ trông tương tự như sau:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Bây giờ bạn có thể đưa các tệp JSON này vào cơ sở dữ liệu, chỉ mục tìm kiếm, hoặc bất kỳ công cụ phân tích downstream nào.

## Câu Hỏi Thường Gặp (và câu trả lời nhanh)

**Q: Nếu tôi cần xử lý PDF thay vì ảnh thì sao?**  
A: Đầu tiên chuyển mỗi trang PDF thành ảnh (ví dụ, dùng `pdf2image`) và đặt các tệp PNG/JPG kết quả vào `input_dir`. Logic batch OCR vẫn không thay đổi.

**Q: Tôi có thể đổi định dạng đầu ra thành văn bản thuần không?**  
A: Chắc chắn. Thay `format="json"` bằng `format="txt"` và engine sẽ ghi một tệp `.txt` chỉ chứa văn bản đã trích xuất.

**Q: Các tập tin quét của tôi nằm trong nhiều thư mục con—script có duyệt đệ quy không?**  
A: Có. `batch_process` mặc định duyệt cây thư mục. Nếu bạn muốn đầu ra phẳng, đặt `flatten=True` (nếu thư viện hỗ trợ) hoặc xử lý hậu kỳ tên tệp JSON.

**Q: Làm sao tôi xử lý các script không phải Latin?**  
A: Khởi tạo `OcrEngine` với tham số ngôn ngữ, ví dụ `OcrEngine(lang="spa+eng")`. Vòng lặp batch không cần thay đổi gì.

## Mẹo Chuyên Nghiệp & Những Cạm Bẫy Thường Gặp

- **Kích thước batch quan trọng:** Nếu bạn thấy CPU tăng đột biến, hãy giảm tốc quá trình bằng cách chèn `time.sleep(0.1)` đơn giản giữa các tệp.  
- **Logging:** Thay lời gọi `print` bằng mô-đun `logging` của Python để ghi lại thời gian và mức độ lỗi.  
- **Xung đột tên tệp:** Nếu hai ảnh quét có cùng tên cơ sở nhưng nằm trong các thư mục con khác nhau, các tệp JSON sẽ ghi đè lên nhau. Thêm một hash của đường dẫn tương đối vào tên đầu ra để tránh điều này.  
- **Rò rỉ bộ nhớ:** Một số backend OCR giữ lại tài nguyên gốc. Gọi `ocr_engine.close()` vào cuối script nếu thư viện cung cấp phương thức dọn dẹp.

## Toàn Bộ Script – Sẵn Sàng Sao Chép & Dán

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Kết quả console dự kiến**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Bạn có thể xác minh JSON bằng cách mở bất kỳ tệp nào trong `json_output` bằng trình soạn thảo văn bản hoặc tải nó trong Python:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Bạn sẽ thấy văn bản thô đã được OCR trích xuất được in ra console.

## Kết Luận

Chúng ta vừa vừa hoàn thành **cách batch OCR** một thư mục đầy ảnh đã quét và **trích xuất văn bản từ các tập tin quét** thành các tệp JSON sạch, có thể đọc được bởi máy. Cách tiếp cận được thiết kế đơn giản: thiết lập engine một lần, chỉ định thư mục, và để thư viện thực hiện phần nặng. Từ đây bạn có thể:

- Kết nối JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
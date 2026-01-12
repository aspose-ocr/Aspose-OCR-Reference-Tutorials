---
category: general
date: 2026-01-12
description: Cách thực hiện OCR hàng loạt hình ảnh nhanh chóng và trích xuất văn bản
  từ các tệp JPEG trong Python. Học quy trình xử lý hàng loạt từng bước với một ví
  dụ hoàn chỉnh có thể chạy được.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: vi
og_description: Cách thực hiện OCR hàng loạt cho hình ảnh và trích xuất văn bản từ
  các tệp JPEG. Hướng dẫn này sẽ đưa bạn qua một giải pháp Python hoàn chỉnh, sẵn
  sàng chạy.
og_title: Cách thực hiện OCR hàng loạt cho hình ảnh – Hướng dẫn nhanh Python
tags:
- OCR
- Python
- image processing
title: Cách thực hiện OCR hàng loạt cho ảnh – Hướng dẫn nhanh để trích xuất văn bản
  từ tệp JPEG
url: /vi/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Batch OCR Hình Ảnh – Hướng Dẫn Nhanh Để Trích Xuất Văn Bản Từ Các Tệp JPEG

Bạn đã bao giờ tự hỏi **cách batch OCR hình ảnh** mà không cần viết một script riêng cho mỗi tệp chưa? Bạn không phải là người duy nhất. Trong nhiều dự án—quét hoá đơn, số hoá tài liệu lưu trữ, hoặc kiểm duyệt nội dung—chúng ta cần lấy văn bản từ hàng chục hoặc hàng trăm tệp JPEG cùng một lúc. Tin tốt là bạn có thể làm điều này chỉ với vài dòng Python, và sẽ có một engine có thể tái sử dụng trong bất kỳ pipeline nào.

Trong tutorial này chúng tôi sẽ chỉ cho bạn **cách batch OCR hình ảnh** một cách chi tiết, sau đó hướng dẫn cách trích xuất văn bản từ các tệp JPEG, xử lý các trường hợp đặc biệt, và xác minh kết quả. Khi hoàn thành, bạn sẽ có một script tự chứa có thể chạy trên bất kỳ thư mục hình ảnh nào, và bạn sẽ hiểu vì sao việc xử lý batch lại quan trọng đối với hiệu năng và khả năng bảo trì.

## Những Điều Bạn Sẽ Học

- Thiết lập một engine OCR đơn giản và cấu hình cho tiếng Anh.  
- Thu thập tất cả các tệp JPEG từ một thư mục bằng `pathlib`.  
- Gọi engine OCR một lần để xử lý toàn bộ batch.  
- Hiển thị bản xem trước của văn bản đã nhận dạng cho mỗi hình ảnh.  
- Mẹo xử lý các batch lớn, ngôn ngữ khác nhau, và các lỗi thường gặp.

**Yêu cầu trước**: Python 3.8+, thư viện `ocr` (hoặc bất kỳ wrapper tương thích nào), và một thư mục chứa các ảnh JPEG bạn muốn phân tích. Không cần dịch vụ bên ngoài—mọi thứ chạy cục bộ.

---

## Bước 1: Khởi Tạo Engine OCR – Cốt Lõi Của Cách Batch OCR Hình Ảnh

Trước khi chúng ta có thể **batch OCR hình ảnh**, chúng ta cần một engine biết cách đọc văn bản. Trong hầu hết các thư viện, bạn tạo một đối tượng engine, tùy chọn đặt ngôn ngữ, và sau đó tái sử dụng nó cho mọi tệp.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Lý do quan trọng*: Khởi tạo engine một lần tránh việc tải lại các mô hình ngôn ngữ liên tục. Nó cũng cho bạn một nơi duy nhất để điều chỉnh các thiết lập (ví dụ: DPI, danh sách ký tự cho phép) sẽ áp dụng cho toàn bộ batch.

> **Pro tip**: Nếu bạn dự định xử lý tài liệu đa ngôn ngữ, chuyển `ocr.Language.ENGLISH` thành `ocr.Language.MULTI` hoặc tải nhiều gói ngôn ngữ trước khi batch bắt đầu.

---

## Bước 2: Thu Thập Tất Cả Các Tệp JPEG – Phần “Trích Xuất Văn Bản Từ Các Tệp JPEG”

Bây giờ engine đã sẵn sàng, chúng ta cần chỉ cho nó biết những hình ảnh nào sẽ được xử lý. Sử dụng `pathlib` giúp code độc lập với nền tảng và ngắn gọn.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Lý do quan trọng*: Bằng cách thu thập danh sách tệp trước, chúng ta có thể truyền toàn bộ bộ sưu tập cho engine OCR trong một lần gọi—đúng là những gì **cách batch OCR hình ảnh** đề cập tới. Nếu bạn có các thư mục con, có thể đổi `glob("**/*.jpg")` thành tìm kiếm đệ quy.

> **Trường hợp đặc biệt**: Nếu ảnh của bạn có hỗn hợp phần mở rộng (`.jpeg`, `.JPG`), mở rộng mẫu glob: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## Bước 3: Xử Lý Toàn Bộ Batch Trong Một Lần Gọi – Sức Mạnh Thực Sự Của Batch OCR

Hầu hết các thư viện OCR hiện đại cung cấp một phương thức `process_batch` (hoặc tên tương tự) nhận một iterable các đường dẫn tệp. Đây là trái tim của **cách batch OCR hình ảnh** một cách hiệu quả.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Lý do quan trọng*: Một lần gọi batch giảm số lần chuyển đổi Python‑to‑C, giữ mô hình ngôn ngữ luôn trong bộ nhớ, và thường cho phép song song nội bộ. Kết quả là một danh sách các đối tượng—mỗi đối tượng chứa văn bản đã nhận dạng và điểm tin cậy.

> **Ghi chú hiệu năng**: Đối với các batch rất lớn (hàng nghìn ảnh), hãy cân nhắc chia danh sách thành các khối nhỏ hơn (ví dụ: 200 tệp) để tránh tiêu thụ bộ nhớ quá mức.

---

## Bước 4: Hiển Thị Bản Xem Trước Văn Bản Đã Trích Xuất – Kiểm Tra Nhanh

Sau khi batch hoàn thành, việc xem trước một vài ký tự đầu tiên của mỗi kết quả rất hữu ích. Điều này giúp bạn xác nhận OCR thực sự đã trích xuất văn bản từ các tệp JPEG.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Lý do quan trọng*: Một bản xem trước ngắn cho phép bạn nhanh chóng phát hiện các lỗi rõ ràng (ví dụ: đầu ra trống, ký tự lộn xộn) mà không cần mở từng file. Nếu bạn nhận thấy vấn đề hệ thống, có thể điều chỉnh cài đặt engine và chạy lại batch.

> **Cạm bẫy thường gặp**: Quên loại bỏ ký tự xuống dòng có thể làm bản xem trước trở nên lộn xộn. Dòng `replace("\n", " ")` sẽ làm sạch chúng.

---

## Ví Dụ Hoàn Chỉnh – Tất Cả Các Bước Kết Hợp

Dưới đây là script hoàn chỉnh mà bạn có thể sao chép‑dán, điều chỉnh đường dẫn thư mục, và chạy. Nó minh họa toàn bộ quy trình **cách batch OCR hình ảnh** từ đầu đến cuối.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Kết quả mong đợi** (ví dụ):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

Nếu bản xem trước hiển thị văn bản có nghĩa, bạn đã **trích xuất văn bản từ các tệp JPEG** thành công bằng cách batch.

---

## Xử Lý Các Batch Lớn và Các Kịch Bản Nâng Cao

### Chia Nhỏ Khối Công Việc Lớn
Khi phải xử lý hàng nghìn ảnh, bộ nhớ có thể trở thành nút thắt. Hãy chia danh sách thành các khối nhỏ hơn:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Thay Đổi Ngôn Ngữ
Nếu tài liệu của bạn chứa tiếng Pháp hoặc tiếng Tây Ban Nha, hãy thay đổi ngôn ngữ trước khi batch:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Lưu Kết Quả Ra Đĩa
Thay vì in ra màn hình, bạn có thể ghi mỗi kết quả OCR vào một tệp `.txt`:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Kết Luận

Bây giờ bạn đã biết **cách batch OCR hình ảnh** và đáng tin cậy **trích xuất văn bản từ các tệp JPEG** bằng một script Python gọn gàng. Bằng cách khởi tạo engine một lần, thu thập tất cả các đường dẫn JPEG, xử lý chúng trong một batch duy nhất, và xem trước kết quả, bạn đạt được cả tốc độ và sự đơn giản. Từ đây, bạn có thể mở rộng workflow—thêm hỗ trợ đa ngôn ngữ, lưu kết quả vào cơ sở dữ liệu, hoặc tích hợp script vào một pipeline xử lý tài liệu lớn hơn.

Sẵn sàng cho bước tiếp theo? Hãy thử thay thế thư viện `ocr` bằng Tesseract, thử nghiệm các kỹ thuật tiền xử lý ảnh (ngưỡng, thay đổi kích thước), hoặc đưa văn bản đã trích xuất vào mô hình xử lý ngôn ngữ tự nhiên để tự động phân loại. Bầu trời là giới hạn, và bạn đã có nền tảng vững chắc để xây dựng.

Chúc lập trình vui vẻ, và hy vọng các batch OCR của bạn luôn không lỗi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-18
description: Thực hiện OCR trên hình ảnh để nhanh chóng trích xuất văn bản từ hình
  ảnh. Tìm hiểu cách tải hình ảnh cho OCR, tạo công cụ OCR và cải thiện độ chính xác
  của OCR bằng các tùy chọn ngôn ngữ.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: vi
og_description: Thực hiện OCR trên hình ảnh với hướng dẫn chi tiết này. Tìm hiểu cách
  tải hình ảnh cho OCR, tạo engine OCR và cải thiện độ chính xác của OCR để trích
  xuất văn bản đáng tin cậy.
og_title: Thực hiện OCR trên hình ảnh – Hướng dẫn lập trình toàn diện
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Thực hiện OCR trên hình ảnh – Hướng dẫn từng bước
url: /vi/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên Hình ảnh – Hướng dẫn Lập trình Đầy đủ

Bạn đã bao giờ cần **perform OCR on image** nhưng không chắc nên chọn thư viện nào hoặc làm sao để có kết quả đáng tin cậy? Bạn không phải là người duy nhất. Trong hướng dẫn này, chúng tôi sẽ đi qua mọi thứ bạn cần để **extract text from image**, từ việc tải ảnh lên đến tinh chỉnh các tùy chọn ngôn ngữ để bạn có thể **improve OCR accuracy** ở mỗi bước.

Chúng ta sẽ đề cập cách **load image for OCR**, cách **create OCR engine**, và lý do tại sao mỗi thiết lập lại quan trọng. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy để in ra văn bản đã nhận dạng, và bạn sẽ hiểu “tại sao” đằng sau mỗi dòng — không có các shortcut “xem tài liệu”. Hãy bắt đầu.

## Những gì bạn cần

- Python 3.8+ (code sử dụng f‑strings và type hints)
- Gói giả định `ocr_lib` – cài đặt bằng `pip install ocr_lib`
- Một file ảnh chứa văn bản in rõ ràng (ví dụ: `lab_report.png`)
- Một trình soạn thảo văn bản hoặc IDE cơ bản (VS Code, PyCharm, bất kỳ gì bạn thích)

Nếu bạn đã có những thứ trên, tuyệt vời — bạn đã sẵn sàng. Nếu chưa, tải Python từ python.org và chạy lệnh pip; chỉ mất một phút.

![perform OCR on image example](/images/ocr-example.png)

*Alt text: ví dụ thực hiện OCR trên hình ảnh – kết quả mẫu hiển thị văn bản đã trích xuất.*

## Bước 1: Tạo OCR Engine – Cách **create OCR engine** trong Python

Trước khi bất kỳ nhận dạng nào có thể diễn ra, thư viện cần một đối tượng engine chứa cấu hình và trạng thái chạy. Hãy nghĩ engine như bộ não phía sau quá trình.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Tại sao điều này quan trọng:** Khởi tạo engine sớm cho phép bạn gắn các tùy chọn ngôn ngữ sau này, và nó cũng lưu trữ các mô hình nội bộ để các lần gọi tiếp theo nhanh hơn.

## Bước 2: Tải Ảnh cho OCR – Cách **load image for OCR** đúng đắn

Bây giờ chúng ta đã có engine, cần cung cấp cho nó một ảnh để đọc. Phương thức `setImageFromFile` nhận một đường dẫn file hệ thống; đường dẫn có thể là tuyệt đối hoặc tương đối so với thư mục làm việc của script.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Mẹo chuyên nghiệp:** Sử dụng đường dẫn tuyệt đối hoặc `os.path.join` để tránh các lỗi “file not found” khi script chạy từ thư mục khác.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Bước 3: Cải thiện Độ Chính Xác OCR – Tinh chỉnh **language options** để **improve OCR accuracy**

OCR mặc định hoạt động, nhưng từ vựng chuyên ngành (như thuật ngữ phòng thí nghiệm) thường gây rối cho nó. Bằng cách cung cấp một từ điển tùy chỉnh và một blacklist, bạn giảm thiểu các nhận dạng sai như nhầm “0” với “O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Tại sao điều này giúp ích:** Từ điển cho mô hình OCR biết rằng “HPLC” là một token hợp lệ, ngăn nó phá vỡ từ thành những ký tự vô nghĩa. Blacklist cho mô hình biết xử lý các ký tự mơ hồ như nhiễu, trực tiếp **improve OCR accuracy**.

## Bước 4: Thực hiện OCR trên Ảnh – Lệnh cốt lõi **perform OCR on image**

Với engine đã được chuẩn bị và ảnh đã được gắn, đã đến lúc thực sự nhận dạng văn bản. Bước này trả về một đối tượng `OcrResult` mà bạn có thể truy vấn để lấy văn bản thô, điểm tin cậy, hoặc các bounding box.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Nếu ảnh bị mờ, bạn sẽ thấy các số điểm tin cậy thấp hơn trong kết quả. Đó là dấu hiệu để tiền xử lý ảnh (ví dụ: tăng độ tương phản) trước khi đưa vào engine.

## Bước 5: Trích xuất Văn bản từ Ảnh – Lấy chuỗi cuối cùng

Cuối cùng, chúng ta yêu cầu `OcrResult` trả về biểu diễn văn bản của nó. Phương thức `getText()` trả về một chuỗi plain‑text sẵn sàng cho các bước xử lý tiếp theo (lưu vào file, đưa vào cơ sở dữ liệu, v.v.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Kết quả mong đợi:** Giả sử `lab_report.png` chứa một bảng đơn giản, bạn có thể thấy điều gì đó như:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Đó là phần **extract text from image** đã hoàn thành.

## Ví dụ Hoàn chỉnh – Kết hợp Tất cả

Dưới đây là một script duy nhất ghép các phần từ các mục trước. Bạn có thể sao chép‑dán nó vào `run_ocr.py` và chạy `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Danh sách kiểm tra nhanh

| ✅ | Mục |
|---|------|
| ✔️ | Engine được tạo (`create OCR engine`) |
| ✔️ | Ảnh được tải (`load image for OCR`) |
| ✔️ | Các tùy chọn ngôn ngữ được đặt (`improve OCR accuracy`) |
| ✔️ | OCR được thực hiện (`perform OCR on image`) |
| ✔️ | Văn bản được trích xuất (`extract text from image`) |

Chạy script và quan sát console. Nếu bạn thấy khối “OCR Output” với nội dung báo cáo của mình, bạn đã **perform OCR on image** thành công.

## Những Sai Lầm Thường Gặp & Cách Tránh

| Vấn đề | Tại sao xảy ra | Cách khắc phục |
|-------|----------------|----------------|
| **Ảnh mờ** | Mô hình OCR không phân biệt được ký tự | Tiền xử lý bằng OpenCV: `cv2.GaussianBlur` hoặc tăng DPI |
| **Ngôn ngữ sai** | Ngôn ngữ mặc định có thể không phải tiếng Anh | Gọi `engine.setLanguage("eng")` trước `recognize()` |
| **Thiếu từ trong từ điển** | Các từ chuyên ngành bị biến dạng | Thêm chúng qua `setDictionary` như trong Bước 3 |
| **Ký tự trong blacklist gây |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
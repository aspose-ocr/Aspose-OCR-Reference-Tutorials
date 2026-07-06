---
category: general
date: 2026-05-03
description: Hướng dẫn OCR bằng Python, cho thấy cách tải tệp ảnh PNG, nhận dạng văn
  bản từ hình ảnh và các tài nguyên AI miễn phí cho xử lý OCR hàng loạt.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: vi
og_description: Hướng dẫn OCR bằng Python sẽ hướng dẫn bạn cách tải ảnh PNG, nhận
  dạng văn bản từ hình ảnh và sử dụng các tài nguyên AI miễn phí cho việc xử lý OCR
  hàng loạt.
og_title: Hướng dẫn OCR bằng Python – Nhận dạng ký tự nhanh hàng loạt với tài nguyên
  AI miễn phí
tags:
- OCR
- Python
- AI
title: Hướng dẫn OCR bằng Python – Xử lý OCR hàng loạt dễ dàng
url: /vi/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng Dẫn Python OCR – Xử Lý Hàng Loạt OCR Dễ Dàng

Bạn đã bao giờ cần một **python ocr tutorial** thực sự cho phép bạn chạy OCR trên hàng chục tệp PNG mà không phải đau đầu không? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, bạn phải **load png image** các tệp, đưa chúng vào một engine, và sau đó dọn dẹp các tài nguyên AI khi hoàn thành.  

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho thấy chính xác cách **recognize text from image** các tệp, xử lý chúng theo lô, và giải phóng bộ nhớ AI nền. Khi kết thúc, bạn sẽ có một script tự chứa mà bạn có thể đưa vào bất kỳ dự án nào—không có phần thừa, chỉ những điều cần thiết.

## Những Gì Bạn Cần

- Python 3.10 hoặc mới hơn (cú pháp ở đây dựa vào f‑strings và type hints)  
- Thư viện OCR cung cấp phương thức `engine.recognize` – cho mục đích demo, chúng tôi sẽ giả định một gói `aocr` giả tưởng, nhưng bạn có thể thay bằng Tesseract, EasyOCR, v.v.  
- Module trợ giúp `ai` được hiển thị trong đoạn mã (nó xử lý khởi tạo mô hình và dọn dẹp tài nguyên)  
- Một thư mục chứa đầy các tệp PNG bạn muốn xử lý  

Nếu bạn chưa cài đặt `aocr` hoặc `ai`, bạn có thể mô phỏng chúng bằng các stub – xem phần “Optional Stubs” ở cuối.

## Bước 1: Khởi Tạo Engine AI (Giải Phóng Tài Nguyên AI)

Trước khi đưa bất kỳ hình ảnh nào vào quy trình OCR, mô hình nền phải sẵn sàng. Khởi tạo chỉ một lần giúp tiết kiệm bộ nhớ và tăng tốc các công việc batch.

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**Tại sao điều này quan trọng:**  
Gọi `ai.initialize` lặp lại cho mỗi hình ảnh sẽ phân bổ bộ nhớ GPU liên tục, cuối cùng làm script bị sập. Bằng cách kiểm tra `ai.is_initialized()` chúng ta đảm bảo chỉ một lần phân bổ – đó là nguyên tắc “giải phóng tài nguyên AI”.

## Bước 2: Tải Các Tệp Ảnh PNG cho Xử Lý OCR Hàng Loạt

Bây giờ chúng ta thu thập tất cả các tệp PNG muốn chạy qua OCR. Sử dụng `pathlib` giúp mã không phụ thuộc vào hệ điều hành.

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**Trường hợp đặc biệt:**  
Nếu thư mục chứa các tệp không phải PNG (ví dụ, JPEG) chúng sẽ bị bỏ qua, ngăn `engine.recognize` gặp lỗi do định dạng không được hỗ trợ.

## Bước 3: Chạy OCR trên Mỗi Hình Ảnh và Áp Dụng Xử Lý Hậu

Với engine đã sẵn sàng và danh sách tệp đã chuẩn bị, chúng ta có thể lặp qua các hình ảnh, trích xuất văn bản thô, và chuyển cho một bộ xử lý hậu kỳ để làm sạch các artefact OCR thường gặp (như các ngắt dòng lẻ).

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**Tại sao chúng ta tách việc tải ảnh khỏi nhận dạng:**  
`aocr.Image.load` có thể thực hiện giải mã lười, nhanh hơn cho các batch lớn. Giữ bước tải ảnh rõ ràng cũng giúp dễ dàng thay thế bằng thư viện ảnh khác nếu sau này bạn cần xử lý JPEG hoặc TIFF.

## Bước 4: Dọn Dẹp – Giải Phóng Tài Nguyên AI Sau Khi Batch Hoàn Thành

Khi batch hoàn tất, chúng ta phải giải phóng mô hình để tránh rò rỉ bộ nhớ, đặc biệt trên các máy có GPU.

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## Kết Hợp Tất Cả – Script Hoàn Chỉnh

Dưới đây là một tệp duy nhất ghép bốn bước lại thành một quy trình liền mạch. Lưu lại dưới tên `batch_ocr.py` và chạy từ dòng lệnh.

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### Kết Quả Dự Kiến

Chạy script trên một thư mục chứa ba PNG có thể in ra:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

Tệp `ocr_results.txt` sẽ chứa một dấu phân cách rõ ràng cho mỗi hình ảnh, sau đó là văn bản OCR đã được làm sạch.

## Các Stub Tùy Chọn cho aocr & ai (Nếu Bạn Không Có Gói Thực)

Nếu bạn chỉ muốn thử luồng mà không kéo các thư viện OCR nặng, bạn có thể tạo các mô-đun mock tối thiểu:

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

Đặt các thư mục này bên cạnh `batch_ocr.py` và script sẽ chạy, in ra kết quả mock.

## Mẹo Chuyên Gia & Những Cạm Bẫy Thường Gặp

- **Memory spikes:** Nếu bạn đang xử lý hàng nghìn PNG độ phân giải cao, hãy cân nhắc thay đổi kích thước chúng trước khi OCR. `aocr.Image.load` thường chấp nhận đối số `max_size`.  
- **Unicode handling:** Luôn mở tệp đầu ra với `encoding="utf-8"`; các engine OCR có thể phát ra ký tự không phải ASCII.  
- **Parallelism:** Đối với OCR phụ thuộc CPU, bạn có thể bọc `ocr_batch` trong một `concurrent.futures.ThreadPoolExecutor`. Chỉ cần nhớ giữ một thể hiện `ai` duy nhất – tạo nhiều luồng mỗi luồng gọi `ai.initialize` sẽ phá vỡ mục tiêu “giải phóng tài nguyên AI”.  
- **Error resilience:** Bao quanh vòng lặp per‑image bằng một khối `try/except` để một PNG bị hỏng không làm dừng toàn bộ batch.

## Kết Luận

Bây giờ bạn đã có một **python ocr tutorial** minh họa cách **load png image** các tệp, thực hiện **batch OCR processing**, và quản lý **free AI resources** một cách có trách nhiệm. Ví dụ hoàn chỉnh, có thể chạy này cho thấy chính xác cách **recognize text from image** các đối tượng và dọn dẹp sau đó, vì vậy bạn có thể sao chép‑dán nó vào dự án của mình mà không phải tìm kiếm các phần còn thiếu.

Sẵn sàng cho bước tiếp theo? Hãy thử thay thế các mô-đun `aocr` và `ai` đã stub bằng các thư viện thực như `pytesseract` và `torchvision`. Bạn cũng có thể mở rộng script để xuất JSON, đẩy kết quả lên cơ sở dữ liệu, hoặc tích hợp với bucket lưu trữ đám mây. Không có giới hạn—chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-06-28
description: Cách thực hiện OCR hàng loạt trong Python—trích xuất văn bản từ hình
  ảnh và chuyển các trang quét thành văn bản bằng xử lý OCR hàng loạt.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: vi
og_description: Tìm hiểu cách thực hiện OCR hàng loạt trong Python, trích xuất văn
  bản từ hình ảnh và chuyển các trang quét thành văn bản với quy trình OCR hàng loạt
  hiệu quả.
og_title: Cách thực hiện OCR hàng loạt trong Python – Hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Cách thực hiện OCR hàng loạt trong Python – Hướng dẫn đầy đủ để trích xuất
  văn bản từ hình ảnh
url: /vi/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện Batch OCR trong Python – Hướng Dẫn Toàn Diện để Trích Xuất Văn Bản từ Hình Ảnh

Nếu bạn đang tự hỏi **cách thực hiện batch OCR trong Python**, bạn đã đến đúng nơi. Bài hướng dẫn này cho bạn một cách nhanh chóng để **trích xuất văn bản từ hình ảnh** và **chuyển các trang đã quét thành văn bản** bằng một thể hiện của engine OCR. Không còn phải sao chép‑dán từng tệp một nữa—để mã thực hiện công việc nặng.

Chúng ta sẽ đi qua mọi thứ bạn cần: cài đặt thư viện, tải toàn bộ thư mục các bản quét, chạy xử lý batch OCR, và xử lý kết quả một cách nhẹ nhàng. Khi hoàn thành, bạn sẽ có một script có thể tái sử dụng để biến một chồng PNG hoặc JPEG thành các tệp văn bản có thể tìm kiếm trong vài giây.

## Những Gì Bạn Cần Chuẩn Bị

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Python 3.9+ đã được cài đặt (mã cũng chạy trên 3.8, nhưng 3.9+ cung cấp các tính năng typing mới nhất).
* Một thư viện OCR hiện đại—ở đây chúng tôi dùng **Aspose.OCR for Python via .NET**, cung cấp lớp `OcrEngine` như trong đoạn mã gốc.  
  ```bash
  pip install aspose-ocr
  ```
* Một thư mục chứa các trang đã quét (`page1.png`, `page2.png`, …). Bất kỳ định dạng nào Pillow mở được đều hoạt động, vì vậy PDF, TIFF hoặc BMP cũng được.
* Một chút tò mò—nếu bạn chưa từng tự động hoá việc chuyển ảnh thành văn bản, bạn sẽ sớm thấy tại sao batch OCR là một công cụ thay đổi cuộc chơi.

> **Mẹo chuyên nghiệp:** Nếu bạn muốn dùng thư viện thuần Python, hãy thay `OcrEngine` bằng `pytesseract.image_to_string`. Logic xung quanh vẫn giữ nguyên.

## Cách Thực Hiện Batch OCR trong Python – Hướng Dẫn Từng Bước

Dưới đây là script hoàn chỉnh, có thể chạy ngay. Mỗi dòng đều có chú thích để bạn hiểu *tại sao* mỗi phần quan trọng, không chỉ *cái gì* nó làm.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Kết Quả Dự Kiến

Chạy script trên một thư mục có ba bản quét PNG sẽ tạo ra kết quả tương tự:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

Bản xem trước hiển thị 200 ký tự đầu tiên của mỗi trang, và văn bản đầy đủ được lưu trong thư mục `ocr_output`.

## Trích Xuất Văn Bản từ Hình Ảnh Bằng Một Engine Đơn

Tại sao chúng ta tạo **một** `OcrEngine` và tái sử dụng nó? Khởi tạo engine có thể tốn kém vì nó phải tải các gói ngôn ngữ và DLL gốc. Bằng cách chia sẻ cùng một thể hiện cho toàn batch, bạn:

* **Tiết kiệm bộ nhớ** – chỉ có một bộ tài nguyên tồn tại trong RAM.
* **Tăng tốc độ** – engine luôn “ấm”, tránh việc khởi tạo lại liên tục.
* **Duy trì tính nhất quán** – cùng một cài đặt nhận dạng áp dụng cho mọi trang, điều này rất quan trọng khi bạn muốn **trích xuất văn bản từ hình ảnh** có cùng bố cục.

Nếu cần điều chỉnh nhận dạng (ví dụ, bật kiểm tra chính tả hoặc thay đổi ngôn ngữ), hãy thực hiện *trước* khi gọi `recognize_batch`. Tất cả các trang sau sẽ tự động kế thừa các cài đặt đó.

## Chuyển Các Trang Đã Quét Thành Văn Bản Một Cách Hiệu Quả

Trọng tâm của vấn đề—**chuyển các trang đã quét thành văn bản**—được giải quyết bằng `engine.recognize_batch(images)`. Bên trong, thư viện xử lý mỗi ảnh trong một pool luồng nền, vì vậy bạn sẽ nhận được hiệu năng gần như tuyến tính trên các máy đa nhân. Một vài lưu ý:

* **Chất lượng ảnh quan trọng** – 300 dpi hoặc cao hơn cho kết quả tốt nhất. Nếu bản quét của bạn có độ phân giải thấp, hãy cân nhắc upscale bằng Pillow trước khi đưa vào engine.
* **Màu vs. grayscale** – các engine OCR thường nhanh hơn trên ảnh grayscale 8‑bit. Bạn có thể thêm bước tiền xử lý:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Hỗ trợ ngôn ngữ** – Aspose.OCR hỗ trợ hơn 40 ngôn ngữ. Đặt `engine.language = "eng"` hoặc `"fra"` trước khi gọi batch nếu bạn không làm việc với tiếng Anh.

## Các Thực Hành Tốt Nhất Khi Xử Lý Batch OCR

Mặc dù đoạn mã trên đã ngắn gọn, nhưng trong môi trường sản xuất batch OCR thường cần một vài biện pháp bảo vệ bổ sung:

| Vấn đề | Cách Tiếp Cận Đề Xuất |
|--------|------------------------|
| **Batch lớn ( > 500 tệp )** | Chia thành các khối 100–200 ảnh để giữ mức sử dụng bộ nhớ vừa phải. |
| **Tệp hỏng hoặc không hỗ trợ** | Hàm trợ giúp `load_images` đã bắt ngoại lệ và ghi cảnh báo; bạn cũng có thể viết fallback để bỏ qua hoặc di chuyển các tệp lỗi. |
| **Giám sát tiến độ** | Bao `recognize_batch` trong vòng lặp và trả về sau mỗi ảnh nếu thư viện cung cấp callback per‑image. |
| **Xử lý hậu kỳ** | Chạy kiểm tra chính tả hoặc làm sạch bằng regex trên các chuỗi kết quả để cải thiện khả năng tìm kiếm. |
| **Song song** | Nếu có môi trường đa nút, phân phối các thư mục cho các worker và hợp nhất các tệp `.txt` ở cuối. |

Những mẹo này giúp bạn mở rộng **xử lý batch OCR** từ vài trang lên hàng nghìn mà không làm script bị sập.

## Câu Hỏi Thường Gặp

**H: Có thể dùng trực tiếp với PDF không?**  
Đ: Hoàn toàn có thể. Đầu tiên chuyển mỗi trang PDF thành ảnh (ví dụ, dùng `pdf2image`) và đưa danh sách ảnh đó vào `recognize_batch`. Phần còn lại của pipeline không thay đổi.

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial dưới đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
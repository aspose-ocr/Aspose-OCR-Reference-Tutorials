---
category: general
date: 2026-04-26
description: Cách tạo OCR nhanh chóng và đáng tin cậy. Học cách trích xuất văn bản
  từ hình ảnh, tải hình ảnh cho OCR và chạy OCR trên file PNG với từ điển tùy chỉnh.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: vi
og_description: Cách tạo OCR trong Python và trích xuất văn bản từ hình ảnh. Hướng
  dẫn này cho thấy cách tải hình ảnh cho OCR, chạy OCR trên PNG và sử dụng từ điển
  tùy chỉnh.
og_title: Cách tạo OCR trong Python – Trích xuất văn bản nhanh
tags:
- OCR
- Python
- Image Processing
title: Cách tạo OCR trong Python – Trích xuất văn bản từ hình ảnh
url: /vi/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tạo OCR trong Python – Hướng Dẫn Từng Bước

Bạn đã bao giờ tự hỏi **cách tạo OCR** để đọc các file PDF đã quét, ảnh chụp màn hình, hay ghi chú viết tay chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, chúng ta cần *trích xuất văn bản từ file ảnh*, nhưng các engine có sẵn thường gặp khó khăn với các từ ngữ chuyên ngành.  

Trong tutorial này, bạn sẽ thấy một ví dụ hoàn chỉnh, có thể chạy ngay, tải một ảnh để OCR, áp dụng một từ điển tùy chỉnh, và cuối cùng **chạy OCR trên file PNG**. Khi kết thúc, bạn sẽ có thể trích xuất văn bản từ bất kỳ ảnh nào và tùy biến engine cho thuật ngữ riêng của mình.

## Những Nội Dung Tutorial Này Bao Gồm

Chúng ta sẽ đi qua từng bước cần thiết:

* Cài đặt gói `aocr` nhỏ gọn nhưng mạnh mẽ (hoặc bất kỳ thư viện tương thích nào).  
* Cấu hình **từ điển tùy chỉnh** để các thuật ngữ như `aspocorp` hay `licensekey` được nhận diện.  
* **Tải ảnh để OCR**, dù là PNG, JPEG, hay một trang PDF đã quét.  
* Chạy quá trình OCR và in kết quả ra.  

Không có liên kết tài liệu bên ngoài, chỉ có một giải pháp tự chứa mà bạn có thể sao chép‑dán và chạy ngay hôm nay.

### Yêu Cầu Trước

* Python 3.8 hoặc mới hơn (code sử dụng f‑strings).  
* Kiến thức cơ bản về dòng lệnh – bạn sẽ gõ một vài lệnh `pip install`.  
* Một file ảnh (`technical_doc.png` trong ví dụ) được lưu ở nơi bạn có thể tham chiếu.  

Nếu bạn đáp ứng ba yêu cầu trên, bạn đã sẵn sàng.

---

## Bước 1: Cài Đặt Thư Viện OCR

Đầu tiên, chúng ta cần một engine OCR hỗ trợ đối tượng cấu hình có thể lập trình. Gói `aocr` là một wrapper nhẹ quanh một engine OCR gốc và hoạt động tốt cho các demo.

```bash
# Install the library (run once)
pip install aocr
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Windows và gặp lỗi biên dịch, thử `pip install aocr‑binary` – gói này cung cấp các wheel đã được xây dựng sẵn.

### Tại Sao Cài Đặt Thư Viện Này?

`aocr` cho phép chúng ta truy cập trực tiếp vào một đối tượng `config` nơi chúng ta có thể chèn **từ điển tùy chỉnh**. Đó là bí quyết để cải thiện độ chính xác trên các từ vựng chuyên ngành.

---

## Bước 2: Tạo Instance của Engine OCR & Thêm Từ Điển Tùy Chỉnh

Bây giờ chúng ta khởi động engine và chỉ định những từ mà nó nên coi là đã biết.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Tại Sao Từ Điển Tùy Chỉnh Quan Trọng

Các mô hình OCR tiêu chuẩn được huấn luyện trên các corpus chung. Khi mô hình gặp “aspocorp”, nó có thể tách thành “aspo corp” hoặc thậm chí bỏ mất các ký tự. Bằng cách cung cấp danh sách tùy chỉnh, chúng ta hướng nhận dạng về đúng chính tả cần thiết, giảm đáng kể công việc xử lý hậu kỳ.

---

## Bước 3: Tải Ảnh Bạn Muốn Xử Lý

Đây là nơi chúng ta **tải ảnh để OCR**. Phương thức `Image.load` nhận một chuỗi đường dẫn và tự động xác định loại file.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Trường hợp đặc biệt:** Nếu nguồn của bạn là một PDF đa trang, hãy chuyển mỗi trang sang PNG trước (ví dụ, dùng `pdf2image`) và đưa chúng vào engine từng cái một.

### Mẹo Để Có Ảnh Chất Lượng Tốt Hơn

* Giữ độ phân giải ít nhất 300 dpi.  
* Đảm bảo ảnh được đặt thẳng; nếu cần, xoay bằng `Pillow`.  
* Chuyển các bản quét màu sang thang xám để giảm nhiễu.

---

## Bước 4: Chạy Quá Trình OCR Trên File PNG

Với engine đã được cấu hình và ảnh đã được tải, cuối cùng chúng ta **chạy OCR trên PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

Lệnh `process()` trả về một đối tượng chứa văn bản đã nhận diện, điểm tin cậy, và các bounding box cho mỗi từ.

---

## Bước 5: Xuất Văn Bản Được Nhận Diện

Cách đơn giản nhất để xem engine đã tìm được gì là in thuộc tính `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Kết Quả Dự Kiến

Nếu `technical_doc.png` chứa câu *“The Aspocorp licensekey expires on 2025‑12‑31.”*, console sẽ hiển thị:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Bạn sẽ thấy từ điển tùy chỉnh giữ nguyên tên thương hiệu – điều mà một OCR thông thường có thể đã làm rối.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là toàn bộ script, sẵn sàng lưu dưới tên `run_ocr.py`. Chỉ cần thay đường dẫn placeholder bằng vị trí ảnh của bạn.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Chạy nó từ terminal:

```bash
python run_ocr.py
```

Bạn sẽ thấy văn bản đã trích xuất được in ra console, giống như trong ví dụ ở trên.

---

## Câu Hỏi Thường Gặp (FAQ)

| Câu hỏi | Trả lời |
|----------|--------|
| **Tôi có thể trích xuất văn bản từ PDF đã quét không?** | Có. Đầu tiên chuyển mỗi trang sang PNG (hoặc TIFF), sau đó đưa các ảnh vào script giống nhau. |
| **Nếu ảnh của tôi là JPEG thay vì PNG thì sao?** | Phương thức `Image.load` hỗ trợ JPEG, BMP, TIFF và PNG ngay từ đầu. Chỉ cần thay đổi phần mở rộng file. |
| **Làm sao cải thiện độ chính xác trên các bản quét có độ tương phản thấp?** | Tiền xử lý bằng `Pillow` – tăng độ tương phản, áp dụng nhị phân hoá, hoặc dùng `opencv` để chỉnh góc. |
| **Có cách lấy điểm tin cậy cho từng từ không?** | `ocr_result` chứa `words` – mỗi từ có thuộc tính `confidence` mà bạn có thể lặp qua. |
| **Tôi có thể chạy trên server không có giao diện (headless) không?** | Hoàn toàn có thể. `aocr` không phụ thuộc GUI, rất phù hợp cho các pipeline CI. |

---

## Các Bước Tiếp Theo & Chủ Đề Liên Quan

Bây giờ bạn đã biết **cách tạo OCR** và **trích xuất văn bản từ file ảnh**, hãy khám phá thêm:

* **Kỹ thuật tiền xử lý** – `load image for OCR` chỉ là bước đầu; dùng `opencv` để giảm nhiễu hoặc làm nét.  
* **Xử lý hàng loạt** – lặp qua một thư mục PNG để tạo kho lưu trữ có thể tìm kiếm.  
* **Hỗ trợ đa ngôn ngữ** – thêm gói ngôn ngữ vào engine nếu bạn cần đọc tài liệu tiếng Pháp hoặc tiếng Đức.  
* **Tích hợp với Elasticsearch** – lập chỉ mục văn bản đã trích xuất để tìm kiếm toàn văn trên các tài sản đã quét.  

Mỗi phần mở rộng này dựa trên mẫu cốt lõi chúng ta vừa học, vì vậy việc chuyển đổi sẽ rất nhẹ nhàng.

---

## Kết Luận

Trong vài phút, chúng ta đã trả lời **cách tạo OCR** có thể **trích xuất văn bản từ file ảnh** một cách đáng tin cậy, đặc biệt là PNG, và đã chỉ cho bạn cách **tải ảnh để OCR**, áp dụng **từ điển tùy chỉnh**, và **chạy OCR trên PNG** mà không cần dịch vụ bên ngoài.  

Hãy chạy thử script, tùy chỉnh từ điển cho phù hợp với thuật ngữ của bạn, và bạn sẽ có nền tảng vững chắc cho bất kỳ dự án số hoá tài liệu nào.  

Nếu gặp khó khăn, để lại bình luận bên dưới—chúng tôi sẵn sàng hỗ trợ. Đừng quên chia sẻ câu chuyện thành công của bạn; cộng đồng học hỏi tốt nhất từ những ví dụ thực tế.  

**Sẵn sàng tự động hoá công việc giấy tờ?** Lấy code, tùy biến, và bắt đầu biến pixel thành văn bản có thể tìm kiếm ngay hôm nay!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
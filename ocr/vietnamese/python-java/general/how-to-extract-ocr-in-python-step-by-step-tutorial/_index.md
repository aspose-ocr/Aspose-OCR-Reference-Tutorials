---
category: general
date: 2026-04-26
description: Cách trích xuất OCR từ hình ảnh bằng Python – một ví dụ OCR bằng Python
  cho thấy cách tải hình ảnh để OCR và trích xuất văn bản từ biên lai.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: vi
og_description: cách trích xuất OCR từ hình ảnh bằng Python. Tìm hiểu ví dụ OCR bằng
  Python, tải hình ảnh để OCR và trích xuất văn bản từ biên lai chỉ trong vài phút.
og_title: cách trích xuất OCR trong Python – Hướng dẫn đầy đủ
tags:
- OCR
- Python
- Image Processing
title: Cách trích xuất OCR trong Python – Hướng dẫn từng bước
url: /vi/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách trích xuất OCR trong Python – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **cách trích xuất OCR** từ một biên lai mờ hoặc một hoá đơn đã quét chưa? Bạn không phải là người duy nhất—các nhà phát triển thường gặp khó khăn khi cần văn bản sạch, có thể đọc được bằng máy từ hình ảnh. Tin tốt là gì? Chỉ với vài dòng Python, bạn có thể biến một bức ảnh biên lai thành văn bản có độ tin cậy cao và có thể tìm kiếm.

Trong hướng dẫn này, chúng ta sẽ đi qua một **python ocr example** minh họa **cách tải ảnh cho OCR**, chạy engine, và chỉ giữ lại các ký tự đạt ngưỡng độ tin cậy 85 %. Khi kết thúc, bạn sẽ có thể **trích xuất văn bản từ biên lai** mà không cần lục lọi tài liệu hay đoán các tham số API.

## Những gì bạn cần

- Python 3.9 hoặc mới hơn (cú pháp chúng tôi dùng hoạt động trên 3.8+)
- Gói `aocr` (hoặc bất kỳ thư viện OCR nào cung cấp lớp `OcrEngine`). Cài đặt bằng:
```bash
pip install aocr
```
- Một hình ảnh biên lai mẫu (`receipt.png`) đặt trong thư mục bạn có thể tham chiếu.
- Một trình soạn thảo văn bản hoặc IDE—VS Code, PyCharm, hoặc thậm chí một notebook đơn giản cũng được.

Chỉ vậy thôi. Không có khung công tác nặng, không có dịch vụ bên ngoài, chỉ Python thuần.

![Kết quả OCR độ tin cậy cao – cách trích xuất OCR từ biên lai](/images/ocr-high-confidence.png)

*Văn bản thay thế hình ảnh: cách trích xuất OCR từ biên lai bằng Python OCR*

## Bước 1 – Tạo thể hiện OCR Engine (cách trích xuất OCR)

Điều đầu tiên chúng ta làm là khởi tạo một OCR engine. Hãy nghĩ nó như bộ não sẽ đọc các pixel cho chúng ta.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Tại sao?** Khởi tạo `OcrEngine` cung cấp cho bạn một đối tượng cấu hình mới. Bạn có thể sau này điều chỉnh mô hình ngôn ngữ, cài đặt DPI, hoặc các bước tiền xử lý—tất cả mà không cần chạm vào vòng lặp xử lý chính.

## Bước 2 – Tải ảnh cho OCR

Tiếp theo chúng ta chỉ engine tới hình ảnh muốn phân tích. Đây là nơi từ khóa **load image for ocr** xuất hiện.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Mẹo chuyên nghiệp:** Nếu hình ảnh của bạn nằm trong thư mục khác, hãy sử dụng `os.path.join` để xây dựng đường dẫn độc lập nền tảng.

**Tại sao phải tải ảnh theo cách này?** Trợ giúp `Image.load` đọc tệp vào định dạng mà engine hiểu, tự động xử lý các định dạng phổ biến (PNG, JPEG, TIFF). Bỏ qua bước này hoặc cung cấp raw bytes sẽ gây ra lỗi `ValueError`.

## Bước 3 – Chạy quy trình OCR

Bây giờ chúng ta thực sự chạy OCR. Phương thức `process` trả về một đối tượng kết quả phong phú chứa các ký hiệu đã nhận dạng, điểm tin cậy và hộp bao.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**`ocr_result` chứa gì?** Trong hầu hết các thư viện, nó bao gồm:

- `text`: chuỗi gộp thô.
- `symbol_confidences`: danh sách các tuple `(char, confidence)`.
- `boxes`: tọa độ cho mỗi ký tự (hữu ích cho việc gỡ lỗi trực quan).

Có quyền truy cập vào độ tin cậy từng ký tự là cần thiết cho bước tiếp theo.

## Bước 4 – Giữ lại chỉ các ký tự độ tin cậy cao (≥ 85 %)

Biên lai thường có vết bẩn, in mờ hoặc nhiễu nền. Bằng cách lọc bỏ các ký tự độ tin cậy thấp, chúng ta cải thiện đáng kể việc phân tích sau này.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Tại sao 85 %?** Theo kinh nghiệm, ngưỡng khoảng 0.85 cân bằng độ thu hồi và độ chính xác cho hầu hết các biên lai in. Nếu bạn thấy thiếu số, hạ ngưỡng; nếu nhận được ký tự rác, tăng ngưỡng.

## Bước 5 – Xuất văn bản đã trích xuất độ tin cậy cao

Cuối cùng, chúng ta in (hoặc lưu) chuỗi đã được làm sạch. Đây là cốt lõi của quy trình **extract text from receipt** của chúng ta.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

Kết quả đầu ra thường trông như sau:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

Bây giờ bạn có thể đưa chuỗi này vào trình ghi CSV, cơ sở dữ liệu, hoặc bất kỳ pipeline phân tích nào tiếp theo.

## Toàn bộ script sẵn sàng chạy

Dưới đây là đoạn mã hoàn chỉnh mà bạn có thể sao chép‑dán vào `ocr_receipt.py` và chạy ngay lập tức.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Lưu file, đảm bảo `receipt.png` tồn tại, và thực thi:

```bash
python ocr_receipt.py
```

Bạn sẽ thấy văn bản biên lai đã được làm sạch được in ra console.

## Các trường hợp đặc biệt & Kịch bản nếu‑xảy‑ra

| Tình huống | Giải pháp đề xuất |
|-----------|----------------|
| **Độ tin cậy rất thấp trên toàn bộ** | Tiền xử lý ảnh: tăng độ tương phản, chuyển sang thang xám, hoặc áp dụng bộ lọc giảm nhiễu (`cv2.GaussianBlur`). |
| **Ký tự không phải Latin** | Cung cấp mô hình ngôn ngữ cho `OcrEngine` (ví dụ, `ocr_engine.language = "spa"` cho tiếng Tây Ban Nha). |
| **Nhiều biên lai trong một ảnh** | Chạy OCR trên toàn bộ ảnh, sau đó tách kết quả bằng biểu thức chính quy phát hiện `\\n\\n+` (dòng ngắt đôi). |
| **Cần cả văn bản OCR thô** | Giữ `ocr_result.text` cùng với phiên bản đã lọc để gỡ lỗi. |

Những biến thể này đảm bảo kiến thức **how to use OCR** của bạn mở rộng vượt ra ngoài trường hợp đơn giản nhất.

## Những sai lầm thường gặp (Và cách tránh chúng)

- **Quên cài đặt thư viện** – `pip install aocr` phải thành công trước khi bạn import.
- **Sử dụng dấu phân tách đường dẫn sai** trên Windows (`\\` vs `/`). Dùng `os.path.join`.
- **Cố định ngưỡng độ tin cậy** mà không thử nghiệm – luôn thực hiện kiểm tra nhanh trực quan trên một vài biên lai trước.
- **Bỏ qua chuẩn hoá Unicode** – một số biên lai chứa ký tự gạch đặc biệt; chạy `unicodedata.normalize('NFKC', text)` nếu bạn dự định lưu kết quả.

## Các bước tiếp theo – Vượt ra ngoài nền tảng cơ bản

Bây giờ bạn đã biết **cách trích xuất OCR** dữ liệu từ một biên lai duy nhất, bạn có thể muốn:

1. **Xử lý hàng loạt một thư mục các biên lai** – lặp qua tất cả các file PNG/JPG và ghi mỗi kết quả vào CSV.
2. **Tích hợp với cơ sở dữ liệu** – lưu `high_confidence_text` trong SQLite để tra cứu nhanh.
3. **Áp dụng phân tích ngôn ngữ tự nhiên** – dùng regex hoặc `dateutil` để lấy ngày, tổng tiền và số thuế.
4. **Thử nghiệm các thư viện thay thế** – `pytesseract`, `easyocr`, hoặc các dịch vụ đám mây (Google Vision, Azure OCR) nếu bạn cần hỗ trợ đa ngôn ngữ hoặc độ chính xác cao hơn.

Mỗi chủ đề này tự nhiên bao gồm các từ khóa phụ của chúng ta: *python ocr example*, *extract text from receipt*, *load image for ocr*, và *how to use OCR*.

## Kết luận

Chúng ta vừa đi qua một **python ocr example** hoàn chỉnh, cho thấy **cách trích xuất OCR** văn bản từ ảnh biên lai, lọc bỏ các ký tự độ tin cậy thấp, và xuất kết quả sạch. Các bước đơn giản, mã tự chứa, và cách tiếp cận đủ linh hoạt để áp dụng cho các dự án lớn hơn.

Hãy thử với các biên lai của bạn, điều chỉnh ngưỡng độ tin cậy, và sau đó mở rộng lên xử lý hàng loạt. Nếu gặp những bất thường—như logo mờ hoặc phông chữ lạ—hãy nhớ các mẹo trường hợp đặc biệt ở trên. Chúc lập trình vui vẻ, và chúc các pipeline OCR của bạn luôn chính xác!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
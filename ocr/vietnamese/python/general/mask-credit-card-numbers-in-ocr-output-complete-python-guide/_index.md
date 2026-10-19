---
category: general
date: 2026-04-26
description: Ẩn nhanh số thẻ tín dụng bằng xử lý hậu kỳ AsposeAI OCR. Tìm hiểu về
  tuân thủ PCI, ẩn bằng biểu thức chính quy và làm sạch dữ liệu trong hướng dẫn từng
  bước.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: vi
og_description: Ẩn số thẻ tín dụng trong kết quả OCR bằng AsposeAI. Hướng dẫn này
  bao gồm tuân thủ PCI, việc ẩn bằng biểu thức chính quy và làm sạch dữ liệu.
og_title: Ẩn Số Thẻ Tín Dụng – Hướng Dẫn Xử Lý Hậu Kỳ OCR Python Toàn Diện
tags:
- OCR
- Python
- security
title: Che giấu số thẻ tín dụng trong đầu ra OCR – Hướng dẫn Python toàn diện
url: /vi/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ẩn Số Thẻ Tín Dụng – Hướng Dẫn Python Đầy Đủ

Bạn đã bao giờ cần **ẩn số thẻ tín dụng** trong văn bản lấy trực tiếp từ công cụ OCR chưa? Bạn không phải là người duy nhất. Trong các ngành được quy định, việc để lộ toàn bộ PAN (Primary Account Number) có thể khiến bạn gặp rắc rối với các kiểm toán viên tuân thủ PCI. Tin tốt? Với vài dòng Python và hook post‑processing của AsposeAI, bạn có thể tự động ẩn tám chữ số ở giữa và giữ an toàn.

Trong tutorial này chúng ta sẽ đi qua một kịch bản thực tế: chạy OCR trên ảnh biên lai, sau đó áp dụng một hàm **OCR post‑processing** tùy chỉnh để làm sạch bất kỳ dữ liệu PCI nào. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng, có thể chèn vào bất kỳ workflow nào của AsposeAI, cùng với một vài mẹo thực tiễn để xử lý các trường hợp biên và mở rộng giải pháp.

## Những Điều Bạn Sẽ Học

- Cách đăng ký một post‑processor tùy chỉnh với **AsposeAI**.  
- Tại sao cách **regular expression masking** vừa nhanh vừa đáng tin cậy.  
- Những kiến thức cơ bản về **PCI compliance** liên quan đến việc làm sạch dữ liệu.  
- Cách mở rộng mẫu để hỗ trợ nhiều định dạng thẻ hoặc số quốc tế.  
- Kết quả mong đợi và cách xác minh rằng việc ẩn đã hoạt động.

> **Prerequisites** – Bạn nên có môi trường Python 3 hoạt động, gói Aspose.AI for OCR đã được cài đặt (`pip install aspose-ocr`), và một ảnh mẫu (ví dụ: `receipt.png`) chứa số thẻ tín dụng. Không cần dịch vụ bên ngoài nào khác.

---

## Bước 1: Định Nghĩa Post‑Processor Ẩn Số Thẻ Tín Dụng

Trọng tâm của giải pháp nằm trong một hàm nhỏ nhận kết quả OCR, chạy quy trình **regular expression masking**, và trả về văn bản đã được làm sạch.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Tại sao cách này hoạt động:**  
- Biểu thức chính quy `(\d{4})\d{8}(\d{4})` khớp chính xác 16 chữ số liên tiếp, định dạng phổ biến cho Visa, MasterCard và nhiều loại thẻ khác.  
- Bằng cách bắt nhóm bốn chữ số đầu và bốn chữ số cuối (`\1` và `\2`), chúng ta giữ lại đủ thông tin để gỡ lỗi trong khi tuân thủ các quy tắc **PCI compliance** cấm lưu trữ toàn bộ PAN.  
- Thay thế `\1****\2` ẩn tám chữ số nhạy cảm ở giữa, biến `1234567812345678` thành `1234****5678`.

> **Pro tip:** Nếu bạn cần hỗ trợ số American Express 15 chữ số, hãy thêm một mẫu thứ hai như `r'(\d{4})\d{6}(\d{5})'` và thực hiện cả hai thay thế tuần tự.

---

## Bước 2: Khởi Tạo Engine AsposeAI

Trước khi chúng ta có thể gắn post‑processor, chúng ta cần một thể hiện của engine OCR. AsposeAI gói sẵn mô hình OCR và một API đơn giản cho việc xử lý tùy chỉnh.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Tại sao khởi tạo ở đây?**  
Tạo đối tượng `AsposeAI` một lần và tái sử dụng nó cho nhiều ảnh giảm thiểu chi phí. Engine cũng lưu cache các mô hình ngôn ngữ, giúp tăng tốc các lần gọi tiếp theo—rất hữu ích khi bạn quét hàng loạt biên lai.

---

## Bước 3: Đăng Ký Hàm Ẩn Tùy Chỉnh

AsposeAI cung cấp phương thức `set_post_processor` cho phép bạn gắn bất kỳ callable nào. Chúng ta truyền hàm `mask_pci` cùng với một dictionary cài đặt tùy chọn (hiện tại để trống).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Đi gì đang diễn ra phía sau?**  
Khi bạn sau này gọi `run_postprocessor`, AsposeAI sẽ chuyển kết quả OCR thô cho `mask_pci`. Hàm nhận một đối tượng nhẹ (`data`) chứa văn bản đã nhận dạng, và bạn trả về một chuỗi mới. Thiết kế này giữ nguyên phần OCR gốc trong khi cho phép bạn thực thi các chính sách **data sanitization** ở một nơi duy nhất.

---

## Bước 4: Chạy OCR Trên Ảnh Biên Lai

Bây giờ engine đã biết cách làm sạch đầu ra, chúng ta đưa một ảnh vào. Đối với tutorial này, chúng ta giả sử bạn đã có một đối tượng `engine` được cấu hình với ngôn ngữ và độ phân giải phù hợp.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** Nếu bạn chưa có đối tượng được cấu hình trước, bạn có thể tạo một cái mới bằng:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

Lệnh `recognize_image` trả về một đối tượng có thuộc tính `text` chứa chuỗi thô, chưa được ẩn.

---

## Bước 5: Áp Dụng Post‑Processor Đã Đăng Ký

Với dữ liệu OCR thô trong tay, chúng ta chuyển nó cho instance AI. Engine tự động chạy hàm `mask_pci` mà chúng ta đã đăng ký trước đó.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Tại sao dùng `run_postprocessor` thay vì gọi hàm trực tiếp?**  
Việc này giữ cho workflow nhất quán, đặc biệt khi bạn có nhiều post‑processor (ví dụ: kiểm tra chính tả, phát hiện ngôn ngữ). AsposeAI xếp chúng theo thứ tự bạn đăng ký, đảm bảo kết quả xác định.

---

## Bước 6: Xác Minh Kết Quả Đã Được Làm Sạch

Cuối cùng, hãy in ra văn bản đã được làm sạch và xác nhận rằng bất kỳ số thẻ tín dụng nào đã được ẩn đúng cách.

```python
print(final_result.text)
```

**Kết quả mong đợi** (đoạn trích):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Nếu biên lai không chứa số thẻ, văn bản sẽ không thay đổi—không có gì để ẩn, không có gì để lo lắng.

---

## Xử Lý Các Trường Hợp Biên và Các Biến Thể Thông Thường

### Nhiều Số Thẻ Trong Một Tài Liệu
Nếu biên lai có hơn một PAN (ví dụ: thẻ khách hàng cộng với thẻ thanh toán), biểu thức chính quy sẽ chạy toàn cục, tự động ẩn tất cả các khớp. Không cần thêm mã nào.

### Định Dạng Không Tiêu Chuẩn
Đôi khi OCR chèn khoảng trắng hoặc dấu gạch ngang (`1234 5678 1234 5678` hoặc `1234-5678-1234-5678`). Mở rộng mẫu để bỏ qua các ký tự này:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Phần `[ -]?` được thêm vào cho phép có hoặc không có khoảng trắng hoặc dấu gạch ngang giữa các khối chữ số.

### Thẻ Quốc Tế
Đối với PAN 19 chữ số được sử dụng ở một số khu vực, bạn có thể mở rộng mẫu:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Chỉ cần nhớ rằng **PCI compliance** vẫn yêu cầu ẩn các chữ số ở giữa, bất kể độ dài.

### Ghi Log Các Giá Trị Đã Ẩn (Tùy Chọn)
Nếu bạn cần lưu vết audit, hãy truyền một cờ qua `custom_settings` và điều chỉnh hàm:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Sau đó đăng ký với:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Chạy script này trên một biên lai chứa `4111111111111111` sẽ tạo ra:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Đó là toàn bộ pipeline—từ OCR thô đến **data sanitization**—được gói gọn trong vài dòng Python sạch sẽ.

---

## Kết Luận

Chúng tôi vừa cho bạn thấy cách **ẩn số thẻ tín dụng** trong kết quả OCR bằng hook post‑processing của AsposeAI, một quy trình regular‑expression ngắn gọn, và một vài mẹo thực hành tốt cho **PCI compliance**. Giải pháp hoàn toàn tự chứa, hoạt động với bất kỳ ảnh nào mà engine OCR có thể đọc, và có thể mở rộng để bao phủ các định dạng thẻ phức tạp hơn hoặc yêu cầu ghi log.

Sẵn sàng bước tiếp? Hãy thử kết hợp hàm ẩn này với một quy trình **chèn vào cơ sở dữ liệu** chỉ lưu lại bốn chữ số cuối để tham chiếu, hoặc tích hợp một **batch processor** quét toàn bộ thư mục biên lai qua đêm. Bạn cũng có thể khám phá các tác vụ **OCR post‑processing** khác như chuẩn hoá địa chỉ hoặc phát hiện ngôn ngữ—mỗi tác vụ đều theo cùng một mẫu chúng ta đã dùng ở đây.

Có câu hỏi về các trường hợp biên, hiệu năng, hoặc cách điều chỉnh mã cho thư viện OCR khác? Để lại bình luận bên dưới, và chúng ta sẽ tiếp tục thảo luận. Chúc lập trình vui vẻ và luôn bảo mật!

![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-18
description: Hướng dẫn cơ bản OCR bằng Python cho thấy cách chuyển đổi TIFF sang văn
  bản, tải OCR cho hình ảnh, thiết lập các lớp GPU và sửa các số 0 đầu tiên bằng Aspose
  AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: vi
og_description: Hướng dẫn OCR cơ bản bằng Python sẽ hướng dẫn bạn chuyển đổi các tệp
  TIFF thành văn bản sạch, tải ảnh, thiết lập các lớp GPU và sửa các số 0 đầu tiên.
og_title: OCR cơ bản Python – chuyển đổi TIFF sang văn bản
tags:
- OCR
- Python
- AI
- Aspose
title: OCR cơ bản Python – chuyển đổi TIFF thành văn bản
url: /vi/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Chuyển đổi TIFF sang Văn bản với Xử lý hậu AI

Bạn đang tìm cách thực hiện **basic ocr python** trên các tài liệu đã quét? Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn chuyển đổi tệp TIFF thành văn bản sạch, có thể tìm kiếm được bằng Aspose OCR và một bộ xử lý hậu AI.  

Nếu bạn từng gặp khó khăn khi **chuyển đổi TIFF sang văn bản** vì kết quả thô đầy lỗi chính tả hoặc ký tự lạ, bạn không đơn độc. Chúng tôi cũng sẽ chỉ cho bạn cách **load image OCR**, điều chỉnh engine để **set GPU layers**, và thậm chí **sửa các số 0 đầu** thường xuất hiện trong số hóa đơn.

## Những gì bạn sẽ học

- Cách khởi tạo engine Aspose OCR cho tài liệu in.  
- Các bước chính xác để **load image OCR** từ tệp TIFF và lấy văn bản thô.  
- Cấu hình mô hình AI, tự động tải xuống, và **set GPU layers** để tăng tốc suy luận.  
- Thêm kiểm tra chính tả tích hợp và một hàm tùy chỉnh **sửa các số 0 đầu**.  
- Làm sạch kết quả OCR và giải phóng tài nguyên một cách đúng đắn.  

Kết thúc tutorial này, bạn sẽ có một script Python duy nhất, có thể tái sử dụng, chuyển bất kỳ tệp TIFF nào thành văn bản đã được tinh chỉnh, có thể tìm kiếm—không cần sao chép‑dán thủ công.

### Yêu cầu trước

- Python 3.8+ đã được cài đặt trên máy của bạn.  
- Gói `aspose-ocr` (`pip install aspose-ocr`).  
- Tùy chọn: một GPU có ít nhất 4 GB VRAM nếu bạn muốn **set GPU layers**; nếu không, code sẽ tự động chuyển sang CPU.

---

## basic ocr python – load image và nhận dạng văn bản

Điều đầu tiên chúng ta cần làm là **load image OCR** để engine có thể đọc các pixel. `OcrEngine` của Aspose hỗ trợ nhiều định dạng, nhưng ở đây chúng ta tập trung vào TIFF vì đây là định dạng phổ biến nhất cho hóa đơn đã quét.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang làm việc với các tệp TIFF đa trang, Aspose sẽ tự động xử lý từng trang theo thứ tự, vì vậy bạn không cần vòng lặp bổ sung.

Bây giờ hình ảnh đã được tải, hãy chạy một lượt nhận dạng cơ bản.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Bạn sẽ thấy kết quả giống như:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Bạn có nhận thấy *các số 0* trước các chữ cái không? Đó là một hiện tượng thường gặp của OCR mà chúng ta sẽ làm sạch sau.

![luồng công việc basic ocr python](/images/ocr-workflow.png "sơ đồ luồng công việc basic ocr python")

---

## Bước 2: Chuyển đổi TIFF sang văn bản – chuẩn bị bộ xử lý hậu AI

Kết quả OCR thô có ích, nhưng hầu hết các pipeline sản xuất cần một phiên bản đã được tinh chỉnh. Aspose cung cấp một wrapper `AsposeAI` có thể tải mô hình từ Hugging Face, chạy trên GPU và tự động áp dụng kiểm tra chính tả.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Tại sao `set GPU layers` lại quan trọng

Tham số `gpu_layers` chỉ cho mô hình GGUF cơ bản biết bao nhiêu lớp transformer sẽ được giữ trên GPU. Nhiều lớp hơn = suy luận nhanh hơn nhưng tiêu tốn VRAM nhiều hơn. Nếu bạn dùng một laptop cấu hình trung bình, hãy giảm giá trị xuống `10` hoặc bỏ hoàn toàn để chạy trên CPU.

---

## Bước 3: Áp dụng kiểm tra chính tả và **sửa các số 0 đầu**

Aspose AI đi kèm với một bộ kiểm tra chính tả tích hợp, bắt hầu hết các lỗi tiếng Anh. Tuy nhiên, các sửa chữa đặc thù ngành—như chuyển một `0` đầu thành `O` cho mã hóa đơn—cần một bộ xử lý hậu tùy chỉnh.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Lý do hoạt động:** Biểu thức chính quy tìm kiếm một ranh giới từ (`\b`), một số 0, rồi đúng ba ký tự in hoa. Sau đó thay thế số 0 bằng chữ “O”. Bạn có thể mở rộng mẫu này cho các trường hợp khác (ví dụ, `0[0-9]{2}` cho các số bị đọc sai).

---

## Bước 4: Làm sạch kết quả OCR bằng bộ xử lý hậu AI

Bây giờ chúng ta kết hợp mọi thứ: chuỗi thô từ **basic ocr python**, kiểm tra chính tả, và hàm sửa số 0. Phương thức `run_postprocessor` trả về một phiên bản đã được làm sạch, sẵn sàng cho các hệ thống downstream.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Kết quả điển hình sau khi qua bộ xử lý hậu:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Bạn sẽ thấy số 0 đầu đã chuyển thành `O`, và các lỗi chính tả phổ biến đã được sửa. Văn bản giờ đã phù hợp để lập chỉ mục trong công cụ tìm kiếm hoặc đưa vào pipeline trích xuất dữ liệu.

---

## Bước 5: Giải phóng tài nguyên AI – giữ GPU luôn sẵn sàng

Nếu bạn chạy nhiều công việc OCR trong một dịch vụ lâu dài, nên giải phóng bộ nhớ GPU của mô hình khi hoàn tất.

```python
ocr_ai.free_resources()
```

Bỏ qua bước này có thể gây ra lỗi “out‑of‑memory” trong các lần gọi tiếp theo, đặc biệt khi **set GPU layers** ở mức cao.

---

## Các biến thể tùy chọn & Trường hợp đặc biệt

| Tình huống | Cần thay đổi |
|-----------|--------------|
| **Tài liệu viết tay** | Dùng `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` thay vì `PRINTED`. |
| **Không có GPU** | Đặt `gpu_layers=0` hoặc bỏ tham số; mô hình sẽ chạy trên CPU (chậm hơn nhưng an toàn). |
| **Ngôn ngữ khác** | Thay ID repo Hugging Face bằng mô hình ngôn ngữ tương ứng, ví dụ `microsoft/Florence-2-base`. |
| **Xử lý hàng loạt** | Bao bọc các bước trong vòng lặp `for file in glob("*.tif"):` và lưu kết quả vào danh sách hoặc CSV. |
| **Mẫu số 0 phức tạp hơn** | Mở rộng hàm `invoice_fix` với các regex bổ sung, như `r"\b0+([A-Z]{2,})\b"` cho nhiều số 0 đầu. |

---

## Kết luận

Chúng ta vừa hoàn thành một pipeline **basic ocr python** để tải TIFF, trích xuất văn bản thô, và sau đó làm sạch bằng mô hình AI trong khi **set GPU layers** để tối ưu hiệu năng. Bộ xử lý hậu tùy chỉnh cho thấy cách **sửa các số 0 đầu**, một chi tiết nhỏ nhưng thường bị bỏ qua và có thể gây lỗi cho các phân tích downstream.

Hãy thử nghiệm: thay đổi mức quantization (`float16` cho độ chính xác cao hơn), thay bộ kiểm tra chính tả bằng từ điển chuyên ngành, hoặc xâu chuỗi nhiều hàm sửa tùy chỉnh. Quy trình vẫn giữ nguyên—load, recognize, configure AI, post‑process, và clean up.

**Các bước tiếp theo** bạn có thể khám phá:

- Tích hợp kết quả đã làm sạch vào cơ sở dữ liệu hoặc chỉ mục Elasticsearch.  
- Áp dụng cùng cách tiếp cận để **chuyển đổi TIFF sang văn bản** cho các PDF đa ngôn ngữ.  
- Thêm giao diện UI với Flask hoặc FastAPI để người dùng không chuyên có thể tải lên tệp và nhận văn bản đã làm sạch ngay lập tức.  

Chúc lập trình vui vẻ, và hy vọng kết quả OCR của bạn luôn sắc nét, không còn số 0 dư!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
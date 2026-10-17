---
category: general
date: 2026-04-26
description: Cách xử lý hậu kỳ kết quả OCR và trích xuất văn bản kèm tọa độ. Tìm hiểu
  giải pháp từng bước sử dụng đầu ra có cấu trúc và chỉnh sửa bằng AI.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: vi
og_description: Cách xử lý hậu kỳ kết quả OCR và trích xuất văn bản kèm tọa độ. Hãy
  theo dõi hướng dẫn toàn diện này để có quy trình làm việc đáng tin cậy.
og_title: Cách Xử Lý Hậu OCR – Hướng Dẫn Toàn Diện
tags:
- OCR
- Python
- AI
- Text Extraction
title: Cách xử lý hậu kỳ OCR – Trích xuất văn bản kèm tọa độ trong Python
url: /vi/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tiền Xử Lý OCR – Trích Xuất Văn Bản Kèm Tọa Độ trong Python

Bạn đã bao giờ cần **cách tiền xử lý OCR** vì kết quả thô bị nhiễu hoặc lệch không? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế—quét hoá đơn, số hoá biên lai, hoặc thậm chí tăng cường trải nghiệm AR—động cơ OCR cung cấp cho bạn các từ thô, nhưng bạn vẫn phải làm sạch chúng và theo dõi vị trí của mỗi từ trên trang. Đó là lúc chế độ đầu ra có cấu trúc kết hợp với bộ xử lý hậu xử lý dựa trên AI tỏa sáng.

Trong tutorial này chúng ta sẽ đi qua một pipeline Python hoàn chỉnh, có thể chạy được, **trích xuất văn bản kèm tọa độ** từ một hình ảnh, thực hiện bước sửa lỗi dựa trên AI, và in ra mỗi từ cùng với vị trí `(x, y)` của nó. Không thiếu import, không có các shortcut mơ hồ “xem tài liệu”—chỉ có một giải pháp tự chứa mà bạn có thể đưa vào dự án ngay hôm nay.

> **Pro tip:** Nếu bạn đang dùng một thư viện OCR khác, hãy tìm chế độ “structured” hoặc “layout”; các khái niệm vẫn giữ nguyên.

---

## Yêu Cầu Trước

| Yêu Cầu | Tại sao quan trọng |
|-------------|----------------|
| Python 3.9+ | Cú pháp hiện đại và hỗ trợ type hints |
| Thư viện `ocr` hỗ trợ `OutputMode.STRUCTURED` (ví dụ: `myocr` giả tưởng) | Cần thiết cho dữ liệu bounding‑box |
| Module hậu xử lý AI (có thể là OpenAI, HuggingFace, hoặc mô hình tùy chỉnh) | Cải thiện độ chính xác sau OCR |
| Tập tin ảnh (`input.png`) trong thư mục làm việc | Nguồn dữ liệu sẽ được đọc |

Nếu bất kỳ mục nào trên nghe lạ, chỉ cần cài đặt các gói placeholder bằng `pip install myocr ai‑postproc`. Đoạn code dưới đây cũng bao gồm các stub dự phòng để bạn có thể thử luồng mà không cần các thư viện thực.

---

## Bước 1: Kích Hoạt Chế Độ Đầu Ra Có Cấu Trúc cho Động Cơ OCR  

Điều đầu tiên chúng ta làm là yêu cầu động cơ OCR cung cấp nhiều hơn chỉ văn bản thuần. Đầu ra có cấu trúc trả về mỗi từ cùng với bounding box và điểm tin cậy, điều này thiết yếu cho **trích xuất văn bản kèm tọa độ** sau này.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Lý do quan trọng:* Nếu không bật chế độ có cấu trúc, bạn sẽ chỉ nhận được một chuỗi dài, và sẽ mất thông tin không gian cần thiết để phủ lên văn bản trên ảnh hoặc đưa vào phân tích layout downstream.

---

## Bước 2: Nhận Dạng Hình Ảnh và Ghi Lại Các Từ, Hộp, và Độ Tin Cậy  

Bây giờ chúng ta đưa ảnh vào engine. Kết quả là một đối tượng chứa danh sách các đối tượng từ, mỗi đối tượng cung cấp `text`, `x`, `y`, `width`, `height`, và `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Trường hợp đặc biệt:* Nếu ảnh rỗng hoặc không đọc được, `structured_result.words` sẽ là một danh sách rỗng. Thực hành tốt là kiểm tra và xử lý một cách nhẹ nhàng.

---

## Bước 3: Chạy Xử Lý Hậu Xử Lý Dựa Trên AI Trong Khi Bảo Quản Vị Trí  

Ngay cả các engine OCR tốt nhất cũng có thể sai—ví dụ “O” vs. “0” hoặc thiếu dấu. Một mô hình AI được huấn luyện trên văn bản chuyên ngành có thể sửa những lỗi này. Điều then chốt là chúng ta giữ nguyên tọa độ gốc để bố cục không gian vẫn nguyên vẹn.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Tại sao chúng ta bảo quản tọa độ:* Nhiều tác vụ downstream (ví dụ: tạo PDF, gán nhãn AR) phụ thuộc vào vị trí chính xác. AI chỉ thay đổi trường `text`, để nguyên `x`, `y`, `width`, `height`.

---

## Bước 4: Lặp Qua Các Từ Đã Được Sửa và Hiển Thị Văn Bản Cùng Tọa Độ  

Cuối cùng, chúng ta duyệt qua các từ đã được sửa và in ra mỗi từ cùng với góc trên‑trái `(x, y)`. Điều này đáp ứng mục tiêu **trích xuất văn bản kèm tọa độ**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Kết quả mong đợi (ví dụ):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Mỗi dòng hiển thị từ đã sửa và vị trí chính xác trên ảnh gốc.

---

## Ví Dụ Hoàn Chỉnh Hoạt Động  

Dưới đây là một script duy nhất gắn kết mọi thứ lại với nhau. Bạn có thể sao chép‑dán, điều chỉnh các câu lệnh import cho phù hợp với thư viện thực tế của mình, và chạy trực tiếp.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**Chạy script**

```bash
python ocr_postprocess_demo.py
```

Nếu bạn đã cài đặt các thư viện thực, script sẽ xử lý `input.png` của bạn. Nếu không, triển khai stub cho phép bạn thấy luồng và kết quả dự kiến mà không cần phụ thuộc bên ngoài.

---

## Câu Hỏi Thường Gặp (FAQ)

| Câu Hỏi | Trả Lời |
|----------|--------|
| *Does this work with Tesseract?* | Tesseract không cung cấp chế độ có cấu trúc ngay lập tức, nhưng các wrapper như `pytesseract.image_to_data` trả về bounding boxes mà bạn có thể đưa vào cùng một bộ hậu xử lý AI. |
| *What if I need the bottom‑right corner instead of top‑left?* | Mỗi đối tượng từ cũng cung cấp `width` và `height`. Tính `x2 = x + width` và `y2 = y + height` để có góc đối diện. |
| *Can I batch‑process multiple images?* | Chắc chắn. Đặt các bước trong một vòng lặp `for image_path in Path("folder").glob("*.png"):` và thu thập kết quả cho mỗi file. |
| *How do I choose an AI model for correction?* | Đối với văn bản chung, một GPT‑2 nhỏ được fine‑tuned trên lỗi OCR hoạt động tốt. Đối với dữ liệu chuyên ngành (ví dụ: toa thuốc y tế), hãy huấn luyện mô hình sequence‑to‑sequence trên dữ liệu cặp nhiễu‑sạch. |
| *Is the confidence score useful after AI correction?* | Bạn vẫn có thể giữ điểm tin cậy gốc để debug, nhưng AI có thể trả về điểm tin cậy riêng nếu mô hình hỗ trợ. |

---

## Trường Hợp Cạnh & Thực Hành Tốt Nhất  

1. **Empty or corrupted images** – luôn xác minh `structured_result.words` không rỗng trước khi tiếp tục.  
2. **Non‑Latin scripts** – đảm bảo engine OCR được cấu hình cho ngôn ngữ mục tiêu; bộ hậu xử lý AI phải được huấn luyện trên cùng một script.  
3. **Performance** – việc sửa lỗi bằng AI có thể tốn kém. Lưu cache kết quả nếu bạn sẽ tái sử dụng cùng một ảnh, hoặc chạy bước AI bất đồng bộ.  
4. **Coordinate system** – các thư viện OCR có thể dùng các gốc khác nhau (top‑left vs. bottom‑left). Điều chỉnh cho phù hợp khi phủ lên PDF hoặc canvas.  

---

## Kết Luận  

Bạn đã có một công thức toàn diện, đầu‑cuối‑đầu cho **cách tiền xử lý OCR** và **trích xuất văn bản kèm tọa độ** một cách đáng tin cậy. Bằng cách bật đầu ra có cấu trúc, đưa kết quả qua lớp sửa lỗi AI, và bảo quản các bounding box gốc, bạn có thể biến các bản quét OCR nhiễu thành văn bản sạch, có không gian, sẵn sàng cho các tác vụ downstream như tạo PDF, tự động nhập dữ liệu, hoặc phủ lên thực tế tăng cường.

Sẵn sàng cho bước tiếp theo? Hãy thử thay thế AI stub bằng một lời gọi OpenAI `gpt‑4o‑mini`, hoặc tích hợp pipeline vào FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
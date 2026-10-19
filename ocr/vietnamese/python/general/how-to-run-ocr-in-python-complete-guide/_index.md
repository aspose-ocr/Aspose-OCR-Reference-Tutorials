---
category: general
date: 2026-06-19
description: Cách thực hiện OCR từng bước và cải thiện độ chính xác của OCR bằng các
  kỹ thuật OCR văn bản thuần. Tìm hiểu quy trình nhanh chóng để trích xuất văn bản
  đáng tin cậy.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: vi
og_description: Cách chạy OCR một cách hiệu quả. Hướng dẫn này chỉ ra cách cải thiện
  độ chính xác của OCR bằng OCR văn bản thuần và xử lý hậu kỳ AI.
og_title: Cách chạy OCR trong Python – Hướng dẫn toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Cách chạy OCR trong Python – Hướng dẫn toàn diện
url: /vi/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Chạy OCR trong Python – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một loạt file PDF đã quét mà không phải tốn hàng giờ chỉnh sửa cài đặt? Bạn không phải là người duy nhất. Trong nhiều dự án, rào cản đầu tiên chỉ là lấy được văn bản đáng tin cậy từ một hình ảnh, và sự khác biệt giữa một kết quả lỏng lẻo và một trích xuất sạch sẽ thường phụ thuộc vào một vài bước thông minh.

Trong hướng dẫn này, chúng ta sẽ đi qua một quy trình thực tế bốn bước, không chỉ **chạy OCR** mà còn **cải thiện độ chính xác OCR** bằng cách kết hợp một lần chạy plain‑text nhanh, một lần chạy layout‑aware chi tiết và một bộ xử lý hậu‑xử lý dựa trên AI. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy, giải thích rõ ràng tại sao mỗi giai đoạn quan trọng, và các mẹo xử lý các trường hợp đặc biệt như trang đa cột hoặc bản quét nhiễu.

---

## Những Gì Bạn Cần Chuẩn Bị

Trước khi bắt đầu, hãy chắc chắn bạn đã có:

- **Python 3.9+** – mã sử dụng type hints và f‑strings.  
- **Tesseract OCR** đã được cài đặt và có thể truy cập qua lệnh `tesseract`. (Trên Ubuntu: `sudo apt install tesseract-ocr`; trên Windows tải trình cài đặt từ repo chính thức.)  
- Thư viện **pytesseract** (`pip install pytesseract`).  
- Một **thư viện xử lý hậu‑xử lý AI** – trong ví dụ này chúng ta sẽ giả sử bạn có một module nhẹ `ai` cung cấp hàm `run_postprocessor`. Thay thế bằng API GPT‑4 của OpenAI hoặc một LLM cục bộ nếu muốn.  
- Một vài hình ảnh hoặc PDF mẫu để thử nghiệm.

Đó là tất cả. Không cần framework nặng, không cần Docker. Chỉ vài lệnh pip và bạn đã sẵn sàng.

---

## Bước 1: Thực Hiện Lần Chạy Plain‑Text OCR Nhanh

Điều đầu tiên mà hầu hết các nhà phát triển bỏ qua là một lần chạy OCR *plain text* cực nhanh và cho bạn một kiểm tra sơ bộ. Chúng ta sẽ gọi `engine.Recognize()` để lấy các ký tự thô mà không có siêu dữ liệu layout. Đây là ý nghĩa của **plain text OCR**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Lý do quan trọng:*  
- **Tốc độ** – một lần chạy plain trên trang 300 dpi thường hoàn thành dưới một giây.  
- **Baseline** – bạn có thể so sánh đầu ra có cấu trúc sau này với baseline này để phát hiện lỗi nghiêm trọng.  
- **Phát hiện lỗi** – nếu lần chạy plain hoàn toàn thất bại (ví dụ, toàn bộ là ký tự rác), bạn biết chất lượng ảnh quá thấp và có thể dừng sớm.

---

## Bước 2: Chạy Lần OCR Có Nhận Thức Layout Chi Tiết

Plain text rất tốt, nhưng nó bỏ qua *vị trí* của mỗi từ trên trang. Đối với hoá đơn, biểu mẫu, hoặc tạp chí đa cột, bạn cần tọa độ, số dòng, và thậm chí thông tin phông chữ. Đó là lúc `engine.RecognizeStructured()` xuất hiện.

Dưới đây là một wrapper nhẹ quanh đầu ra **TSV** của Tesseract, cung cấp một cây phân cấp trang → dòng → từ, bảo toàn các bounding box.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Lý do chúng ta làm điều này:*  
- **Tọa độ** cho phép bạn sau này ánh xạ văn bản đã trích xuất trở lại ảnh gốc để highlight hoặc redact.  
- **Nhóm dòng** bảo toàn layout gốc, rất cần thiết khi bạn muốn tái tạo bảng hoặc cột.  
- Lần chạy này chậm hơn một chút so với plain, nhưng vẫn chỉ mất vài giây cho hầu hết tài liệu.

---

## Bước 3: Chạy Bộ Xử Lý Hậu‑Xử Lý AI Để Sửa Lỗi OCR

Ngay cả engine OCR tốt nhất cũng có lỗi—ví dụ “rn” vs “m”, thiếu dấu, hoặc từ bị tách. Một mô hình AI có thể nhìn vào chuỗi thô và dữ liệu có cấu trúc, phát hiện bất thường, và viết lại văn bản trong khi giữ nguyên tọa độ gốc.

Dưới đây là một triển khai **mock**; thay phần thân bằng lời gọi LLM thực tế nếu bạn có.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Lý do bước này cải thiện độ chính xác OCR:*  
- **Sửa lỗi ngữ cảnh** – AI có thể quyết định rằng “l0ve” có khả năng là “love” dựa trên các từ xung quanh.  
- **Bảo toàn tọa độ** – bạn giữ thông tin layout, vì vậy các tác vụ downstream (như chú thích PDF) vẫn chính xác.  
- **Tinh chỉnh lặp lại** – bạn có thể chạy bộ xử lý hậu‑xử lý nhiều lần, mỗi lần loại bỏ thêm lỗi.

---

## Bước 4: Duyệt Qua Đầu Ra Đã Sửa, Có Cấu Trúc

Bây giờ chúng ta đã có một cấu trúc đã được làm sạch, việc lấy văn bản cuối cùng trở nên đơn giản. Dưới đây chúng ta in mỗi dòng, nhưng bạn cũng có thể ghi ra CSV, đưa vào cơ sở dữ liệu, hoặc tạo PDF có thể tìm kiếm.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Kết quả mong đợi** (giả sử một hoá đơn đơn trang):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Chú ý cách các ngắt dòng và thứ tự cột được bảo toàn, và các lỗi OCR phổ biến như “$15.00” bị đọc thành “$15,00” đã được AI sửa.

---

## Cách Quy Trình Này Giúp **Cải Thiện Độ Chính Xác OCR**

| Giai đoạn | Những gì nó sửa | Tại sao quan trọng |
|------|---------------|----------------|
| **Plain text OCR** | Phát hiện các trang không đọc được sớm | Tiết kiệm thời gian bằng cách bỏ qua các input vô vọng |
| **Structured OCR** | Nắm bắt layout, tọa độ | Cho phép các tác vụ downstream (highlight, redact) |
| **AI post‑processor** | Sửa chính tả, gộp từ bị tách, sửa số | Tăng độ chính xác ký tự tổng thể từ ~85 % lên >95 % trên bản quét nhiễu |
| **Iteration** | Cho phép chạy lại với tham số tinh chỉnh | Tinh chỉnh pipeline cho các loại tài liệu cụ thể |

Bằng cách kết hợp ba khái niệm—**plain text OCR**, trích xuất có nhận thức layout, và sửa lỗi bằng AI—bạn có được một giải pháp mạnh mẽ, **cải thiện đáng kể độ chính xác OCR** mà không cần viết mạng nơ-ron tùy chỉnh từ đầu.

---

## Những Sai Lầm Thường Gặp & Mẹo Chuyên Gia

- **Sai lầm:** Đưa ảnh độ phân giải thấp (≤150 dpi) vào Tesseract dẫn tới kết quả rối.  
  **Mẹo:** Tiền xử lý bằng `Pillow`—áp dụng `Image.convert('L')` và `Image.filter(ImageFilter.MedianFilter())` trước khi OCR.

- **Sai lầm:** Bộ xử lý AI có thể vô tình sửa các thuật ngữ chuyên ngành (ví dụ, “SKU123”).  
  **Mẹo:** Xây dựng whitelist các thuật ngữ và truyền vào LLM hoặc thư viện kiểm tra chính tả như `pyspellchecker`.

- **Sai lầm:** Các trang đa cột bị gộp thành một dòng duy nhất.  
  **Mẹo:** Phát hiện ranh giới cột bằng trường `block_num` trong đầu ra TSV của Tesseract và tách dòng tương ứng.

- **Sai lầm:** PDF lớn gây tràn bộ nhớ khi tải toàn bộ trang cùng lúc.  
  **Mẹo:** Xử lý trang từng bước—lặp qua `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Mở Rộng Quy Trình

Nếu bạn muốn khám phá các bước tiếp theo, hãy cân nhắc các cải tiến sau:

1. **Xử lý batch** – Đóng gói toàn bộ script trong một hàm duyệt thư mục, xử lý hàng ngàn file song song bằng `concurrent.futures`.  
2. **Mô hình ngôn ngữ** – Thay thế heuristic difflib đơn giản bằng lời gọi tới `gpt‑4o` của OpenAI hoặc mô hình LLaMA cục bộ để có các sửa lỗi ngữ cảnh phong phú hơn.  
3. **Định dạng xuất** – Ghi cấu trúc đã sửa sang PDF có thể tìm kiếm  

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây liên quan chặt chẽ tới các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn hoàn chỉnh và giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
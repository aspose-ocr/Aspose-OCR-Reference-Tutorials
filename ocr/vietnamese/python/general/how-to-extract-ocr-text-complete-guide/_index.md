---
category: general
date: 2026-02-22
description: Tìm hiểu cách trích xuất văn bản OCR và nâng cao độ chính xác OCR bằng
  xử lý hậu kỳ AI. Dễ dàng làm sạch văn bản OCR trong Python với ví dụ hướng dẫn từng
  bước.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: vi
og_description: Khám phá cách trích xuất văn bản OCR, cải thiện độ chính xác OCR và
  làm sạch văn bản OCR bằng quy trình Python đơn giản với xử lý hậu kỳ AI.
og_title: Cách trích xuất văn bản OCR – Hướng dẫn từng bước
tags:
- OCR
- AI
- Python
title: Cách Trích Xuất Văn Bản OCR – Hướng Dẫn Toàn Diện
url: /vi/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Trích Xuất Văn Bản OCR – Hướng Dẫn Lập Trình Đầy Đủ

Bạn đã bao giờ tự hỏi **cách trích xuất OCR** từ một tài liệu đã quét mà không bị rơi vào đống lỗi chính tả và các dòng bị cắt ngắt không? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, đầu ra thô từ một công cụ OCR trông giống như một đoạn văn lộn xộn, và việc làm sạch nó cảm giác như một công việc vất vả.  

Tin tốt là gì? Bằng cách theo dõi hướng dẫn này, bạn sẽ thấy một cách thực tế để lấy dữ liệu OCR có cấu trúc, chạy một bộ xử lý hậu AI, và có được **văn bản OCR sạch** sẵn sàng cho các phân tích tiếp theo. Chúng tôi cũng sẽ đề cập đến các kỹ thuật để **cải thiện độ chính xác OCR** sao cho kết quả đáng tin cậy ngay từ lần đầu.

Trong vài phút tới, chúng ta sẽ bao quát mọi thứ bạn cần: các thư viện bắt buộc, một script có thể chạy được đầy đủ, và các mẹo tránh những bẫy thường gặp. Không có các lối tắt mơ hồ “xem tài liệu” — chỉ có một giải pháp hoàn chỉnh, tự chứa mà bạn có thể sao chép‑dán và chạy.

## Những Gì Bạn Cần

- Python 3.9+ (code sử dụng type hints nhưng vẫn hoạt động trên các phiên bản 3.x cũ hơn)
- Một engine OCR có thể trả về kết quả có cấu trúc (ví dụ: Tesseract qua `pytesseract` với flag `--psm 1`, hoặc một API thương mại cung cấp siêu dữ liệu block/dòng)
- Một mô hình xử lý hậu AI – trong ví dụ này chúng ta sẽ mô phỏng bằng một hàm đơn giản, nhưng bạn có thể thay bằng `gpt‑4o-mini` của OpenAI, Claude, hoặc bất kỳ LLM nào nhận văn bản và trả về kết quả đã được làm sạch
- Một vài hình ảnh mẫu (PNG/JPG) để thử nghiệm

Nếu bạn đã có sẵn những thứ này, hãy cùng bắt đầu.

## Cách Trích Xuất OCR – Lấy Dữ Liệu Ban Đầu

Bước đầu tiên là gọi engine OCR và yêu cầu nó trả về một **đại diện có cấu trúc** thay vì một chuỗi đơn giản. Kết quả có cấu trúc bảo tồn ranh giới block, line và word, giúp việc làm sạch sau này dễ dàng hơn rất nhiều.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **Tại sao điều này quan trọng:** Bằng cách bảo tồn các block và line, chúng ta tránh phải đoán nơi bắt đầu các đoạn văn. Hàm `recognize_structured` cung cấp cho chúng ta một cây phân cấp sạch sẽ mà sau này có thể đưa vào mô hình AI.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Chạy đoạn mã sẽ in ra dòng đầu tiên chính xác như engine OCR đã nhận, thường chứa các nhận dạng sai như “0cr” thay vì “OCR”.

## Cải Thiện Độ Chính Xác OCR Với Xử Lý Hậu AI

Bây giờ chúng ta đã có đầu ra có cấu trúc thô, hãy đưa nó cho một bộ xử lý hậu AI. Mục tiêu là **cải thiện độ chính xác OCR** bằng cách sửa các lỗi phổ biến, chuẩn hoá dấu câu, và thậm chí tái phân đoạn các dòng khi cần.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **Mẹo chuyên nghiệp:** Nếu bạn không có đăng ký LLM, bạn có thể thay thế lời gọi bằng một transformer cục bộ (ví dụ: `sentence‑transformers` + mô hình chỉnh sửa đã được fine‑tuned) hoặc thậm chí một cách tiếp cận dựa trên quy tắc. Ý tưởng chính là AI sẽ nhìn thấy mỗi dòng một cách độc lập, thường đủ để **làm sạch văn bản OCR**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Bây giờ bạn sẽ thấy một câu đã được làm sạch hơn rất nhiều — các lỗi chính tả đã được thay thế, khoảng trắng thừa đã bị loại bỏ, và dấu câu đã được sửa.

## Làm Sạch Văn Bản OCR Để Có Kết Quả Tốt Hơn

Ngay cả sau khi AI đã chỉnh sửa, bạn có thể muốn thực hiện một bước làm sạch cuối cùng: loại bỏ các ký tự không phải ASCII, thống nhất các ngắt dòng, và gộp nhiều khoảng trắng lại. Lần xử lý bổ sung này đảm bảo đầu ra sẵn sàng cho các tác vụ downstream như NLP hoặc nhập dữ liệu vào cơ sở dữ liệu.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

Hàm `final_cleanup` sẽ cho bạn một chuỗi thuần túy mà bạn có thể đưa trực tiếp vào một chỉ mục tìm kiếm, một mô hình ngôn ngữ, hoặc xuất ra CSV. Vì chúng ta đã giữ lại ranh giới block, cấu trúc đoạn văn vẫn được bảo toàn.

## Các Trường Hợp Cạnh & Kịch Bản “Nếu”

- **Bố cục đa cột:** Nếu nguồn của bạn có các cột, engine OCR có thể xen kẽ các dòng. Bạn có thể phát hiện tọa độ cột từ đầu ra TSV và sắp xếp lại các dòng trước khi gửi chúng cho AI.
- **Kịch bản không phải Latin:** Đối với các ngôn ngữ như Trung Quốc hoặc Ả Rập, hãy chuyển prompt của LLM để yêu cầu sửa lỗi theo ngôn ngữ cụ thể, hoặc sử dụng mô hình đã được fine‑tuned cho script đó.
- **Tài liệu lớn:** Gửi từng dòng một có thể chậm. Hãy gộp các dòng (ví dụ: 10 dòng mỗi yêu cầu) và để LLM trả về danh sách các dòng đã được làm sạch. Đừng quên tuân thủ giới hạn token.
- **Thiếu block:** Một số engine OCR chỉ trả về danh sách phẳng các từ. Trong trường hợp này, bạn có thể tái tạo các dòng bằng cách nhóm các từ có giá trị `line_num` tương tự.

## Ví Dụ Hoàn Chỉnh Hoạt Động

Kết hợp mọi thứ lại, dưới đây là một file duy nhất bạn có thể chạy từ đầu đến cuối. Thay các placeholder bằng API key và đường dẫn hình ảnh của bạn.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
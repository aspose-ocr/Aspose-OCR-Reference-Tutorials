---
category: general
date: 2026-06-06
description: Cách OCR PDF bằng Python, trích xuất văn bản từ PDF, chuyển đổi văn bản
  PDF đã quét và thay đổi ngôn ngữ OCR chỉ trong vài dòng mã.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: vi
og_description: 'Cách OCR PDF bằng Python: hướng dẫn thực tế chỉ cho bạn cách trích
  xuất văn bản từ PDF, chuyển đổi văn bản PDF đã quét và thay đổi ngôn ngữ OCR một
  cách dễ dàng.'
og_title: Cách OCR PDF trong Python – Hướng dẫn lập trình đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Cách OCR PDF trong Python – Hướng dẫn chi tiết từng bước
url: /vi/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách OCR PDF trong Python – Hướng Dẫn Chi Tiết Từng Bước

Bạn đã bao giờ tự hỏi **cách OCR PDF** mà không phải trả tiền cho các công cụ SaaS đắt đỏ chưa? Bạn không phải là người duy nhất. Dù bạn đang số hoá những cuốn sách cũ, trích xuất dữ liệu từ hoá đơn, hay chỉ cần văn bản có thể tìm kiếm từ một báo cáo đã quét, việc thành thạo OCR PDF trong Python có thể tiết kiệm cho bạn hàng giờ sao chép thủ công.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ ngắn gọn, hoạt động được, mà **trích xuất văn bản từ PDF**, cho bạn thấy cách **chuyển đổi văn bản PDF đã quét** thành các chuỗi có thể chỉnh sửa, và thậm chí minh họa cách **thay đổi ngôn ngữ OCR** nếu tài liệu của bạn không phải tiếng Anh. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng và chèn vào bất kỳ dự án nào.

## Yêu Cầu Trước & Cài Đặt

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- Python 3.8+ đã được cài đặt (mã chạy được trên 3.9, 3.10 và các phiên bản mới hơn)
- Gói `ocr` cung cấp lớp `OcrEngine` (bạn có thể cài đặt bằng `pip install ocr-lib` – thay thế bằng tên gói thực tế bạn dùng)
- Một file PDF mà bạn muốn xử lý; trong demo chúng ta sẽ dùng `high_res_book.pdf` đặt trong thư mục `YOUR_DIRECTORY`

Nếu bạn đang dùng môi trường ảo (được khuyến nghị mạnh mẽ), hãy kích hoạt nó trước:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Mẹo chuyên nghiệp:** Giữ các file PDF của bạn trong một thư mục `data/` riêng biệt để tránh các rắc rối liên quan đến đường dẫn sau này.

## Bước 1: Tạo Một Instance của OCR Engine (Cách OCR PDF – Khởi Tạo)

Điều đầu tiên bạn cần làm khi muốn **thực hiện OCR trên PDF** là khởi tạo engine. Hãy nghĩ engine như bộ não sẽ đọc từng trang, giải mã các glyph, và trả lại cho bạn văn bản thuần.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Tại sao điều này quan trọng: nếu không có engine, bạn sẽ không có ngữ cảnh cho các cài đặt ngôn ngữ, tùy chọn render, hay xử lý PDF. Đối tượng `OcrEngine` chứa tất cả các mặc định này và cho phép bạn điều chỉnh chúng sau này.

## Bước 2: Đặt Ngôn Ngữ Nhận Diện (Thay Đổi Ngôn Ngữ OCR)

Hầu hết các thư viện OCR mặc định là tiếng Anh, nhưng nếu tài liệu của bạn là tiếng Pháp, Đức, hoặc thậm chí tiếng Nhật thì sao? Thay đổi ngôn ngữ chỉ cần gọi `set_recognition_language`. Điều này đáp ứng yêu cầu **thay đổi ngôn ngữ OCR** và đảm bảo độ chính xác cao hơn.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Tại sao bạn có thể cần điều này:** Một kho lưu trữ đa ngôn ngữ thường chứa các trang hỗn hợp. Chuyển đổi ngôn ngữ ngay lập tức giúp tránh nhận dạng sai các ký tự như “ß” hay “ñ”.

## Bước 3: Cấu Hình Các Tùy Chọn Render PDF (Chuyển Đổi Văn Bản PDF Đã Quét Hiệu Quả)

Khi làm việc với PDF đã quét, độ phân giải và chế độ màu ảnh hưởng mạnh tới chất lượng OCR. Render ở 300 DPI với chế độ grayscale là điểm cân bằng cho hầu hết tài liệu—đủ chi tiết nhưng không gây tốn bộ nhớ quá mức.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

Các lệnh chuỗi có thể trông cầu kỳ, nhưng chúng chỉ là một Fluent API trả về cùng một đối tượng tùy chọn mỗi lần. Nếu bạn cần màu (ví dụ, cho các sơ đồ màu), hãy thay `"grayscale"` bằng `"color"`.

## Bước 4: Nhận Diện PDF và Lấy Văn Bản Trang Đầu Tiên (Trích Xuất Văn Bản Từ PDF)

Bây giờ là phần cốt lõi của **cách OCR PDF**: đưa engine một đường dẫn file và lấy ra văn bản đã nhận dạng. Phương thức trả về một danh sách các kết quả trang; mỗi kết quả chứa thuộc tính `text`.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Nếu bạn cần toàn bộ tài liệu, hãy lặp qua `results`:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### Nếu PDF Được Mã Hoá?

Một số PDF được bảo vệ bằng mật khẩu. Trong trường hợp đó, bạn có thể truyền mật khẩu vào `recognize_pdf`:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

Engine sẽ giải mã ngay trong quá trình thực hiện OCR—không cần bước bổ sung nào.

## Bước 5: Xử Lý Sau Văn Bản Đã Trích Xuất (Tinh Chỉnh Văn Bản Được Trích Xuất Từ PDF)

Kết quả OCR thô thường chứa các ngắt dòng, khoảng trắng thừa, hoặc một vài ký tự nhận dạng sai. Một routine làm sạch nhanh sẽ chuẩn bị chuỗi đã trích xuất cho các bước xử lý tiếp theo (đánh chỉ mục tìm kiếm, lưu trữ cơ sở dữ liệu, v.v.).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Bây giờ bạn có thể an toàn **trích xuất văn bản từ PDF** và đưa nó vào bất kỳ pipeline NLP, công cụ tìm kiếm, hoặc thao tác `open(...).write()` đơn giản nào.

## Bonus: Xử Lý Hàng Loạt Nhiều PDF (Mở Rộng OCR Trên PDF)

Nếu bạn có một thư mục đầy các PDF đã quét, hãy bọc logic trong một vòng lặp:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Đoạn mã này cho thấy cách **thực hiện OCR trên PDF** hàng loạt, một nhu cầu phổ biến cho các dự án số hoá.

## Kết Quả Dự Kiến

Chạy ví dụ một trang (Bước 4) sẽ in ra một thứ gì đó như sau:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Nếu bạn xử lý một cuốn sách nhiều trang, console sẽ hiển thị văn bản đã làm sạch của mỗi trang, và script batch sẽ tạo một file `.txt` bên cạnh mỗi PDF.

## Những Sai Lầm Thường Gặp & Cách Tránh

| Vấn đề | Triệu chứng | Cách khắc phục |
|-------|------------|----------------|
| PDF nguồn độ phân giải thấp | Ký tự bị rối, từ bị thiếu | Tăng DPI (`set_dpi(400)` hoặc cao hơn) |
| Đặt ngôn ngữ sai | Nhiều ký tự không nhận dạng, đặc biệt là ký tự có dấu | Dùng `engine.set_recognition_language(ocr.Language.FRENCH)` hoặc enum phù hợp |
| PDF lớn gây lỗi bộ nhớ | `MemoryError` hoặc treo sau vài trang | Xử lý trang theo khối (`engine.recognize_pdf(..., max_pages=10)`) |
| Thiếu font trong PDF | Kết quả trống cho một số trang | Đảm bảo PDF thực sự chứa ảnh raster; một số PDF chỉ là vector và cần cách xử lý khác |

## Minh Họa Hình Ảnh

Dưới đây là một hình minh hoạ nhanh về quy trình làm việc. Văn bản alt được viết chuẩn SEO.

![luồng công việc OCR PDF hiển thị khởi tạo engine, cài đặt ngôn ngữ, tùy chọn render, nhận dạng và trích xuất văn bản](/images/ocr-workflow.png)

*Biểu đồ không bắt buộc để code chạy, nhưng nó giúp những người học bằng hình ảnh thấy được vị trí của mỗi bước trong quy trình.*

## Kết Luận

Chúng ta đã bao quát **cách OCR PDF** trong Python từ đầu đến cuối: tạo engine OCR, **thay đổi ngôn ngữ OCR**, cấu hình render để **chuyển đổi văn bản PDF đã quét**, và cuối cùng **trích xuất văn bản từ PDF** để sử dụng tiếp. Đoạn mã hoàn chỉnh, có thể chạy ngay đã sẵn sàng để chèn vào bất kỳ dự án nào, và script batch tùy chọn cho thấy cách mở rộng giải pháp.

Tiếp theo, bạn có thể muốn khám phá:

- Thêm **thực hiện OCR trên PDF** cho các kho lưu trữ đa ngôn ngữ bằng cách lặp qua danh sách ngôn ngữ.
- Tích hợp văn bản đã trích xuất với Elasticsearch để tìm kiếm toàn văn.
- Sử dụng OCR để tạo PDF có thể tìm kiếm bằng cách nhúng lớp văn bản trở lại file gốc (nhiều thư viện cung cấp phương thức `save_as_searchable_pdf`).

Hãy thoải mái thử nghiệm, điều chỉnh cài đặt DPI, hoặc chuyển sang backend OCR khác. Các nguyên tắc cơ bản vẫn giữ nguyên, và giờ bạn đã có nền tảng vững chắc để xây dựng tiếp.

Chúc lập trình vui vẻ, và hy vọng các tài liệu đã quét của bạn cuối cùng cũng trở nên có thể tìm kiếm được!

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Nhận Diện Văn Bản PDF – Các Hoạt Động OCR với Aspose.OCR cho Java](/ocr/english/java/ocr-operations/)
- [Cách OCR Văn Bản Ảnh Với Ngôn Ngữ Sử Dụng Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Cách OCR PDF trong .NET với Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
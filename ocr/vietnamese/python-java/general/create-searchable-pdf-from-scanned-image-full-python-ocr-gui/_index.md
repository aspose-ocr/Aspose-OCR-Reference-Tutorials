---
category: general
date: 2026-07-05
description: Tạo PDF có thể tìm kiếm bằng Python. Tìm hiểu cách OCR một PNG đã quét,
  chuyển đổi PDF hình ảnh đã quét và có được PDF có thể tìm kiếm trong vài phút.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm nhanh chóng. Hướng dẫn này chỉ cách OCR một
  PNG, chuyển đổi PDF ảnh quét và tạo PDF có thể tìm kiếm bằng Python.
og_title: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét – Hướng dẫn OCR Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét – Hướng dẫn OCR Python đầy đủ
url: /vi/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ hình ảnh đã quét – Hướng dẫn Python OCR đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **tạo PDF có thể tìm kiếm** từ một bức ảnh đã quét mà không phải trả tiền cho phần mềm đắt tiền chưa? Bạn không phải là người duy nhất. Ở nhiều văn phòng, PDF xuất hiện dưới dạng hình ảnh phẳng—khó tìm kiếm, không thể sao chép‑dán, và gây rắc rối cho các cuộc kiểm toán tuân thủ. Tin tốt? Chỉ với vài dòng Python, bạn có thể biến PNG tĩnh thành một PDF hoàn toàn có thể tìm kiếm, và quy trình này dễ dàng hơn bạn nghĩ.

Trong tutorial này, chúng ta sẽ đi qua một **ví dụ nhận dạng OCR** hoàn chỉnh, bao gồm mọi thứ từ cài đặt thư viện phù hợp đến việc ghi file PDF cuối cùng. Khi kết thúc, bạn sẽ biết chính xác cách **chuyển đổi PDF ảnh quét**, cách **ocr pdf** một cách lập trình, và sẽ có một script có thể tái sử dụng trong bất kỳ dự án nào.

## Những gì bạn sẽ học

- Cài đặt và cấu hình thư viện OCR cho Python (chúng ta sẽ dùng `pytesseract` và `pdf2image`).
- Khởi tạo engine OCR và đặt ngôn ngữ.
- Tải một PNG đã quét (hoặc bất kỳ hình ảnh nào) và chạy OCR trên nó.
- Chuyển kết quả OCR thành **PDF có thể tìm kiếm** (mảng byte) và lưu lại.
- Mẹo xử lý tài liệu đa trang, ngôn ngữ khác nhau, và các lỗi thường gặp.

Bạn không cần kinh nghiệm trước về OCR—chỉ cần một môi trường Python 3 hoạt động và chút tò mò.

---

## Tạo PDF có thể tìm kiếm – Tổng quan

Dưới đây là sơ đồ quy trình cấp cao của các bước chúng ta sẽ thực hiện.  

![Sơ đồ quy trình tạo PDF có thể tìm kiếm](https://example.com/flowchart.png "Sơ đồ quy trình tạo PDF có thể tìm kiếm")

*Alt text: Sơ đồ quy trình tạo PDF có thể tìm kiếm hiển thị việc khởi tạo engine, tải ảnh, nhận dạng OCR, chuyển đổi PDF và ghi file.*

---

## Bước 1: Khởi tạo Engine OCR (how to ocr pdf)

Tại sao chúng ta cần khởi tạo bất kỳ thứ gì? Engine OCR là bộ não giải mã các mẫu pixel thành ký tự. Bằng cách tạo một instance của engine và đặt ngôn ngữ một cách rõ ràng, chúng ta cho thư viện biết bảng chữ cái nào sẽ xuất hiện, giúp độ chính xác tăng đáng kể.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Mẹo chuyên nghiệp:** Nếu bạn cần OCR tài liệu đa ngôn ngữ, hãy cài đặt các gói ngôn ngữ tương ứng cho Tesseract và truyền danh sách như `"eng+spa"` vào `ocr_language`.

---

## Bước 2: Tải ảnh đã quét (convert scanned image pdf)

Phần tiếp theo của câu đố là đưa dữ liệu ảnh vào Python. Dù bạn có một PNG đơn lẻ hay một TIFF đa trang, lớp `PIL.Image` có thể mở chúng. Nếu bạn bắt đầu từ một PDF đã chứa ảnh quét, `pdf2image` sẽ chuyển mỗi trang thành một ảnh cho chúng ta.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Tại sao điều này quan trọng:** Việc tải ảnh dưới dạng đối tượng Pillow cho phép chúng ta truy cập dữ liệu pixel thô, mà engine OCR cần. Bỏ qua bước này và đưa raw bytes trực tiếp sẽ gây lỗi.

---

## Bước 3: Thực hiện nhận dạng OCR trên ảnh (ocr recognition example)

Bây giờ là phần thú vị—để engine đọc văn bản. `pytesseract.image_to_pdf_or_hocr` trả về một luồng byte PDF đã chứa lớp văn bản vô hình, chính là những gì chúng ta cần cho một **PDF có thể tìm kiếm**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Trường hợp đặc biệt:** Nếu ảnh của bạn có độ tương phản thấp, hãy cân nhắc áp dụng một ngưỡng đơn giản trước khi OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Bước tiền xử lý nhỏ này có thể tăng độ chính xác một cách đáng kể.

---

## Bước 4: Ghi byte PDF vào file (convert png searchable pdf)

Thư viện OCR cung cấp cho chúng ta một mảng byte—nghĩ như nội dung thô của một file PDF. Điều duy nhất chúng ta cần làm bây giờ là ghi các byte này ra đĩa.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Bạn sẽ thấy gì:** Mở file kết quả trong bất kỳ trình xem PDF nào và thử tìm kiếm một từ mà bạn biết có trong ảnh gốc. Đánh dấu sẽ nhảy thẳng đến vị trí, chứng minh lớp văn bản vô hình hoạt động.

---

## Bước 5: Mở rộng cho tài liệu đa trang (convert scanned image pdf)

Các hợp đồng thực tế thường kéo dài nhiều trang. Để **convert scanned image pdf** các file chứa nhiều trang, lặp qua từng trang, OCR chúng, và nối các PDF kết quả lại với nhau.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Tại sao phải gộp?** Mỗi lần gọi `image_to_pdf_or_hocr` tạo ra một PDF độc lập. Gộp chúng đảm bảo tài liệu cuối cùng giữ đúng thứ tự trang gốc.

---

## Các lỗi thường gặp & Cách khắc phục

| Triệu chứng | Nguyên nhân khả dĩ | Cách khắc phục |
|-------------|---------------------|----------------|
| Không có văn bản có thể tìm kiếm sau khi mở PDF | Tesseract không tìm thấy ký tự nào (kết quả trống) | Kiểm tra chất lượng ảnh, tăng DPI, hoặc áp dụng tiền xử lý (độ tương phản, nhị phân hoá). |
| Ký tự bị lỗi (ví dụ, �) | Gói ngôn ngữ sai hoặc thiếu phông chữ | Cài đặt dữ liệu ngôn ngữ đúng (`tesseract‑lang‑eng`) và đảm bảo `ocr_language` khớp. |
| Kích thước file PDF quá lớn (>10 MB cho một ảnh một trang) | Sử dụng PNG không nén làm nguồn; OCR thêm ảnh độ phân giải cao | Thu nhỏ ảnh trước khi OCR (`image.thumbnail((1240, 1754))` cho A4). |
| Script bị lỗi trên Windows với thông báo “tesseract.exe not found” | Binary Tesseract không có trong PATH | Thêm `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (điều chỉnh đường dẫn). |

---

## Script hoàn chỉnh, sẵn sàng chạy

Kết hợp tất cả lại, đây là một file duy nhất bạn có thể sao chép‑dán và chạy:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Lưu lại với tên `create_searchable_pdf.py`, thay thế các placeholder bằng đường dẫn thực tế, và chạy:

```bash
python create_searchable_pdf.py
```

Bạn sẽ thấy một

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách OCR PDF trong .NET với Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Chuyển đổi hình ảnh sang PDF C# – Lưu kết quả OCR đa trang](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR nhận dạng tài liệu PDF trong Aspose.OCR cho Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
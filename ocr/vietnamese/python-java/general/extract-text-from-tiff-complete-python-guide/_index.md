---
category: general
date: 2026-06-16
description: Trích xuất văn bản từ các tệp TIFF bằng OCR Python. Tìm hiểu cách chuyển
  đổi TIFF sang văn bản từng bước, xử lý tài liệu đa trang một cách dễ dàng.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: vi
og_description: Trích xuất văn bản từ các tệp TIFF bằng Python OCR. Hãy làm theo hướng
  dẫn này để chuyển đổi TIFF sang văn bản, xử lý các bản quét đa trang và nhận kết
  quả sạch sẽ.
og_title: Trích xuất văn bản từ TIFF – Hướng dẫn Python toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Trích xuất văn bản từ TIFF – Hướng dẫn Python toàn diện
url: /vi/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ TIFF – Hướng dẫn Python đầy đủ

Bạn đã bao giờ cần **trích xuất văn bản từ ảnh TIFF** nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn này khi làm việc với các kho lưu trữ đã quét hoặc tài liệu cũ. Tin tốt là gì? Chỉ với vài dòng Python, bạn có thể **chuyển đổi TIFF sang văn bản** trong chớp mắt, ngay cả khi tệp chứa hàng chục trang.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ thực tế: tải một tệp TIFF đa trang, đặt ngôn ngữ OCR là tiếng Pháp, và lấy văn bản đã nhận dạng ra từ mỗi trang. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy, hiểu lý do mỗi bước quan trọng, và biết cách điều chỉnh cho các ngôn ngữ hoặc định dạng ảnh khác.

## Các yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- Python 3.8 hoặc mới hơn đã được cài đặt.
- Gói `ocr` (hoặc bất kỳ thư viện OCR nào tương thích cung cấp lớp `OcrEngine`). Bạn có thể cài đặt bằng `pip install ocr-lib`—thay thế bằng tên gói thực tế bạn đang dùng.
- Một tệp TIFF đa trang (ví dụ: `french-scans.tif`) mà bạn muốn xử lý.
- Kiến thức cơ bản về lập trình Python.

Không có phụ thuộc nặng, không có dịch vụ bên ngoài—chỉ cần Python thuần và một engine OCR.

---

## Bước 1: Thiết lập Engine OCR để **Trích xuất văn bản từ TIFF**

Đầu tiên, chúng ta cần một thể hiện engine OCR và phải chỉ định ngôn ngữ sử dụng. Trong trường hợp này, tài liệu nguồn là tiếng Pháp, vì vậy chúng ta sẽ đặt ngôn ngữ cho phù hợp.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Tại sao lại quan trọng:**  
Cài đặt ngôn ngữ cải thiện độ chính xác đáng kể. Các ký tự tiếng Pháp như “é” hay “ç” sẽ bị nhận dạng sai thành ký tự chung nếu engine mặc định tiếng Anh. Bằng cách chọn tiếng Pháp một cách rõ ràng, chúng ta cung cấp cho engine bản đồ ký tự đúng.

> **Mẹo chuyên nghiệp:** Nếu bạn xử lý tài liệu đa ngôn ngữ, có thể thay đổi `engine.language` ngay trước mỗi lời gọi `recognize()`.

---

## Bước 2: Tải TIFF đa trang mà bạn muốn **Chuyển đổi TIFF sang Văn bản**

Một tệp TIFF có thể chứa nhiều khung—nghĩ mỗi khung là một trang riêng. Thư viện OCR trừu tượng hoá việc này cho chúng ta, vì vậy chỉ cần trỏ tới tệp.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Cảnh báo trường hợp đặc biệt:**  
Nếu đường dẫn tệp sai hoặc TIFF bị hỏng, phương thức `load_from_file` sẽ ném ra ngoại lệ. Hãy bọc nó trong khối `try/except` cho mã sản xuất:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Bước 3: Chạy OCR trên toàn bộ tài liệu – Cốt lõi của **Trích xuất văn bản từ TIFF**

Bây giờ chúng ta để engine thực hiện phép màu. Lời gọi `recognize()` xử lý mọi trang một lần và trả về một đối tượng kết quả phong phú.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Đằng sau màn hình đang diễn ra gì?**  
Engine lặp qua từng khung, áp dụng tiền xử lý (điều chỉnh góc, nhị phân hoá), chạy mạng nơ-ron, và tổng hợp kết quả. Vì chúng ta chỉ gọi `recognize()` một lần, thư viện có thể chia sẻ tài nguyên giữa các trang, nhanh hơn so với việc lặp thủ công.

---

## Bước 4: Lấy Văn bản Đã Nhận dạng ra từ Kết quả JSON – **Chuyển đổi TIFF sang Văn bản** Trang theo Trang

Đối tượng kết quả có thể được tuần tự hoá thành JSON. Trong JSON đó, bạn sẽ thấy một mảng `pages`, mỗi phần tử chứa trường `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Bây giờ chúng ta có một danh sách Python sạch sẽ, mỗi phần tử tương ứng với đầu ra OCR của một trang.

---

## Bước 5: In hoặc Lưu Văn bản cho Mỗi Trang – Phần Cuối cùng của **Trích xuất văn bản từ TIFF**

Hãy lặp qua các trang và hiển thị văn bản đã trích xuất. Bạn cũng có thể ghi mỗi trang vào một tệp `.txt` riêng nếu muốn.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Đầu ra Dự kiến (ví dụ)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Nếu OCR thành công, bạn sẽ thấy một khối câu tiếng Pháp sạch sẽ cho mỗi trang. Nếu gặp ký tự lộn xộn, hãy kiểm tra lại cài đặt ngôn ngữ hoặc cân nhắc tăng độ phân giải ảnh trước khi OCR.

---

## Xử lý Các Trường Hợp Thường Gặp Khi Bạn **Chuyển đổi TIFF sang Văn bản**

| Vấn đề | Nguyên nhân | Giải pháp nhanh |
|-------|-------------|-----------------|
| **Mảng `pages` rỗng** | TIFF không được tải đúng hoặc không có khung nào. | Kiểm tra lại đường dẫn tệp và đảm bảo TIFF không phải là PNG một trang được đổi tên thành TIFF. |
| **Ký tự rác** | Không khớp ngôn ngữ hoặc chất lượng ảnh thấp. | Đặt đúng `engine.language` và tiền xử lý ảnh (ví dụ: tăng DPI). |
| **Bùng RAM khi xử lý TIFF lớn** | Tải toàn bộ các trang cùng lúc tiêu tốn RAM. | Xử lý theo lô: tải một khung, nhận dạng, sau đó giải phóng trước khi chuyển sang khung tiếp theo. |
| **Lỗi Unicode khi in** | Mã hoá console không hỗ trợ ký tự có dấu. | Dùng `print(page["text"].encode('utf-8').decode('utf-8'))` hoặc cấu hình terminal sang UTF‑8. |

---

## Mở Rộng Script: Từ **Trích xuất Văn bản từ TIFF** đến Xử lý Hàng Loạt

Khi đã có nền tảng vững chắc, hãy xem xét các bước tiếp theo:

1. **Chuyển đổi hàng loạt** – Đóng gói toàn bộ quy trình trong hàm `def ocr_tiff(path):` và lặp qua một thư mục chứa các tệp TIFF.
2. **Xuất ra tệp** – Thay vì in, ghi văn bản mỗi trang vào `page_{i}.txt` hoặc ghép tất cả vào một tài liệu duy nhất.
3. **Engine OCR thay thế** – Nếu cần độ chính xác cao hơn, thay `ocr.OcrEngine()` bằng Tesseract (`pytesseract`) hoặc Azure Cognitive Services—vẫn giữ logic “trích xuất văn bản từ TIFF”.
4. **Xử lý hậu kỳ** – Chạy kiểm tra chính tả, phát hiện ngôn ngữ, hoặc làm sạch bằng regex để tinh chỉnh đầu ra OCR thô.

---

## Script Đầy Đủ, Sẵn Sàng Chạy

Dưới đây là toàn bộ mã, sẵn sàng sao chép‑dán. Nó bao gồm xử lý lỗi cơ bản và tùy chọn lưu văn bản mỗi trang vào các tệp riêng.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Chạy script này, chỉ định `tiff_file` tới tài liệu của bạn, và xem console hiện ra các câu tiếng Pháp sạch sẽ. Nếu bạn cung cấp `out_folder`, bạn cũng sẽ tìm thấy một loạt tệp `page_#.txt` sẵn sàng cho các bước xử lý tiếp theo.

---

## Kết luận

Chúng ta vừa **trích xuất văn bản từ các tệp TIFF** bằng một quy trình OCR Python đơn giản, và bạn đã biết cách **chuyển đổi TIFF sang văn bản** một cách đáng tin cậy. Từ việc khởi tạo engine với ngôn ngữ phù hợp đến việc lặp qua kết quả JSON của mỗi trang, mọi bước đều được giải thích kèm “tại sao”, giúp bạn áp dụng mô hình này cho các ngôn ngữ, định dạng ảnh, hoặc công việc batch lớn hơn.

Tiếp theo bạn muốn làm gì? Hãy thử thay đổi backend OCR sang Tesseract, thử các gói ngôn ngữ khác, hoặc tích hợp đầu ra vào cơ sở dữ liệu có khả năng tìm kiếm. Khi bạn có thể biến các ảnh quét thành văn bản có thể tìm kiếm, khả năng là vô hạn.

Nếu gặp bất kỳ khó khăn nào hoặc có ý tưởng cải tiến, đừng ngần ngại để lại bình luận. Chúc bạn coding vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
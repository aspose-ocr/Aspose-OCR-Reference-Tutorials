---
category: general
date: 2026-03-26
description: Chuyển đổi hình ảnh thành bảng bằng Python sử dụng OCR và AI. Tìm hiểu
  cách trích xuất bảng từ hình ảnh, cải thiện độ chính xác của OCR và nhận kết quả
  có cấu trúc nhanh chóng.
draft: false
keywords:
- convert image to table
- extract table from image
- extract tabular data image
- enhance OCR accuracy
language: vi
og_description: Chuyển đổi hình ảnh thành bảng trong Python. Hướng dẫn này chỉ cách
  trích xuất bảng từ hình ảnh, nâng cao độ chính xác OCR và làm việc với dữ liệu có
  cấu trúc.
og_title: Chuyển đổi hình ảnh thành bảng – Hướng dẫn Python từng bước
tags:
- OCR
- Python
- AI post‑processing
title: Chuyển đổi hình ảnh thành bảng – Hướng dẫn Python đầy đủ
url: /vi/python/general/convert-image-to-table-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi hình ảnh thành bảng – Hướng dẫn Python toàn diện

Bạn đã bao giờ cần **convert image to table** nhưng lại bế tắc vì chỉ nhìn vào một ảnh chụp mờ? Bạn không phải là người duy nhất. Trong nhiều dự án dựa trên dữ liệu, cách nhanh nhất để đưa số liệu vào dataframe là chụp một bức ảnh của bảng đã in và để script thực hiện công việc nặng. Tin tốt? Với một engine OCR hiện đại kết hợp với một AI post‑processor nhỏ, bạn có thể lấy được một bảng sạch, có cấu trúc từ hầu hết bất kỳ hình ảnh nào.

Trong tutorial này, chúng ta sẽ đi qua một **real‑world example that extracts tabular data image**, làm sạch nó, và in mỗi hàng dưới dạng văn bản thuần. Khi kết thúc, bạn sẽ hiểu cách **enhance OCR accuracy**, xử lý các lỗi thường gặp, và điều chỉnh mã cho các pipeline của riêng bạn. Không có phép màu, chỉ có Python, một vài thư viện, và một chút suy luận.

> **Bạn sẽ cần**  
> * Python 3.9+  
> * Thư viện OCR hỗ trợ `OutputFormat.Structured` (ví dụ, `myocr`)  
> * AI post‑processor tùy chọn (có thể là một transformer nhẹ hoặc một hàm dựa trên quy tắc)  
> * Tệp hình ảnh mẫu (`table.png`) chứa một bảng đơn giản

---

## Bước 1: Chuyển đổi hình ảnh thành bảng – Nhận dạng hình ảnh với đầu ra có cấu trúc

Điều đầu tiên chúng ta làm là đưa ảnh vào engine OCR và yêu cầu một kết quả **structured**. Đầu ra có cấu trúc có nghĩa là engine cố gắng suy ra các hàng, cột và ranh giới ô thay vì trả về một chuỗi phẳng.

```python
import myocr as ocr          # Hypothetical OCR package
import myengine as engine    # Wrapper around the OCR engine
import myai as ai            # Simple AI post‑processor

def recognize_image(path: str):
    """
    Sends the image to the OCR engine and asks for a tabular
    (structured) representation.
    """
    # Step 1: Recognize the image and request a structured (tabular) result
    structured_result = engine.recognize_image(
        path,
        output_format=ocr.OutputFormat.Structured
    )
    return structured_result
```

**Tại sao điều này quan trọng:**  
Nếu bạn yêu cầu OCR trả về văn bản thuần, bạn sẽ nhận được một đống ký tự lộn xộn mà không có khái niệm về hàng hay cột. Bằng cách yêu cầu định dạng có cấu trúc, engine thực hiện công việc nặng như phát hiện dòng, căn chỉnh cột, và thậm chí hợp nhất ô cơ bản. Điều này giảm đáng kể lượng phân tích thủ công bạn sẽ cần sau này.

> **Mẹo chuyên nghiệp:** Đảm bảo hình ảnh có độ tương phản tốt và độ nghiêng tối thiểu. Một bản quét 300 dpi thường cho kết quả tốt nhất.

---

## Bước 2: Nâng cao độ chính xác OCR – Xử lý hậu kỳ cấu trúc thô

OCR không hoàn hảo—đặc biệt khi hình ảnh nguồn chứa các đường mờ hoặc phông chữ lạ. Đó là nơi một AI nhẹ (hoặc thậm chí một script dựa trên quy tắc) có thể làm sạch đầu ra, sửa các nhận dạng sai thường gặp, và thêm ngữ cảnh còn thiếu.

```python
def enhance_structure(structured_result):
    """
    Runs a post‑processor that fixes typical OCR errors
    (e.g., 'O' vs '0', merged cells) and adds semantic context.
    """
    # Step 2: Enhance the raw OCR structure with AI (adds context, corrects errors)
    enhanced_structure = ai.run_postprocessor(structured_result)
    return enhanced_structure
```

**Tại sao điều này quan trọng:**  
Một bảng OCR thô có thể gắn nhãn tiêu đề là “Q1 2022” nhưng đọc sai “1” thành “l”. Lớp AI có thể học các mẫu này từ một bộ dữ liệu huấn luyện nhỏ và xuất ra một bảng sạch hơn. Ngay cả một heuristics đơn giản (thay “l” cô lập bằng “1” khi xung quanh là chữ số) cũng có thể tăng **enhance OCR accuracy** đáng kể.

> **Trường hợp góc phổ biến:** Nếu bảng chứa các ô hợp nhất, OCR có thể sao chép nội dung qua các cột. Post‑processor nên phát hiện các ô liền kề giống nhau và gộp chúng lại.

---

## Bước 3: Trích xuất dữ liệu bảng từ hình ảnh – Lặp qua các hàng và hiển thị văn bản ô

Bây giờ chúng ta đã có một cấu trúc gọn gàng, việc trích xuất dữ liệu trở nên đơn giản. Chúng ta sẽ lặp qua bảng đầu tiên được phát hiện và in mỗi hàng dưới dạng danh sách các giá trị ô.

```python
def print_table(enhanced_structure):
    """
    Prints each row of the first detected table.
    """
    # Step 3: Iterate over the rows of the first detected table and display cell text
    for row in enhanced_structure.tables[0].rows:
        print([cell.text for cell in row.cells])

if __name__ == "__main__":
    # Path to your image file
    image_path = "YOUR_DIRECTORY/table.png"

    # Run the pipeline
    raw = recognize_image(image_path)
    cleaned = enhance_structure(raw)
    print_table(cleaned)
```

**Bạn sẽ thấy:**  
Giả sử `table.png` chứa một lưới đơn giản 3 × 2, đầu ra có thể trông như sau:

```
['Product', 'Price']
['Apple', '$1.20']
['Banana', '$0.80']
```

Nếu OCR bỏ lỡ một tiêu đề, AI post‑processor có thể chèn nó dựa trên ngữ cảnh xung quanh, vì vậy bảng cuối cùng đã sẵn sàng cho pandas hoặc bất kỳ phân tích tiếp theo nào.

> **Cảnh báo:** Các hàng trống ở cuối bảng. Một số engine OCR thêm một hàng trống khi gặp khoảng trắng. Một kiểm tra nhanh `if any(cell.text for cell in row.cells):` có thể lọc chúng ra.

---

## Bonus: Đi xa hơn – Lưu bảng thành CSV hoặc DataFrame

Hầu hết các workflow thực tế cần dữ liệu ở dạng tệp CSV hoặc pandas DataFrame. Dưới đây là một đoạn mã nhỏ chuyển các hàng đã in thành CSV mà không rời khỏi quá trình Python.

```python
import csv
import pandas as pd

def save_to_csv(enhanced_structure, output_path="output.csv"):
    rows = [
        [cell.text for cell in row.cells]
        for row in enhanced_structure.tables[0].rows
        if any(cell.text for cell in row.cells)  # Skip empty rows
    ]
    # Write CSV
    with open(output_path, "w", newline="", encoding="utf-8") as f:
        writer = csv.writer(f)
        writer.writerows(rows)

    # Also return a DataFrame for immediate use
    return pd.DataFrame(rows[1:], columns=rows[0])  # Assume first row is header

# Example usage:
df = save_to_csv(cleaned, "my_table.csv")
print(df.head())
```

Bây giờ bạn có một DataFrame sẵn sàng sử dụng, hoàn hảo cho phân tích, trực quan hoá, hoặc đưa vào mô hình machine‑learning.

---

## Câu hỏi thường gặp (FAQ)

**Q: Điều này có hoạt động với PDF chứa bảng đã quét không?**  
A: Hoàn toàn—chỉ cần chuyển mỗi trang PDF thành hình ảnh (ví dụ, dùng `pdf2image`) và đưa các PNG kết quả vào cùng pipeline.

**Q: Bảng của tôi có các ô tiêu đề hợp nhất; AI có sửa được không?**  
A: Một post‑processor được đào tạo tốt có thể phát hiện các ô hợp nhất bằng cách kiểm tra span của ô. Nếu bạn dùng cách tiếp cận dựa trên quy tắc, hãy tìm văn bản giống nhau trong các ô liền kề và gộp chúng lại.

**Q: Nếu OCR trả về nhiều bảng thì sao?**  
A: `enhanced_structure.tables` là một danh sách. Bạn có thể lặp qua nó, hoặc chọn bảng có số hàng/cột nhiều nhất—bất kỳ cái nào phù hợp với mong đợi của bạn.

**Q: Tôi có thể thay thế AI post‑processor bằng một việc dọn dẹp regex đơn giản không?**  
A: Có. Đối với nhiều dự án, một vài phép thay thế regex (ví dụ, sửa “O” → “0”) là đủ. Điều quan trọng là chạy *điều gì đó* sau OCR để cải thiện **enhance OCR accuracy**.

## Kết luận

Chúng tôi vừa trình bày cách **convert image to table** trong Python, từ nhận dạng OCR thô đến cấu trúc dữ liệu được AI‑enhance, sẵn sàng sử dụng. Quy trình ba bước—nhận dạng, nâng cao, trích xuất—bao phủ các thách thức cốt lõi của **extract table from image** và minh họa các cách thực tế để **enhance OCR accuracy**.  

Chụp một ảnh chụp màn hình của bất kỳ bảng tính nào, chỉ đường dẫn script tới nó, và bạn sẽ có một CSV hoặc DataFrame trong vài giây. Từ đây bạn có thể khám phá các thủ thuật nâng cao hơn: PDF đa trang, bảng viết tay, hoặc thậm chí luồng video thời gian thực.  

Sẵn sàng cho thử thách tiếp theo? Hãy thử đưa các khung video trực tiếp vào pipeline, hoặc thử nghiệm các post‑processor dựa trên mô hình ngôn ngữ có thể suy ra tên cột thiếu. Không giới hạn, và giờ bạn đã có nền tảng vững chắc để xây dựng.

Chúc lập trình vui vẻ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
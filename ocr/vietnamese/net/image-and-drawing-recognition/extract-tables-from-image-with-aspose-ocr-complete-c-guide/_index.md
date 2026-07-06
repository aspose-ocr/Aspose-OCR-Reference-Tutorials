---
category: general
date: 2026-05-31
description: Trích xuất bảng từ hình ảnh bằng Aspose OCR trong C#. Tìm hiểu cách chuyển
  đổi hình ảnh thành bảng, bật tính năng phát hiện bảng và xuất kết quả một cách hiệu
  quả.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: vi
og_description: Trích xuất bảng từ hình ảnh bằng Aspose OCR. Hướng dẫn này cho thấy
  cách chuyển đổi hình ảnh thành bảng, bật tính năng phát hiện bảng và xử lý kết quả
  trong C#.
og_title: Trích xuất bảng từ hình ảnh – Hướng dẫn C# từng bước
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: Trích xuất bảng từ hình ảnh bằng Aspose OCR – Hướng dẫn C# đầy đủ
url: /vi/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất bảng từ hình ảnh – Hướng dẫn C# đầy đủ

Bạn đã bao giờ cần **trích xuất bảng từ hình ảnh** nhưng không chắc bắt đầu từ đâu? Bạn không đơn độc; nhiều nhà phát triển gặp khó khăn này khi cố gắng chuyển đổi hóa đơn hoặc biên lai đã quét thành dữ liệu có thể sử dụng. Tin tốt là gì? Với Aspose OCR bạn có thể **chuyển đổi hình ảnh thành bảng** chỉ trong vài dòng mã C#.

Trong tutorial này chúng ta sẽ đi qua một ví dụ thực tế: tải một file PNG chứa bảng, chuyển bố cục hình ảnh thành một lưới có cấu trúc, và in nội dung của mỗi ô cùng với điểm tin cậy. Khi kết thúc, bạn sẽ có một đoạn mã hoàn chỉnh có thể chèn vào bất kỳ dự án .NET nào, cùng với các mẹo xử lý các trường hợp đặc biệt và mở rộng giải pháp.

## Những gì bạn cần

- **.NET 6.0** hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.6+)
- Gói NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)
- Một file ảnh thực sự chứa bảng (ví dụ: `invoice_with_table.png`)
- Một IDE C# cơ bản (Visual Studio, Rider, hoặc VS Code với extension C#)

Đó là tất cả—không cần engine OCR phụ, không có phụ thuộc nặng. Sẵn sàng? Hãy bắt đầu.

## Bước 1: Khởi tạo Engine OCR để **Trích xuất bảng từ hình ảnh**

Đầu tiên, chúng ta tạo một thể hiện `OcrEngine` và chỉ định nó tới ảnh nguồn của chúng ta. Hãy nghĩ engine như bộ não sẽ đọc từng pixel và cố gắng hiểu bố cục.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **Why this matters:** Without initializing the engine correctly, the OCR engine has nothing to analyze, and you’ll never get any tables out of the picture. The `ImageStream.FromFile` call also takes care of common format issues (PNG, JPEG, BMP) so you don’t need extra conversion steps.

> **Tại sao điều này quan trọng:** Nếu không khởi tạo engine đúng cách, engine OCR sẽ không có gì để phân tích và bạn sẽ không bao giờ nhận được bảng nào từ ảnh. Lệnh `ImageStream.FromFile` cũng xử lý các vấn đề định dạng phổ biến (PNG, JPEG, BMP) nên bạn không cần các bước chuyển đổi thêm.

## Bước 2: Bật tính năng Phát hiện Bảng – Chìa khóa để **Chuyển đổi hình ảnh thành bảng**

Aspose OCR có thể đọc văn bản thuần từ ảnh, nhưng nó sẽ không tự động hiểu các hàng và cột trừ khi bạn yêu cầu nó tìm bảng. Đây là nơi cờ `DetectTables` phát huy vai trò.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Pro tip:** If you only need raw text, leave `DetectTables` as `false`. Enabling it adds a small overhead, but the payoff is a clean, structured result that you can directly feed into a spreadsheet or database.

> **Mẹo chuyên nghiệp:** Nếu bạn chỉ cần văn bản thô, để `DetectTables` là `false`. Bật tính năng này sẽ tạo một chút chi phí bổ sung, nhưng đổi lại bạn sẽ có kết quả sạch sẽ, có cấu trúc và có thể đưa trực tiếp vào bảng tính hoặc cơ sở dữ liệu.

## Bước 3: Thực hiện Nhận dạng OCR – Khoảnh khắc quyết định

Bây giờ chúng ta yêu cầu engine thực sự đọc ảnh. Phương thức `Recognize` trả về một đối tượng `OcrResult` chứa cả văn bản thuần và bất kỳ bảng nào được phát hiện.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **What happens under the hood?** Aspose runs a series of image preprocessing steps (deskewing, binarization) before applying its neural‑network‑based text recognizer. When `DetectTables` is true, it also runs a layout analysis pass that groups characters into rows and columns.

> **Bên trong thực tế:** Aspose thực hiện một loạt các bước tiền xử lý ảnh (điều chỉnh nghiêng, nhị phân hoá) trước khi áp dụng bộ nhận dạng văn bản dựa trên mạng nơ-ron. Khi `DetectTables` được bật, nó còn thực hiện một bước phân tích bố cục để nhóm ký tự thành hàng và cột.

## Bước 4: Duyệt qua các Bảng đã Phát hiện – **Trích xuất bảng từ hình ảnh** trong hành động

Nếu engine tìm thấy bất kỳ bảng nào, chúng sẽ xuất hiện trong `result.Tables`. Chúng ta sẽ lặp qua mỗi bảng, sau đó qua từng hàng và cột, in ra văn bản ô và phần trăm tin cậy.

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **Why check confidence?** OCR isn’t perfect, especially with low‑resolution scans. The `Confidence` value (0‑100) lets you decide whether to accept the cell as‑is or flag it for manual review. A typical threshold is 80 % for critical data.

> **Tại sao cần kiểm tra độ tin cậy?** OCR không hoàn hảo, đặc biệt với các bản quét độ phân giải thấp. Giá trị `Confidence` (0‑100) cho phép bạn quyết định có chấp nhận ô như hiện tại hay đánh dấu để xem xét thủ công. Ngưỡng thường dùng là 80 % cho dữ liệu quan trọng.

### Kết quả dự kiến

Giả sử ảnh nguồn chứa một bảng 3 × 4 các mục hóa đơn, bạn có thể thấy kết quả như sau:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

Nếu không có bảng nào được phát hiện, `result.Tables` sẽ rỗng—không có gì để in, nhưng chương trình vẫn sẽ thoát một cách êm thấm.

## Bước 5: Xử lý các Trường hợp Cạnh và Những Cạm bẫy Thông thường

### Hình ảnh độ phân giải thấp

Khi ảnh nguồn dưới 150 dpi, thuật toán phát hiện bảng có thể bỏ lỡ ranh giới ô. Một cách khắc phục nhanh là tăng kích thước ảnh bằng `System.Drawing` trước khi đưa vào Aspose:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### Bảng bị nghiêng

Nếu bảng bị quay một vài độ, bật tính năng tự động chỉnh nghiêng:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### Nhiều bảng trên một trang

Aspose OCR trả về mỗi bảng như một đối tượng riêng trong `result.Tables`. Bạn có thể xử lý chúng riêng lẻ, hoặc hợp nhất chúng thành một `DataTable` duy nhất nếu cần một cái nhìn tổng hợp.

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### Xuất ra Excel

Khi đã có một `DataTable`, việc xuất ra file `.xlsx` trở nên dễ dàng với `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

Bây giờ bạn đã thực sự **chuyển đổi hình ảnh thành bảng** và có thể chuyển file bảng tính cho các quy trình downstream.

## Ví dụ Hoạt động Đầy đủ – Từ Đầu đến Cuối

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy, kết hợp mọi thứ lại. Dán nó vào một dự án console mới, thay đổi đường dẫn file, và nhấn **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**Giải thích luồng công việc**

1. **Engine setup** – Loads the image and tells Aspose to look for tables.  
   **Cài đặt Engine** – Tải ảnh và thông báo cho Aspose tìm kiếm bảng.
2. **Options tuning** – `DetectTables` does the heavy lifting; `Deskew` improves accuracy on angled scans.  
   **Tinh chỉnh tùy chọn** – `DetectTables` thực hiện phần công việc nặng; `Deskew` cải thiện độ chính xác khi ảnh bị nghiêng.
3. **Recognition** – Returns both plain text and a collection of `Table` objects.  
   **Nhận dạng** – Trả về cả văn bản thuần và một tập hợp các đối tượng `Table`.
4. **Iteration** – Prints each cell with confidence, while also building a `DataTable` for later export.  
   **Duyệt** – In mỗi ô kèm độ tin cậy, đồng thời xây dựng một `DataTable` để xuất sau này.
5. **Export** – Uses `ClosedXML` (a lightweight, no‑interop library) to write an `.xlsx` file—perfect for downstream analytics or reporting.  
   **Xuất** – Sử dụng `ClosedXML` (thư viện nhẹ, không cần interop) để ghi file `.xlsx`—lý tưởng cho phân tích hoặc báo cáo downstream.

## Câu hỏi Thường gặp

- **Does this work with PDFs?**  
  Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`), then feed the bitmap to Aspose OCR.  
  **Điều này có hoạt động với PDF không?**  
  Có. Đầu tiên chuyển mỗi trang PDF thành ảnh (`PdfRenderer` hoặc `Ghostscript`), sau đó đưa bitmap vào Aspose OCR.

- **Can I extract tables from a JPG?**  
  Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP, and TIFF out of the box.  
  **Tôi có thể trích xuất bảng từ JPG không?**  
  Chắc chắn. Phương thức `ImageStream.FromFile` hỗ trợ JPEG, PNG, BMP và TIFF ngay lập tức.

- **What if my table has merged cells?**  
  Aspose OCR treats merged cells as separate logical cells; you may need to post‑process the output to combine them based on confidence or content patterns.  
  **Nếu bảng của tôi có các ô hợp nhất thì sao?**  
  Aspose OCR coi các ô hợp nhất như các ô logic riêng biệt; bạn có thể cần xử lý hậu kỳ để kết hợp chúng dựa trên độ tin cậy hoặc mẫu nội dung.

- **Is there a limit on table size?**  
  Practically, the engine handles tables up to several hundred rows. Performance degrades linearly, so consider chunking very large scans.  
  **Có giới hạn về kích thước bảng không?**  
  Thực tế, engine có thể xử lý các bảng lên tới vài trăm hàng. Hiệu năng giảm theo tỷ lệ tuyến tính, vì vậy hãy cân nhắc chia nhỏ các bản quét rất lớn.

## Kết luận

Chúng tôi vừa cho bạn thấy cách

## Bạn nên học gì tiếp theo?

- [Cách trích xuất bảng từ hình ảnh bằng Aspose.OCR cho .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Trích xuất Văn bản từ Hình ảnh – Tối ưu hoá OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)
- [Cách trích xuất Văn bản từ Hình ảnh bằng cách Chuẩn bị Các Hình chữ nhật trong OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
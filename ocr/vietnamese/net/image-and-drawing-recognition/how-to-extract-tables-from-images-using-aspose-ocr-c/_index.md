---
category: general
date: 2026-03-28
description: Tìm hiểu cách trích xuất bảng từ hình ảnh bằng Aspose OCR trong C#. Hướng
  dẫn này bao gồm cách phát hiện bảng trong hình ảnh, tải hình ảnh để OCR và trích
  xuất bảng từ các tệp PNG.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: vi
og_description: Hướng dẫn từng bước cách trích xuất bảng từ hình ảnh bằng Aspose OCR
  trong C#. Bao gồm mã nguồn, giải thích và mẹo phát hiện bảng trong các tệp hình
  ảnh.
og_title: Cách Trích Xuất Bảng Từ Hình Ảnh Sử Dụng Aspose OCR (C#)
tags:
- Aspose OCR
- C#
- Table Extraction
title: Cách trích xuất bảng từ hình ảnh bằng Aspose OCR (C#)
url: /vi/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Trích Xuất Bảng Từ Hình Ảnh Sử Dụng Aspose OCR (C#)

Bạn đã bao giờ tự hỏi **cách trích xuất bảng** từ một hoá đơn đã quét hoặc một ảnh chụp màn hình bảng tính chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, chúng ta cần chuyển đổi một bức ảnh của bảng thành dữ liệu có thể truy vấn—thường là CSV hoặc DataTable. Tin tốt là gì? Aspose OCR làm cho việc này trở nên cực kỳ đơn giản, và bạn chỉ cần vài dòng C#.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: từ **load image for OCR**, tới **detect tables in image**, và cuối cùng là **extract table from image** và lưu dưới dạng file CSV. Khi kết thúc, bạn sẽ có một ứng dụng console sẵn sàng chạy, có thể **extract tables from PNG** (hoặc bất kỳ bitmap nào được hỗ trợ) mà không gặp rắc rối.

## Các Điều Kiện Cần Thiết

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- .NET 6.0 SDK hoặc phiên bản mới hơn (mã cũng chạy được với .NET Framework)
- Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích)
- Tệp giấy phép Aspose.OCR for .NET (bạn có thể bắt đầu với bản dùng thử miễn phí)
- Một hình mẫu chứa bảng (ví dụ: `invoice_table.png`)

Nếu có bất kỳ mục nào chưa quen, đừng lo—chỉ cần cài đặt .NET SDK và lấy gói NuGet, bạn sẽ sẵn sàng.

## Tổng Quan Về Giải Pháp

Ở mức cao, luồng công việc trông như sau:

1. **Load the image** bạn muốn xử lý.
2. **Run OCR recognition** để engine biết vị trí của văn bản.
3. **Create a TableExtractor** để quét kết quả OCR tìm cấu trúc dạng lưới.
4. **Extract all detected tables** và chọn bảng bạn cần.
5. **Save the table** dưới dạng CSV (hoặc bất kỳ định dạng nào bạn muốn).

Mỗi bước sẽ được giải thích chi tiết bên dưới, kèm theo các đoạn mã đầy đủ để bạn có thể sao chép‑dán.

<img src="table_extraction_example.png" alt="ví dụ cách trích xuất bảng từ hình ảnh" width="600">

*(Hình trên hiển thị một bảng hoá đơn mẫu mà chúng ta sẽ trích xuất.)*

## Bước 1 – Load the Image for OCR

Điều đầu tiên bạn cần làm là cho Aspose OCR biết file nào sẽ được đọc. Thư viện hỗ trợ PNG, JPEG, BMP, TIFF và một vài định dạng khác. Đây là đoạn mã tối thiểu:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**Tại sao lại quan trọng:**  
`Image.FromFile` thực hiện việc giải mã PNG (hoặc bất kỳ bitmap nào) thành định dạng mà OCR engine có thể hiểu. Nếu bỏ qua bước này hoặc truyền file bị hỏng, lời gọi `Recognize()` tiếp theo sẽ ném ra ngoại lệ.

> **Mẹo:** Nếu bạn đang xử lý các PDF lớn, hãy trích xuất mỗi trang thành hình ảnh trước—nếu không, OCR engine sẽ hết bộ nhớ.

## Bước 2 – Recognize the Page (Required Before Table Detection)

Nhận dạng chuyển đổi dữ liệu pixel thô thành bố cục văn bản có thể tìm kiếm. Nếu không thực hiện bước này, `TableExtractor` sẽ không có gì để làm việc.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**Đằng sau màn hình đang diễn ra gì?**  
Aspose OCR chạy bộ phát hiện văn bản dựa trên mạng nơ‑ron, sau đó tạo ra một cây phân cấp các đối tượng `Page`, `Paragraph` và `Word`. Bộ phát hiện bảng sẽ sau đó kiểm tra mối quan hệ không gian giữa các từ này.

Nếu bạn xử lý nhiều hình ảnh trong một vòng lặp, hãy cân nhắc tái sử dụng cùng một đối tượng `OcrEngine` và chỉ thay đổi thuộc tính `Image`—cách này giảm tải việc cấp phát bộ nhớ.

## Bước 3 – Create a TableExtractor and Detect Tables in Image

Khi dữ liệu OCR đã có, chúng ta có thể yêu cầu Aspose tìm các bảng. Lớp `TableExtractor` thực hiện đúng chức năng này.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**Tại sao lại dùng `ExtractAll()`?**  
Một hình ảnh có thể chứa nhiều bảng (nghĩ đến một báo cáo đa phần). `ExtractAll()` trả về một `List<Table>` để bạn có thể duyệt, chọn bảng phù hợp, hoặc thậm chí hợp nhất chúng sau này.

Nếu bạn chỉ cần bảng đầu tiên, có thể an toàn dùng `extractedTables[0]`, nhưng luôn kiểm tra danh sách không rỗng để tránh `IndexOutOfRangeException`.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## Bước 4 – Save the Extracted Table as CSV (or Any Other Format)

Aspose làm cho việc xuất dữ liệu trở nên đơn giản. Lớp `Table` có các phương thức `SaveCsv`, `SaveXls` và `SaveJson` tích hợp sẵn. Dưới đây là cách ghi file CSV:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**File CSV sẽ trông như thế nào?**  
Giả sử hình ảnh nguồn chứa một lưới 4 × 3, CSV có thể xuất hiện như sau:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

Bạn có thể mở file này trong Excel, Power BI, hoặc đưa thẳng vào pipeline dữ liệu của mình.

## Ví Dụ Hoàn Chỉnh Từ Đầu Đến Cuối

Dưới đây là chương trình hoàn chỉnh, tự chứa. Sao chép vào một dự án console mới (`dotnet new console`) và chạy. Đảm bảo đã cài đặt gói NuGet `Aspose.OCR` (`dotnet add package Aspose.OCR`).

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### Kết Quả Mong Đợi

Khi chạy chương trình, bạn sẽ thấy đầu ra tương tự:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

Mở `invoice_table.csv` và bạn sẽ thấy các hàng và cột phản ánh đúng hình ảnh gốc.

## Các Câu Hỏi Thường Gặp & Trường Hợp Cạnh

### Nếu hình ảnh là JPEG thay vì PNG thì sao?

Mã vẫn hoạt động—chỉ cần thay đổi phần mở rộng file trong `Image.FromFile`. Aspose OCR tự động phát hiện định dạng, vì vậy **extract tables from png** không phải là yêu cầu bắt buộc; nó hoạt động với bất kỳ bitmap nào được hỗ trợ.

### Bảng của tôi có các ô hợp nhất. Chúng có được giữ lại không?

Các ô hợp nhất sẽ được xử lý như các cột riêng biệt trong đầu ra CSV vì CSV không hỗ trợ việc kéo dài ô. Nếu bạn cần định dạng phong phú hơn (ví dụ Excel với ô hợp nhất), hãy dùng `SaveXls` thay thế:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### Bộ phát hiện bỏ lỡ một cột. Làm sao cải thiện độ chính xác?

- Tăng độ phân giải hình ảnh (≥300 dpi là lý tưởng).
- Tiền xử lý hình ảnh: chuyển sang grayscale, tăng độ tương phản, hoặc áp dụng bộ lọc deskew.
- Điều chỉnh các thiết lập Aspose OCR như `PageSegMode` hoặc `Language` nếu bảng chứa ký tự không phải Latin.

### Có thể trích xuất bảng trực tiếp từ PDF không?

Có. Đầu tiên chuyển mỗi trang PDF thành hình ảnh (sử dụng `Aspose.PDF` hoặc bất kỳ thư viện chuyển PDF‑to‑image nào), sau đó đưa các hình ảnh này vào cùng quy trình.

## Mẹo Để Triển Khai Sản Xuất

1. **Wrap OCR in a try/catch** – môi trường cấp phép qua mạng có thể ném ngoại lệ giấy phép.
2. **Dispose of `Image` objects** – bao bọc chúng trong khối `using` để giải phóng tài nguyên gốc.
3. **Log the confidence scores** – `TableExtractor` cung cấp `Table.Confidence` để bạn lưu trữ và giám sát chất lượng.
4. **Batch processing** – Khi xử lý hàng trăm hoá đơn, hãy song song hoá các lời gọi OCR nhưng vẫn tuân thủ hướng dẫn thread‑safety của giấy phép.

## Bước Tiếp Theo

Bây giờ bạn đã biết **cách trích xuất bảng** từ hình ảnh, có thể khám phá thêm:

- **Detect tables in image** video (sử dụng `TableExtractor` của Aspose trên từng khung hình).
- **Load image for OCR** từ một API web, cho phép dịch vụ trích xuất bảng dựa trên đám mây.
- **Extract tables from PNG** lưu trong Azure Blob Storage, tích hợp với Azure Functions để xử lý không máy chủ.

Hãy thử nghiệm với các định dạng file khác nhau, tinh chỉnh cài đặt OCR, hoặc truyền thẳng đầu ra CSV vào cơ sở dữ liệu. Không có giới hạn nào.

---

*Chúc lập trình vui vẻ! Nếu gặp khó khăn hoặc có ý tưởng cải tiến, hãy để lại bình luận bên dưới. Chúng ta sẽ cùng nhau giải quyết.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
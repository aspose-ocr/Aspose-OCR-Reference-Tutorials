---
category: general
date: 2026-03-18
description: Trích xuất bảng từ hình ảnh bằng Aspose OCR trong C#. Tìm hiểu cách chuyển
  bảng sang JSON, lấy JSON của bảng và trích xuất văn bản từ hình ảnh trong vài phút.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: vi
og_description: Trích xuất bảng từ hình ảnh bằng Aspose OCR trong C#. Học cách chuyển
  bảng sang JSON, lấy JSON của bảng và trích xuất văn bản từ hình ảnh nhanh chóng.
og_title: Trích xuất bảng từ hình ảnh bằng Aspose OCR – Hướng dẫn C# đầy đủ
tags:
- Aspose OCR
- C#
- Table Extraction
title: Trích xuất bảng từ hình ảnh bằng Aspose OCR – Hướng dẫn C# đầy đủ
url: /vi/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất bảng từ hình ảnh – Hướng dẫn đầy đủ C# 

Bạn đã bao giờ cần **extract table from image** nhưng không chắc thư viện nào có thể thực hiện mà không phải thực hiện một đống phân tích thủ công? Bạn không phải là người duy nhất. Trong nhiều dự án xử lý hoá đơn hoặc quét biên lai, điểm đau thực sự là chuyển một bitmap nhiễu thành một bảng có cấu trúc mà hệ thống hạ nguồn của bạn có thể tiêu thụ.  

Tin tốt? Với Aspose OCR bạn có thể **convert table to JSON** trong một vài dòng, và bạn cũng nhận được văn bản thuần của toàn bộ hình ảnh, vì vậy **extract text from image** là một phần thưởng. Trong hướng dẫn này chúng tôi sẽ đi qua toàn bộ quy trình – từ tải hình ảnh đến nhận một biểu diễn JSON gọn gàng của bảng được phát hiện.

> **Quick win:** Khi kết thúc, bạn sẽ có một ứng dụng console C# có thể chạy được, in cả văn bản OCR thô và một chuỗi JSON mà bạn có thể đưa thẳng vào cơ sở dữ liệu hoặc API.

## Yêu cầu trước

- .NET 6.0 SDK (hoặc bất kỳ phiên bản .NET gần đây nào) đã được cài đặt.  
- Giấy phép Aspose OCR hợp lệ hoặc bản dùng thử miễn phí (thư viện hoạt động mà không cần giấy phép nhưng sẽ thêm watermark).  
- Một hình ảnh thực sự chứa bảng – ví dụ `invoice_table.png`.  
- Visual Studio 2022, VS Code, hoặc bất kỳ trình chỉnh sửa nào bạn thích.

Không cần các gói NuGet bổ sung nào ngoài `Aspose.OCR`.

## Bước 1: Thiết lập dự án và cài đặt Aspose  OCR

Đầu tiên, tạo một dự án console mới và thêm thư viện OCR.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Nếu bạn đang sử dụng proxy công ty, thêm cờ `--no-restore` và chạy `dotnet restore` sau với các biến môi trường phù hợp.

## Bước 2: Khởi tạo OCR Engine và bật nhận dạng bảng

Trọng tâm của giải pháp là `OcrEngine`. Bằng cách bật `EnableTableRecognition` chúng ta nói với Aspose  OCR tìm các cấu trúc dạng lưới thay vì xử lý mọi thứ như văn bản thuần.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

Tại sao bước này quan trọng? Nếu không bật nhận dạng bảng, engine sẽ làm phẳng hình ảnh thành một chuỗi duy nhất, khiến việc tái tạo các hàng và cột sau này trở nên không thể. Bật tính năng này thêm một giai đoạn phân tích bố cục nhẹ, gần như không tốn hiệu năng nhưng mang lại lợi ích lớn cho các bước tiếp theo.

## Bước 3: Tải hình ảnh của bạn và chạy nhận dạng

Bây giờ chúng ta chỉ định engine tới tệp chứa bảng. `ImageStream.FromFile` hỗ trợ hầu hết các định dạng phổ biến (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Nếu hình ảnh quá lớn, hãy cân nhắc thay đổi kích thước trước để tăng tốc xử lý. Aspose  OCR tự động phát hiện DPI, nhưng quét 300 DPI là mức lý tưởng cho hầu hết các bảng.

## Bước 4: Trích xuất văn bản thuần – “extract text from image”

Mặc dù mục tiêu chính của chúng ta là bảng, bạn thường vẫn cần văn bản thô để ghi log hoặc xử lý dự phòng.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

Thuộc tính `Text` nối tất cả những gì engine nhận thấy, giữ nguyên các ngắt dòng. Điều này hữu ích khi bạn cần xác minh rằng OCR đã đọc đúng tiêu đề hoặc chân trang ngoài khu vực bảng.

## Bước 5: Lấy bảng đã phát hiện dưới dạng JSON – “convert table to json” & “get table json”

Đây là nơi phép thuật xảy ra. `GetTableAsJson()` tuần tự hoá các hàng, cột và nội dung ô đã phát hiện thành một chuỗi JSON sạch sẽ.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

JSON kết quả trông giống như sau (được định dạng để dễ đọc):

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

Tại sao JSON là định dạng ưu tiên? Nó không phụ thuộc ngôn ngữ, dễ dàng giải tuần tự thành các đối tượng, và hoạt động tốt với các API web hiện đại. Nếu bạn cần CSV thay thế, chỉ cần lặp qua các hàng và nối các văn bản ô bằng dấu phẩy.

## Bước 6: (Tùy chọn) Chuyển JSON thành đối tượng .NET – “convert image to json”

Nếu bạn thích làm việc với kiểu mạnh, hãy giải tuần tự JSON bằng `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Bạn sẽ định nghĩa `TableModel`, `RowModel`, và `CellModel` để phù hợp với schema JSON. Bước này cho thấy cách bạn có thể chuyển từ **convert image to json** tới một đối tượng có kiểu, giúp việc xác thực ở các bước sau trở nên dễ dàng.

## Ví dụ hoạt động đầy đủ

Kết hợp mọi thứ lại, đây là chương trình hoàn chỉnh, sẵn sàng chạy. Lưu nó dưới tên `Program.cs` trong thư mục dự án đã tạo trước đó.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### Kết quả mong đợi

Khi bạn chạy `dotnet run`, bạn sẽ thấy một kết quả tương tự như:

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

Nếu đầu ra trông trống, hãy kiểm tra lại rằng `EnableTableRecognition` được đặt thành `true` và hình ảnh thực sự chứa các đường lưới rõ ràng.

## Các lỗi thường gặp & Cách tránh

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Không có JSON trả về** | Phát hiện bảng bị tắt hoặc hình ảnh có độ tương phản quá thấp. | Đảm bảo `ocrEngine.Settings.EnableTableRecognition = true` và cải thiện chất lượng hình ảnh (tăng độ tương phản, nhị phân hoá). |
| **Các hàng không đầy đủ** | OCR bị nhầm lẫn do các ô hợp nhất hoặc văn bản bị xoay. | Tiền xử lý hình ảnh: chỉnh nghiêng (`ImageProcessor.Rotate`) hoặc tách các ô hợp nhất thủ công. |
| **Ký tự Unicode rối** | Phông chữ không được nhận dạng (ví dụ: viết tay). | Chuyển gói ngôn ngữ qua `ocrEngine.Language = Language.English;` hoặc sử dụng engine OCR khác cho văn bản viết tay. |
| **Chậm hiệu năng** | Hình ảnh quá lớn (>5 MP). | Giảm kích thước xuống khoảng 1500 px chiều rộng trong khi giữ DPI. |

## Các bước tiếp theo: Vượt ra ngoài những kiến thức cơ bản

Bây giờ bạn có thể **extract table from image** và **convert table to JSON**, hãy xem xét các mở rộng sau:

- **Lưu JSON** vào cơ sở dữ liệu bằng Entity Framework.  
- **Xử lý hậu** JSON để chuẩn hoá định dạng tiền tệ (ví dụ: loại bỏ `$`).  
- **Xử lý hàng loạt** một thư mục hoá đơn bằng `Directory.GetFiles` và song song hoá với `Parallel.ForEach`.  
- **Tích hợp** với Azure Functions hoặc AWS Lambda cho các pipeline OCR không máy chủ.  

Mỗi chủ đề đó tự nhiên sẽ đưa vào các từ khóa phụ như **convert image to json** (khi bạn gửi toàn bộ kết quả OCR tới một endpoint đám mây) và **get table json** cho phân tích hạ nguồn.

---

### Kết luận

Chúng tôi vừa cho bạn thấy cách **extract table from image** bằng Aspose OCR, chuyển bảng đó thành JSON sạch sẽ, và thậm chí giải tuần tự nó thành các đối tượng C#. Mẫu tương tự

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
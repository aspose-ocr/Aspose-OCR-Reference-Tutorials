---
category: general
date: 2026-03-02
description: Tìm hiểu cách lưu JSON khi trích xuất văn bản từ hình ảnh bằng Aspose
  OCR. Bao gồm mã ghi file JSON, mẹo tải ảnh bitmap và ví dụ đầy đủ bằng C#.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: vi
og_description: Khám phá cách lưu JSON khi trích xuất văn bản từ hình ảnh bằng Aspose
  OCR. Mã C# đầy đủ, các bước ghi file JSON và các mẹo thực tế.
og_title: Cách Lưu JSON Từ OCR trong C# – Hướng Dẫn Lập Trình Đầy Đủ
tags:
- C#
- OCR
- Aspose
- JSON
title: Cách Lưu JSON Từ OCR trong C# – Hướng Dẫn Chi Tiết Từng Bước
url: /vi/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Lưu JSON từ OCR trong C# – Hướng Dẫn Chi Tiết Từng Bước

Bạn đã bao giờ tự hỏi **cách lưu JSON** chứa văn bản bạn vừa trích xuất từ một bức ảnh chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần *trích xuất văn bản từ dữ liệu hình ảnh* và sau đó lưu thông tin đó dưới dạng một tệp JSON được định dạng gọn gàng. Tin tốt là gì? Giải pháp khá đơn giản một khi bạn có các thành phần cần thiết.

Trong tutorial này, chúng ta sẽ đi qua một kịch bản thực tế: sử dụng Aspose.OCR để **trích xuất văn bản từ hình ảnh**, sau đó **ghi tệp JSON**, và cuối cùng **cách lưu JSON** lên đĩa. Trong quá trình này, chúng ta cũng sẽ chỉ cho bạn cách **tải đối tượng bitmap image** một cách đúng đắn, và đề cập một vài trường hợp đặc biệt mà bạn có thể gặp. Khi kết thúc, bạn sẽ có một ứng dụng console C# tự chứa, thực hiện mọi thứ từ tải ảnh đến tạo ra một tài liệu JSON sẵn sàng sử dụng.

## Những Gì Bạn Cần Chuẩn Bị

- .NET 6.0 trở lên (mã cũng hoạt động với .NET Core và .NET Framework)
- Aspose.OCR for .NET (bạn có thể tải gói NuGet dùng thử miễn phí)
- Một ảnh PNG hoặc JPG mẫu chứa văn bản tiếng Anh
- Visual Studio, VS Code, hoặc bất kỳ IDE nào hỗ trợ C#

Không cần thư viện bổ sung—chỉ cần namespace chuẩn `System.Drawing` để xử lý bitmap và `System.Text.Json` để tuần tự hoá.

---

## Bước 1 – Tải Bitmap Image (phần “load bitmap image”)

Trước khi OCR có thể thực hiện, bạn phải đưa ảnh vào bộ nhớ dưới dạng `Bitmap`. Hãy nghĩ đây như việc mở một cuốn sách trước khi bắt đầu đọc các trang của nó.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **Mẹo:** Nếu ảnh quá lớn, hãy cân nhắc thu nhỏ nó trước để cải thiện hiệu năng. Engine OCR hoạt động nhanh hơn trên các ảnh dưới 2 MB.

---

## Bước 2 – Cấu Hình Aspose OCR Engine

Bây giờ bitmap đã sẵn sàng, chúng ta cần một `OcrEngine`. Đối tượng này biết cách **trích xuất văn bản từ hình ảnh** và tùy chọn cung cấp dữ liệu hình học như bounding box.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

Tại sao bật `ExportBoundingBoxes`? Nếu bạn muốn làm nổi bật các từ trong UI, các tọa độ này rất hữu ích. Nếu không cần, bạn có thể đặt flag này thành `false` và JSON sẽ nhẹ hơn một chút.

---

## Bước 3 – Thực Hiện OCR và Nhận Kết Quả Có Cấu Trúc

Với engine đã được cấu hình, bước tiếp theo là thực hiện **cách trích xuất văn bản** thực sự. Phương thức `RecognizeToOcrResult` trả về một đối tượng phong phú chứa văn bản đã nhận dạng, điểm tin cậy, và dữ liệu bố cục tùy chọn.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

Biến `ocrResult` giờ đã chứa mọi thứ bạn cần. Nếu bạn kiểm tra trong debugger, sẽ thấy một cây phân cấp gồm các đối tượng `Page`, `Paragraph`, `Line`, và `Word`, mỗi cái có thuộc tính `Text` riêng.

---

## Bước 4 – Tuần Tự Hoá Kết Quả Thành Chuỗi JSON Định Dạng

Đây là nơi **cách lưu json** thực sự bắt đầu. Chúng ta sẽ dùng `System.Text.Json` vì nó đã được tích hợp, nhanh và hỗ trợ in đẹp (pretty printing) ngay từ đầu.

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Nếu bạn cần quy tắc đặt tên khác (ví dụ camelCase), chỉ cần thêm `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` vào options.

---

## Bước 5 – Ghi JSON Lên Đĩa (bước “write json file”)

Cuối cùng, chúng ta **ghi tệp JSON** vào hệ thống file. Đây là câu trả lời cụ thể cho **cách lưu json** trong môi trường C#.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

Sau khi dòng lệnh này thực thi, bạn sẽ thấy một file `sample-page.json` được căn chỉnh đẹp mắt nằm cạnh ảnh gốc. Mở nó bằng bất kỳ trình soạn thảo văn bản nào hoặc truyền vào dịch vụ khác—dữ liệu OCR của bạn đã sẵn sàng di chuyển.

---

## Bước 6 – Kiểm Tra Kết Quả (Bạn Sẽ Nhìn Thấy Gì?)

Chạy chương trình sẽ in một thông báo ngắn trên console:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

Mở file JSON đã tạo và bạn sẽ thấy nội dung tương tự:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Nếu flag `ExportBoundingBoxes` được bật, mỗi từ cũng sẽ chứa tọa độ `Rectangle`. Điều này rất tiện cho công việc UI phía sau.

---

## Các Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Ảnh không tồn tại hoặc đường dẫn sai?

Bao quanh việc tải bitmap bằng khối `try/catch` và đưa ra lỗi rõ ràng:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### Làm sao xử lý ngôn ngữ không phải tiếng Anh?

Chỉ cần thay đổi thuộc tính `Language`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose hỗ trợ hơn 50 ngôn ngữ, vì vậy hãy chọn ngôn ngữ phù hợp với tài liệu nguồn của bạn.

### Có cần giải phóng đối tượng `Bitmap` không?

Có. `Bitmap` triển khai `IDisposable`, vì vậy hãy bao quanh nó bằng câu lệnh `using` để giải phóng tài nguyên gốc kịp thời.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### Muốn JSON gọn hơn, không có thụt lề?

Thay đổi `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

Điều này sẽ giảm kích thước tệp—hữu ích trong các kịch bản băng thông hạn chế.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là chương trình đầy đủ tích hợp tất cả các bước, xử lý lỗi, và các mẹo thực tiễn đã thảo luận. Lưu lại dưới tên `Program.cs` và chạy từ dòng lệnh hoặc IDE của bạn.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**Chức năng của đoạn mã:**  
1. Kiểm tra xem ảnh có tồn tại hay không.  
2. Tải ảnh một cách an toàn bằng khối `using`.  
3. Thực hiện OCR để **trích xuất văn bản từ hình ảnh**.  
4. Tuần tự hoá kết quả thành chuỗi JSON được căn chỉnh đẹp.  
5. Lưu chuỗi này lên đĩa, trả lời câu hỏi cốt lõi **cách lưu json**.

Chạy `dotnet run` (hoặc nhấn F5 trong Visual Studio) và bạn sẽ thấy thông báo xác nhận khi tệp đã được ghi.

---

## Kết Luận

Bạn đã có một công thức hoàn chỉnh, sẵn sàng cho môi trường production để **cách lưu JSON** xuất phát từ việc trích xuất văn bản bằng OCR. Từ việc tải bitmap image đến việc ghi một tệp JSON sạch sẽ, mỗi bước đều được giải thích kèm “tại sao” phía sau mã, giúp bạn dễ dàng tùy chỉnh giải pháp cho dự án của mình.

Nếu bạn muốn khám phá bước tiếp theo, hãy cân nhắc:

- **Cách trích xuất văn bản** từ PDF bằng cách chuyển mỗi trang thành ảnh trước.  
- Sử dụng dữ liệu bounding‑box để làm nổi bật từ trong UI WPF hoặc WinForms.  
- Stream JSON trực tiếp tới một Web API thay vì ghi tệp (dùng `HttpClient`).

Hãy thử, điều chỉnh các tùy chọn, và để dữ liệu OCR phục vụ cho bất kỳ ứng dụng nào bạn đang xây dựng. Có câu hỏi? Để lại bình luận, chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
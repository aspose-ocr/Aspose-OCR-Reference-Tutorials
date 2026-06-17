---
category: general
date: 2026-03-15
description: Cách sử dụng Aspose OCR để trích xuất văn bản từ hình ảnh và chuyển đổi
  hình ảnh sang JSON trong C#. Học cách nhận dạng văn bản từ PNG và nhận kết quả có
  cấu trúc nhanh chóng.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: vi
og_description: Cách sử dụng Aspose OCR để trích xuất văn bản từ hình ảnh và chuyển
  đổi hình ảnh sang JSON trong C#. Hướng dẫn này sẽ chỉ cho bạn cách nhận dạng văn
  bản từ PNG và nhận được đầu ra có cấu trúc.
og_title: Cách sử dụng Aspose OCR để chuyển đổi hình ảnh sang JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Cách sử dụng Aspose OCR để chuyển đổi hình ảnh sang JSON
url: /vi/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng Aspose OCR Để Chuyển Đổi Hình Ảnh Sang JSON

Cách sử dụng Aspose OCR là một câu hỏi phổ biến khi các nhà phát triển cần trích xuất văn bản từ hình ảnh. Nếu bạn muốn **convert image to JSON** hoặc **recognize text from PNG**, hướng dẫn này sẽ đáp ứng nhu cầu của bạn—không thừa thãi, chỉ cung cấp giải pháp thực tế, từ đầu đến cuối.

Trong vài phút tới, chúng ta sẽ đi qua mọi thứ bạn cần: cài đặt thư viện, cấu hình engine để xuất JSON, tải một file PNG hoá đơn, chạy OCR, và cuối cùng ghi kết quả vào file `.json`. Khi kết thúc, bạn sẽ có thể **extract text from image** chỉ với một lời gọi phương thức, và bạn sẽ hiểu tại sao mỗi bước lại quan trọng.

> **Pro tip:** Aspose OCR hỗ trợ nhiều định dạng ảnh (PNG, JPEG, BMP, TIFF). Đoạn mã dưới đây sẽ xử lý tất cả chúng, vì vậy bạn không cần viết logic riêng cho từng định dạng.

## Những Gì Bạn Cần

- .NET 6.0 trở lên (mã cũng hoạt động trên .NET Framework 4.6+)
- Gói Aspose.OCR NuGet hợp lệ (bản dùng thử miễn phí hoặc có giấy phép)
- File ảnh bạn muốn xử lý (ví dụ, `receipt.png`)
- Visual Studio, VS Code, hoặc bất kỳ trình soạn thảo C# nào bạn thích  

Chỉ vậy—không phụ thuộc thêm, không dịch vụ bên ngoài. Sẵn sàng? Hãy bắt đầu.

![cách sử dụng engine Aspose OCR](image-placeholder.png "cách sử dụng engine Aspose OCR")

## Cách Sử Dụng Aspose OCR – Cấu Hình Đầu Ra JSON

Điều đầu tiên bạn cần làm khi **how to use aspose** cho OCR là tạo một thể hiện `OcrEngine` và chỉ định nó xuất ra JSON. Công tắc cấu hình nhỏ này giúp bạn tránh việc phải tự serialize kết quả sau này.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Why this matters:** Việc đặt `OutputFormat` thành `Json` có nghĩa là engine OCR đã sắp xếp văn bản thành một cấu trúc phân cấp gồm các trang, dòng và từ. Bạn không cần phải phân tích chuỗi thô sau này, điều này làm cho việc xử lý tiếp theo—như đưa dữ liệu vào cơ sở dữ liệu—gọn gàng hơn.

## Chuyển Đổi Hình Ảnh Sang JSON Với Aspose OCR

Bây giờ engine đã được cấu hình, hãy nói chi tiết hơn về phần **convert image to JSON**.

1. **Load the image** – `Image.FromFile` hoạt động với bất kỳ định dạng hỗ trợ nào. Nếu bạn đang làm việc với một stream (ví dụ, file được tải lên), bạn có thể dùng `Image.FromStream` thay thế.  
2. **Run `Recognize`** – phương thức này trả về một đối tượng `OcrResult`. Vì chúng ta đã đặt đầu ra là JSON, `ocrResult.Text` đã chứa một chuỗi JSON.  
3. **Write the file** – `File.WriteAllText` là cách đơn giản nhất để lưu JSON. Nếu bạn cần lưu vào một bucket trên cloud, chỉ cần thay dòng này bằng lời gọi SDK phù hợp.

### Đầu Ra JSON Dự Kiến

Một payload JSON điển hình trông như sau (được rút gọn để ngắn gọn):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Bây giờ bạn có thể đưa cấu trúc này vào bất kỳ hệ thống downstream nào—cho dù là công cụ báo cáo, mô hình machine‑learning, hay một file log đơn giản.

## Trích Xuất Văn Bản Từ Hình Ảnh Bằng Aspose OCR

Nếu bạn chỉ cần chuỗi thô (tức là không quan tâm tới JSON), chỉ cần chuyển định dạng đầu ra về plain text:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**When to choose plain text?**  
- Gỡ lỗi nhanh hoặc xuất ra console.  
- Các trường hợp bạn sẽ áp dụng post‑processing tùy chỉnh (ví dụ, trích xuất bằng regex).  

Nhưng hãy nhớ, **extract text from image** sử dụng JSON sẽ cung cấp dữ liệu vị trí—hữu ích cho việc làm nổi bật văn bản trong UI hoặc căn chỉnh với các trường biểu mẫu.

## Nhận Diện Văn Bản Từ File PNG

PNG là định dạng không mất dữ liệu, thường cho độ chính xác OCR tốt hơn so với JPEG nén mạnh. Dưới đây là danh sách nhanh để đảm bảo bạn đạt kết quả tốt nhất khi **recognize text from PNG**:

| Mục Kiểm Tra | Lý Do Giúp |
|--------------|------------|
| Sử dụng DPI 300+ | Độ phân giải cao hơn cung cấp cho engine nhiều pixel hơn để xử lý. |
| Giữ ảnh ở dạng grayscale | Giảm nhiễu; Aspose OCR tự động chuyển đổi, nhưng tiền xử lý có thể tăng tốc. |
| Xóa nhiễu nền | Nền sạch sẽ cải thiện điểm tin cậy. |

Nếu bạn gặp điểm tin cậy thấp, hãy thử tăng DPI hoặc áp dụng bộ lọc ngưỡng đơn giản trước khi đưa ảnh vào Aspose.

## Cách Trích Xuất Kết Quả OCR Theo Chương Trình

Ngoài việc lưu JSON, bạn có thể muốn đọc các trường cụ thể theo chương trình—ví dụ, tổng số tiền trên hoá đơn. Vì JSON chứa cấu trúc phân cấp, bạn có thể deserialize nó thành một đối tượng C#:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Bây giờ bạn có thể truy vấn `ocrData` bằng LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Why this works:** JSON đã cho bạn biết vị trí của mỗi từ trên trang, vì vậy bạn có thể xác định trường một cách đáng tin cậy ngay cả khi bố cục thay đổi nhẹ.

## Các Trường Hợp Cạnh & Những Cạm Bẫy Thông Thường

- **Null Result:** Nếu `ocrEngine.Recognize` trả về `null`, ảnh có thể không được hỗ trợ hoặc bị hỏng. Luôn kiểm tra trước:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Large Files:** Đối với các ảnh đa megabyte, hãy cân nhắc stream ảnh hoặc thay đổi kích thước trước khi OCR để tránh sử dụng bộ nhớ quá mức.

- **License Issues:** Phiên bản dùng thử sẽ thêm watermark vào đầu ra. Đảm bảo bạn tải giấy phép sớm trong chương trình:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Non‑Latin Scripts:** Aspose OCR hỗ trợ nhiều ngôn ngữ, nhưng bạn phải đặt thuộc tính `Language` cho phù hợp (ví dụ, `ocrEngine.Configuration.Language = Language.English;`).

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
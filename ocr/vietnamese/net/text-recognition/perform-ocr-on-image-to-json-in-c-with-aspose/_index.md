---
category: general
date: 2026-04-08
description: Học cách thực hiện OCR trên hình ảnh và ghi file JSON bằng C# sử dụng
  Aspose OCR. Hướng dẫn Aspose OCR C# này cho thấy việc chuyển đổi OCR hình ảnh sang
  JSON kèm các giá trị độ tin cậy.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: vi
og_description: Thực hiện OCR trên hình ảnh và xuất kết quả ra tệp JSON trong C#.
  Hướng dẫn này bao gồm toàn bộ quy trình làm việc Aspose OCR C#, bao gồm cả độ tin
  cậy.
og_title: Thực hiện OCR trên hình ảnh thành JSON trong C# – Hướng dẫn OCR của Aspose
tags:
- Aspose
- OCR
- C#
- JSON
title: Thực hiện OCR trên hình ảnh thành JSON trong C# với Aspose
url: /vi/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên hình ảnh và chuyển sang JSON trong C# với Aspose

Bạn đã bao giờ cần **thực hiện OCR trên các tệp hình ảnh** nhưng không chắc làm sao đưa kết quả vào định dạng có cấu trúc? Bạn không đơn độc—các nhà phát triển thường hỏi: “Làm sao biến một bức ảnh quét thành dữ liệu có thể sử dụng?” Tin tốt là Aspose.OCR làm cho việc này trở nên dễ dàng, và bạn thậm chí có thể **ghi tệp JSON C#**‑style kèm theo các chỉ số confidence.

Trong hướng dẫn này, chúng ta sẽ đi qua một **aspose OCR C# tutorial** hoàn chỉnh, bao gồm mọi bước từ tải ảnh đến xuất văn bản đã nhận dạng dưới dạng JSON. Khi kết thúc, bạn sẽ có một ứng dụng console có thể **thực hiện OCR trên hình ảnh**, chuyển kết quả sang JSON (kèm giá trị confidence), và lưu lại chỉ với một dòng lệnh. Không có bước ẩn, không có script bên ngoài—chỉ thuần C#.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn đã có:

- .NET 6.0 SDK hoặc mới hơn (mã cũng chạy được với .NET Core và .NET Framework)
- Visual Studio 2022 (hoặc bất kỳ trình soạn thảo nào bạn thích)
- Giấy phép **Aspose.OCR for .NET** hợp lệ hoặc giấy phép tạm thời miễn phí (bản dùng thử miễn phí đủ cho việc thử nghiệm)
- Một tệp hình ảnh (`input.png`) bạn muốn xử lý (bất kỳ định dạng phổ biến nào—PNG, JPG, BMP—cũng được)

Đó là tất cả. Nếu thiếu bất kỳ mục nào, hãy tải về ngay; các phần còn lại của tutorial giả định rằng chúng đã sẵn sàng.

## Bước 1: Cài đặt gói NuGet Aspose.OCR

Điều đầu tiên—thêm thư viện vào dự án. Mở terminal trong thư mục dự án và chạy:

```bash
dotnet add package Aspose.OCR
```

Lệnh này sẽ tải phiên bản mới nhất (tính đến tháng 4 2026 là 23.12) và thêm các DLL cần thiết vào thư mục `bin`. Không cần cấu hình thêm nào.

## Bước 2: Khởi tạo OCR Engine (Perform OCR on Image)

Bây giờ chúng ta tạo một thể hiện `OcrEngine` và chỉ định ngôn ngữ sẽ dùng. Tiếng Anh (`"en"`) là phổ biến nhất, nhưng bạn có thể đổi thành `"fr"`, `"de"` hoặc bất kỳ ngôn ngữ nào được hỗ trợ.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Lý do khởi tạo ở đây:** `OcrEngine` chứa toàn bộ cấu hình cần thiết cho quá trình nhận dạng. Đặt ngôn ngữ từ đầu giúp engine sử dụng đúng bộ ký tự, từ đó cải thiện đáng kể độ chính xác.

## Bước 3: Nhận dạng ảnh và lấy Confidence

Khi engine đã sẵn sàng, chúng ta truyền cho nó tệp ảnh. Phương thức `RecognizeImage` trả về một đối tượng `OcrResult` chứa cả văn bản đã trích xuất và chỉ số confidence cho mỗi từ.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Đằng sau màn hình:** Aspose chạy một bộ nhận dạng dựa trên neural‑network, phân tích từng khối pixel, so sánh với mô hình ngôn ngữ và gắn kèm giá trị confidence (0‑100) cho mỗi từ.

## Bước 4: Chuyển kết quả sang JSON (OCR Image to JSON)

Aspose làm cho việc chuyển đổi trở nên đơn giản. Khi truyền `includeConfidence: true` chúng ta nhận được payload JSON như sau:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Đây là đoạn mã tạo chuỗi JSON:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Tại sao cần confidence?** Nếu bạn định đưa dữ liệu vào các quy trình downstream (ví dụ: kiểm tra, tô sáng UI), việc biết từ nào có độ tin cậy thấp sẽ giúp quyết định có nên yêu cầu người dùng xác nhận hay không.

## Bước 5: Ghi tệp JSON C#‑Style

Bây giờ chúng ta thực sự **write JSON file C#**. Phương thức `File.WriteAllText` là nguyên tử và hoạt động đa nền tảng, rất phù hợp cho các ứng dụng console.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Đó là toàn bộ quy trình—năm bước ngắn gọn để **perform OCR on image**, chuyển đầu ra sang JSON và lưu lại.

## Ví dụ Hoạt động Đầy đủ

Dưới đây là chương trình hoàn chỉnh bạn có thể sao chép‑dán vào `Program.cs`. Đảm bảo `input.png` nằm trong cùng thư mục với binary đã biên dịch hoặc điều chỉnh đường dẫn cho phù hợp.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Kết quả Dự Kiến

Khi bạn chạy chương trình (`dotnet run`), sẽ thấy đầu ra tương tự:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

Và `output.json` sẽ chứa JSON có cấu trúc như đã trình bày ở trên, bao gồm phần trăm confidence cho mỗi từ.

## Mẹo Chuyên Gia & Các Trường Hợp Cạnh

- **Xử lý file thiếu:** Bao quanh lời gọi `RecognizeImage` bằng `try/catch` cho `FileNotFoundException` nếu bạn dùng đường dẫn động.
- **Ngôn ngữ khác:** Đặt `ocrEngine.Language = "fr"` cho tiếng Pháp, hoặc tải gói ngôn ngữ tùy chỉnh bằng `ocrEngine.LoadLanguage("custom.lang")`.
- **Tài liệu lớn:** Đối với PDF đa trang, trước tiên chuyển mỗi trang thành ảnh (ví dụ: dùng `Aspose.PDF`) rồi lặp lại các bước OCR.
- **Tinh chỉnh hiệu năng:** Nếu chỉ cần kết quả nhanh, chuyển sang `RecognitionMode.Fast`—bạn sẽ mất một chút độ chính xác nhưng tăng tốc độ.
- **Định dạng JSON:** Muốn JSON được in đẹp? Dùng `JsonConvert.SerializeObject` từ Newtonsoft với `Formatting.Indented` sau khi giải mã chuỗi JSON của Aspose.

## Câu Hỏi Thường Gặp

**Q: Điều này có hoạt động với .NET Framework không?**  
A: Hoàn toàn có. Gói NuGet này cũng nhắm tới .NET Standard 2.0, vì vậy bạn có thể tham chiếu từ .NET Framework 4.6.1 trở lên.

**Q: Nếu tôi cần confidence cho toàn bộ tài liệu, không phải từng từ?**  
A: `OcrResult` còn cung cấp `OverallConfidence`. Bạn có thể thêm nó thủ công vào JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: Tôi có thể stream JSON trực tiếp tới một web API không?**  
A: Có. Thay `File.WriteAllText` bằng một POST của `HttpClient` để gửi `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
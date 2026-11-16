---
category: general
date: 2026-04-26
description: Trích xuất văn bản từ các tệp PNG nhanh chóng bằng C#. Tìm hiểu cách
  chuyển đổi hình ảnh thành văn bản, đọc tệp PNG, lặp qua các hình ảnh và thực hiện
  OCR hàng loạt trong vài phút.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: vi
og_description: Trích xuất văn bản từ các tệp PNG nhanh chóng bằng C#. Hướng dẫn này
  chỉ cách chuyển đổi hình ảnh thành văn bản, đọc tệp PNG, lặp qua các hình ảnh và
  thực hiện OCR hàng loạt cho chúng.
og_title: Trích xuất văn bản từ PNG – Hướng dẫn OCR batch C# hoàn chỉnh
tags:
- C#
- OCR
- Aspose
title: Trích xuất văn bản từ PNG – Hướng dẫn OCR batch đầy đủ bằng C#
url: /vi/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ PNG – Hướng dẫn OCR C# Batch hoàn chỉnh

Bạn đã bao giờ cần **trích xuất văn bản từ các tệp PNG** nhưng không biết bắt đầu từ đâu? Bạn không cô đơn—nhiều lập trình viên gặp khó khăn này khi lần đầu tiên thử OCR trên một thư mục chứa ảnh chụp màn hình. Tin tốt là chỉ với vài dòng C# và Aspose OCR, bạn có thể chuyển đổi hình ảnh thành văn bản, đọc tệp PNG, lặp qua các ảnh, và xử lý hàng loạt mọi thứ trong một lần chạy.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ứng dụng console đã sẵn sàng chạy, thực hiện đúng những gì trên. Khi kết thúc, bạn sẽ có một giải pháp tự chứa, lấy văn bản ra khỏi mọi PNG trong một thư mục và tạo một tệp `.txt` tương ứng bên cạnh mỗi ảnh. Không cần script phụ, không cần sao chép‑dán thủ công—chỉ cần mã.

## Những gì bạn cần

- **.NET 6 SDK** (hoặc bất kỳ phiên bản .NET nào mới hơn). Miễn phí, nhanh, và hoạt động ở mọi nơi.
- **Aspose.OCR for .NET** (gói NuGet). Thư viện bao gồm tăng tốc GPU nếu bạn có GPU tương thích, nhưng cũng tự động chuyển sang CPU nếu không.
- Một thư mục chứa một vài **hình ảnh PNG** bạn muốn xử lý.  
- Trình soạn thảo văn bản hoặc IDE—Visual Studio, VS Code, Rider—bất kỳ gì bạn thích.

Đó là tất cả. Nếu bạn đã có những thứ trên, bạn đã sẵn sàng bắt đầu.

![ví dụ trích xuất văn bản từ png](image.png "ảnh chụp màn hình demo trích xuất văn bản từ png")

*Văn bản thay thế ảnh: “trích xuất văn bản từ png bằng OCR batch C#”*

## Bước 1 – Thiết lập dự án và cài đặt Aspose.OCR

Đầu tiên, tạo một dự án console mới và thêm gói Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Tại sao chúng ta dùng ứng dụng console? Đó là môi trường đơn giản nhất cho các công việc batch, và bạn có thể chạy nó từ dòng lệnh hoặc lên lịch bằng một task runner. Nếu sau này bạn cần giao diện UI, bạn chỉ cần chuyển logic cốt lõi vào một class library.

## Bước 2 – Khởi tạo Engine OCR tăng tốc GPU (hoặc fallback CPU)

Aspose cung cấp một `GpuOcrEngine` tự động phát hiện GPU hỗ trợ. Nếu không tìm thấy, nó sẽ quay lại engine CPU thông thường—không cần viết mã bổ sung.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Mẹo chuyên nghiệp:** Nếu bạn đang chạy trên server không có GPU, bạn có thể thay `GpuOcrEngine` bằng `OcrEngine` và mã sẽ hoạt động giống hệt.

## Bước 3 – Lặp qua các ảnh trong thư mục mục tiêu

Chúng ta cần **lặp qua các ảnh** và chỉ chọn các tệp PNG. Phương thức `Directory.GetFiles` thực hiện phần lớn công việc, và chúng ta sẽ kiểm tra trường hợp thư mục rỗng.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Chú ý việc sử dụng `SearchOption.TopDirectoryOnly`. Nếu sau này bạn muốn duyệt đệ quy vào các thư mục con, chỉ cần chuyển sang `AllDirectories`. Thay đổi nhỏ này cho phép bạn **chuyển đổi hình ảnh thành văn bản** trong toàn bộ cây thư mục chỉ bằng một dòng.

## Bước 4 – Thực hiện OCR và lưu kết quả

Bây giờ là phần cốt lõi của quy trình **batch OCR images**. Chúng ta tải mỗi PNG, chạy `Recognize()`, và ghi chuỗi đã trích xuất vào tệp `.txt` có cùng tên cơ sở.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Tại sao lại bọc trong try/catch?** Các batch ảnh thực tế thường chứa tệp hỏng hoặc PNG sử dụng profile màu không phổ biến. Bắt ngoại lệ ngăn toàn bộ quá trình bị sập và cho phép tiếp tục xử lý các tệp còn lại.

## Bước 5 – Chạy ứng dụng và kiểm tra đầu ra

Biên dịch và khởi chạy ứng dụng:

```bash
dotnet run
```

Bạn sẽ thấy log console tương tự như:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Mở bất kỳ tệp `.txt` nào đã tạo—đó là văn bản đã được trích xuất. Nếu tệp rỗng, hãy kiểm tra lại chất lượng ảnh; OCR hoạt động tốt nhất với văn bản rõ, độ tương phản cao.

### Script kiểm tra nhanh (tùy chọn)

Nếu bạn muốn chắc chắn mọi PNG đều có tệp văn bản tương ứng, chạy dòng PowerShell ngắn gọn này:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Các biến thể thường gặp & Trường hợp đặc biệt

| Tình huống | Cần thay đổi gì |
|-----------|----------------|
| **Ngôn ngữ không phải Latin** (ví dụ: Cyrillic) | Đặt `ocrEngine.Language = Language.Cyrillic;` |
| **Bộ ảnh lớn (>10 000 tệp)** | Sử dụng `Parallel.ForEach` để tăng tốc xử lý, nhưng cần giám sát việc sử dụng bộ nhớ GPU. |
| **Cần giữ thứ tự ảnh gốc** | Sắp xếp `pngFiles` trước vòng `foreach` (`Array.Sort(pngFiles);`). |
| **Chạy trên server CI không có GPU** | Thay `GpuOcrEngine` bằng `OcrEngine` để tránh lỗi khởi tạo GPU. |
| **Chỉ muốn xử lý các tệp chứa từ khóa cụ thể** | Sau khi lấy `result.Text`, kiểm tra `result.Text.Contains("Invoice")` trước khi ghi tệp. |

Những điều chỉnh này cho phép bạn tùy biến quy trình **chuyển đổi hình ảnh thành văn bản** cho hầu hết các kịch bản bạn gặp phải.

## Toàn bộ mã nguồn (Sẵn sàng sao chép‑dán)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Lưu lại dưới tên `Program.cs`, chạy `dotnet run`, và xem kết quả.

## Kết luận

Bây giờ bạn đã có **cách hoàn chỉnh, sẵn sàng sản xuất để trích xuất văn bản từ các tệp PNG** bằng C#. Hướng dẫn đã bao quát mọi thứ—from thiết lập dự án, khởi tạo engine OCR tăng tốc GPU, **lặp qua các ảnh**, đến **batch OCR images** và lưu kết quả dưới dạng văn bản thuần.  

Nếu bạn muốn khám phá các bước tiếp theo, hãy thử:

- **Chuyển đổi hình ảnh thành văn bản** cho các định dạng khác (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
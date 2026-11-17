---
category: general
date: 2026-03-23
description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR trong C# và học cách thêm
  logger console để nhận phản hồi thời gian thực.
draft: false
keywords:
- extract text from image
- add console logger
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR và thêm bộ ghi nhật
  ký console để giám sát quá trình. Hướng dẫn C# từng bước.
og_title: Trích xuất văn bản từ hình ảnh trong C# – Hướng dẫn lập trình toàn diện
tags:
- OCR
- C#
- logging
title: Trích xuất văn bản từ hình ảnh trong C# – Hướng dẫn đầy đủ
url: /vi/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh trong C# – Hướng dẫn đầy đủ

Cần **trích xuất văn bản từ hình ảnh** một cách nhanh chóng và đáng tin cậy? Với Aspose OCR, bạn có thể làm điều đó chỉ trong vài dòng C#.  
Chúng tôi cũng sẽ chỉ cho bạn cách **thêm logger console** để bạn có thể quan sát tiến trình của engine OCR ngay trên terminal.

Hãy tưởng tượng bạn có một biên lai đã quét, một ghi chú viết tay, hoặc một trang PDF được lưu dưới dạng PNG. Bạn muốn lấy các ký tự thô mà không cần mở giao diện người dùng cồng kềnh. Hướng dẫn này sẽ dẫn bạn qua một giải pháp sao chép‑dán hoàn chỉnh, hoạt động ngay với .NET 6+ và thư viện Aspose OCR mới nhất.

Khi hoàn thành hướng dẫn này, bạn sẽ có thể:

* Tải một tệp hình ảnh và chạy OCR để **trích xuất văn bản từ hình ảnh**.  
* Kết nối một logger console vào Aspose AI để bạn thấy thư viện đang làm gì phía sau.  
* Áp dụng bộ xử lý hậu‑xử lý kiểm tra chính tả tích hợp để làm sạch các lỗi OCR.  

> **Prerequisites** – Một môi trường phát triển .NET hoạt động (Visual Studio 2022, VS Code, hoặc Rider), .NET 6 SDK hoặc mới hơn, và giấy phép Aspose OCR (hoặc bản dùng thử miễn phí). Không cần bất kỳ gói bên thứ ba nào khác.

---

## Những gì bạn sẽ cần

| Item | Why it matters |
|------|----------------|
| **Aspose.OCR** NuGet package | Cung cấp lớp `OcrEngine` thực sự đọc hình ảnh. |
| **Aspose.OCR.AI** NuGet package | Cung cấp khung xử lý hậu‑xử lý `AsposeAI`, bao gồm kiểm tra chính tả. |
| **Microsoft.Extensions.Logging** (optional) | Cung cấp giao diện `ILogger` cho bước **add console logger**. |
| **Một hình ảnh đầu vào** (`input.png`) | Tệp nguồn mà chúng ta sẽ **trích xuất văn bản từ hình ảnh**. |

Bạn có thể cài đặt các gói qua terminal:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Bước 1 – Trích xuất Văn bản từ Hình ảnh với Aspose OCR

Điều đầu tiên chúng ta làm là đưa hình ảnh cho engine OCR. Khối này thực hiện phần việc nặng và trả về một chuỗi thô có thể vẫn còn lỗi chính tả.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**Tại sao điều này hoạt động:** `OcrEngine` ẩn đi tất cả các bước tiền xử lý hình ảnh mức thấp (nhị phân hoá, hiệu chỉnh nghiêng, v.v.). Khi `Recognize()` trả về `true`, thuộc tính `Text` đã chứa các ký tự dự đoán tốt nhất.  

> **Tip:** Nếu hình ảnh của bạn lớn, hãy cân nhắc thay đổi kích thước xuống ≤ 2000 px ở cạnh dài nhất trước khi đưa vào engine. Điều này tăng tốc xử lý mà không làm giảm độ chính xác.

---

## Bước 2 – Thêm Console Logger để Nhận Thông Tin Theo Thời Gian Thực

Bây giờ chúng ta đưa vào phần **add console logger**. Logging không chỉ dành cho việc gỡ lỗi; nó cung cấp khả năng quan sát việc tải mô hình, các bước xử lý AI, và bất kỳ cảnh báo nào mà thư viện có thể phát sinh.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

Bạn có thể kết nối logger này vào Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Bạn sẽ thấy gì:** Khi mô hình kiểm tra chính tả được tự động tải xuống, console sẽ in ra một dòng như:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Đó là lợi thế của **add console logger** – bạn không bao giờ phải đoán một thao tác nền có thành công hay không.

---

## Bước 3 – Cấu Hình và Đăng Ký Bộ Xử Lý Hậu‑Xử Lý Kiểm Tra Chính Tả

Aspose AI đi kèm với một bộ xử lý hậu‑xử lý kiểm tra chính tả tiện lợi, giúp làm sạch các lỗi OCR thường gặp (ví dụ, “rec0gn1ze” → “recognize”). Chúng ta sẽ cấu hình nó, tùy chọn chỉ định thư mục lưu mô hình, và sau đó đăng ký.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**Tại sao bạn có thể muốn một đường dẫn tùy chỉnh:** Trong các pipeline CI/CD, bạn thường muốn cache mô hình trong một thư mục đã biết để tránh việc tải lại nhiều lần. Cờ `AllowAutoDownload` đảm bảo mô hình được tải về lần đầu khi chạy mã.

---

## Bước 4 – Chạy Bộ Xử Lý Hậu‑Xử Lý trên Kết Quả OCR

Với văn bản OCR đã có và bộ xử lý kiểm tra chính tả sẵn sàng, chúng ta đưa chuỗi thô cho `AsposeAI`. Engine sẽ chạy mô hình, và bộ xử lý sẽ lưu trữ văn bản đã được chỉnh sửa nội bộ.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Sau lời gọi này, `spellProcessor` chứa một tập hợp các đối tượng `RecognitionResult`, mỗi đối tượng có thuộc tính `RecognitionText` chứa phiên bản đã được làm sạch.

---

## Bước 5 – Lấy và Hiển Thị Văn Bản Đã Được Chỉnh Sửa

Cuối cùng chúng ta rút chuỗi đã chỉnh sửa ra khỏi bộ xử lý và in ra. Đây là khoảnh khắc bạn thực sự cảm nhận được lợi ích của cả OCR và quy trình **add console logger**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Kết quả mong đợi** (giả sử hình ảnh chứa cụm từ “Aspose OCR demo” với một vài lỗi OCR):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Chú ý cách logger thông báo mô hình đã sẵn sàng, và dòng văn bản đã được chỉnh sửa hiển thị sạch sẽ.

---

## Bước 6 – Dọn Dẹp Tài Nguyên

Cả `AsposeAI` và `OcrEngine` đều triển khai `IDisposable`. Việc giải phóng chúng sẽ giải phóng bộ nhớ native và các handle file, điều này đặc biệt quan trọng trong các dịch vụ chạy lâu dài.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Ví dụ Hoàn Chỉnh

Dưới đây là toàn bộ chương trình bạn có thể sao chép‑dán vào một dự án console mới (`dotnet new console`). Thay `"YOUR_DIRECTORY"` bằng thư mục thực tế trên máy của bạn.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-21
description: Cách thực hiện OCR hàng loạt trong C# một cách đơn giản—học cách trích
  xuất văn bản từ hình ảnh, chuyển đổi hình ảnh thành văn bản và lưu OCR dưới dạng
  văn bản với cài đặt ngôn ngữ.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: vi
og_description: Cách thực hiện OCR hàng loạt trong C# cho phép bạn trích xuất văn
  bản từ hình ảnh, chuyển đổi hình ảnh thành văn bản và lưu OCR dưới dạng văn bản
  đồng thời dễ dàng thiết lập ngôn ngữ OCR.
og_title: Cách thực hiện OCR hàng loạt trong C# – Hướng dẫn nhanh
tags:
- OCR
- C#
- Aspose
title: Cách thực hiện OCR hàng loạt trong C# – Trích xuất văn bản từ hình ảnh nhanh
  chóng
url: /vi/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR hàng loạt trong C# – Trích xuất văn bản từ hình ảnh nhanh chóng

Bạn đã bao giờ tự hỏi **cách thực hiện OCR hàng loạt** khi có hàng trăm bức ảnh nằm trong một thư mục chưa? Bạn không phải là người duy nhất—các nhà phát triển liên tục hỏi cách trích xuất văn bản từ hình ảnh mà không phải viết vòng lặp cho từng tệp. Tin tốt là Aspose.OCR cung cấp cho bạn một cách sạch sẽ, sẵn sàng song song để **chuyển đổi hình ảnh thành văn bản** chỉ trong vài dòng C#.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho bạn thấy cách **lưu OCR dưới dạng văn bản**, chọn ngôn ngữ phù hợp, và tăng tốc xử lý song song để đạt tốc độ cao. Khi hoàn thành, bạn sẽ có một giải pháp tự chứa có thể đưa vào bất kỳ dự án .NET nào.

## Những gì bạn cần

- .NET 6 hoặc mới hơn (API hoạt động với .NET Core và .NET Framework)
- Aspose.OCR cho .NET (gói NuGet `Aspose.OCR`)
- Thư mục chứa các hình ảnh bạn muốn xử lý (PNG, JPEG, TIFF, v.v.)
- Một chút tò mò về lập trình song song (tùy chọn, nhưng hữu ích)

Không cần dịch vụ bổ sung, không cần khóa cloud—chỉ cần mã C# thuần chạy cục bộ.

---

![how to batch OCR workflow](placeholder.png){alt="sơ đồ quy trình batch OCR"}

## Bước 1: Thiết lập dự án và cài đặt Aspose.OCR

Đầu tiên, tạo một ứng dụng console (hoặc sử dụng lại một dự án hiện có) và thêm gói Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng Visual Studio, nhấp chuột phải vào dự án → *Manage NuGet Packages* → tìm kiếm *Aspose.OCR* và cài đặt phiên bản ổn định mới nhất.

Điều này cho phép bạn truy cập vào `OcrBatchProcessor`, `OcrEngineSettings`, và enum `Language`.

## Bước 2: Xác định thư mục đầu vào và đầu ra

Bộ xử lý batch cần biết nơi lưu trữ các ảnh nguồn và nơi ghi các tệp văn bản đã trích xuất. Giữ đường dẫn ở dạng tuyệt đối hoặc tương đối so với thư mục gốc của dự án—chỉ cần đảm bảo các thư mục tồn tại trước khi chạy mã.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Tại sao điều này quan trọng:** Nếu thư mục đầu ra không tồn tại, bộ xử lý sẽ ném ra ngoại lệ, làm gián đoạn toàn bộ batch. Tạo trước sẽ đảm bảo quá trình chạy suôn sẻ.

## Bước 3: Cấu hình cài đặt OCR (bao gồm ngôn ngữ)

Đây là nơi bạn **đặt ngôn ngữ OCR** cho toàn bộ batch. Aspose.OCR hỗ trợ hàng chục ngôn ngữ; tiếng Anh là mặc định, nhưng bạn có thể chuyển sang tiếng Pháp, tiếng Tây Ban Nha, v.v., bằng cách thay đổi giá trị enum `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Nếu bạn cần xử lý các ngôn ngữ khác nhau cho từng ảnh, bạn có thể ghi đè cài đặt này cho mỗi tệp sau—sẽ được đề cập ở phần sau.

## Bước 4: Xây dựng đối tượng `OcrBatchProcessor`

Bây giờ chúng ta liên kết mọi thứ lại. `OcrBatchProcessor` cho phép bạn chỉ định thư mục đầu vào, thư mục đầu ra, định dạng đầu ra, tùy chọn song song, và các cài đặt chung mà chúng ta vừa tạo.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Tại sao cần song song?** Khi bạn có hàng chục hoặc hàng trăm hình ảnh, xử lý từng cái một có thể rất chậm. Đặt `MaxDegreeOfParallelism` thành 4 cho phép runtime sử dụng bốn lõi CPU đồng thời, giảm đáng kể thời gian tổng trên một máy làm việc điển hình.

## Bước 5: Thực thi thao tác batch

Với bộ xử lý đã được cấu hình, việc thực thi chỉ là một lời gọi phương thức. Thư viện sẽ tự động liệt kê tệp, thực hiện OCR và ghi kết quả.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Khi console in ra *“Batch OCR completed.”* bạn sẽ thấy một tệp `.txt` bên cạnh mỗi ảnh gốc trong thư mục `BatchResults`. Mỗi tệp văn bản chứa các ký tự thô được trích xuất từ ảnh nguồn—đúng là những gì bạn cần để **trích xuất văn bản từ hình ảnh** cho các bước xử lý tiếp theo.

### Kết quả mong đợi

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Mở bất kỳ tệp nào trong số đó và bạn sẽ thấy biểu diễn dạng văn bản thuần của nội dung ảnh.

## Bước 6: Xác minh kết quả (Tùy chọn)

Thói quen tốt là kiểm tra lại một vài tệp để chắc chắn OCR đã thực hiện đúng như mong đợi. Một cách nhanh là đọc dòng đầu tiên của mỗi tệp đã tạo và in ra console:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Nếu bạn nhận thấy ký tự bị rối, hãy cân nhắc chuyển đổi cài đặt `Language` hoặc điều chỉnh chất lượng ảnh (ví dụ: tăng DPI, chuyển sang ảnh xám).

## Các biến thể nâng cao & Trường hợp đặc biệt

### 1. Ghi đè ngôn ngữ theo tệp

Đôi khi một batch chứa tài liệu đa ngôn ngữ. Bạn có thể kiểm tra tên mỗi ảnh và gán ngôn ngữ ngay tại thời điểm chạy:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Định dạng đầu ra khác

Nếu bạn cần PDF có thể tìm kiếm thay vì văn bản thuần, hãy thay đổi `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Điều này sẽ **chuyển đổi hình ảnh thành văn bản** bên trong một container PDF, giữ nguyên bố cục gốc.

### 3. Xử lý hình ảnh lớn

Các ảnh có độ phân giải rất cao có thể tiêu tốn bộ nhớ. Để quá trình nhẹ hơn, bật giảm mẫu ảnh:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Ghi lỗi

Bộ xử lý sẽ ném ngoại lệ cho các tệp không đọc được. Bao bọc `Execute` trong try/catch và ghi lại tên các tệp gặp vấn đề:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Ví dụ hoàn chỉnh

Kết hợp tất cả lại, đây là chương trình đầy đủ, sẵn sàng sao chép và dán:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Lưu lại dưới tên `Program.cs`, biên dịch dự án, và chạy `dotnet run`. Bạn sẽ thấy output console xác nhận hoàn thành, tiếp theo là một đoạn preview ngắn của văn bản đã trích xuất.

---

## Kết luận

Chúng ta vừa khám phá **cách thực hiện OCR hàng loạt** trong C# bằng Aspose.OCR, cho bạn thấy cách **trích xuất văn bản từ hình ảnh**, **chuyển đổi hình ảnh thành văn bản**, và **lưu OCR dưới dạng văn bản** đồng thời **đặt ngôn ngữ OCR** phù hợp với nội dung. Ví dụ này hoàn toàn hoạt động, bao gồm xử lý song song để tăng tốc, và cung cấp các điểm mở rộng cho các kịch bản nâng cao như ghi đè ngôn ngữ theo tệp hoặc xuất PDF.

Sẵn sàng bước tiếp? Hãy thử thay `OcrOutputFormat.PlainText` bằng `SearchablePdf` và xem việc tạo PDF có thể tìm kiếm dễ dàng như thế nào. Hoặc thử các giá trị `MaxDegreeOfParallelism` khác nhau để khai thác tối đa mọi mili giây trên máy đa lõi.

Nếu gặp khó khăn, hãy kiểm tra lại đường dẫn thư mục, đảm bảo các ảnh có thể đọc được, và xác nhận enum ngôn ngữ khớp với văn bản trong ảnh của bạn. Chúc lập trình vui vẻ, và chúc các batch OCR của bạn nhanh chóng và chính xác!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
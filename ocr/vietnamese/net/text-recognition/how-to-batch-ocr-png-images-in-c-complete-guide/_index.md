---
category: general
date: 2026-04-26
description: Cách thực hiện OCR hàng loạt cho ảnh PNG nhanh chóng. Học cách trích
  xuất văn bản từ PNG, chuyển đổi ảnh sang văn bản, ghi lại văn bản đã nhận dạng và
  đọc thư mục PNG bằng Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: vi
og_description: Cách thực hiện OCR hàng loạt ảnh PNG trong C# với Aspose OCR. Hướng
  dẫn này chỉ ra cách trích xuất văn bản từ PNG, chuyển đổi ảnh thành văn bản và ghi
  lại văn bản đã nhận dạng một cách hiệu quả.
og_title: Cách thực hiện OCR hàng loạt ảnh PNG trong C# – Từng bước
tags:
- OCR
- C#
- Aspose
title: Cách thực hiện OCR hàng loạt cho ảnh PNG trong C# – Hướng dẫn chi tiết
url: /vi/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR hàng loạt ảnh PNG trong C# – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **cách thực hiện OCR hàng loạt** cho một thư mục chứa các tệp PNG mà không cần viết một chương trình riêng cho mỗi hình ảnh chưa? Bạn không phải là người duy nhất phải xử lý hàng chục ảnh chụp màn hình, biên lai đã quét, hoặc đồ họa cần chuyển thành văn bản có thể tìm kiếm. Trong hướng dẫn này, chúng tôi sẽ trình bày một giải pháp thực tế giúp **trích xuất văn bản từ PNG**, **chuyển đổi hình ảnh thành văn bản**, và **ghi văn bản đã nhận dạng** vào các tệp riêng lẻ — đồng thời tự động đọc thư mục PNG.

Cuối cùng, bạn sẽ có một ứng dụng console C# sẵn sàng chạy, có thể xử lý bất kỳ số lượng hình ảnh nào trong một lần. Không cần script phụ, không cần sao chép‑dán thủ công — chỉ cần mã thuần thực hiện công việc nặng cho bạn.

## Những gì bạn cần

- **.NET 6.0** hoặc mới hơn (mã hoạt động tốt trên .NET Framework cũng được).  
- Gói NuGet **Aspose.OCR for .NET** (bản dùng thử miễn phí đủ cho việc thử nghiệm).  
- Một thư mục chứa một vài tệp *.png* mà bạn muốn OCR.  
- Visual Studio 2022 hoặc bất kỳ IDE C# nào bạn thích.

Nếu bạn đã có những thứ trên, chúng ta có thể bắt đầu triển khai ngay.

## Bước 1 – Chuẩn bị Thư mục Đầu vào và Đầu ra *(Đọc thư mục PNG)*

Điều đầu tiên chúng ta làm là chỉ định cho chương trình thư mục chứa các hình ảnh và quyết định nơi sẽ lưu các tệp *.txt* kết quả. Sử dụng `Directory.GetFiles` cung cấp cho chúng ta một danh sách sạch sẽ của mọi tệp PNG trong thư mục.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Tại sao điều này quan trọng:**

- Sử dụng ký tự đại diện (`*.png`) đảm bảo chúng ta chỉ xử lý các tệp hình ảnh, bỏ qua bất kỳ tài liệu lạc lõng nào.  
- Tạo thư mục đầu ra ngay khi cần tránh lỗi `DirectoryNotFoundException` sau này.

> **Mẹo chuyên nghiệp:** Nếu bạn cần hỗ trợ các định dạng khác (JPEG, BMP), chỉ cần mở rộng mẫu tìm kiếm hoặc gọi `Directory.EnumerateFiles` với nhiều phần mở rộng.

## Bước 2 – Khởi tạo Engine OCR *(Chuyển đổi hình ảnh thành văn bản)*

Aspose.OCR cung cấp hai loại engine: một `OcrEngine` chạy trên CPU và một `GpuOcrEngine` được tăng tốc bằng GPU. Đối với hầu hết các công việc batch, engine CPU là hoàn toàn đủ, nhưng bạn có thể thay đổi tên lớp nếu có GPU phù hợp.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Tại sao điều này quan trọng:**

- Đặt ngôn ngữ sẽ cải thiện độ chính xác đáng kể vì engine biết bộ ký tự nào sẽ xuất hiện.  
- Chuyển sang `GpuOcrEngine` chỉ cần một dòng thay đổi nếu bạn gặp nút thắt hiệu năng khi xử lý batch lớn.

## Bước 3 – Tạo Batch Recogniser

Aspose cung cấp một `BatchRecognizer` tiện lợi, nhận một enumerable các đường dẫn tệp và truyền kết quả trở lại từng cái một. Điều này tránh việc tải toàn bộ hình ảnh vào bộ nhớ cùng lúc — một chi tiết quan trọng đối với các thư mục lớn.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Tại sao điều này quan trọng:**

- Batch recogniser bao gói logic vòng lặp, cho phép chúng ta tập trung vào việc xử lý mỗi kết quả thay vì lo lắng cách lặp một cách an toàn.

## Bước 4 – Thực hiện OCR trên tất cả hình ảnh và ghi kết quả *(Ghi Văn bản Đã Nhận Dạng)*

Bây giờ chúng ta thực sự thực hiện OCR. Phương thức `Recognize` trả về một `IEnumerable<RecognitionResult>` trong đó mỗi kết quả chứa văn bản đã trích xuất và các siêu dữ liệu khác.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Tại sao điều này quan trọng:**

- Sử dụng `File.WriteAllText` đảm bảo văn bản được lưu với mã hoá UTF‑8 mặc định, giữ nguyên các ký tự đặc biệt.  
- Việc đặt tên tăng dần (`out_0.txt`, `out_1.txt`) phù hợp với thứ tự xử lý, hữu ích cho việc gỡ lỗi.

> **Trường hợp đặc biệt:** Nếu bất kỳ hình ảnh nào không thể OCR (ví dụ, tệp hỏng), `RecognitionResult.Text` sẽ rỗng. Bạn có thể thêm một kiểm tra đơn giản trong vòng lặp để ghi lại các lỗi:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Bước 5 – Kết hợp Tất cả – Ví dụ Hoạt động Đầy đủ

Dưới đây là chương trình hoàn chỉnh mà bạn có thể sao chép‑dán vào một dự án console mới. Nó bao gồm các chỉ thị `using`, kiểm tra thư mục, và một giao diện console nhỏ để bạn biết khi batch hoàn thành.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Kết quả mong đợi:**

Chạy chương trình sẽ in ra một thứ gì đó như sau:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

Và bạn sẽ thấy các tệp `out_0.txt` … `out_11.txt` trong thư mục đầu ra, mỗi tệp chứa phiên bản văn bản thuần của hình ảnh tương ứng.

## Câu hỏi Thường gặp & Mẹo

| Câu hỏi | Trả lời |
|----------|--------|
| *Tôi có thể OCR các thư mục con không?* | Có — thay thế `Directory.GetFiles` bằng `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *Nếu tôi cần một ngôn ngữ khác thì sao?* | Đặt `ocrEngine.Language = Language.Spanish;` (hoặc bất kỳ enum nào được hỗ trợ). |
| *Làm sao để xử lý các batch lớn (hàng ngàn tệp)?* | Xem xét xử lý theo từng khối hoặc sử dụng `Parallel.ForEach` với mức độ song song được giới hạn để tránh tiêu tốn bộ nhớ. |
| *Kết quả luôn ở dạng UTF‑8 không?* | `File.WriteAllText` mặc định là UTF‑8 không có BOM, phù hợp với hầu hết các ngôn ngữ dựa trên Latin. Đối với các script châu Á bạn có thể cần đặt `Encoding.UTF8` một cách rõ ràng. |
| *Tôi có thể lấy điểm confidence không?* | `RecognitionResult` cung cấp thuộc tính `Confidence` — bạn có thể ghi lại cùng với văn bản để kiểm soát chất lượng. |

## Tổng quan trực quan *(Cách thực hiện OCR hàng loạt – Sơ đồ)*

![Sơ đồ quy trình OCR hàng loạt hiển thị thư mục đầu vào → engine OCR → batch recogniser → các tệp txt đầu ra](https://example.com/diagram-how-to-batch-ocr.png "Cách thực hiện OCR hàng loạt")

*Văn bản alt chứa từ khóa chính, đáp ứng yêu cầu SEO cho hình ảnh.*

## Kết luận

Chúng ta vừa mới trình bày **cách thực hiện OCR hàng loạt** cho một thư mục các tệp PNG bằng Aspose.OCR, từ việc đọc thư mục PNG đến ghi mỗi tệp văn bản đã nhận dạng. Giải pháp hoàn toàn độc lập, hoạt động trên bất kỳ môi trường .NET hiện đại nào, và có thể mở rộng để tăng tốc bằng GPU, hỗ trợ đa ngôn ngữ, hoặc xử lý song song.

Bạn đã sẵn sàng cho bước tiếp theo? Hãy thử thay `Language.Latin` bằng một ngôn ngữ khác, hoặc tích hợp kết quả vào chỉ mục tìm kiếm để tài liệu của bạn trở nên có thể tìm kiếm ngay lập tức. Không gì là không thể khi bạn đã thành thạo OCR hàng loạt.

Chúc lập trình vui vẻ, và hãy cho tôi biết trong phần bình luận nếu bạn gặp bất kỳ khó khăn nào!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
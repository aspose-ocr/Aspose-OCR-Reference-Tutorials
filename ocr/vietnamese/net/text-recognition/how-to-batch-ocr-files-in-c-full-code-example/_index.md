---
category: general
date: 2026-02-17
description: Cách thực hiện OCR hàng loạt nhiều tệp PDF và hình ảnh trong C# bằng
  Aspose OCR. Học cách trích xuất văn bản từ PDF, chuyển PDF sang văn bản và nhận
  dạng văn bản từ hình ảnh.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: vi
og_description: Cách thực hiện OCR hàng loạt nhiều tài liệu trong C# với Aspose OCR.
  Nhận mã từng bước để trích xuất văn bản từ PDF, chuyển PDF sang văn bản và nhận
  dạng văn bản từ hình ảnh.
og_title: Cách xử lý OCR hàng loạt tệp trong C# – Hướng dẫn đầy đủ
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Cách xử lý OCR hàng loạt các tệp trong C# – Ví dụ mã đầy đủ
url: /vi/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách batch OCR các tệp trong C# – Hướng dẫn toàn diện

Bạn đã bao giờ tự hỏi **cách batch OCR** một đống PDF và ảnh scan mà không phải viết vòng lặp riêng cho từng tệp chưa? Bạn không phải là người duy nhất. Hầu hết các nhà phát triển gặp khó khăn này khi cần lấy văn bản từ hàng chục trang cùng một lúc. Tin tốt là gì? Với Aspose OCR, bạn có thể đưa một tập hợp các tệp vào một engine duy nhất và để nó thực hiện công việc nặng.  

Trong tutorial này, chúng ta sẽ đi qua một giải pháp thực tế cho phép bạn **extract text from pdf**, **convert pdf to text**, và **recognize text from images** trong một lần chạy batch. Khi kết thúc, bạn sẽ có một ứng dụng console sẵn sàng chạy, in kết quả OCR cho mỗi trang, và bạn sẽ hiểu lý do đằng sau mỗi bước để có thể điều chỉnh cho dự án của mình.

## Prerequisites – Những gì bạn cần trước khi bắt đầu

- **.NET 6.0 trở lên** (mã cũng chạy trên .NET Framework, nhưng .NET 6+ được khuyến nghị)
- **Gói NuGet Aspose.OCR** – cài đặt bằng `dotnet add package Aspose.OCR`
- Một vài tệp mẫu: một PDF đa trang (`doc1.pdf`) và một TIFF đã scan (`doc2.tif`). Đặt chúng trong một thư mục bạn có thể tham chiếu, ví dụ `C:\OCRSamples`.
- Kiến thức cơ bản về C# – bạn nên quen với các câu lệnh `using` và các collection.

> Pro tip: Nếu bạn chưa có license, Aspose cung cấp một key tạm thời miễn phí giúp loại bỏ giới hạn 100 trang trong quá trình phát triển.

## Bước 1: Thiết lập dự án và import các namespace

Đầu tiên, tạo một dự án console mới (hoặc thêm vào dự án hiện có) và import các namespace cần thiết.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Why this matters:** Importing `Aspose.OCR.Image` gives you the convenient `ImageStream.FromFile` method, which automatically splits PDF pages into separate image streams. That’s the secret sauce that makes batch processing painless.

## Bước 2: Khởi tạo OCR Engine

Engine là thành phần thực hiện việc giao tiếp với OCR gốc. Bạn chỉ cần một instance cho toàn bộ batch.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Explanation:** Re‑using the same `OcrEngine` reduces memory churn and speeds up processing because the native libraries stay loaded between pages.

## Bước 3: Xây dựng danh sách các Image Stream

Ở đây chúng ta tập hợp mọi tài liệu cần xử lý. `ImageStream.FromFile` thông minh đủ để tách một PDF thành các trang riêng lẻ, vì vậy một PDF ba trang sẽ trở thành ba stream riêng.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Edge case:** If you have a mixture of PDFs, TIFFs, JPEGs, or PNGs, just add them to the same list – Aspose handles the format detection automatically.

## Bước 4: Thực hiện batch OCR

Bây giờ chúng ta chuyển danh sách này cho engine. `RecognizeBatch` trả về một collection các đối tượng `OcrResult`, mỗi đối tượng tương ứng với một trang.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Why batch?** Running OCR page‑by‑page in a manual loop forces the engine to re‑initialise each time, which can double processing time. `RecognizeBatch` keeps the engine warm and streams results back as they become available.

## Bước 5: Xuất văn bản đã nhận dạng

Cuối cùng, chúng ta duyệt qua các kết quả và ghi văn bản của mỗi trang ra console. Tại đây bạn có thể thay `Console.WriteLine` bằng việc ghi file, chèn vào database, hoặc bất kỳ hành động downstream nào khác.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Kết quả Console dự kiến

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Nếu bạn chạy chương trình với các tệp mẫu, sẽ thấy một khối văn bản cho mỗi trang, chứng minh rằng bạn đã **extract text scanned pdf** thành công trong một lần chạy.

## Xử lý các vấn đề thường gặp

| Vấn đề | Nguyên nhân | Giải pháp nhanh |
|--------|-------------|-----------------|
| **Lỗi out‑of‑memory** | Các PDF lớn tạo ra nhiều ảnh độ phân giải cao. | Giới hạn DPI khi tải PDF: `ocrEngine.Settings.ImageDpi = 200;` |
| **Ký tự rác** | Bản scan nguồn chất lượng thấp hoặc ngôn ngữ không được hỗ trợ. | Đặt ngôn ngữ rõ ràng: `ocrEngine.Language = Language.English;` |
| **Kết quả không đầy đủ** | Danh sách batch chứa tệp bị hỏng. | Bao `RecognizeBatch` trong try/catch và log `e.Message` cho tệp gây lỗi. |
| **Nút thắt hiệu năng** | Chạy trên một luồng duy nhất trên máy đa lõi. | Sử dụng `Parallel.ForEach` với các instance `OcrEngine` riêng cho mỗi luồng (nâng cao). |

## Bonus: Lưu kết quả OCR thành file txt

Nếu bạn muốn giữ một file `.txt` riêng cho mỗi trang, chỉ cần thêm một đoạn ghi nhỏ vào trong vòng lặp:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Bây giờ bạn đã biến **convert pdf to text** thành một thư mục các file plain‑text gọn gàng—hoàn hảo cho việc indexing hoặc tìm kiếm downstream.

## Ví dụ hoàn chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng copy‑paste. Không có phụ thuộc ẩn, không có script ngoài.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Chạy `dotnet run` từ thư mục dự án và quan sát console hiện ra văn bản đã trích xuất. Đó là **how to batch OCR** một tập hợp tài liệu chỉ trong vài dòng C#.

## Những gì chúng ta đã học – Tóm tắt nhanh

- Thiết lập app console .NET và cài đặt Aspose.OCR.  
- Tạo một instance `OcrEngine` duy nhất để tối ưu hiệu suất.  
- Xây dựng danh sách các đối tượng `ImageStream` tự động tách PDF thành các trang.  
- Thực thi `RecognizeBatch` để **extract text from pdf** và các định dạng ảnh khác trong một lần.  
- In kết quả và tùy chọn lưu chúng thành các file `.txt` riêng, hoàn thiện quy trình **convert pdf to text**.  

## Các bước tiếp theo và chủ đề liên quan

- **Mở rộng quy mô**: Sử dụng `Parallel.ForEach` với một pool các đối tượng `OcrEngine` để xử lý hàng trăm tệp đồng thời.  
- **Gói ngôn ngữ**: Thay `Language.English` bằng `Language.French` hoặc tải từ điển tùy chỉnh khi bạn cần **recognize text from images** bằng các ngôn ngữ khác.  
- **Xử lý hậu kỳ**: Đưa đầu ra OCR qua bộ kiểm tra chính tả hoặc parser ngôn ngữ tự nhiên để cải thiện độ chính xác cho các hợp đồng đã scan.  
- **Thư viện thay thế**: So sánh Aspose OCR với Tesseract.NET nếu bạn muốn một giải pháp mã nguồn mở—cả hai đều có thể **extract text scanned pdf** nhưng khác nhau về giấy phép và độ chính xác ngay từ đầu.

---

![how to batch OCR example](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
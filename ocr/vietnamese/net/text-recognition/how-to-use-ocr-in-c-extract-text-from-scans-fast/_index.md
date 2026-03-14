---
category: general
date: 2026-03-13
description: Cách sử dụng OCR trong C# để trích xuất văn bản từ các bản quét. Học
  cách chuyển đổi TIFF sang văn bản với Aspose OCR, tăng tốc GPU và mã từng bước.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: vi
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản từ các bản quét. Hướng
  dẫn này cho bạn biết cách chuyển đổi TIFF sang văn bản bằng Aspose OCR và tăng tốc
  GPU.
og_title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ ảnh quét nhanh chóng
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cách sử dụng OCR trong C# – Trích xuất nhanh văn bản từ ảnh quét
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong C# – Trích Xuất Văn Bản từ Ảnh Quét Nhanh Chóng

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để lấy văn bản có thể đọc được từ một đống file TIFF đã quét chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế—như số hoá hoá đơn, lưu trữ tài liệu lịch sử, hoặc chỉ đơn giản là làm cho PDF có thể tìm kiếm—các nhà phát triển cần một cách đáng tin cậy để **trích xuất văn bản từ ảnh quét** mà không gặp khó khăn.

Tin tốt là gì? Với Aspose OCR và một vài dòng C# bạn có thể chuyển đổi TIFF sang văn bản trong vài giây, ngay cả trên một máy làm việc bình thường. Dưới đây là ví dụ hoàn chỉnh, sẵn sàng chạy, cùng với lý do cho mỗi lựa chọn để bạn có thể điều chỉnh cho quy trình của mình.

## Những Gì Bạn Cần Chuẩn Bị

Trước khi bắt đầu, hãy chắc chắn bạn đã có sẵn các mục sau:

| Yêu Cầu Trước | Lý Do |
|--------------|----------------|
| .NET 6+ (hoặc .NET Framework 4.7+) | Gói NuGet Aspose OCR nhắm tới các runtime .NET hiện đại. |
| Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích) | Cung cấp IntelliSense và khả năng gỡ lỗi dễ dàng. |
| GPU hỗ trợ CUDA & driver (tùy chọn) | Cho phép `ocrEngine.UseGpu = true` để tăng tốc đáng kể khi xử lý lô lớn. |
| Thư mục chứa các ảnh TIFF bạn muốn xử lý | Hướng dẫn này sử dụng file `*.tif`, nhưng bạn có thể thay đổi mẫu. |
| Gói NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Thư viện cốt lõi thực hiện các tác vụ nặng. |

Nếu bạn thiếu bất kỳ mục nào, hãy tải về ngay—không có lý do nào để đọc tiếp mà sau này lại gặp lỗi phụ thuộc.

## Tổng Quan Về Giải Pháp

Ở mức cao, chương trình thực hiện ba việc:

1. **Tạo một OCR engine** và tùy chọn bật tăng tốc GPU.  
2. **Duyệt qua mọi file TIFF** trong một thư mục, thực hiện nhận dạng, và lấy văn bản thu được.  
3. **Ghi văn bản** vào file `.txt` nằm cạnh hình ảnh gốc.

Đó là tất cả. Mã nguồn được giữ tối giản, nhưng vẫn minh họa các thực tiễn tốt như lựa chọn ngôn ngữ rõ ràng, giải phóng tài nguyên đúng cách, và xử lý lỗi cho các trường hợp thường gặp.

![Ví dụ cách sử dụng OCR trong C#](/images/how-to-use-ocr-csharp.png "Minh hoạ cách sử dụng OCR trong C# để trích xuất văn bản từ ảnh quét")

## Bước 1: Khởi Tạo OCR Engine (Cách Sử Dụng OCR)

Điều đầu tiên bạn cần là một thể hiện của `OcrEngine`. Đối tượng này là cổng vào mọi chức năng của Aspose OCR. Mặc định nó chạy trên CPU, nhưng đặt `UseGpu = true` sẽ yêu cầu thư viện chuyển các phép tính ma trận nặng sang card đồ họa của bạn—miễn là bạn đã cài driver hỗ trợ CUDA.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Tại sao điều này quan trọng:**  
- **Tăng tốc GPU** có thể rút ngắn thời gian xử lý tới 70 % cho các ảnh quét độ phân giải cao.  
- **Lựa chọn ngôn ngữ rõ ràng** tránh việc engine đoán và cải thiện độ chính xác, đặc biệt với các script không phải Latin.

## Bước 2: Chỉ Định Thư Mục Chứa Ảnh Quét (Chuyển TIFF sang Văn Bản)

Tiếp theo chúng ta cho chương trình biết nơi tìm các ảnh. Sử dụng `Directory.GetFiles` với bộ lọc `*.tif` giữ cho logic đơn giản và tránh kéo các file không liên quan như `.jpg` hay `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Lưu ý trường hợp đặc biệt:** Nếu thư mục rỗng, vòng lặp dưới sẽ không bao giờ chạy, điều này hoàn toàn bình thường. Bạn sẽ thấy thông báo “No files found” thân thiện sau này.

## Bước 3: Xử Lý Mỗi File TIFF (Trích Xuất Văn Bản từ Ảnh Quét)

Bây giờ là phần cốt lõi của chương trình: tải mỗi ảnh, chạy OCR, và lưu kết quả. Trợ giúp `ImageStream.FromFile` truyền luồng file trực tiếp vào bộ nhớ, hiệu quả hơn so với việc tải một `Bitmap` trước.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Tại sao chúng ta bọc mỗi vòng lặp trong `try/catch`:**  
Xử lý một lô tài liệu luôn có rủi ro; một file TIFF bị hỏng hoặc lỗi hết bộ nhớ không nên làm dừng toàn bộ quá trình. Khối catch ghi lại vấn đề và tiếp tục, giữ cho pipeline ổn định.

### Đầu Ra Dự Kiến

Với mỗi file `example.tif` bạn sẽ tìm thấy một file `example.txt` kèm theo, chứa nội dung tương tự:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Nếu OCR engine không đọc được một dòng, nó sẽ để lại dòng trống hoặc ký tự lộn xộn—không gây crash.

## Bước 4: Dọn Dẹp và Giải Phóng (Thực Hành Tốt)

`OcrEngine` triển khai `IDisposable`, vì vậy việc giải phóng tài nguyên native khi hoàn thành là phép lịch sự. Trong một ứng dụng console ngắn, bạn có thể để GC tự làm, nhưng việc giải phóng rõ ràng là thói quen đáng có.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là chương trình đầy đủ bạn có thể dán vào một dự án Console App mới. Nó biên dịch ngay, với giả định bạn đã thêm gói NuGet Aspose.OCR.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Danh Sách Kiểm Tra Nhanh

- **Cờ GPU** – xóa hoặc đặt thành `false` nếu bạn không có driver CUDA.  
- **Ngôn ngữ** – thay `Language.English` bằng bất kỳ ngôn ngữ hỗ trợ nào khác.  
- **Mẫu file** – đổi `"*.tif"` thành `"*.png"` hoặc `"*.*"` nếu ảnh quét của bạn ở định dạng khác.  

## Những Cạm Bẫy Thường Gặp & Mẹo Nhanh (hướng dẫn OCR c#)

| Cạm Bẫy | Cách Tránh |
|---------|------------|
| **Lỗi hết bộ nhớ** khi xử lý lô lớn | Xử lý file theo từng khối nhỏ hơn hoặc gọi `GC.Collect()` sau mỗi 50 file (hiếm khi cần). |
| **GPU không được phát hiện** nhưng `UseGpu = true` | Engine sẽ tự động chuyển về CPU, nhưng bạn có thể kiểm tra `ocrEngine.IsGpuAvailable` sau khi khởi tạo. |
| **Gói ngôn ngữ sai** gây ra kết quả rối | Luôn đặt `ocrEngine.Language` một cách rõ ràng; mặc định có thể là `Language.Unknown`. |
| **Đường dẫn file chứa ký tự Unicode** | Dùng `Path.GetFullPath` để chuẩn hoá, hoặc thêm tiền tố `@"\\?\"` trên Windows nếu đường dẫn quá dài |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-02-14
description: Cách sử dụng OCR trong C# để trích xuất văn bản từ các tệp PNG nhanh
  chóng. Học OCR hàng loạt hình ảnh, xử lý nhiều hình ảnh và sử dụng Aspose OCR C#
  trong một hướng dẫn duy nhất.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: vi
og_description: Cách sử dụng OCR trong C# với Aspose OCR C#. Hướng dẫn này cho thấy
  cách trích xuất văn bản từ các tệp PNG, thực hiện OCR hàng loạt cho hình ảnh và
  xử lý nhiều hình ảnh một cách hiệu quả.
og_title: Cách sử dụng OCR trong C# – Trích xuất văn bản PNG hàng loạt
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cách sử dụng OCR trong C# – Xử lý hàng loạt ảnh PNG với Aspose OCR
url: /vi/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong C# – Xử lý hàng loạt ảnh PNG với Aspose OCR

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để trích xuất văn bản từ một loạt các tệp PNG mà không cần viết một hàm riêng cho từng tệp chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần **trích xuất văn bản PNG** ở quy mô lớn, đặc biệt khi các hình ảnh nằm trong một thư mục và bạn phải khởi động engine OCR cho mỗi tệp.  

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh, sẵn sàng chạy, cho phép **batch OCR images**, **process multiple images** song song và tận dụng thư viện mạnh mẽ **Aspose OCR C#**. Khi hoàn thành, bạn sẽ có một file thực thi duy nhất có thể đọc bất kỳ số lượng PNG nào, trích xuất văn bản và in kết quả ra console—tất cả chỉ với vài dòng code.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (code cũng hoạt động với .NET Core và .NET Framework)  
- Giấy phép Aspose.OCR cho .NET hợp lệ (hoặc bản dùng thử miễn phí) – bạn có thể tải từ trang web của Aspose.  
- Một thư mục chứa các tệp PNG bạn muốn đọc.  
- Visual Studio 2022 (hoặc bất kỳ IDE nào hỗ trợ C#).  

- Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.OCR`.

## Bước 1: Cách sử dụng OCR – Khởi tạo Engine Aspose OCR

Điều đầu tiên bạn cần là một thể hiện của lớp `Engine`. Đối tượng này trừu tượng hoá công nghệ OCR bên dưới và có thể chạy trên CPU hoặc GPU, tùy thuộc vào phần cứng và giấy phép của bạn.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Lý do quan trọng:* Khởi tạo engine một lần và tái sử dụng nó trên các luồng giúp tiết kiệm bộ nhớ và tránh chi phí tải lại mô hình OCR liên tục. Nó cũng đảm bảo các thiết lập nhất quán cho tất cả các ảnh.

## Bước 2: Trích xuất văn bản PNG – Thu thập các đường dẫn ảnh

Tiếp theo, chúng ta cần một tập hợp các đường dẫn tệp. Trong dự án thực tế bạn có thể đọc thư mục một cách động, nhưng để minh bạch ở đây chúng ta sẽ liệt kê một vài tệp mẫu.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Mẹo:* Thay `YOUR_DIRECTORY` bằng đường dẫn tuyệt đối hoặc tương đối tới thư mục chứa ảnh của bạn. Nếu có hàng chục tệp, bạn có thể thay danh sách thủ công bằng `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Bước 3: Xử lý OCR hàng loạt – Thực hiện nhận dạng song song

Xử lý ảnh lần lượt là cách đơn giản nhưng chậm. Bằng cách sử dụng `Parallel.ForEach` chúng ta có thể **process multiple images** đồng thời, tận dụng CPU đa nhân.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Tại sao lại song song?* Mỗi lời gọi OCR tiêu tốn CPU nhưng độc lập, vì vậy chạy chúng đồng thời có thể giảm đáng kể thời gian tổng thể, đặc biệt trên máy 4 nhân trở lên.

## Bước 4: Xử lý nhiều ảnh – Hiển thị văn bản đã trích xuất

Bây giờ chúng ta đã có một tập hợp các đối tượng `OcrResult`, chúng ta có thể duyệt qua và in ra văn bản đã nhận dạng. Đây là nơi bạn thường lưu kết quả vào cơ sở dữ liệu hoặc ghi vào file, nhưng việc in ra console giúp ví dụ ngắn gọn hơn.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Kết quả console dự kiến (ví dụ):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Nếu bất kỳ ảnh nào không tải được, Aspose sẽ ném ra ngoại lệ; bạn có thể bọc lời gọi `engine.Recognize` trong khối try/catch để ghi log lỗi mà không làm dừng toàn bộ batch.

## Bước 5: Ví dụ hoàn chỉnh – Tất cả các phần cùng nhau

Dưới đây là chương trình đầy đủ mà bạn có thể sao chép‑dán vào một dự án console C# mới. Nó bao gồm mọi thứ từ các câu lệnh `using` cho tới vòng lặp xuất kết quả cuối cùng.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Chạy mẫu

1. Tạo một dự án **Console App** mới trong Visual Studio.  
2. Thêm gói NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`).  
3. Thay `YOUR_DIRECTORY` bằng đường dẫn chứa các tệp PNG của bạn.  
4. Biên dịch và chạy – bạn sẽ thấy văn bản đã trích xuất được in ra console.

## Mẹo chuyên nghiệp & Các trường hợp đặc biệt

- **Tăng tốc GPU:** Nếu bạn có GPU tương thích và giấy phép Aspose OCR, bật tính năng này qua `EngineSettings` trước khi tạo engine. Điều này có thể giảm vài giây cho mỗi ảnh.  
- **Tập tin lớn:** Đối với ảnh lớn hơn 10 MB, cân nhắc giảm kích thước trước để giảm áp lực bộ nhớ.  
- **Hỗ trợ ngôn ngữ:** Mặc định engine giả định tiếng Anh. Đặt `engine.Language = Language.French;` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ) để cải thiện độ chính xác với văn bản không phải tiếng Anh.  
- **Xử lý lỗi:** Khối `try/catch` trong vòng lặp song song đảm bảo một file hỏng không làm dừng toàn bộ batch. Bạn cũng có thể ghi log lỗi vào file để xem lại sau.  
- **Lưu trữ kết quả:** Thay vì in ra, bạn có thể ghi `result.Text` vào file `.txt` bằng `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Kết luận

Bây giờ bạn đã biết **cách sử dụng OCR** trong C# để **trích xuất văn bản PNG**, **batch OCR images**, và **process multiple images** một cách hiệu quả với Aspose OCR C#. Giải pháp này hoàn toàn tự chứa, chạy song song, và có thể mở rộng để xử lý hàng trăm hoặc hàng nghìn tệp với ít thay đổi.

Sẵn sàng cho bước tiếp theo? Hãy thử thay đổi việc in ra console bằng báo cáo CSV, thử nghiệm tăng tốc GPU, hoặc đưa văn bản OCR vào chỉ mục tìm kiếm. Các khả năng là vô hạn, và mẫu pattern—khởi tạo một lần, chạy song song, xử lý lỗi mềm mại—sẽ giúp bạn trong bất kỳ pipeline xử lý ảnh nào.

Chúc lập trình vui vẻ, và chúc các job OCR của bạn nhanh chóng và không lỗi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
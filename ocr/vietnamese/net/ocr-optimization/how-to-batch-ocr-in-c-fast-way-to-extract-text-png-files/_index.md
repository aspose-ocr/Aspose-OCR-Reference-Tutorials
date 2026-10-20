---
category: general
date: 2026-04-03
description: Học cách thực hiện OCR hàng loạt với Aspose.OCR trong C#. Hướng dẫn này
  chỉ cho bạn cách trích xuất văn bản từ các hình ảnh PNG và chuyển đổi hình ảnh thành
  văn bản một cách hiệu quả.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: vi
og_description: Khám phá cách thực hiện OCR hàng loạt trong C# để trích xuất văn bản
  từ hình ảnh PNG và chuyển đổi hình ảnh thành văn bản bằng Aspose.OCR. Bao gồm mã
  nguồn đầy đủ.
og_title: Cách thực hiện OCR hàng loạt trong C# – Hướng dẫn nhanh
tags:
- OCR
- C#
- Aspose
title: Cách thực hiện OCR hàng loạt trong C# – Cách nhanh để trích xuất văn bản từ
  các tệp PNG
url: /vi/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR hàng loạt trong C# – Cách nhanh để Trích xuất Văn bản từ Tệp PNG

Bạn đã bao giờ tự hỏi **cách thực hiện OCR hàng loạt** cho một thư mục đầy ảnh chụp màn hình mà không cần viết vòng lặp cho từng tệp chưa? Bạn không phải là người duy nhất. Trong nhiều dự án—như số hóa hoá đơn hoặc lưu trữ biên lai đã quét—bạn sẽ có hàng chục, thậm chí hàng trăm tệp PNG cần trích xuất văn bản. Tin tốt? Với Aspose.OCR, bạn có thể **trích xuất văn bản PNG** các hình ảnh một cách song song, và toàn bộ quá trình chỉ cần vài dòng C#.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho bạn thấy cách **chuyển đổi hình ảnh thành văn bản** bằng bộ xử lý hàng loạt. Chúng tôi sẽ trình bày các yêu cầu trước, giải thích lý do mỗi dòng quan trọng, và thậm chí đưa vào một vài mẹo chuyên nghiệp để bạn tránh những bẫy thường gặp sau này.

## Yêu cầu trước

- **.NET 6.0** (hoặc phiên bản mới hơn) đã được cài đặt trên máy của bạn. Các runtime cũ vẫn hoạt động, nhưng phiên bản mới nhất mang lại hiệu năng tốt hơn và hỗ trợ async.
- Gói **Aspose.OCR for .NET**. Bạn có thể tải về qua NuGet: `dotnet add package Aspose.OCR`.
- Một thư mục chứa đầy các hình ảnh **PNG** mà bạn muốn xử lý. Chúng tôi sẽ gọi nó là `YOUR_DIRECTORY` trong suốt hướng dẫn.
- Một lượng RAM vừa phải—OCR hàng loạt có thể tiêu tốn nhiều bộ nhớ nếu bạn tăng độ song song, nhưng việc sử dụng `Environment.ProcessorCount` giúp giữ an toàn.

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng pipeline CI/CD, hãy thêm tệp giấy phép Aspose làm bí mật để tránh giới hạn 20 trang của bản đánh giá miễn phí.

Bây giờ, hãy bắt tay vào thực hành.

## Bước 1: Thiết lập Batch OCR Processor (Từ khóa chính trong tiêu đề)

Điều đầu tiên bạn cần là một thể hiện của `BatchOcrProcessor`. Lớp này trừu tượng hoá logic đa luồng và cho phép bạn tập trung vào việc xử lý từng hình ảnh.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Tại sao điều này quan trọng:**  
- `Engine = new OcrEngine()` cung cấp cho bạn một engine OCR mới cho mỗi luồng, tránh xung đột.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` tự động mở rộng theo số lõi, mang lại thông lượng tốt nhất mà không cần tinh chỉnh thủ công.

## Bước 2: Kết nối vào sự kiện Tiến độ (Giúp theo dõi quá trình trích xuất)

Việc nhìn thấy tiến độ là rất quan trọng khi xử lý hàng trăm tệp. Sự kiện `ProgressChanged` được kích hoạt sau khi mỗi tệp hoàn thành, cho phép bạn ghi lại trạng thái.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Tại sao bạn sẽ thích nó:**  
- Phản hồi thời gian thực ngăn bạn băn khoăn liệu ứng dụng có bị treo hay không.  
- Nếu bạn cần tạm dừng hoặc hủy, bạn đã có một điểm hook để kiểm tra `e.Current` so với `e.Total`.

## Bước 3: Định nghĩa việc quét thư mục và mẫu tệp (Trích xuất Văn bản PNG)

Bây giờ chúng ta cho bộ xử lý biết nơi cần tìm và loại tệp nào cần lấy. Mẫu `"*.png"` đảm bảo chúng ta chỉ xử lý các hình ảnh PNG.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Tại sao điều này quan trọng:**  
- Sử dụng mẫu glob giữ cho mã linh hoạt; thay đổi `*.png` thành `*.jpg` nếu sau này bạn cần xử lý JPEG.  
- Callback nhận cả đường dẫn hình ảnh và văn bản đã nhận dạng, cho phép bạn kiểm soát hoàn toàn những gì sẽ làm tiếp theo.

## Bước 4: Lưu Văn bản Đã Nhận Dạng Bên cạnh Nguồn (Chuyển đổi Hình ảnh thành Văn bản)

Trong callback, chúng ta sẽ ghi kết quả OCR vào một tệp `.txt` nằm ngay bên cạnh PNG gốc. Đây là cách đơn giản nhất để **chuyển đổi hình ảnh thành văn bản** cho các quy trình xử lý tiếp theo.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Tại sao chúng tôi chọn tệp `.txt` bên cạnh:**  
- Nó giữ mối quan hệ rõ ràng—mở PNG, mở TXT, so sánh.  
- Không cần cơ sở dữ liệu hay lớp lưu trữ bổ sung trong các dự án quy mô nhỏ.

## Bước 5: Kết thúc với Thông báo Hoàn thành Thân thiện

Một thông báo console gọn gàng sẽ cho bạn biết khi mọi thứ đã hoàn thành.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Khi bạn chạy chương trình, bạn sẽ thấy đầu ra như:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Mỗi PNG bây giờ có một tệp `.txt` kèm theo chứa văn bản đã trích xuất.

## Ví dụ Hoạt động Đầy đủ (Tất cả các Bước Kết hợp)

Dưới đây là toàn bộ chương trình bạn có thể sao chép‑dán vào một dự án console mới. Không có phần nào bị thiếu—chỉ cần thay `YOUR_DIRECTORY` bằng đường dẫn tuyệt đối tới các hình ảnh của bạn.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Kết quả Mong đợi

- Đối với mỗi `image.png` trong `C:\MyImages`, một `image.txt` sẽ xuất hiện bên cạnh.  
- Console in ra các dòng tiến độ, giúp dễ dàng theo dõi các lô lớn.  
- Không cần vòng lặp thủ công hay quản lý luồng—`BatchOcrProcessor` xử lý mọi thứ.

## Các Câu hỏi Thường gặp & Trường hợp Cạnh

### Nếu ảnh của tôi không phải là PNG thì sao?

Chỉ cần thay đổi đối số thứ hai trong `ProcessFolder` thành `"*.jpg"` hoặc `"*.*"` để bao gồm tất cả các tệp. Engine OCR hoạt động với hầu hết các định dạng raster.

### Tiêu thụ bộ nhớ bao nhiêu?

`BatchOcrProcessor` tải một hình ảnh cho mỗi luồng. Với `Environment.ProcessorCount` đặt, ví dụ, là 8 lõi, bạn sẽ có tám hình ảnh trong bộ nhớ cùng lúc. Nếu gặp ngoại lệ OutOfMemory, hãy giảm độ song song:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Tôi có thể tùy chỉnh ngôn ngữ OCR không?

Chắc chắn. Sau khi tạo engine, đặt thuộc tính `Language` của nó:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose hỗ trợ nhiều ngôn ngữ; chỉ cần thêm gói NuGet phù hợp nếu cần.

### Còn việc xử lý lỗi thì sao?

Bao bọc callback trong khối try/catch và ghi lại các lỗi. Bộ xử lý sẽ tiếp tục với tệp tiếp theo, ngăn một hình ảnh hỏng làm dừng toàn bộ quá trình.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Mẹo Chuyên nghiệp để Mở rộng

- **Chia nhỏ thư mục**: Nếu bạn có hàng chục nghìn tệp, hãy chia chúng thành các thư mục con và chạy nhiều công việc batch tuần tự.  
- **Sử dụng máy ảo đám mây**: Một máy có nhiều lõi hơn (ví dụ, 32 lõi) sẽ hoàn thành nhanh hơn đáng kể. Chỉ cần nhớ điều chỉnh giới hạn giấy phép.  
- **Xử lý hậu kỳ văn bản**: Sau khi trích xuất, bạn có thể chạy regex để lấy số hoá đơn hoặc ngày. Các tệp `.txt` là đầu vào hoàn hảo cho các pipeline như vậy.

## Kết luận

Bây giờ bạn đã có một công thức vững chắc, sẵn sàng cho sản xuất để **thực hiện OCR hàng loạt** cho một thư mục PNG, **trích xuất văn bản PNG** và **chuyển đổi hình ảnh thành văn bản** bằng Aspose.OCR trong C#. Ví dụ này độc lập, giải thích “tại sao” mỗi dòng, và bao gồm các mẹo để xử lý khối lượng công việc lớn hơn hoặc các loại tệp khác.

Sẵn sàng cho bước tiếp theo? Hãy thử thay đổi callback để đẩy kết quả vào cơ sở dữ liệu, hoặc thêm tiền xử lý ảnh (ví dụ, chỉnh góc) trước OCR. Mẫu này mở rộng tốt, vì vậy bạn có thể áp dụng nó cho bất kỳ kịch bản xử lý hàng loạt nào.

Chúc lập trình vui vẻ, và hy vọng các pipeline OCR của bạn nhanh chóng và không lỗi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
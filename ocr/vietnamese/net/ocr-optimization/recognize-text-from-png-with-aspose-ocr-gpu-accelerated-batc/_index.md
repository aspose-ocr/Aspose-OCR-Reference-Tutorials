---
category: general
date: 2026-04-01
description: Tìm hiểu cách nhận dạng văn bản từ các tệp PNG nhanh chóng bằng cách
  thiết lập ID thiết bị GPU và kích hoạt tăng tốc GPU trong Aspose OCR. Hướng dẫn
  C# chi tiết từng bước.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: vi
og_description: Nhận dạng văn bản từ các tệp PNG nhanh chóng bằng cách thiết lập ID
  thiết bị GPU. Hãy theo dõi hướng dẫn C# đầy đủ này để kích hoạt tăng tốc GPU với
  Aspose OCR.
og_title: Nhận dạng văn bản từ PNG – Hướng dẫn OCR Aspose tăng tốc GPU
tags:
- C#
- OCR
- GPU
- Aspose
title: Nhận dạng văn bản từ PNG với Aspose OCR – Demo Hàng loạt Tăng tốc GPU
url: /vi/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhận dạng văn bản từ png – Hướng dẫn đầy đủ C# tăng tốc bằng GPU

Bạn đã bao giờ cần **recognize text from png** các hình ảnh nhưng lại thấy quá trình thực hiện chậm chạp? Bạn không phải là người duy nhất. Hầu hết các nhà phát triển bắt đầu bằng một lời gọi OCR đơn giản, rồi nhìn vào console di chuyển chậm như rùa khi một thư mục chứa hàng chục ảnh chụp màn hình.  

Tin tốt? Aspose OCR có thể chuyển tải công việc nặng sang card đồ họa của bạn, và chỉ với vài dòng bạn có thể **set gpu device id** để chọn GPU cụ thể mà bạn muốn. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, lấy mọi PNG trong một thư mục, bật tăng tốc GPU, chọn GPU đầu tiên, và in ra số ký tự cho mỗi tệp.

Khi kết thúc, bạn sẽ có một chương trình tự chứa mà bạn có thể chèn vào bất kỳ dự án .NET nào, và bạn sẽ hiểu tại sao việc bật GPU quan trọng, cách xử lý các trường hợp đặc biệt, và những gì cần điều chỉnh để đạt hiệu năng tốt hơn nữa.

## Những gì bạn cần

- **.NET 6.0** hoặc mới hơn (mã cũng biên dịch được với .NET Core).  
- Gói NuGet **Aspose.OCR** – cài đặt bằng `dotnet add package Aspose.OCR`.  
- Một máy có GPU tương thích CUDA (thường là NVIDIA) và driver phù hợp.  
- Một thư mục chứa đầy các hình ảnh **PNG** mà bạn muốn xử lý.  

Nếu bất kỳ mục nào trong số này bạn chưa quen, đừng lo lắng. Các bước dưới đây bao gồm các lệnh chính xác bạn cần, và chúng tôi cũng sẽ thảo luận cách xử lý khi không có GPU.

## Bước 1: Khởi tạo Engine OCR và Bật tăng tốc GPU  

Điều đầu tiên bạn phải làm là tạo một thể hiện `OcrEngine` và bật hỗ trợ GPU. Cờ này báo cho Aspose sử dụng các thư viện CUDA gốc phía sau.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Tại sao điều này quan trọng:** Nếu không có `UseGpuAcceleration`, mỗi hình ảnh sẽ được xử lý trên CPU, điều này có thể chậm hơn hàng chục lần, đặc biệt với các PNG có độ phân giải cao. Bật cờ này cũng chuẩn bị engine để chấp nhận một thiết bị GPU cụ thể sau này.

## Bước 2: Đặt GPU Device ID (Tùy chọn nhưng Được khuyến nghị)  

Nếu workstation của bạn có hơn một GPU, bạn có thể quyết định GPU nào sẽ dùng. Các ID thiết bị bắt đầu từ **0**, vì vậy `0` chọn GPU đầu tiên, `1` GPU thứ hai, và cứ tiếp tục như vậy.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Mẹo chuyên nghiệp:** Khi chạy trên máy chủ chia sẻ, việc đặt rõ ràng GPU device ID có thể ngăn công việc của bạn chiếm tài nguyên từ các tiến trình khác. Nếu bạn bỏ qua dòng này, Aspose sẽ chọn thiết bị mặc định, thường ổn đối với cấu hình một GPU.

## Bước 3: Thu thập tất cả các tệp PNG từ Thư mục Batch của bạn  

Tiếp theo chúng ta cần tìm mọi PNG mà bạn muốn chạy OCR. Phương thức `Directory.GetFiles` thực hiện công việc nặng này.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Trường hợp đặc biệt:** Nếu thư mục rỗng, `imageFiles` sẽ là một mảng rỗng. Chúng tôi sẽ xử lý điều này sau bằng một thông báo thân thiện.

## Bước 4: Xử lý mỗi hình ảnh và xuất số ký tự đã nhận dạng  

Bây giờ là vòng lặp chính. Đối với mỗi PNG, chúng ta gọi `Recognize`, sau đó in ra tên tệp và độ dài của văn bản đã trích xuất.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Bạn sẽ thấy:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Nếu một hình ảnh không chứa văn bản, số đếm sẽ là `0`. Điều này hoàn toàn bình thường đối với các ảnh chụp màn hình chỉ là đồ họa.

## Bước 5: Chạy chương trình và Kiểm tra việc sử dụng GPU  

Biên dịch tệp (`dotnet build`) và chạy nó (`dotnet run`). Khi console cuộn, bạn có thể mở công cụ giám sát GPU (như NVIDIA Smi) để xem mức sử dụng GPU tăng ngắn ngủi cho mỗi hình ảnh. Nếu bạn không thấy hoạt động nào, hãy kiểm tra lại:

1. Driver CUDA đã được cài đặt.  
2. `UseGpuAcceleration` được đặt thành `true`.  
3. `GpuDeviceId` đúng khớp với một GPU vật lý.

Nếu GPU không khả dụng, Aspose sẽ tự động chuyển sang CPU, nhưng bạn sẽ mất lợi thế về tốc độ.

## Các biến thể thường gặp & Mẹo  

| Tình huống | Cần thay đổi |
|-----------|----------------|
| **Định dạng ảnh khác** (ví dụ, JPEG) | Thay đổi mẫu tìm kiếm thành `*.jpg` hoặc `*.*` và Aspose vẫn sẽ nhận dạng văn bản. |
| **Số lượng batch lớn** (hàng nghìn tệp) | Xử lý theo từng khối để tránh áp lực bộ nhớ: chia `imageFiles` thành các mảng nhỏ hơn. |
| **Cần văn bản thực tế, không chỉ độ dài** | Thay `ocrResult.Text.Length` bằng `ocrResult.Text` trong `WriteLine`. |
| **Chạy trên server không có giao diện** | Đảm bảo server có driver GPU; nếu không, đặt `UseGpuAcceleration = false` để tránh lỗi không cần thiết. |
| **Nhiều GPU, muốn cân bằng tải** | Lặp `ocrEngine.GpuDeviceId = i % gpuCount` trong `foreach` để xoay vòng các thiết bị. |

## Kết quả mong đợi & Xác minh  

Khi mọi thứ hoạt động, console sẽ in mỗi tên tệp kèm theo số ký tự, như đã hiển thị ở trên. Để kiểm tra lại kết quả OCR thực tế, bạn có thể tạm thời xuất văn bản:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Chỉ cần nhớ xóa hoặc comment dòng này khi xử lý batch lớn; in ra hàng nghìn dòng có thể làm ngập terminal của bạn.

## Ví dụ Hoạt động Đầy đủ (Sẵn sàng sao chép‑dán)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Lưu lại dưới tên `GpuBatchDemo.cs`, chạy `dotnet add package Aspose.OCR`, sau đó `dotnet run`. Bạn sẽ thấy số ký tự xuất hiện gần như ngay lập tức cho mỗi PNG, nhờ vào tăng tốc GPU.

## Kết luận  

Bạn giờ đã biết cách **recognize text from png** các tệp một cách hiệu quả bằng cách bật tăng tốc GPU và rõ ràng **set gpu device id** trong Aspose OCR. Chương trình hoàn chỉnh, sao chép‑dán này xử lý việc khám phá thư mục, kiểm tra các trường hợp đặc biệt, và cung cấp phản hồi ngay lập tức về hiệu năng OCR.  

Bước tiếp theo? Hãy thử thay thế lời gọi `Recognize` bằng `ocrEngine.RecognizeAsync` nếu bạn cần xử lý không chặn, hoặc thử nghiệm các tùy chọn tiền xử lý ảnh khác nhau (ví dụ, nhị phân hoá) mà Aspose cung cấp. Bạn cũng có thể đưa kết quả OCR vào cơ sở dữ liệu hoặc chỉ mục tìm kiếm để có giải pháp tìm kiếm toàn văn.  

Có câu hỏi về việc xử lý PDF đa trang, hoặc muốn so sánh Aspose OCR với Tesseract? Hãy để lại bình luận hoặc khám phá các hướng dẫn khác của chúng tôi về **batch OCR C#**, **mẹo hiệu năng OCR**, và **xử lý ảnh bằng GPU**. Chúc lập trình vui vẻ!  

![Kết quả console hiển thị số ký tự đã nhận dạng cho các tệp PNG – nhận dạng văn bản từ png bằng tăng tốc GPU](image-placeholder.png "ví dụ đầu ra nhận dạng văn bản từ png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
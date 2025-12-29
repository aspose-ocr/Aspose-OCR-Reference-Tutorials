---
category: general
date: 2025-12-29
description: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét bằng xử lý hàng loạt Aspose
  OCR. Học cách chuyển đổi hình ảnh sang PDF, tiền xử lý hình ảnh cho OCR và chỉnh
  nghiêng tài liệu đã quét.
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- convert images to pdf
- preprocess images for ocr
- deskew scanned documents
language: vi
og_description: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét bằng xử lý hàng loạt Aspose
  OCR. Học cách chuyển đổi hình ảnh sang PDF, tiền xử lý hình ảnh cho OCR và chỉnh
  nghiêng tài liệu đã quét.
og_title: Tạo PDF có thể tìm kiếm với OCR hàng loạt – Hướng dẫn C#
tags:
- OCR
- C#
- PDF/A
- Aspose
title: Tạo PDF có thể tìm kiếm với OCR hàng loạt – Hướng dẫn C#
url: /vi/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm với OCR hàng loạt – Hướng dẫn C#

Bạn đã bao giờ **tạo file PDF có thể tìm kiếm** từ một đống ảnh quét nhưng lại bị kẹt ở bước đầu tiên chưa? Bạn không đơn độc—nhiều nhà phát triển gặp cùng một rào cản khi phải xử lý các bản quét lộn xộn, các trang không đồng đều, hoặc chỉ đơn giản là chuyển đổi hàng loạt.  

Tin tốt là gì? Với Aspose OCR bạn có thể xây dựng một **pipeline xử lý OCR hàng loạt** không chỉ **chuyển đổi ảnh sang pdf** mà còn **tiền xử lý ảnh cho OCR** và thậm chí **làm thẳng tài liệu quét** một cách tự động. Trong tutorial này chúng ta sẽ đi qua toàn bộ quy trình, từ việc thiết lập engine đến tinh chỉnh kết quả, để bạn có thể chạy trên một thư mục chứa nhiều file và nhận được các file PDF/A‑2b có thể tìm kiếm.

> **Bạn sẽ nhận được:** một ứng dụng console C# duy nhất, có thể chạy, nhận một thư mục chứa ảnh (hoặc PDF), làm sạch mỗi trang, chạy OCR và tạo ra một file PDF/A‑2b có thể tìm kiếm ngay bên cạnh nguồn. Không có các đoạn code rời rạc, chỉ một giải pháp thống nhất.

---

## Prerequisites

- .NET 6 SDK hoặc mới hơn (code cũng biên dịch được với .NET Core).  
- Gói NuGet Aspose OCR (`Aspose.OCR`).  
- Một thư mục chứa các ảnh quét (TIFF, JPEG, PNG) hoặc PDF mà bạn muốn chuyển thành PDF có thể tìm kiếm.  
- (Tùy chọn) Một key license thực—nếu không, chế độ dùng thử sẽ thêm watermark, nhưng vẫn hoạt động để thử nghiệm.

Nếu bạn đã có những thứ trên, hãy bắt đầu.

---

## Overview – How the whole pipeline creates a searchable pdf

1. **Kích hoạt chế độ dùng thử** (hoặc tải license của bạn).  
2. **Cấu hình `OcrBatchProcessor`** – chỉ định nơi đọc file, nơi ghi PDF, định dạng muốn dùng, và số luồng chạy song song.  
3. **Tiền‑xử lý mỗi ảnh** – làm thẳng, giảm nhiễu, và loại bỏ nền để engine OCR nhận được trang sạch.  
4. **Chạy batch** – Aspose xử lý mọi file, thực hiện OCR và ghi ra PDF/A‑2b có thể tìm kiếm.  
5. **Thông báo hoàn thành** – một thông điệp console đơn giản, nhưng bạn có thể gắn logger hoặc webhook.

Đó là luồng tổng quan. Đoạn code dưới đây thực hiện từng bước với đầy đủ chú thích, để bạn có thể tùy chỉnh bất kỳ phần nào mà không làm hỏng toàn bộ.

---

## Step 1 – Activate trial mode (or load your license)

Trước khi gọi bất kỳ lớp nào của Aspose, bạn cần thông báo cho thư viện biết bạn đã có license. Đối với các thí nghiệm nhanh, chế độ dùng thử là đủ.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

// Activate trial mode – replace with OcrEngine.SetLicense("YourLicenseFile.lic") for production
OcrEngine.EnableTrialMode();
```

> **Mẹo chuyên nghiệp:** đặt việc kích hoạt license ở đầu file `Program.cs`. Nếu quên, engine sẽ ném exception khi lần đầu gọi `Process()`.

---

## Step 2 – Configure the batch OCR processing engine

Ở đây chúng ta thiết lập đối tượng **batch OCR processing**. Lưu ý `InputFolder` và `OutputFolder` trong ví dụ này trùng nhau, nhưng bạn có thể tách chúng nếu muốn.

```csharp
// Define where your source images live and where the searchable PDFs should be saved
var ocrBatch = new OcrBatchProcessor
{
    // Folder that contains the images or PDFs to be processed
    InputFolder = @"C:\Scans\Incoming",

    // Folder where searchable PDF/A‑2b files will be saved
    OutputFolder = @"C:\Scans\Processed",

    // Choose the output format – searchable PDF/A‑2b (perfect for archiving)
    OutputFormat = SaveFormat.SearchablePdf,

    // Limit the number of concurrent OCR operations to avoid CPU spikes
    MaxDegreeOfParallelism = 3,

    // Pre‑process each image: deskew, denoise, and remove background
    Preprocess = img => ImageFilters
                            .Deskew(img)          // fixes rotated pages
                            .Denoise()            // reduces speckles
                            .RemoveBackground()   // clears colored backgrounds
};
```

### Tại sao các thiết lập này quan trọng

- **`MaxDegreeOfParallelism`**: Chạy quá nhiều luồng OCR có thể làm quá tải CPU, đặc biệt trên máy workstation vừa phải. Ba luồng là mức cân bằng tốt cho hầu hết các laptop quad‑core.  
- **Pipeline `Preprocess`**: Ba bộ lọc này cùng nhau cải thiện đáng kể độ chính xác OCR. `Deskew` sửa lỗi “quét nghiêng”, `Denoise` loại bỏ nhiễu ngẫu nhiên, và `RemoveBackground` đảm bảo engine chỉ nhìn thấy chữ đen trên nền trắng.  
- **`SaveFormat.SearchablePdf`**: Tạo file PDF/A‑2b vừa đáp ứng yêu cầu lưu trữ lâu dài vừa có thể tìm kiếm—điều này là yêu cầu của nhiều tiêu chuẩn tuân thủ.

---

## Step 3 – Execute the batch and watch the magic happen

Chạy batch đơn giản chỉ cần gọi `Process()`. Phương thức này sẽ chặn cho đến khi mọi file hoàn thành, sau đó trả về. Nếu bạn cần báo cáo tiến độ, có thể gắn sự kiện `ProgressChanged` (không được hiển thị ở đây).

```csharp
// Start processing – this will walk through every file in InputFolder
ocrBatch.Process();

// Let the user (or calling script) know we’re finished
Console.WriteLine("All files processed. Searchable PDFs are ready.");
```

Khi console in ra dòng cuối cùng, bạn sẽ thấy một PDF có thể tìm kiếm cho mỗi ảnh đầu vào trong `C:\Scans\Processed`. Mở bất kỳ file nào trong Adobe Reader, nhấn **Ctrl+F**, và bạn có thể tìm kiếm văn bản vừa được trích xuất từ bản quét.

---

## Step 4 – Full runnable program (copy‑paste ready)

Dưới đây là chương trình **đầy đủ, tự chứa** mà bạn có thể sao chép vào một dự án console mới (`dotnet new console`). Đảm bảo đã thêm gói NuGet Aspose.OCR trước (`dotnet add package Aspose.OCR`).

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

namespace CreateSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Activate trial mode (replace with real license for production)
            OcrEngine.EnableTrialMode();

            // 2️⃣ Configure batch OCR processing
            var ocrBatch = new OcrBatchProcessor
            {
                InputFolder = @"C:\Scans\Incoming",   // 👉 change to your source folder
                OutputFolder = @"C:\Scans\Processed", // 👉 change to your target folder
                OutputFormat = SaveFormat.SearchablePdf,
                MaxDegreeOfParallelism = 3,
                Preprocess = img => ImageFilters
                                        .Deskew(img)          // fixes rotated pages
                                        .Denoise()            // cleans up noise
                                        .RemoveBackground()   // strips colored backgrounds
            };

            // 3️⃣ Run the batch
            ocrBatch.Process();

            // 4️⃣ Notify completion
            Console.WriteLine("All files processed. Searchable PDFs are ready.");
        }
    }
}
```

### Expected output

```
All files processed. Searchable PDFs are ready.
```

Sau khi chạy, vào thư mục `C:\Scans\Processed` sẽ thấy một loạt file `.pdf`—mỗi file đều có thể tìm kiếm, mỗi file đều tuân thủ PDF/A‑2b. Mở bất kỳ file nào, gõ một từ bạn biết có trong bản quét gốc, và voilà, văn bản sẽ được đánh dấu.

---

## Common questions & edge‑case handling

### What if my source folder contains PDFs already?

Aspose OCR có thể nhận PDF trực tiếp; nó sẽ rasterize mỗi trang, áp dụng các bộ lọc **preprocess** giống nhau, và nhúng lớp OCR. Không cần code bổ sung.

### How do I change the output format to a plain PDF (non‑searchable)?

Thay `SaveFormat.SearchablePdf` bằng `SaveFormat.Pdf`. Bạn sẽ mất lớp văn bản có thể tìm kiếm, nhưng độ trung thực hình ảnh vẫn giữ nguyên.

### My scans are in color—does background removal affect that?

`RemoveBackground()` chỉ nhắm vào nền không phải màu trắng trong khi vẫn giữ lại văn bản chính. Nếu bạn cần giữ lại đồ họa màu, có thể bỏ bộ lọc này:

```csharp
.Preprocess = img => ImageFilters.Deskew(img).Denoise()
```

### I’m running on a server with limited RAM—can I lower the thread count?

Chắc chắn. Đặt `MaxDegreeOfParallelism` thành `1` hoặc `2`. Batch sẽ mất nhiều thời gian hơn, nhưng mức sử dụng RAM sẽ thấp hơn.

---

## Visual summary (optional)

Nếu bạn thích một sơ đồ nhanh, hãy hình dung luồng này:

![Create searchable pdf workflow – shows input folder → preprocessing → OCR → searchable PDF output](/images/ocr-workflow.png)

*Alt text hình ảnh:* **Sơ đồ quy trình tạo PDF có thể tìm kiếm** – minh họa quá trình OCR hàng loạt, chuyển đổi và các bước làm thẳng.

---

## Conclusion

Bạn đã có một giải pháp **đầy đủ, sẵn sàng cho môi trường production** để **tạo PDF có thể tìm kiếm** từ bất kỳ lô ảnh quét nào. Bằng cách tận dụng **batch OCR processing**, bạn có thể **chuyển đổi ảnh sang pdf**, **tiền xử lý ảnh cho OCR**, và tự động **làm thẳng tài liệu quét**—tất cả chỉ với vài dòng C#.

Bước tiếp theo? Thử thêm quy tắc đặt tên tùy chỉnh, gắn một framework logging để ghi lại điểm tin cậy OCR, hoặc thử các `ImageFilters` khác như `Sharpen()` cho văn bản mờ. API Aspose OCR đủ linh hoạt để phát triển cùng nhu cầu của bạn.

Chúc lập trình vui vẻ, và hy vọng các PDF của bạn luôn có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-21
description: Tìm hiểu cách chỉnh nghiêng ảnh và nhận dạng văn bản trong ảnh bằng Aspose
  OCR. Chuyển đổi jpg sang văn bản và sửa góc quay của ảnh chỉ trong vài dòng mã C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: vi
og_description: Cách chỉnh nghiêng ảnh và trích xuất văn bản từ JPEG bằng Aspose OCR.
  Hãy làm theo hướng dẫn từng bước này để chuyển đổi jpg sang văn bản và sửa lỗi xoay
  ảnh.
og_title: Cách loại bỏ nghiêng ảnh trong C# – Hướng dẫn nhanh Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Cách loại bỏ độ nghiêng của ảnh trong C# – Hướng dẫn toàn diện sử dụng Aspose
  OCR
url: /vi/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Hướng Lại Ảnh trong C# – Hướng Dẫn Toàn Diện Sử Dụng Aspose OCR

Bạn đã bao giờ tự hỏi **cách định hướng lại ảnh** khi chúng được quét ra với góc nghiêng lạ không? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp phải vấn đề này khi cố gắng trích xuất văn bản từ biên lai, hoá đơn hoặc ghi chú viết tay. Tin tốt là với Aspose OCR, bạn có thể sửa góc quay của ảnh và lấy được văn bản sạch, có thể tìm kiếm chỉ trong vài dòng mã.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: từ cài đặt thư viện, bật tính năng tự động định hướng lại, đến nhận dạng ảnh văn bản và cuối cùng chuyển đổi JPG sang văn bản. Khi kết thúc, bạn sẽ có một ứng dụng console sẵn sàng chạy mà **nhận dạng văn bản jpg** mà không cần tự mình quay ảnh trước.

## Những Điều Cần Chuẩn Bị

- **.NET 6.0** trở lên (mã chạy được trên .NET Core và .NET Framework đều được)  
- Gói NuGet **Aspose.OCR for .NET** – khuyến nghị sử dụng phiên bản 23.12 hoặc mới hơn  
- Một mẫu **JPEG bị nghiêng** (ví dụ, `skewed_receipt.jpg`) được đặt ở vị trí mà ứng dụng của bạn có thể đọc  
- Visual Studio, VS Code, hoặc bất kỳ trình soạn thảo C# nào bạn thích  

Không cần bất kỳ công cụ bên thứ ba nào khác. Thư viện tự xử lý việc định hướng lại, OCR và thậm chí phát hiện ngôn ngữ bên trong.

![ví dụ cách định hướng lại ảnh](/images/deskew-example.png "cách định hướng lại ảnh bằng Aspose OCR")

## Bước 1: Thiết Lập Dự Án và Cài Đặt Aspose.OCR

Để mọi thứ gọn gàng, hãy bắt đầu một dự án console mới:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

Dòng `dotnet add package` sẽ tải về các binary **Aspose.OCR** cùng với tất cả các phụ thuộc native. Nếu bạn đang dùng Windows, các DLL native sẽ được lấy tự động; trên Linux/macOS bạn có thể cần cài gói `libgdiplus`, nhưng đó chỉ là một lần cài đặt.

## Bước 2: Bật Tự Động Định Hướng Lại (Sửa Góc Quay Ảnh)

Bây giờ mở `Program.cs` và thay thế nội dung của nó bằng đoạn mã dưới đây. Dòng quan trọng ở đây là `ocrEngine.Settings.Deskew = true;` – đây là cờ cho phép engine **tự động định hướng lại ảnh**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Tại Sao Nên Bật Định Hướng Lại?

Khi máy quét đưa trang vào với một góc nghiêng, đường cơ sở của văn bản cũng bị lệch. Các engine OCR truyền thống sẽ đọc mỗi ký tự như một phiên bản nghiêng, làm giảm đáng kể độ chính xác. Bằng cách đặt `Deskew = true`, Aspose OCR thực hiện một phép biến đổi Hough nhanh phía sau, quay lại bitmap về chiều ngang, rồi thực hiện nhận dạng. Kết quả giống như bạn tự quay ảnh trong Photoshop—nhưng nhanh hơn và hoàn toàn tự động.

## Bước 3: Nhận Dạng Ảnh Văn Bản và Chuyển Đổi JPG Sang Văn Bản

Lệnh `Recognize` thực hiện đồng thời hai việc:

1. **Định hướng lại** ảnh (vì chúng ta đã bật cờ).  
2. **Trích xuất** nội dung văn bản, trả về trong một đối tượng `OcrResult`.

Bạn có thể xem `ocrResult.Text` như một chuỗi thông thường, ghi nó vào file, hoặc đưa vào các pipeline xử lý tiếp theo. Nếu bạn cần điểm tin cậy thô cho mỗi từ, `ocrResult.Words` cung cấp một tập hợp với các giá trị `Confidence`.

### Ví Dụ Kết Quả

Giả sử `skewed_receipt.jpg` chứa một biên lai đơn giản, bạn có thể thấy kết quả như sau:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Chú ý cách các số được căn chỉnh gọn gàng mặc dù ảnh gốc đã bị quay khoảng 7°. Đó là sức mạnh của **sửa góc quay ảnh** được tích hợp trong thư viện.

## Bước 4: Chạy Ví Dụ và Xác Minh Kết Quả

Biên dịch và chạy:

```bash
dotnet run
```

Nếu mọi thứ được cấu hình đúng, bạn sẽ thấy văn bản đã trích xuất được in ra console. Nếu gặp ngoại lệ như `FileNotFoundException`, hãy kiểm tra lại đường dẫn tới file JPEG và đảm bảo file có thể đọc được.

### Những Cạm Bẫy Thường Gặp & Mẹo Chuyên Nghiệp

- **Ảnh lớn** – bộ nhớ OCR tăng theo kích thước ảnh. Hãy thu nhỏ các file quá lớn (ví dụ, > 3000 px chiều rộng) trước khi đưa vào engine.  
- **Kịch bản không phải Latin** – Mặc định engine giả định tiếng Anh. Đặt `ocrEngine.Settings.Language = OcrLanguage.French;` (hoặc bất kỳ ngôn ngữ hỗ trợ nào) nếu bạn cần **nhận dạng ảnh văn bản** bằng các bảng chữ cái khác.  
- **Xử lý hàng loạt** – Đối với nhiều file, hãy tái sử dụng cùng một thể hiện `OcrEngine`; tạo engine mới cho mỗi file sẽ gây tốn tài nguyên không cần thiết.  
- **Kiểm tra chất lượng** – Sau khi định hướng lại, bạn có thể xuất bitmap đã chỉnh sửa bằng `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` để kiểm tra trực quan việc sửa góc quay.

## Ví Dụ Hoàn Chỉnh (Tất Cả Cùng Nhau)

Dưới đây là chương trình hoàn chỉnh, tự chứa mà bạn có thể sao chép‑dán vào `Program.cs`. Nó bao gồm các chú thích, xử lý lỗi, và một bước tùy chọn để lưu ảnh đã định hướng lại.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Chạy chương trình sẽ **nhận dạng văn bản jpg** các file, tự động sửa mọi độ nghiêng, và in ra console văn bản sạch, có thể tìm kiếm.

## Kết Luận

Bây giờ bạn đã có một đoạn mã vững chắc, sẵn sàng cho môi trường production, cho thấy **cách định hướng lại ảnh** và trích xuất nội dung của chúng bằng Aspose OCR. Cách tiếp cận này hoạt động với biên lai, hoá đơn, hợp đồng đã quét, hoặc bất kỳ file JPEG nào mà văn bản không hoàn toàn nằm ngang. 

Các bước tiếp theo bạn có thể khám phá:

- **Xử lý hàng loạt** một thư mục các JPEG và ghi mỗi kết quả vào file `.txt` (liên quan tới *chuyển đổi jpg sang văn bản*).  
- Tích hợp bước OCR vào một API ASP.NET Core để khách hàng có thể tải lên ảnh và nhận văn bản dạng JSON.  
- Thử nghiệm các cài đặt OCR khác nhau như `ocrEngine.Settings.Language` hoặc `ocrEngine.Settings.RecognitionMode` để cải thiện độ chính xác cho tài liệu không phải tiếng Anh.  

Hãy thử nghiệm, điều chỉnh các cài đặt, và để engine thực hiện công việc nặng. Như thường lệ, nếu bạn gặp khó khăn hoặc có tối ưu thông minh nào muốn chia sẻ, hãy để lại bình luận bên dưới. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
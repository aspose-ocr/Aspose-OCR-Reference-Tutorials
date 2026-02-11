---
category: general
date: 2026-02-11
description: Tìm hiểu cách chạy OCR trên tệp TIFF đa trang trong C# bằng Aspose OCR.
  Chuyển đổi TIFF sang văn bản, trích xuất văn bản từ TIFF và nhận dạng văn bản từ
  hình ảnh một cách nhanh chóng.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: vi
og_description: Cách chạy OCR trên tệp TIFF đa trang bằng Aspose OCR trong C#. Hướng
  dẫn từng bước để chuyển TIFF thành văn bản, trích xuất văn bản từ TIFF và nhận dạng
  văn bản từ hình ảnh.
og_title: Cách chạy OCR trên ảnh TIFF đa trang – Hướng dẫn C# đầy đủ
tags:
- OCR
- C#
- Aspose
- TIFF
title: Cách chạy OCR trên ảnh TIFF đa trang với Aspose OCR – Hướng dẫn C#
url: /vi/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chạy OCR trên ảnh TIFF đa trang với Aspose OCR

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một tệp TIFF đã quét chứa nhiều trang chưa? Bạn không đơn độc—nhiều nhà phát triển gặp khó khăn này khi họ cần trích xuất văn bản có thể tìm kiếm từ các tài liệu cũ. Tin tốt là gì? Với Aspose OCR, bạn có thể nhận dạng văn bản từ các tệp hình ảnh chỉ trong vài dòng mã C#, và bạn sẽ có được văn bản thuần được nối liền, sẵn sàng để lập chỉ mục hoặc xử lý tiếp.

Trong tutorial này chúng ta sẽ đi qua toàn bộ quy trình: từ cài đặt gói Aspose OCR, tải một TIFF đa trang, chuyển đổi TIFF sang văn bản và cuối cùng hiển thị nội dung đã trích xuất. Khi kết thúc, bạn sẽ có thể **trích xuất văn bản từ TIFF**, **nhận dạng văn bản từ hình ảnh**, và thậm chí tự động hoá quy trình cho hàng chục tệp trong một công việc batch. Không có phép thuật, chỉ là các bước thực tế, rõ ràng.

## Những gì bạn sẽ học

- Cách thiết lập engine Aspose OCR để nhận dạng ngôn ngữ tiếng Anh.  
- Mã chính xác cần thiết để **chuyển đổi TIFF sang văn bản** bằng lớp `OcrEngine`.  
- Mẹo xử lý ảnh đa trang và đảm bảo mỗi trang được tách riêng đúng cách.  
- Những bẫy thường gặp (như thiếu phụ thuộc gốc) và cách tránh chúng.  

**Prerequisites** – bạn sẽ cần .NET 6 hoặc mới hơn, Visual Studio (hoặc bất kỳ trình soạn thảo C# nào), và một kết nối internet cho tính năng tải tài nguyên tự động. Đó là tất cả; không cần thư viện gốc bổ sung để vật lộn.

---

## Bước 1 – Cài đặt gói Aspose OCR NuGet

Trước khi bạn có thể **thực hiện OCR trên hình ảnh** bạn phải thêm thư viện vào dự án của mình.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Nếu bạn đang làm việc trong Visual Studio, bạn cũng có thể nhấp chuột phải vào dự án → *Manage NuGet Packages* → tìm “Aspose.OCR” và nhấn *Install*.

Gói này bao gồm mọi thứ bạn cần, và với `AutomaticResourceDownload = true` engine sẽ tự động tải các gói ngôn ngữ khi cần.

---

## Bước 2 – Khởi tạo Engine OCR (Cách chạy OCR)

Bây giờ gói đã sẵn sàng, chúng ta tạo và cấu hình một thể hiện `OcrEngine`. Đây là trái tim của **cách chạy OCR** trong kịch bản của chúng ta.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Tại sao điều này quan trọng:** Thiết lập `Language` cho engine biết bộ ký tự nào sẽ được mong đợi, trong khi `AutomaticResourceDownload` giúp bạn không phải tự tay đặt các tệp ngôn ngữ trên máy chủ. `OutputFormat` là `Text` cung cấp cho chúng ta một chuỗi đơn giản—hoàn hảo cho các pipeline **chuyển đổi TIFF sang văn bản**.

---

## Bước 3 – Tải ảnh TIFF đa trang (Nhận dạng văn bản từ hình ảnh)

Một TIFF có thể chứa nhiều khung, mỗi khung đại diện cho một trang. Lớp `System.Drawing.Image` trừu tượng hoá điều này cho chúng ta.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **Nếu tệp không ở cùng thư mục?** Chỉ cần cung cấp đường dẫn tuyệt đối đầy đủ hoặc dùng `Path.Combine` với `AppContext.BaseDirectory`.  
> **Về việc sử dụng bộ nhớ?** Câu lệnh `using` sẽ giải phóng ảnh sau khi xử lý, ngăn ngừa rò rỉ—rất quan trọng khi bạn batch‑process hàng chục TIFF lớn.

Lệnh `Recognize` tự động lặp qua mọi trang trong TIFF, nối các kết quả lại với dấu ngắt dòng. Đó là lý do bạn sẽ thấy mỗi trang được tách riêng khi in `ocrResult.Text`.

---

## Bước 4 – Ví dụ làm việc đầy đủ (Tất cả các bước trong một tệp)

Dưới đây là một ứng dụng console hoàn chỉnh, sẵn sàng chạy. Sao chép‑dán nó vào một dự án console .NET mới và nhấn **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Kết quả mong đợi** (rút gọn để ngắn gọn):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Mỗi trang xuất hiện trên một dòng riêng vì `OcrOutputFormat.Text` chèn dấu ngắt dòng giữa các khung. Nếu bạn cần một ký tự phân tách khác, có thể xử lý hậu kỳ `result.Text` bằng `String.Replace`.

---

## Bước 5 – Xử lý các trường hợp góc cạnh phổ biến

### 5.1 Tệp TIFF lớn  
Khi làm việc với các TIFF có kích thước gigabyte, việc tải toàn bộ tệp vào bộ nhớ có thể gây vấn đề. Một cách khắc phục là xử lý từng khung một cách riêng biệt:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Tài liệu không phải tiếng Anh  
Nếu bạn cần **nhận dạng văn bản từ hình ảnh** bằng tiếng Tây Ban Nha hoặc Pháp, chỉ cần thay đổi thuộc tính `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose sẽ tự động tải các tài nguyên ngôn ngữ phù hợp.

### 5. Lưu kết quả  
Thường bạn sẽ muốn **chuyển đổi TIFF sang văn bản** và lưu kết quả vào tệp `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Bạn cũng có thể tách đầu ra theo trang bằng cách dùng `String.Split(Environment.NewLine)` và ghi mỗi đoạn vào một tệp riêng.

---

## Mẹo chuyên nghiệp & Những lưu ý

- **AutomaticResourceDownload** hoạt động lần đầu khi bạn chạy ứng dụng; các lần chạy sau sẽ làm việc offline.  
- Nếu bạn thấy ký tự bị lỗi, hãy kiểm tra lại cài đặt `Language`; các gói ngôn ngữ không khớp sẽ gây nhận dạng sai.  
- Đối với PDF đã được raster hoá thành TIFF, bạn có thể muốn tăng `ocrEngine.Dpi` (mặc định là 300) để cải thiện độ chính xác.  
- Luôn bao bọc `Image.FromFile` trong một khối `using`; nếu không, bạn sẽ khóa tệp và không thể xóa hoặc di chuyển nó sau này.

---

## Câu hỏi thường gặp

**Q: Điều này có hoạt động với TIFF một trang không?**  
A: Chắc chắn. Engine xử lý TIFF một khung giống như các TIFF đa khung; bạn sẽ chỉ nhận được một dòng văn bản.

**Q: Tôi có thể xử lý tệp PNG hoặc JPEG theo cùng cách không?**  
A: Có—chỉ cần thay đổi phần mở rộng tệp. Phương thức `Recognize` chấp nhận bất kỳ định dạng `System.Drawing.Image` nào.

**Q: Nếu tôi cần kết quả OCR dưới dạng PDF thay vì văn bản thuần thì sao?**  
A: Đặt `OutputFormat = OcrOutputFormat.Pdf` và `ocrResult` sẽ chứa một mảng byte PDF mà bạn có thể ghi ra đĩa.

---

## Kết luận

Bạn giờ đã có một giải pháp toàn diện, đầu‑tới‑cuối để **cách chạy OCR** trên các tệp TIFF đa trang bằng Aspose OCR trong C#. Bằng cách cấu hình engine, tải ảnh và gọi `Recognize`, bạn có thể **trích xuất văn bản từ TIFF**, **chuyển đổi TIFF sang văn bản**, và **nhận dạng văn bản từ hình ảnh** chỉ với vài dòng mã. Hãy tự do điều chỉnh ngôn ngữ, định dạng đầu ra, hoặc xử lý từng khung để phù hợp với nhu cầu batch‑processing của riêng bạn.

Sẵn sàng cho bước tiếp theo? Hãy thử kết hợp cách này với một dịch vụ folder‑watcher để tự động **thực hiện OCR trên hình ảnh** khi chúng xuất hiện trong thư mục đích, hoặc tích hợp đầu ra vào chỉ mục tìm kiếm để có khả năng tìm kiếm toàn văn ngay lập tức. Các khả năng là vô hạn, và đoạn mã bạn vừa xem là nền tảng vững chắc.

Nếu bạn gặp bất kỳ khó khăn nào, hãy để lại bình luận bên dưới hoặc nhắn tin cho tôi trên GitHub. Chúc bạn lập trình vui vẻ, và tận hưởng việc biến những tệp TIFF cứng đầu thành văn bản có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
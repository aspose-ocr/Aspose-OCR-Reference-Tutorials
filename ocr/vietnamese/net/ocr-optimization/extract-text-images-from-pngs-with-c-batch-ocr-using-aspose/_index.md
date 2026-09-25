---
category: general
date: 2026-02-09
description: Trích xuất văn bản từ hình ảnh nhanh chóng bằng C# bằng cách đặt mức
  độ song song tối đa cho OCR hàng loạt – học cách chuyển đổi các trang quét, xử lý
  OCR đa hình ảnh và đọc văn bản PNG một cách hiệu quả.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: vi
og_description: Trích xuất văn bản từ hình ảnh trong C# bằng cách đặt mức độ song
  song tối đa. Hướng dẫn này cho thấy cách chuyển đổi các trang đã quét, thực hiện
  OCR trên nhiều hình ảnh và đọc văn bản PNG bằng Aspose OCR.
og_title: Trích xuất văn bản từ ảnh PNG bằng C# – Hướng dẫn OCR hàng loạt hoàn chỉnh
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Trích xuất văn bản từ hình PNG bằng C# – OCR hàng loạt sử dụng Aspose OCR
url: /vi/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# trích xuất hình ảnh văn bản từ PNG bằng C# – Batch OCR sử dụng Aspose OCR

Bạn đã bao giờ cần **trích xuất hình ảnh văn bản** từ một thư mục chứa các PNG đã quét nhưng lại băn khoăn “làm sao để nhanh hơn?” chưa? Bạn không đơn độc. Trong nhiều dự án thực tế, các nhà phát triển phải **đặt max parallelism** để hàng chục trang được xử lý trong vài giây thay vì vài phút.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy ngay, **chuyển đổi các trang đã quét**, thực hiện **nhiều OCR ảnh**, và cuối cùng **đọc văn bản png** mà không gặp khó khăn. Không có liên kết “xem tài liệu” mơ hồ—chỉ có mã bạn có thể sao chép‑dán, giải thích tại sao mỗi dòng quan trọng, và mẹo tránh các bẫy thường gặp.

> **Mẹo chuyên nghiệp:** Nếu bạn đã sử dụng Aspose OCR ở nơi khác, bạn sẽ nhận thấy lớp `OcrEngine` xuất hiện ở đây, nhưng chúng ta sẽ điều chỉnh cấu hình của nó để thực hiện xử lý song song thực sự.

---

## Những gì bạn cần

- **.NET 6+** (hoặc .NET Framework 4.6+). API hoạt động giống nhau, nhưng runtime mới hơn cho việc quản lý luồng tốt hơn.  
- **Aspose.OCR for .NET** – cài đặt qua NuGet: `Install-Package Aspose.OCR`.  
- Một thư mục chứa một vài PNG đã quét (`page1.png`, `page2.png`, …).  
- Một IDE hoặc trình soạn thảo mà bạn cảm thấy thoải mái (Visual Studio, Rider, VS Code…).

Đó là tất cả. Không cần dịch vụ phụ trợ, không cần khóa cloud, chỉ xử lý cục bộ thuần túy.

---

## extract text images – Đặt Max Parallelism cho Batch OCR

Khi bạn khởi chạy OCR trên nhiều tệp, engine mặc định sẽ sử dụng một luồng duy nhất. Điều này an toàn nhưng cực kỳ chậm. Bằng cách cấu hình `MaxDegreeOfParallelism` bạn cho engine biết có bao nhiêu luồng có thể được tạo đồng thời.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Tại sao lại là 4?**  
Bốn là mức cân bằng trên hầu hết các laptop hiện đại—đủ lõi để CPU bận rộn, nhưng không quá nhiều khiến các tiến trình khác bị thiếu tài nguyên. Nếu bạn chạy trên máy chủ có 16 lõi, hãy tăng lên 12 hoặc 14 để thấy tốc độ cải thiện đáng kể.

---

## Convert scanned pages – Xây dựng Bộ sưu tập Image Stream

Aspose yêu cầu mỗi ảnh dưới dạng `ImageStream`. Hàm trợ giúp `FromFile` đọc tệp, giữ nó trong bộ nhớ và truyền cho engine OCR. Bạn cũng có thể cung cấp một `MemoryStream` nếu ảnh của bạn đến từ cơ sở dữ liệu hoặc phản hồi HTTP.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Trường hợp góc cạnh:** Nếu bất kỳ tệp nào bị thiếu hoặc hỏng, `FromFile` sẽ ném ra `FileNotFoundException`. Hãy bao bọc việc khởi tạo trong `try/catch` nếu bạn dự đoán dữ liệu đầu vào không ổn định.

---

## multiple image ocr – Thực hiện Batch OCR

Bây giờ công việc nặng sẽ diễn ra. `RecognizeBatch` tạo ra số luồng bạn đã đặt trước, xử lý từng ảnh, và trả về danh sách các đối tượng `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Trong nền, mỗi luồng tải ảnh của mình, chạy mạng nơ-ron, và trích xuất văn bản thuần. Thứ tự kết quả khớp với thứ tự của danh sách đầu vào, vì vậy bạn có thể an toàn ánh xạ trang 1 → kết quả 0, v.v.

---

## read png text – Hiển thị Nội dung Đã Trích xuất

Cuối cùng chúng ta lặp qua các kết quả và in văn bản thuần ra console. Đây là nơi bạn có thể chuyển đầu ra sang tệp, cơ sở dữ liệu, hoặc thậm chí một dịch vụ NLP phía sau.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Kết quả Console Dự kiến

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Nếu bạn thấy các phần trống, hãy kiểm tra lại rằng các PNG không phải là ảnh trắng hoàn toàn—OCR cần có độ tương phản.

---

## Mẹo Thực tế & Các Bẫy Thường Gặp

| Tình huống | Cách xử lý |
|-----------|------------|
| **Áp lực bộ nhớ** khi batch lớn | Xử lý ảnh theo khối 10‑20 tệp, sau đó gọi `GC.Collect()` nếu bạn nhận thấy mức tăng đột biến. |
| **Nhận dạng ngôn ngữ sai** | Đặt `ocrEngine.Configuration.Language = OcrLanguage.English;` (hoặc ngôn ngữ mục tiêu) trước khi gọi `RecognizeBatch`. |
| **Hiệu năng chậm dù đã song song** | Kiểm tra SSD có bị throttling I/O không; đọc tất cả tệp vào bộ nhớ trước (như chúng ta làm với `ImageStream.FromFile`). |
| **Thiếu ký tự** | Tăng `ocrEngine.Configuration.DPI = 300;` để xử lý ở độ phân giải cao hơn. |

---

## Mở rộng Ví dụ – Từ PNG sang PDF hoặc DOCX

Nếu cuối cùng bạn cần **chuyển đổi các trang đã quét** thành PDF có thể tìm kiếm, chỉ cần đưa `ocrResults[i].PlainText` vào một thư viện PDF (ví dụ, Aspose.PDF) và chồng lớp văn bản vô hình lên. Thủ thuật song song tương tự cũng áp dụng ở đó.

---

## Mã Nguồn Đầy Đủ (Sẵn Sàng Sao Chép‑Dán)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Lưu lại dưới tên `BatchExample.cs`, chạy `dotnet run`, và xem console của bạn được lấp đầy bằng văn bản đã ẩn trong các PNG quét.

---

## Tóm tắt Trực quan

![extract text images example](images/ocr-batch.png){alt="ví dụ trích xuất hình ảnh văn bản"}

Sơ đồ cho thấy luồng: **tệp PNG → bộ sưu tập ImageStream → OcrEngine (max parallelism) → kết quả OCR → Console / lưu trữ downstream**.

---

## Kết luận

Bạn đã có một công thức hoàn chỉnh, đầu‑đến‑cuối để **trích xuất hình ảnh văn bản** trong C# đồng thời **đặt max parallelism**, **chuyển đổi các trang đã quét**, xử lý **nhiều OCR ảnh**, và **đọc png text** một cách hiệu quả. Mã nguồn độc lập, các giải thích bao phủ cả “cách làm” và “tại sao”, và các mẹo giúp bạn tránh những rắc rối thường gặp.

Tiếp theo bạn muốn làm gì? Hãy thử thay danh sách PNG bằng vòng lặp động `Directory.GetFiles`, thử các số luồng khác nhau, hoặc đưa đầu ra vào một PDF có thể tìm kiếm. Mẫu này có thể mở rộng lên hàng trăm trang mà chỉ cần thêm một vài dòng code.

Có câu hỏi hoặc trường hợp góc cạnh khó xử? Hãy để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
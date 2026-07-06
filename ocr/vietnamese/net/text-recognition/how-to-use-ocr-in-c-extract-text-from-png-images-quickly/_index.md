---
category: general
date: 2026-03-29
description: Cách sử dụng OCR với Aspose để trích xuất văn bản từ tệp PNG và chuyển
  đổi hình ảnh thành văn bản. Tìm hiểu OCR bất đồng bộ từng bước trong C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: vi
og_description: Cách sử dụng OCR với Aspose trong C# để trích xuất văn bản từ các
  tệp PNG. Hướng dẫn này sẽ dẫn bạn qua OCR bất đồng bộ, mã code và các mẹo.
og_title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ ảnh PNG
tags:
- OCR
- C#
- Aspose
title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh PNG nhanh chóng
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong C# – Trích Xuất Văn Bản từ Hình PNG Nhanh Chóng

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để lấy văn bản từ một vài ảnh chụp màn hình PNG chưa? Có thể bạn có các biên lai, hoá đơn đã quét, hoặc mô phỏng giao diện UI và bạn cần văn bản đó ở định dạng có thể tìm kiếm. Tin tốt là gì? Với Aspose.OCR bạn có thể chuyển đổi hình ảnh thành văn bản chỉ với vài dòng mã C# bất đồng bộ.  

Trong tutorial này chúng tôi sẽ chỉ cho bạn cách trích xuất văn bản từ các tệp PNG, giải thích lý do mỗi bước quan trọng, và cung cấp một chương trình sẵn sàng chạy để in ra văn bản đã nhận dạng cho mỗi trang. Khi kết thúc, bạn sẽ có thể **trích xuất văn bản từ hình ảnh** mà không cần mò mẫm tài liệu.

## Những Điều Bạn Sẽ Học

- Cài đặt và tham chiếu gói NuGet Aspose.OCR.  
- Khởi tạo engine OCR và đặt ngôn ngữ (tiếng Anh trong ví dụ này).  
- Cung cấp một mảng các tệp PNG cho `RecognizeImagesAsync` để xử lý nhanh, không chặn.  
- Duyệt qua các đối tượng `OcrResult` và xuất các chuỗi đã trích xuất.  

Không có dịch vụ bên ngoài, không có callback phức tạp—chỉ là C# async sạch sẽ, hoạt động trên .NET 6+.

---

## Yêu Cầu Trước

| Yêu Cầu | Lý Do |
|-------------|--------|
| .NET 6 SDK (hoặc mới hơn) | Các tính năng ngôn ngữ hiện đại như `async Main`. |
| Visual Studio 2022 hoặc VS Code | IDE để biên dịch và chạy mã. |
| Gói NuGet Aspose.OCR (`Aspose.OCR`) | Cung cấp lớp `OcrEngine` được sử dụng trong mẫu. |
| Một vài ảnh PNG (`page1.png`, `page2.png`, …) | Các tệp đầu vào cho quá trình OCR. |

Nếu bạn đã có một dự án .NET, chỉ cần chạy `dotnet add package Aspose.OCR`. Nếu chưa, tạo một ứng dụng console mới với `dotnet new console -n OcrDemo`.

---

## Bước 1: Cài Đặt Aspose.OCR và Thiết Lập Dự Án

Đầu tiên, thêm thư viện OCR vào dự án của bạn:

```bash
dotnet add package Aspose.OCR
```

Tại sao lại quan trọng: Aspose.OCR gói sẵn engine OCR gốc, các gói ngôn ngữ, và một API đơn giản. Khi lấy nó qua NuGet, bạn đảm bảo tính tương thích phiên bản và cập nhật tự động.

---

## Bước 2: Khởi Tạo Engine OCR và Chọn Ngôn Ngữ

Engine cần biết sẽ tìm kiếm ngôn ngữ nào. Tiếng Anh là phổ biến nhất, nhưng bạn có thể thay thế bằng `Language.Spanish`, `Language.French`, v.v.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Mẹo chuyên nghiệp:** Luôn đặt ngôn ngữ một cách rõ ràng; để mặc định có thể làm giảm độ chính xác và tăng thời gian xử lý.

---

## Bước 3: Chuẩn Bị Danh Sách Các Tệp PNG

Bạn có thể cung cấp một tệp duy nhất hoặc một mảng. Cung cấp một mảng cho phép engine xử lý hàng loạt một cách bất đồng bộ, rất thích hợp cho một vài trang.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Nếu ảnh của bạn nằm trong một thư mục con, chỉ cần thêm tiền tố đường dẫn tương đối (`"images/page1.png"`). Engine sẽ ném ra một `FileNotFoundException` rõ ràng nếu đường dẫn sai—vì vậy hãy kiểm tra kỹ tên tệp.

---

## Bước 4: Chạy OCR Bất Đồng Bộ trên Tất Cả Các Ảnh

Phương thức `RecognizeImagesAsync` trả về một mảng `OcrResult`. Vì nó là async, UI (hoặc console) của bạn sẽ vẫn phản hồi trong khi OCR chạy ở nền.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Tại sao lại async?**  
Nếu bạn tích hợp OCR vào một web API hoặc ứng dụng desktop, bạn không muốn luồng bị chặn trong khi engine quét từng pixel. `await` giải phóng luồng trở lại pool, cải thiện khả năng mở rộng.

---

## Bước 5: Hiển Thị Văn Bản Đã Trích Xuất cho Mỗi Trang

Bây giờ chúng ta đã có kết quả, hãy lặp qua chúng và in ra văn bản đã nhận dạng. Thuộc tính `Text` chứa đầu ra dạng plain‑text, sẵn sàng cho các xử lý tiếp theo (ví dụ: lưu vào cơ sở dữ liệu).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Kết Quả Dự Kiến

Giả sử `page1.png` chứa “Invoice #12345” và `page2.png` chứa “Total: $89.99”, bạn sẽ thấy thứ gì đó như sau:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Nếu OCR không tìm thấy bất kỳ văn bản nào, thuộc tính `Text` sẽ là một chuỗi rỗng—hãy xử lý trường hợp này trong code production bằng cách kiểm tra `string.IsNullOrWhiteSpace`.

---

## Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là chương trình đầy đủ bạn có thể sao chép‑dán vào `Program.cs`. Nó bao gồm tất cả các using directive, async `Main`, và các chú thích giải thích từng bước.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Lưu tệp, đặt các PNG của bạn cạnh file thực thi (hoặc điều chỉnh đường dẫn), và chạy:

```bash
dotnet run
```

Bạn sẽ thấy văn bản đã trích xuất được in ra console, xác nhận rằng bạn đã **chuyển đổi hình ảnh thành văn bản** thành công.

---

## Xử Lý Các Trường Hợp Cạnh Thường Gặp

| Tình Huống | Cách Giải Quyết |
|-----------|-----------------|
| **PNG độ phân giải thấp** | Tăng `ocrEngine.ImageProcessingOptions.Dpi` trước khi nhận dạng. |
| **Nhiều ngôn ngữ** | Đặt `ocrEngine.Language = Language.English | Language.Spanish;` (bitwise OR). |
| **Lô lớn (hàng trăm tệp)** | Xử lý theo từng khối (ví dụ: 20 tệp mỗi lần gọi `RecognizeImagesAsync`) để tránh tăng đột biến bộ nhớ. |
| **Cần điểm tin cậy** | Sử dụng `ocrResults[i].Confidence` (số thực từ 0 đến 1) để lọc kết quả chất lượng thấp. |

Những tinh chỉnh này giúp pipeline OCR của bạn vững chắc, đặc biệt khi chuyển từ demo sang production.

---

## Bonus: Lưu Kết Quả vào Tệp Văn Bản

Nếu bạn muốn một bản sao lưu thay vì in ra console, thêm một helper nhỏ:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Bây giờ bạn có một tệp duy nhất **trích xuất văn bản từ hình ảnh** để xử lý tiếp downstream—hoàn hảo cho việc lập chỉ mục, tìm kiếm, hoặc đưa vào mô hình ngôn ngữ.

---

## Kết Luận

Chúng ta đã đi qua **cách sử dụng OCR** trong C# với Aspose để **trích xuất văn bản từ PNG** và **chuyển đổi hình ảnh thành văn bản** một cách hiệu quả. Cách tiếp cận async đảm bảo ứng dụng của bạn luôn phản hồi, trong khi API đơn giản giữ cho mã dễ đọc và bảo trì.  

Hãy thử với các tài liệu của riêng bạn, khám phá các ngôn ngữ khác nhau, và thậm chí chuỗi kết quả vào một chỉ mục tìm kiếm hoặc dịch vụ tóm tắt. Khi bạn có thể biến ảnh thành các chuỗi có thể tìm kiếm một cách đáng tin cậy, khả năng là vô hạn.

---

### Các Bước Tiếp Theo & Chủ Đề Liên Quan

- **Trích xuất văn bản từ hình ảnh** ở các định dạng khác (JPEG, TIFF) – chỉ cần đổi phần mở rộng tệp.  
- **Xử lý batch với Parallel.ForEach** cho khối lượng công việc lớn.  
- **Làm sạch sau OCR** bằng biểu thức chính quy để chuẩn hoá ngày tháng, số tiền, hoặc ID.  
- **Tích hợp với Azure Cognitive Services** nếu bạn cần OCR dựa trên đám mây với các tính năng bổ sung.  

Bạn cứ để lại bình luận nếu gặp khó khăn, hoặc chia sẻ cách bạn mở rộng luồng công việc này. Chúc lập trình vui vẻ!   ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="kết quả OCR ví dụ"} 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
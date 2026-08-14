---
category: general
date: 2026-03-07
description: Học cách sử dụng OCR trong C# để trích xuất văn bản từ các tệp hình ảnh.
  Hướng dẫn này trình bày OCR ngoại tuyến, chuyển đổi hình ảnh thành văn bản và tải
  hình ảnh cho OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: vi
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản từ hình ảnh offline.
  Mã từng bước, mẹo và giải thích đầy đủ về việc chuyển đổi hình ảnh thành văn bản.
og_title: Cách sử dụng OCR trong C# – Hướng dẫn toàn diện offline
tags:
- OCR
- C#
- Aspose
title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh ngoại tuyến
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong C# – Trích Xuất Văn Bản từ Hình Ảnh Offline

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** trong một dự án .NET mà không cần gửi dữ liệu lên đám mây chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển cần *trích xuất văn bản từ file hình ảnh* trên một máy trạm bảo mật, và họ lo ngại lưu lượng mạng có thể lộ thông tin nhạy cảm.  

Tin tốt là gì? Với Aspose.OCR bạn có thể nhận dạng văn bản từ PNG, JPEG hoặc PDF hoàn toàn offline. Trong hướng dẫn này chúng ta sẽ đi qua việc tải một hình ảnh để OCR, cấu hình engine ở chế độ offline, và cuối cùng **chuyển đổi hình ảnh sang văn bản** chỉ với vài dòng C#.

Khi đọc xong hướng dẫn này, bạn sẽ có thể:

* Cài đặt gói NuGet Aspose.OCR.  
* Thiết lập engine OCR để xử lý offline.  
* Tải một hình ảnh để OCR và trích xuất nội dung văn bản của nó.  

Không cần dịch vụ bên ngoài, không cần API key—chỉ cần mã C# thuần chạy trên bất kỳ máy Windows hoặc Linux nào.

---

## Các Điều Kiện Cần Có

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 SDK hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+).  
* Visual Studio 2022, VS Code, hoặc bất kỳ trình soạn thảo nào hỗ trợ C#.  
* Một bản sao của thư viện **Aspose.OCR** – bạn có thể lấy từ NuGet (`Aspose.OCR`).  
* Thư mục tài nguyên OCR (`Resources`) đi kèm với thư viện (chứa các file dữ liệu ngôn ngữ).  
* Một hình ảnh mẫu (ví dụ: `offline_test.png`) được đặt trong một thư mục đã biết.

> **Pro tip:** Đặt thư mục resources cạnh file thực thi của bạn; điều này giúp đơn giản hoá cấu hình `ResourcesPath`.

---

## Bước 1: Cài Đặt Gói NuGet Aspose.OCR

Đầu tiên, thêm thư viện vào dự án của bạn. Mở terminal trong thư mục dự án và chạy:

```bash
dotnet add package Aspose.OCR
```

Hoặc, nếu bạn thích giao diện Visual Studio, chuột phải vào **Dependencies → Manage NuGet Packages**, tìm *Aspose.OCR*, và nhấn **Install**.

> Cài đặt gói sẽ kéo toàn bộ các binary cần thiết, vì vậy bạn không cần thêm bất kỳ DLL nào khác.

---

## Bước 2: Tạo và Cấu Hình Engine OCR (Cách Sử Dụng OCR – Chế Độ Offline)

Bây giờ chúng ta sẽ khởi tạo engine OCR và chỉ định nó làm việc **offline**. Điều này đảm bảo không có lưu lượng mạng nào xảy ra trong quá trình nhận dạng.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**Tại sao lại offline?**  
Khi `EngineMode` được đặt thành `Online`, engine sẽ liên hệ với cloud của Aspose để tải các gói ngôn ngữ ngay lập tức. Trong các môi trường được quy định (tài chính, y tế) lưu lượng này thường bị cấm. Bằng cách ép buộc chế độ offline, bạn đảm bảo mọi thứ chỉ diễn ra trên máy cục bộ.

---

## Bước 3: Chỉ Định Thư Mục Tài Nguyên OCR cho Engine

Engine OCR cần dữ liệu ngôn ngữ (mô hình đã được huấn luyện) để nhận dạng ký tự. Hãy cho nó biết vị trí các file này:

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

Nếu bạn không chắc thư mục nằm ở đâu, hãy tìm trong thư mục gói NuGet (`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`). Sao chép toàn bộ thư mục này vào dự án của bạn để dễ dàng triển khai hơn.

---

## Bước 4: Tải Hình Ảnh Để OCR (Load Image for OCR)

Bạn có thể đưa bất kỳ bitmap nào được hỗ trợ vào engine. Ở đây chúng ta sẽ tải một PNG lưu trên đĩa:

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**Mẹo:** Nếu bạn cần xử lý hình ảnh từ một stream (ví dụ, tải lên qua API), hãy dùng `ImageStream.FromStream(yourStream)` thay thế.

---

## Bước 5: Thực Hiện Quá Trình Nhận Dạng và Chuyển Đổi Hình Ảnh Sang Văn Bản

Khi mọi thứ đã sẵn sàng, kích hoạt OCR. Phương thức `Recognize()` sẽ thực hiện phần lớn công việc, và văn bản đã trích xuất sẽ có sẵn qua thuộc tính `Text`.

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

---

## Bước 6: Xuất Văn Bản Đã Trích Xuất

Cuối cùng, hiển thị kết quả. Trong một ứng dụng console bạn có thể đơn giản ghi ra console, nhưng trong một web API bạn sẽ trả về chuỗi dưới dạng JSON.

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

Chạy chương trình sẽ in ra nội dung văn bản của `offline_test.png`. Ví dụ, nếu hình ảnh chứa câu *“Hello, World!”*, bạn sẽ thấy:

```
=== OCR Result ===
Hello, World!
```

---

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng chạy. Sao chép‑dán vào một dự án console mới (`dotnet new console`) và điều chỉnh các đường dẫn cho phù hợp với môi trường của bạn.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Kết quả mong đợi:** Console in ra chính xác văn bản có trong file PNG. Nếu hình ảnh mờ, kết quả có thể chứa các ký tự nhận dạng sai—xem phần khắc phục sự cố bên dưới.

---

## Những Sai Lầm Thường Gặp & Mẹo (Nhận Dạng Văn Bản Từ PNG Hiệu Quả)

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| **Kết quả rỗng** | `ResourcesPath` trỏ sai thư mục hoặc thiếu file ngôn ngữ. | Kiểm tra thư mục có chứa `eng.traineddata` (hoặc các file ngôn ngữ khác) và xác nhận lại chuỗi đường dẫn. |
| **Ký tự rác** | Độ phân giải hình ảnh quá thấp hoặc chưa được binarize. | Tiền xử lý ảnh (tăng DPI, áp dụng `ImageProcessor` để làm nét). |
| **Độ trễ hiệu suất** | Hình ảnh lớn được xử lý ở độ phân giải đầy đủ. | Thu nhỏ ảnh xuống tối đa 2000 px chiều rộng trước khi đưa vào OCR. |
| **Định dạng không hỗ trợ** | Sử dụng BMP với định dạng pixel bất thường. | Chuyển đổi ảnh sang PNG hoặc JPEG trước (`System.Drawing.Image.Save`). |

**Pro tip:** Nếu cần nhận dạng đa ngôn ngữ, đặt `ocrEngine.Settings.Language = Language.English | Language.French;` trước khi gọi `Recognize()`.

---

## Câu Hỏi Thường Gặp

**H: Có thể chạy mã này trên Linux không?**  
Đáp: Hoàn toàn có thể. Aspose.OCR hỗ trợ đa nền tảng; chỉ cần đảm bảo các thư viện native có sẵn (được đóng gói trong gói NuGet).

**H: Nếu tôi không có thư mục Resources thì sao?**  
Bạn có thể tải các gói ngôn ngữ miễn phí từ trang web của Aspose hoặc giải nén chúng từ gói NuGet (`.../aspose.ocr/<version>/resources`).

**H: Có cách lấy điểm tin cậy (confidence scores) không?**  
Có. Sau khi gọi `Recognize()`, kiểm tra `ocrEngine.RecognizedWords` — mỗi từ đều có thuộc tính `Confidence`.

---

## Kết Luận

Chúng ta đã tìm hiểu **cách sử dụng OCR** trong C# để *trích xuất văn bản từ file hình ảnh* hoàn toàn offline. Bằng cách cài đặt Aspose.OCR, cấu hình `EngineMode.Offline`, chỉ định thư mục resources, tải ảnh, và gọi `Recognize()`, bạn có thể chuyển đổi hình ảnh sang văn bản một cách đáng tin cậy mà không cần kết nối internet.  

Hãy lấy đoạn mã ở trên, thay đổi đường dẫn ảnh của bạn, và bắt đầu xây dựng các tính năng như PDF có thể tìm kiếm, tự động nhập dữ liệu, hoặc công cụ trợ năng. Tiếp theo, bạn có thể khám phá **nhận dạng văn bản từ PNG** hàng loạt, hoặc tích hợp engine vào một API ASP.NET Core để cung cấp kết quả OCR cho các ứng dụng front‑end.

Chúc lập trình vui vẻ, và đừng ngại thử nghiệm—OCR thực sự linh hoạt khi engine đã được thiết lập đúng cách!

--- 

![Diagram showing offline OCR workflow – how to use OCR in a secure environment](https://example.com/ocr-workflow.png "how to use OCR diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
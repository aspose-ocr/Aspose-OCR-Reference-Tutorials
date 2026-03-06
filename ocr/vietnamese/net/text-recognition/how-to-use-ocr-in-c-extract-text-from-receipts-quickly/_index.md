---
category: general
date: 2026-03-05
description: Cách sử dụng OCR trong C# để trích xuất văn bản từ hình ảnh biên lai.
  Tìm hiểu cách tải hình ảnh cho OCR và nhận dạng hình ảnh biên lai trong vài phút.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: vi
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản từ biên lai. Hãy theo
  dõi hướng dẫn từng bước này để tải hình ảnh cho OCR và nhận dạng hình ảnh biên lai
  một cách hiệu quả.
og_title: Cách sử dụng OCR trong C# – Trích xuất nhanh văn bản biên lai
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: cách sử dụng OCR trong C# – Trích xuất văn bản từ biên lai nhanh chóng
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong C# – Trích xuất văn bản từ biên lai nhanh chóng

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để lấy dữ liệu trực tiếp từ một bức ảnh biên lai mua hàng chưa? Bạn không phải là người duy nhất. Trong nhiều ứng dụng doanh nghiệp nhỏ, nút thắt là việc chuyển đổi một tệp PNG mờ thành văn bản có cấu trúc mà bạn có thể thực sự làm việc.

Tin tốt? Chỉ với vài dòng C# và Aspose.OCR, bạn có thể **load image for OCR**, chạy engine, và **recognize receipt image** trong chưa đầy một phút. Dưới đây bạn sẽ thấy một ví dụ hoàn chỉnh, sẵn sàng chạy, cùng các mẹo cho những phần khó mà hầu hết các hướng dẫn thường bỏ qua.

## Những gì hướng dẫn này bao gồm

* Cài đặt gói NuGet Aspose.OCR.  
* Cấu hình engine OCR – cốt lõi của **how to use OCR** một cách chính xác.  
* Tải lên tệp biên lai (đó là bước **load image for OCR**).  
* Chạy quá trình nhận dạng và trích xuất cả dữ liệu bố cục JSON và XML.  
* Xử lý các vấn đề thường gặp như thiếu giấy phép hoặc định dạng ảnh không được hỗ trợ.  

Khi kết thúc, bạn sẽ có một chương trình tự chứa có thể trích xuất văn bản từ bất kỳ biên lai nào bạn đặt vào một thư mục. Không cần dịch vụ bên ngoài, không có phép thuật ẩn.

## Yêu cầu trước

* .NET 6 SDK hoặc phiên bản mới hơn (mã cũng biên dịch được với .NET Core).  
* Một tệp giấy phép Aspose.OCR hợp lệ (`Aspose.OCR.lic`). Bạn có thể nhận bản dùng thử miễn phí từ Aspose nếu chưa có.  
* Một ảnh biên lai mẫu – `receipt.png` hoạt động tốt, nhưng bất kỳ định dạng raster phổ biến nào cũng được.  

Nếu bạn đã có những thứ này, tuyệt vời – hãy bắt đầu.

![how to use OCR example](https://example.com/ocr-receipt.png "how to use OCR example")

## Bước 1: Cài đặt Aspose.OCR và Tạo dự án mới

Đầu tiên, bạn cần thư viện thực hiện công việc nặng. Mở terminal trong thư mục dự án và chạy:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Lệnh đó tạo một ứng dụng console và tải gói Aspose.OCR mới nhất. Theo kinh nghiệm của tôi, giữ tên dự án ngắn giúp các đường dẫn được tạo ra dễ đọc hơn, đặc biệt khi bạn bắt đầu quản lý nhiều ứng dụng demo.

## Bước 2: Khởi tạo Engine OCR – Trái tim của **how to use OCR**

Bây giờ chúng ta sẽ viết mã trả lời câu hỏi “**how to use OCR** trong C#”. Mở `Program.cs` và thay thế nội dung bằng đoạn mã dưới đây. Lưu ý các chú thích – chúng giải thích *lý do* đằng sau mỗi dòng, không chỉ *cái gì*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Tại sao cách này hoạt động

* **`OcrEngine`** là điểm vào; nó chứa tất cả cấu hình bạn có thể điều chỉnh sau (ngôn ngữ, DPI, v.v.).  
* **`SetLicense`** loại bỏ watermark đánh giá – một bước quan trọng khi bạn dự định phát hành mã.  
* **`ImageStream.FromFile`** thực hiện công việc **load image for OCR**, hỗ trợ PNG, JPEG, BMP, TIFF và hơn nữa.  
* **`Recognize()`** là phương thức thực sự **recognize receipt image**. Bên trong nó thực hiện nhị phân hoá, phân đoạn và phân loại ký tự.  
* Xuất ra JSON và XML cung cấp cho bạn cả bản dump dễ đọc cho con người và cấu trúc thân thiện với máy mà bạn có thể đưa vào các bộ phân tích downstream.

## Bước 3: Chạy Demo và Xác minh Kết quả

Biên dịch và thực thi:

```bash
dotnet run
```

Nếu mọi thứ được cấu hình đúng, bạn sẽ thấy một kết quả giống như:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

Console sẽ in ra văn bản thuần, trong khi `receipt.json` và `receipt.xml` chứa thông tin bố cục chi tiết (tọa độ, điểm tin cậy, v.v.). Các tệp này hữu ích nếu bạn cần ánh xạ mỗi dòng tới một trường trong cơ sở dữ liệu sau này.

## Các trường hợp đặc biệt & Mẹo chuyên nghiệp

### 1️⃣ Thiếu hoặc Giấy phép không hợp lệ

Nếu `SetLicense` thất bại, engine sẽ chuyển sang chế độ dùng thử và bạn sẽ nhận được watermark trong kết quả. Bao quanh lời gọi này trong try/catch và ghi lại một thông báo thân thiện:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Định dạng ảnh không được hỗ trợ

Aspose.OCR hỗ trợ hầu hết các định dạng raster, nhưng nếu bạn đưa vào một PDF hoặc TIFF đa trang, bạn sẽ cần chuyển trang cần thiết sang ảnh trước. Thư viện `Aspose.PDF` có thể thực hiện chuyển đổi này.

### 3️⃣ Biên lai lớn & Hiệu năng

Xử lý ảnh 10 MB có thể chậm. Giảm độ phân giải trước khi đưa vào engine:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

Phương thức `Resize` giữ tỷ lệ khung hình (`0` cho chiều cao) và giảm đáng kể kích thước tệp mà không làm giảm độ chính xác OCR cho các biên lai thông thường.

### 4️⃣ Vấn đề Ngôn ngữ & Phông chữ

Biên lai có thể chứa các ký tự đặc biệt (€, ¥, v.v.). Đặt ngôn ngữ một cách rõ ràng nếu bạn biết locale:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Đối với biên lai đa ngôn ngữ, bạn có thể bật chế độ đa ngôn ngữ:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Trích xuất Dữ liệu có cấu trúc

Văn bản thô hữu ích, nhưng hầu hết các ứng dụng cần các trường có cấu trúc (ngày, tổng, mặt hàng). Bố cục JSON bao gồm tọa độ `BoundingBox` cho mỗi từ. Bạn có thể xử lý sau như sau:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Đoạn mã này chỉ minh họa ý tưởng; trong môi trường thực tế bạn có thể sẽ dùng biểu thức chính quy hoặc một engine quy tắc nhỏ.

## Câu hỏi thường gặp

**Q: Tôi có thể chạy điều này trên Linux không?**  
A: Chắc chắn. Aspose.OCR hỗ trợ đa nền tảng; chỉ cần cài đặt runtime .NET trên máy Linux và cùng một mã sẽ hoạt động.

**Q: Nếu tôi cần xử lý hàng chục biên lai mỗi phút thì sao?**  
A: Tạo một vòng lặp `Parallel.ForEach` và tái sử dụng một thể hiện `OcrEngine` duy nhất – nó an toàn với đa luồng cho các thao tác chỉ đọc. Hãy nhớ xử lý giới hạn đồng thời của giấy phép.

**Q: Điều này có hoạt động với ảnh chụp bằng điện thoại di động ở góc nghiêng không?**  
A: Engine bao gồm chức năng cân chỉnh cơ bản, nhưng với ảnh nghiêng mạnh bạn có thể tiền xử lý bằng thư viện xử lý ảnh (ví dụ, OpenCV) để làm thẳng biên lai trước.

## Ví dụ Hoạt động Đầy đủ (Sao chép‑Dán)

Dưới đây là toàn bộ chương trình bạn có thể đặt vào `Program.cs`. Không cần tệp nào khác ngoại trừ giấy phép và ảnh biên lai.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
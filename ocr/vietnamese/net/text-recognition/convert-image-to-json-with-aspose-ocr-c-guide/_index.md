---
category: general
date: 2026-01-15
description: Chuyển đổi hình ảnh sang JSON bằng Aspose OCR trong C#. Tìm hiểu cách
  trích xuất văn bản từ hình ảnh, lấy các hộp giới hạn JSON và nhận dạng hình ảnh
  biên lai.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: vi
og_description: Chuyển đổi hình ảnh sang JSON bằng Aspose OCR trong C#. Hướng dẫn
  từng bước để trích xuất văn bản từ hình ảnh, nhận dạng hình ảnh biên lai và lấy
  các hộp giới hạn JSON.
og_title: Chuyển đổi hình ảnh sang JSON với hướng dẫn Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Chuyển đổi hình ảnh sang JSON với hướng dẫn Aspose OCR C#
url: /vi/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển Đổi Hình Ảnh sang JSON với Hướng Dẫn Aspose OCR C#

Bạn đã bao giờ cần **convert image to JSON** nhưng không chắc thư viện nào có thể cung cấp cả văn bản thô và tọa độ chính xác của từng từ không? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp phải vấn đề này khi họ cố gắng trích xuất văn bản từ các tệp hình ảnh—đặc biệt là biên lai—cùng với việc cần một payload JSON có thể đọc được bởi máy cho các quy trình downstream.

Trong hướng dẫn này, chúng tôi sẽ đi qua một **Aspose OCR C# example** hoàn chỉnh, cho bạn thấy cách trích xuất văn bản từ hình ảnh, nhận dạng hình ảnh biên lai, và xuất **JSON bounding boxes** cho mỗi từ. Khi kết thúc, bạn sẽ có một ứng dụng console sẵn sàng chạy, in ra một chuỗi JSON được định dạng đẹp mà bạn có thể đưa vào bất kỳ API, cơ sở dữ liệu, hoặc pipeline phân tích nào.

> **Bạn sẽ nhận được gì**  
> • Một dự án C# hoàn chỉnh có khả năng **converts image to JSON**  
> • Hiểu tại sao chúng ta bật `IncludeBoundingBoxes` (đó là chìa khóa cho `json bounding boxes`)  
> • Mẹo xử lý các định dạng hình ảnh và ngôn ngữ khác nhau  

Hãy bắt đầu.

---

## Những Điều Cần Chuẩn Bị

- **.NET 6.0 SDK** (hoặc bất kỳ phiên bản nào mới hơn) – mã nguồn nhắm tới .NET 6 nhưng cũng hoạt động trên .NET Framework 4.7+.  
- **Aspose.OCR for .NET** NuGet package – bạn có thể cài đặt bằng `dotnet add package Aspose.OCR`.  
- Một hình ảnh biên lai mẫu (`receipt.jpg`) đặt trong thư mục bạn có thể tham chiếu từ dự án.  
- Visual Studio 2022, VS Code, hoặc bất kỳ IDE nào bạn thích.

Không cần dịch vụ bên ngoài nào khác; mọi thứ chạy cục bộ.

## Chuyển Đổi Hình Ảnh sang JSON – Tổng Quan

Ý tưởng cốt lõi rất đơn giản: tải một hình ảnh, yêu cầu Aspose OCR nhận dạng tiếng Anh (hoặc bất kỳ ngôn ngữ nào được hỗ trợ), yêu cầu nó bao gồm bounding boxes, và cuối cùng yêu cầu kết quả ở định dạng **JSON**. Thư viện thực hiện toàn bộ công việc nặng—OCR, phân tích bố cục, và tuần tự hoá JSON.

Đây là sơ đồ cấp cao của luồng (hình dung như một bức tranh nhỏ):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Sơ đồ nhỏ ấy nắm bắt toàn bộ pipeline chúng ta sẽ triển khai.

## Bước 1: Thiết Lập Dự Án và Cài Đặt Aspose OCR

Đầu tiên, tạo một dự án console mới và thêm gói Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Visual Studio, nhấp chuột phải vào dự án → *Manage NuGet Packages* → tìm **Aspose.OCR** và cài đặt phiên bản ổn định mới nhất (hiện tại 23.12).

## Bước 2: Tải Hình Ảnh Muốn Nhận Diện

Chúng ta sẽ sử dụng phương thức `OcrImage.FromFile` để đọc hình ảnh biên lai. Đảm bảo đường dẫn trỏ tới một tệp thực tế; nếu không sẽ gặp `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Nếu hình ảnh của bạn nằm cùng thư mục với `.csproj`, bạn có thể chỉ cần dùng `"receipt.jpg"`.

## Bước 3: Cấu Hình OCR Options cho JSON Bounding Boxes

Phép màu xảy ra khi chúng ta bật `OutputFormat = OutputFormat.Json` **và** `IncludeBoundingBoxes = true`. Cái đầu tiên yêu cầu Aspose tuần tự hoá kết quả thành JSON, trong khi cái thứ hai thêm `x`, `y`, `width`, và `height` cho mỗi từ—đúng những gì bạn cần cho `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Bạn cũng có thể điều chỉnh `ocrOptions.Dpi` hoặc `ocrOptions.Language` nếu cần độ phân giải cao hơn hoặc ngôn ngữ khác.

## Bước 4: Thực Hiện Nhận Diện – Trích Xuất Văn Bản từ Hình Ảnh

Bây giờ chúng ta gọi `Recognize`. Phương thức trả về một đối tượng `OcrResult` chứa chuỗi JSON, văn bản thô, và các thông tin khác.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Nếu bạn cần xử lý các ngôn ngữ khác, thay `Language.English` bằng `Language.Spanish`, `Language.French`, v.v. Aspose hỗ trợ hơn 30 ngôn ngữ ngay từ đầu.

## Bước 5: Xuất Kết Quả – Payload JSON của Bạn

Cuối cùng, chúng ta in JSON ra console. Trong một ứng dụng thực tế, bạn có thể ghi nó vào tệp hoặc đẩy lên một dịch vụ.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Chạy chương trình sẽ tạo ra một tài liệu JSON tương tự như đoạn mã dưới đây.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Lưu ý mỗi từ bây giờ có **JSON bounding box**—hoàn hảo để đưa vào lớp phủ UI hoặc bộ phân tích downstream.

## Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là chương trình hoàn chỉnh, sẵn sàng sao chép‑dán. Không có phần ẩn, không có cuộc gọi bên ngoài—chỉ C# thuần.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Cẩn thận với:**  
> • **Lỗi đường dẫn tệp** – kiểm tra lại vị trí hình ảnh.  
> • **Thiếu gói NuGet** – đảm bảo `Aspose.OCR` đã được tham chiếu.  
> • **Định dạng hình ảnh không được hỗ trợ** – sử dụng JPEG, PNG, BMP, hoặc TIFF để có kết quả tốt nhất.

## Các Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Tôi có thể chuyển đổi một **trang PDF** sang JSON thay vì JPEG không?

Có. Đầu tiên chuyển trang PDF sang hình ảnh (ví dụ, dùng `Aspose.PDF`), sau đó đưa hình ảnh đó vào cùng pipeline OCR. Đầu ra JSON sẽ giống hệt vì bước OCR chỉ quan tâm đến dữ liệu raster.

### Nếu biên lai bị mờ thì sao?

Tăng DPI trong `ocrOptions`. Ví dụ:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

DPI cao hơn có thể tăng mức sử dụng bộ nhớ, vì vậy cân bằng giữa chất lượng và hiệu suất.

### Tôi cần **nhiều ngôn ngữ** trên cùng một biên lai (ví dụ, English + Spanish).

Bạn có thể truyền một mảng các ngôn ngữ:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose sẽ cố gắng nhận dạng từng ngôn ngữ theo thứ tự đã chỉ định.

### Làm thế nào để ghi JSON vào tệp?

Chỉ cần thay dòng `Console.WriteLine` bằng:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Bây giờ bạn có một tệp lưu trữ có thể chuyển tới các dịch vụ khác.

## Tóm Tắt Trực Quan

![convert image to json example](convert-image-to-json.png "convert image to json example")

*Ảnh chụp màn hình hiển thị đầu ra JSON của console sau khi chạy bản demo.*

## Kết Luận

Chúng tôi vừa cho bạn thấy cách **convert image to JSON** bằng Aspose OCR trong C#. Bằng cách cấu hình `OutputFormat` và `IncludeBoundingBoxes`, bạn có thể **extract text from image**, **recognize receipt image**, và nhận được **JSON bounding boxes** chính xác cho mỗi từ. Mã đầy đủ, có thể chạy được nằm trong đoạn mã ở trên, vì vậy bạn có thể chèn nó vào bất kỳ dự án .NET nào ngay bây giờ.

Tiếp theo? Hãy thử đưa JSON vào một trình xem front‑end để làm nổi bật từng từ, hoặc đẩy dữ liệu vào mô hình machine‑learning phân loại các mục trên biên lai. Bạn cũng có thể thử nghiệm với các ngôn ngữ khác, cài đặt DPI cao hơn, hoặc xử lý hàng loạt nhiều hình ảnh trong một vòng lặp.

Nếu gặp bất kỳ khó khăn nào, hãy nhớ các mẹo về đường dẫn tệp, DPI, và mảng ngôn ngữ. Đừng ngần ngại để lại bình luận hoặc mở issue trên repo GitHub bạn tạo cho bản demo này. Chúc lập trình vui vẻ, và tận hưởng việc biến hình ảnh thành JSON có cấu trúc!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
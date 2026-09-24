---
category: general
date: 2026-01-01
description: Hướng dẫn OCR bằng C# cho thấy cách trích xuất văn bản, tải hình ảnh
  để OCR và ghi JSON vào tệp bằng Aspose.OCR – hướng dẫn từng bước.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: vi
og_description: Hướng dẫn OCR bằng C# giúp bạn thực hiện việc trích xuất văn bản từ
  hình ảnh, tải hình ảnh cho OCR và ghi JSON vào tệp bằng Aspose.OCR.
og_title: Hướng dẫn OCR bằng C# – Trích xuất văn bản và xuất ra JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: Hướng dẫn OCR bằng C# – Trích xuất văn bản từ hình ảnh và xuất ra JSON
url: /vi/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng dẫn c# OCR – Trích xuất văn bản từ hình ảnh và xuất ra JSON

Bạn có bao giờ tự hỏi làm thế nào để trích xuất văn bản từ một hóa đơn đã quét mà không phải tốn hàng giờ viết các bộ phân tích tùy chỉnh? Bạn không đơn độc. Trong **c# OCR tutorial** chúng tôi sẽ chỉ cho bạn cách tải một hình ảnh để OCR, chạy engine nhận dạng, và sau đó **write JSON to file** để bạn có thể đưa dữ liệu vào các hệ thống downstream.

Hãy tưởng tượng bạn có một thư mục chứa các biên lai, mỗi file có tên `receipt1.png`, `receipt2.png`, và bạn cần một cách nhanh chóng để chuyển chúng thành các bản ghi JSON có thể tìm kiếm. Đó là vấn đề chúng ta sẽ giải quyết, và vào cuối bạn sẽ có một ứng dụng console sẵn sàng chạy thực hiện điều đó. Không có phụ thuộc nào ngoài Aspose.OCR, và không có phép màu—chỉ những bước rõ ràng, có thể tái tạo.

> **What you’ll learn**
> - How to **load image for OCR** using Aspose.OCR.
> - The best way to **how to extract text** and get confidence scores.
> - Converting the OCR result into a nicely structured **OCR image to JSON** payload.
> - Safely **write JSON to file** and verify the output.

## Yêu cầu trước

- .NET 6 SDK hoặc phiên bản mới hơn (code cũng chạy trên .NET Core).  
- Visual Studio 2022 hoặc bất kỳ trình soạn thảo nào bạn thích.  
- Gói NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  
- Một file ảnh (PNG, JPG, BMP) bạn muốn xử lý – trong demo chúng tôi sẽ dùng `invoice.png`.

Nếu bạn thiếu bất kỳ mục nào trong số này, hãy tải SDK từ trang của Microsoft và thêm gói NuGet qua Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

Bây giờ nền tảng đã sẵn sàng, hãy đi sâu vào phần thực thi thực tế.

## Bước 1: c# OCR tutorial – Khởi tạo Engine OCR

Trước khi chúng ta có thể **load image for OCR**, chúng ta cần một thể hiện của engine sẽ điều khiển quá trình nhận dạng. Lớp `OcrEngine` nhẹ, nhưng thực hành tốt là bọc nó trong một khối `using` để tài nguyên được giải phóng kịp thời.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Pro tip:* Nếu bạn dự định xử lý nhiều ảnh trong một batch, hãy tái sử dụng cùng một thể hiện `OcrEngine` thay vì tạo mới mỗi lần. Điều này giảm tải bộ nhớ và tăng tốc độ.

## Bước 2: Tải hình ảnh cho OCR

Bây giờ chúng ta thực sự **load image for OCR**. Aspose.OCR hỗ trợ nhiều định dạng, vì vậy bạn có thể chỉ tới một PNG, JPEG, hoặc thậm chí một TIFF đa trang. Phương thức `OcrImage.FromFile` đọc file và chuẩn bị nó cho việc nhận dạng.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **Why this matters:** Loading the image separately lets you inspect its dimensions, DPI, or even pre‑process it (e.g., binarization) before sending it to the engine. If the image is corrupted, `FromFile` will throw a clear exception, which you can catch and log.

## Bước 3: Cách trích xuất văn bản – Chạy nhận dạng

Với ảnh đã sẵn sàng, chúng ta cuối cùng có thể **how to extract text** từ nó. Phương thức `Recognize` trả về một đối tượng `OcrResult` chứa không chỉ văn bản thuần mà còn dữ liệu vị trí và điểm tin cậy cho mỗi từ.

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Edge case:* Some PDFs contain invisible text layers. If you feed a PDF page rendered as an image, the engine may see nothing. In those cases, consider using Aspose.PDF to extract the hidden layer first, then fall back to OCR only when needed.

## Bước 4: OCR image to JSON – Chuyển đổi kết quả

Lớp `OcrResult` cung cấp một helper tiện lợi `ToJson()` giúp tuần tự hoá toàn bộ tập kết quả—bao gồm hộp bao quanh và điểm tin cậy của mỗi từ—thành một chuỗi JSON. Đây là cách sạch nhất để đạt được **OCR image to JSON** mà không cần tự viết serializer.

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

Nếu bạn muốn một schema tùy chỉnh, bạn có thể lặp qua `ocrResult.Words` và xây dựng đối tượng của riêng mình, nhưng trong hầu hết các trường hợp JSON tích hợp đã đủ và đã được cấu trúc tốt.

## Bước 5: Ghi JSON vào tệp

Bây giờ là phần cuối cùng của câu đố: lưu trữ payload JSON. Phương thức `File.WriteAllText` đảm bảo file được tạo (hoặc ghi đè) một cách nguyên tử. Hãy chắc chắn thư mục đích tồn tại, nếu không bạn sẽ gặp `DirectoryNotFoundException`.

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Tip:* If you need UTF‑8 with BOM or a different encoding, use the overload that accepts an `Encoding` argument.

## Bước 6: Xác minh đầu ra

Một lệnh `Console.WriteLine` nhanh chóng cho chúng ta biết quá trình đã hoàn thành thành công. Bạn cũng có thể mở file JSON trong một trình xem để xác nhận cấu trúc.

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Đoạn JSON dự kiến

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

JSON bao gồm vị trí của mỗi từ, rất hữu ích nếu bạn muốn sau này làm nổi bật văn bản trong giao diện người dùng.

## Ví dụ Hoạt động Đầy đủ

Dưới đây là chương trình hoàn chỉnh, sẵn sàng sao chép‑dán. Thay `YOUR_DIRECTORY` bằng đường dẫn thực tế nơi ảnh của bạn nằm.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

Chạy chương trình (`dotnet run` từ thư mục dự án) và bạn sẽ thấy `invoice.json` bên cạnh file PNG gốc.

## Những Cạm Bẫy Thường Gặp & Cách Tránh

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **FileNotFoundException** when loading the image | Path typo or missing file | Use `Path.Combine` and check `File.Exists` before calling `FromFile`. |
| **Low confidence scores** | Poor image quality, low DPI | Pre‑process with `ocrImage.AdjustContrast` or upscale the image to 300 DPI. |
| **JSON file empty** | `ocrResult` returned null (engine failed) | Verify that the image format is supported and that the license (if any) is correctly applied. |
| **Performance bottleneck on large batches** | Re‑creating `OcrEngine` each iteration | Reuse a single `OcrEngine` instance across the batch, disposing only at the end. |

## Các Bước Tiếp Theo

Bây giờ bạn đã thành thạo **c# OCR tutorial**, bạn có thể muốn:

- **Batch process** một thư mục toàn bộ và tổng hợp các file JSON thành một cơ sở dữ liệu duy nhất.  
- **Integrate** kết quả với Azure Cognitive Search để tạo PDF có thể tìm kiếm.  
- **Add language support** bằng cách đặt `ocrEngine.Language = OcrLanguage.Spanish` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ).  
- **Post‑process** JSON để trích xuất bảng hoặc cặp khóa‑giá trị bằng các biểu thức chính quy.

Mỗi mở rộng này dựa trên các khái niệm cốt lõi chúng ta đã đề cập: tải ảnh cho OCR, trích xuất văn bản, chuyển đổi sang JSON, và ghi JSON ra đĩa.

---

### Kết luận

Trong **c# OCR tutorial** này chúng tôi đã đi qua mọi bước cần thiết để **load image for OCR**, **how to extract text**, chuyển đổi kết quả thành payload **OCR image to JSON**, và cuối cùng **write JSON to file**. Ví dụ code đầy đủ đã sẵn sàng đưa vào bất kỳ dự án .NET nào, và các giải thích cung cấp ngữ cảnh để bạn tùy chỉnh giải pháp cho các tình huống thực tế.

Hãy thử với bộ biên lai hoặc hóa đơn của riêng bạn—tinh chỉnh tiền xử lý ảnh, thử nghiệm các ngôn ngữ khác nhau, và quan sát JSON đầu ra phát triển. Nếu gặp khó khăn, hãy xem lại bảng cạm bẫy hoặc để lại bình luận bên dưới. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
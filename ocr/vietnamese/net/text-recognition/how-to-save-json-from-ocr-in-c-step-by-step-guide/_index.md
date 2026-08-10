---
category: general
date: 2026-02-19
description: Cách lưu JSON từ kết quả OCR trong C# – học cách trích xuất văn bản từ
  hình ảnh, ghi tệp JSON trong C#, và chuyển đổi hình ảnh sang JSON với Aspose OCR.
draft: false
keywords:
- how to save json
- extract text from image
- write json file c#
- convert image to json
- c# ocr tutorial
language: vi
og_description: Cách lưu JSON từ kết quả OCR trong C# rất dễ dàng. Hãy theo dõi hướng
  dẫn này để trích xuất văn bản từ hình ảnh và ghi file JSON theo phong cách C#.
og_title: Cách Lưu JSON Từ OCR trong C# – Hướng Dẫn Toàn Diện
tags:
- C#
- OCR
- JSON
title: Cách Lưu JSON Từ OCR trong C# – Hướng Dẫn Từng Bước
url: /vi/net/text-recognition/how-to-save-json-from-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Lưu JSON từ OCR trong C# – Hướng Dẫn Toàn Diện

Cách lưu json từ kết quả OCR trong C# là một nhu cầu phổ biến khi bạn chuyển đổi giấy tờ đã quét thành dữ liệu có cấu trúc. Trong hướng dẫn này, bạn sẽ thấy chính xác cách trích xuất văn bản từ hình ảnh, chuyển nó thành json, và cuối cùng ghi file json theo phong cách C#—không có lời vòng vo, chỉ có giải pháp hoạt động.

Bạn đã bao giờ cố gắng đọc một biên lai bằng máy quét, chỉ để kết thúc với một bức ảnh mờ mà bạn không thể tìm kiếm? Đó là vấn đề mà nhiều nhà phát triển gặp phải khi họ cần trích xuất dữ liệu từ hình ảnh. Khi kết thúc bài viết này, bạn sẽ có một ứng dụng console nhỏ đọc một hình ảnh, lấy văn bản bằng Aspose OCR, và lưu một file json sạch sẽ mà bạn có thể đưa vào bất kỳ dịch vụ downstream nào.

Chúng tôi sẽ bao phủ mọi thứ: gói NuGet bạn cần, mã chính xác (đầy đủ, có thể chạy, và được chú thích kỹ lưỡng), các lỗi thường gặp, và một cách nhanh chóng để xác minh đầu ra. Không cần kinh nghiệm OCR trước—chỉ cần hiểu cơ bản về C# và .NET.

## Yêu Cầu Trước

- .NET 6 SDK hoặc phiên bản mới hơn (mã nhắm tới .NET 6 nhưng hoạt động trên .NET 5+)
- Visual Studio 2022, VS Code, hoặc bất kỳ trình soạn thảo nào bạn thích
- Một file hình ảnh (`input.png`) bạn muốn xử lý
- Truy cập Internet để tải gói NuGet **Aspose.OCR**

Nếu bất kỳ mục nào còn thiếu, hãy tải chúng ngay; nếu không bạn sẽ lãng phí thời gian sau này.  

> **Mẹo chuyên nghiệp:** Aspose OCR cung cấp khóa dùng thử miễn phí—hoàn hảo để thử nghiệm mà không cần giấy phép.

## Bước 1: Cài Đặt Gói NuGet Aspose OCR

Đầu tiên, thêm thư viện thực hiện công việc nặng. Mở terminal trong thư mục dự án của bạn và chạy:

```bash
dotnet add package Aspose.OCR
```

Lệnh duy nhất này tải xuống các binary Aspose OCR mới nhất và thêm tham chiếu vào file `.csproj` của bạn.  

> **Tại sao bước này quan trọng:** Nếu không có gói, lớp `OcrEngine` sẽ không tồn tại, và bạn sẽ gặp lỗi biên dịch.  

Bây giờ gói đã sẵn sàng, hãy tạo khung cho ứng dụng console của chúng ta.

## Bước 2: Thiết Lập Cấu Trúc Dự Án

Tạo một dự án console mới nếu bạn chưa làm:

```bash
dotnet new console -n JsonExportOcr
cd JsonExportOcr
```

Trong `Program.cs` thay thế nội dung mặc định bằng ví dụ đầy đủ dưới đây. Chúng tôi sẽ đi qua từng dòng sau, nhưng việc có file sẵn giúp bạn sao chép‑dán mà không bỏ sót dấu ngoặc.

## Bước 3: Khởi Tạo OCR Engine (Trích Xuất Văn Bản Từ Hình Ảnh)

Dòng mã thực tế đầu tiên tạo một OCR engine và chỉ định nó tìm kiếm ký tự tiếng Anh. Bạn có thể chuyển sang `Language.Spanish` hoặc bất kỳ ngôn ngữ hỗ trợ nào khác, nhưng tiếng Anh là trường hợp phổ biến nhất.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3.1: Create an OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Step 3.2: Recognize text from the input image
        // Replace the path with where your image actually lives
        string inputPath = @"YOUR_DIRECTORY/input.png";
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);
```

**Điều gì đang xảy ra?**  
- `OcrEngine` là điểm vào cho Aspose OCR.  
- Đặt `Language` cải thiện độ chính xác vì engine có thể áp dụng các heuristics riêng cho ngôn ngữ.  
- `RecognizeImage` trả về một đối tượng `OcrResult` chứa tất cả các từ đã nhận dạng, điểm tin cậy và hộp bao quanh.

Nếu hình ảnh bị thiếu hoặc hỏng, câu lệnh guard sẽ in ra thông báo thân thiện và dừng lại—kiểm tra nhỏ này giúp bạn tránh lỗi null‑reference gây nhầm lẫn sau này.

## Bước 4: Chuyển Đổi Kết Quả OCR Sang JSON (Chuyển Đổi Hình Ảnh Sang JSON)

Aspose OCR đi kèm với một trợ giúp gọi là `JsonResultWriter`. Nó tuần tự hoá `OcrResult` thành một chuỗi JSON sạch sẽ phản ánh cấu trúc bạn mong đợi từ một REST API.

```csharp
        // Step 4: Convert the OCR result to a JSON string
        string jsonResult = JsonResultWriter.Write(ocrResult);
```

**Tại sao sử dụng `JsonResultWriter`?**  
- Nó tự động xử lý các đối tượng phức tạp (như các bộ sưu tập `Word` lồng nhau).  
- Bạn tránh việc tự viết serializer, có thể bỏ sót các trường tinh vi như phần trăm tin cậy.

Ở thời điểm này `jsonResult` trông tương đối như sau (được in đẹp để dễ đọc):

```json
{
  "PageCount": 1,
  "Pages": [
    {
      "PageNumber": 1,
      "Words": [
        {
          "Text": "Hello",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 50, "Height": 15 }
        },
        // … more words …
      ]
    }
  ]
}
```

Bạn có thể sao chép đoạn mã đó vào một trình xem JSON để khám phá cấu trúc.  

> **Trường hợp đặc biệt:** Nếu hình ảnh của bạn chứa nhiều trang, JSON sẽ bao gồm một mảng `Pages`—đảm bảo các bên tiêu thụ downstream có thể xử lý nó.

## Bước 5: Ghi JSON Vào Đĩa (Cách Lưu JSON)

Bây giờ là phần cốt lõi của hướng dẫn: **cách lưu json** vào một file trên đĩa. Lớp .NET `File` cho phép thực hiện điều này trong một dòng, nhưng chúng tôi sẽ thêm một chút xử lý lỗi để tăng độ bền.

```csharp
        // Step 5: Write the JSON string to an output file
        string outputPath = @"YOUR_DIRECTORY/output.json";
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
```

Đó là lúc bạn cuối cùng trả lời câu hỏi *cách lưu json*—file được tạo, ghi đè nếu đã tồn tại, và bạn nhận được thông báo console rõ ràng xác nhận thành công.

## Bước 6: Xác Minh Kết Quả

Sau khi chương trình kết thúc, mở `output.json` trong bất kỳ trình soạn thảo nào (VS Code, Notepad++, hoặc thậm chí trình duyệt). Bạn sẽ thấy một biểu diễn JSON được định dạng đẹp mắt của đầu ra OCR. Nếu bạn thấy các mảng `"Words": []` trống, hãy kiểm tra lại chất lượng hình ảnh—OCR gặp khó khăn với độ tương phản thấp hoặc nhiễu mạnh.

Bạn cũng có thể chạy một kiểm tra nhanh từ dòng lệnh:

```bash
dotnet run
```

Bạn sẽ thấy:

```
JSON saved to YOUR_DIRECTORY/output.json
```

Nếu bạn gặp lỗi, console sẽ cho bạn biết liệu file đầu vào bị thiếu hay thao tác ghi thất bại.

## Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là chương trình **đầy đủ** bạn có thể sao chép‑dán vào `Program.cs`. Thay thế `YOUR_DIRECTORY` bằng thư mục chứa `input.png`. Không cần file nào khác.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3: Initialize OCR engine (extract text from image)
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Define file paths
        string inputPath = @"YOUR_DIRECTORY/input.png";
        string outputPath = @"YOUR_DIRECTORY/output.json";

        // Validate input image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        // Recognize text
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Convert OCR result to JSON (convert image to json)
        string jsonResult = JsonResultWriter.Write(ocrResult);

        // Write JSON to disk (how to save json)
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
    }
}
```

Chạy chương trình, mở file đã tạo, và bạn đã hoàn thành thành công một **hướng dẫn c# ocr** cho thấy **cách lưu json** từ một hình ảnh.

## Các Vấn Đề Thường Gặp & Mẹo (Ghi File JSON C#)

| Vấn Đề | Nguyên Nhân | Cách Khắc Phục |
|-------|----------------|-----|
| **Mảng `Words` trống** | Hình ảnh quá tối hoặc độ phân giải thấp | Tiền xử lý hình ảnh (tăng độ tương phản, sử dụng DPI cao hơn) |
| **`File.WriteAllText` ném UnauthorizedAccessException** | Cố gắng ghi vào thư mục chỉ đọc | Chọn thư mục có quyền ghi (ví dụ: `%TEMP%` hoặc thư mục dự án của bạn) |
| **Thiếu gói NuGet** | Quên chạy `dotnet add package Aspose.OCR` | Chạy lại lệnh và biên dịch lại |
| **JSON là một dòng duy nhất** | `WriteAllText` ghi chuỗi thô mà không định dạng | Sử dụng `JsonResultWriter.Write(ocrResult, true)` nếu overload tồn tại, hoặc chạy đầu ra qua `JsonSerializer` với `WriteIndented = true` |

Những kiểm tra nhanh này giữ cho quy trình **ghi file json c#** của bạn suôn sẻ và ngăn ngừa những khoảnh khắc đáng sợ “không có gì xảy ra”.

## Các Bước Tiếp Theo (Trích Xuất Văn Bản Từ Hình Ảnh & Thêm Nữa)

Bây giờ bạn đã biết **cách lưu json**, bạn có thể muốn:

- **Lưu** 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
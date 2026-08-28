---
category: general
date: 2026-01-02
description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR trong C#. Tìm hiểu cách
  chuyển đổi hình ảnh sang định dạng JSONL một cách nhanh chóng và đáng tin cậy.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR và chuyển đổi sang
  định dạng JSONL. Hướng dẫn C# chi tiết từng bước cho các nhà phát triển.
og_title: Trích xuất văn bản từ hình ảnh – Chuyển đổi sang JSONL trong C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Trích xuất văn bản từ hình ảnh và chuyển sang JSONL – Hướng dẫn C#
url: /vi/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh và Chuyển đổi sang JSONL – Hướng dẫn C# đầy đủ

Bạn đã bao giờ cần **extract text from image** nhưng không chắc thư viện nào sẽ cho bạn đầu ra sạch sẽ, có cấu trúc? Bạn không phải là người duy nhất. Trong nhiều dự án xử lý biên lai hoặc số hoá tài liệu, nút thắt là chuyển đổi bitmap thành văn bản có thể tìm kiếm *và* định dạng có thể đọc được bởi máy.

Tin tốt? Với Aspose OCR bạn có thể **extract text from image** và, chỉ với vài dòng mã, **convert image to JSONL** cho phân tích downstream. Hướng dẫn này sẽ đưa bạn qua toàn bộ quá trình, từ tải PNG đến ghi file JSON‑Lines có thể được truyền vào pipeline dữ liệu.

> **Gợi ý:** Nếu bạn đã đang sử dụng .NET 6 hoặc phiên bản mới hơn, cùng một đoạn mã sẽ hoạt động mà không cần cấu hình thêm.

## Yêu cầu trước — Bạn cần có gì

- **.NET 6 SDK** (hoặc bất kỳ phiên bản .NET gần đây nào)
- Gói NuGet **Aspose.OCR**  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** để tuần tự hoá  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Một hình ảnh mẫu (ví dụ, `receipt.png`) đặt trong thư mục bạn có thể tham chiếu.
- Một IDE hoặc trình soạn thảo mà bạn chọn—Visual Studio, VS Code, Rider, v.v.

Không cần cài đặt phức tạp, không dịch vụ bên ngoài, chỉ một vài gói NuGet.

![Trích xuất văn bản từ hình ảnh bằng C#](https://example.com/assets/ocr-sample.png)

*Alt text: trích xuất văn bản từ hình ảnh bằng C# với Aspose OCR*

## Bước 1: Tải Hình ảnh Bạn Muốn Xử lý  

Điều đầu tiên bạn làm khi muốn **extract text from image** là cung cấp cho engine OCR một bitmap. Sử dụng `System.Drawing.Bitmap` rất đơn giản và hoạt động với hầu hết các định dạng raster.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Tại sao điều này quan trọng:** Tải hình ảnh dưới dạng `Bitmap` cung cấp cho engine OCR quyền truy cập trực tiếp vào pixel, giúp cải thiện tốc độ và độ chính xác nhận dạng so với việc truyền luồng byte thô.

## Bước 2: Cấu hình Aspose OCR cho Đầu ra JSON‑Lines  

Aspose OCR cho phép bạn chỉ định ngôn ngữ, định dạng đầu ra và một vài tùy chỉnh hiệu năng. Ở đây chúng ta yêu cầu **JSON‑Lines** (một đối tượng JSON mỗi dòng) vì nó hoàn hảo cho việc xử lý dòng‑đến‑dòng sau này.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần biên lai đa ngôn ngữ, đặt `Language = Language.Multilingual` hoặc truyền một mảng các giá trị `Language`.

## Bước 3: Chạy OCR và Ghi lại Kết quả  

Bây giờ chúng ta thực sự **extract text from image**. Phương thức `Recognize` trả về một đối tượng `OcrResult` chứa một tập hợp các đối tượng `OcrLine`, mỗi đối tượng đại diện cho một dòng văn bản đã nhận dạng cùng với hộp bao quanh của nó.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

Tại thời điểm này `ocrResult.Lines` chứa mọi thứ bạn cần—văn bản thô, điểm tin cậy và tọa độ.

## Bước 4: Tuần tự hoá Các Dòng thành JSON‑Lines  

Chúng ta sẽ chuyển tập hợp thành một chuỗi JSON được thụt lề đẹp mắt. Mặc dù JSON‑Lines thường gọn gàng, việc thêm thụt lề giúp file dễ kiểm tra hơn trong quá trình phát triển.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Biến `jsonLines` kết quả trông như sau (được cắt ngắn để ngắn gọn):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Mỗi dòng kết thúc bằng ký tự xuống dòng, tạo cho bạn một file **JSONL** (JSON‑Lines) thực sự.

## Bước 5: Ghi JSON‑Lines ra Đĩa  

Cuối cùng, chúng ta lưu kết quả để các dịch vụ khác—như Spark, Logstash, hoặc một script Bash đơn giản—có thể tiêu thụ nó từng dòng một.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Khi bạn mở `receipt.jsonl` bạn sẽ thấy một đối tượng JSON mỗi dòng, sẵn sàng để stream.

## Bước 6: Xác minh Xuất dữ liệu  

Một kiểm tra nhanh giúp bạn tiết kiệm hàng giờ debug sau này. Hãy đọc lại vài dòng đầu và in chúng ra console.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Đầu ra console điển hình:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Nếu bạn thấy tương tự, chúc mừng—bạn đã thành công **extract text from image** và **convert image to JSONL**.

## Những Cạm Bẫy Thường Gặp & Cách Tránh  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank output** | Đường dẫn hình ảnh không đúng hoặc file không đọc được. | Sử dụng `File.Exists(imagePath)` trước khi tạo bitmap. |
| **Low confidence scores** | Hình ảnh mờ hoặc độ tương phản thấp. | Tiền xử lý hình ảnh (ví dụ, `Bitmap.RotateFlip`, `Graphics.Clear`) hoặc tăng DPI. |
| **Incorrect language** | OCR mặc định là tiếng Anh nhưng biên lai ở ngôn ngữ khác. | Đặt `options.Language = Language.Spanish` (hoặc enum phù hợp). |
| **JSONL appears as a single JSON array** | Bạn đã dùng `Formatting.None` mà không xử lý xuống dòng. | Đảm bảo mỗi đối tượng được tuần tự hoá kết thúc bằng `Environment.NewLine`. |

## Ví dụ Hoạt Động Đầy Đủ  

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Dán vào dự án console và nhấn **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Kết quả mong đợi:** Một file `receipt.jsonl` chứa một đối tượng JSON mỗi dòng, mỗi đối tượng có các trường `Text`, `Confidence`, và `BoundingBox`. Bây giờ bạn có thể đưa file này vào bất kỳ pipeline phân tích nào tiêu thụ JSONL.

## Các Bước Tiếp Theo – Vượt Qua OCR Cơ Bản  

- **Batch processing:** Đóng gói logic trên trong một vòng lặp `foreach` để xử lý toàn bộ thư mục chứa biên lai.  
- **Parallelism:** Sử dụng `Parallel.ForEach` để tăng tốc đa lõi khi xử lý hàng ngàn hình ảnh.  
- **Post‑processing:** Loại bỏ các dòng có độ tin cậy thấp (`Confidence < 0.9`) trước khi lưu.  
- **Integration:** Đẩy JSONL trực tiếp tới Azure Blob Storage hoặc AWS S3 bằng các SDK tương ứng.  
- **Alternative formats:** Thay đổi `OutputFormat` thành `PlainText` hoặc `Xml` nếu hệ thống downstream của bạn ưu tiên các định dạng đó.  

## Kết luận  

Bạn hiện có một giải pháp toàn diện, đầu‑cuối cho việc **extracting text from image** và **converting image to JSONL** bằng Aspose OCR trong C#. Hướng dẫn đã bao phủ mọi thứ từ tải bitmap đến xác minh đầu ra, cùng một số mẹo thực tế để giữ pipeline của bạn vững chắc.

Hãy thử với các biên lai, hoá đơn hoặc mẫu quét của bạn—xem engine OCR biến pixel thành dữ liệu có thể tìm kiếm, cấu trúc theo dòng trong vài giây. Nếu gặp các trường hợp đặc biệt (ví dụ, ảnh quét lệch hoặc văn bản đa ngôn ngữ), hãy xem lại phần *RecognitionOptions* và điều chỉnh ngôn ngữ hoặc các bước tiền xử lý.

Chúc lập trình vui vẻ, và chúc pipeline dữ liệu của bạn luôn sạch sẽ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
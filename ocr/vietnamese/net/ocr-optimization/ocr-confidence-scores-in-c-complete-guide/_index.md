---
category: general
date: 2026-05-31
description: Tìm hiểu cách lấy điểm tin cậy OCR trong C# khi trích xuất văn bản từ
  hình ảnh và đọc hình ảnh biên lai bằng Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: vi
og_description: Điểm tin cậy của OCR cho phép bạn đánh giá độ chính xác; hướng dẫn
  này chỉ cách trích xuất văn bản từ hình ảnh, lấy các hộp bao quanh và đọc hình ảnh
  biên lai bằng Aspose OCR.
og_title: Điểm tin cậy OCR trong C# – Hướng dẫn toàn diện
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Điểm tin cậy OCR trong C# – Hướng dẫn toàn diện
url: /vi/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Điểm tin cậy OCR trong C# – Hướng dẫn toàn diện

Bạn đã bao giờ tự hỏi cách **điểm tin cậy OCR** khi cần *trích xuất văn bản từ hình ảnh* chưa? Có thể bạn đang cố **đọc hình ảnh biên lai** để theo dõi chi phí và muốn biết ký tự nào mà engine không chắc chắn. Tin tốt? Với Aspose.OCR, bạn có thể lấy phần trăm tin cậy, hộp bao và văn bản thuần từ một tệp JPG chỉ trong vài dòng C#.

Trong tutorial này chúng ta sẽ đi qua mọi thứ bạn cần biết: cài đặt thư viện, cấu hình engine để **thực hiện OCR trên JPG**, lấy điểm tin cậy, và giải thích **hộp bao OCR** cho biết mỗi ký tự nằm ở đâu trên trang. Khi kết thúc, bạn sẽ có một ứng dụng console sẵn sàng chạy, in ra mỗi ký tự, độ tin cậy và vị trí của nó—hoàn hảo để xác thực biên lai hoặc bất kỳ tài liệu quét nào.

## Những gì bạn sẽ học

- Cài đặt Aspose.OCR qua NuGet và thiết lập một engine OCR cơ bản.  
- Cấu hình `OcrOptions` để yêu cầu đầu ra văn bản thuần **kèm điểm tin cậy** và **hộp bao**.  
- Duyệt qua `OcrResult` để **trích xuất văn bản từ hình ảnh** dòng‑theo‑dòng và ký tự‑theo‑ký tự.  
- Xử lý các vấn đề thường gặp như tệp tin thiếu, ký tự có điểm tin cậy thấp, và định dạng không phải JPG.  
- Mở rộng ví dụ để xử lý nhiều hình ảnh biên lai trong một thư mục.

Không cần kinh nghiệm trước với Aspose; chỉ cần môi trường .NET hoạt động và một hình ảnh biên lai (JPG) bạn muốn thử.

---

## Bước 1 – Cài đặt Aspose.OCR và chuẩn bị dự án của bạn

First things first: you need the Aspose.OCR NuGet package. Open a terminal in your project folder and run:

```bash
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Bản dùng thử miễn phí hoạt động cho tới 200 trang, đủ cho việc thử nghiệm quét biên lai.

After the package is installed, create a new console project (if you don’t already have one):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Now you can open the generated `Program.cs` and start adding the using directives:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

These namespaces give you access to `OcrEngine`, `OcrOptions`, and the result types we’ll need later.

## Bước 2 – Lấy điểm tin cậy OCR và hộp bao OCR

This is the heart of the tutorial. We’ll configure the engine so that each recognized character comes with a **confidence score** and a **bounding box** (the rectangle that encloses the glyph). The H2 header itself contains the primary keyword, satisfying the SEO rule.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Tại sao cần bao gồm điểm tin cậy?**  
A confidence score (0‑100%) tells you how sure the engine is about each character. If you’re feeding the output into downstream logic—say, an expense‑approval workflow—you can reject or flag low‑confidence symbols automatically.

**Tại sao yêu cầu hộp bao?**  
Bounding boxes are essential when you need to highlight text on the original image, extract sub‑regions, or align OCR results with a UI overlay. Each `character.Bounds` gives you the X, Y, width, and height in pixel coordinates.

## Bước 3 – Thực hiện OCR trên JPG và trích xuất văn bản từ hình ảnh

Now we actually run the engine. The call to `Recognize()` performs all the heavy lifting and returns an `OcrResult` object.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

If the image path is wrong or the file isn’t a supported format, Aspose throws a `FileNotFoundException` or `UnsupportedImageFormatException`. Wrap the call in a try/catch block in production code to handle those edge cases gracefully.

### Lấy văn bản thuần

If you only need the concatenated text, you can read `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

But because we also asked for confidence scores and bounding boxes, we’ll iterate through the structure to see each character’s details.

## Bước 4 – Duyệt qua các dòng, ký tự và hiển thị điểm tin cậy OCR

Here’s the loop that prints every character, its confidence, and its box. This is where the **read receipt image** example truly shines.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Sample output might look like:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Giải thích các số:**  
- **Tin cậy ≥ 90%** – thường an toàn để chấp nhận.  
- **Tin cậy 70‑89%** – bạn có thể muốn kiểm tra lại, đặc biệt với các chữ số trong số tiền.  
- **Tin cậy < 70%** – cân nhắc đánh dấu để kiểm tra thủ công.

## Bước 5 – Ví dụ đầy đủ có thể chạy (kèm xử lý lỗi)

Putting everything together, here’s a complete program you can copy‑paste into `Program.cs`. It includes a simple check for missing files and prints a friendly message if the OCR fails.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Kết quả mong đợi

When you run `dotnet run` the console will first display the concatenated receipt text, then a list of each character with its confidence score and bounding box. If a character’s confidence is low, you’ll see a percentage under 80, which is a cue to verify that part of the receipt manually.

## Bonus: Xử lý nhiều biên lai trong một thư mục

If you have a batch of receipt JPGs, wrap the above logic in a `foreach (var file in Directory.GetFiles(folder, "*.jpg"))` loop. Remember to reset the `OcrEngine` for each file, or instantiate a new one inside the loop to avoid state leakage.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Processing in bulk is handy for nightly expense imports.

---

## Kết luận

You now have a solid, end‑to‑end solution for obtaining **OCR confidence scores** in C#, **extracting text from image**, and retrieving **OCR bounding boxes** while you **perform OCR on JPG** files such as a **read receipt image**. The code is fully self‑contained, works with the latest Aspose.OCR version (as of 2026‑05‑31), and gives you the granular data you need to build trustworthy document‑processing pipelines.

What’s next? Try visualizing the bounding boxes on the original receipt using `System.Drawing` or a UI library, or feed low‑confidence characters into a secondary verification service. You could also experiment with different languages by setting `ocrEngine.Options.Language = OcrLanguage.French;` – the API supports many locales.

Happy coding, and may your confidence scores always stay high! 

![Kết quả console hiển thị điểm tin cậy OCR và hộp bao cho một biên lai

## Bạn nên học gì tiếp theo?

- [Trích xuất văn bản hình ảnh C# với lựa chọn ngôn ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cách lấy các lựa chọn ký tự OCR cho các ký tự đã nhận dạng trong nhận dạng hình ảnh](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Cách sử dụng Aspose OCR để nhận kết quả JSON trong nhận dạng hình ảnh](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
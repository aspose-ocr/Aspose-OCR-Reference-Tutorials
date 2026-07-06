---
category: general
date: 2026-04-26
description: Trích xuất văn bản từ hình ảnh trong C# bằng Aspose.OCR và học cách chuyển
  đổi hình ảnh sang định dạng JSON và XML trong vài phút.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: vi
og_description: Trích xuất văn bản từ hình ảnh trong C# bằng Aspose.OCR. Tìm hiểu
  từng bước cách chuyển kết quả sang JSON và XML ngay lập tức.
og_title: Trích xuất văn bản từ hình ảnh trong C# – Chuyển sang JSON & XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Trích xuất văn bản từ hình ảnh trong C# – Chuyển sang JSON & XML
url: /vi/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ hình ảnh trong C# – Chuyển sang JSON & XML

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** trong một dự án .NET nhưng cảm thấy bế tắc ở câu hỏi “làm sao tôi thực sự lấy dữ liệu ra?” Bạn không phải là người duy nhất. Trong nhiều ứng dụng thực tế—như xử lý hoá đơn, quét biên lai, hoặc xác thực thẻ—việc lấy các ký tự thô từ một bức ảnh là bước đầu tiên, quan trọng.  

Tin tốt? Với Aspose.OCR bạn có thể thực hiện điều này chỉ trong vài dòng code, sau đó ngay lập tức **chuyển đổi hình ảnh sang JSON** hoặc **chuyển đổi hình ảnh sang XML** cho các hệ thống downstream. Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ mã sẵn sàng chạy, giải thích lý do mỗi phần quan trọng, và cho bạn một vài mẹo để tránh các lỗi thường gặp.

---

## Những gì bạn cần

- **.NET 6+** (bất kỳ SDK mới nào cũng hoạt động; mẫu hướng tới .NET 6)
- **Aspose.OCR for .NET** gói NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Một tệp hình ảnh (PNG, JPG, v.v.) chứa văn bản có thể in; chúng tôi sẽ sử dụng `invoice.png` làm ví dụ.
- Một trình soạn thảo mã—Visual Studio, VS Code, hoặc Rider—bất kỳ cái nào bạn thích.

Đó là tất cả. Không cần engine OCR bổ sung, không dịch vụ bên ngoài, chỉ một gói NuGet duy nhất.

## Bước 1: Thiết lập Engine OCR – Cách trích xuất văn bản từ hình ảnh

Đầu tiên chúng ta tạo một thể hiện `OcrEngine` và chỉ định nó tới tệp hình ảnh. Bước này là nền tảng; nếu không tải đúng hình ảnh, engine sẽ không nhận dạng được gì.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Tại sao điều này quan trọng:**  

- `OcrEngine` bao bọc tất cả các bước tiền xử lý hình ảnh mức thấp (nhị phân hoá, chỉnh nghiêng).
- Tải hình ảnh bằng `ImageStream.FromFile` đảm bảo engine đọc đúng byte, giữ nguyên DPI và độ sâu màu—cả hai đều có thể ảnh hưởng đến độ chính xác nhận dạng.

> **Mẹo chuyên nghiệp:** Nếu các hình ảnh nguồn của bạn ở dạng stream (ví dụ, được tải lên qua một web API), hãy sử dụng `ImageStream.FromStream(yourStream)` thay vì `FromFile`.

## Bước 2: Cho Engine biết Ngôn ngữ Mong đợi – trích xuất văn bản từ hình ảnh một cách chính xác

Aspose.OCR hỗ trợ nhiều bảng chữ cái. Việc chỉ định ngôn ngữ đúng sẽ thu hẹp bộ ký tự và tăng độ chính xác.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Tại sao:**  

Khi bạn đặt `Language.Latin`, engine OCR sẽ bỏ qua các glyph Cyrillic hoặc Asian, giảm các kết quả dương tính giả. Nếu sau này bạn cần xử lý tài liệu đa ngôn ngữ, bạn có thể chuyển sang `Language.Multilingual` hoặc kết hợp các ngôn ngữ.

## Bước 3: Chạy Quy trình Nhận dạng – trích xuất văn bản từ hình ảnh trong một lần gọi

Bây giờ chúng ta thực sự nhận dạng văn bản. Phương thức `Recognize` trả về một đối tượng `RecognitionResult` chứa văn bản thô, điểm tin cậy, và thậm chí dữ liệu bố cục.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Tại sao:**  

Gọi `Recognize` một lần là đủ vì engine bên trong thực hiện tiền xử lý, phân đoạn và phân loại ký tự. Thuộc tính `Text` cung cấp cho bạn một chuỗi thuần túy, hoàn hảo cho việc ghi log hoặc xác thực nhanh.

## Bước 4: Chuyển đổi Kết quả sang JSON – chuyển hình ảnh sang json dễ dàng

Nhiều dịch vụ hiện đại ưu tiên payload dạng JSON. Aspose.OCR cung cấp phương thức `ToJson` tiện lợi, nó tuần tự hoá toàn bộ `RecognitionResult`, bao gồm các giá trị tin cậy và hộp giới hạn.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Tại sao bạn có thể muốn JSON:**  

- **Tính tương thích:** Các ứng dụng front‑end (React, Angular) có thể tiêu thụ JSON trực tiếp.
- **Gỡ lỗi:** JSON bao gồm độ tin cậy cho từng ký tự, cho phép bạn đánh dấu các từ có độ tin cậy thấp để xem xét thủ công.

> **Trường hợp đặc biệt:** Nếu hệ thống downstream của bạn chỉ cần văn bản thuần, bạn có thể lấy `recognitionResult.Text` và đóng gói nó trong một đối tượng JSON tùy chỉnh thay vì payload đầy đủ của Aspose.

## Bước 5: Chuyển đổi Kết quả sang XML – chuyển hình ảnh sang xml cho hệ thống legacy

Một số doanh nghiệp vẫn dựa vào các schema XML để trao đổi dữ liệu. Phương thức `ToXml` tương tự `ToJson` nhưng xuất ra XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Tại sao XML:**  

- **Kiểm tra schema:** Bạn có thể định nghĩa một XSD phù hợp với cấu trúc mà Aspose tạo ra, đảm bảo tuân thủ hợp đồng.
- **Tích hợp:** Các hệ thống ERP hoặc quản lý tài liệu cũ thường có khả năng phân tích XML ngay từ đầu.

## Ví dụ Hoạt động Đầy đủ – Mã một chỗ

Dưới đây là chương trình đầy đủ kết nối mọi thành phần. Sao chép‑dán vào một dự án console mới (`dotnet new console`) và chạy.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Kết quả mong đợi (console):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

Các tệp JSON và XML sẽ chứa cấu trúc phong phú hơn, ví dụ:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

### Nếu hình ảnh bị mờ hoặc xoay thì sao?

Aspose.OCR tự động chỉnh nghiêng hầu hết các hình ảnh, nhưng trong các trường hợp cực đoan bạn có thể muốn tiền xử lý bằng `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Thêm một chút tăng độ tương phản (`ImageProcessor.AdjustContrast`) cũng có thể cải thiện điểm tin cậy.

### Tôi có thể trích xuất văn bản từ PDF không?

Có—đầu tiên chuyển mỗi trang PDF thành hình ảnh (ví dụ, dùng Aspose.PDF hoặc thư viện miễn phí như PDFium) rồi đưa các hình ảnh đó vào quy trình OCR giống nhau.

### Làm sao tôi xử lý đa ngôn ngữ trong một tài liệu?

Đặt `ocrEngine.Language = Language.Multilingual;` hoặc kết hợp các ngôn ngữ cụ thể:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Be aware that broader language sets may

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
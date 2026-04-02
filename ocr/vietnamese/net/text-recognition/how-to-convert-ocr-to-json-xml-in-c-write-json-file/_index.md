---
category: general
date: 2026-04-01
description: Cách chuyển đổi đầu ra OCR sang JSON và XML trong C# – học cách trích
  xuất văn bản từ hình ảnh và ghi file JSON C# bằng Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: vi
og_description: Cách chuyển đổi kết quả OCR thành các tệp JSON và XML có cấu trúc
  bằng C#. Hướng dẫn từng bước để trích xuất văn bản từ hình ảnh và ghi tệp JSON bằng
  C#.
og_title: Cách chuyển đổi OCR sang JSON & XML trong C# – Ghi tệp JSON
tags:
- OCR
- C#
- Aspose
title: Cách chuyển đổi OCR sang JSON & XML trong C# – Ghi tệp JSON
url: /vi/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Chuyển Đổi OCR sang JSON & XML trong C# – Ghi Tập Tin JSON

**Cách chuyển đổi OCR** kết quả thành một thứ bạn thực sự có thể sử dụng là câu hỏi mà nhiều nhà phát triển đặt ra. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách trích xuất văn bản từ một hình ảnh, chuyển đầu ra OCR thành JSON và XML được định dạng đẹp mắt, và sau đó ghi các tệp này vào đĩa bằng C#.

Nếu bạn từng nhìn chằm chằm vào một chuỗi OCR thô và nghĩ, “Phải có cách tốt hơn để lưu trữ cái này,” thì bạn đang ở đúng nơi. Khi kết thúc, bạn sẽ có một chương trình hoàn chỉnh, có thể chạy được mà không chỉ **extracts text from image** files but also knows how to **write JSON file C#** and **write XML file C#** without breaking a sweat.

## Những gì bạn cần

- **.NET 6.0** hoặc mới hơn (mã này cũng hoạt động với .NET Framework 4.6+).  
- **Aspose.OCR** package NuGet – cài đặt bằng `dotnet add package Aspose.OCR`.  
- Một hình ảnh chứa văn bản (ví dụ: `invoice.png`).  
- Bất kỳ IDE nào bạn thích – Visual Studio, Rider, hoặc VS Code đều được.

> **Mẹo chuyên nghiệp:** Giữ các tệp hình ảnh trong một thư mục riêng (ví dụ: `Resources/`) để các đường dẫn luôn gọn gàng.

## Bước 1: Thiết lập Engine OCR – Cách chuyển đổi OCR

Đầu tiên, chúng ta tạo một thể hiện `OcrEngine` và chỉ định ngôn ngữ cần nhận dạng. Trong hầu hết các trường hợp, tiếng Anh là đủ, nhưng bạn có thể thay `Language.English` bằng bất kỳ ngôn ngữ nào được hỗ trợ.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Tại sao điều này quan trọng:** Khởi tạo engine với ngôn ngữ đúng sẽ cải thiện độ chính xác đáng kể, đặc biệt đối với các script không phải Latin.

## Bước 2: Nhận dạng Văn bản – Trích xuất Văn bản từ Hình ảnh

Bây giờ chúng ta đưa hình ảnh vào engine. Phương thức `Recognize` trả về một đối tượng `OcrResult` chứa văn bản thô cũng như dữ liệu vị trí.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Nếu không tìm thấy hình ảnh, `Recognize` sẽ ném ra `FileNotFoundException`. Để demo đơn giản, chúng tôi sẽ giả định đường dẫn đúng, nhưng trong môi trường thực tế bạn nên bọc nó trong khối try‑catch.

## Bước 3: Chuyển đổi Kết quả sang JSON – Ghi Tập tin JSON C#

Aspose.OCR làm cho việc tuần tự hoá trở nên dễ dàng. Phương thức `ToJson` nhận một cờ `indent` để tạo ra đầu ra được định dạng đẹp, rất phù hợp khi bạn muốn mở tệp trong trình soạn thảo văn bản.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Mẫu JSON Dự Kiến

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Cách trích xuất văn bản:** Thuộc tính `Text` cung cấp cho bạn chuỗi thuần túy mà bạn có thể đưa vào các dịch vụ khác (chỉ mục tìm kiếm, cơ sở dữ liệu, v.v.).

## Bước 4: Lưu JSON – Ghi Tập tin JSON C# (Tiếp tục)

Khi chuỗi JSON đã sẵn sàng, chúng ta chỉ cần ghi nó vào tệp bằng `File.WriteAllText`. Điều này đảm bảo mã hoá UTF‑8 theo mặc định.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Bây giờ bạn có một tệp `invoice.json` nằm cạnh hình ảnh của mình, sẵn sàng cho quá trình xử lý tiếp theo.

## Bước 5: Chuyển đổi Kết quả sang XML – Ghi Tập tin XML C#

Nếu bạn ưu tiên XML cho các hệ thống legacy, phương thức `ToXml` sẽ thực hiện phần công việc nặng. Giống như `ToJson`, nó cũng hỗ trợ định dạng đẹp.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Mẫu XML Dự Kiến

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Bước 6: Lưu XML – Ghi Tập tin XML C# (Tiếp tục)

Lưu XML giống hệt bước JSON; chỉ cần chỉ đến phần mở rộng `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Ví dụ Hoạt Động Đầy Đủ

Kết hợp tất cả lại, đây là chương trình hoàn chỉnh mà bạn có thể sao chép và dán vào một ứng dụng console:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Chạy chương trình, và bạn sẽ thấy hai tệp mới—`invoice.json` và `invoice.xml`—ở đúng vị trí bạn chỉ định. Mở chúng để xác nhận cấu trúc khớp với các mẫu ở trên.

## Câu hỏi Thường gặp & Trường hợp Cạnh

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu hình ảnh chứa nhiều ngôn ngữ thì sao?** | Tạo các thể hiện `OcrEngine` riêng cho mỗi ngôn ngữ hoặc sử dụng `Language.Multi` nếu được hỗ trợ. |
| **Tôi có thể kiểm soát định dạng đầu ra (ví dụ, loại bỏ dữ liệu vùng) không?** | Có. Cả `ToJson` và `ToXml` đều chấp nhận các tham số tùy chọn để lọc trường; xem tài liệu Aspose.OCR cho `ExportOptions`. |
| **Làm sao để xử lý các PDF lớn với nhiều trang?** | Xử lý từng trang riêng lẻ, tổng hợp kết quả, sau đó tuần tự hoá một lần. |
| **Đầu ra có an toàn UTF‑8 không?** | Chắc chắn—Aspose.OCR sử dụng Unicode nội bộ, và `File.WriteAllText` ghi dưới dạng UTF‑8 theo mặc định. |
| **Về hiệu năng thì sao?** | OCR tiêu tốn nhiều CPU. Đối với các công việc batch, hãy cân nhắc thực hiện song song trên các lõi hoặc sử dụng API đám mây của Aspose. |

## Kết luận

Bây giờ bạn đã biết **cách chuyển đổi OCR** kết quả thành cả JSON và XML bằng C#. Bằng cách làm theo các bước trên, bạn có thể **trích xuất văn bản từ hình ảnh**, sau đó **ghi tập tin JSON C#** và **ghi tập tin XML C#** chỉ với một vài dòng mã. Cách tiếp cận này nhanh, đáng tin cậy và hoạt động với bất kỳ loại hình ảnh nào mà Aspose.OCR hỗ trợ.

Sẵn sàng cho thử thách tiếp theo? Hãy thử cung cấp the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
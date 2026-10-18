---
category: general
date: 2026-02-28
description: cách chạy OCR trong C# bằng Aspose OCR – học cách trích xuất văn bản
  từ hình ảnh, chuyển đổi hình ảnh sang JSON hoặc XML chỉ trong vài bước.
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: vi
og_description: cách chạy OCR trong C# bằng Aspose OCR – khám phá cách trích xuất
  văn bản từ hình ảnh và chuyển đổi hình ảnh sang JSON hoặc XML với một ví dụ đã sẵn
  sàng chạy.
og_title: Cách chạy OCR với Aspose OCR trong C# – Hướng dẫn đầy đủ
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cách chạy OCR với Aspose OCR trong C# – Hướng dẫn đầy đủ
url: /vi/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách chạy OCR với Aspose OCR trong C# – Hướng dẫn toàn diện

Nếu bạn đang thắc mắc **cách chạy OCR** trên ảnh biên lai bằng C#, bạn đã đến đúng nơi. Trong hướng dẫn này, chúng ta sẽ thực hiện **trích xuất văn bản từ ảnh** và sau đó **chuyển ảnh sang JSON** hoặc **chuyển ảnh sang XML** bằng Aspose OCR—tất cả trong một chương trình tự chứa duy nhất.

Hãy tưởng tượng bạn đang xây dựng một ứng dụng theo dõi chi phí và cần lấy các mục chi tiêu từ các biên lai được chụp ảnh. Nhập liệu thủ công từng mục thật là phiền phức, đúng không? Khi kết thúc hướng dẫn này, bạn sẽ có một đoạn mã có thể tái sử dụng để đọc bất kỳ ảnh nào, trả về văn bản có cấu trúc, và cung cấp cả dạng JSON và XML sẵn sàng cho các quy trình xử lý tiếp theo.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- .NET 6.0 SDK hoặc mới hơn (mã cũng chạy trên .NET Framework 4.8)
- Visual Studio 2022 (hoặc bất kỳ trình soạn thảo nào bạn thích)
- Gói NuGet **Aspose.OCR** đang hoạt động (`Install-Package Aspose.OCR`)
- Một ảnh mẫu (ví dụ: `receipt.png`) được đặt trong thư mục bạn có thể tham chiếu

Không cần cấu hình bổ sung; thư viện đã bao gồm tất cả các mô hình OCR cần thiết.

![Receipt image for OCR processing – how to run OCR](receipt.png)

> *Văn bản thay thế: Ảnh biên lai để xử lý OCR – cách chạy OCR*

## Triển khai từng bước

Dưới đây chúng tôi chia giải pháp thành các phần logic. Mỗi bước giải thích **tại sao** chúng ta thực hiện, không chỉ **cái gì** trong mã.

### 1️⃣ Khởi tạo OCR Engine – nền tảng của **cách chạy OCR**

Lớp `OcrEngine` là điểm vào. Khi khởi tạo, nó sẽ tải các mô hình ngôn ngữ nội bộ và chuẩn bị engine cho việc nhận dạng.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **Mẹo:** Sử dụng lại cùng một `OcrEngine` cho nhiều ảnh sẽ giảm việc tiêu tốn bộ nhớ và tăng tốc xử lý hàng loạt.

### 2️⃣ Tải ảnh – cốt lõi của **trích xuất văn bản từ ảnh**

Aspose OCR làm việc với lớp `Image` riêng của nó. Việc dùng câu lệnh `using` đảm bảo tay cầm tệp được giải phóng kịp thời.

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

Nếu ảnh ở định dạng khác (BMP, TIFF, PDF), cùng một phương thức `Load` sẽ xử lý—không cần chuyển đổi thêm.

### 3️⃣ Thực hiện nhận dạng OCR – trung tâm của **cách chạy OCR**

Gọi `Recognize` thực hiện các công việc nặng: phân tích bố cục, tách ký tự, và phân loại theo ngôn ngữ.

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

Đối tượng `OcrResult` trả về chứa văn bản thô, điểm tin cậy, và cây bố cục chi tiết có thể được tuần tự hoá.

### 4️⃣ Chuyển ảnh sang JSON – cách đơn giản để **chuyển ảnh sang json**

JSON rất phù hợp cho API web hoặc kho dữ liệu NoSQL. Phương thức `ToJson` cho bạn một chuỗi được định dạng đẹp, giúp việc gỡ lỗi trở nên dễ dàng.

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

Kết quả JSON điển hình trông như sau (được rút gọn để ngắn gọn):

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

Bạn có thể đưa JSON này trực tiếp vào một endpoint REST hoặc lưu vào Azure Cosmos DB.

### 5️⃣ Chuyển ảnh sang XML – khi **chuyển ảnh sang xml** là yêu cầu

Một số hệ thống cũ vẫn tiêu thụ XML. Aspose cung cấp `ToXml` để tạo ra một biểu diễn sạch sẽ, tương thích với schema.

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

Đoạn XML mẫu:

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

Cả hai định dạng đều bảo toàn cùng một dữ liệu phân cấp, vì vậy bạn có thể chọn bất kỳ định dạng nào phù hợp với pipeline downstream của mình.

## Những lỗi thường gặp & Cách trích xuất văn bản một cách đáng tin cậy

Ngay cả khi dùng thư viện mạnh mẽ, các ảnh thực tế vẫn có thể gây khó khăn. Dưới đây là ba vấn đề bạn có thể gặp và cách khắc phục tương ứng.

### 📏 Ảnh độ phân giải thấp

**Tại sao quan trọng:** Phông chữ nhỏ bị gộp lại, làm giảm điểm tin cậy.  
**Giải pháp:** Tiền xử lý ảnh—phóng to bằng `Image.Resize` hoặc áp dụng bộ lọc làm nét trước khi truyền vào `Recognize`.

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 Độ tương phản kém

**Tại sao quan trọng:** Văn bản sáng trên nền tối làm rối thuật toán tách ký tự.  
**Giải pháp:** Đảo màu hoặc điều chỉnh độ sáng/độ tương phản qua `Image.AdjustBrightnessContrast`.

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 Tài liệu đa ngôn ngữ

**Tại sao quan trọng:** Mô hình ngôn ngữ mặc định là tiếng Anh; khi có hỗn hợp ngôn ngữ sẽ gây ra kết quả rối.  
**Giải pháp:** Đặt `ocrEngine.Language = OcrLanguage.Multilingual;` trước khi nhận dạng.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

Xử lý những trường hợp này sẽ giúp **cách trích xuất văn bản** từ bất kỳ ảnh nào trở thành một quy trình đáng tin cậy thay vì một trò may rủi.

## Ví dụ hoàn chỉnh (Sẵn sàng sao chép‑dán)

Dưới đây là chương trình đầy đủ, sẵn sàng biên dịch và chạy. Chỉ cần thay `YOUR_DIRECTORY` bằng đường dẫn tới ảnh của bạn và nhấn F5.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**Kết quả console mong đợi** (được định dạng để dễ đọc) hiển thị cả cấu trúc JSON và XML chứa văn bản đã trích xuất và các hộp bao quanh.

## Tóm tắt – Những gì chúng ta đã đề cập

- **cách chạy OCR** với Aspose OCR trong C#
- Quy trình từng bước để **trích xuất văn bản từ ảnh**
- Hai tùy chọn tuần tự hoá: **chuyển ảnh sang json** và **chuyển ảnh sang xml**
- Mẹo xử lý ảnh độ phân giải thấp, độ tương phản thấp và đa ngôn ngữ
- Một mẫu mã hoàn chỉnh, sao chép‑dán, bạn có thể đưa vào bất kỳ dự án .NET nào

## Bước tiếp theo là gì?

Bây giờ bạn đã có thể **cách trích xuất văn bản** và nhận dữ liệu có cấu trúc, hãy cân nhắc các ý tưởng tiếp theo:

- Đưa JSON vào một Azure Function để lưu biên lai trong Cosmos DB.
- Sử dụng đầu ra XML để điền dữ liệu vào hệ thống kế toán dựa trên SOAP hiện có.
- Kết hợp Aspose OCR với mô hình máy học để tự động phân loại loại chi phí.

Hãy thoải mái thử nghiệm—thay `receipt.png` bằng hoá đơn, danh thiếp, hoặc ghi chú viết tay. Mẫu này hoạt động đồng nhất cho

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
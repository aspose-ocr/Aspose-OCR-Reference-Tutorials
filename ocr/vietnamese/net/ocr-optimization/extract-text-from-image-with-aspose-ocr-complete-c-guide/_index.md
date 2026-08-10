---
category: general
date: 2026-04-08
description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR trong C#. Tìm hiểu cách
  tiền xử lý hình ảnh cho OCR và cách tiền xử lý hình ảnh để tăng độ chính xác.
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR trong C#. Hướng dẫn
  này chỉ cách tiền xử lý hình ảnh cho OCR và cách tiền xử lý hình ảnh để đạt kết
  quả tốt nhất.
og_title: Trích xuất văn bản từ hình ảnh bằng Aspose OCR – Hướng dẫn C# đầy đủ
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Trích xuất văn bản từ hình ảnh bằng Aspose OCR – Hướng dẫn C# đầy đủ
url: /vi/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn C# Đầy đủ

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng kết quả lại đầy lỗi? Bạn không phải là người duy nhất—hầu hết các nhà phát triển gặp phải vấn đề này khi ảnh nguồn bị nghiêng, nhiễu hoặc độ tương phản thấp. Tin tốt là một quy trình tiền xử lý ngắn gọn có thể biến một bức ảnh mờ nhạt thành nguồn sạch cho OCR, và Aspose OCR biến mọi thứ trở nên dễ dàng.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ thực tế cho thấy **cách tiền xử lý ảnh cho OCR** bằng các bộ lọc tích hợp của Aspose OCR, sau đó **trích xuất văn bản từ ảnh** chỉ với vài dòng C#. Khi hoàn thành, bạn sẽ có một chương trình sẵn sàng chạy, hiểu tại sao mỗi bộ lọc quan trọng, và biết cách điều chỉnh pipeline cho các trường hợp đặc biệt của mình.

## Những gì bạn cần

- .NET 6.0 trở lên (mã cũng chạy trên .NET Framework 4.7+)
- Gói NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Một ảnh mẫu bị nghiêng, nhiễu hoặc độ tương phản thấp (ví dụ: `skewed_noisy.jpg`)
- Bất kỳ IDE nào bạn thích—Visual Studio, Rider, hoặc VS Code đều được

Không cần thư viện gốc bổ sung, không cần dịch vụ web, chỉ C# thuần.

## Bước 1: Thiết lập Engine OCR – Điểm khởi đầu để Trích xuất Văn bản

Điều đầu tiên cần làm: tạo một thể hiện `OcrEngine` và chỉ định ngôn ngữ cần nhận dạng. Tiếng Anh là phổ biến nhất, nhưng bạn có thể thay `"en"` bằng `"fr"`, `"de"` và các ngôn ngữ khác.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**Tại sao lại quan trọng:** Engine chứa các từ điển nội bộ và heuristics riêng ngôn ngữ. Nếu bỏ qua việc đặt ngôn ngữ, Aspose sẽ mặc định là tiếng Anh, nhưng việc chỉ định rõ ràng giúp tránh bất ngờ khi bạn chuyển sang locale khác.

## Bước 2: Xây dựng Pipeline Tiền xử lý – Cách tiền xử lý ảnh để đạt kết quả tốt nhất

Bây giờ chúng ta thêm các bộ lọc. Hãy nghĩ chúng như một bộ công cụ chỉnh sửa ảnh mini chạy tự động trước bước OCR. Ba bộ lọc dưới đây bao phủ các vấn đề phổ biến nhất:

| Bộ lọc | Những gì nó sửa | Khi nào nên dùng |
|--------|----------------|-------------------|
| `DeskewFilter` | Xoay ảnh trở lại chiều ngang | Ảnh chụp góc nghiêng |
| `DenoiseFilter` | Giảm các đốm nhiễu và hạt | Ảnh chụp trong điều kiện ánh sáng yếu hoặc tài liệu quét |
| `ContrastStretchFilter` | Tăng độ tương phản, làm cho văn bản tối nổi bật | Bản in mờ hoặc ảnh chụp màn hình bị phai màu |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**Mẹo chuyên nghiệp:** Thứ tự quan trọng. Đầu tiên Deskew, rồi Denoise, cuối cùng là ContrastStretch. Nếu đảo ngược, bạn có thể làm tăng nhiễu thay vì loại bỏ.

## Bước 3: Chạy OCR – Cuối cùng là Trích xuất Văn bản từ Ảnh

Khi pipeline đã sẵn sàng, truyền đường dẫn ảnh cho engine. Aspose sẽ tự động áp dụng các bộ lọc, sau đó chạy thuật toán nhận dạng.

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Nếu không tìm thấy tệp, bạn sẽ nhận được `FileNotFoundException` rõ ràng. Đó là lý do chúng tôi khuyên dùng đường dẫn tuyệt đối trong quá trình phát triển, sau đó chuyển sang đường dẫn tương đối hoặc giá trị cấu hình cho môi trường production.

## Bước 4: Hiển thị Kết quả – Xem những gì bạn nhận được

Đối tượng `OcrResult` chứa văn bản thô, điểm tin cậy, và thậm chí các bounding box của từng từ. Để demo nhanh, chúng ta chỉ in văn bản ra console.

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Khi chạy chương trình, bạn sẽ thấy đầu ra giống như:

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

Nếu kết quả bị rối, hãy kiểm tra lại chất lượng ảnh hoặc thử thêm các bộ lọc khác (ví dụ: `BinarizationFilter` cho ảnh nhị phân).

## Ví dụ Hoàn chỉnh – Sao chép‑Dán và Chạy

Dưới đây là chương trình đầy đủ, tự chứa. Chỉ cần thay `YOUR_DIRECTORY/skewed_noisy.jpg` bằng đường dẫn thực tế tới ảnh thử nghiệm của bạn.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Kết quả mong đợi** – Console sẽ in ra dạng văn bản thuần của nội dung trong ảnh. Nếu ảnh chứa một biển hiệu đơn giản ghi “OpenAI”, bạn sẽ thấy đúng từ đó, không có ký tự thừa.

## Các Trường hợp Đặc biệt & Cách Điều chỉnh Pipeline

### 1️⃣ Ảnh Rất Tối

Nếu bộ lọc độ tương phản không đủ, hãy thêm trước một `BrightnessCorrectionFilter`:

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ Tài liệu Đa Ngôn ngữ

Đặt `Language = "en+fr"` (Aspose hỗ trợ các mã ngôn ngữ ngăn cách bằng dấu phẩy) và thêm `LanguageDetectionFilter` nếu muốn engine tự động phát hiện ngôn ngữ.

### 3️⃣ PDF lớn Được Chuyển thành Ảnh

Xử lý một PDF hàng nghìn trang từng ảnh một có thể chậm. Sử dụng `Parallel.ForEach` để chạy OCR trên nhiều ảnh đồng thời, nhưng nhớ rằng `OcrEngine` không thread‑safe—tạo một thể hiện riêng cho mỗi luồng.

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ Lấy Bounding Boxes

Nếu bạn cần vị trí của từng từ (ví dụ: để highlight), hãy kiểm tra `ocrResult.Regions`. Mỗi region chứa tọa độ `Rectangle` mà bạn có thể dùng để vẽ lên giao diện UI.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## Những Sai lầm Thường gặp (Và Cách Tránh)

- **Bỏ qua bước Deskew** – Ngay cả góc nghiêng 2 độ cũng có thể làm giảm điểm tin cậy tới 20 %. Luôn thêm `DeskewFilter` khi nguồn không được căn chỉnh hoàn hảo.
- **Sử dụng JPEG với nén mạnh** – Các artefact nén giống như nhiễu; chuyển sang PNG hoặc TIFF để OCR tốt hơn.
- **Hard‑code đường dẫn** – Đường dẫn tương đối hoạt động cục bộ, nhưng trong pipeline CI/CD bạn nên đọc vị trí ảnh từ cấu hình hoặc biến môi trường.

## Kiểm tra Cấu hình của Bạn

1. Chạy chương trình với ảnh sạch, độ tương phản cao. Bạn nên nhận được văn bản gần như hoàn hảo.
2. Thay bằng ảnh nhiễu, nghiêng. Xác nhận rằng đầu ra được cải thiện sau khi thêm ba bộ lọc.
3. Thử loại bỏ từng bộ lọc một để thấy tác động của chúng—điều này giúp bạn hiểu *tại sao* mỗi bước quan trọng.

## Kết luận

Chúng ta vừa minh họa cách **trích xuất văn bản từ ảnh** bằng Aspose OCR, và đã chỉ ra một cách thực tế để **tiền xử lý ảnh cho OCR** hoạt động trong hầu hết các tình huống thực tế. Bằng cách nối chuỗi `DeskewFilter`, `DenoiseFilter`, và `ContrastStretchFilter` bạn cung cấp cho engine một “canvas” sạch, giúp độ chính xác tăng đáng kể.

Từ đây, bạn có thể khám phá các bộ lọc nâng cao hơn, xử lý tài liệu đa trang, hoặc tích hợp kết quả OCR vào chỉ mục tìm kiếm. Dù bạn chọn gì, mẫu pattern cốt lõi—khởi tạo, tiền xử lý, nhận dạng, và tiêu thụ—vẫn giữ nguyên.

Sẵn sàng nâng cấp? Hãy thử thêm `BinarizationFilter` cho các bản quét đen‑trắng, hoặc đưa kết quả vào cơ sở dữ liệu để tạo PDF có thể tìm kiếm. Chúc lập trình vui vẻ, và mong mọi ảnh bạn đưa vào Aspose đều trả về văn bản rõ ràng, dễ đọc!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-26
description: Nhận dạng văn bản từ file png và trích xuất dữ liệu biên lai bằng Aspose
  OCR trong C#. Chuyển đổi hình ảnh sang JSON‑L và xử lý biên lai bằng OCR trong một
  ví dụ hoàn chỉnh.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: vi
og_description: Nhận dạng văn bản từ PNG và chuyển biên lai thành JSON‑L với Aspose
  OCR trong C#. Mã đầy đủ từng bước và các mẹo.
og_title: Nhận dạng văn bản từ PNG – Hướng dẫn Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: Nhận dạng văn bản từ PNG – Hướng dẫn Aspose OCR C# JSON‑L
url: /vi/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhận dạng văn bản từ png – Hướng dẫn đầy đủ Aspose OCR C#  

Bạn đã bao giờ cần **nhận dạng văn bản từ png** nhưng không chắc thư viện nào sẽ cho kết quả sạch sẽ, từng dòng một? Bạn không phải là người duy nhất. Trong nhiều ứng dụng doanh nghiệp nhỏ, biên lai được lưu dưới dạng ảnh PNG, và việc trích xuất số tiền, ngày tháng hoặc tên cửa hàng là một vấn đề hàng ngày.  

Tin tốt là gì? Chỉ với vài dòng C# và thư viện **Aspose OCR** bạn có thể **trích xuất văn bản từ biên lai**, sau đó **chuyển đổi ảnh sang jsonl** để phân tích downstream. Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ pipeline — tải PNG, chạy OCR, và ghi mỗi dòng vào file JSON‑L — để bạn có thể **xử lý biên lai với OCR** ngay lập tức.

Chúng ta sẽ bao phủ mọi thứ bạn cần: các gói NuGet bắt buộc, một chương trình có thể chạy được đầy đủ, giải thích lý do mỗi bước quan trọng, và một vài mẹo thực tiễn bạn sẽ đánh giá cao khi biên lai trở nên lộn xộn. Không cần tài liệu bên ngoài; chỉ cần sao chép‑dán, chạy và tùy chỉnh.

---

## Những gì bạn sẽ học

- Cách **nhận dạng văn bản từ png** bằng `Aspose.OCR`.  
- Cách **trích xuất văn bản từ biên lai** dưới dạng các đối tượng dòng và lấy điểm confidence.  
- Cách **chuyển đổi ảnh sang jsonl** để mỗi dòng OCR trở thành một đối tượng JSON riêng.  
- Cách **xử lý biên lai với OCR** end‑to‑end, xử lý các trường hợp đặc biệt như ảnh trống hoặc dòng có confidence thấp.  
- Các mẹo khắc phục lỗi OCR thường gặp và cải thiện độ chính xác.

### Yêu cầu trước

- .NET 6.0 trở lên (mã cũng chạy được với .NET Core và .NET Framework).  
- Visual Studio 2022 hoặc bất kỳ IDE nào bạn thích.  
- Giấy phép Aspose OCR hợp lệ (bạn có thể bắt đầu với giấy phép tạm thời miễn phí từ Aspose.com).  
- Một mẫu biên lai lưu dưới tên `receipt.png` trong thư mục bạn kiểm soát.

---

## Bước 1: Nhận dạng văn bản từ png với Aspose OCR

Điều đầu tiên chúng ta cần là một `OcrEngine` đã được khởi tạo. Đối tượng này chứa các cài đặt của engine OCR (ngôn ngữ, chế độ phát hiện, v.v.). Mặc định nó sử dụng tiếng Anh và tự động phát hiện bố cục trang, đủ cho hầu hết các biên lai.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Tại sao điều này quan trọng:**  
`OcrEngine` là thành phần nặng; tạo một lần và tái sử dụng cho nhiều ảnh sẽ giảm tải bộ nhớ. Nếu bạn cần ngôn ngữ khác (ví dụ biên lai tiếng Tây Ban Nha), bạn có thể đặt `ocrEngine.Language = OcrLanguage.Spanish;` trước khi gọi `Recognize`.

---

## Bước 2: Trích xuất văn bản từ các dòng biên lai

`OcrResult` chứa một collection tên là `Lines`. Mỗi dòng giữ nguyên văn bản thô và một điểm confidence (0‑100). Lấy chúng ra cho phép bạn kiểm soát chi tiết — có thể loại bỏ các dòng confidence thấp hoặc đánh dấu chúng để kiểm tra thủ công.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Tại sao chúng ta phải escape JSON:**  
Văn bản biên lai có thể chứa dấu ngoặc kép (`"`) hoặc dấu gạch chéo ngược (`\`) sẽ làm hỏng một chuỗi JSON đơn giản. Phương thức `EscapeJson` đảm bảo mỗi dòng JSON hợp lệ.

**Kết quả đầu ra trông như thế nào:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Mỗi dòng là một bản ghi riêng, hoàn hảo để stream vào data lake hoặc đưa vào mô hình machine‑learning.

---

## Bước 3: Chuyển đổi ảnh sang JSONL – xử lý các trường hợp đặc biệt

Khi bạn xử lý một loạt biên lai, một vài ảnh có thể bị trắng, hỏng, hoặc có điểm confidence cực thấp. Hãy làm cho pipeline vững chắc hơn một chút.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Tại sao cần lọc:**  
Biên lai in trên giấy mờ có thể tạo ra các ký tự lẻ loi với confidence thấp. Loại bỏ mọi thứ dưới 80 % thường loại bỏ nhiễu trong khi vẫn giữ dữ liệu hữu ích.

---

## Bước 4: Xử lý biên lai với OCR – ví dụ end‑to‑end

Kết hợp tất cả lại, đây là chương trình **đầy đủ, sẵn sàng chạy**. Thay `YOUR_DIRECTORY` bằng thư mục chứa file PNG của bạn.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Chạy mã:**  
1. Mở terminal trong thư mục dự án.  
2. `dotnet add package Aspose.OCR` – cài đặt thư viện.  
3. `dotnet run` – bạn sẽ thấy thông báo thành công và một file `receipt.jsonl` xuất hiện.

**Kết quả mong đợi:** Một file JSON dạng dòng, mỗi dòng phản ánh một dòng biên lai, kèm theo điểm confidence. Bạn có thể truyền file này vào Power BI, Elastic, hoặc bất kỳ công cụ phân tích nào hỗ trợ JSON‑L.

---

## Những lỗi thường gặp & Mẹo chuyên nghiệp

| Vấn đề | Nguyên nhân | Giải pháp nhanh |
|-------|------------|-----------------|
| **Kết quả trống** | Đường dẫn ảnh sai hoặc file không phải PNG. | Kiểm tra lại đường dẫn, dùng `File.Exists(imagePath)`. |
| **Ký tự rác** | DPI thấp hoặc PNG bị nén mạnh. | Sử dụng bản scan ít nhất 300 dpi; tránh nén JPEG quá mức. |
| **Quá nhiều dòng confidence thấp** | Biên lai in trên giấy nhiệt đã phai. | Tăng ngưỡng `minConfidence` hoặc tiền xử lý ảnh (tăng độ tương phản/threshold). |
| **Lỗi phân tích JSON** | Dấu ngoặc kép chưa được escape trong văn bản biên lai. | Giữ helper `EscapeJson` hoặc chuyển sang `System.Text.Json` để serialize mạnh mẽ hơn. |

**Mẹo pro:** Nếu bạn cần trích xuất các trường cụ thể (ví dụ tổng tiền), chạy một regex đơn giản trên mỗi `line.Text` sau khi đã có file JSON‑L. Điều này tách biệt OCR khỏi logic nghiệp vụ và giúp debug dễ dàng hơn.

---

## Mở rộng giải pháp

- **Xử lý batch:** Đặt logic `Main` trong một vòng `foreach` duyệt tất cả file PNG trong một thư mục.  
- **Hỗ trợ đa ngôn ngữ:** Đặt `ocrEngine.Language = OcrLanguage.Spanish;` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ) trước `Recognize`.  
- **Đầu ra có cấu trúc:** Thay vì JSON từng dòng, xây dựng một đối tượng `Receipt` với các thuộc tính `Date`, `Merchant`, `Total`, rồi serialize một lần.

Tất cả các biến thể này vẫn **chuyển đổi ảnh sang jsonl** ở lõi, vì vậy bạn có thể thay đổi consumer downstream mà không cần chạm vào phần OCR.

---

## Kết luận

Chúng ta vừa trình bày cách **nhận dạng văn bản từ png** bằng Aspose OCR, **trích xuất văn bản từ biên lai**, và **chuyển đổi ảnh sang jsonl** để xử lý downstream dễ dàng. Chương trình C# tự chứa đầy đủ quy trình — từ tải PNG, xử lý các trường hợp đặc biệt, tới ghi file JSON‑L sạch sẽ — giúp bạn ngay lập tức **xử lý biên lai với OCR** trong dự án của mình.

Hãy thử với một vài biên lai mẫu, điều chỉnh ngưỡng confidence, và bạn sẽ thấy một đống ảnh nhiễu nhanh chóng biến thành dữ liệu có cấu trúc, sẵn sàng cho phân tích. Khi đã quen, khám phá xử lý batch hoặc thêm một mô hình ML nhỏ để tự động phân loại danh mục chi phí.

Có câu hỏi, hoặc tìm ra cách tối ưu thú vị? Để lại bình luận bên dưới — chúc lập trình vui!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
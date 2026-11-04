---
category: general
date: 2026-04-11
description: Tìm hiểu cách tắt OCR trong Aspose OCR cho C# để chạy offline, trích
  xuất văn bản từ hình ảnh mà không cần internet và tải hình ảnh đúng cách cho OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: vi
og_description: Cách tắt OCR trong Aspose OCR cho C# và chạy offline, trích xuất văn
  bản từ hình ảnh mà không cần internet, và tải hình ảnh cho OCR một cách dễ dàng.
og_title: Cách vô hiệu hoá OCR trong C# – Hướng dẫn OCR offline của Aspose
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Cách tắt OCR trong C# – Hướng dẫn OCR Offline của Aspose
url: /vi/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Vô Hiệu Hóa OCR trong C# – Hướng Dẫn Aspose OCR Offline

Bạn đã bao giờ tự hỏi **cách vô hiệu hóa OCR** khi cần một giải pháp thực sự offline chưa? Có thể bạn đang xây dựng một ứng dụng desktop bảo mật không thể dựa vào kết nối mạng, hoặc bạn chỉ muốn tránh các tải xuống không mong muốn. Dù sao, tin tốt là Aspose OCR cho phép bạn tắt việc tự động tải tài nguyên, chỉ định một thư mục cục bộ, và giữ mọi thứ trên‑premises. Trong tutorial này, bạn cũng sẽ thấy cách **trích xuất văn bản từ hình ảnh** và **tải hình ảnh cho OCR** một cách chính xác mà không gặp trục trặc.

Chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, thể hiện mọi bước—từ khởi tạo engine đến in ra văn bản tiếng Nhật đã nhận dạng. Không có tài liệu bên ngoài, không có phép màu ẩn; chỉ có mã C# thuần túy mà bạn có thể đưa vào dự án ngay hôm nay. Khi hoàn thành, bạn sẽ hiểu tại sao việc tắt tính năng tự động tải xuống quan trọng, cách đặt đường dẫn tài nguyên, và những cạm bẫy cần tránh.

## Yêu cầu trước

- .NET 6.0 (hoặc bất kỳ phiên bản .NET gần đây nào) đã được cài đặt trên máy của bạn.  
- Gói NuGet Aspose.OCR for .NET (`Install-Package Aspose.OCR`).  
- Một thư mục đã chứa các tài nguyên ngôn ngữ bạn cần (ví dụ: mô hình tiếng Nhật).  
- Một tệp hình ảnh (`japan_doc.png`) mà bạn muốn chạy OCR.

Nếu bạn chưa có các gói ngôn ngữ, hãy tải chúng từ cổng thông tin Aspose một lần, giải nén vào thư mục như `AsposeOCRResources`, và bạn đã sẵn sàng. Không có tải xuống nào khác sẽ xảy ra sau khi bạn đã tắt tính năng tự động tải xuống.

![Cách vô hiệu hóa OCR offline](/images/how-to-disable-ocr.png "hình minh họa cách vô hiệu hóa OCR")

## Bước 1 – Tạo Instance của OCR Engine  

Điều đầu tiên bạn làm là khởi tạo `OcrEngine`. Hãy nghĩ đối tượng này như bộ não sẽ đọc hình ảnh của bạn.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Tại sao điều này quan trọng:** Không có engine, bạn không thể cấu hình bất cứ thứ gì. Đối tượng chứa tất cả các cài đặt, bao gồm cả cờ quan trọng cho biết thư viện có được phép truy cập internet hay không.

## Bước 2 – Vô Hiệu Hóa Tự Động Tải Tài Nguyên  

Mặc định, Aspose OCR sẽ cố gắng tải các tệp ngôn ngữ còn thiếu ngay lập tức. Để giữ mọi thứ offline, chuyển công tắc `AutoDownloadResources` thành `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Mẹo chuyên nghiệp:** Tắt tính năng này không chỉ bảo đảm tính riêng tư mà còn tăng tốc lần nhận dạng đầu tiên vì engine sẽ không lãng phí thời gian kiểm tra cập nhật.

## Bước 3 – Chỉ Định Thư Mục Tài Nguyên Cục Bộ  

Bây giờ hãy cho engine biết nơi lưu các gói ngôn ngữ đã tải trước. Đây là đường dẫn bạn đã thiết lập trong phần yêu cầu trước.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Có thể xảy ra lỗi gì?** Nếu đường dẫn sai hoặc tệp ngôn ngữ cần thiết thiếu, engine sẽ ném ra `ResourceNotFoundException`. Hãy kiểm tra lại chính tả thư mục và chắc chắn mô hình tiếng Nhật (`jpn.traineddata`) có trong đó.

## Bước 4 – Chọn Mô Hình Ngôn Ngữ Cục Bộ  

Chọn ngôn ngữ mà bạn thực sự có trên đĩa. Trong ví dụ của chúng ta, chúng ta dùng tiếng Nhật, nhưng bạn có thể thay `Language.Japanese` bằng bất kỳ ngôn ngữ nào khác mà bạn đã tải về.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Trường hợp đặc biệt:** Một số ngôn ngữ yêu cầu từ điển bổ sung (ví dụ: tiếng Trung). Đảm bảo các tệp phụ trợ cũng nằm trong cùng thư mục tài nguyên.

## Bước 5 – Tải Hình Ảnh cho OCR  

Đây là nơi chúng ta **tải hình ảnh cho OCR**. Phương thức `ImageStream.FromFile` đọc tệp vào một stream mà Aspose có thể xử lý.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Mẹo:** Các định dạng được hỗ trợ bao gồm PNG, JPEG, BMP và TIFF. Nếu bạn cần xử lý PDF, hãy chuyển mỗi trang thành hình ảnh trước.

## Bước 6 – Thực Hiện Quá Trình Nhận Dạng  

Bây giờ engine thực sự đọc các pixel và cố gắng chuyển chúng thành văn bản.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Tại sao bước này có thể chậm:** OCR tiêu tốn nhiều CPU, đặc biệt với hình ảnh độ phân giải cao. Nếu hiệu năng là mối quan tâm, hãy cân nhắc giảm kích thước hình ảnh trước khi nhận dạng.

## Bước 7 – Xuất Văn Bản Đã Trích Xuất  

Cuối cùng, chúng ta **trích xuất văn bản từ hình ảnh** và in ra console.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Chạy chương trình sẽ hiển thị các ký tự tiếng Nhật có trong `japan_doc.png`. Nếu mọi thứ được cấu hình đúng, bạn sẽ thấy một khối văn bản Unicode sạch sẽ trên console.

### Kết Quả Dự Kiến

```
これはサンプルの日本語テキストです。
```

(Kết quả thực tế của bạn sẽ phụ thuộc vào nội dung của hình ảnh.)

## Các Cạm Bẫy Thường Gặp & Cách Tránh  

| Vấn đề | Nguyên nhân | Giải pháp |
|--------|-------------|-----------|
| **Thiếu tệp ngôn ngữ** | `AutoDownloadResources` bị đặt `false`, nên engine không thể tải nó. | Kiểm tra `ResourcesPath` trỏ đúng tới thư mục chứa `jpn.traineddata`. |
| **Đường dẫn hình ảnh sai** | `ImageStream.FromFile` ném `FileNotFoundException`. | Sử dụng đường dẫn tuyệt đối hoặc đảm bảo thư mục làm việc được đặt đúng. |
| **Định dạng hình ảnh không được hỗ trợ** | Aspose chỉ đọc một số định dạng nhất định. | Chuyển đổi hình ảnh sang PNG hoặc JPEG trước khi gọi `FromFile`. |
| **Hết bộ nhớ khi xử lý hình ảnh lớn** | OCR tải toàn bộ hình ảnh vào bộ nhớ. | Thu nhỏ hoặc chia hình ảnh thành các khối, hoặc tăng giới hạn bộ nhớ cho tiến trình. |

## Mở Rộng Ví Dụ  

- **Xử lý hàng loạt:** Lặp qua một thư mục chứa nhiều hình ảnh, gọi cùng một đoạn mã nhận dạng, và ghi mỗi kết quả vào một tệp `.txt` riêng.  
- **Ngôn ngữ khác:** Thay `Language.Japanese` bằng `Language.English` (hoặc bất kỳ ngôn ngữ nào khác) sau khi đặt các tệp tài nguyên tương ứng.  
- **Tiền xử lý tùy chỉnh:** Sử dụng Aspose.Imaging để chỉnh sửa độ nghiêng hoặc tăng độ tương phản trước OCR nhằm cải thiện độ chính xác.

## Kết Luận  

Bây giờ bạn đã biết **cách vô hiệu hóa OCR** trong Aspose OCR cho C# và chạy hoàn toàn offline. Bằng cách đặt `AutoDownloadResources` thành `false`, chỉ định engine tới thư mục tài nguyên cục bộ, và **tải hình ảnh cho OCR** đúng cách, bạn có thể **trích xuất văn bản từ hình ảnh** mà không cần kết nối internet. Cách tiếp cận này lý tưởng cho môi trường bảo mật, pipeline CI, hoặc bất kỳ kịch bản nào mà truy cập mạng bị hạn chế.

Sẵn sàng cho bước tiếp theo? Hãy thử xử lý toàn bộ thư mục các PDF đã quét, thử nghiệm với các gói ngôn ngữ khác nhau, hoặc tích hợp kết quả OCR vào cơ sở dữ liệu có khả năng tìm kiếm. Cấu hình offline bạn vừa xây dựng hôm nay là nền tảng vững chắc cho bất kỳ quy trình xử lý tài liệu on‑premises nào.

Chúc lập trình vui vẻ, và đừng ngại để lại bình luận nếu gặp khó khăn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
date: 2026-07-23
description: Tìm hiểu cách trích xuất văn bản từ hình ảnh bằng Aspose.OCR for .NET,
  chuẩn bị các hình chữ nhật để cải thiện độ chính xác của OCR và chuyển đổi hình
  ảnh sang văn bản một cách hiệu quả.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: Chuẩn bị Các Hình chữ nhật trong Nhận dạng Hình ảnh OCR
og_description: Trích xuất văn bản từ hình ảnh bằng Aspose.OCR for .NET. Tìm hiểu
  cách chuẩn bị các hình chữ nhật, nâng cao độ chính xác của OCR, và chuyển đổi hình
  ảnh sang văn bản một cách hiệu quả.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: Trích xuất Văn bản từ Hình ảnh với Các Hình chữ nhật – OCR Guide
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: Trích xuất Văn bản từ Hình ảnh với Các Hình chữ nhật – OCR Guide
url: /vi/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh với Các Hình chữ nhật – Hướng dẫn OCR

## Giới thiệu

Optical Character Recognition (OCR) cho phép bạn **trích xuất văn bản từ hình ảnh** để chúng có thể tìm kiếm và chỉnh sửa. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách nâng cao độ chính xác của OCR bằng cách chuẩn bị các hình chữ nhật tùy chỉnh để tập trung engine vào các vùng chính xác mà bạn cần. Sử dụng Aspose.OCR cho .NET, bạn sẽ thấy toàn bộ quy trình — từ thiết lập dự án đến việc lấy các chuỗi đã nhận dạng — để bạn có thể nhúng chuyển đổi hình ảnh‑thành‑văn bản đáng tin cậy vào bất kỳ ứng dụng .NET nào.

## Câu trả lời nhanh
- **Ý nghĩa của “extract text from image” là gì?** Nó chuyển các ký tự hình ảnh trong một bức ảnh thành các chuỗi có thể đọc được bởi máy.  
- **Thư viện nào xử lý việc này trong .NET?** Aspose.OCR cho .NET cung cấp một engine OCR đầy đủ tính năng.  
- **Tôi có cần giấy phép cho môi trường sản xuất không?** Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép thương mại là bắt buộc cho triển khai.  
- **Tôi có thể giới hạn OCR chỉ trong các vùng cụ thể không?** Có — định nghĩa các hình chữ nhật để nhắm mục tiêu chỉ các khu vực chứa văn bản hữu ích.  
- **Các phiên bản .NET nào được hỗ trợ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## “extract text from image” với hình chữ nhật là gì?
Quá trình `extract text from image` đọc các ký tự bên trong các vùng hình chữ nhật đã định nghĩa, bỏ qua mọi thứ khác. Bằng cách giới hạn OCR trong các vùng đó, bạn sẽ đạt độ chính xác cao hơn, xử lý nhanh hơn và giảm công sức hậu xử lý. Cách tiếp cận này tách riêng văn bản bạn quan tâm trong khi loại bỏ đồ họa nền, các yếu tố trang trí và các nhiễu hình ảnh khác có thể làm rối engine OCR.

## Tại sao cần chuẩn bị các hình chữ nhật trước OCR?
Việc chuẩn bị các hình chữ nhật cho phép bạn tập trung engine OCR vào những phần quan trọng nhất của hình ảnh, cải thiện cả tốc độ và độ chính xác. Bằng cách thu hẹp khu vực phân tích, bạn giảm lượng dữ liệu mà engine phải xem xét, dẫn đến kết quả nhanh hơn và ít lỗi nhận dạng do nhiễu hình ảnh không cần thiết.

- **Tập trung vào nội dung liên quan:** Bỏ qua tiêu đề, chân trang hoặc đồ họa trang trí có thể làm rối engine.  
- **Tăng hiệu suất:** Các vùng nhỏ hơn yêu cầu ít phép tính hơn, giảm thời gian chạy lên tới 40 % trên các bản quét lớn.  
- **Cải thiện độ chính xác:** Giảm nhiễu hình ảnh làm tăng tỷ lệ nhận dạng ký tự từ ~85 % lên >95 % trên các tài liệu có nhiễu.

## Tại sao điều này quan trọng đối với các dự án thực tế
Nhiều tài liệu kinh doanh — biên lai, hoá đơn, thẻ ID — kết hợp văn bản với logo hoặc mã vạch. Bằng cách vẽ các hình chữ nhật quanh các trường bạn thực sự cần, bạn chỉ trích xuất dữ liệu có giá trị, giảm đáng kể công việc làm sạch sau này và nâng độ tin cậy của quy trình tự động. Việc trích xuất có mục tiêu này giảm công sức hậu xử lý và giúp duy trì tuân thủ các tiêu chuẩn xử lý dữ liệu.

## Các trường hợp sử dụng phổ biến
- **Tự động nhập dữ liệu:** Lấy các trường cụ thể từ biểu mẫu quét hoặc biên lai chi phí.  
- **Kiểm tra tuân thủ:** Tách riêng các điều khoản pháp lý hoặc tuyên bố quy định để xác minh.  
- **Lập chỉ mục nội dung:** Lập chỉ mục chỉ tiêu đề hoặc chú thích của hình ảnh để tăng khả năng hiển thị trên công cụ tìm kiếm.

## Yêu cầu trước

- Kiến thức cơ bản về C# và phát triển .NET.  
- Thư viện Aspose.OCR cho .NET đã được cài đặt – tải xuống **[here](https://releases.aspose.com/ocr/net/)** hoặc duyệt tất cả các bản phát hành **[here](https://releases.aspose.com/)**.  
- Một hình ảnh mẫu (ví dụ, `sample.png`) chứa văn bản bạn muốn trích xuất.

## Nhập không gian tên

Các câu lệnh `using` đưa engine OCR và các lớp hình học vào phạm vi.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Bước 1: Thiết lập Thư mục Tài liệu của Bạn

Xác định thư mục chứa hình ảnh của bạn và tạo một thể hiện của engine OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Cách trích xuất văn bản từ hình ảnh bằng nhiều hình chữ nhật
Tải hình ảnh một lần, sau đó cung cấp danh sách các hình chữ nhật cho engine OCR. Mỗi hình chữ nhật xác định một vùng quan tâm, và engine trả về một chuỗi riêng cho mỗi vùng, cho phép bạn xử lý các trường riêng lẻ và kết hợp kết quả khi cần.

### Định nghĩa các hình chữ nhật
`Rectangle` objects describe the X‑Y coordinates and size of each zone you want to scan.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### Thực hiện nhận dạng OCR
The `RecognizeImage` method processes the image using the supplied rectangle list and returns recognized text for each region.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Cách trích xuất văn bản từ hình ảnh bằng RecognitionSettings (Cách tiếp cận thay thế)
Nếu bạn thích gọi dựa trên cài đặt, bạn có thể đạt được kết quả tương tự với `RecognitionSettings`. Đối tượng này cho phép bạn gộp các định nghĩa hình chữ nhật cùng với ngôn ngữ, DPI và các tùy chọn OCR khác, cung cấp một lời gọi API sạch sẽ, chỉ với một tham số.

### Định nghĩa cài đặt nhận dạng
`RecognitionSettings` lets you bundle the rectangle list and additional options (e.g., language, DPI) into a single object.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### Hiển thị văn bản đã nhận dạng
Iterate over the returned strings and output each region’s text.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Các vấn đề thường gặp & Mẹo

- **Tọa độ hình chữ nhật không đúng:** Xác minh rằng `X`, `Y`, `Width`, và `Height` khớp với khu vực mong muốn.  
- **Chất lượng hình ảnh:** Hình ảnh độ phân giải thấp hoặc nén mạnh làm giảm kết quả OCR; cân nhắc tiền xử lý như nhị phân hoá.  
- **Kết quả rỗng:** Đảm bảo các hình chữ nhật thực sự chứa văn bản có thể đọc được; nếu không engine sẽ trả về chuỗi rỗng.

## Khắc phục sự cố và Thực hành tốt nhất

| Triệu chứng | Nguyên nhân khả dĩ | Cách khắc phục |
|------------|---------------------|----------------|
| Không có đầu ra hoặc chuỗi rỗng | Hình chữ nhật nằm ngoài giới hạn hình ảnh | Kiểm tra lại kích thước hình ảnh và tọa độ hình chữ nhật |
| Ký tự bị rối | Độ tương phản kém hoặc nhiễu | Áp dụng chuyển đổi grayscale và ngưỡng trước OCR |
| Hiệu suất chậm trên tệp lớn | Quá nhiều hình chữ nhật hoặc hình ảnh quá lớn | Chia hình ảnh hoặc giảm số lượng hình chữ nhật khi có thể |

## Kết luận

Bây giờ bạn đã biết cách **trích xuất văn bản từ hình ảnh** bằng cách chuẩn bị các hình chữ nhật tùy chỉnh với Aspose.OCR cho .NET. Cách tiếp cận này cho phép bạn kiểm soát chính xác quá trình OCR, cung cấp các tính năng trích xuất văn bản nhanh hơn, chính xác hơn cho bất kỳ giải pháp .NET nào.

## Câu hỏi thường gặp

**Q:** Tôi có thể sử dụng Aspose.OCR cho .NET với các framework .NET khác không?  
**A:** Có, Aspose.OCR cho .NET hoạt động với .NET Framework 4.5+, .NET Core 3.1+, và .NET 5/6/7.

**Q:** Có bản dùng thử miễn phí không?  
**A:** Chắc chắn! Tải bản dùng thử **[here](https://releases.aspose.com/)**.

**Q:** Tôi có thể nhận hỗ trợ cho Aspose.OCR cho .NET ở đâu?  
**A:** Truy cập **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** để được hỗ trợ chuyên biệt.

**Q:** Tôi có thể nhận giấy phép tạm thời để thử nghiệm không?  
**A:** Có, giấy phép tạm thời có sẵn **[here](https://purchase.aspose.com/temporary-license/)**.

**Q:** Tài liệu chính thức ở đâu?  
**A:** Tham chiếu API đầy đủ nằm **[here](https://reference.aspose.com/ocr/net/)**.

---

**Cập nhật lần cuối:** 2026-07-23  
**Đã kiểm tra với:** Aspose.OCR 24.11 for .NET  
**Tác giả:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Hướng dẫn liên quan

- [Cách trích xuất hình chữ nhật cho đoạn văn trong nhận dạng hình ảnh OCR](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [Cách OCR hình ảnh – Thực hiện OCR trên hình ảnh trong nhận dạng hình ảnh OCR](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Cách trích xuất văn bản từ hình ảnh bằng Aspose.OCR cho .NET](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
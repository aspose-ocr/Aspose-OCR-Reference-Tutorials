---
date: 2025-12-27
description: Khám phá hỗ trợ ngôn ngữ OCR nâng cao và các tính năng với Aspose.OCR
  cho .NET. Hiệu quả, chính xác và thân thiện với nhà phát triển.
linktitle: OCR Language Support – Ignored Characters in Image Recognition
second_title: Aspose.OCR .NET API
title: Hỗ trợ ngôn ngữ OCR – Các ký tự bị bỏ qua trong nhận dạng hình ảnh
url: /vi/net/ocr-settings/specify-ignored-characters/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hỗ trợ Ngôn ngữ OCR: Chỉ định Các ký tự Bị Bỏ qua trong Nhận dạng Hình ảnh

## Giới thiệu

Hỗ trợ ngôn ngữ OCR là nền tảng của tự động hoá tài liệu hiện đại, cho phép các ứng dụng đọc văn bản từ hình ảnh trên nhiều bảng chữ cái và ký hiệu. Trong hướng dẫn này, bạn sẽ học cách chỉ cho **Aspose.OCR for .NET** bỏ qua các ký tự cụ thể trong quá trình nhận dạng — một thủ thuật quan trọng khi bạn cần kết quả sạch hơn hoặc muốn lọc bỏ nhiễu như số trang hoặc ký hiệu trang trí. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng chạy thể hiện tính năng này từ đầu đến cuối.

## Câu trả lời nhanh
- **“Ignored characters” có nghĩa là gì?** Các ký tự mà engine OCR bỏ qua khi xây dựng chuỗi kết quả.  
- **Tại sao lại sử dụng?** Cải thiện độ chính xác khi một số ký tự không liên quan đến logic kinh doanh của bạn.  
- **Phương thức API nào xử lý?** `RecognitionSettings.IgnoredCharacters`.  
- **Có thể kết hợp với các gói ngôn ngữ không?** Có — các ký tự bị bỏ qua hoạt động cùng với bất kỳ ngôn ngữ nào bạn tải.  
- **Cần giấy phép không?** Cần một giấy phép tạm thời hoặc đầy đủ cho việc sử dụng trong môi trường sản xuất.

## Yêu cầu trước

Trước khi khám phá các chức năng phong phú do Aspose.OCR for .NET cung cấp, hãy đảm bảo bạn đã chuẩn bị các yêu cầu sau:

1. **Cài đặt Aspose.OCR**  

   Đảm bảo rằng bạn đã cài đặt thành công Aspose.OCR cho .NET. Bạn có thể tìm các tệp cần thiết trên [trang tải xuống](https://releases.aspose.com/ocr/net/).

2. **Thiết lập Thư mục Tài liệu**  

   Tạo một thư mục riêng cho tài liệu của bạn. Điều này sẽ rất quan trọng để chạy các ví dụ một cách liền mạch. Cập nhật biến `dataDir` trong các ví dụ với đường dẫn tới thư mục tài liệu của bạn.

3. **Giấy phép tạm thời (Tùy chọn)**  

   Nếu bạn đang khám phá Aspose.OCR cho .NET với giấy phép tạm thời, hãy lấy nó từ [đây](https://purchase.aspose.com/temporary-license/).

## Nhập không gian tên

Để bắt đầu hành trình với Aspose.OCR cho .NET, bạn cần nhập các không gian tên cần thiết. Thêm các dòng sau vào mã của bạn:

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## Tại sao phải chỉ định các ký tự bị bỏ qua?

Trong nhiều tình huống thực tế — chẳng hạn như xử lý hoá đơn, biên lai, hoặc biểu mẫu đa ngôn ngữ — bạn có thể gặp các ký tự lặp lại không phải là dữ liệu có ý nghĩa (ví dụ: dấu gạch nối dùng làm dấu phân cách, số trang, hoặc ký hiệu trang trí). Bằng cách yêu cầu engine OCR bỏ qua chúng, bạn giảm bớt công việc xử lý hậu kỳ và cải thiện độ tin cậy tổng thể của các phân tích downstream.

## Hướng dẫn từng bước

### Bước 1: Thiết lập Thư mục Tài liệu của bạn

Bắt đầu bằng cách chỉ định thư mục nơi lưu trữ tài liệu của bạn. Thay thế `"Your Document Directory"` bằng đường dẫn thực tế tới tài liệu của bạn.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### Bước 2: Khởi tạo Aspose.OCR

Tạo một thể hiện của engine OCR. Đối tượng này sẽ xử lý tất cả các lời gọi nhận dạng tiếp theo.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Bước 3: Nhận dạng hình ảnh với các ký tự bị bỏ qua

Gửi tệp hình ảnh cùng với một đối tượng `RecognitionSettings` liệt kê các ký tự bạn muốn bỏ qua. Trong ví dụ này chúng ta bỏ qua các ký tự `a`, `b` và `1`.

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### Bước 4: Hiển thị văn bản đã nhận dạng

Cuối cùng, xuất văn bản đã được làm sạch ra console hoặc bất kỳ nơi nào bạn muốn.

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## Các vấn đề thường gặp & Mẹo

- **Đường dẫn không đúng:** Đảm bảo `dataDir` kết thúc bằng dấu phân cách đường dẫn (`\` hoặc `/`) phù hợp với hệ điều hành của bạn.  
- **Ngôn ngữ không được hỗ trợ:** Engine OCR phải có gói ngôn ngữ cho hình ảnh nguồn; nếu không, các ký tự bị bỏ qua sẽ không được áp dụng đúng.  
- **Lỗi giấy phép:** Nếu bạn thấy ngoại lệ liên quan đến giấy phép, hãy xác minh rằng tệp giấy phép tạm thời được tham chiếu đúng trong dự án của bạn.

## Kết luận

Aspose.OCR cho .NET cung cấp cho các nhà phát triển khả năng OCR nâng cao, giúp đơn giản hoá quá trình chuyển đổi hình ảnh thành văn bản có thể chỉnh sửa và tìm kiếm. Bằng cách làm theo hướng dẫn từng bước này, bạn đã học cách loại bỏ các ký tự không mong muốn, làm cho các pipeline OCR của mình sạch hơn và đáng tin cậy hơn. Khám phá [tài liệu](https://reference.aspose.com/ocr/net/) để có những hiểu biết sâu hơn và khám phá cách Aspose.OCR có thể nâng cao các dự án OCR của bạn.

## Câu hỏi thường gặp

### Câu hỏi 1: Tôi có thể sử dụng Aspose.OCR cho .NET trong các dự án phi thương mại không?

A1: Có, Aspose.OCR cho .NET có thể được sử dụng trong cả dự án thương mại và phi thương mại. Tham khảo [chi tiết giấy phép](https://purchase.aspose.com/buy) để biết thêm thông tin.

### Câu hỏi 2: Có bản dùng thử miễn phí không?

A2: Chắc chắn! Bạn có thể truy cập bản dùng thử miễn phí [tại đây](https://releases.aspose.com/) để khám phá các tính năng và lợi ích của Aspose.OCR cho .NET trước khi quyết định.

### Câu hỏi 3: Làm sao tôi có thể nhận hỗ trợ cho Aspose.OCR?

A3: Đối với bất kỳ câu hỏi hoặc hỗ trợ nào, hãy truy cập [diễn đàn Aspose.OCR](https://forum.aspose.com/c/ocr/16) để kết nối với cộng đồng và tìm kiếm lời khuyên từ chuyên gia.

### Câu hỏi 4: Aspose.OCR hỗ trợ những ngôn ngữ nào?

A4: Aspose.OCR hỗ trợ một loạt các ngôn ngữ, làm cho nó trở thành lựa chọn đa năng cho các nhiệm vụ OCR. Tham khảo tài liệu để biết danh sách đầy đủ.

### Câu hỏi 5: Tôi có thể mua giấy phép tạm thời cho Aspose.OCR không?

A5: Có, nếu bạn cần giấy phép tạm thời, bạn có thể lấy nó [tại đây](https://purchase.aspose.com/temporary-license/) cho việc sử dụng ngắn hạn.

**Cập nhật lần cuối:** 2025-12-27  
**Kiểm tra với:** Aspose.OCR 23.12 cho .NET  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
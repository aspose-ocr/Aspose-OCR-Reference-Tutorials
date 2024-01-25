---
title: Lưu kết quả nhiều trang dưới dạng tài liệu trong nhận dạng hình ảnh OCR
linktitle: Lưu kết quả nhiều trang dưới dạng tài liệu trong nhận dạng hình ảnh OCR
second_title: API Aspose.OCR .NET
description: Mở khóa tiềm năng của Aspose.OCR cho .NET. Dễ dàng lưu kết quả OCR nhiều trang dưới dạng tài liệu với hướng dẫn từng bước toàn diện này.
type: docs
weight: 14
url: /vi/net/ocr-optimization/save-multipage-result-as-document/
---
## Giới thiệu

Chào mừng bạn đến với thế giới hấp dẫn của nhận dạng ký tự quang học (OCR) bằng Aspose.OCR cho .NET! Trong hướng dẫn này, chúng ta sẽ khám phá cách khai thác các khả năng của Aspose.OCR để lưu kết quả OCR nhiều trang dưới dạng tài liệu. Cho dù bạn là nhà phát triển dày dạn kinh nghiệm hay mới bắt đầu với OCR, hướng dẫn này sẽ hướng dẫn bạn từng bước, đảm bảo bạn tận dụng tối đa công cụ mạnh mẽ này.

## Điều kiện tiên quyết

Trước khi đi sâu vào hướng dẫn, hãy đảm bảo bạn đã thiết lập mọi thứ:

1.  Cài đặt Aspose.OCR cho .NET: Bắt đầu bằng cách tải xuống và cài đặt Aspose.OCR cho .NET. Bạn có thể tìm thấy các tập tin cần thiết[đây](https://releases.aspose.com/ocr/net/).

2.  Nhận bản dùng thử hoặc giấy phép miễn phí: Nếu chưa có, bạn có thể nhận bản dùng thử miễn phí[đây](https://releases.aspose.com/) hoặc mua giấy phép[đây](https://purchase.aspose.com/buy).

3.  Khám phá tài liệu: Làm quen với[tài liệu](https://reference.aspose.com/ocr/net/)cho Aspose.OCR cho .NET. Đây là nguồn thông tin chi tiết mà bạn có thể truy cập.

4.  Truy cập Diễn đàn hỗ trợ: Nếu bạn gặp phải bất kỳ vấn đề hoặc có thắc mắc nào,[diễn đàn hỗ trợ](https://forum.aspose.com/c/ocr/16) là nguồn tài nguyên cộng đồng có giá trị.

Bây giờ bạn đã hoàn tất, hãy chuyển sang hướng dẫn từng bước.

## Nhập không gian tên

Bắt đầu dự án của bạn bằng cách nhập các không gian tên cần thiết:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

## Bước 1: Đặt thư mục tài liệu của bạn

```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```

 Đảm bảo thay thế`"Your Document Directory"` với đường dẫn thực tế đến thư mục tài liệu của bạn.

## Bước 2: Khởi tạo Aspose.OCR

```csharp
// Khởi tạo một phiên bản của AsposeOcr
AsposeOcr api = new AsposeOcr();
```

 Tạo một thể hiện của`AsposeOcr` để truy cập các chức năng OCR.

## Bước 3: Nhận dạng hình ảnh

```csharp
// Nhận dạng hình ảnh
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Sử dụng Aspose.OCR để nhận dạng văn bản từ nhiều hình ảnh. Điều chỉnh đường dẫn tệp theo tệp hình ảnh của bạn.

## Bước 4: Lưu kết quả ở định dạng ưa thích

```csharp
// Lưu kết quả ở định dạng ưa thích của bạn
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Chọn định dạng bạn muốn (Docx, Text, Pdf hoặc Xlsx) và lưu kết quả OCR dưới dạng tài liệu nhiều trang.

## Phần kết luận

Chúc mừng! Bạn đã học thành công cách lưu kết quả OCR nhiều trang dưới dạng tài liệu bằng Aspose.OCR cho .NET. Công cụ đa năng này mở ra vô số khả năng nhận dạng văn bản trong dự án của bạn.

## Câu hỏi thường gặp

### Câu hỏi 1: Giấy phép tạm thời có sẵn cho mục đích thử nghiệm không?

 A1: Có, bạn có thể xin giấy phép tạm thời[đây](https://purchase.aspose.com/temporary-license/) để thử nghiệm Aspose.OCR.

### Câu hỏi 2: Tôi có thể nhận dạng văn bản từ hình ảnh ở các định dạng khác nhau không?

A2: Chắc chắn rồi! Aspose.OCR hỗ trợ nhiều định dạng hình ảnh khác nhau, đảm bảo tính linh hoạt trong các tác vụ OCR của bạn.

### Câu hỏi 3: Có bất kỳ hạn chế nào về số lượng hình ảnh để nhận dạng không?

Câu trả lời 3: Số lượng hình ảnh bạn có thể xử lý tùy thuộc vào giấy phép của bạn. Kiểm tra tài liệu để biết chi tiết.

### Câu hỏi 4: Làm cách nào để xử lý lỗi trong quá trình nhận dạng OCR?

Câu trả lời 4: Tham khảo tài liệu về cách xử lý lỗi tốt nhất hoặc tìm kiếm sự trợ giúp trong diễn đàn hỗ trợ.

### Câu hỏi 5: Aspose.OCR có hỗ trợ các ngôn ngữ khác ngoài tiếng Anh không?

Câu trả lời 5: Có, Aspose.OCR hỗ trợ nhiều ngôn ngữ. Khám phá tài liệu để biết chi tiết hỗ trợ ngôn ngữ.
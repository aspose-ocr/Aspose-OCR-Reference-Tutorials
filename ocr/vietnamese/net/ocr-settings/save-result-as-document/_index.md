---
description: Tìm hiểu cách lưu kết quả OCR với Aspose.OCR cho .NET – chuyển đổi hình
  ảnh sang PDF, trích xuất văn bản từ PNG và lưu văn bản đã nhận dạng dưới dạng DOCX,
  TXT, PDF hoặc XLSX.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: Cách lưu kết quả OCR dưới dạng tài liệu
url: /vi/net/ocr-settings/save-result-as-document/
weight: 10
---

 final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách lưu kết quả OCR dưới dạng tài liệu

## Giới thiệu

Trong hướng dẫn này, bạn sẽ khám phá **cách lưu OCR** bằng cách sử dụng Aspose.OCR cho .NET. Chúng tôi sẽ hướng dẫn cách nhận dạng văn bản trong hình ảnh, sau đó chuyển văn bản đó sang các định dạng tài liệu phổ biến như DOCX, TXT, PDF và XLSX. Khi hoàn thành, bạn sẽ có thể tự động trích xuất dữ liệu từ ảnh và lưu nó dưới dạng các tệp có thể tìm kiếm, chỉnh sửa—lý tưởng cho việc lưu trữ, báo cáo hoặc xử lý tiếp theo.

## Câu trả lời nhanh
- **“cách lưu ocr” có nghĩa là gì?** Nó đề cập đến việc lưu trữ văn bản đã được nhận dạng từ một hình ảnh vào một định dạng tệp như DOCX, PDF, v.v.  
- **Tôi có thể xuất ra những định dạng nào?** DOCX, TXT, PDF và XLSX được hỗ trợ ngay lập tức.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc đánh giá; giấy phép thương mại là bắt buộc cho môi trường sản xuất.  
- **Có thể chuyển đổi ảnh sang PDF trực tiếp không?** Có—lưu kết quả OCR dưới dạng PDF để có tài liệu PDF có thể tìm kiếm.  
- **PNG có được hỗ trợ không?** Chắc chắn; bạn có thể **trích xuất văn bản từ ảnh PNG** bằng cùng một API.

## OCR là gì và tại sao nên lưu kết quả dưới dạng tài liệu?

Optical Character Recognition (OCR) chuyển đổi văn bản in hoặc viết tay trong hình ảnh thành các chuỗi có thể đọc được bởi máy. Việc lưu các chuỗi này dưới dạng tài liệu cho phép bạn:

* Tạo PDF có thể tìm kiếm để tuân thủ quy định.  
* Điền dữ liệu vào bảng tính (XLSX) để phân tích.  
* Tạo báo cáo có thể chỉnh sửa (DOCX).  
* Lưu trữ nhật ký dạng văn bản thuần (TXT) để tìm kiếm nhanh.

## Yêu cầu trước

Trước khi bắt đầu, hãy đảm bảo bạn đã có:

- Aspose.OCR cho .NET được cài đặt. Bạn có thể tải xuống **[tại đây](https://releases.aspose.com/ocr/net/)**.  
- Một thư mục trên máy tính của bạn để chứa các ảnh nguồn và tài liệu đầu ra. Cập nhật biến `dataDir` trong mã để trỏ tới thư mục này.

## Nhập các namespace

Chúng ta cần một vài namespace của .NET để truy cập I/O tệp và các lớp Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Bước 1: Khởi tạo Aspose.OCR

Đặt đường dẫn tới thư mục làm việc của bạn và tạo một thể hiện của engine OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Bước 2: Nhận dạng ảnh

Chuyển file ảnh (ví dụ: PNG) cho bộ nhận dạng. Đây là nơi chúng ta **nhận dạng văn bản trong ảnh** và chuyển chúng thành một `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Bước 3: Lưu kết quả dưới các định dạng khác nhau

Bây giờ chúng ta xuất văn bản đã nhận dạng. Chọn định dạng phù hợp với quy trình làm việc của bạn—cho dù bạn cần **chuyển đổi ảnh sang PDF**, **trích xuất văn bản từ PNG**, hay tạo bảng tính.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Bước 4: Hiển thị thông báo thành công

Một thông báo console đơn giản xác nhận quá trình đã hoàn thành mà không có lỗi.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Những khó khăn thường gặp & Mẹo

- **Đường dẫn tệp:** Luôn sử dụng đường dẫn tuyệt đối hoặc đảm bảo `dataDir` kết thúc bằng ký tự phân tách đường dẫn (`\` hoặc `/`).  
- **Chất lượng ảnh:** Ảnh có độ phân giải cao hơn cải thiện độ chính xác; cân nhắc tiền xử lý (điều chỉnh góc, giảm nhiễu) để có kết quả tốt hơn.  
- **Chế độ giấy phép:** Trong chế độ đánh giá, đầu ra có thể chứa watermark; áp dụng giấy phép hợp lệ để loại bỏ.

## Câu hỏi thường gặp

**Q1. Aspose.OCR có tương thích với các định dạng ảnh khác nhau không?**  
A1: Có, Aspose.OCR hỗ trợ nhiều định dạng ảnh, mang lại tính linh hoạt cho các tác vụ OCR của bạn.

**Q2: Tôi có thể tùy chỉnh cài đặt nhận dạng để cải thiện độ chính xác không?**  
A2: Chắc chắn! Aspose.OCR cung cấp `RecognitionSettings` để tinh chỉnh quá trình OCR theo yêu cầu cụ thể của bạn.

**Q3: Có bản dùng thử miễn phí không?**  
A3: Có, bạn có thể bắt đầu với bản dùng thử miễn phí **[tại đây](https://releases.aspose.com/)**.

**Q4: Làm sao để lấy giấy phép tạm thời cho Aspose.OCR?**  
A4: Giấy phép tạm thời có thể được lấy **[tại đây](https://purchase.aspose.com/temporary-license/)**.

**Q5: Tôi có thể tìm kiếm trợ giúp hoặc kết nối với cộng đồng ở đâu?**  
A5: Tham gia cộng đồng Aspose.OCR tại **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** để được hỗ trợ và thảo luận.

---

**Cập nhật lần cuối:** 2026-02-12  
**Đã kiểm tra với:** Aspose.OCR 24.11 cho .NET  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-02-13
description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Aspose.OCR. Học cách chuyển
  đổi hình ảnh sang PDF, trích xuất văn bản từ hình ảnh, nhúng phông chữ vào PDF và
  nhận dạng văn bản từ PNG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: vi
og_description: Tạo PDF có thể tìm kiếm từ hình ảnh với Aspose.OCR. Hướng dẫn này
  cho thấy cách chuyển đổi hình ảnh sang PDF, nhúng phông chữ và trích xuất văn bản
  từ PNG một cách dễ dàng.
og_title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn C# từng bước
tags:
- C#
- OCR
- Aspose
- PDF generation
title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn C# đầy đủ
url: /vi/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ Hình ảnh – Hướng dẫn đầy đủ C#

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một file PNG đã quét nhưng không biết bắt đầu từ đâu chưa? Bạn không phải là người duy nhất. Trong nhiều dự án—như số hoá hoá đơn hoặc lưu trữ các sách hướng dẫn cũ—khả năng chuyển một bức ảnh thành PDF mà bạn thực sự có thể tìm kiếm là một bước đột phá.  

Trong tutorial này chúng ta sẽ đi qua các bước chính xác để **chuyển đổi hình ảnh sang PDF**, **trích xuất văn bản từ hình ảnh**, nhúng các phông chữ cần thiết, và cuối cùng tạo ra một file PDF hoàn toàn có thể tìm kiếm. Không có tham chiếu mơ hồ, chỉ có một ví dụ đầy đủ, có thể chạy ngay mà bạn có thể sao chép‑dán vào Visual Studio hôm nay.

> **Bạn sẽ nhận được:** một ứng dụng console C# đọc `input.png`, chạy OCR, nhúng phông chữ, giữ lại hình raster gốc làm nền, và ghi ra `output.pdf`. Khi kết thúc, bạn sẽ hiểu *tại sao* mỗi dòng mã quan trọng và cách tùy chỉnh cho các kịch bản của riêng bạn.

---

## Yêu cầu trước

- .NET 6.0 SDK hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+).  
- Aspose.OCR cho .NET – bạn có thể tải từ NuGet (`Install-Package Aspose.OCR`).  
- Một file PNG mẫu (`input.png`) đặt trong thư mục bạn kiểm soát.  
- Kiến thức cơ bản về dự án console C# (nếu chưa từng tạo, chỉ cần mở Visual Studio → **Create a new project** → **Console App** → **C#**).

> **Mẹo:** Aspose cung cấp giấy phép dùng thử miễn phí; chỉ cần đặt file `.lic` cạnh file thực thi và thư viện sẽ hoạt động mà không có watermark.

---

## Bước 1: Cài đặt OCR Engine – Nhận dạng Văn bản từ PNG

Điều đầu tiên chúng ta cần là một OCR engine có thể thực sự đọc các ký tự trong file PNG. Aspose.OCR làm cho việc này trở nên đơn giản.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**Tại sao điều này quan trọng:**  
Cài đặt `Language` cho engine biết bộ ký tự nào sẽ được mong đợi. Nếu bỏ qua, engine sẽ mặc định ở chế độ chung có thể hiểu sai các ký tự có dấu hoặc số. Đối với tài liệu đa ngôn ngữ, bạn có thể truyền danh sách ngăn cách bằng dấu phẩy như `OcrLanguage.English | OcrLanguage.French`.

---

## Bước 2: Tải và Nhận dạng Hình ảnh – Trích xuất Văn bản từ Hình ảnh

Bây giờ engine đã sẵn sàng, chúng ta đưa vào PNG cần xử lý.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**Điều gì đang diễn ra phía sau?**  
`RecognizeImage` quét bitmap, xác định các khối văn bản, và lưu kết quả trong `ocrEngine`. Bạn có thể truy cập `ocrEngine.Text` nếu chỉ cần chuỗi thô, nhưng để tạo PDF có thể tìm kiếm, chúng ta sẽ để Aspose thực hiện chuyển đổi trực tiếp.

> **Trường hợp đặc biệt:** Nếu PNG của bạn quá lớn (hơn 10 MB) có thể hết bộ nhớ. Khi đó, hãy cân nhắc giảm kích thước hình ảnh trước hoặc sử dụng `OcrEngine.RecognizeImage(Stream)` để truyền dữ liệu dạng stream.

---

## Bước 3: Cấu hình Tùy chọn Xuất PDF – Nhúng Phông chữ trong PDF

Một PDF có thể tìm kiếm sẽ không hữu ích nếu phông chữ không được nhúng; tài liệu sẽ bị hỏng trên các máy không có phông chữ cần thiết. Aspose cho phép chúng ta bật/tắt tính năng này bằng một đối tượng tùy chọn đơn giản.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**Tại sao cần nhúng phông chữ?**  
Khi `EmbedFonts` là `true`, PDF sẽ chứa dữ liệu phông chữ bên trong file. Điều này đảm bảo bất kỳ trình xem nào—Chrome, Adobe Reader, hay ứng dụng di động—cũng hiển thị văn bản đúng như mong muốn, ngay cả khi hệ thống mục tiêu không có phông chữ đó.

**Khi nào bạn sẽ đặt `KeepOriginalImage` thành `false`?**  
Nếu bạn chỉ cần văn bản đã trích xuất và muốn file nhỏ hơn, tắt tùy chọn này sẽ loại bỏ hình nền, để lại một PDF “sạch” chỉ có văn bản.

---

## Bước 4: Xuất ra PDF có thể tìm kiếm – Chuyển Đổi Hình ảnh sang PDF

Với kết quả OCR và các tùy chọn PDF đã sẵn sàng, bước cuối cùng chỉ là một dòng lệnh ghi PDF có thể tìm kiếm ra đĩa.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**Bạn sẽ thấy gì:**  
Mở `output.pdf` bằng bất kỳ trình xem nào, bạn có thể chọn văn bản, sao chép, và thậm chí thực hiện tìm kiếm (`Ctrl + F`) để định vị các từ ban đầu chỉ tồn tại dưới dạng pixel trong PNG.

---

## Ví dụ Hoàn chỉnh

Dưới đây là chương trình đầy đủ mà bạn có thể biên dịch và chạy ngay lập tức. Thay `YOUR_DIRECTORY` bằng thư mục chứa `input.png`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Kết quả mong đợi trên console:**

```
Searchable PDF created.
```

Mở `output.pdf` và thử tìm kiếm một từ bạn biết có trong `input.png`. Nếu từ đó được đánh dấu, bạn đã thành công **tạo PDF có thể tìm kiếm** từ hình ảnh.

---

## Câu hỏi Thường gặp & Mẹo Chuyên nghiệp

### “Tôi có thể xử lý nhiều hình ảnh trong một lần chạy không?”

Chắc chắn. Đặt logic nhận dạng và xuất vào trong một vòng lặp, có thể dùng `Directory.GetFiles(..., "*.png")`. Chỉ cần nhớ đặt tên PDF duy nhất cho mỗi file, ví dụ `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### “Nếu tài liệu của tôi chứa cả tiếng Anh và tiếng Tây Ban Nha thì sao?”

Đặt thuộc tính ngôn ngữ thành cờ kết hợp:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Aspose sẽ cố gắng phát hiện ký tự từ cả hai bảng chữ cái.

### “File PDF quá lớn—làm sao giảm kích thước?”

Hai mẹo nhanh:

1. Đặt `pdfOptions.KeepOriginalImage = false` để loại bỏ nền raster.  
2. Sử dụng `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (bạn cần thêm thuộc tính này) để nén hình ảnh được nhúng.

### “Tôi có cần giấy phép cho môi trường sản xuất không?”

Bản dùng thử hoạt động tốt cho việc thử nghiệm, nhưng để triển khai thương mại bạn phải mua giấy phép và đăng ký sớm trong ứng dụng:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## Mở rộng Giải pháp

Bây giờ bạn đã biết cách **tạo PDF có thể tìm kiếm**, bạn có thể muốn:

- **Thêm watermark** – sử dụng `PdfDocument` từ Aspose.PDF để chồng lên văn bản sau OCR.  
- **Xử lý hàng loạt PDF** – kết hợp nhiều PDF có thể tìm kiếm thành một bằng `PdfFileEditor`.  
- **Tích hợp với Azure Blob Storage** – đọc/ghi luồng ảnh và PDF trực tiếp từ đám mây, loại bỏ I/O file cục bộ.

Mỗi phần mở rộng này tuân theo cùng một mẫu: lấy kết quả OCR, cấu hình thư viện tiếp theo, và nối các thao tác lại với nhau.

---

## Kết luận

Bạn vừa học cách **tạo PDF có thể tìm kiếm** từ một hình PNG bằng Aspose.OCR trong C#. Bằng cách khởi tạo OCR engine, nhận dạng văn bản, cấu hình `SearchablePdfOptions` để **nhúng phông chữ trong PDF**, và xuất ra, bạn sẽ có một file vừa giống hệt bản gốc về mặt hình ảnh vừa có khả năng tìm kiếm đầy đủ.  

Từ đây, bạn có thể thử nghiệm chuyển đổi hàng loạt, các ngôn ngữ khác nhau, hoặc nén chặt hơn—tùy theo quy trình làm việc của mình. Nếu gặp khó khăn, diễn đàn Aspose và tài liệu API là nguồn tài nguyên đáng tin cậy, nhưng các bước cốt lõi ở trên sẽ bao phủ 90 % các trường hợp sử dụng thông thường.

Chúc lập trình vui vẻ, và hy vọng các PDF của bạn luôn có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
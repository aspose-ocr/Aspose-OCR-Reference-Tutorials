---
category: general
date: 2026-01-15
description: บทเรียน OCR ด้วย C# ที่แสดงวิธีการจดจำข้อความจากภาพ, ดึงข้อความจากใบแจ้งหนี้และแปลงภาพเป็นข้อความโดยใช้
  Aspose OCR บน GPU.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: th
og_description: บทเรียน OCR ด้วย C# ที่สอนให้คุณจดจำข้อความจากภาพ, ดึงข้อความจากใบแจ้งหนี้และแปลงภาพเป็นข้อความด้วย
  Aspose OCR บน GPU.
og_title: c# OCR tutorial – การจดจำข้อความด้วย GPU ที่เร็ว
tags:
- OCR
- C#
- Aspose
- GPU
title: บทเรียน OCR ด้วย C# – การจดจำข้อความจากภาพด้วยการเร่งความเร็วด้วย GPU
url: /th/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – จดจำข้อความจากรูปภาพด้วยการเร่งความเร็ว GPU

เคยต้องการ **c# ocr tutorial** ที่ทำงานได้จริงโดยไม่ต้องลองผิดลองถูกไม่มีที่สิ้นสุดหรือไม่? บางทีคุณอาจกำลังมองดูใบแจ้งหนี้ความละเอียดสูงและสงสัยว่าจะ **extract text from invoice** ไฟล์ได้ภายในไม่กี่วินาทีอย่างไร ข่าวดีคือคุณไม่ต้องสร้างล้อใหม่—Aspose.OCR ให้ API ที่สะอาดและเร่งด้วย GPU ที่ทำงานหนักให้คุณ

ในคู่มือนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ซึ่งแสดงวิธี **recognize text from image** ไฟล์, **convert image to text**, และจัดการกับปัญหาที่พบบ่อยที่สุด เมื่อเสร็จคุณจะมีโปรแกรมที่ทำงานอิสระซึ่งสามารถอ่านรูปภาพของเอกสารใด ๆ ตั้งแต่ใบเสร็จจนถึงสัญญาที่สแกน และส่งออกข้อความที่สะอาดและค้นหาได้

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการติดตั้งและอ้างอิงแพคเกจ Aspose.OCR NuGet.
- วิธีการกำหนดค่า OCR engine ให้ทำงานบน GPU เพื่อประสิทธิภาพที่เร็วแรง.
- วิธีที่ถูกต้องในการ **load image for ocr** ด้วย `OcrImage.FromFile`.
- วิธีการเรียก `Recognize` พร้อมภาษาที่ต้องการและดึงผลลัพธ์.
- เคล็ดลับสำหรับการจัดการกับ PDF หลายหน้า, การสแกนที่คอนทราสต์ต่ำ, และการจัดการข้อผิดพลาด.

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose มาก่อน; เพียงแค่มีสภาพแวดล้อมการพัฒนา .NET ที่ทำงานได้ (Visual Studio 2022 หรือ VS Code) และ GPU ที่พอใช้ (แม้แต่ GPU แบบบูรณาการของ Intel ก็เพียงพอ).

---

## ขั้นตอนที่ 1 – ติดตั้ง Aspose.OCR และเตรียมโปรเจคของคุณ

สิ่งแรกที่ต้องทำ: คุณต้องการไลบรารี Aspose.OCR วิธีที่ง่ายที่สุดคือผ่าน NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** หากคุณกำหนดเป้าหมายเป็น .NET 6 หรือใหม่กว่า แพคเกจจะดึงไบนารี GPU เนทีฟสำหรับ Windows, Linux, และ macOS โดยอัตโนมัติ ไม่ต้องคัดลอก DLL เพิ่มเติม.

เมื่อเพิ่มแพคเกจแล้ว ให้เปิดไฟล์โปรเจคของคุณ (`*.csproj`) และตรวจสอบการอ้างอิง:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

ตอนนี้คุณมีทุกอย่างที่ต้องการเพื่อเริ่มเขียนโค้ดแล้ว.

## ขั้นตอนที่ 2 – สร้าง OCR Engine ที่ใช้ GPU (c# ocr tutorial)

หัวใจของ **c# ocr tutorial** คือ `OcrEngine` โดยการตั้งค่า `Engine = Engine.Gpu` เราบอก Aspose ให้ใช้การ์ดกราฟิกแทน CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Why GPU?** GPU สามารถประมวลผลพิกเซลหลายพันพิกเซลพร้อมกัน ทำให้เวลา OCR ลดจากวินาทีเป็นเศษวินาทีบนภาพขนาดใหญ่ที่มี DPI สูง.

## ขั้นตอนที่ 3 – โหลดภาพสำหรับ OCR (load image for ocr)

การโหลดภาพอย่างถูกต้องสำคัญกว่าที่คุณคิด `OcrImage.FromFile` รองรับ PNG, JPEG, BMP, TIFF, และแม้กระทั่งหน้าของ PDF อีกด้วย มันยังอ่านค่า DPI ของภาพซึ่งมีผลต่อความแม่นยำ.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Note:** หากคุณกำลังจัดการกับ PDF คุณสามารถแยกแต่ละหน้าเป็น `OcrImage` แล้วป้อนทีละหน้า.

## ขั้นตอนที่ 4 – จดจำข้อความจากภาพ (recognize text from image)

ตอนนี้จุดมุ่งหมายของเราจะเกิดขึ้น เราขอให้ engine จดจำข้อความภาษาอังกฤษ แต่คุณสามารถส่งภาษาที่ Aspose รองรับใด ๆ (Spanish, German, Chinese, ฯลฯ).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

คุณสมบัติ `result.Text` มีสตริงธรรมดา หากคุณต้องการคะแนนความเชื่อมั่นของแต่ละคำ คุณสามารถตรวจสอบ `result.Regions`.

### ผลลัพธ์ที่คาดหวัง

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

หากภาพเบลอ คุณอาจเห็นอักขระแปลก ๆ — นี่คือจุดที่การเตรียมข้อมูลจากขั้นตอนที่ 3 ช่วยได้.

## ขั้นตอนที่ 5 – ดึงข้อความจากใบแจ้งหนี้ – ตัวอย่างจากโลกจริง

สมมติว่าคุณมีโฟลเดอร์ที่เต็มไปด้วยใบแจ้งหนี้ที่สแกนและคุณต้องการดึงจำนวนเงินรวม ด้านล่างเป็นการขยายโค้ดก่อนหน้าที่ใช้ regular expression อย่างง่าย.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

คุณจะเรียก `ExtractTotalAmount(result.Text);` ทันทีหลังจากพิมพ์ผลลัพธ์ OCR นี้แสดงให้เห็นว่าการ **extract text from invoice** ไฟล์เป็นเรื่องง่ายแค่ไหนเมื่อคุณมีสตริงดิบแล้ว.

## ขั้นตอนที่ 6 – แปลงภาพเป็นข้อความเป็นชุด (convert image to text)

การประมวลผลไฟล์เดียวอาจพอสำหรับการสาธิต แต่โค้ดในการผลิตมักต้องจัดการกับหลายสิบหรือหลายร้อยภาพ นี่คือ loop สั้น ๆ ที่ประมวลผลทั้งไดเรกทอรี:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

การเรียก `ProcessFolder(ocrEngine, @"C:\Invoices")` จะ **convert image to text** สำหรับทุกไฟล์ที่รองรับในโฟลเดอร์โดยใช้ GPU เพื่อความเร็ว.

## กรณีขอบและปัญหาที่พบบ่อย

| Situation | Why It Happens | Quick Fix |
|-----------|----------------|-----------|
| **Low‑contrast scan** | OCR มีปัญหาในการแยกแยะพื้นหน้าและพื้นหลัง. | เพิ่มคอนทราสต์ (`ImagePreprocessor.AdjustContrast`) หรือใช้ adaptive thresholding. |
| **Multi‑page PDF** | `OcrImage.FromFile` อ่านเฉพาะหน้าหนึ่งแรก. | ใช้ `PdfDocument` เพื่อแยกแต่ละหน้าเป็น `OcrImage` แล้ววนลูป. |
| **Unsupported language** | ภาษาที่ตั้งค่าเริ่มต้นคืออังกฤษ. | ส่งค่า `Language.Spanish` หรือค่า enum ที่รองรับอื่น ๆ. |
| **GPU not detected** | ไบนารีเนทีฟหายหรือไดรเวอร์ล้าสมัย. | ตรวจสอบว่าไดรเวอร์ GPU เป็นเวอร์ชันล่าสุด; ติดตั้งใหม่แพคเกจ NuGet ด้วย flag `-runtime`. |
| **Out‑of‑memory on huge images** | หน่วยความจำ GPU มีจำกัด. | ลดขนาดภาพ (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกและวางลงในแอปคอนโซลใหม่ได้ รวมถึงเมธอดช่วยเหลือทั้งหมดที่กล่าวถึงข้างต้น.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-21
description: ทำ OCR บนภาพโดยใช้ C# เรียนรู้วิธีโหลดภาพสำหรับ OCR ดึงข้อความจาก PNG
  และจดจำข้อความจากภาพด้วยตัวอย่างโค้ดขนาดเล็ก
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: th
og_description: ทำ OCR บนภาพด้วย C# อย่างรวดเร็ว คู่มือนี้แสดงวิธีโหลดภาพสำหรับ OCR,
  ดึงข้อความจากไฟล์ PNG, และจดจำข้อความจากภาพพร้อมผลลัพธ์ HTML ที่คำนึงถึงการจัดวาง
og_title: ทำ OCR บนรูปภาพด้วย C# – บทเรียนการเขียนโปรแกรมเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: ทำ OCR บนรูปภาพด้วย C# – คู่มือขั้นตอนเต็ม
url: /th/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพด้วย C# – คู่มือขั้นตอนเต็ม

เคยสงสัยไหมว่า **perform OCR on image** อย่างไรโดยไม่ต้องต่อสู้กับ GUI ที่หนักหน่วง? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังแปลงใบเสร็จเป็นดิจิทัล ดึงข้อมูลจากแบบฟอร์มสแกน หรือแค่ต้องการเปลี่ยน PNG ให้เป็นข้อความที่ค้นหาได้ เพียงไม่กี่บรรทัดของ C# ก็ทำได้

ในบทเรียนนี้เราจะอธิบายการโหลดรูปภาพสำหรับ OCR, การจดจำข้อความจากรูปภาพ, และสุดท้ายการแปลงข้อความจาก PNG เป็น HTML ที่สะอาด เมื่อเสร็จคุณจะมีแอปคอนโซลที่พร้อมรันซึ่ง **performs OCR on image** และรักษาเลย์เอาต์เดิมไว้

## สิ่งที่คุณจะสร้าง

- โปรแกรมคอนโซลขนาดเล็กที่อ่าน PNG (หรือรูปภาพที่รองรับอื่นใด)  
- ใช้ OCR engine เพื่อ **recognize text from image**  
- บันทึกผลเป็น HTML ที่คำนึงถึงเลย์เอาต์ พร้อมฝังรูปภาพต้นฉบับ  
- แสดงวิธี **load image for OCR**, **extract text from PNG**, และจัดการกับกรณีขอบทั่วไป  

> **Prerequisites**  
> - .NET 6.0 SDK หรือใหม่กว่า (คุณสามารถตั้งเป้าหมายเป็น .NET Framework 4.7+ ได้)  
> - ไลบรารี OCR ที่รองรับ NuGet – ตัวอย่างใช้ *Aspose.OCR* แต่ไลบรารีใดที่มี API คล้ายกันก็ใช้ได้  
> - ความรู้พื้นฐาน C# (ไม่ต้องซับซ้อน)  

พร้อมหรือยัง? ดี—มาเริ่มกันเลย

## Perform OCR on Image – Full Code Walkthrough

ด้านล่างเป็นโปรแกรม **complete, runnable** คัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ (`dotnet new console`) แล้วกด **F5**

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Expected output**  
> ```
> HTML with layout saved.
> ```  
> หลังจากรันคุณจะพบ `form.html` อยู่ข้างไฟล์ PNG ของคุณ เปิดในเบราว์เซอร์แล้วคุณจะเห็นเลย์เอาต์เดิม แต่ข้อความตอนนี้สามารถเลือกและค้นหาได้

### Load Image for OCR

บรรทัด `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` คือจุดที่เร **load image for OCR** `ImageStream` helper จะจัดการรายละเอียดรูปแบบไฟล์ให้คุณ จึงสามารถใส่ JPEG, BMP หรือ TIFF ได้โดยไม่ต้องเปลี่ยนโค้ด  

**ทำไมไม่ส่ง `Bitmap` ตรงๆ?**  
เพราะหลาย OCR SDK ต้องการสตรีมที่บรรจุเมตาดาต้า DPI ด้วย การใช้ loader ในไลบรารีทำให้ engine เห็นภาพตรงตามที่แสดงบนหน้าจอ ซึ่งช่วยเพิ่มความแม่นยำ

#### Pro tip
หากคุณประมวลผลไฟล์หลายไฟล์ ให้ห่อขั้นตอนการโหลดใน `try/catch` และบันทึก `FileNotFoundException` ใดๆ นั่นจะป้องกันไม่ให้แบตช์ทั้งหมดล่มเพราะไฟล์หนึ่งหายไป

### Extract Text from PNG

เมื่อ `engine.Recognize()` เสร็จ OCR engine จะเก็บข้อความที่จดจำไว้ภายใน คุณสามารถดึงออกเป็นสตริงได้หากต้องการเพียงข้อความดิบ:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

นี่เป็นวิธีที่เร็วที่สุดในการ **extract text from PNG** เมื่อคุณไม่สนใจเลย์เอาต์ สำหรับงานใส่ข้อมูลส่วนใหญ่ ข้อความธรรมดาก็พอ—แค่จำไว้ว่าให้ตัดบรรทัดว่างออกหากจะนำเข้า CSV

### Recognize Text from Image

การเรียก `Recognize()` ทำงานหนักให้ engine ทำตามขั้นตอนต่อไปนี้  

1. ปรับภาพให้เป็นมาตรฐาน (deskews, removes noise)  
2. แบ่งภาพเป็นบรรทัดและคำ  
3. รันตัวจำแนกแบบ neural‑network ที่ฝึกด้วย glyph ล้านๆ ตัว  

เนื่องจากเราตั้งค่า `Language = OcrLanguage.English` engine จะใช้พจนานุกรมภาษาอังกฤษ ซึ่งลด false positives อย่างมาก หากต้องการรองรับหลายภาษา เพียงส่งอาเรย์ของภาษา:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Handling Layout‑Aware HTML Output

นักพัฒนาส่วนใหญ่หยุดที่ข้อความธรรมดา แต่ `HtmlSaveOptions` ที่เราใช้ทำให้คุณ **perform OCR on image** และรักษาโครงสร้างภาพไว้สองค่าสำคัญ:

- `PreserveLayout = true` – รักษาคอลัมน์, ตาราง, และช่องว่าง  
- `EmbedImages = true` – ฝัง PNG ต้นฉบับเป็น `<img>` ที่เข้ารหัส Base64 ทำให้ HTML เป็นไฟล์เดียว

หากต้องการไฟล์ที่เบากว่า ตั้งค่า `EmbedImages = false` แล้ว HTML จะอ้างอิง PNG ดั้งเดิมบนดิสก์แทน

#### Edge case: Large files

สำหรับภาพที่ใหญ่กว่า 5 MB การฝังอาจทำให้ขนาด HTML พุ่งขึ้น ในกรณีเช่นนี้ให้เปลี่ยนเป็นอ้างอิงภาพภายนอกและพิจารณาบีบอัด PNG ก่อนด้วย `ImageProcessor.Compress`

## Common Pitfalls and Pro Tips

| Symptom | Likely Cause | Fix |
|--------|--------------|-----|
| Garbled characters | Wrong language set or missing language pack | Install the appropriate language data files and set `engine.Language` correctly |
| No text in output | Image is too dark or low‑resolution | Pre‑process with `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Layout broken in HTML | `PreserveLayout` left at default `false` | Set `PreserveLayout = true` in `HtmlSaveOptions` |
| Slow processing on many pages | Engine re‑initializes per file | Reuse the same `OcrEngine` instance and only change `engine.Image` each loop |

### Scaling to Multiple Files

หากต้องการ **perform OCR on image** ไฟล์หลายไฟล์ในโฟลเดอร์ ให้ห่อโลจิกหลักในลูปง่ายๆ:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

สังเกตว่าเรา **load image for OCR** ภายในลูป แต่ใช้ `engine` และ `htmlOptions` เดียวกัน ซึ่งช่วยลดการใช้หน่วยความจำและเร่งความเร็วงานแบตช์

## Going Beyond: Exporting to PDF or DOCX

`engine` เดียวกันสามารถบันทึกเป็นฟอร์แมตอื่นได้:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

หากระบบต่อท้ายของคุณต้องการ PDF ที่ค้นหาได้ เพียงเปลี่ยนบรรทัดเดียว—ไม่ต้องเขียน pipeline แยก

## Conclusion

เราได้แสดงวิธี **perform OCR on image** ด้วย C# ตั้งแต่การโหลดรูปภาพจนถึง **extract text from PNG** และสุดท้าย **recognize text from image** เป็นไฟล์ HTML ที่คำนึงถึงเลย์เอาต์ ตัวอย่างเต็มพร้อมรันแล้ว และคุณเข้าใจแล้วว่าขั้นตอนแต่ละขั้นตอนสำคัญอย่างไร ปรับให้รองรับภาษาต่างๆ ได้อย่างไร และควรระวังจุดบกพร่องอะไรบ้าง

ต่อไปลองสลับภาษาอังกฤษเป็นภาษาท้องถิ่นอื่น ทดลอง `PreserveLayout = false` เพื่อให้ HTML เบากว่า หรือส่งออกข้อความธรรมดาไปยังฐานข้อมูลเพื่อทำดัชนีค้นหา ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณผสาน OCR engine ที่แข็งแกร่งกับบรรทัดโค้ด C# เพียงไม่กี่บรรทัด

มีคำถามเกี่ยวกับการจัดการ TIFF หลายหน้า หรืออยากรู้วิธีรวมเข้ากับ ASP.NET Core API? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

## Related Tutorials

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
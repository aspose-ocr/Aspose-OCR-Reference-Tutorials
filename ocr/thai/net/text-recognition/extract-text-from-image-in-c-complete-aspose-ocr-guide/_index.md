---
category: general
date: 2026-01-10
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# เรียนรู้วิธีแปลงข้อความจากเอกสารสแกนด้วยการประมวลผลแบบกลุ่มและบันทึกผลลัพธ์
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: th
og_description: สกัดข้อความจากภาพด้วย Aspose OCR ใน C# บทเรียนนี้แสดงวิธีแปลงข้อความของเอกสารสแกนโดยใช้การประมวลผลแบบกลุ่ม
og_title: ดึงข้อความจากภาพใน C# – คู่มือ Aspose OCR ฉบับสมบูรณ์
tags:
- OCR
- C#
- Aspose
- Image Processing
title: ดึงข้อความจากภาพใน C# – คู่มือ Aspose OCR ฉบับสมบูรณ์
url: /th/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากรูปภาพ – คู่มือ Aspose OCR ฉบับสมบูรณ์

เคยต้องการ **สกัดข้อความจากรูปภาพ** แต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว; นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อทำงานกับ PDF ที่สแกน, TIFF หลายหน้า, หรือใบเสร็จที่เป็นรูปถ่าย. ข่าวดีคือด้วย Aspose OCR คุณสามารถ **แปลงข้อความจากเอกสารที่สแกน** ได้ด้วยเพียงไม่กี่บรรทัดของ C#.

ในบทแนะนำนี้เราจะเดินผ่านสถานการณ์จริง: รับไฟล์ TIFF หลายหน้า, รัน OCR แบบแบตช์บนแต่ละหน้า, และเขียนไฟล์ข้อความเดียวที่บรรจุเนื้อหาของทุกหน้า. เมื่อเสร็จคุณจะมีแอปคอนโซลที่พร้อมรัน, เข้าใจเหตุผลของแต่ละขั้นตอน, และรู้วิธีปรับเปลี่ยนกระบวนการสำหรับกรณีขอบเช่นรูปภาพที่มีรหัสผ่านหรือแพ็คเกจภาษาที่กำหนดเอง.

## ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK หรือใหม่กว่า (โค้ดทำงานกับ .NET Core และ .NET Framework ด้วย)  
- Visual Studio 2022 (หรือเครื่องมือแก้ไขที่คุณชอบ)  
- ไฟล์ลิขสิทธิ์ Aspose OCR (หรือคุณสามารถใช้โหมดประเมินผลฟรี)  
- ไฟล์รูปภาพหลายหน้า (เช่น `multipage.tif`) ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้  

ไม่มีแพ็กเกจ NuGet เพิ่มเติมที่จำเป็นนอกจาก `Aspose.OCR`; เราจะติดตั้งมันในขั้นตอนแรก.

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR และตั้งค่าโปรเจกต์

เริ่มต้นโดยสร้างโปรเจกต์คอนโซลใหม่และดึงไลบรารี Aspose OCR เข้ามา.

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **เคล็ดลับ:** หากคุณมีไฟล์ลิขสิทธิ์ (`Aspose.OCR.lic`), ให้คัดลอกไปยังโฟลเดอร์รากของโปรเจกต์. ไลบรารีจะดึงไฟล์นี้โดยอัตโนมัติขณะรัน.

ทำไมต้องทำขั้นตอนนี้? การติดตั้งแพ็กเกจทำให้คุณเข้าถึง `BatchProcessor`, `OcrEngine`, และคลาสที่มีประโยชน์อื่น ๆ ที่ช่วยซ่อนการจัดการภาพระดับล่าง. มันยังรับประกันว่าคุณใช้ алгоритм OCR ล่าสุดที่ Aspose จัดให้.

## ขั้นตอนที่ 2 – โหลดรูปภาพหลายหน้าโดยใช้ BatchProcessor

`BatchProcessor` ถูกออกแบบมาสำหรับสถานการณ์นี้โดยเฉพาะ: การวนซ้ำแต่ละหน้าของไฟล์หลายหน้าโดยที่คุณไม่ต้องแยกไฟล์ด้วยตนเอง.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

`BatchProcessor` จะอ่านทุกหน้าเข้าหน่วยความจำและให้เข้าถึงผ่าน `batchProcessor.Pages`. แต่ละอ็อบเจ็กต์หน้าเก็บหมายเลขของมัน (`ocrPage.Number`) ซึ่งเราจะใช้ต่อไปเพื่อสร้างหัวข้อที่ชัดเจน.

## ขั้นตอนที่ 3 – เตรียม StringBuilder เพื่อสะสมผลลัพธ์

เราต้องการไฟล์ข้อความเดียวที่บรรจุผลลัพธ์ OCR ของทุกหน้า, แยกด้วยหัวข้อ. `StringBuilder` เป็นวิธีที่มีประสิทธิภาพที่สุดในการต่อสตริงในลูป.

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

ทำไมต้องใช้ `StringBuilder`? การต่อสตริงด้วย `+` ภายในลูปจะสร้างสตริงใหม่ทุกครั้ง, ทำให้ประสิทธิภาพลดลง—โดยเฉพาะกับเอกสารขนาดใหญ่.

## ขั้นตอนที่ 4 – วนซ้ำแต่ละหน้า, รัน OCR, และเพิ่มผลลัพธ์

นี่คือหัวใจของบทแนะนำ: วนผ่านแต่ละหน้า, จดจำข้อความ, และบันทึกพร้อมเครื่องหมายหน้าหนังสือ.

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**ทำไมต้องสร้าง `OcrEngine` ใหม่สำหรับแต่ละหน้า?** นักพัฒนาบางคนอาจใช้เอนจินเดียวและเปลี่ยนคุณสมบัติ `Image`, แต่การทำเช่นนั้นอาจเก็บการตั้งค่าภาษา หรือผลลัพธ์ก่อนหน้าไว้, ทำให้เกิดบั๊กที่ละเอียดอ่อน. การสร้างเอนจินใหม่ทุกครั้งรับประกันว่ามีสภาพแวดล้อมที่สะอาด.

### การจัดการกรณีขอบที่พบบ่อย

- **หน้าว่าง:** หากหน้าหนึ่งไม่มีข้อความที่สามารถจดจำได้, `ocrEngine.Text` จะเป็นสตริงว่าง. คุณอาจต้องใส่ตัวแทนเช่น “(ไม่พบข้อความ)”.
- **การเลือกภาษา:** โดยค่าเริ่มต้น Aspose OCR ใช้ภาษาอังกฤษ. หากต้องการประมวลผลภาษาเยอรมันหรือฝรั่งเศส, ตั้งค่า `ocrEngine.Language = Language.German;` ก่อนเรียก `Recognize()`.
- **เคล็ดลับประสิทธิภาพ:** สำหรับ TIFF ขนาดใหญ่, คุณสามารถเปิด `ocrEngine.UseParallelProcessing = true;` เพื่อใช้หลายคอร์.

## ขั้นตอนที่ 5 – เขียนผลลัพธ์ที่รวมกันลงไฟล์ข้อความ

สุดท้าย, บันทึกสตริงที่สะสมไว้ลงดิสก์.

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

ไฟล์ `multipage_result.txt` ที่ได้จะมีลักษณะประมาณนี้:

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

คุณได้ **สกัดข้อความจากรูปภาพ** และ **แปลงข้อความจากเอกสารที่สแกน** เป็นรูปแบบที่สามารถค้นหาและแก้ไขได้.

## โบนัส – ภาพรวมเชิงภาพ (Alt Text)

ด้านล่างเป็นแผนภาพกระบวนการอย่างง่ายที่แสดงขั้นตอนทั้งหมด.  
*Alt text:* “แผนภาพแสดงวิธีสกัดข้อความจากรูปภาพโดยใช้การประมวลผลแบบแบตช์ของ Aspose OCR ใน C#”.

![OCR Flow Diagram](placeholder-image-url.png)

*(หากคุณกำลังเผยแพร่บทแนะนำนี้บนเว็บไซต์แบบสแตติก, ให้แทนที่ placeholder ด้วยไฟล์ SVG หรือ PNG จริง.)*

## คำถามที่พบบ่อย

**ทำงานกับไฟล์ PDF ได้หรือไม่?**  
ใช่, Aspose OCR สามารถอ่านหน้าของ PDF เป็นภาพได้. คุณเพียงแค่ต้องแปลง PDF เป็นภาพก่อน, หรือใช้ `PdfDocument` จาก `Aspose.PDF` แล้วส่งภาพที่แรสเตอร์ไลซ์ของแต่ละหน้าให้ `OcrEngine`.

**ถ้า TIFF ของฉันมีรหัสผ่านจะทำอย่างไร?**  
`BatchProcessor` ไม่รองรับการถอดรหัสโดยตรง. ให้ถอดรหัสไฟล์ด้วยไลบรารีเช่น `Aspose.Imaging` ก่อนส่งต่อไปยังขั้นตอน OCR.

**สามารถส่งออกเป็น JSON แทนข้อความธรรมดาได้หรือไม่?**  
ได้เลย. แทนที่ตรรกะ `StringBuilder` ด้วยตัวแปลง JSON (เช่น `System.Text.Json`) และเก็บข้อความของแต่ละหน้าไว้ภายใต้คีย์ `pageNumber`.

## ตัวอย่างทำงานเต็มรูปแบบ

นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน `Program.cs`. มันรวมคำสั่ง `using` ทั้งหมด, การจัดการข้อผิดพลาด, และคอมเมนต์.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

รันโปรแกรมด้วยคำสั่ง:

```bash
dotnet run
```

คุณควรเห็นข้อความในคอนโซลยืนยันความสำเร็จ, และไฟล์ผลลัพธ์จะมีข้อความ OCR ที่ต่อกันเรียบร้อย.

## สรุป

เราได้สาธิตวิธีการ **สกัดข้อความจากรูปภาพ** อย่างเป็นระบบด้วย Aspose OCR, เปลี่ยนไฟล์สแกนหลายหน้าให้เป็นข้อความธรรมดาที่ค้นหาได้. ด้วยการใช้ `BatchProcessor` และการตั้งค่า `OcrEngine` แยกต่อหน้า, คุณสามารถ **แปลงข้อความจากเอกสารที่สแกน** ได้อย่างเชื่อถือได้ พร้อมโค้ดที่เรียบง่ายและดูแลรักษาง่าย.

ลองทดลองเพิ่มเติม: ใช้ภาษาต่าง ๆ, เปลี่ยนเป็นการส่งออกเป็น JSON, หรือรวมตรรกะนี้เข้าไปใน Web API ที่ประมวลผลไฟล์อัปโหลดแบบเรียลไทม์. รูปแบบหลักยังคงเหมือนเดิม—โหลด, จดจำ, สะสม, และบันทึก.

มีคำถามเพิ่มเติมเกี่ยวกับ OCR, การลิขสิทธิ์ Aspose, หรือการจัดการชุดเอกสารขนาดใหญ่? แสดงความคิดเห็นด้านล่างหรือดูเอกสารอย่างเป็นทางการของ Aspose เพื่อข้อมูลเชิงลึกเพิ่มเติม. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
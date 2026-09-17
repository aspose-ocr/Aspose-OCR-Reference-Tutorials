---
category: general
date: 2026-01-04
description: สร้าง PDF ที่ค้นหาได้จาก PDF ที่สแกนอย่างรวดเร็ว เรียนรู้วิธีแปลง PDF
  ที่สแกน เพิ่ม OCR ให้กับ PDF และปรับคุณภาพภาพด้วย Aspose OCR ใน C#
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: th
og_description: สร้าง PDF ที่ค้นหาได้จาก PDF สแกนอย่างรวดเร็ว ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อแปลง
  PDF สแกน, เพิ่ม OCR ให้ PDF, และปรับคุณภาพภาพ.
og_title: สร้าง PDF ที่ค้นหาได้จากไฟล์สแกนโดยใช้ Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: สร้าง PDF ที่ค้นหาได้จากไฟล์สแกนโดยใช้ Aspose OCR
url: /th/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้จากไฟล์สแกนโดยใช้ Aspose OCR

เคยต้อง **สร้าง PDF ที่ค้นหาได้** จากกองเอกสารสแกนหลายไฟล์แต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อตั้งค่า pipeline การจัดการเอกสาร ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถ **แปลง PDF ที่สแกน**, เติม OCR, และปรับคุณภาพภาพได้เพียงไม่กี่บรรทัดของ C#.

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด ตั้งแต่การโหลด PDF ที่สแกนจนถึงการบันทึกเป็นเวอร์ชันที่ค้นหาได้เต็มรูปแบบ. เมื่อเสร็จคุณจะรู้ **วิธีใช้ OCR** กับ Aspose, ทำไมแต่ละการตั้งค่าถึงสำคัญ, และจะปรับอะไรเมื่อผลลัพธ์ไม่เป็นตามที่คาด. ไม่มีการอ้างอิงแบบคลุมเครือ—เพียงตัวอย่างที่ทำงานได้เต็มรูปแบบที่คุณสามารถนำไปใส่ในโปรเจกต์ของคุณได้ทันที.

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงมือทำ, ตรวจสอบให้แน่ใจว่าคุณมี:

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Core และ .NET Framework ด้วย)
- ไลเซนส์ Aspose OCR ที่ถูกต้อง (รุ่นทดลองฟรีใช้สำหรับการทดสอบ)
- PDF อินพุตชื่อ `input.pdf` ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม
- Visual Studio 2022 หรือเครื่องมือแก้ไข C# ใด ๆ ที่คุณชอบ

แค่นั้นเอง. หากมีส่วนใดที่คุณไม่คุ้นเคย, หยุดและติดตั้งส่วนที่ขาด—ไม่มีสิ่งอื่นที่จำเป็น.

## ขั้นตอนที่ 1: เริ่มต้น OCR Engine และโหลด PDF ที่สแกน  
**(นี่คือจุดที่เราจะ **เพิ่ม OCR ให้กับ PDF** ครั้งแรก.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*ทำไมต้องทำขั้นตอนนี้?*  
`OcrEngine` คือหัวใจของ Aspose OCR. การโหลด PDF บอก engine ว่าจะต้องมองหารูปภาพเรสเตอร์ที่ต้องวิเคราะห์ต่อไป. หากข้ามขั้นตอนนี้, จะไม่มีอะไรให้แปลงและขั้นตอนต่อไปจะโยนข้อยกเว้น.

> **เคล็ดลับ:** หาก PDF ของคุณมีการป้องกันด้วยรหัสผ่าน, ใช้ `ocrEngine.LoadPdf(path, password)` เพื่อหลีกเลี่ยงข้อผิดพลาดขณะรัน.

## ขั้นตอนที่ 2: ตั้งค่าภาษาหลักและภาษาเพิ่มเติม  
**(เราจะ **แปลง PDF ที่สแกน** เป็นภาษาอังกฤษ, ฝรั่งเศส, และเยอรมัน.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*ทำไมภาษาถึงสำคัญ?*  
ความแม่นยำของ OCR พึ่งพาชุดอักขระที่คาดหวัง. การระบุภาษาอังกฤษเป็นภาษาแรกและเพิ่มฝรั่งเศส/เยอรมันทำให้ engine สามารถตีความอักขระที่มีสำเนียงและ glyph พิเศษได้อย่างถูกต้อง. ลืมตั้งค่านี้มักทำให้ข้อความเป็นอักขระผสมกัน.

## ขั้นตอนที่ 3: ปรับคุณภาพภาพ – ปรับแต่งผลลัพธ์ PDF  
**(ที่นี่เราจะ **ปรับคุณภาพภาพ** เพื่อหาสมดุลระหว่างขนาดไฟล์และความอ่านง่าย.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*ทำไมต้องปรับ `ImageQuality`?*  
ค่าที่สูงกว่า (90‑100) จะรักษาความคมชัด, ซึ่งสำคัญต่อความแม่นยำของ OCR, แต่ก็ทำให้ไฟล์ขนาดใหญ่ขึ้น. หากคุณต้องเก็บหลายล้านหน้า, ลดลงเป็น 70‑80 เพื่อให้ PDF แบนลงโดยไม่เสียความอ่านมากเกินไป.

## ขั้นตอนที่ 4: บันทึกผลลัพธ์เป็น PDF ที่ค้นหาได้  
**(ตอนนี้เราจะ **สร้าง PDF ที่ค้นหาได้** เพื่อให้คุณสามารถทำดัชนีได้.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*จริง ๆ แล้วเกิดอะไรขึ้น?*  
Aspose OCR ดึงชั้นข้อความจากแต่ละหน้าและฝังไว้ด้านหลังภาพต้นฉบับ. PDF ยังคงดูเหมือนเดิม, แต่คุณสามารถเลือก, คัดลอก, และค้นหาข้อความได้—เป็นประโยชน์อย่างมากสำหรับ workflow ต่อไป.

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ (ไม่บังคับแต่แนะนำ)  
ง่ายต่อการสมมติว่าทุกอย่างทำงานเรียบร้อย, แต่การตรวจสอบอย่างเร็วช่วยหลีกเลี่ยงปัญหาในภายหลัง.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

เปิดไฟล์, ลองเลือกคำหนึ่งคำ, หรือกด `Ctrl+F` แล้วพิมพ์วลีที่คุณรู้ว่ามีอยู่ในสแกนต้นฉบับ. หากข้อความสามารถเลือกได้, คุณได้ **สร้าง PDF ที่ค้นหาได้** อย่างสำเร็จ.

## กรณีขอบเขตทั่วไป & วิธีจัดการ  

| สถานการณ์ | ทำไมถึงเกิด | วิธีแก้เร็ว |
|-----------|--------------|-------------|
| **หน้าที่มีความละเอียดแตกต่าง** (บางหน้า 150 dpi, บางหน้า 300 dpi) | คุณภาพ OCR แตกต่างตามหน้า, ทำให้การค้นหาไม่สม่ำเสมอ. | ตั้งค่า `ocrEngine.Config.Dpi = 300;` ก่อนโหลดเพื่อบังคับอัพสแคล, หรือทำการพรี‑โปรเซสด้วย `ImageProcessor` เพื่อทำให้ DPI สม่ำเสมอ. |
| **PDF ที่เข้ารหัส** | Aspose OCR ไม่สามารถอ่านได้หากไม่มีรหัสผ่าน. | ส่งรหัสผ่านไปยัง `LoadPdf` ตามที่แสดงข้างต้น. |
| **PDF ขนาดใหญ่ (>500 MB)** | การใช้หน่วยความจำพุ่งสูง, ทำให้เกิด `OutOfMemoryException`. | แบ่งเอกสารเป็นชิ้นส่วน: `ocrEngine.SplitPdfIntoPages();` แล้วทำ OCR ทีละหน้าและรวมผลลัพธ์. |
| **อักขระไม่ใช่ละติน** (เช่น Cyrillic) | ไม่ได้เพิ่มภาษา, ทำให้ตัวอักษรกลายเป็น “?” | เพิ่ม `Language.Russian` (หรือภาษาที่ต้องการ) ไปยัง `AdditionalLanguages`. |
| **คุณภาพภาพต่ำเกินไป** | ข้อความเบลอ, OCR ล้มเหลว. | เพิ่มค่า `ImageQuality` หรือใช้ `pdfOptions.Dpi = 300;` เพื่อฝังภาพความละเอียดสูงกว่า. |

## ตัวอย่างเต็มพร้อมรัน  

ด้านล่างเป็นโปรแกรมสมบูรณ์ที่คุณสามารถคัดลอก‑วางลงในแอปคอนโซลใหม่. รวมทุกขั้นตอน, การจัดการข้อผิดพลาด, และคอมเมนต์เพื่อความชัดเจน.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

เมื่อคุณเปิด `output.pdf`, ควรจะสามารถเลือกและค้นหาข้อความใด ๆ ที่มีอยู่ในสแกนต้นฉบับได้.

---

## คำถามที่พบบ่อย (FAQs)

**ถาม: วิธีนี้ทำงานกับ PDF ที่มีทั้งภาพสแกนและข้อความดั้งเดิมได้หรือไม่?**  
ตอบ: ทำได้แน่นอน. Aspose OCR จะเพิ่มชั้นข้อความที่ซ่อนอยู่เฉพาะที่จำเป็น, ส่วนข้อความที่มีอยู่แล้วจะไม่ถูกแก้ไข.

**ถาม: สามารถประมวลผลหลาย PDF ในโฟลเดอร์พร้อมกันได้หรือไม่?**  
ตอบ: ได้. ห่อโค้ดข้างต้นด้วยลูป `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` แล้วปรับเส้นทางเอาต์พุตตามต้องการ.

**ถาม: จะลดขนาด PDF สุดท้ายได้อีกอย่างไร?**  
ตอบ: ลด `ImageQuality` ลง 70‑80, เปิด `Compress`, หรือใช้ `pdfOptions.Dpi = 150` เพื่อลดความละเอียดของภาพก่อนฝัง.

**ถาม: มีวิธีดึงข้อความ OCR โดยไม่ต้องสร้าง PDF หรือไม่?**  
ตอบ: เรียก `ocrEngine.ExtractText();` หลังจากโหลด PDF. คำสั่งนี้จะคืนสตริงข้อความธรรมดาที่คุณสามารถเก็บหรือทำดัชนีต่อได้.

---

## สรุป  

เราได้อธิบาย **วิธีใช้ OCR** กับ Aspose เพื่อ **สร้าง PDF ที่ค้นหาได้** จากเอกสารสแกน, แสดง **การแปลง PDF ที่สแกน**, **การเพิ่ม OCR ให้ PDF**, และ **การปรับคุณภาพภาพ** เพื่อผลลัพธ์ที่ดีที่สุด. โค้ดตัวอย่างเต็มพร้อมรันและตารางการแก้ไขปัญหาพร้อมให้คุณใช้งานทันที.

ต่อไปคุณอาจลอง:

- ใช้แพ็คเกจภาษาต่าง ๆ สำหรับคลังเอกสารหลายภาษา
- พรี‑โปรเซสภาพแบบกำหนดเอง (deskew, despeckle) ผ่าน `ImageProcessor`
- ผสาน PDF ที่ค้นหาได้เข้ากับ pipeline ของ SharePoint หรือ ElasticSearch

หากเจออุปสรรคหรือค้นพบวิธีปรับแต่งที่ฉลาด, อย่าลังเลที่จะแสดงความคิดเห็น. Happy coding, และสนุกกับ PDF ที่ค้นหาได้ทันที!

![สร้างแผนภาพการไหลของ PDF ที่ค้นหาได้แสดง OCR engine → การตั้งค่าภาษา → ตัวเลือกการบันทึก PDF → ผลลัพธ์ PDF ที่ค้นหาได้](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
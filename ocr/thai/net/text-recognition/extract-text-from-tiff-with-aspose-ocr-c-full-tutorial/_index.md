---
category: general
date: 2026-01-09
description: ดึงข้อความจากไฟล์ TIFF ด้วย Aspose OCR ใน C#. เรียนรู้วิธีการรับ 50 ตัวอักษรแรกของแต่ละผลลัพธ์ในบทแนะนำขั้นตอนต่อขั้นตอนนี้.
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: th
og_description: ดึงข้อความจากไฟล์ TIFF ด้วย Aspose OCR ใน C# คู่มือนี้แสดงวิธีรับ
  50 ตัวอักษรแรกของผลลัพธ์ OCR แต่ละรายการ ทีละขั้นตอน
og_title: สกัดข้อความจากไฟล์ TIFF ด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
tags:
- Aspose OCR
- C#
- TIFF processing
title: สกัดข้อความจากไฟล์ TIFF ด้วย Aspose OCR C# – คู่มือเต็ม
url: /th/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจาก TIFF – การสอน Aspose OCR C# อย่างสมบูรณ์

เคยต้อง **ดึงข้อความจากภาพ TIFF** แต่ไม่แน่ใจว่าจะใช้ไลบรารีไหน? คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อต้องดึงข้อความที่ค้นหาได้จาก TIFF หลายหน้า โดยเฉพาะเมื่อประสิทธิภาพเป็นสิ่งสำคัญ

ใน **aspose ocr c# tutorial** นี้ เราจะพาคุณผ่านตัวอย่างที่พร้อมรันซึ่งไม่เพียงดึงข้อความทั้งหมด แต่ยังแสดงวิธี **ดึงอักขระ 50 ตัวแรก** ของแต่ละหน้าเพื่อเป็นตัวอย่างอย่างรวดเร็ว เมื่อเสร็จแล้วคุณจะมีโปรแกรมที่สามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้

## สิ่งที่คุณต้องมี

- .NET 6 (หรือเวอร์ชัน .NET ล่าสุด) – โค้ดสามารถคอมไพล์ได้ทั้งบน .NET Core และ .NET Framework  
- ไลเซนส์ Aspose.OCR for .NET ที่ใช้งานได้ (คุณสามารถเริ่มต้นด้วยการทดลองฟรี)  
- โฟลเดอร์ที่มีไฟล์ `.tif` หนึ่งไฟล์หรือหลายไฟล์ที่ต้องการประมวลผล  
- Visual Studio, VS Code หรือ IDE ใดก็ได้ที่คุณชอบ – ตัวอย่างเป็น C# ธรรมดา ไม่จำกัดเครื่องมือแก้ไข

> **Pro tip:** หากคุณทำงานบนเซิร์ฟเวอร์ CI ให้เพิ่มแพคเกจ NuGet ของ Aspose.OCR (`Aspose.OCR`) ลงในไฟล์โปรเจกต์ของคุณ; ไลบรารีเป็นแบบจัดการเต็มรูปแบบและไม่มีการพึ่งพาเนทีฟ

## ขั้นตอนที่ 1: ติดตั้งแพคเกจ NuGet ของ Aspose OCR

เริ่มต้นด้วยการนำเอาเอนจิน OCR เข้ามาในโปรเจกต์ เปิดเทอร์มินัลในโฟลเดอร์โซลูชันของคุณและรัน:

```bash
dotnet add package Aspose.OCR
```

คำสั่งนี้จะดึงเวอร์ชันเสถียรล่าสุด (ณ มกราคม 2026 คือ 23.9) และอัปเดตไฟล์ `.csproj` ของคุณโดยอัตโนมัติ ไม่ต้องจัดการ DLL ด้วยตนเอง

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine

ต่อไปเราจะสร้างอินสแตนซ์ของ `OcrEngine` คิดว่าเป็น “สมอง” ที่จะอ่านทุกหน้า TIFF

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

ทำไมต้องสร้างอินสแตนซ์เพียงครั้งเดียว? เพราะ `RecognizeImages` สามารถรับคอลเลกชันของเส้นทางไฟล์ ทำให้เอนจินใช้บัฟเฟอร์ภายในซ้ำได้และเร่งความเร็วการประมวลผลแบบแบตช์อย่างมาก

## ขั้นตอนที่ 3: รวบรวมไฟล์ TIFF ทั้งหมดในหนึ่งคำสั่ง

แทนที่จะวนลูปอ่านโฟลเดอร์ด้วยตนเอง เราจะให้ .NET ทำงานหนักให้ `Directory.GetFiles` จะคืนค่า `IEnumerable<string>` ที่เราสามารถส่งตรงไปยังคำสั่ง OCR ได้

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **ถ้าภาพของฉันเป็น JPEG หรือ PNG?** เพียงเปลี่ยนรูปแบบการค้นหา (`"*.jpg"` หรือ `"*.*"`). Aspose OCR รองรับรูปแบบเรสเตอร์ทั่วไปทั้งหมด

## ขั้นตอนที่ 4: รัน OCR บนคอลเลกชันทั้งหมด

นี่คือบรรทัดสำคัญที่ประมวลผลทุกไฟล์ในคำขอเดียว วิธีนี้จะคืนพจนานุกรมที่คีย์คือเส้นทางไฟล์และค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความที่ได้รับการจดจำ

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

ทำไมต้องประมวลผลแบบแบตช์? เพื่อลดค่าโอเวอร์เฮดจากการโหลดเอนจิน OCR ซ้ำ ๆ และบนเครื่องหลายคอร์ Aspose จะทำงานแบบขนานภายในโดยอัตโนมัติ ทำให้คุณเห็นการเพิ่มความเร็วอย่างชัดเจน

## ขั้นตอนที่ 5: แสดงตัวอย่าง – ดึงอักขระ 50 ตัวแรก

หลายกรณี UI ต้องการเพียงส่วนสั้น ๆ ไม่ใช่เอกสารเต็ม เราจะดึงอักขระ 50 ตัวแรก (หรือจำนวนน้อยกว่า หากหน้าสั้น) แล้วพิมพ์พร้อมชื่อไฟล์

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

บรรทัด `Math.Min(50, fullText.Length)` รับประกันว่าเราไม่เกินขอบเขตของสตริง – เป็นการป้องกันเล็ก ๆ ที่หลีกเลี่ยง `ArgumentOutOfRangeException` เมื่อผลลัพธ์ OCR สั้นกว่า 50 ตัวอักษร

### ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล

สมมติว่าคุณมีไฟล์ TIFF สองไฟล์ (`invoice1.tif` และ `receipt2.tif`) คอนโซลอาจแสดงดังนี้:

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

แต่ละบรรทัดลงท้ายด้วยจุดไข่ปลา (`...`) เพื่อบ่งบอกว่าตัวอย่างเป็นเพียงส่วนเริ่มต้นของข้อความที่ยาวกว่า

## ขั้นตอนที่ 6: จัดการกับกรณีขอบและข้อผิดพลาดทั่วไป

### ไฟล์ว่างหรือเสียหาย

หากไฟล์ไม่สามารถอ่านได้ `RecognizeImages` ยังจะคืนรายการที่มีคุณสมบัติ `Text` ว่างเปล่า คุณสามารถกรองรายการเหล่านี้ออกได้:

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### แบตช์ขนาดใหญ่

การประมวลผลหลายพันไฟล์ TIFF อาจใช้หน่วยความจำมาก ในกรณีเช่นนี้ให้ใช้ overload ที่รับ `Stream` ต่อภาพหนึ่งไฟล์ หรือแบ่งรายการเป็นชิ้นย่อย ๆ:

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### การสนับสนุนภาษาและฟอนต์

หากเอกสารของคุณมีอักขระที่ไม่ใช่ละติน ให้ตั้งค่าภาษา ก่อนเรียก `RecognizeImages`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

การปรับเล็ก ๆ นี้สามารถเพิ่มความแม่นยำได้อย่างมาก

## ขั้นตอนที่ 7: ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถวางลงในโปรเจกต์คอนโซลใหม่ (`dotnet new console`) แล้วรันได้ทันที (เพียงเปลี่ยน `YOUR_DIRECTORY/Batch` เป็นเส้นทางจริง)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

รันโปรแกรมด้วย `dotnet run`. คุณควรเห็นตัวอย่างสั้น ๆ สำหรับแต่ละไฟล์ TIFF ยืนยันว่าคุณได้ **ดึงข้อความจาก TIFF** ด้วย Aspose OCR อย่างสำเร็จ

## คำถามที่พบบ่อย (FAQ)

**Q: ทำงานกับ TIFF หลายหน้าได้หรือไม่?**  
A: ได้. Aspose OCR จะจัดการแต่ละหน้าเป็นภาพแยกภายใน ดังนั้น TIFF หลายหน้าจะให้สตริงที่ต่อเนื่องต่อไฟล์เดียว คุณสามารถแยกส่วนต่อไปได้หากต้องการ

**Q: ความแม่นยำของ OCR มีระดับเท่าไหร่โดยไม่ต้องปรับแต่ง?**  
A: สำหรับสแกนที่คมชัดและความละเอียดสูง (300 DPI หรือมากกว่า) คุณสามารถคาดหวังความแม่นยำ >95 % สำหรับข้อความภาษาอังกฤษ การทำพรี‑โปรเซส (deskew, binarization) สามารถทำให้แม่นยำยิ่งขึ้น

**Q: สามารถส่งออกผลลัพธ์เป็นไฟล์ CSV ได้หรือไม่?**  
A: แน่นอน. แทนที่ `Console.WriteLine` ด้วย `StreamWriter` แล้วเขียนแถว `fileName,preview`. อย่าลืมหลบคอมม่าในข้อความตัวอย่าง

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

- **บันทึกผลลัพธ์ OCR** – เก็บข้อความเต็มในฐานข้อมูลเพื่อทำคลังข้อมูลที่ค้นหาได้  
- **รวมกับการแปลง PDF** – ใช้ Aspose.PDF เพื่อฝังข้อความที่ดึงได้กลับเข้า PDF ที่ค้นหาได้  
- **ประมวลผลแบตช์บน Azure Functions** – ขยายการทำงาน OCR โดยไม่ต้องจัดการเซิร์ฟเวอร์  

ส่วนขยายทั้งหมดนี้เชื่อมโยงกลับไปยังแนวคิดหลักของการ **ดึงข้อความจาก TIFF** อย่างมีประสิทธิภาพ พร้อมให้คุณ **ดึงอักขระ 50 ตัวแรก** เพื่อแสดงตัวอย่าง UI อย่างรวดเร็ว

---

*ขอให้สนุกกับการเขียนโค้ด! หากเจอปัญหาใด ๆ คอมเมนต์ด้านล่าง – ฉันจะพยายามช่วยคุณปรับแต่ง pipeline ของ OCR ให้ดีที่สุด* 

![ดึงข้อความจาก TIFF ด้วย Aspose OCR](https://example.com/images/extract-text-from-tiff.png "ดึงข้อความจาก TIFF ด้วย Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-07
description: ดึงข้อความจากไฟล์ PNG ด้วย C# เรียนรู้วิธีแปลงภาพเป็นข้อความด้วย C# และอ่านข้อความจากภาพสแกนได้อย่างรวดเร็ว
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: th
og_description: ดึงข้อความจากไฟล์ PNG ด้วย C#. คู่มือนี้แสดงวิธีแปลงภาพเป็นข้อความด้วย
  C# และอ่านข้อความจากภาพสแกนด้วย Aspose OCR.
og_title: สกัดข้อความจากไฟล์ PNG ด้วย C# – คู่มือ OCR ฉบับเต็ม
tags:
- OCR
- C#
- Aspose
- Image Processing
title: ดึงข้อความจาก PNG ด้วย C# – คู่มือ OCR แบบเต็ม
url: /th/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจาก PNG ใน C# – คู่มือ OCR ฉบับเต็ม

เคยต้องการ **extract text from PNG** ไฟล์แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาส่วนใหญ่เคยเจออุปสรรคนี้เมื่อต้องเผชิญกับกราฟิกที่สแกนหรือภาพหน้าจอที่ต้องการแปลงเป็นข้อความที่ค้นหาได้ ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# และ Aspose OCR คุณสามารถเปลี่ยน PNG ใดก็ได้เป็นสตริงที่แก้ไขได้ในพริบตา

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งแต่การค้นหา PNG บนดิสก์, การเปิดใช้งานงาน OCR แบบขนาน, ไปจนถึงการแสดงตัวอย่างที่เรียบร้อยของแต่ละผลลัพธ์. เมื่อเสร็จคุณจะรู้วิธี **convert image to text C#** แบบ, คุณจะสามารถ **read text from scanned images** อย่างมีประสิทธิภาพ, และคุณยังจะเห็นวิธีที่ดีที่สุดในการ **run OCR on images** โดยไม่ทำให้ UI thread ของคุณพัง

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานบน .NET Core และ .NET Framework ด้วยเช่นกัน)  
- แพ็กเกจ NuGet ของ Aspose.OCR (`Install-Package Aspose.OCR`)  
- โฟลเดอร์ที่เต็มไปด้วยไฟล์ *.png* ที่คุณต้องการประมวลผล  
- IDE ใดก็ได้ที่คุณชอบ (Visual Studio, VS Code, Rider…)

ไม่จำเป็นต้องกำหนดค่าเพิ่มเติม; ไลบรารีมาพร้อมกับทุกอย่างที่จำเป็นสำหรับการถอดรหัส PNG, JPEG, TIFF, หรืออะไรก็ตามที่คุณต้องการ

## ขั้นตอนที่ 1: ค้นหาไฟล์ PNG ทั้งหมด – เริ่ม “Extract Text from PNG”

ก่อนอื่นเราต้องค้นหา PNG ทุกไฟล์ที่เราตั้งใจจะทำ OCR. การใช้ `Directory.GetFiles` เป็นวิธีที่รวดเร็วและเชื่อถือได้.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*ทำไมเรื่องนี้ถึงสำคัญ:* การสแกนไดเรกทอรีครั้งเดียวทำให้ส่วนที่เหลือของ pipeline ง่ายขึ้น, และการตรวจสอบตั้งแต่ต้นป้องกันสถานการณ์ “no‑output” ที่เงียบซึ่งอาจแก้ไขได้ยากในภายหลัง.

## ขั้นตอนที่ 2: สร้างงาน OCR แบบขนาน – อย่างมีประสิทธิภาพ **run OCR on images**

การทำ OCR อย่างต่อเนื่องนั้นเหมาะสำหรับไฟล์จำนวนไม่มาก, แต่โครงการในโลกจริงมักต้องจัดการกับหลายสิบหรือหลายร้อยไฟล์. โดยการเปิด `Task` ต่อภาพ เราจะทำให้ CPU ทำงานอย่างเต็มที่ในขณะที่ไลบรารีทำงานหนักของมัน.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*เคล็ดลับ:* `Task.Run` ย้ายงานไปยัง thread pool, ซึ่งหมายความว่า UI ของคุณ (หากมี) จะตอบสนองได้. หากคุณอยู่บนเซิร์ฟเวอร์, รูปแบบเดียวกันจะขยายได้ดีบนหลายคอร์.

## ขั้นตอนที่ 3: รอทุก Task – รวบรวมผลลัพธ์

ตอนนี้เรารอให้ทุกการทำ OCR เสร็จสิ้น. `Task.WhenAll` ส่งกลับอาเรย์ที่เรียงตามลำดับไฟล์เดิม, ทำให้จับคู่ผลลัพธ์กับชื่อไฟล์ได้ง่าย.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*หมายเหตุกรณีขอบ:* หากภาพใดภาพหนึ่งทำให้เกิดข้อผิดพลาด (ไฟล์เสีย, ฟอร์แมตที่ไม่รองรับ) `WhenAll` ทั้งหมดจะส่งต่อข้อยกเว้น. คุณสามารถห่อ `Task.Run` ภายในด้วย try/catch และคืนค่าเป็นสตริงว่างหรือข้อความวินิจฉัยหากต้องการความทนทานต่อข้อผิดพลาด.

## ขั้นตอนที่ 4: แสดงตัวอย่าง – ตรวจสอบผลลัพธ์ **convert image to text C#**

การแสดงตัวอย่างอย่างรวดเร็วช่วยให้คุณยืนยันว่า OCR ทำงานได้ก่อนที่คุณจะเริ่มบันทึกข้อมูลที่อื่น.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

ผลลัพธ์คอนโซลทั่วไปจะเป็นเช่นนี้:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

หากตัวอย่างแสดงข้อความไร้สาระ, ตรวจสอบคุณภาพของภาพอีกครั้งหรือพิจารณาการประมวลผลล่วงหน้า (เช่น การทำไบนารี) – แต่สำหรับ PNG ที่สะอาดส่วนใหญ่ Aspose OCR จะทำได้ถูกต้องตั้งแต่ครั้งแรก.

## ตัวเลือก: บันทึกผลลัพธ์เป็น CSV – กรณีใช้งานจริง

โครงการส่วนใหญ่ต้องการข้อความที่ดึงออกมาในรูปแบบโครงสร้าง. ด้านล่างเป็นตัวช่วยขนาดเล็กที่เขียนชื่อไฟล์และข้อความ OCR ทั้งหมดลงในไฟล์ CSV.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

ตอนนี้คุณสามารถนำเข้า CSV ไปยัง Excel, Power BI, หรือระบบ downstream ใด ๆ ที่คาดหวัง **read text from scanned images**.

## คำถามที่พบบ่อย

**ถ้า PNG ของฉันมีขนาดใหญ่ (เกิน 5 MB) จะทำอย่างไร?**  
Aspose OCR จะทำการ down‑sample ภาพขนาดใหญ่โดยอัตโนมัติเพื่อให้การใช้หน่วยความจำอยู่ในระดับที่เหมาะสม, แต่คุณสามารถปรับขนาดด้วยตนเองโดยใช้ `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` เพื่อจำกัดความกว้างที่ 2000 px พร้อมคงอัตราส่วน.

**ฉันสามารถรันนี้บน Linux ได้หรือไม่?**  
ได้. Aspose OCR เป็นแบบข้ามแพลตฟอร์ม; เพียงตรวจสอบให้แน่ใจว่าติดตั้ง dependencies เนทีฟ (`libgdiplus` บนบางดิสโทร) แล้ว.

**ภาษาของ OCR ตั้งค่าเป็นอังกฤษโดยค่าเริ่มต้นหรือไม่?**  
ถูกต้อง. หากคุณต้องการภาษาอื่น, ตั้งค่า `engine.Language = OcrLanguage.French;` (หรือ enum ที่รองรับใด ๆ) ก่อนเรียก `Recognize()`.

**ฉันจะจัดการกับ PDF ที่ป้องกันด้วยรหัสผ่านและมี PNG อย่างไร?**  
แปลงหน้าของ PDF เป็นภาพก่อน (โดยใช้ Aspose PDF หรือไลบรารีอื่น), จากนั้นส่ง PNG เหล่านั้นเข้าสู่ pipeline เดียวกัน. หลักการของ **how to run OCR on images** ยังคงเหมือนเดิม.

## ตัวอย่างทำงานเต็ม (Async Main)

ด้านล่างเป็นโปรแกรมแบบ self‑contained ที่คุณสามารถคัดลอกและวางลงในโปรเจกต์คอนโซล. มันรวมทุกส่วนที่กล่าวมาข้างต้น, พร้อมตัวช่วยขนาดเล็กเพื่อยืนยันโฟลเดอร์อินพุต.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่างสำหรับ PNG สองไฟล์):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **extract text from PNG** ไฟล์โดยใช้ C#. ตั้งแต่การค้นหาไฟล์, การเปิดงาน OCR แบบขนาน, การแสดงตัวอย่างสตริง, จนถึงการบันทึกลง CSV—คู่มือนี้ให้รูปแบบพร้อมใช้งานในผลิตภัณฑ์สำหรับสถานการณ์ **convert image to text C#**.  

หากคุณพร้อมสำหรับขั้นตอนต่อไป, ลองป้อนไฟล์ JPEG หรือ TIFF ผ่าน pipeline เดียวกัน, ทดลองใช้ภาษาต่าง ๆ ของ OCR, หรือเชื่อมผลลัพธ์เข้ากับดัชนีการค้นหาเพื่อที่คุณจะสามารถ **read text from scanned images** ได้ทันที.  

มีคำถามเกี่ยวกับกรณีขอบ, การปรับประสิทธิภาพ, หรือการให้สิทธิ์ใช้งาน? แสดงความคิดเห็นหรือทักคอมมูนิตี้ของ Aspose — โค้ดให้สนุก!  

![Extract text from PNG example](extract-text-png.png "Extract text from PNG using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
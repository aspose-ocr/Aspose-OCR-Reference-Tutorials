---
category: general
date: 2026-03-21
description: เรียนรู้วิธีแก้ไขการเอียงของไฟล์ภาพและจดจำข้อความในภาพด้วย Aspose OCR.
  แปลง jpg เป็นข้อความและแก้ไขการหมุนของภาพด้วยโค้ด C# เพียงไม่กี่บรรทัด.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: th
og_description: วิธีแก้ไขการเอียงของภาพและดึงข้อความจากไฟล์ JPEG ด้วย Aspose OCR.
  ปฏิบัติตามคำแนะนำขั้นตอนต่อขั้นตอนนี้เพื่อแปลง JPG เป็นข้อความและแก้ไขการหมุนของภาพ.
og_title: วิธีทำให้ภาพตรงใน C# – บทเรียน Aspose OCR อย่างรวดเร็ว
tags:
- OCR
- C#
- Aspose
title: วิธีทำให้ภาพตรงใน C# – คู่มือฉบับสมบูรณ์โดยใช้ Aspose OCR
url: /th/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพใน C# – คู่มือฉบับสมบูรณ์โดยใช้ Aspose OCR

เคยสงสัยไหมว่า **how to deskew image** ไฟล์ที่สแกนออกมามีมุมเอียงแปลก ๆ? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจอปัญหานี้เมื่อพยายามดึงข้อความจากใบเสร็จ, ใบแจ้งหนี้, หรือบันทึกมือ. ข่าวดีคือด้วย Aspose OCR คุณสามารถแก้ไขการหมุนของภาพและดึงข้อความที่สะอาดและค้นหาได้ในเพียงไม่กี่บรรทัด.

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งแต่การติดตั้งไลบรารี, การเปิดใช้งานการแก้ไขการเอียงอัตโนมัติ, การจดจำภาพข้อความและสุดท้ายการแปลง JPG เป็นข้อความ. เมื่อจบคุณจะมีแอปคอนโซลที่พร้อมรันซึ่งสามารถ **recognize text jpg** ไฟล์ได้โดยไม่ต้องหมุนภาพด้วยตนเองก่อน.

## สิ่งที่คุณต้องการ

- **.NET 6.0** หรือใหม่กว่า (โค้ดทำงานได้บน .NET Core และ .NET Framework ทั้งสอง)  
- **Aspose.OCR for .NET** NuGet package – แนะนำให้ใช้เวอร์ชัน 23.12 หรือใหม่กว่า  
- ตัวอย่าง **skewed JPEG** (เช่น `skewed_receipt.jpg`) ที่วางไว้ในตำแหน่งที่แอปของคุณสามารถอ่านได้  
- Visual Studio, VS Code, หรือเครื่องมือแก้ไข C# ใด ๆ ที่คุณชอบ  

ไม่จำเป็นต้องใช้เครื่องมือของบุคคลที่สามอื่นใด. ไลบรารีจัดการการแก้ไขการเอียง, OCR, และแม้กระทั่งการตรวจจับภาษาโดยอัตโนมัติ.

![how to deskew image example](/images/deskew-example.png "how to deskew image using Aspose OCR")

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และติดตั้ง Aspose.OCR

เพื่อให้เป็นระเบียบ เริ่มโปรเจกต์คอนโซลใหม่:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

`dotnet add package` จะดึงไบนารีของ **Aspose.OCR** พร้อมกับการพึ่งพาเนทีฟทั้งหมด. หากคุณใช้ Windows คุณจะได้รับ DLL เนทีฟโดยอัตโนมัติ; บน Linux/macOS คุณอาจต้องติดตั้งแพคเกจ `libgdiplus` ซึ่งเป็นการติดตั้งเพียงครั้งเดียว.

## ขั้นตอนที่ 2: เปิดใช้งานการแก้ไขการเอียงอัตโนมัติ (Correct Image Rotation)

ตอนนี้เปิดไฟล์ `Program.cs` และแทนที่เนื้อหาด้วยโค้ดด้านล่าง. บรรทัดสำคัญคือ `ocrEngine.Settings.Deskew = true;` – นี่คือแฟล็กที่บอกให้เอนจิน **how to deskew image** โดยอัตโนมัติ.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### ทำไมต้องเปิดใช้งาน Deskew?

เมื่อสแกนเนอร์ป้อนหน้าที่มีมุมเอียง เส้นฐานของข้อความก็จะเอียง. เครื่อง OCR แบบดั้งเดิมจะอ่านแต่ละอักขระเป็นเวอร์ชันที่เอียง ทำให้ความแม่นยำลดลงอย่างมาก. โดยการตั้งค่า `Deskew = true` Aspose OCR จะทำการแปลง Hough‑transform อย่างรวดเร็วภายใน, หมุนบิตแมพกลับเป็นแนวนอน, แล้วทำการจดจำ. ผลลัพธ์เทียบเท่ากับการที่คุณหมุนภาพใน Photoshop ด้วยตนเอง—แต่เร็วกว่าและอัตโนมัติเต็มรูปแบบ.

## ขั้นตอนที่ 3: จดจำภาพข้อความและแปลง JPG เป็นข้อความ

`Recognize` ทำสองอย่างพร้อมกัน:

1. **Deskews** ภาพ (เพราะเราเปิดแฟล็กนี้).  
2. **Extracts** เนื้อหาข้อความ, ส่งกลับในอ็อบเจ็กต์ `OcrResult`.

คุณสามารถใช้ `ocrResult.Text` เป็นสตริงธรรมดา, เขียนลงไฟล์, หรือส่งต่อไปยัง pipeline การประมวลผลต่อไป. หากคุณต้องการคะแนนความเชื่อมั่นแบบดิบต่อคำ, `ocrResult.Words` จะให้คอลเลกชันที่มีค่า `Confidence`.

### ตัวอย่างผลลัพธ์

สมมติว่า `skewed_receipt.jpg` มีใบเสร็จง่าย ๆ คุณอาจเห็นผลลัพธ์ประมาณนี้:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

สังเกตว่าตัวเลขจัดเรียงอย่างสวยงามแม้ว่าภาพต้นฉบับจะถูกหมุนประมาณ 7°. นั่นคือความมหัศจรรย์ของ **correct image rotation** ที่ฝังอยู่ในไลบรารี.

## ขั้นตอนที่ 4: รันตัวอย่างและตรวจสอบผลลัพธ์

คอมไพล์และรัน:

```bash
dotnet run
```

หากทุกอย่างเชื่อมต่อถูกต้อง คุณจะเห็นข้อความที่ดึงออกมาพิมพ์บนคอนโซล. หากเกิดข้อยกเว้นเช่น `FileNotFoundException` ให้ตรวจสอบเส้นทางไปยังไฟล์ JPEG ของคุณและตรวจสอบว่าไฟล์สามารถอ่านได้.

### ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

- **Large Images** – การใช้หน่วยความจำของ OCR เพิ่มขึ้นตามขนาดภาพ. ควรปรับขนาดไฟล์ที่ใหญ่เกินไป (เช่น ความกว้าง > 3000 px) ก่อนส่งให้เอนจิน.  
- **Non‑Latin Scripts** – โดยค่าเริ่มต้นเอนจินสมมติว่าเป็นภาษาอังกฤษ. ตั้งค่า `ocrEngine.Settings.Language = OcrLanguage.French;` (หรือภาษาอื่นที่รองรับ) หากคุณต้องการ **recognize text image** ในอักษรอื่น.  
- **Batch Processing** – สำหรับไฟล์จำนวนมาก, ใช้ instance ของ `OcrEngine` เดียวกันซ้ำ; การสร้างเอนจินใหม่ต่อไฟล์จะทำให้เกิดภาระที่ไม่จำเป็น.  
- **Quality Check** – หลังจากทำ Deskew คุณสามารถส่งออกบิตแมพที่แก้ไขแล้วผ่าน `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` เพื่อยืนยันการแก้ไขการหมุนแบบเห็นภาพ.

## ตัวอย่างทำงานเต็มรูปแบบ (ทั้งหมดรวมกัน)

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และเป็นอิสระที่คุณสามารถคัดลอกและวางลงใน `Program.cs`. มันรวมคอมเมนต์, การจัดการข้อผิดพลาด, และขั้นตอนเสริมเพื่อบันทึกภาพที่ทำ Deskew แล้ว.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

การรันโปรแกรมจะ **recognize text jpg** ไฟล์, แก้ไขการเอียงโดยอัตโนมัติ, และพิมพ์ข้อความที่สะอาดและค้นหาได้บนคอนโซล.

## สรุป

ตอนนี้คุณมีโค้ดสแนปที่มั่นคงและพร้อมใช้งานในผลิตภัณฑ์ซึ่งแสดง **how to deskew image** ไฟล์และดึงเนื้อหาของมันโดยใช้ Aspose OCR. วิธีนี้ทำงานได้กับใบเสร็จ, ใบแจ้งหนี้, สัญญาที่สแกน, หรือ JPEG ใด ๆ ที่ข้อความไม่อยู่ในแนวนอนอย่างสมบูรณ์.

ขั้นตอนต่อไปที่คุณอาจสำรวจ:

- **Batch processing** ของโฟลเดอร์ JPEG และเขียนผลลัพธ์แต่ละไฟล์เป็นไฟล์ `.txt` (เชื่อมโยงกับ *convert jpg to text*).  
- การรวมขั้นตอน OCR เข้าใน ASP.NET Core API เพื่อให้ลูกค้าสามารถอัปโหลดภาพและรับข้อความในรูปแบบ JSON.  
- ทดลองใช้การตั้งค่า OCR ต่าง ๆ เช่น `ocrEngine.Settings.Language` หรือ `ocrEngine.Settings.RecognitionMode` เพื่อปรับปรุงความแม่นยำสำหรับเอกสารที่ไม่ใช่ภาษาอังกฤษ.

ลองใช้งาน, ปรับแต่งการตั้งค่า, และให้เอนจินทำงานหนักแทนคุณ. อย่างเช่นเคย, หากคุณเจอปัญหาหรือมีการปรับปรุงที่ฉลาดอยากแบ่งปัน, ฝากคอมเมนต์ด้านล่าง. โค้ดสนุก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
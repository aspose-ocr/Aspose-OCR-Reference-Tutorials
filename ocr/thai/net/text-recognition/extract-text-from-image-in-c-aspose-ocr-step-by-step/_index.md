---
category: general
date: 2026-03-05
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# เรียนรู้วิธีอ่านไฟล์ภาพใน C#
  แปลง DJVU เป็นข้อความ และรับผลลัพธ์ OCR จากภาพเป็นสตริงอย่างรวดเร็ว
draft: false
keywords:
- extract text from image
- read image file c#
- convert djvu to text
- ocr image to string
- recognize text from djvu
language: th
og_description: ดึงข้อความจากรูปภาพด้วย Aspose OCR ใน C# คู่มือนี้แสดงวิธีอ่านไฟล์รูปภาพใน
  C# แปลง DJVU เป็นข้อความ และจัดการ OCR รูปภาพเป็นสตริงอย่างง่ายดาย.
og_title: ดึงข้อความจากรูปภาพใน C# – คู่มือ Aspose OCR ฉบับสมบูรณ์
tags:
- Aspose OCR
- C#
- Image Processing
title: ดึงข้อความจากรูปภาพใน C# – ขั้นตอนการใช้ Aspose OCR
url: /th/net/text-recognition/extract-text-from-image-in-c-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพใน C# – คู่มือ Aspose OCR ฉบับสมบูรณ์

เคยต้องการ **extract text from image** แต่ไม่แน่ใจว่าห้องสมุดใดจะให้ผลลัพธ์ที่เชื่อถือได้? บางทีคุณอาจมีชุดสแกน DJVU จำนวนมากและต้องการข้อความธรรมดาโดยไม่ต้องยุ่งกับเครื่องมือของบุคคลที่สาม ในบทแนะนำนี้เราจะแก้ปัญหานั้นในไม่กี่นาทีโดยใช้ Aspose OCR สำหรับ .NET.  

เราจะอธิบายขั้นตอนการอ่านไฟล์รูปภาพใน C#, การแปลงเอกสาร DJVU เป็นข้อความ, และการแปลงภาพ OCR ใด ๆ ให้เป็นสตริงที่สะอาด สุดท้ายคุณจะได้แอปคอนโซลพร้อมใช้งานที่พิมพ์ข้อความที่ได้รับการจดจำออกทางคอนโซล ไม่ต้องอ้างอิง “ดูเอกสาร” ที่คลุมเครือ—เพียงโซลูชันที่สมบูรณ์พร้อมคัดลอกและวาง.

## สิ่งที่คุณต้องเตรียม

- **.NET 6.0** หรือใหม่กว่า (โค้ดทำงานบน .NET Framework 4.6+ ด้วย)  
- **Aspose.OCR for .NET** แพคเกจ NuGet (ไลเซนส์ทดลองฟรีใช้สำหรับการทดสอบ)  
- ไฟล์ DJVU หรือรูปภาพที่รองรับใด ๆ (PNG, JPEG, BMP, เป็นต้น)  
- Visual Studio, Rider หรือโปรแกรมแก้ไขที่คุณชื่นชอบ  

หากคุณขาดสิ่งใดสิ่งหนึ่ง เพียงติดตั้งแพคเกจ NuGet:

```bash
dotnet add package Aspose.OCR
```

เท่านี้ก็พร้อมตั้งค่าแล้ว. มาเริ่มกันเลย.

## ขั้นตอนที่ 1: เริ่มต้น OCR Engine – extract text from image

สิ่งแรกที่คุณทำคือสร้างอินสแตนซ์ของ `OcrEngine`. คิดว่ามันเป็นสมองที่อ่านพิกเซลและแปลงเป็นอักขระ.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

ทำไมเราถึงสร้างอินสแตนซ์ของเอนจิน *ก่อน* โหลดไฟล์? การออกแบบของ Aspose แยกการกำหนดค่า (เช่น ไลเซนส์) ออกจากข้อมูลภาพจริง ทำให้คุณสามารถใช้เอนจินเดียวกันสำหรับหลายไฟล์โดยไม่ต้องสร้างอ็อบเจ็กต์ใหม่—เป็นการเพิ่มประสิทธิภาพเล็กน้อย.

## ขั้นตอนที่ 2: ใส่ไลเซนส์ Aspose OCR ของคุณ (ไม่บังคับแต่แนะนำ)

หากคุณมีไลเซนส์เชิงพาณิชย์ ให้ตั้งค่าเดี๋ยวนี้ การข้ามขั้นตอนนี้จะทำให้เข้าสู่โหมดสาธิต ซึ่งจะเพิ่มลายน้ำในผลลัพธ์และจำกัดจำนวนหน้า.

```csharp
        // Apply license – remove this line if you’re using the free trial
        ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Pro tip:** เก็บไฟล์ไลเซนส์ไว้ด้านนอกระบบควบคุมเวอร์ชัน (เช่น ใน environment variable) เพื่อหลีกเลี่ยงการคอมมิตโดยบังเอิญ.

## ขั้นตอนที่ 3: โหลดภาพ – read image file c# made easy

Aspose สามารถอ่านหลายรูปแบบ รวมถึง DJVU ที่หายาก เราจะใช้ตัวช่วย `ImageStream.FromFile` เพื่อโหลดไฟล์เข้าสู่เอนจิน.

```csharp
        // Load the image (DJVU, PNG, JPEG, etc.)
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.djvu");
```

หากคุณต้องการทำงานกับ `byte[]` (เช่น เมื่อภาพมาจากฐานข้อมูล) คุณสามารถใช้ `ImageStream.FromBytes(byteArray)` แทนได้ ความยืดหยุ่นนี้มีประโยชน์เมื่อคุณต้อง **read image file C#** จากสตรีมแทนดิสก์.

## ขั้นตอนที่ 4: ทำ OCR – ocr image to string in a single call

ตอนนี้จุดมหัศจรรย์เกิดขึ้น การเรียก `Recognize()` จะรัน OCR engine และคืนค่า `RecognitionResult` ที่มีข้อความที่ดึงออกมา, คะแนนความมั่นใจ, และข้อมูลอื่น ๆ

```csharp
        // Run OCR and get the result
        var result = ocrEngine.Recognize();

        // Extract plain text
        string recognizedText = result.Text;
```

ทำไมไม่เรียก `Recognize().Text` ตรง ๆ? การแยกการเรียกทำให้คุณสามารถตรวจสอบ `result.Confidence` หรือ `result.Regions` หากต้องการข้อมูลละเอียดในภายหลัง—มีประโยชน์สำหรับการดีบักหรือสร้าง UI ที่ไฮไลท์คำที่ความมั่นใจต่ำ.

## ขั้นตอนที่ 5: แสดงข้อความที่ดึงออก – ผลลัพธ์สุดท้ายของคุณ

สุดท้าย เขียนข้อความไปยังคอนโซล ในแอปพลิเคชันจริงคุณอาจเขียนไปยังไฟล์, ฐานข้อมูล, หรือส่งผ่าน API.

```csharp
        // Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Expected output** (ตัดทอนเพื่อความกระชับ):

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

หาก OCR engine ไม่สามารถจดจำอักขระใด ๆ ได้ `recognizedText` จะเป็นสตริงว่าง ในกรณีนั้นให้ตรวจสอบคุณภาพของภาพอีกครั้งหรือปรับการตั้งค่าภาษาของเอนจิน (เช่น `ocrEngine.Language = Language.English;`).

## การแปลง DJVU เป็นข้อความ – recognize text from djvu in bulk

คุณอาจมีไฟล์ DJVU หลายสิบไฟล์ที่ต้องประมวลผล ให้ใส่ตรรกะข้างต้นในลูป:

```csharp
string[] files = Directory.GetFiles("YOUR_DIRECTORY", "*.djvu");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string text = ocrEngine.Recognize().Text;
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Converted {Path.GetFileName(file)} → {Path.GetFileNameWithoutExtension(file)}.txt");
}
```

ส่วนนี้ **converts DJVU to text** โดยอัตโนมัติ สร้างไฟล์ `.txt` ข้างเคียงกับแต่ละไฟล์ต้นฉบับ เป็นวิธีรวดเร็วในการสร้างคลังข้อมูลที่ค้นหาได้จากเอกสารสแกนเก่า.

## การจัดการกรณีขอบ – what if the image is noisy?

ความแม่นยำของ OCR ลดลงเมื่อภาพเบลอ, มีคอนทราสต์ต่ำ, หรือมีพื้นหลังสี. Aspose OCR มีตัวเลือกการเตรียมข้อมูลล่วงหน้า:

```csharp
// Example: Binarize the image to improve contrast
ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image, threshold: 128);
```

หรือคุณสามารถตั้งค่าเอนจินให้ตรวจจับภาษาด้วยตนเอง:

```csharp
ocrEngine.Language = Language.Detect; // Detects language based on content
```

การปรับแต่งเหล่านี้มักทำให้ผลลัพธ์ความแม่นยำจาก 60 % เพิ่มเป็น 95 % ลองใช้เมธอด `Threshold`, `Denoise`, หรือ `Deskew` หากพบปัญหา.

## ตัวอย่างทำงานเต็มรูปแบบ – คัดลอก, วาง, รัน

ด้านล่างเป็นโปรแกรมทั้งหมดพร้อมคอมไพล์ แทนที่ `"YOUR_DIRECTORY/input.djvu"` ด้วยพาธของไฟล์ของคุณและตรวจสอบให้แน่ใจว่าไฟล์ไลเซนส์เข้าถึงได้.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Apply license (optional)
        // ocrEngine.SetLicense("Aspose.OCR.lic"); // Uncomment if you have a license

        // 3️⃣ Load the image (DJVU, PNG, JPEG, etc.)
        string imagePath = "YOUR_DIRECTORY/input.djvu";
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 4️⃣ Perform OCR
        var result = ocrEngine.Recognize();
        string recognizedText = result.Text;

        // 5️⃣ Output the text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

รันด้วย:

```bash
dotnet run
```

คุณควรเห็นข้อความที่ดึงออกมาพิมพ์บนคอนโซล เหมือนกับตัวอย่างก่อนหน้า.

## คำถามทั่วไป & ข้อควรระวัง

- **Does this work with PDF files?**  
  ไม่ได้โดยตรง Aspose OCR จัดการกับภาพแรสเตอร์; สำหรับ PDF คุณต้องแปลงแต่ละหน้าเป็นภาพก่อน (เช่น ใช้ Aspose.PDF) แล้วจึงส่งภาพเหล่านั้นให้ OCR engine.  

- **What if I need to process a large batch on a server?**  
  สร้าง **single** `OcrEngine` แล้วใช้ซ้ำในหลายเธรด เอนจินปลอดภัยต่อเธรดสำหรับการดำเนินการแบบอ่านอย่างเดียว แต่ต้องหลีกเลี่ยงการแชร์อินสแตนซ์ `Image` เดียวกันพร้อมกัน.  

- **Can I extract formatted text (fonts, sizes)?**  
  Aspose OCR คืนค่าเป็นข้อความ Unicode ธรรมดาเท่านั้น หากต้องการสกัดข้อมูลที่คงรูปแบบคุณต้องใช้โซลูชันที่ซับซ้อนกว่า เช่น OCR‑ML หรือไลบรารี PDF ที่รักษาเลย์เอาต์.

## ขั้นตอนต่อไป – ขยายเวิร์กโฟลว์ของคุณ

ตอนนี้คุณสามารถ **extract text from image** อย่างเชื่อถือได้แล้ว ลองพิจารณา:

- เก็บผลลัพธ์ใน Elasticsearch เพื่อการค้นหาแบบเต็มข้อความ.  
- ส่งข้อความไปยังโมเดลภาษาเพื่อสรุปเนื้อหา.  
- เพิ่ม UI ง่ายด้วย ASP.NET Core เพื่ออัปโหลดไฟล์และดูผล OCR ทันที.  

ทั้งหมดนี้สร้างบนโค้ดหลักเดียวกันที่เราอธิบายไว้ ดังนั้นคุณพร้อมที่จะขยายโซลูชันต่อไป.

---

### สรุปสั้น

- เรา **initialized** `OcrEngine` (หัวใจของ Aspose OCR).  
- ใส่ **license** เพื่อเปิดฟีเจอร์เต็ม.  
- **Loaded** ไฟล์ DJVU ด้วย `ImageStream.FromFile`.  
- เรียก `Recognize()` เพื่อรับผลลัพธ์ **ocr image to string**.  
- พิมพ์ **extracted text** ไปยังคอนโซล.  

นี่คือสูตรครบถ้วนสำหรับการแปลงภาพที่รองรับใด ๆ—including DJVU—ให้เป็นข้อความที่ค้นหาได้ด้วย C#.

---

อย่าลังเลที่จะทดลองกับรูปแบบภาพต่าง ๆ ปรับการตั้งค่าการเตรียมข้อมูลล่วงหน้า หรือเชื่อมโค้ดนี้กับไลบรารี Aspose อื่น ๆ หากเจอปัญหาใด ๆ คอมเมนต์ด้านล่าง—ขอให้เขียนโค้ดสนุก!  

![ตัวอย่างการดึงข้อความจากรูปภาพ](/images/ocr-example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
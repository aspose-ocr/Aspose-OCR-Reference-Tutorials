---
category: general
date: 2026-04-03
description: จดจำข้อความจากภาพโดยใช้ Aspose OCR ใน C#. เรียนรู้การโหลดภาพสำหรับ OCR,
  แยกข้อความจากภาพ, เขียนไฟล์ JSON ด้วย C#, และทำ OCR บนไฟล์ PNG.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: th
og_description: จดจำข้อความจากรูปภาพด้วย Aspose OCR ใน C#. คู่มือแบบขั้นตอนต่อขั้นตอนในการโหลดรูปภาพเพื่อ
  OCR, ดึงข้อความจากรูปภาพ, เขียนไฟล์ JSON ด้วย C#, และทำ OCR บน PNG.
og_title: แยกข้อความจากภาพใน C# – บทเรียน OCR ของ Aspose อย่างครบถ้วน
tags:
- OCR
- C#
- Aspose
title: แยกข้อความจากภาพใน C# – คู่มือ Aspose OCR ฉบับเต็ม
url: /th/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากรูปภาพใน C# – คู่มือ Aspose OCR ฉบับสมบูรณ์

เคยต้อง **จดจำข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าจะเลือกไลบรารีใดใช่ไหม? บางทีคุณอาจมีชุดใบเสร็จสแกน, ภาพ PNG, หรือโน้ตมือเขียนที่ต้องการแปลงเป็นข้อมูลที่ค้นหาได้ ข่าวดีคือ: ด้วย Aspose.OCR คุณทำได้ในไม่กี่บรรทัดของโค้ด C# และยังได้ไฟล์ JSON ที่เรียบร้อยเพื่อใช้ต่อในระบบอื่น ๆ

ในบทเรียนนี้เราจะอธิบายขั้นตอนการโหลดภาพสำหรับ OCR, ดึงข้อความจากภาพ, แปลงผลลัพธ์เป็นไฟล์ JSON, และสุดท้ายจัดการไฟล์ PNG อย่างง่ายดาย เมื่อเสร็จคุณจะมีแอปคอนโซลที่พร้อมรันซึ่ง **จดจำข้อความจากรูปภาพ** และเขียนผลลัพธ์ลงใน *output.json*.

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Framework ด้วย)
- แพ็กเกจ NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- ไฟล์ PNG (หรือรูปแบบที่รองรับ) ที่ต้องการประมวลผล
- Visual Studio, VS Code, หรือเครื่องมือแก้ไข C# ใด ๆ ที่คุณชอบ

ไม่ต้องใช้ไลบรารีของบุคคลที่สามเพิ่มเติม—เพียงแค่เอ็นจิ้น Aspose OCR และตัวแปลง `System.Text.Json` ที่มาพร้อมกับ .NET

## ขั้นตอนที่ 1: จดจำข้อความจากรูปภาพโดยใช้ Aspose OCR

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ของ `OcrEngine` ซึ่งอ็อบเจกต์นี้ทำงานหนักเบื้องหลังให้คุณ

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**ทำไมเรื่องนี้สำคัญ:** การสร้าง `OcrEngine` ครั้งเดียวแล้วนำกลับมาใช้ซ้ำจะมีประสิทธิภาพมากกว่าการสร้างเอ็นจิ้นใหม่สำหรับแต่ละไฟล์ การเรียก `RecognizeToResult` จะคืนค่าอ็อบเจกต์ `OcrResult` ที่มีข้อความที่ดึงออกมาแล้ว, คะแนนความมั่นใจ, และกรอบขอบ—พร้อมสำหรับการประมวลผลต่อไป

## ขั้นตอนที่ 2: โหลดรูปภาพสำหรับ OCR – จัดการรูปแบบต่าง ๆ

Aspose OCR สามารถอ่าน PNG, JPEG, BMP, และรูปแบบอื่น ๆ มากมาย หากคุณกำลังทำงานกับ PNG ที่มีความโปร่งใส คุณอาจต้องทำให้แบนก่อนเพื่อหลีกเลี่ยงช่องว่างที่ไม่คาดคิด

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**เคล็ดลับ:** ตรวจสอบให้แน่ใจว่าขนาดภาพอยู่ในระดับที่สมเหตุสมผล (เช่น ความกว้าง > 50 px) ภาพขนาดเล็กมากอาจทำให้เอ็นจิ้น OCR พลาดอักขระ ส่งผลให้คะแนนความมั่นใจต่ำ

## ขั้นตอนที่ 3: เขียนไฟล์ JSON ด้วย C# – ทำให้ผลลัพธ์ใช้งานได้

ตัวแปลง `System.Text.Json` มีความเร็วและเป็นส่วนหนึ่งของ .NET อยู่แล้ว แต่คุณสามารถสลับไปใช้ `Newtonsoft.Json` หากต้องการคอนเวอร์เตอร์แบบกำหนดเอง ตัวอย่างด้านบนใช้ `WriteIndented = true` อยู่แล้ว ทำให้ไฟล์ที่สร้างออกมามีรูปแบบที่มนุษย์อ่านได้ง่าย

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

การมีข้อมูล OCR ในรูปแบบ JSON ช่วยให้คุณนำเข้าไปยังฐานข้อมูล, ส่งผ่าน HTTP, หรือป้อนให้กับ pipeline ของ machine‑learning ได้อย่างง่ายดาย

## ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์ – การตรวจสอบอย่างรวดเร็ว

หลังจากโปรแกรมทำงานเสร็จ ให้เปิด `output.json` แล้วมองหา field `"Text"` หากมีสตริงที่คาดหวัง คุณได้ **ดึงข้อความจากรูปภาพ** สำเร็จแล้ว หากคะแนนความมั่นใจต่ำ ให้พิจารณาเตรียมภาพล่วงหน้า (เช่น เพิ่มความคอนทราสต์หรือใช้การแปลงเป็นไบนารี)

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

การรันคอนโซลจะพิมพ์ผลลัพธ์ประมาณนี้:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

นั่นเป็นสัญญาณที่ดีว่า OCR ทำงานตามที่คาดไว้

## ปัญหาที่พบบ่อยและกรณีขอบ

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **ผลลัพธ์เป็นค่าว่าง** | ภาพมืดเกินไปหรือใช้สีสเปซที่ไม่รองรับ | แปลงเป็นระดับสีเทา, เพิ่มความสว่าง, หรือทำให้ PNG แบน (ดูขั้นตอน 2) |
| **อักขระแปลก** | DPI ต่ำ (< 72) หรือมีสัญญาณรบกวนมาก | ขยายภาพหรือใช้ฟิลเตอร์ลดสัญญาณรบกวนก่อนส่งให้ `RecognizeToResult` |
| **ไฟล์ใหญ่ทำให้ใช้หน่วยความจำมาก** | การโหลด PNG ขนาดหลายเมกะพิกเซลลงใน `Bitmap` ใช้ RAM มาก | ประมวลผลภาพเป็นชิ้น ๆ หรือย่อขนาดภาพโดยยังคงความอ่านได้ |
| **ข้อผิดพลาดการแปลงเป็น JSON** | `OcrResult` มีการอ้างอิงแบบวงกลม (เป็นไปได้น้อย) | ใช้ `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## โบนัส: ทำ OCR บน PNG ในลูปแบบแบตช์

หากคุณมีโฟลเดอร์ที่เต็มไปด้วยไฟล์ PNG คุณสามารถขยายตัวอย่างให้วนลูปผ่านไฟล์เหล่านั้นได้:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

ตอนนี้โปรแกรม **ทำ OCR บน PNG** จำนวนมากพร้อมกัน และสร้างไฟล์ JSON ที่สอดคล้องกันสำหรับแต่ละภาพ

## สรุป

คุณเพิ่งเรียนรู้วิธี **จดจำข้อความจากรูปภาพ** ใน C# ด้วย Aspose OCR, **โหลดรูปภาพสำหรับ OCR**, **ดึงข้อความจากรูปภาพ**, และ **เขียนไฟล์ JSON ด้วย C#** เพื่อเก็บผลลัพธ์ ตัวอย่างที่สมบูรณ์และสามารถรันได้ครอบคลุมขั้นตอนสำคัญทั้งหมด, อธิบายเหตุผลที่แต่ละส่วนสำคัญ, และแสดงวิธีจัดการกับข้อจำกัดเฉพาะของ PNG

ขั้นตอนต่อไป? ลองนำ JSON ไปใส่ในดัชนีการค้นหา, ผสานกับการตรวจจับภาษา, หรือรวมเข้ากับ Web API ที่ประมวลผลการอัปโหลดแบบเรียลไทม์ คุณอาจสนใจตรวจสอบการสนับสนุนการจดจำลายมือของ Aspose หากกรณีการใช้งานของคุณต้องการเช่นนั้น

มีคำถามเกี่ยวกับกรณีขอบหรือการปรับประสิทธิภาพ? แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!

![จดจำข้อความจากรูปภาพ ตัวอย่าง](/images/ocr-demo.png "แผนภาพแสดงวิธีที่ Aspose OCR จดจำข้อความจากรูปภาพ")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
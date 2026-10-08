---
category: general
date: 2026-02-11
description: แปลงภาพ OCR เป็น JSON ด้วย C# เรียนรู้การดึงข้อความจากภาพ อ่านไฟล์ภาพด้วย
  C# จัดรูปแบบผลลัพธ์ JSON และพิมพ์ JSON อย่างสวยงามด้วย C# โดยใช้ Aspose.OCR.
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: th
og_description: แปลงภาพ OCR เป็น JSON ด้วย C# คู่มือนี้แสดงวิธีดึงข้อความจากภาพ, อ่านไฟล์ภาพด้วย
  C#, จัดรูปแบบผลลัพธ์ JSON และพิมพ์ JSON อย่างสวยงามด้วย C# โดยใช้ Aspose.OCR.
og_title: OCR รูปภาพเป็น JSON ใน C# – คู่มือขั้นตอนโดยละเอียด
tags:
- OCR
- C#
- JSON
title: OCR รูปภาพเป็น JSON ใน C# – คู่มือขั้นตอนเต็ม
url: /th/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to json ใน C# – คู่มือขั้นตอนเต็ม

เคยต้องการ **ocr image to json** แต่ไม่แน่ใจว่าจะเลือกไลบรารีไหนหรือจะได้ผลลัพธ์ที่จัดรูปแบบสวยงามอย่างไร? คุณไม่ได้อยู่คนเดียว ในแอปพลิเคชันจริงหลาย ๆ อย่าง—การสแกนใบเสร็จ, การตรวจสอบบัตรประจำตัว, หรือการจัดเก็บเอกสารอย่างง่าย—คุณจะต้องการดึงข้อความจากภาพและได้ JSON ที่สะอาดซึ่งบริการต่อไปสามารถใช้ได้

ในบทเรียนนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งแต่การอ่านไฟล์ภาพใน C# ไปจนถึงการดึงข้อความด้วย Aspose.OCR, จากนั้นขอผลลัพธ์เป็น JSON ที่มีโครงสร้าง, และสุดท้าย pretty‑print JSON เพื่อให้มนุษย์อ่านได้ง่าย เมื่อเสร็จคุณจะมีโค้ดสั้น ๆ ที่พร้อมใช้งานในระดับ production ที่สามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้  

เราจะพูดถึงข้อผิดพลาดทั่วไป (เช่น การขาด language pack) และแสดงตัวอย่างการเปลี่ยนแปลงอย่างรวดเร็ว—เช่น การสลับเป็น XML หรือการจัดการ PDF หลายหน้า ไม่ต้องอ้างอิงเอกสารภายนอก; ทุกอย่างที่คุณต้องการอยู่ที่นี่

## สิ่งที่คุณต้องการ

- **.NET 6+** (โค้ดทำงานได้กับ .NET Framework 4.7+ ด้วยเช่นกัน)
- **Aspose.OCR for .NET** – ติดตั้งผ่าน NuGet (`Install-Package Aspose.OCR`)
- รูปภาพตัวอย่าง (เช่น `receipt.png`) วางไว้ในตำแหน่งที่คุณสามารถอ้างอิงได้
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ C# (ถ้าคุณเคยเขียน “Hello World” มาก่อน คุณก็พร้อมแล้ว)

> *เคล็ดลับมืออาชีพ:* หากคุณทำงานบนเซิร์ฟเวอร์ CI ให้ตั้งค่า `AutomaticResourceDownload = true` เพื่อให้ Aspose ดึงข้อมูลภาษาโดยอัตโนมัติ—ไม่ต้องจัดการ DLL ด้วยตนเอง

## ขั้นตอนที่ 1: อ่านไฟล์ภาพใน C# และสร้าง OCR engine  

สิ่งแรกที่เราทำคือโหลดภาพจากดิสก์ การใช้ `System.Drawing.Image` ทำให้โค้ดสั้นและรองรับ PNG, JPEG, BMP, และแม้กระทั่ง TIFF หลายหน้า (engine จะเลือกหน้าแรกโดยค่าเริ่มต้น)

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
- `AutomaticResourceDownload` ป้องกันการพังของโปรแกรมขณะรันเมื่อไฟล์ภาษาอังกฤษไม่มีอยู่ในเครื่อง  
- การตั้งค่า `OutputFormat` เป็น `Json` หมายความว่า engine จะทำการแปลงผล OCR ดิบเป็นอ็อบเจกต์ที่มีโครงสร้างให้แล้ว—ไม่ต้องทำการแปลงสตริงด้วยตนเอง

## ขั้นตอนที่ 2: รัน OCR และรับผลลัพธ์เป็น JSON  

ต่อไปเรานำ bitmap ที่โหลดแล้วส่งเข้า engine เมธอด `Recognize` จะคืนค่า `OcrResult` ที่มี property `Text` เก็บสตริง JSON

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**กรณีขอบ:** หากภาพเสียหายหรือพาธไม่ถูกต้อง `Image.FromFile` จะโยน `FileNotFoundException` ให้ห่อบล็อกด้วย `try/catch` หากคาดว่าจะมีอินพุตที่ไม่เสถียร

## ขั้นตอนที่ 3: แยกวิเคราะห์และจัดรูปแบบ JSON – pretty print JSON ใน C#  

JSON ดิบจาก OCR engine จะกระชับและอ่านยาก การใช้ `System.Text.Json` เราสามารถ deserialize เป็น `JsonDocument` แล้ว serialize ใหม่พร้อมการเยื้อง

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**สิ่งที่คุณจะเห็น:**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

JSON ตอนนี้รวมข้อความต่อบรรทัด, กล่องขอบเขต, ภาษาที่ตรวจพบ, และคะแนนความเชื่อมั่น—เหมาะอย่างยิ่งสำหรับส่งต่อไปยังระบบวิเคราะห์หรือคอมโพเนนต์ UI

## ขั้นตอนที่ 4: โบนัส – เปลี่ยนรูปแบบผลลัพธ์หรือภาษา  

หากคุณต้องการ **format json output** เป็น XML หรืออยาก OCR ใบเสร็จสเปน เพียงปรับการตั้งค่า engine เล็กน้อย:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

ส่วนที่เหลือของโค้ดยังคงเหมือนเดิม; คุณเพียงเปลี่ยนขั้นตอนการ deserialize (ใช้ `XmlDocument` สำหรับ XML)

## ตัวอย่างการทำงานเต็มรูปแบบ  

รวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์เดียวที่คุณสามารถคัดลอก‑วางไปยังแอปคอนโซล:

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

การรันโปรแกรมนี้จะพิมพ์ JSON ที่จัดรูปแบบอย่างสวยงามไปยังคอนโซลและบันทึกไว้ที่ `C:\Temp\ocr_pretty.json` บล็อก `try/catch` ทำให้แม้ภาพไม่สามารถอ่านได้ คุณก็จะได้รับข้อความแสดงข้อผิดพลาดที่ชัดเจนแทนการพังโดยไม่มีสัญญาณ

## คำถามทั่วไป & สิ่งที่ควรระวัง  

- **ถ้า OCR คืนข้อความว่าง?**  
  ส่วนใหญ่หมายถึงภาพมีสัญญาณรบกวนมากเกินไปหรือภาษาไม่ตรงกัน ลองเพิ่มความคอนทราสต์ของภาพหรือสลับ `Language` เป็น `AutoDetect`  

- **ฉันสามารถประมวลผลหลายภาพในลูปได้หรือไม่?**  
  ทำได้แน่นอน ห่อบล็อก `using (var img = Image.FromFile(...))` ภายในลูป `foreach (var file in Directory.GetFiles(...))` แล้วเก็บ `prettyJson` แต่ละอันลงในรายการหรือบันทึกเป็นไฟล์แยก  

- **สคีม่า JSON มีความเสถียรหรือไม่?**  
  Aspose รับประกันความเข้ากันได้ย้อนหลังสำหรับรูปแบบ `Json` แต่ควรตรวจสอบ attribute `Version` ในการตอบกลับหากคุณกำหนดเป้าหมายที่เวอร์ชัน API เฉพาะ  

- **ต้องใช้ไลเซนส์สำหรับ Aspose.OCR หรือไม่?**  
  คีย์ประเมินผลฟรีทำงานได้ถึง 100 หน้า สำหรับ production ให้ซื้อไลเซนส์และตั้งค่าโดยใช้ `License license = new License(); license.SetLicense("Aspose.OCR.lic");`

## สรุป  

คุณมี **complete, self‑contained solution to ocr image to json** ใน C# แล้ว โดยการอ่านไฟล์ภาพ, ตั้งค่า OCR engine, ขอผลลัพธ์เป็น JSON, และ pretty‑print คุณสามารถผสานการดึงข้อความเข้าไปในบริการ .NET ใดก็ได้โดยไม่ต้องจัดการสตริงแบบ hack  

จากนี้คุณอาจสำรวจ **extract text from image** สำหรับไฟล์ประเภทอื่น (PDF, TIFF หลายหน้า), ทดลองกับภาษาต่าง ๆ, หรือส่ง JSON ไปยัง NoSQL สำหรับการวิเคราะห์ ไม่จำกัดแค่ความคิด—แค่จำไว้ว่าให้จัดการข้อผิดพลาดอย่างรอบคอบและตรวจสอบไลเซนส์เมื่อขยายขนาด

ขอให้สนุกกับการเขียนโค้ด และขอให้ pipeline OCR ของคุณแม่นยำเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
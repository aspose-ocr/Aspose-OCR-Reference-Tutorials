---
category: general
date: 2026-01-13
description: บทเรียน OCR ด้วย C# ที่แสดงวิธีดึงข้อความจากภาพ, โหลดภาพสำหรับ OCR, และจัดรูปแบบผลลัพธ์
  JSON ด้วย Aspose OCR. เรียนรู้การแปลงอ็อบเจ็กต์เป็น JSON.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: th
og_description: บทเรียน OCR ด้วย C# ที่แนะนำขั้นตอนการดึงข้อความจากภาพ, การโหลดภาพสำหรับ
  OCR, และการจัดรูปแบบผลลัพธ์ JSON ด้วย Aspose OCR.
og_title: บทเรียน OCR ด้วย C# – ดึงข้อความและจัดรูปแบบ JSON
tags:
- OCR
- C#
- JSON
title: บทเรียน OCR ด้วย C# – ดึงข้อความจากภาพและรับ JSON ที่จัดรูปแบบ
url: /th/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – ดึงข้อความจากภาพและจัดรูปแบบผลลัพธ์ JSON

เคยสงสัยไหมว่า **ดึงข้อความจากไฟล์ภาพ** ในโปรเจกต์ C# อย่างไรโดยไม่ต้องจัดการกับการประมวลผลพิกเซลระดับต่ำ? นั่นคือปัญหาที่ *c# ocr tutorial* นี้แก้ได้ ในไม่กี่นาทีคุณจะได้เห็นวิธี **โหลดภาพสำหรับ OCR**, รัน Aspose OCR, และ **จัดรูปแบบผลลัพธ์ JSON** เพื่อให้คุณสามารถส่งข้อมูลตรงไปยัง API หรือฐานข้อมูลของคุณได้

เราจะเดินผ่านทุกบรรทัดของโค้ด, อธิบายว่าทำไมแต่ละส่วนถึงสำคัญ, และแม้แต่แสดง JSON ที่คุณควรคาดหวังไว้ให้โดยตรง เมื่อเสร็จแล้วคุณจะมีแอปคอนโซลที่พร้อมรันซึ่งแปลงไฟล์ PNG ใบแจ้งหนี้เป็น JSON ที่สะอาดและจัดย่อหน้าได้อย่างสวยงาม ไม่มีส่วนเกิน เพียงโซลูชันที่ใช้งานได้จริงที่คุณสามารถนำไปใส่ในโปรเจกต์ .NET 6+ ใดก็ได้

## สิ่งที่ c# ocr tutorial นี้ครอบคลุม

- การติดตั้งแพ็กเกจ NuGet Aspose.OCR  
- การโหลดไฟล์ภาพสำหรับการประมวลผล OCR  
- การจดจำข้อความภาษาอังกฤษ (หรือภาษาที่รองรับอื่นใด)  
- **การแปลงผล OCR เป็น JSON** พร้อมการจัดย่อหน้า (pretty‑printing)  
- การแสดง JSON ในคอนโซลและบันทึกลงไฟล์หากต้องการ  

คุณต้องมีความเข้าใจพื้นฐานของ C# และ .NET SDK เวอร์ชันล่าสุดเท่านั้น ไม่ต้องมีอะไรเพิ่มเติม หากคุณสนใจ **ดึงข้อความจากไฟล์ภาพ** สำหรับใบแจ้งหนี้, ใบเสร็จ, หรือแบบฟอร์มสแกน ให้อ่านต่อไป

---

## ขั้นตอนที่ 1: ตั้งค่าสภาพแวดล้อมสำหรับ c# ocr tutorial

ก่อนเขียนโค้ดใด ๆ ตรวจสอบให้แน่ใจว่าคุณมีเครื่องมือที่จำเป็น:

1. **.NET 6 SDK หรือใหม่กว่า** – ดาวน์โหลดได้จากเว็บไซต์ของ Microsoft  
2. **Visual Studio 2022** (Community ทำงานได้ดี) หรือเครื่องมือแก้ไขใดก็ได้ที่คุณชอบ  
3. **แพ็กเกจ NuGet Aspose.OCR** – รัน `dotnet add package Aspose.OCR` ในโฟลเดอร์โปรเจกต์ของคุณ  

> **เคล็ดลับ:** หากคุณใช้ CI pipeline ให้เพิ่มการอ้างอิงแพ็กเกจลงในไฟล์ `.csproj` ของคุณเพื่อให้การสร้าง (build) ดึงแพ็กเกจมาโดยอัตโนมัติ

---

## ขั้นตอนที่ 2: โหลดภาพสำหรับ OCR

ขั้นตอนแรกที่สำคัญในบทเรียนของเราคือการดึงภาพที่ต้องการประมวลผล Aspose OCR รองรับรูปแบบทั่วไปเช่น PNG, JPEG, และ TIFF

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **ทำไมขั้นตอนนี้สำคัญ:** การโหลดภาพเป็น `OcrImage` ทำให้เอนจินเข้าถึงข้อมูลบิตแมปและข้อมูล DPI ซึ่งช่วยเพิ่มความแม่นยำของการจดจำ หากข้ามขั้นตอนนี้หรือใส่ไฟล์ที่เสียหายจะทำให้เกิดข้อยกเว้น (exception) ระหว่างรัน

---

## ขั้นตอนที่ 3: ดึงข้อความจากภาพ

ตอนนี้เราจะรันเอนจิน OCR จริง ๆ เมธอด `Recognize` จะคืนค่าออบเจ็กต์ `OcrResult` ที่เต็มไปด้วยข้อความดิบ, คะแนนความเชื่อมั่น, และรายละเอียดการจัดวาง

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **กรณีขอบ:** หากต้องประมวลผลเอกสารหลายภาษา ให้เรียก `Recognize` สองครั้งด้วยค่า `OcrLanguage` ที่ต่างกันแล้วต่อผลลัพธ์เข้าด้วยกัน เอนจินนี้ปลอดภัยต่อการทำงานหลายเธรด (thread‑safe) ดังนั้นคุณสามารถทำงานแบบขนานกับชุดข้อมูลขนาดใหญ่ได้

---

## ขั้นตอนที่ 4: แปลงออบเจ็กต์เป็น JSON – จัดรูปแบบผลลัพธ์ JSON

ออบเจ็กต์ `OcrResult` เป็นคลาส C# ธรรมดา ซึ่งหมายความว่าเราสามารถส่งต่อให้ `System.Text.Json` ได้ โดยเปิดใช้งาน `WriteIndented` ผลลัพธ์จะเป็นรูปแบบที่มนุษย์อ่านได้ง่าย

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **สิ่งที่คุณจะได้:** สตริง JSON ที่จัดย่อหน้าอย่างสวยงาม ซึ่งรวมถึงข้อความที่จดจำได้, ความเชื่อมั่น, และโครงสร้างหน้า การจัดรูปแบบนี้เหมาะสำหรับการบันทึก, ส่งไปยังเว็บเซอร์วิส, หรือเก็บในฐานข้อมูล NoSQL

---

## ขั้นตอนที่ 5: แสดงและ (เลือก) บันทึก JSON ที่จัดรูปแบบแล้ว

สุดท้ายเราจะพิมพ์ JSON ไปที่คอนโซล คุณยังสามารถเขียนลงไฟล์ด้วย `File.WriteAllText` หากต้องการ

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**ผลลัพธ์คอนโซลที่คาดหวัง (ตัดบางส่วนเพื่อความกระชับ):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

หากเอนจิน OCR ไม่พบข้อความ ฟิลด์ `Text` จะเป็นสตริงว่างและ `Confidence` จะเป็น `0` ซึ่งเป็นสัญญาณให้คุณตรวจสอบคุณภาพของภาพอีกครั้ง

---

## ขั้นตอนที่ 6: ตัวอย่างทำงานครบถ้วน

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในแอปคอนโซลใหม่ได้:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

รันโปรแกรม (`dotnet run` จากโฟลเดอร์โปรเจกต์) แล้วดูคอนโซลพิมพ์ JSON ที่จัดย่อหน้าอย่างสวยงามของใบแจ้งหนี้ที่สแกนไว้

---

## ข้อผิดพลาดทั่วไป & เคล็ดลับ (c# ocr tutorial Extras)

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| **ฟิลด์ `Text` ว่าง** | ภาพมีคอนทราสต์ต่ำหรือหมุนผิดทิศ | ทำการพรี‑โปรเซสภาพ (เพิ่มคอนทราสต์, แก้ไขการเอียง) หรือใช้ `OcrEngine.ImagePreprocess` |
| **`System.DllNotFoundException`** | ไฟล์ไบนารีของ Aspose OCR ที่เป็นเนทีฟหาย | ตรวจสอบให้แน่ใจว่าแพ็กเกจ NuGet ถูกกู้คืนอย่างถูกต้องและสถาปัตยกรรมรันไทม์ (x64/x86) ตรงกับ OS |
| **ความล่าช้าเมื่อประมวลผล PDF ขนาดใหญ่** | OCR ประมวลผลทุกหน้าแบบต่อเนื่อง | ทำงานแบบขนานโดยสร้างอินสแตนซ์ `OcrEngine` แยกตามหน้า (เอนจินปลอดภัยต่อเธรด) |
| **JSON ใหญ่เกินไป** | คุณกำลังซีเรียลไลซ์รายละเอียดทั้งหมดรวมถึง bounding box | สร้าง DTO ที่มีเพียง `Text` และ `Confidence` ก่อนทำการซีเรียลไลซ์ |

> **จำไว้:** จุดมุ่งหมายของบทเรียนนี้คือการแสดงกระบวนการแบบครบวงจรที่สะอาด คุณสามารถตัด JSON ลงหรือเพิ่มเมตาดาต้าอื่น ๆ ได้ตามต้องการในภายหลัง

---

## สรุป

คุณเพิ่งทำ **c# ocr tutorial** ที่โหลดภาพ, **ดึงข้อความจากภาพ**, และสร้าง **ผลลัพธ์ JSON ที่จัดรูปแบบ** โดย **การแปลงออบเจ็กต์เป็น JSON** ขั้นตอนทั้งหมดง่าย โค้ดพร้อมรัน และ JSON ถูกจัดย่อหน้าอย่างสมบูรณ์สำหรับการใช้งานต่อ

ต่อไปคุณจะทำอะไร? ลองเปลี่ยน `OcrLanguage.English` เป็น `OcrLanguage.French` หรือทำลูปอ่านโฟลเดอร์ใบเสร็จหลายไฟล์ คุณอาจสำรวจการบันทึก JSON ลง Azure Blob Storage หรือส่งต่อให้โมเดลแมชชีน‑เลิร์นนิง

หากเจออุปสรรคใด ๆ ให้ตรวจสอบว่าเส้นทางภาพถูกต้องและไลเซนส์ Aspose OCR (หากมี) ถูกโหลดก่อนเรียก `Recognize` ขอให้เขียนโค้ดอย่างสนุกและผลลัพธ์ OCR ของคุณคมชัดเสมอ! 

--- 

*Image illustrating the OCR flow (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
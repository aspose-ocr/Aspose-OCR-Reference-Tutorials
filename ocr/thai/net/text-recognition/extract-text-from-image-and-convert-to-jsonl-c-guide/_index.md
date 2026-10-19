---
category: general
date: 2026-01-02
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C#. เรียนรู้วิธีแปลงภาพเป็นรูปแบบ
  JSONL อย่างรวดเร็วและเชื่อถือได้.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: th
og_description: ดึงข้อความจากภาพด้วย Aspose OCR และแปลงเป็นรูปแบบ JSONL. คู่มือสอน
  C# อย่างละเอียดขั้นตอนต่อขั้นตอนสำหรับนักพัฒนา.
og_title: ดึงข้อความจากภาพ – แปลงเป็น JSONL ด้วย C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: ดึงข้อความจากภาพและแปลงเป็น JSONL – คู่มือ C#
url: /th/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากรูปภาพและแปลงเป็น JSONL – คอร์สสอน C# ฉบับสมบูรณ์

เคยต้อง **สกัดข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าคลังไหนจะให้ผลลัพธ์ที่สะอาดและเป็นโครงสร้างหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการที่ต้องประมวลผลใบเสร็จหรือดิจิไทซ์เอกสาร ปัญหาสำคัญคือการเปลี่ยนบิตแมปให้เป็นข้อความที่ค้นหาได้ *และ* รูปแบบที่เครื่องอ่านได้  

ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถ **สกัดข้อความจากรูปภาพ** และด้วยไม่กี่บรรทัดของโค้ด **แปลงรูปภาพเป็น JSONL** เพื่อการวิเคราะห์ต่อไป คู่มือนี้จะพาคุณผ่านขั้นตอนทั้งหมด ตั้งแต่การโหลด PNG ไปจนถึงการเขียนไฟล์ JSON‑Lines ที่สามารถสตรีมเข้าสู่ pipeline ของข้อมูลได้

> **เคล็ดลับ:** หากคุณใช้ .NET 6 หรือใหม่กว่า โค้ดเดียวกันทำงานได้โดยไม่ต้องตั้งค่าเพิ่มเติม

## สิ่งที่ต้องเตรียมล่วงหน้า — What You’ll Need

- **.NET 6 SDK** (หรือเวอร์ชัน .NET ล่าสุดใดก็ได้)
- **Aspose.OCR** NuGet package  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** สำหรับการแปลงเป็น JSON  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- ตัวอย่างรูปภาพ (เช่น `receipt.png`) ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้
- IDE หรือ editor ที่คุณชอบ—Visual Studio, VS Code, Rider ฯลฯ

ไม่มีการตั้งค่าซับซ้อน ไม่มีบริการภายนอก เพียงแค่ NuGet package ไม่กี่ตัว

![สกัดข้อความจากรูปภาพโดยใช้ C#](https://example.com/assets/ocr-sample.png)

*Alt text: สกัดข้อความจากรูปภาพโดยใช้ C# กับ Aspose OCR*

## ขั้นตอนที่ 1: โหลดรูปภาพที่ต้องการประมวลผล  

สิ่งแรกที่คุณทำเมื่ออยาก **สกัดข้อความจากรูปภาพ** คือให้ OCR engine ได้รับบิตแมป การใช้ `System.Drawing.Bitmap` ทำได้ง่ายและรองรับรูปแบบ raster ส่วนใหญ่

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **ทำไมเรื่องนี้สำคัญ:** การโหลดรูปภาพเป็น `Bitmap` ให้ OCR engine เข้าถึงพิกเซลโดยตรง ซึ่งช่วยเพิ่มความเร็วและความแม่นยำของการจดจำเมื่อเทียบกับการสตรีมไบต์ดิบ

## ขั้นตอนที่ 2: ตั้งค่า Aspose OCR สำหรับผลลัพธ์แบบ JSON‑Lines  

Aspose OCR ให้คุณระบุภาษา, รูปแบบผลลัพธ์, และการปรับแต่งประสิทธิภาพเล็กน้อย ที่นี่เราขอ **JSON‑Lines** (หนึ่ง JSON object ต่อบรรทัด) เพราะเหมาะกับการประมวลผลแบบบรรทัดต่อบรรทัดในภายหลัง

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **เคล็ดลับระดับมืออาชีพ:** หากต้องจัดการใบเสร็จหลายภาษา ให้ตั้งค่า `Language = Language.Multilingual` หรือส่งอาเรย์ของค่า `Language` ที่ต้องการ

## ขั้นตอนที่ 3: รัน OCR และเก็บผลลัพธ์  

ตอนนี้เราจะ **สกัดข้อความจากรูปภาพ** จริง ๆ เมธอด `Recognize` จะคืนค่าเป็นอ็อบเจกต์ `OcrResult` ที่มีคอลเลกชันของ `OcrLine` แต่ละรายการแทนบรรทัดของข้อความที่จดจำได้พร้อมกับกรอบขอบเขต

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

ในขณะนี้ `ocrResult.Lines` มีทุกอย่างที่คุณต้องการ—ข้อความดิบ, คะแนนความเชื่อมั่น, และพิกัด

## ขั้นตอนที่ 4: แปลงคอลเลกชันเป็น JSON‑Lines  

เราจะเปลี่ยนคอลเลกชันเป็นสตริง JSON ที่จัดรูปแบบอย่างสวยงาม แม้ว่า JSON‑Lines ปกติจะกระชับ การเพิ่มการเยื้องทำให้ไฟล์อ่านง่ายขึ้นในขั้นตอนพัฒนา

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

ตัวแปร `jsonLines` ที่ได้จะมีลักษณะประมาณนี้ (ตัดให้สั้นเพื่อความกระชับ)

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

แต่ละบรรทัดจบด้วยอักขระ newline ทำให้คุณได้ไฟล์ **JSONL** (JSON‑Lines) ที่แท้จริง

## ขั้นตอนที่ 5: เขียน JSON‑Lines ลงดิสก์  

สุดท้ายเราจะบันทึกผลลัพธ์เพื่อให้บริการอื่น—เช่น Spark, Logstash, หรือสคริปต์ Bash ง่าย ๆ—สามารถอ่านได้บรรทัดต่อบรรทัด

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

เมื่อคุณเปิด `receipt.jsonl` คุณจะเห็น JSON object หนึ่งอันต่อบรรทัด พร้อมสำหรับการสตรีม

## ขั้นตอนที่ 6: ตรวจสอบการส่งออก  

การตรวจสอบอย่างรวดเร็วจะช่วยประหยัดเวลาการดีบักในภายหลัง เรามาอ่านบรรทัดแรก ๆ กลับมาและพิมพ์ลงคอนโซล

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

ผลลัพธ์ที่แสดงบนคอนโซลทั่วไป:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

หากคุณเห็นสิ่งคล้ายกัน ยินดีด้วย—คุณได้ **สกัดข้อความจากรูปภาพ** และ **แปลงรูปภาพเป็น JSONL** สำเร็จแล้ว

## ข้อผิดพลาดที่พบบ่อยและวิธีหลีกเลี่ยง  

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| **ผลลัพธ์เป็นค่าว่าง** | เส้นทางรูปภาพไม่ถูกต้องหรือไฟล์ไม่สามารถอ่านได้ | ใช้ `File.Exists(imagePath)` ก่อนสร้าง bitmap |
| **คะแนนความเชื่อมั่นต่ำ** | รูปภาพเบลอหรือคอนทราสต์ต่ำ | ทำการพรี‑โปรเซสรูปภาพ (เช่น `Bitmap.RotateFlip`, `Graphics.Clear`) หรือเพิ่ม DPI |
| **ภาษาไม่ถูกต้อง** | OCR ตั้งค่าเป็นอังกฤษโดยอัตโนมัติ แต่ใบเสร็จเป็นภาษาอื่น | ตั้งค่า `options.Language = Language.Spanish` (หรือ enum ที่เหมาะสม) |
| **JSONL แสดงเป็นอาเรย์ JSON เดียว** | ใช้ `Formatting.None` โดยไม่มีการจัดการ newline | ตรวจสอบให้แต่ละอ็อบเจกต์ที่แปลงเป็นสตริงจบด้วย `Environment.NewLine` |

## ตัวอย่างทำงานเต็มรูปแบบ  

ด้านล่างเป็นโปรแกรมที่พร้อมรัน เพียงคัดลอกไปยังโปรเจกต์คอนโซลและกด **F5**

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** ไฟล์ `receipt.jsonl` ที่มี JSON object หนึ่งอันต่อบรรทัด แต่ละอันมีฟิลด์ `Text`, `Confidence`, และ `BoundingBox` คุณสามารถนำไฟล์นี้เข้าสู่ pipeline วิเคราะห์ใด ๆ ที่รับ JSONL ได้ทันที

## ขั้นตอนต่อไป – ขยายขอบเขตการใช้งาน OCR พื้นฐาน  

- **การประมวลผลเป็นชุด:** ห่อหุ้มโลจิกข้างต้นในลูป `foreach` เพื่อจัดการโฟลเดอร์ใบเสร็จทั้งหมด
- **การทำงานแบบขนาน:** ใช้ `Parallel.ForEach` เพื่อเร่งความเร็วบนหลายคอร์เมื่อจัดการภาพหลายพันรูป
- **การหลังประมวลผล:** กรองบรรทัดที่ความเชื่อมั่นต่ำ (`Confidence < 0.9`) ก่อนบันทึก
- **การบูรณาการ:** ส่ง JSONL ตรงไปยัง Azure Blob Storage หรือ AWS S3 ด้วย SDK ที่เกี่ยวข้อง
- **รูปแบบทางเลือก:** เปลี่ยน `OutputFormat` เป็น `PlainText` หรือ `Xml` หากระบบปลายทางต้องการรูปแบบเหล่านั้น

## สรุป  

คุณมีโซลูชันครบวงจรสำหรับ **การสกัดข้อความจากรูปภาพ** และ **การแปลงรูปภาพเป็น JSONL** ด้วย Aspose OCR ใน C# แล้ว บทเรียนนี้ครอบคลุมตั้งแต่การโหลด bitmap ไปจนถึงการตรวจสอบผลลัพธ์ พร้อมเคล็ดลับปฏิบัติที่ช่วยให้ pipeline ของคุณมั่นคง  

ลองใช้กับใบเสร็จ, ใบแจ้งหนี้, หรือแบบฟอร์มสแกนของคุณเอง—ดู OCR engine แปลงพิกเซลเป็นข้อมูลที่ค้นหาได้และจัดเป็นบรรทัดในไม่กี่วินาที หากเจอกรณีขอบ (เช่น การสแกนเอียงหรือข้อความหลายภาษา) ให้กลับไปตรวจสอบส่วน *RecognitionOptions* และปรับค่า language หรือขั้นตอนพรี‑โปรเซสตามต้องการ  

ขอให้เขียนโค้ดสนุกและ pipeline ของคุณสะอาดตาเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
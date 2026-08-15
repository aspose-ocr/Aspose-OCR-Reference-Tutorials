---
category: general
date: 2026-04-17
description: เรียนรู้ตัวอย่าง Aspose OCR เพื่ออ่านไฟล์รูปภาพด้วย C#, ดึงข้อความจากรูปภาพด้วย
  C# และเขียนไฟล์ JSON ด้วย C#. คู่มือการทำ OCR ด้วย C# อย่างครบถ้วนแบบขั้นตอนต่อขั้นตอน.
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: th
og_description: เชี่ยวชาญตัวอย่าง Aspose OCR เพื่ออ่านภาพ ดึงข้อความ และเขียนไฟล์
  JSON ด้วย C# ปฏิบัติตามบทเรียน OCR C# สั้น ๆ นี้.
og_title: ตัวอย่าง Aspose OCR – แปลงข้อความจากรูปภาพเป็น JSON ใน C#
tags:
- Aspose
- OCR
- C#
- JSON
title: ตัวอย่าง Aspose OCR – แปลงข้อความในรูปภาพเป็น JSON ด้วย C#
url: /th/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตัวอย่าง aspose ocr – แปลงข้อความจากรูปภาพเป็น JSON ใน C#

เคยต้องการ **aspose ocr example** ที่ไม่เพียงแค่อ่านรูปภาพ แต่ยังส่งออก JSON ที่เรียบร้อยสำหรับการประมวลผลต่อไปหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการ—เช่นระบบอัตโนมัติใบแจ้งหนี้, การสแกนใบเสร็จ, หรือแม้กระทั่งการจัดเก็บเอกสารอย่างง่าย—นักพัฒนาต่างเจออุปสรรคเดียวกัน: “จะเอาผลลัพธ์ OCR ไปอยู่ในรูปแบบที่ API ของฉันชอบได้อย่างไร?”

ข่าวดีคืออะไร? ด้วย Aspose.OCR คุณทำได้ในไม่กี่บรรทัดและฉันจะแสดงให้คุณเห็นอย่างละเอียด จนกระทั่งคุณจะรู้วิธี **read image file C#**, **extract text image C#**, และ **write JSON file C#**—ทั้งหมดในบทเรียน OCR C# ที่สะอาดและนำกลับมาใช้ใหม่ได้

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดยังคอมไพล์ได้กับ .NET Core ด้วย)  
- Aspose.OCR for .NET NuGet package (`Install-Package Aspose.OCR`)  
- รูปภาพ (`input.jpg`) ที่มีข้อความที่อ่านได้อย่างชัดเจน  
- โปรแกรมแก้ไขข้อความหรือ Visual Studio (IDE ใดก็ได้)  

ไม่มีไฟล์กำหนดค่าเพิ่มเติม ไม่มีเวทมนตร์ที่ซ่อนอยู่—แค่ SDK กับรูปภาพเท่านั้น

## ขั้นตอนที่ 1 – อ่านไฟล์รูปภาพ C# ด้วย Aspose.OCR

ก่อนอื่นคุณต้องส่งภาพที่ถูกต้องให้กับเครื่องมือ OCR Aspose.OCR คาดหวังอ็อบเจ็กต์ `OcrImage` ซึ่งคุณสามารถสร้างโดยตรงจากเส้นทางไฟล์

```csharp
using Aspose.OCR;
using System.IO;

// Path to the source picture
string imagePath = @"C:\MyProject\Images\input.jpg";

// Load the image – this is the “read image file C#” part
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

*ทำไมสิ่งนี้ถึงสำคัญ:* การโหลดภาพตั้งแต่แรกช่วยให้คุณตรวจสอบการมีอยู่ของไฟล์และจับปัญหารูปแบบก่อนที่เครื่องมือจะเริ่มประมวลผลพิกเซล หากไฟล์หายไป `FromFile` จะโยนข้อยกเว้นที่ชัดเจนให้คุณจัดการต่อไป

## ขั้นตอนที่ 2 – เริ่มต้นเครื่องมือ Aspose OCR

การสร้างเครื่องมือใช้ทรัพยากรน้อย แต่คุณควรห่อไว้ในคำสั่ง `using` เพื่อให้ทรัพยากรถูกปล่อยอย่างทันท่วงที

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*เคล็ดลับ:* เครื่องมือเริ่มต้นทำงานได้ดีสำหรับข้อความส่วนใหญ่ที่เป็นภาษาละติน หากคุณต้องการภาษาอื่น คุณสามารถตั้งค่า `ocrEngine.Language = Language.YourLanguage;` ก่อนเรียก `Recognize`

## ขั้นตอนที่ 3 – ดึงข้อความจากรูปภาพ C# – ทำการจดจำ

ตอนนี้งานหนักเริ่มขึ้นเมธอด `Recognize` จะคืนค่าอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความดิบ, คะแนนความเชื่อมั่น, และกล่องขอบเขตของแต่ละคำ

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

คุณจะสังเกตว่า `ocrResult.Text` เก็บสตริงธรรมดา ส่วน `ocrResult.Regions` ให้ข้อมูลตำแหน่ง หากคุณต้องการไฮไลท์คำใน UI

## ขั้นตอนที่ 4 – เขียนไฟล์ JSON C# – แปลงผลลัพธ์เป็น JSON

การแปลงเป็น JSON ทำได้ง่ายด้วย `System.Text.Json` เราจะจัดรูปแบบให้อ่านง่ายสำหรับมนุษย์

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*ทำไมเราถึงใช้ `System.Text.Json`*: มันเป็นส่วนหนึ่งของ .NET, เร็ว, และไม่ต้องพึ่งพาไลบรารีเพิ่มเติม หากคุณชอบใช้ Newtonsoft เพียงเปลี่ยนไม่กี่บรรทัดเท่านั้น

## ขั้นตอนที่ 5 – บันทึก JSON ลงดิสก์

สุดท้ายให้เขียนสตริงลงไฟล์ ซึ่งเป็นส่วนของ **write json file c#** ที่เสร็จสมบูรณ์

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### ตัวอย่างผลลัพธ์ JSON (ตัวอย่าง)

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑01\nTotal: $1,234.56",
  "Regions": [
    {
      "BoundingBox": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Confidence": 0.98,
      "Text": "Invoice #12345"
    },
    {
      "BoundingBox": { "X": 10, "Y": 60, "Width": 150, "Height": 30 },
      "Confidence": 0.96,
      "Text": "Date: 2024‑03‑01"
    },
    {
      "BoundingBox": { "X": 10, "Y": 100, "Width": 180, "Height": 30 },
      "Confidence": 0.99,
      "Text": "Total: $1,234.56"
    }
  ]
}
```

*หมายเหตุ:* ตัวเลขที่แสดงจะต่างกันตามภาพของคุณ แต่โครงสร้างคงที่—เหมาะอย่างยิ่งสำหรับส่งต่อไปยัง API, ฐานข้อมูล, หรือเครื่องมือแสดงผลด้านหน้า

## ตัวอย่างเต็มของ C# OCR – รวมทุกขั้นตอน

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วางครบถ้วน ซึ่งเชื่อมทุกขั้นตอนเข้าด้วยกัน ไม่ขาดส่วนใด ไม่ใช้ “ดูเอกสาร” เป็นทางลัด

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\MyProject\Images\input.jpg";
        var ocrImage = OcrImage.FromFile(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine();
        // Example: ocrEngine.Language = Language.English; // optional

        // -------------------------------------------------
        // Step 3: Perform OCR recognition
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // -------------------------------------------------
        // Step 4: Serialize the result to indented JSON
        // -------------------------------------------------
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // -------------------------------------------------
        // Step 5: Write the JSON to a file
        // -------------------------------------------------
        string jsonOutputPath = @"C:\MyProject\Output\output.json";
        File.WriteAllText(jsonOutputPath, json);

        // -------------------------------------------------
        // Step 6: Let the user know we’re done
        // -------------------------------------------------
        Console.WriteLine("OCR data saved as JSON.");
    }
}
```

### การรันโค้ด

1. แทนที่เส้นทาง `@"C:\MyProject\…"` ทั้งสองด้วยไดเรกทอรีของคุณจริง  
2. สร้างโปรเจกต์ (`dotnet build`) และรัน (`dotnet run`)  
3. เปิด `output.json`—คุณควรเห็นการแสดงผลที่จัดโครงสร้างอย่างสวยงามของข้อความในภาพ

## คำถามทั่วไป & กรณีขอบ

**ถ้าภาพของฉันเบลอล่ะ?**  
Aspose.OCR มีตัวเลือกการเตรียมภาพล่วงหน้า เช่น `ocrEngine.ImagePreprocessOptions.Deskew = true;` เปิดใช้งานก่อนเรียก `Recognize` เพื่อเพิ่มความแม่นยำ

**ฉันสามารถจำกัดผลลัพธ์ให้เป็นข้อความธรรมดาเท่านั้นได้ไหม?**  
ทำได้—แค่ทำการ serialize `ocrResult.Text` แทนอ็อบเจ็กต์ทั้งหมด:

```csharp
string plainJson = JsonSerializer.Serialize(
    new { Text = ocrResult.Text },
    new JsonSerializerOptions { WriteIndented = true });
```

**ต้องจัดการกับ PDF หลายหน้าไหม?**  
ตัวอย่างนี้มุ่งเน้นที่ภาพเดียว แต่คุณสามารถวนลูปผ่านภาพแต่ละหน้าที่แปลงจาก PDF, รันขั้นตอนเดียวกัน, แล้วรวมผลลัพธ์เป็นอาร์เรย์ JSON

## เคล็ดลับระดับมืออาชีพ & สิ่งที่ควรระวัง

- **File paths:** ใช้ `Path.Combine` เพื่อหลีกเลี่ยงการเขียน backslash แบบคงที่ โดยเฉพาะหากคุณย้ายไปใช้ Linux  
- **Memory:** สำหรับชุดข้อมูลขนาดใหญ่ ให้ใช้ `OcrEngine` ตัวเดียวซ้ำแทนการสร้างใหม่สำหรับแต่ละภาพ  
- **JSON size:** หากต้องการแค่ข้อความเท่านั้น ให้ละเว้น property `Regions` เพื่อลดขนาด payload  
- **Version check:** บทเรียนนี้ทดสอบกับ Aspose.OCR 23.9.0; เวอร์ชันใหม่ ๆ มี API เดียวกัน แต่ควรตรวจสอบ release notes สำหรับการเปลี่ยนแปลงที่อาจทำให้โค้ดเสีย

![ตัวอย่างผลลัพธ์ OCR JSON – ตัวอย่าง aspose ocr](https://example.com/sample-ocr-json.png "ตัวอย่าง JSON ของ aspose ocr")

## สรุป

เราได้เดินผ่าน **aspose ocr example** ที่ครบถ้วน ซึ่งอ่านภาพ, ดึงข้อความ, และเขียนผลลัพธ์เป็นไฟล์ JSON ด้วย C# แท้ โซลูชันนี้เป็นอิสระ, พร้อมใช้งานในสภาพการผลิต, และขยายได้ง่าย—ไม่ว่าจะเพิ่มการสนับสนุนภาษา, ปรับค่าเกณฑ์ความเชื่อมั่น, หรือส่ง JSON ไปยังบริการต่อเนื่อง

ถ้าคุณกำลังมองหาขั้นตอนต่อไป ลองเชื่อมบทเรียนนี้กับ **C# OCR tutorial** ที่อัปโหลด JSON ไปยัง Azure Cognitive Search, หรือทดลองดึงตารางจากใบแจ้งหนี้ ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณมี JSON ในมือ

มีไอเดียหรือวิธีการใหม่ที่อยากแชร์ไหม? แสดงความคิดเห็น, fork repo, หรือทักมาที่ GitHub ของฉัน Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
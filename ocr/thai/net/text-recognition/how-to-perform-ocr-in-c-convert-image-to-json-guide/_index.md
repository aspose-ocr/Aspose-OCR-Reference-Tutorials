---
category: general
date: 2026-02-17
description: วิธีทำ OCR ด้วย C# และแปลงภาพเป็น JSON อย่างรวดเร็ว ตามบทเรียน OCR ด้วย
  C# นี้เพื่อดึงข้อความจากภาพและบันทึกโครงสร้างเป็น JSON.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: th
og_description: ทำอย่างไรจึงจะทำ OCR ใน C#? คู่มือนี้จะแสดงวิธีแปลงภาพเป็น JSON, ดึงข้อความจากภาพใน
  C#, และโหลดไฟล์ภาพสำหรับ OCR.
og_title: วิธีทำ OCR ใน C# – แปลงรูปภาพเป็น JSON
tags:
- OCR
- C#
- Aspose
title: วิธีทำ OCR ใน C# – คู่มือแปลงภาพเป็น JSON
url: /th/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ใน C# – คู่มือแปลงภาพเป็น JSON

เคยสงสัย **วิธีทำ OCR** บนใบเสร็จ, ใบแจ้งหนี้, หรือเอกสารสแกนใด ๆ ด้วย C# หรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาหลายคนมักติดขัดเมื่อจำเป็นต้องดึงข้อความ *และ*รักษาโครงสร้างโดยไม่ต้องเขียนพาร์เซอร์เองหลายชั่วโมง  

ในบทแนะนำนี้เราจะพาคุณผ่าน **c# ocr tutorial** อย่างครบถ้วน ที่แสดงให้เห็นวิธีทำ OCR, **แปลงภาพเป็น json**, และบันทึกผลลัพธ์เพื่อการวิเคราะห์ต่อไป หลังจากทำตามแล้วคุณจะมีแอปคอนโซลที่พร้อมรัน ซึ่งโหลดไฟล์ภาพใน C#, ดึงข้อความ, และเขียนไฟล์ JSON รายละเอียดที่มีพิกัด, คะแนนความเชื่อมั่น, และข้อความดิบ

## สิ่งที่ต้องเตรียม — Prerequisites

- .NET 6 SDK หรือใหม่กว่า (โค้ดนี้ทำงานบน .NET Core ด้วย)  
- Visual Studio 2022 หรือโปรแกรมแก้ไขที่คุณชอบ  
- ใบอนุญาต Aspose OCR (คุณสามารถเริ่มต้นด้วยรุ่นทดลองฟรี)  
- ตัวอย่างภาพ, เช่น `receipt.png`, วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้  

เท่านี้—ไม่มีแพคเกจ NuGet เพิ่มเติมนอกจาก `Aspose.OCR` หากคุณมีสิ่งเหล่านี้ครบ คุณก็พร้อมเริ่มแล้ว

## วิธีทำ OCR และรับผลลัพธ์เป็น JSON

หัวใจของ **วิธีทำ OCR** ด้วย Aspose นั้นง่าย: สร้าง `OcrEngine`, ส่งสตรีมภาพเข้าไป, เรียก `Recognize`, แล้วทำการแปลง `OcrResult` เป็น JSON มาดูขั้นตอนทีละขั้นตอนกัน

### ขั้นตอน 1: ติดตั้งแพคเกจ NuGet ของ Aspose OCR

เปิดเทอร์มินัลในโฟลเดอร์โครงการและรัน:

```bash
dotnet add package Aspose.OCR
```

> **เคล็ดลับ:** ใช้แฟล็ก `--version` เพื่อระบุเวอร์ชันล่าสุดที่เสถียร (เช่น `23.9.0`). จะทำให้การสร้างของคุณทำซ้ำได้

### ขั้นตอน 2: สร้าง Skeleton ของโปรเจกต์คอนโซล

หากยังไม่มีโปรเจกต์, สร้างใหม่:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

ตอนนี้คุณมีไฟล์ `Program.cs` พร้อมสำหรับโค้ดที่จะ **load image file c#** และเริ่มกระบวนการ OCR

### ขั้นตอน 3: เขียนโค้ดเต็มรูปแบบ OCR‑to‑JSON

ด้านล่างเป็นโปรแกรมที่พร้อมรัน คัดลอก‑วางลงใน `Program.cs`. ทุกบรรทัดมีคอมเมนต์เพื่อให้คุณเห็น *ทำไม* แต่ละส่วนสำคัญ

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### สิ่งที่โค้ดทำ

| ขั้นตอน | ทำไมจึงสำคัญ |
|------|----------------|
| **Initialize OcrEngine** | ตั้งค่าภาษาเริ่มต้น (อังกฤษ) และเตรียมโมเดลภายใน |
| **Load image file** | การใช้ `ImageStream.FromFile` ทำให้ภาพถูกอ่านในรูปแบบที่ Aspose คาดหวัง |
| **Recognize** | งานหลัก—วิเคราะห์พิกเซล, แบ่งอักขระ, และค้นหาคำในพจนานุกรม |
| **ToJson** | สร้างผลลัพธ์โครงสร้างที่รวมกล่องขอบเขต, ความเชื่อมั่น, และข้อความดิบ |
| **WriteAllText** | บันทึก JSON เพื่อให้คุณสามารถแชร์กับบริการอื่นได้ |
| **Console.WriteLine** | ให้ฟีดแบ็กทันที—สะดวกเมื่อรันจากเทอร์มินัล |

> **ระวัง:** หากภาพของคุณมีขนาดใหญ่, ควรปรับขนาดก่อนเพื่อเพิ่มความเร็วและลดการใช้หน่วยความจำ. Aspose มีเมธอด `Resize` ที่คุณสามารถเรียกใช้บน `ImageStream`

### ขั้นตอน 4: รันแอปและตรวจสอบผลลัพธ์

จากเทอร์มินัล:

```bash
dotnet run
```

คุณควรเห็น:

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

เปิด `receipt.json` ด้วยโปรแกรมแก้ไขใดก็ได้; คุณจะพบข้อมูลประมาณนี้:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

JSON นี้บันทึก **extract text image c#** พร้อมเมตาดาต้าเลย์เอาต์, เหมาะสำหรับการประมวลผลต่อไป

## แปลงภาพเป็น JSON – เกินกว่าพื้นฐาน

ตอนนี้คุณรู้ **วิธีทำ OCR** แล้ว, มาดูตัวแปรเพิ่มเติมที่อาจต้องใช้ในโครงการจริง

### จัดการหลายหน้า

หากแหล่งข้อมูลของคุณเป็น PDF หรือ TIFF หลายหน้า, เพียงวนลูปแต่ละหน้า:

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### ปรับภาษาและความแม่นยำ

Aspose รองรับมากกว่า 40 ภาษา. เพื่อสลับเป็นสเปน:

```csharp
ocrEngine.Language = Language.Spanish;
```

คุณยังสามารถปรับ `ocrEngine.Settings` เพื่อเปิด **auto‑rotate**, **noise removal**, หรือ **dictionary‑based correction**—ทั้งหมดช่วยปรับคุณภาพของ JSON ที่ได้

### บันทึก JSON ในรูปแบบ Pretty‑Printed

หากต้องการ JSON ที่มีการเยื้องเพื่ออ่านง่าย:

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Load Image File C# – ข้อผิดพลาดทั่วไปและเคล็ดลับ

เมื่อคุณ **load image file c#**, อาจเจอปัญหา:

- **File not found** – ตรวจสอบให้แน่ใจว่าใช้พาธแบบเต็มหรือใช้ `Path.Combine` กับ `Environment.CurrentDirectory`  
- **Unsupported format** – Aspose รองรับ PNG, JPEG, BMP, TIFF, และ PDF. สำหรับฟอร์แมต RAW ให้แปลงก่อน  
- **Large file memory pressure** – ใช้ `ImageStream.FromFile(path, maxSizeInKB)` เพื่อลดขนาดขณะโหลด

การแก้ไขปัญหาเหล่านี้ตั้งแต่แรกจะช่วยคุณหลีกเลี่ยงข้อยกเว้นที่สับสนในขั้นตอน OCR ต่อไป

## Extract Text Image C# – ตรวจสอบผลลัพธ์

หลังจากได้ JSON, หากต้องการเพียงข้อความดิบ:

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

ส่วนนี้แสดง **extract text image c#** โดยไม่มีรายละเอียดเลย์เอาต์—เหมาะสำหรับการค้นหาอย่างรวดเร็วหรือบันทึกล็อก

---

![Diagram showing OCR workflow – how to perform OCR, convert image to JSON, and extract text image c#](/images/ocr-workflow.png "how to perform OCR workflow")

*ข้อความแทนภาพ: "แผนผังการทำ OCR แสดงขั้นตอนแปลงภาพเป็น JSON และดึงข้อความภาพ c#"*  

*(ภาพเป็นเพียงตัวอย่าง; โปรดแทนที่ด้วยแผนผังจริงเมื่อเผยแพร่)*

---

## สรุป

เราได้ครอบคลุม **วิธีทำ OCR** ใน C# ตั้งแต่ต้นจนจบ, แสดงวิธี **แปลงภาพเป็น JSON**, และอธิบายรายละเอียดของ **load image file c#** และ **extract text image c#** ตัวอย่างโค้ดเต็มพร้อมใช้งานในโครงการ .NET ใด ๆ, และผลลัพธ์ JSON ให้ทั้งข้อความดิบและข้อมูลเลย์เอาต์ที่แม่นยำสำหรับการวิเคราะห์ต่อ

ต่อไปคุณอาจลองส่ง JSON ไปยังฐานข้อมูล, แสดงกล่องขอบเขตบน UI, หรือทำ OCR เป็นชุดหลายไฟล์ คุณยังสามารถทดลองฟีเจอร์ Aspose อื่น ๆ เช่น การจดจำลายมือหรือการตรวจจับบาร์โค้ด—ทั้งหมดสามารถผสานเข้ากับ pipeline เดียวกันได้

หากเจออุปสรรคใด ๆ ให้กลับไปตรวจสอบเคล็ดลับในส่วน “Load Image File C#” หรือสำรวจเอกสารของ Aspose สำหรับการตั้งค่าขั้นสูง ขอให้สนุกกับการเขียนโค้ดและแปลงภาพเป็นข้อมูลโครงสร้าง!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-02
description: บทเรียน OCR ด้วย C# ที่แสดงวิธีดึงข้อความจากภาพใน C# และจดจำข้อความในไฟล์
  PNG จากนั้นเขียน JSON ที่มีการเยื้องโดยใช้ JsonSerializer ของ C# คู่มือขั้นตอนต่อขั้นตอนสำหรับนักพัฒนา
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: th
og_description: บทเรียน OCR ด้วย C# ที่สาธิตวิธีดึงข้อความจากภาพด้วย C# และจดจำข้อความในไฟล์
  PNG จากนั้นเขียน JSON ที่จัดรูปแบบด้วย JsonSerializer ของ C# ตัวอย่างที่สมบูรณ์และสามารถรันได้
og_title: c# OCR tutorial – ดึงข้อความและส่งออกเป็น JSON ที่มีการเยื้อง
tags:
- OCR
- C#
- Aspose
- JSON
title: บทเรียน OCR ด้วย C# – ดึงข้อความจากภาพและส่งออกเป็น JSON ที่จัดย่อหน้า
url: /th/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – ดึงข้อความจากรูปภาพและส่งออกเป็น JSON ที่จัดย่อหน้า

เคยต้องการ **c# ocr tutorial** ที่นำภาพของข้อความไปสู่ไฟล์ JSON ที่จัดรูปแบบอย่างสวยงามหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ – เช่น การสแกนใบแจ้งหนี้, การแยกข้อมูลใบเสร็จ, หรือแม้แต่การดึงข้อความจาก meme – คุณจะได้ไฟล์ PNG แล้วสงสัยว่าจะดึงคำออกมาอย่างไรโดยไม่ต้องเขียน recognizer เอง  

คู่มือนี้ให้วิธีแก้แบบทำมือ: เราจะ **extract text image c#** ด้วย Aspose.OCR, **recognize png text**, แล้ว **write indented json** ด้วย `JsonSerializer` ใน C#. เมื่อเสร็จคุณจะมีแอปคอนโซลที่พร้อมใช้งานและสามารถใส่ลงในโซลูชัน .NET ใดก็ได้ ไม่ต้องอ้างอิง “ดูเอกสาร” ที่คลุมเครือ เพียงตัวอย่างพร้อมคัดลอก‑วางครบชุด

## สิ่งที่คุณต้องมี

- **.NET 6** (หรือเวอร์ชัน .NET ล่าสุด) เวอร์ชันเก่าก็ใช้ได้ แต่โค้ดนี้เขียนให้ทำงานกับ .NET 6+
- **Aspose.OCR for .NET** – ติดตั้งผ่าน NuGet: `dotnet add package Aspose.OCR`.
- ตัวอย่างไฟล์ PNG (`text.png`) ที่มีข้อความชัดเจนและอ่านได้โดยเครื่อง
- IDE หรือ editor ที่คุณชอบ – Visual Studio, VS Code, Rider ฯลฯ

> **เคล็ดลับ:** หากต้องประมวลผลหลายภาพ ควรใช้ instance ของ `OcrEngine` เพียงอันเดียวแทนการสร้างใหม่ทุกไฟล์ จะช่วยลดภาระและเพิ่มอัตราการทำงาน

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์ c# ocr tutorial

เริ่มต้นด้วยการสร้างโปรเจกต์คอนโซล คำสั่งต่อไปนี้จะสร้างโครงสร้างพื้นฐานและดึงไลบรารี OCR เข้ามา:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

จากนั้นเปิดไฟล์ `Program.cs` ที่สร้างขึ้น เราจะเปลี่ยนเนื้อหาเป็นตัวอย่างเต็มในภายหลัง แต่ตอนนี้ให้ตรวจสอบว่าโปรเจกต์คอมไพล์ได้:

```bash
dotnet build
```

หากไม่มีข้อผิดพลาดใด ๆ คุณพร้อมจะดำเนินต่อ

## ขั้นตอนที่ 2: Recognize PNG Text from an Image

หัวใจของ **c# ocr tutorial** ใด ๆ คือ OCR engine เอง Aspose.OCR ซ่อนรายละเอียดระดับล่างและให้คลาส `OcrEngine` ที่ใช้งานง่าย ด้านล่างเราจะสร้าง engine, ชี้ไปที่ไฟล์ PNG, แล้วสั่งให้ทำการจดจำข้อความ

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### ทำไมวิธีนี้ถึงได้ผล

- **`RecognizeImage`** รองรับหลายรูปแบบ (PNG, JPEG, BMP) เรา **recognize png text** เพราะ PNG เก็บรายละเอียดแบบ lossless ทำให้เหมาะกับ OCR
- `OcrResult` ที่คืนค่ามาจะมีทั้งข้อความธรรมดาและคะแนนความเชื่อมั่นของแต่ละ glyph ซึ่งมีประโยชน์หากต้องกรองอักขระที่ความเชื่อมั่นต่ำในภายหลัง

## ขั้นตอนที่ 3: Write Indented JSON with JsonSerializer c#

เมื่อเรามี `ocrResult` แล้ว ขั้นตอนต่อไปใน **c# ocr tutorial** คือแปลงอ็อบเจกต์นี้เป็น JSON ที่มนุษย์อ่านได้ ตัวแปลง `System.Text.Json` ที่มาพร้อม .NET ทำหน้าที่นี้ได้ดี และเราจะตั้งค่าให้ **write indented json** เพื่อความชัดเจน

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### การใช้ `JsonSerializer` อย่างถูกต้อง

- ตัวเลือก `WriteIndented` เป็นวิธีที่ง่ายที่สุดในการ **write indented json** โดยไม่ต้องพึ่งไลบรารีภายนอก
- หากต้องการชื่อคุณสมบัติเป็น camelCase ให้เพิ่ม `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` ลงใน options
- สามารถบันทึกสตริง `jsonOutput` ด้วย `File.WriteAllText("result.json", jsonOutput);` – เป็นการปรับแต่งที่มีประโยชน์สำหรับ pipeline จริง

## ขั้นตอนที่ 4: Run and Verify the Output

คอมไพล์และรันโปรแกรม:

```bash
dotnet run
```

สมมติว่า `text.png` มีข้อความ *“Hello, OCR World!”* คุณควรเห็นผลลัพธ์ประมาณนี้:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

JSON ที่ได้ **indented** ทำให้อ่านง่ายในล็อกหรือส่งต่อให้บริการอื่นต่อไป

### Edge Cases & Tips

| สถานการณ์ | วิธีทำ |
|-----------|--------|
| **ภาพเบลอ** | เพิ่มค่า `ocrEngine.Config.Dpi` (เช่น `ocrEngine.Config.Dpi = 300`) ก่อนเรียก `RecognizeImage` |
| **ภาษาที่ไม่ใช่อังกฤษ** | ตั้งค่า `ocrEngine.Config.Language = OcrLanguage.German` (หรือภาษาอื่นที่รองรับ) |
| **ประมวลผลไฟล์จำนวนมาก** | วนลูปอ่านโฟลเดอร์โดยใช้ instance `OcrEngine` เดียว; เก็บผล JSON แต่ละไฟล์ด้วยชื่อไฟล์ที่ไม่ซ้ำ |
| **ต้องการข้อความที่มีความเชื่อมั่นสูงเท่านั้น** | กรอง `ocrResult.Lines` ที่ `Confidence` ≥ 0.95 ก่อนทำการ serialization |

## ตัวอย่างทำงานเต็มรูปแบบ (Copy‑Paste Ready)

ด้านล่างเป็นโปรแกรม *ทั้งหมด* ที่พร้อมวางลงใน `Program.cs` รวมทุกขั้นตอน การจัดการข้อผิดพลาด และคอมเมนต์ที่ทำให้โค้ดอ่านง่าย

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

รันโค้ด ตรวจสอบคอนโซลหรือไฟล์ `.json` ที่สร้างขึ้น คุณจะเห็นข้อความที่ดึงออกมาพร้อมคะแนนความเชื่อมั่น ทั้งหมดถูกจัด **indented** อย่างเรียบร้อย

## สรุป

คุณได้สร้าง **c# ocr tutorial** ที่แสดงวิธี **extract text image c#**, **recognize png text**, และ **write indented json** ด้วย `JsonSerializer` ตัวอย่างนี้สมบูรณ์ สามารถรันได้ทันที และรวมเคล็ดลับการใช้งานจริงไว้ด้วย  

ขั้นตอนต่อไป? ลองเปลี่ยน Aspose.OCR เป็น engine อื่น (เช่น Tesseract) แล้วดูว่าโครงสร้าง `OcrResult` เปลี่ยนอย่างไร หรือส่ง JSON ไปยัง API ที่เก็บข้อมูล OCR ลงฐานข้อมูล คุณยังสามารถทดลอง **use jsonserializer c#** กับตัวแปลงกำหนดเองสำหรับรูปแบบวันที่หรือการจัดการ enum ได้อีกด้วย

ขอให้เขียนโค้ดสนุกและ OCR pipeline ของคุณแม่นยำเสมอ!  

---  

![c# ocr tutorial diagram](image.png "Diagram illustrating OCR flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
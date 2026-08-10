---
category: general
date: 2026-03-02
description: เรียนรู้วิธีบันทึก JSON ขณะดึงข้อความจากภาพโดยใช้ Aspose OCR รวมถึงโค้ดการเขียนไฟล์
  JSON เคล็ดลับการโหลดภาพบิตแมพ และตัวอย่าง C# เต็มรูปแบบ
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: th
og_description: ค้นพบวิธีบันทึก JSON ขณะสกัดข้อความจากภาพด้วย Aspose OCR. โค้ด C#
  ฉบับเต็ม, ขั้นตอนการเขียนไฟล์ JSON, และเคล็ดลับเชิงปฏิบัติ.
og_title: วิธีบันทึก JSON จาก OCR ด้วย C# – บทเรียนการเขียนโปรแกรมเต็มรูปแบบ
tags:
- C#
- OCR
- Aspose
- JSON
title: วิธีบันทึก JSON จาก OCR ด้วย C# – คู่มือขั้นตอนเต็ม
url: /th/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีบันทึก JSON จาก OCR ใน C# – คู่มือขั้นตอนเต็ม

เคยสงสัย **วิธีบันทึก JSON** ที่มีข้อความที่คุณดึงมาจากรูปภาพหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาหลายคนเจออุปสรรคเมื่อต้อง *ดึงข้อความจากข้อมูลภาพ* แล้วบันทึกข้อมูลนั้นเป็นไฟล์ JSON ที่จัดรูปแบบอย่างเรียบร้อย ข่าวดีคือ? วิธีแก้ง่ายมากเมื่อคุณมีส่วนประกอบที่ถูกต้อง

ในบทเรียนนี้เราจะเดินผ่านสถานการณ์จริง: ใช้ Aspose.OCR เพื่อ **ดึงข้อความจากภาพ**, แล้ว **เขียนไฟล์ JSON** ผลลัพธ์, และสุดท้าย **วิธีบันทึก JSON** ลงดิสก์ ระหว่างทางเราจะสาธิตวิธี **โหลดวัตถุภาพ bitmap** อย่างถูกต้อง และครอบคลุมกรณีขอบที่คุณอาจเจอ เมื่อจบคุณจะได้แอปคอนโซล C# ที่ทำทุกอย่างตั้งแต่โหลดรูปภาพจนถึงสร้างเอกสาร JSON ที่พร้อมใช้งาน

## สิ่งที่คุณต้องเตรียม

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core และ .NET Framework ด้วย)
- Aspose.OCR for .NET (คุณสามารถดาวน์โหลดแพคเกจ NuGet ทดลองใช้ฟรี)
- ตัวอย่างภาพ PNG หรือ JPG ที่มีข้อความภาษาอังกฤษ
- Visual Studio, VS Code หรือ IDE ที่รองรับ C# ใดก็ได้

ไม่ต้องการไลบรารีเพิ่มเติม—เพียงแค่ใช้เนมสเปซมาตรฐาน `System.Drawing` สำหรับการจัดการ bitmap และ `System.Text.Json` สำหรับการแปลงเป็น JSON

---

## ขั้นตอนที่ 1 – โหลดภาพ Bitmap (ส่วน “load bitmap image”)

ก่อนที่ OCR จะทำงานใด ๆ คุณต้องโหลดภาพเข้าสู่หน่วยความจำเป็น `Bitmap` คิดว่าเป็นการเปิดหนังสือก่อนเริ่มอ่านหน้า

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **เคล็ดลับ:** หากภาพมีขนาดใหญ่ ให้พิจารณาเปลี่ยนขนาดก่อนเพื่อเพิ่มประสิทธิภาพ เครื่อง OCR ทำงานเร็วขึ้นกับภาพที่มีขนาดต่ำกว่า 2 MB

---

## ขั้นตอนที่ 2 – กำหนดค่า Aspose OCR Engine

เมื่อ bitmap พร้อมแล้ว เราต้องสร้าง `OcrEngine` วัตถุนี้รู้วิธี **ดึงข้อความจากภาพ** และอาจให้ข้อมูลเรขาคณิตเช่น bounding box

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

ทำไมต้องเปิด `ExportBoundingBoxes`? หากคุณต้องการไฮไลท์คำใน UI พิกัดเหล่านี้มีค่า หากไม่ต้องการก็ตั้งค่าเป็น `false` แล้ว JSON จะบางลงเล็กน้อย

---

## ขั้นตอนที่ 3 – ทำ OCR และรับผลลัพธ์ที่เป็นโครงสร้าง

เมื่อกำหนดค่า engine แล้ว ขั้นตอนต่อไปคือการทำ **how to extract text** จริง ๆ เมธอด `RecognizeToOcrResult` จะคืนอ็อบเจกต์ที่มีข้อความที่รับรู้, คะแนนความเชื่อมั่น, และข้อมูลเลย์เอาต์เสริม

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

ตัวแปร `ocrResult` ตอนนี้เก็บทุกอย่างที่คุณต้องการ หากตรวจสอบใน debugger คุณจะเห็นโครงสร้างของ `Page`, `Paragraph`, `Line`, และ `Word` แต่ละอันมีคุณสมบัติ `Text` ของตนเอง

---

## ขั้นตอนที่ 4 – แปลงผลลัพธ์เป็นสตริง JSON ที่จัดรูปแบบ

นี่คือจุดที่ **how to save json** เริ่มทำงานจริง เราจะใช้ `System.Text.Json` เพราะเป็นส่วนที่มาพร้อม .NET, เร็ว, และรองรับการพิมพ์สวยโดยอัตโนมัติ

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

หากต้องการรูปแบบการตั้งชื่ออื่น (เช่น camelCase) เพียงเพิ่ม `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` ลงใน options

---

## ขั้นตอนที่ 5 – เขียน JSON ลงดิสก์ (ขั้นตอน “write json file”)

สุดท้าย เราจะ **write JSON file** ไปยังระบบไฟล์ นี่คือคำตอบที่ชัดเจนสำหรับ **how to save json** ในสภาพแวดล้อม C#

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

หลังจากบรรทัดนี้ทำงานเสร็จ คุณจะพบไฟล์ `sample-page.json` ที่จัดรูปแบบอย่างสวยงามอยู่ข้างไฟล์ภาพต้นฉบับ เปิดด้วยโปรแกรมแก้ไขข้อความใดก็ได้หรือส่งต่อให้บริการอื่น—ข้อมูล OCR ของคุณพร้อมใช้งานแล้ว

---

## ขั้นตอนที่ 6 – ตรวจสอบผลลัพธ์ (คุณควรเห็นอะไร?)

การรันโปรแกรมควรพิมพ์ข้อความสั้น ๆ ยืนยันบนคอนโซล:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

เปิดไฟล์ JSON ที่สร้างขึ้นและคุณจะเห็นประมาณนี้:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

หากตั้งค่า `ExportBoundingBoxes` เป็น true แต่ละคำจะมีพิกัด `Rectangle` ด้วย ซึ่งสะดวกสำหรับงาน UI ต่อไป

---

## คำถามทั่วไป & กรณีขอบ

### ถ้าเส้นทางภาพไม่ถูกต้องจะทำอย่างไร?

ห่อการโหลด bitmap ด้วยบล็อก `try/catch` แล้วแสดงข้อผิดพลาดที่ชัดเจน:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### จะจัดการกับภาษาที่ไม่ใช่ภาษาอังกฤษอย่างไร?

เพียงเปลี่ยนคุณสมบัติ `Language`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose รองรับมากกว่า 50 ภาษา เลือกภาษาที่ตรงกับแหล่งข้อมูลของคุณ

### จำเป็นต้องทำลายวัตถุ `Bitmap` หรือไม่?

ต้องทำครับ `Bitmap` implements `IDisposable` ดังนั้นห่อด้วย `using` เพื่อปล่อยทรัพยากรเนทีฟโดยเร็ว

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### อยากได้ JSON แบบกะทัดรัดโดยไม่มีการเยื้องบรรทัดจะทำอย่างไร?

สลับ `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

จะลดขนาดไฟล์—เหมาะกับสถานการณ์ที่แบนด์วิธจำกัด

---

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมเต็มที่รวมทุกขั้นตอน, การจัดการข้อผิดพลาด, และเคล็ดลับตามแนวปฏิบัติที่กล่าวไว้ บันทึกเป็น `Program.cs` แล้วรันจากคอมมานด์ไลน์หรือ IDE ของคุณ

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**สิ่งที่ทำ:**  
1. ตรวจสอบว่าภาพมีอยู่จริง  
2. โหลดอย่างปลอดภัยด้วยบล็อก `using`  
3. รัน OCR เพื่อ **ดึงข้อความจากภาพ**  
4. แปลงผลลัพธ์เป็นสตริง JSON ที่จัดรูปแบบอย่างสวยงาม  
5. บันทึกสตริงนั้นลงดิสก์ ตอบคำถามหลัก **how to save json**

รัน `dotnet run` (หรือกด F5 ใน Visual Studio) คุณจะเห็นข้อความยืนยันเมื่อไฟล์ถูกเขียนเสร็จ

---

## สรุป

ตอนนี้คุณมีสูตรครบวงจรพร้อมใช้งานสำหรับ **how to save JSON** ที่มาจากการดึงข้อความด้วย OCR ตั้งแต่การโหลด bitmap ไปจนถึงการเขียนไฟล์ JSON ที่สะอาด ทุกขั้นตอนมีการอธิบาย “ทำไม” ของโค้ด เพื่อให้คุณปรับใช้กับโปรเจกต์ของตนเองได้  

หากอยากสำรวจต่อไป ลองพิจารณา:

- **วิธีดึงข้อความ** จาก PDF โดยแปลงแต่ละหน้าเป็นภาพก่อน  
- ใช้ข้อมูล bounding‑box เพื่อไฮไลท์คำใน UI ของ WPF หรือ WinForms  
- ส่ง JSON โดยตรงไปยัง Web API แทนการบันทึกไฟล์ (ใช้ `HttpClient`)

ลองทำ ปรับแต่งตัวเลือกต่าง ๆ แล้วให้ข้อมูล OCR เติมเต็มแอปพลิเคชันของคุณ หากมีคำถามคอมเมนต์ไว้ได้เลย และขอให้เขียนโค้ดอย่างสนุกสนาน!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
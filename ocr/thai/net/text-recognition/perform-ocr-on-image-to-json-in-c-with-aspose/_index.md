---
category: general
date: 2026-04-08
description: เรียนรู้วิธีทำ OCR บนรูปภาพและเขียนไฟล์ JSON ด้วย C# โดยใช้ Aspose OCR.
  บทเรียน Aspose OCR C# นี้แสดงการแปลงภาพ OCR เป็น JSON พร้อมค่าความมั่นใจ.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: th
og_description: ทำการ OCR บนรูปภาพและส่งออกผลลัพธ์เป็นไฟล์ JSON ด้วย C# บทเรียนนี้ครอบคลุมกระบวนการทำงานของ
  Aspose OCR C# อย่างเต็มรูปแบบ รวมถึงคะแนนความมั่นใจด้วย
og_title: ทำ OCR บนรูปภาพเป็น JSON ใน C# – คู่มือ Aspose OCR
tags:
- Aspose
- OCR
- C#
- JSON
title: ทำ OCR บนรูปภาพเป็น JSON ด้วย C# และ Aspose
url: /th/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพเป็น JSON ใน C# ด้วย Aspose

เคยต้องการ **ทำ OCR บนรูปภาพ** แต่ไม่แน่ใจว่าจะนำผลลัพธ์ไปใส่ในรูปแบบที่เป็นโครงสร้างได้อย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนามักถามว่า “จะเปลี่ยนภาพสแกนให้เป็นข้อมูลที่ใช้ได้อย่างไร?” ข่าวดีคือ Aspose.OCR ทำให้เรื่องนี้ง่ายมาก และคุณยังสามารถ **เขียนไฟล์ JSON แบบ C#**‑style พร้อมคะแนนความเชื่อมั่นได้อีกด้วย.

ในคู่มือนี้เราจะพาคุณผ่าน **aspose OCR C# tutorial** อย่างครบถ้วน ซึ่งครอบคลุมทุกอย่างตั้งแต่การโหลดรูปภาพจนถึงการส่งออกข้อความที่ได้รับการจดจำเป็น JSON. เมื่อเสร็จคุณจะมีแอปคอนโซลที่สามารถ **ทำ OCR บนรูปภาพ**, แปลงผลลัพธ์เป็น JSON (รวมถึงค่าความเชื่อมั่น) และบันทึกด้วยบรรทัดโค้ดเดียว. ไม่มีขั้นตอนที่ซ่อนอยู่, ไม่มีสคริปต์ภายนอก—เพียงแค่ C# แท้.

## ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK หรือเวอร์ชันใหม่กว่า (โค้ดทำงานได้กับ .NET Core และ .NET Framework ด้วยเช่นกัน)
- Visual Studio 2022 (หรือโปรแกรมแก้ไขใดก็ได้ที่คุณชอบ)
- ใบอนุญาต **Aspose.OCR for .NET** ที่ถูกต้องหรือใบอนุญาตชั่วคราวฟรี (รุ่นทดลองฟรีใช้สำหรับการทดสอบได้)
- ไฟล์รูปภาพ (`input.png`) ที่คุณต้องการประมวลผล (รูปแบบทั่วไปใดก็ได้—PNG, JPG, BMP—ก็ใช้ได้)

เท่านี้ก็เรียบร้อยแล้ว. หากคุณขาดสิ่งใดสิ่งหนึ่งใด, ให้ดาวน์โหลดทันที; ส่วนที่เหลือของคู่มือจะสมมติว่ามีพร้อมแล้ว.

## ขั้นตอนที่ 1: ติดตั้งแพคเกจ Aspose.OCR NuGet

เริ่มต้นกันเลย—เพิ่มไลบรารีนี้เข้าในโปรเจกต์ของคุณ. เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์และรัน:

```bash
dotnet add package Aspose.OCR
```

คำสั่งนี้จะดึงเวอร์ชันล่าสุด (ณ เมษายน 2026 คือ 23.12) และเพิ่ม DLL ที่จำเป็นลงในโฟลเดอร์ `bin`. ไม่ต้องกำหนดค่าเพิ่มเติมใด ๆ.

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine (ทำ OCR บนรูปภาพ)

ตอนนี้เราจะสร้างอินสแตนซ์ของ `OcrEngine` และระบุภาษาที่จะใช้. ภาษาอังกฤษ (`"en"`) เป็นภาษาที่ใช้บ่อยที่สุด, แต่คุณสามารถเปลี่ยนเป็น `"fr"`, `"de"` หรือภาษาอื่นที่รองรับได้.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**ทำไมเราต้องเริ่มต้นที่นี่:** `OcrEngine` เก็บการตั้งค่าทั้งหมดที่จำเป็นสำหรับกระบวนการจดจำ. การกำหนดภาษาล่วงหน้าช่วยให้เอนจินใช้ชุดอักขระที่ถูกต้อง, ซึ่งทำให้ความแม่นยำเพิ่มขึ้นอย่างมาก.

## ขั้นตอนที่ 3: จดจำรูปภาพและจับคะแนนความเชื่อมั่น

เมื่อเอนจินพร้อม, เราจะส่งไฟล์รูปภาพให้มัน. เมธอด `RecognizeImage` จะคืนค่าอ็อบเจกต์ `OcrResult` ที่มีทั้งข้อความที่สกัดและคะแนนความเชื่อมั่นสำหรับแต่ละคำ.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**อะไรที่เกิดขึ้นเบื้องหลัง?** Aspose ใช้ตัวจดจำที่อิงจากเครือข่ายประสาทเทียมที่วิเคราะห์บล็อกพิกเซลแต่ละบล็อก, เปรียบเทียบกับโมเดลภาษาของมัน, และแนบค่าความเชื่อมั่น (0‑100) ที่บอกว่ามั่นใจแค่ไหนกับแต่ละคำ.

## ขั้นตอนที่ 4: แปลงผลลัพธ์เป็น JSON (OCR Image to JSON)

Aspose ทำให้การแปลงเป็นเรื่องง่าย. โดยการส่ง `includeConfidence: true` เราจะได้ payload JSON ที่มีลักษณะดังนี้:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

นี่คือโค้ดที่สร้างสตริง JSON:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**ทำไมต้องรวมคะแนนความเชื่อมั่น?** หากคุณตั้งใจจะส่งข้อมูลนี้ต่อไปยังกระบวนการต่อเนื่อง (เช่น การตรวจสอบ, การไฮไลท์ UI), การรู้ว่าคำใดไม่มั่นคงจะช่วยให้คุณตัดสินใจว่าจะขอการยืนยันจากผู้ใช้หรือไม่.

## ขั้นตอนที่ 5: เขียนไฟล์ JSON แบบ C#‑Style

ตอนนี้เราจะ **เขียนไฟล์ JSON แบบ C#** จริง ๆ. เมธอด `File.WriteAllText` ทำงานแบบอะตอมิกและทำงานข้ามแพลตฟอร์ม, ทำให้เหมาะสำหรับแอปคอนโซล.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

นี่คือเวิร์กโฟลว์ทั้งหมด—ห้าขั้นตอนสั้น ๆ ที่ **ทำ OCR บนรูปภาพ**, แปลงผลลัพธ์เป็น JSON, และบันทึกไว้.

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน `Program.cs`. ตรวจสอบให้แน่ใจว่า `input.png` อยู่ในโฟลเดอร์เดียวกับไบนารีที่คอมไพล์หรือปรับเส้นทางให้เหมาะสม.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรันโปรแกรม (`dotnet run`), คุณจะเห็นผลลัพธ์ประมาณนี้:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

และ `output.json` จะมี JSON ที่มีโครงสร้างตามที่แสดงก่อนหน้านี้, พร้อมเปอร์เซ็นต์ความเชื่อมั่นสำหรับแต่ละคำ.

## เคล็ดลับระดับมืออาชีพ & กรณีขอบ

- **การจัดการไฟล์ที่หายไป:** ห่อการเรียก `RecognizeImage` ด้วย `try/catch` สำหรับ `FileNotFoundException` หากคุณคาดว่าจะมีเส้นทางแบบไดนามิก.
- **หลายภาษา:** ตั้งค่า `ocrEngine.Language = "fr"` สำหรับภาษาฝรั่งเศส, หรือโหลดแพ็คเกจภาษาที่กำหนดเองผ่าน `ocrEngine.LoadLanguage("custom.lang")`.
- **เอกสารขนาดใหญ่:** สำหรับ PDF หลายหน้า, ให้แปลงแต่ละหน้ามาเป็นรูปภาพก่อน (เช่น ใช้ `Aspose.PDF`) แล้ววนลูปผ่านขั้นตอน OCR.
- **การปรับประสิทธิภาพ:** หากคุณต้องการผลลัพธ์อย่างรวดเร็ว, ให้สลับเป็น `RecognitionMode.Fast`—คุณจะเสียความแม่นยำเล็กน้อยแต่ได้ความเร็วเพิ่ม.
- **การจัดรูปแบบ JSON:** ต้องการ JSON ที่จัดรูปแบบสวยงาม? ใช้ `JsonConvert.SerializeObject` จาก Newtonsoft พร้อม `Formatting.Indented` หลังจากทำการ deserialize สตริง JSON ของ Aspose.

## คำถามที่พบบ่อย

**ถาม: นี้ทำงานกับ .NET Framework หรือไม่?**  
A: แน่นอน. แพคเกจ NuGet เดียวกันนี้รองรับ .NET Standard 2.0, ดังนั้นคุณสามารถอ้างอิงจาก .NET Framework 4.6.1 ขึ้นไปได้.

**ถาม: ถ้าฉันต้องการคะแนนความเชื่อมั่นของทั้งเอกสาร ไม่ใช่ต่อคำ?**  
A: `OcrResult` ยังเปิดเผย `OverallConfidence`. คุณสามารถเพิ่มมันด้วยตนเองลงใน JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**ถาม: ฉันสามารถสตรีม JSON ตรงไปยังเว็บ API ได้หรือไม่?**  
A: ได้. แทนที่ `File.WriteAllText` ด้วยการ POST ของ `HttpClient` ที่ส่ง `jsonResult`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
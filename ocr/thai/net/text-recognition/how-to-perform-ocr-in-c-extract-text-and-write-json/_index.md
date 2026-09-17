---
category: general
date: 2026-02-09
description: เรียนรู้วิธีทำ OCR ใน C# เพื่อดึงข้อความจากภาพ, จดจำข้อความจาก PNG, และเขียนไฟล์
  JSON ด้วย C# อย่างรวดเร็ว.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: th
og_description: ทำ OCR ใน C# อย่างไร? ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อดึงข้อความจากภาพ,
  จำแนกข้อความจาก PNG, และเขียนไฟล์ JSON ด้วย C# อย่างมีประสิทธิภาพ.
og_title: วิธีทำ OCR ใน C# – ดึงข้อความและเขียนเป็น JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: วิธีทำ OCR ด้วย C# – แยกข้อความและเขียนเป็น JSON
url: /th/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ใน C# – คู่มือฉบับสมบูรณ์

การทำ OCR ใน C# เป็นอุปสรรคทั่วไปเมื่อคุณต้องการ **extract text from image** ไฟล์ ในคู่มือนี้เราจะอธิบายการจดจำข้อความจาก PNG, การส่งออกผลลัพธ์โดยละเอียดเป็นสตริง JSON, และสุดท้าย **write JSON file C#** แบบ. เคยมองแบบฟอร์มที่สแกนแล้วสงสัยว่าจะเปลี่ยนเส้นขีดเหล่านั้นให้เป็นข้อความที่ค้นหาได้อย่างไรไหม? คุณไม่ได้อยู่คนเดียว; นักพัฒนาหลายคนเจอปัญหานี้ตั้งแต่ต้น.

เราจะใช้ไลบรารี Aspose.OCR เพราะมันให้ความมั่นใจต่อสัญลักษณ์โดยอัตโนมัติและทำงานร่วมกับโปรเจกต์ .NET 6+ ได้อย่างราบรื่น. เมื่อจบบทเรียนนี้คุณจะมีแอปคอนโซลพร้อมใช้งานที่โหลด PNG, ดึงอักขระทุกตัว, และบันทึกไฟล์ JSON ที่เรียบร้อยซึ่งคุณสามารถส่งต่อไปยังฐานข้อมูลหรือโมเดล AI. ไม่มีทางลัด “ดูเอกสาร” ที่เป็นความลับ—เพียงโซลูชันที่สมบูรณ์ในตัว.

## สิ่งที่คุณต้องการ

- **.NET 6 SDK** (หรือรุ่นต่อไป) – เวอร์ชัน LTS ปัจจุบันในขณะเขียน.
- **Aspose.OCR for .NET** NuGet package – `Install-Package Aspose.OCR`.
- รูป PNG ที่คุณต้องการสแกน (เช่น `form.png`).  
- IDE หรือ editor – Visual Studio, VS Code, Rider – สิ่งที่คุณสะดวกใช้.

เท่านี้เอง. หากคุณมีส่วนเหล่านี้ครบ คุณก็พร้อมเริ่ม.

![ภาพประกอบการทำ OCR แสดงแอปคอนโซล C# ที่ประมวลผล PNG](ocr-example.png "วิธีทำ OCR ใน C#")

*Image alt text: how to perform OCR illustration showing a C# console app processing a PNG.*

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่ม Dependencies

แรกเริ่ม สร้างโปรเจกต์คอนโซลใหม่และดึงไลบรารี Aspose OCR เข้ามา.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Pro tip:** ใช้ flag `--framework net6.0` หากคุณต้องการล็อก target framework อย่างชัดเจน.

ทำไมขั้นตอนนี้สำคัญ: NuGet package มีคลาส `OcrEngine`, `ImageStream`, และ `JsonExporter` ที่เราจะพึ่งพา. หากไม่มีมัน, คอมไพเลอร์จะไม่รู้ว่า “OCR” คืออะไร.

## ขั้นตอนที่ 2: เขียน Core OCR Logic

เปิด `Program.cs` (หรือสร้างไฟล์ใหม่) และแทนที่เนื้อหาด้วยโค้ดต่อไปนี้. แต่ละส่วนมีคอมเมนต์เพื่อให้คุณเห็นเหตุผลที่อยู่เบื้องหลัง.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### ทำไมแต่ละส่วนจึงสำคัญ

- **OcrEngine**: คิดว่าเป็นสมองของกระบวนการ. มันโหลดโมเดลภาษาและตั้งค่า pipeline การ inference.
- **ImageStream.FromFile**: จัดการกับ PNG, JPEG, BMP ฯลฯ ทั้งหมด. มันแยกความซับซ้อนของ file‑I/O ออก.
- **RecognitionResult**: เก็บข้อความดิบพร้อมคะแนนความมั่นใจ. ที่นี่คุณจะได้ข้อมูลละเอียดที่ต้องการสำหรับการตรวจสอบต่อไป.
- **JsonExporter**: แปลง `RecognitionResult` ที่เต็มไปด้วยข้อมูลให้เป็น payload JSON ที่เรียบร้อย, เหมาะสำหรับ API.
- **File.WriteAllText**: วิธี .NET ที่ตรงไปตรงมาสำหรับ **write JSON file C#** โดยไม่ต้องพึ่งพา dependencies เพิ่มเติม.

## ขั้นตอนที่ 3: รันแอปพลิเคชันและตรวจสอบผลลัพธ์

คอมไพล์และรันโปรแกรม:

```bash
dotnet run
```

คุณควรเห็นข้อความคอนโซลคล้ายกับ:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

เปิด `form.json` – คุณจะพบสิ่งที่คล้ายกับ:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

ขั้นตอน **extract text from image** สำเร็จ, และตอนนี้คุณมีการแทนค่า JSON ที่เครื่องอ่านได้ของทุกอักขระ.

## ขั้นตอนที่ 4: จัดการกับ Edge Cases ที่พบบ่อย

### ไฟล์หายหรือเสียหาย

หากเส้นทาง PNG ผิด, `ImageStream.FromFile` จะโยน `FileNotFoundException`. ห่อโค้ดการโหลดด้วยบล็อก try‑catch:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### คะแนนความมั่นใจต่ำ

บางครั้ง OCR จะให้คะแนนความมั่นใจต่ำสำหรับสแกนที่มีสัญญาณรบกวน. คุณสามารถกรองสัญลักษณ์ก่อนส่งออกได้:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

สิ่งนี้ทำให้ JSON มีเฉพาะอักขระที่เชื่อถือได้ระดับหนึ่ง—มีประโยชน์เมื่อคุณส่งข้อมูลเข้าสู่ pipeline การตรวจสอบต่อไป.

### ไฟล์ขนาดใหญ่และหน่วยความจำ

การประมวลผล PNG ขนาดหลายเมกะไบต์อาจทำให้การใช้หน่วยความจำพุ่งสูง. พิจารณา stream รูปภาพเป็นชิ้นส่วนหรือใช้ `OcrEngine.RecognizeAsync` (มีในเวอร์ชัน Aspose ใหม่) เพื่อให้ UI ตอบสนองได้.

## ขั้นตอนที่ 5: ขยายโซลูชัน (ทางเลือก)

- **Batch processing**: วนลูปผ่านไดเรกทอรีของ PNGs และสร้าง JSON ที่ตรงกันสำหรับแต่ละไฟล์.
- **Database storage**: แทรก JSON ลงในคอลัมน์ SQL `NVARCHAR(MAX)` เพื่อการวิเคราะห์ในภายหลัง.
- **Language selection**: ตั้งค่า `ocrEngine.Language = OcrLanguage.Spanish;` หากคุณต้องการสนับสนุนภาษาที่ไม่ใช่อังกฤษ.

ส่วนขยายทั้งหมดนี้ทำตามรูปแบบ **how to perform OCR** ที่เรากำหนด—initialize, recognize, export, และ persist.

## คำถามที่พบบ่อย

**Q: ทำงานกับ JPG หรือ TIFF ได้ไหม?**  
A: แน่นอน. `ImageStream.FromFile` ตรวจจับรูปแบบโดยอัตโนมัติ, ดังนั้นคุณสามารถแทนที่ PNG ด้วยรูปภาพ raster ที่รองรับใดก็ได้.

**Q: ถ้าต้องการ extract text from a PDF จะทำอย่างไร?**  
A: แปลงแต่ละหน้าของ PDF เป็นภาพก่อน (เช่น ใช้ `Aspose.PDF`) แล้วจึงส่ง PNG เข้าไปในกระบวนการ OCR ที่อธิบายไว้ที่นี่.

**Q: สามารถรับผลลัพธ์ OCR เป็น XML แทน JSON ได้ไหม?**  
A: ได้. Aspose.OCR ยังมี `XmlExporter`. เปลี่ยน `JsonExporter` เป็น `XmlExporter` และปรับนามสกุลไฟล์.

## สรุป

เราได้อธิบาย **how to perform OCR** ใน C# ตั้งแต่ต้นจนจบ, แสดงให้คุณเห็นวิธี **extract text from image**, **recognize text from PNG**, และ **write JSON file C#** อย่างไม่มีอุปสรรค. ตัวอย่างที่สมบูรณ์และสามารถรันได้อยู่ในโค้ดสแนปด้านบน, และตอนนี้คุณเข้าใจเหตุผลของแต่ละขั้นตอน—การเริ่มต้น engine, การจัดการ edge cases, และการบันทึกผลลัพธ์.

ต่อไปคุณอาจสำรวจ pipeline OCR แบบ batch, ผสานผลลัพธ์ JSON กับ Azure Cognitive Search, หรือทดลองโมเดลภาษาที่กำหนดเอง. ไม่มีขีดจำกัดเมื่อคุณเชี่ยวชาญพื้นฐานของ OCR ใน C#.

หากคุณเจอปัญหาใดหรือมีไอเดียสำหรับการขยายเพิ่มเติม, ฝากคอมเมนต์ด้านล่าง. โค้ดให้สนุก, และสนุกกับการเปลี่ยนสแกนพิกเซลเป็นข้อมูลที่สะอาดและค้นหาได้!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
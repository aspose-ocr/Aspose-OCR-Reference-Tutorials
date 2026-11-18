---
category: general
date: 2026-03-26
description: จดจำข้อความจากไฟล์ png และดึงข้อมูลใบเสร็จโดยใช้ Aspose OCR ใน C#. แปลงภาพเป็น
  JSON‑L และประมวลผลใบเสร็จด้วย OCR ในตัวอย่างที่สมบูรณ์.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: th
og_description: จดจำข้อความจาก PNG และแปลงใบเสร็จเป็น JSON‑L ด้วย Aspose OCR ใน C#.
  โค้ดและเคล็ดลับเต็มขั้นตอน
og_title: จดจำข้อความจาก PNG – คู่มือ Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: แยกข้อความจาก PNG – บทเรียน Aspose OCR C# JSON‑L
url: /th/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจาก png – คู่มือ Aspose OCR C# เต็มรูปแบบ

เคยต้อง **จดจำข้อความจากไฟล์ png** แต่ไม่แน่ใจว่าห้องสมุดใดจะให้ผลลัพธ์ที่สะอาดและเป็นบรรทัดต่อบรรทัดหรือไม่? คุณไม่ได้อยู่คนเดียว ในแอปธุรกิจขนาดเล็กหลาย ๆ ตัว ใบเสร็จจะอยู่ในรูปภาพ PNG และการดึงจำนวนเงิน วันที่ หรือชื่อผู้ขายออกมานั้นเป็นปัญหาประจำวัน  

ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของ C# และห้องสมุด **Aspose OCR** คุณสามารถ **ดึงข้อความจากใบเสร็จ** แล้ว **แปลงภาพเป็น jsonl** เพื่อการวิเคราะห์ต่อไปได้ ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด—โหลด PNG, รัน OCR, และเขียนแต่ละบรรทัดลงไฟล์ JSON‑L—เพื่อให้คุณ **ประมวลผลใบเสร็จด้วย OCR** ได้ทันที

เราจะครอบคลุมทุกอย่างที่คุณต้องการ: แพ็คเกจ NuGet ที่จำเป็น, โปรแกรมที่สามารถรันได้เต็มรูปแบบ, คำอธิบายว่าทำไมแต่ละขั้นตอนถึงสำคัญ, และเคล็ดลับปฏิบัติที่คุณจะชื่นชอบเมื่อใบเสร็จเริ่มยุ่งยาก ไม่ต้องอ้างอิงเอกสารภายนอก; เพียงคัดลอก‑วาง, รัน, และปรับแต่ง

---

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **จดจำข้อความจาก png** ด้วย `Aspose.OCR`
- วิธี **ดึงข้อความจากใบเสร็จ** เป็นอ็อบเจ็กต์บรรทัดและจับคะแนนความเชื่อมั่น
- วิธี **แปลงภาพเป็น jsonl** เพื่อให้แต่ละบรรทัด OCR กลายเป็นอ็อบเจ็กต์ JSON แยกกัน
- วิธี **ประมวลผลใบเสร็จด้วย OCR** ตั้งแต่ต้นจนจบ, จัดการกรณีขอบเช่นภาพว่างหรือบรรทัดที่ความเชื่อมั่นต่ำ
- เคล็ดลับการแก้ปัญหา OCR ที่พบบ่อยและการปรับปรุงความแม่นยำ

### ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core และ .NET Framework ด้วย)
- Visual Studio 2022 หรือ IDE ที่คุณชอบ
- ใบอนุญาต Aspose OCR ที่ถูกต้อง (คุณสามารถเริ่มต้นด้วยใบอนุญาตชั่วคราวฟรีจาก Aspose.com)
- ตัวอย่างใบเสร็จที่บันทึกเป็น `receipt.png` ในโฟลเดอร์ที่คุณควบคุม

---

## ขั้นตอนที่ 1: จดจำข้อความจาก png ด้วย Aspose OCR

สิ่งแรกที่เราต้องการคือ `OcrEngine` ที่ถูกกำหนดค่าแล้ว วัตถุนี้เก็บการตั้งค่าเครื่องมือ OCR (ภาษา, โหมดการตรวจจับ ฯลฯ) โดยค่าเริ่มต้นจะใช้ภาษาอังกฤษและตรวจจับโครงสร้างหน้าอัตโนมัติ ซึ่งทำงานได้ดีสำหรับใบเสร็จส่วนใหญ่

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**ทำไมจึงสำคัญ:**  
`OcrEngine` เป็นส่วนที่ทำงานหนัก; การสร้างมันเพียงครั้งเดียวและนำไปใช้ซ้ำกับหลายภาพจะลดการใช้หน่วยความจำ หากคุณต้องการภาษาอื่น (เช่น ใบเสร็จสเปน) คุณสามารถตั้งค่า `ocrEngine.Language = OcrLanguage.Spanish;` ก่อนเรียก `Recognize`

---

## ขั้นตอนที่ 2: ดึงข้อความจากบรรทัดใบเสร็จ

`OcrResult` มีคอลเลกชันชื่อ `Lines` แต่ละบรรทัดจะเก็บข้อความดิบและคะแนนความเชื่อมั่น (0‑100) การดึงข้อมูลเหล่านี้ออกมาจะให้คุณควบคุมได้ละเอียด—you สามารถละทิ้งบรรทัดที่ความเชื่อมั่นต่ำหรือทำเครื่องหมายให้ตรวจสอบด้วยตนเอง

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**ทำไมต้องหลีกเลี่ยง JSON:**  
ข้อความในใบเสร็จอาจมีเครื่องหมายอัญประกาศ (`"`) หรือแบ็คสแลช (`\`) ที่จะทำให้สตริง JSON ธรรมดาเสียหาย วิธี `EscapeJson` รับประกันว่าบรรทัด JSON จะถูกต้อง

**ผลลัพธ์ที่ได้จะเป็นอย่างไร:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

แต่ละบรรทัดเป็นเรคคอร์ดแยกกัน เหมาะสำหรับสตรีมเข้าสู่ data lake หรือป้อนโมเดล machine‑learning

---

## ขั้นตอนที่ 3: แปลงภาพเป็น JSONL – จัดการกรณีขอบ

เมื่อคุณประมวลผลชุดใบเสร็จหลายใบ บางภาพอาจเป็นภาพว่าง, เสียหาย, หรือมีคะแนนความเชื่อมั่นต่ำมาก ให้ทำให้ pipeline แข็งแรงขึ้นเล็กน้อย

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**ทำไมต้องกรอง:**  
ใบเสร็จที่พิมพ์บนกระดาษซีดอาจให้ตัวอักษรแปลก ๆ ที่ความเชื่อมั่นต่ำ การตัดทอนทุกอย่างที่ต่ำกว่า 80 % มักจะลบสัญญาณรบกวนออกได้โดยไม่กระทบข้อมูลที่มีประโยชน์

---

## ขั้นตอนที่ 4: ประมวลผลใบเสร็จด้วย OCR – ตัวอย่างครบวงจร

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรม **พร้อมรันเต็มรูปแบบ** แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่เก็บไฟล์ PNG ของคุณ

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**วิธีรันโค้ด:**  
1. เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์  
2. `dotnet add package Aspose.OCR` – ติดตั้งห้องสมุด  
3. `dotnet run` – คุณจะเห็นข้อความสำเร็จและไฟล์ `receipt.jsonl` ปรากฏขึ้น

**ผลลัพธ์ที่คาดหวัง:** ไฟล์ JSON ที่คั่นด้วยบรรทัด ซึ่งแต่ละบรรทัดสอดคล้องกับบรรทัดในใบเสร็จ พร้อมคะแนนความเชื่อมั่น ตอนนี้คุณสามารถส่งไฟล์นี้ต่อไปยัง Power BI, Elastic, หรือเครื่องมือวิเคราะห์ใด ๆ ที่รองรับ JSON‑L

---

## ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

| ปัญหา | สาเหตุ | วิธีแก้เร็ว |
|-------|--------|-------------|
| **ผลลัพธ์เป็นค่าว่าง** | เส้นทางไฟล์ผิดหรือไฟล์ไม่ใช่ PNG | ตรวจสอบเส้นทางอีกครั้ง, ใช้ `File.Exists(imagePath)` |
| **อักขระแปลก** | DPI ต่ำหรือ PNG ถูกบีบอัดมาก | ใช้สแกนที่ความละเอียดอย่างน้อย 300 dpi; หลีกเลี่ยงการบีบอัด JPEG อย่างรุนแรง |
| **บรรทัดความเชื่อมั่นต่ำมาก** | ใบเสร็จพิมพ์บนกระดาษความร้อนที่ซีด | เพิ่มค่า `minConfidence` หรือทำการประมวลผลภาพล่วงหน้า (คอนทราสต์/threshold) |
| **ข้อผิดพลาดการพาร์ส JSON** | มีอัญประกาศที่ไม่ได้ escape ในข้อความใบเสร็จ | รักษาเมธอด `EscapeJson` หรือเปลี่ยนไปใช้ `System.Text.Json` เพื่อการซีเรียลไลซ์ที่แข็งแรง |

**เคล็ดลับระดับมืออาชีพ:** หากต้องการดึงฟิลด์เฉพาะ (เช่น ยอดรวม) ให้รัน regex ง่าย ๆ บน `line.Text` หลังจากที่คุณมีไฟล์ JSON‑L นี้ วิธีนี้ทำให้ OCR แยกออกจากตรรกะธุรกิจและทำให้การดีบักง่ายขึ้น

---

## การขยายโซลูชัน

- **ประมวลผลเป็นชุด:** ห่อโลจิก `Main` ไว้ใน `foreach` เพื่อวนลูปไฟล์ PNG ทั้งหมดในไดเรกทอรี
- **รองรับหลายภาษา:** ตั้งค่า `ocrEngine.Language = OcrLanguage.Spanish;` (หรือภาษาอื่นที่สนับสนุน) ก่อน `Recognize`
- **ผลลัพธ์แบบโครงสร้าง:** แทนการใช้ JSON บรรทัดต่อบรรทัด, สร้างอ็อบเจ็กต์ `Receipt` ที่มีคุณสมบัติ `Date`, `Merchant`, `Total` แล้วซีเรียลไลซ์ครั้งเดียว

ทุกการเปลี่ยนแปลงเหล่านี้ยังคง **แปลงภาพเป็น jsonl** เป็นแกนหลัก, ดังนั้นคุณสามารถสลับผู้บริโภค downstream ได้โดยไม่ต้องแก้ไขส่วน OCR

---

## สรุป

เราได้แสดงวิธี **จดจำข้อความจาก png** ด้วย Aspose OCR, **ดึงข้อความจากใบเสร็จ**, และ **แปลงภาพเป็น jsonl** เพื่อการประมวลผลต่อไปอย่างง่ายดาย โปรแกรม C# ที่สมบูรณ์และอิสระแสดงขั้นตอนทั้งหมด—from การโหลด PNG, การจัดการกรณีขอบ, ถึงการเขียนไฟล์ JSON‑L ที่สะอาด—เพื่อให้คุณสามารถ **ประมวลผลใบเสร็จด้วย OCR** ในโปรเจกต์ของคุณได้ทันที

ลองใช้กับใบเสร็จตัวอย่างหลายใบ, ปรับค่า threshold ของความเชื่อมั่น, แล้วคุณจะเห็นว่ากองภาพที่รกกลายเป็นข้อมูลโครงสร้างพร้อมวิเคราะห์ได้เร็วแค่ไหน เมื่อคุณคุ้นเคยแล้ว, ลองทำ batch processing หรือเพิ่มโมเดล ML เล็ก ๆ เพื่อจำแนกประเภทค่าใช้จ่ายโดยอัตโนมัติ

มีคำถามหรือพบวิธีปรับปรุงที่เจ๋ง? แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-17
description: เรียนรู้วิธีแยกวิเคราะห์ JSON จากผลลัพธ์ OCR ด้วย C# บทเรียนนี้ครอบคลุมวิธีดึงข้อความ,
  โหลดภาพสำหรับ OCR, รันการจดจำ OCR, และใช้เครื่องมือ OCR ใน C# อย่างมีประสิทธิภาพ.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: th
og_description: วิธีแยกวิเคราะห์ JSON จากผลลัพธ์ OCR ใน C#. ปฏิบัติตามคู่มือของเราเพื่อดึงข้อความ,
  โหลดภาพสำหรับ OCR, รันการจดจำ OCR, และใช้ OCR engine ใน C#
og_title: วิธีแยกวิเคราะห์ JSON ด้วย OCR Engine C# – บทเรียนเต็ม
tags:
- C#
- OCR
- JSON
- Image Processing
title: วิธีแยกวิเคราะห์ JSON ด้วย OCR Engine C# – คู่มือขั้นตอนเต็ม
url: /th/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแยกวิเคราะห์ JSON ด้วย OCR Engine C# – คู่มือขั้นตอนเต็ม

เคยสงสัย **วิธีแยกวิเคราะห์ json** ที่ได้มาจาก OCR engine หรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหานี้—นักพัฒนาส่วนใหญ่มักเจออุปสรรคเดียวกัน คือได้ JSON ดิบแล้วต้องหาวิธีดึงข้อมูลที่ต้องการ เช่น คะแนนความเชื่อมั่นหรือข้อความจริง ในคู่มือนี้เราจะเดินผ่านการโหลดภาพสำหรับ OCR, การทำ OCR recognition, และสุดท้าย **วิธีแยกวิเคราะห์ json** อย่างเป็นระเบียบและดูแลได้ง่าย

เมื่อจบบทเรียนคุณจะสามารถ:

* โหลดภาพสำหรับ OCR ด้วยเพียงไม่กี่บรรทัดของโค้ด  
* ทำ OCR recognition ด้วย C# OCR engine  
* **วิธีดึงข้อความ** และเมตาดาต้าอื่น ๆ จาก payload JSON  
* จัดการกับกรณีขอบที่พบบ่อย (ฟิลด์หาย, รูปแบบที่ไม่คาดคิด) โดยไม่ทำให้แอปพัง

ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่แล้ว

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มลงลึก ตรวจสอบให้แน่ใจว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้บน .NET Framework 4.7+)  
* การอ้างอิงไปยังไลบรารี OCR ที่คุณใช้ (ตัวอย่างใช้คลาส `OcrEngine` สมมติ)  
* แพคเกจ NuGet `Newtonsoft.Json` สำหรับการจัดการ JSON (`Install-Package Newtonsoft.Json`)  
* ไฟล์ภาพ (เช่น `passport.png`) ที่วางไว้ในตำแหน่งที่แอปของคุณสามารถอ่านได้

> **เคล็ดลับ:** หากคุณใช้ OCR SDK เชิงพาณิชย์ ตรวจสอบให้แน่ใจว่าได้เปิดใช้งานรูปแบบ JSON output—ส่วนใหญ่ผู้จำหน่ายจะเปิดให้ผ่านคุณสมบัติกำหนดค่าเช่น `ocrEngine.Config.OutputFormat`

## ขั้นตอนที่ 1 – สร้างและกำหนดค่า OCR Engine (Primary Keyword in Action)

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ของ OCR engine และบอกให้มันคืนค่าเป็น JSON นี่คือจุดที่วลี **how to parse json** ปรากฏในโค้ดของเราเป็นครั้งแรก เพราะ engine จะส่งกลับสตริง JSON ที่เราจะทำการแยกวิเคราะห์ต่อไป

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**ทำไมจึงสำคัญ:** การตั้งค่า `OutputFormat` เป็น `Json` ทำให้ผลลัพธ์มีทั้งข้อความที่จดจำได้ **และ** เมตาดาต้าที่มีประโยชน์ เช่น คะแนนความเชื่อมั่น หากลืมขั้นตอนนี้คุณจะได้เพียงข้อความธรรมดาเท่านั้น และ **how to parse json** จะกลายเป็นเรื่องไม่มีประโยชน์

## ขั้นตอนที่ 2 – โหลดภาพสำหรับ OCR

ต่อไปเราจะโหลดรูปภาพที่ต้องการวิเคราะห์ นี่คือจุดที่คีย์เวิร์ดรอง **load image for OCR** ทำหน้าที่ส่องสว่าง

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **ถ้าไฟล์ไม่พบล่ะ?** ให้ห่อการเรียกใน `try/catch` แล้วแสดงข้อความที่เป็นมิตร—แอปของคุณจะไม่พังและผู้ใช้จะรู้ว่าเกิดอะไรขึ้น

## ขั้นตอนที่ 3 – ทำ OCR Recognition

เมื่อ engine พร้อมและภาพถูกโหลดแล้ว ขั้นตอนต่อไปที่เป็นตรรกะคือการรันกระบวนการจดจำ นี่คือการตอบสนองต่อคีย์เวิร์ดรอง **run OCR recognition**

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

คุณสมบัติ `ocrResult.Text` ตอนนี้จะมีสตริง JSON หากคุณพิมพ์ออกมาที่คอนโซล คุณจะเห็นประมาณนี้:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## ขั้นตอนที่ 4 – วิธีดึงข้อความ (และฟิลด์อื่น) จาก JSON

นี่คือหัวใจของบทเรียน: **how to parse json** และ **how to extract text** จาก payload OCR เราจะใช้ `Newtonsoft.Json.Linq.JObject` เนื่องจากความยืดหยุ่นของมัน

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**ทำไมต้องใช้ `JObject`?** เพราะมันช่วยให้คุณเดินทางในโครงสร้าง JSON ได้อย่างปลอดภัยโดยไม่ต้องกำหนดคลาสโมเดล C# เต็มรูปแบบ ตัวดำเนินการเชิงเงื่อนไข (`?.`) ปกป้องคุณจาก `NullReferenceException` หาก OCR engine ละเว้นฟิลด์ใดฟิลด์หนึ่ง

### การจัดการกรณีขอบ

* **ฟิลด์หาย:** รูปแบบ `?.Value<T>() ?? default` จะคืนค่าตัวสำรองที่เหมาะสม  
* **หลายหน้า:** วนลูป `jsonObject["Pages"]` หากคาดว่าจะมีมากกว่าหนึ่งหน้า  
* **คะแนนความเชื่อมั่นไม่เป็นตัวเลข:** ใช้ `double.TryParse` หาก SDK บางครั้งคืนค่าเป็นสตริง

## ขั้นตอนที่ 5 – รวมทุกอย่างไว้ในเมธอดที่นำกลับมาใช้ใหม่ได้

เพื่อหลีกเลี่ยงการคัดลอก‑วางโค้ดซ้ำ ๆ ให้ห่อกระบวนการทั้งหมดไว้ในเมธอดช่วยเหลือ นี่ยังเป็นการสาธิต **use OCR engine C#** อย่างเป็นระเบียบและนำกลับมาใช้ได้

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

ตอนนี้คุณสามารถเรียก `RunOcrAndParseJson(@"C:\Images\passport.png");` จาก `Main` หรือส่วนอื่นของแอปพลิเคชันของคุณได้เลย

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมคอนโซลที่สมบูรณ์และแยกส่วนได้ คุณสามารถคัดลอก‑วางลงในโปรเจกต์ `.csproj` ใหม่ได้ มันรวมทุกส่วนที่เราได้พูดถึง พร้อมกับการจัดการข้อผิดพลาดเล็กน้อย

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่า OCR สำเร็จ):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

หากไม่สามารถอ่านภาพได้ SDK จะโยนข้อยกเว้นที่เราจับใน `Main` แล้วพิมพ์ข้อความแสดงข้อผิดพลาดที่เป็นมิตรแทนการพังของแอป

## คำถามที่พบบ่อย (FAQs)

**ถาม: ถ้า OCR engine คืนค่าเป็นอาร์เรย์ของหน้า จะทำอย่างไร?**  
ตอบ: วนลูป `json["Pages"]` แล้วต่อข้อความจากแต่ละ `["Text"]` เข้าด้วยกัน หรือประมวลผลแยกตามความต้องการของคุณ

**ถาม: ฉันสามารถ deserialize JSON ไปเป็นคลาส C# ที่มีประเภทได้หรือไม่?**  
ตอบ: ทำได้แน่นอน กำหนดโครงสร้างคลาสให้ตรงกับสคีม่า JSON แล้วใช้ `JsonConvert.DeserializeObject<YourRootClass>(result.Text)` วิธีนี้ให้ความปลอดภัยในระดับคอมไพล์ แต่ต้องรักษาโมเดลให้สอดคล้องกับ output ของ SDK อยู่เสมอ

**ถาม: วิธีนี้ทำงานกับ API OCR แบบ async ได้หรือไม่?**  
ตอบ: ได้ เพียงเปลี่ยน `engine.Recognize()` เป็น `await engine.RecognizeAsync()` และทำให้ `RunOcrAndParseJson` เป็น `async Task` ส่วนการแยกวิเคราะห์ JSON ยังคงเหมือนเดิม

**ถาม: จะบันทึก JSON ลงไฟล์เพื่อวิเคราะห์ต่อในภายหลังอย่างไร?**  
ตอบ: หลังจากได้ `result.Text` แล้วเรียก `File.WriteAllText(@"output.json", result.Text);` จากนั้นสามารถโหลดกลับด้วย `JObject.Parse(File.ReadAllText(...))`

## ถัดไป

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-02-20
description: เรียนรู้วิธีอ่านใบเสร็จใน C# โดยการดึงข้อความจากภาพและแปลงเป็น JSON โค้ดทีละขั้นตอนโดยใช้
  Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: th
og_description: ค้นพบวิธีอ่านใบเสร็จใน C# โดยการโหลดไฟล์รูปภาพ ดึงข้อความด้วย Aspose
  OCR และแปลงผลลัพธ์เป็น JSON ตัวอย่างโค้ดเต็ม.
og_title: วิธีอ่านใบเสร็จใน C# – แยกข้อความ, แปลงเป็น JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: วิธีอ่านใบเสร็จใน C# – คู่มือครบวงจรในการแยกข้อความจากรูปภาพ
url: /th/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

.

We need to translate the table content: Situation, Fix / Recommendation, and the rows.

Translate the step headings and other text.

Let's produce final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีอ่านใบเสร็จใน C# – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีอ่านใบเสร็จ** จากรูปภาพโดยอัตโนมัติหรือไม่? บางทีคุณอาจกำลังสร้างแอปติดตามค่าใช้จ่ายและต้องการดึงรายการจากรูปถ่ายใบเสร็จของร้านค้า ประสบการณ์ของผมบอกว่า ปัญหาที่ใหญ่ที่สุดคือการเปลี่ยน JPEG ที่เบลอให้เป็นข้อมูลโครงสร้างที่คุณสามารถใช้งานได้ ข่าวดีคือ ด้วยบรรทัดโค้ด C# ไม่กี่บรรทัดและ Aspose OCR คุณสามารถ **extract text from image** แล้ว **convert image to JSON** ได้อย่างเหมือนเวทมนตร์

ในบทแนะนำนี้ คุณจะได้โซลูชันที่พร้อมรันที่ **loads an image file C#**, ทำ OCR, และแสดงผลเป็น JSON รายละเอียด ไม่ต้องพึ่งบริการภายนอก ไม่ต้องเรียก REST ที่ซับซ้อน—แค่โค้ด .NET ธรรมดาที่คุณสามารถใส่ลงในคอนโซลหรือโปรเจกต์ ASP.NET ใดก็ได้ เมื่อจบคุณจะเข้าใจว่าทำไมแต่ละขั้นตอนถึงสำคัญ, วิธีจัดการกรณีขอบ (เช่น ใบเสร็จขนาดไม่มาตรฐาน) และรูปแบบของ JSON ที่ได้เป็นอย่างไร

## สิ่งที่คุณต้องเตรียม

- **.NET 6.0 หรือใหม่กว่า** – โค้ดใช้ `System.Drawing.Common` ซึ่งรองรับบน Windows, Linux, และ macOS
- **Aspose.OCR for .NET** – สามารถดาวน์โหลดแพคเกจ NuGet ทดลองใช้ฟรี (`Aspose.OCR`) หรือใช้เวอร์ชันที่มีลิขสิทธิ์ถ้าคุณมี
- **ภาพใบเสร็จตัวอย่าง** (`receipt.jpg`) ที่วางไว้ในตำแหน่งที่แอปของคุณสามารถอ่านได้
- IDE ใดก็ได้ที่คุณชอบ (Visual Studio, Rider, VS Code)

แค่นี้แหละ ไม่ต้องตั้งค่าเพิ่มเติม ไม่ต้อง API keys

---

## Step 1 – Load the Image File C# (Primary Keyword in Action)

ก่อนที่เครื่อง OCR จะทำงานคุณต้องโหลดรูปภาพเข้าสู่หน่วยความจำ นี่คือขั้นตอน “load image file C#” คลาสสิกที่หลายคนมักมองข้าม

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**ทำไมขั้นตอนนี้สำคัญ:**  
`Image.FromFile` จะอ่านไฟล์ *ครั้งเดียว* และเปิดแฮนด์เดิลไว้ ซึ่งเหมาะกับการทำ OCR อย่างรวดเร็ว หากคุณต้องประมวลผลใบเสร็จหลายใบในลูป ควรพิจารณาใช้ `Image.FromStream` เพื่อหลีกเลี่ยงการล็อกไฟล์

> **เคล็ดลับ:** หากเจอ *FileNotFoundException* ให้ตรวจสอบเส้นทางไฟล์และแน่ใจว่าภาพมีอยู่จริง เส้นทางแบบ relative (`"./receipt.jpg"`) ก็ใช้ได้ แต่เส้นทางแบบ absolute จะปลอดภัยกว่าในงาน production

---

## Step 2 – Create and Configure the OCR Engine

Aspose OCR มาพร้อมกับ `OcrEngine` ที่พร้อมใช้ คุณไม่ต้องฝึกโมเดลเอง; ไลบรารีนี้รู้วิธีอ่านข้อความพิมพ์ ซึ่งเป็นสิ่งที่ใบเสร็จส่วนใหญ่ใช้

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**ทำไมต้องตั้งค่าเหล่านี้:**  
`DetectOrientation` บอกให้เครื่องยนต์หมุนภาพอัตโนมัติหากใบเสร็จสแกนกลับหัว การกำหนดภาษาให้แคบลงช่วยลดชุดอักขระและเพิ่มความแม่นยำ—โดยเฉพาะเมื่อคุณต้องการข้อมูลภาษาอังกฤษแบบอัลฟานูเมอริกเท่านั้น

---

## Step 3 – Recognize the Image and Convert to JSON

ต่อไปคือส่วนที่สนุก: **extract text from image** และ **convert image to JSON** ด้วยการเรียกครั้งเดียว

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

เมธอด `RecognizeToJson` จะคืนค่าโครงสร้าง JSON ที่เต็มไปด้วยข้อมูลดังนี้:

- `Text`: ข้อความธรรมดาที่ต่อเนื่องกัน
- `Lines`: อาร์เรย์ของอ็อบเจ็กต์บรรทัดพร้อมพิกัด
- `Words`: คำแต่ละคำพร้อมคะแนนความเชื่อมั่น
- `Regions`: กล่องขอบเขตของบล็อกข้อความที่ตรวจพบ

คุณสามารถ deserialize JSON นี้เป็นอ็อบเจ็กต์ C# หากต้องการเข้าถึงแบบ typed แต่ในหลายกรณีการพิมพ์ JSON ดิบก็เพียงพอ

---

## Step 4 – Output the JSON (or Store It)

มาดูผลลัพธ์และพูดคุยว่าควรทำอะไรต่อกับมัน

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### ตัวอย่างผลลัพธ์

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**ต่อไปทำอะไรดี?**  
แยกอาร์เรย์ `Lines` เพื่อดึงจำนวน `Total` หรือส่ง JSON ไปยังบริการ downstream ที่จัดเก็บรายการค่าใช้จ่าย เนื่องจากผลลัพธ์เป็น JSON อยู่แล้ว คุณสามารถต่อเข้ากับ NoSQL database, Azure Function, หรือ Power Automate flow ได้โดยตรง

---

## Step 5 – Handling Common Edge Cases

แม้ OCR ที่ดีที่สุดก็ยังมีจุดอ่อนบ้าง ด้านล่างเป็นสถานการณ์ที่คุณอาจเจอขณะเรียน **how to read receipt** จากรูปภาพ

| Situation | Fix / Recommendation |
|-----------|----------------------|
| **ใบเสร็จความละเอียดต่ำ (≤ 150 dpi)** | ขยายภาพก่อนด้วย `Bitmap` และ `Graphics` (`InterpolationMode.HighQualityBicubic`) |
| **ใบเสร็จหมุนหรือเอียง** | คง `DetectOrientation = true` ไว้ สำหรับเอียงมาก ให้ทำพรี‑โปรเซสด้วย `Image.RotateFlip` หรือไลบรารี third‑party อย่าง OpenCV |
| **พื้นหลังสี (เช่น ใบเสร็จวางบนโต๊ะ)** | แปลงเป็น grayscale และเพิ่มความคอนทราสต์ก่อน OCR (`ImageAttributes`) |
| **หลายใบเสร็จในภาพเดียว** | ครอบตัดแต่ละใบเสร็จด้วยตนเองหรือใช้ `ocrEngine.Config.RecognizeMultipleRegions = true` |
| **ไฟล์ขนาดใหญ่ทำให้ OutOfMemory** | ใช้ `using` statements ปิด `Image` ทันที หรือประมวลผลเป็นชิ้นส่วน |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Step 6 – Full Working Example (Copy‑Paste Ready)

ด้านล่างเป็นโปรแกรม *ครบถ้วน* ที่คุณสามารถคอมไพล์ได้ทันที รวมทุกขั้นตอน, `using` directives ที่จำเป็น, และการจัดการข้อผิดพลาดอย่างสุภาพ

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**วิธีรัน:**  
`dotnet run` จากโฟลเดอร์โปรเจกต์ หากทุกอย่างตั้งค่าเรียบร้อย คุณจะเห็น JSON แสดงในคอนโซลและบันทึกไว้ข้างไฟล์ใบเสร็จของคุณ

---

## Conclusion

เราได้ครอบคลุม **how to read receipt** จากภาพใน C# ตั้งแต่ต้นจนจบแล้ว โดยการโหลดภาพ, ตั้งค่า Aspose OCR, และเรียก `RecognizeToJson` คุณสามารถ **extract text from image** และ **convert image to JSON** ได้โดยไม่มีโค้ดซ้ำซ้อน วิธีนี้สามารถขยายจากการสาธิตใบเสร็จเดียวไปสู่ตัวประมวลผลแบบแบตช์ที่จัดการหลายร้อยใบเสร็จต่อคืน

ขั้นตอนต่อไปที่คุณอาจลอง:

- **Parse the JSON** เพื่อดึงวันที่, ยอดรวม, และรายการ (ใช้ `System.Text.Json` หรือ `Newtonsoft.Json`)
- **Integrate with a database** (SQL, Cosmos DB) เพื่อเก็บบันทึกค่าใช้จ่ายโดยอัตโนมัติ
- **Add a UI** (WinForms, WPF, หรือ Blazor) ให้ผู้ใช้สามารถลาก‑และ‑วางใบเสร็จได้
- **Swap Aspose OCR** เป็นเอนจินอื่น (Tesseract, Microsoft Azure OCR) หากกังวลเรื่องลิขสิทธิ์—แค่รักษาแพทเทิร์น “load image file C#” เดิมไว้

ลองทำ, ทดลองทำให้พัง, แล้วกลับมาที่นี่เพื่อรีเฟรชความรู้ หากเจออุปสรรค ชุมชน (และฟอรั่ม Aspose) เป็นแหล่งที่ดีในการถามคำถาม ขอให้เขียนโค้ดอย่างสนุกและเปลี่ยนใบเสร็จกระดาษให้กลายเป็นข้อมูลที่ค้นหาได้ง่าย!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
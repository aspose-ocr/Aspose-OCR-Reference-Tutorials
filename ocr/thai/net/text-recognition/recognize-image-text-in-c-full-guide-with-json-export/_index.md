---
category: general
date: 2026-04-06
description: จดจำข้อความจากภาพโดยใช้ Aspose OCR ใน C# เรียนรู้วิธีดึงข้อความ, โหลดไฟล์ภาพใน
  C#, และเขียน JSON ใน C# ด้วยตัวอย่างแบบขั้นตอนง่าย ๆ
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: th
og_description: จดจำข้อความในภาพด้วย Aspose OCR ใน C# คู่มือนี้แสดงวิธีดึงข้อความ
  โหลดไฟล์ภาพใน C# และเขียน JSON ใน C# อย่างรวดเร็ว.
og_title: รู้จำข้อความในภาพด้วย C# – คู่มือขั้นตอนเต็ม
tags:
- OCR
- C#
- Aspose
title: การจดจำข้อความจากรูปภาพใน C# – คู่มือเต็มพร้อมการส่งออกเป็น JSON
url: /th/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การจดจำข้อความในรูปภาพด้วย C# – คู่มือขั้นตอนเต็ม

เคยต้อง **จดจำข้อความในรูปภาพ** จากใบเสร็จสแกนแต่ไม่แน่ใจว่าจะใช้ไลบรารีไหนไหม? คุณไม่ได้เป็นคนเดียว ในหลายแอปจริง—เช่น ตัวติดตามค่าใช้จ่าย, ตัวประมวลผลใบแจ้งหนี้, หรือเครื่องมือช่วยการเข้าถึง—การดึงคำออกจากรูปภาพเป็นอุปสรรคแรก  

ในบทเรียนนี้เราจะทำตามขั้นตอนจริงที่ **จดจำข้อความในรูปภาพ** ด้วยไลบรารี Aspose OCR, แสดง **วิธีดึงข้อความ**, สาธิต **การโหลดไฟล์รูปภาพ c#** อย่างถูกต้อง, และสุดท้าย **เขียน json ใน c#** เพื่อให้คุณสามารถเก็บหรือส่งผลลัพธ์ได้ เมื่อเสร็จคุณจะได้แอปคอนโซลที่พร้อมรันซึ่งแปลง PNG ใด ๆ ให้เป็น JSON ที่เรียบร้อย

---

## สิ่งที่คุณต้องเตรียม

- **.NET 6+** (โค้ดนี้ทำงานกับ .NET Framework 4.8 ได้เช่นกัน แต่ .NET 6 เป็นจุดที่เหมาะที่สุด)
- **Aspose.OCR for .NET** NuGet package. ติดตั้งด้วยคำสั่ง `dotnet add package Aspose.OCR`
- ตัวอย่างรูปภาพ (`input.png`) ที่วางไว้ในตำแหน่งที่แอปของคุณสามารถอ่านได้  
- Visual Studio 2022 หรือเครื่องมือแก้ไขใด ๆ ที่คุณชอบ—ไม่ต้องการเทคนิค IDE พิเศษ

> เคล็ดลับ: เก็บไฟล์รูปภาพไว้ในโฟลเดอร์ชื่อ `Resources` ภายในโปรเจกต์; จะทำให้เส้นทางเป็นระเบียบและหลีกเลี่ยงปัญหา “ไฟล์ไม่พบ”

---

## ขั้นตอนที่ 1: จดจำข้อความในรูปภาพ – โหลดไฟล์รูปภาพ

ก่อนที่เครื่อง OCR จะทำงานคุณต้อง **โหลดไฟล์รูปภาพ c#** อย่างปลอดภัย เมธอด `Image.FromFile` จะโยนข้อยกเว้นหากเส้นทางผิดหรือไฟล์ไม่รองรับรูปแบบ เราจึงต้องป้องกันไว้

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*ทำไมเรื่องนี้สำคัญ*: การโหลดรูปภาพภายในบล็อก `using` ทำให้ทรัพยากร GDI+ ที่ไม่ได้จัดการถูกปล่อยออกอย่างทันท่วงที ป้องกันการรั่วของหน่วยความจำในบริการที่ทำงานต่อเนื่อง

---

## ขั้นตอนที่ 2: วิธีดึงข้อความด้วย Aspose OCR

ตอนนี้บิตแมพอยู่ในหน่วยความจำแล้ว เราจะส่งต่อให้เครื่อง **จดจำข้อความในรูปภาพ** Engine ของ Aspose `OcrEngine` ใช้งานง่าย: สร้างอินสแตนซ์, เรียก `Recognize`, แล้วคุณจะได้อ็อบเจกต์ `OcrResult` ที่มีข้อความดิบ, คะแนนความเชื่อมั่น, และแม้แต่กรอบบาวด์ดิ้ง

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*คำอธิบาย*: เมธอด `Recognize` รันเครือข่ายประสาทเทียมในตัว มันทำงานดีที่สุดกับรูปภาพคอนทราสต์สูง, 300 DPI หากคุณใส่รูปภาพเบลอ คะแนนความเชื่อมั่นจะลดลง—พิจารณาการเตรียมล่วงหน้า (deskew, binarize) สำหรับโค้ดในสภาพการผลิต

---

## ขั้นตอนที่ 3: เขียน JSON ใน C# – ส่งออกผลลัพธ์ OCR

หลาย API ต้องการ JSON ดังนั้นเราจะ **เขียน json ใน c#** ด้วย `JsonExport` ของ Aspose ไลบรารีจะทำการซีเรียลไลซ์ `OcrResult` ทั้งหมด พร้อมรักษาข้อมูลบรรทัดและคะแนนความเชื่อมั่น

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### ตัวอย่าง JSON ที่คาดว่าจะได้

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*ทำไมต้องเป็น JSON?* มันเป็นรูปแบบที่ไม่ขึ้นกับภาษา, ง่ายต่อการดีซีเรียลไลซ์, และเก็บเมตาดาต้า OCR รายละเอียดที่คุณอาจต้องใช้สำหรับการตรวจสอบต่อไป

---

## ขั้นตอนที่ 4: โปรแกรมเต็มที่สามารถรันได้

รวมส่วนต่าง ๆ เข้าด้วยกัน นี่คือแอปคอนโซลที่สมบูรณ์ คัดลอก‑วาง, กู้คืนแพ็กเกจ NuGet, แล้วกด **F5**

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

รันโปรแกรมและเปิด `Resources/output.json`—คุณควรเห็น JSON ที่มีโครงสร้างสวยงามซึ่งแสดงทุกอย่างที่เครื่องจำได้

---

## การจัดการกับกรณีขอบทั่วไป

| สถานการณ์ | วิธีทำ | เหตุผล |
|-----------|--------|--------|
| **Image is null or corrupted** | ห่อ `Image.FromFile` ด้วย try/catch แล้วบันทึกข้อยกเว้น | ป้องกันแอปจากการหยุดทำงานและให้ข้อความผิดพลาดที่ชัดเจน |
| **Low confidence scores** | ตรวจสอบ `ocrResult.Words[i].Confidence` หากต่ำกว่า 0.75 ให้พิจารณาการเตรียมล่วงหน้า (เพิ่ม DPI, sharpen) | เพิ่มความน่าเชื่อถือสำหรับกระบวนการต่อไป เช่น การดึงจำนวนเงิน |
| **Large files (>10 MB)** | ลดขนาดรูปภาพก่อน OCR (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`) | ลดความกดดันของหน่วยความจำและเร่งการจดจำ |
| **Multi‑language documents** | ตั้งค่า `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | ทำให้เครื่องตรวจจับอักขระจากหลายภาษาได้ |

---

## โบนัส: แสดงผล OCR บนภาพ (ทางเลือก)

หากต้องการดูตำแหน่งของแต่ละคำบนรูปภาพ คุณสามารถวาดกรอบบาวด์ดิ้งได้:

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

ไฟล์ `annotated.png` ที่ได้จะมีสี่เหลี่ยมสีแดงล้อมรอบทุกคำที่จำได้—เป็นประโยชน์สำหรับการดีบัก

---

## สรุป

เราได้ **จดจำข้อความในรูปภาพ** ด้วย C# ตั้งแต่การโหลดไฟล์รูปภาพ, เรียกใช้ Aspose OCR เพื่อ **วิธีดึงข้อความ**, และสุดท้าย **เขียน json ใน c#** เพื่อให้ข้อมูลสามารถเดินทางไปไหนก็ได้ ตัวอย่างเต็มทำงานได้ทันที และเคล็ดลับเพิ่มเติมช่วยให้คุณรับมือกับใบเสร็จเบลอ, ไฟล์ขนาดใหญ่, หรือสแกนหลายภาษา

ต่อไปคุณอาจลองสลับ Aspose กับเอนจินอื่น (Tesseract, Microsoft OCR) แล้วเปรียบเทียบคะแนนความเชื่อมั่น, หรือส่ง JSON ไปยังฐานข้อมูลสำหรับการรายงานค่าใช้จ่าย คุณยังสามารถขยายแอปคอนโซลเป็น ASP .NET Core Web API ที่รับอัปโหลดรูปภาพและคืนค่า JSON ทันที

มีคำถามเกี่ยวกับการสเกล, การจัดการข้อผิดพลาด, หรือการผสานกับ Azure Functions? แสดงความคิดเห็นหรือทักมาที่ GitHub ของฉันได้เลย โค้ดดิ้งอย่างสนุกสนาน, ขอให้ OCR ของคุณคมชัดเสมอ!

---

![Screenshot of OCR JSON output – ตัวอย่างการจดจำข้อความในรูปภาพ](https://example.com/ocr-example.png "ตัวอย่างการจดจำข้อความในรูปภาพ")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
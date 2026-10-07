---
category: general
date: 2026-02-13
description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากภาพ, จดจำข้อความจากรูปถ่ายหรือ JPG,
  และทำ OCR บนภาพโดยไม่ต้องเชื่อมต่ออินเทอร์เน็ต.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: th
og_description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากภาพ, จดจำข้อความจากรูปถ่าย, และรัน
  OCR บนภาพพร้อมตัวอย่างที่สมบูรณ์และสามารถทำงานได้
og_title: วิธีใช้ OCR ใน C# – แยกข้อความจากรูปภาพ
tags:
- OCR
- C#
- Image Processing
title: วิธีใช้ OCR ใน C# – ดึงข้อความจากภาพและจดจำข้อความจากรูปถ่าย
url: /th/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – ดึงข้อความจากรูปภาพและจดจำข้อความจากรูปถ่าย

เคยสงสัยไหมว่า **วิธีใช้ OCR** เพื่อดึงคำออกจากภาพหน้าจอ, ใบเสร็จสแกน, หรือรูปถ่ายสุ่มที่คุณถ่ายด้วยโทรศัพท์? คุณไม่ได้เป็นคนเดียวที่คิดแบบนี้. ในหลายแอปพลิเคชันจริง เราต้องแปลงรูปภาพให้เป็นข้อความที่สามารถค้นหาได้, และการทำเช่นนั้นแบบออฟไลน์—โดยไม่ต้องพึ่งการเชื่อมต่ออินเทอร์เน็ตที่ไม่เสถียร—อาจรู้สึกเหมือนปริศนา.

ดังนั้นคู่มือนี้จะแสดงวิธีทำแบบขั้นตอนต่อขั้นตอนเพื่อ **ดึงข้อความจากรูปภาพ** ด้วย C# OCR engine, และยังครอบคลุมวิธี **จดจำข้อความจากรูปถ่าย**, **จดจำข้อความจาก JPG**, และ **รัน OCR บนรูปภาพ** ที่อยู่บนดิสก์ของคุณ. เมื่อเสร็จสิ้นคุณจะได้โปรแกรมที่พร้อมคัดลอก‑วางและทำงานได้ทันที.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีกำหนดค่า OCR engine สำหรับภาษาจีนตัวย่อ (หรือภาษาใดก็ได้ที่คุณเพิ่มเข้าไป).  
- โค้ดที่จำเป็นเพื่อ **โหลดทรัพยากร** จากโฟลเดอร์ในเครื่อง—ไม่ต้องเรียกเครือข่าย.  
- วิธี **จดจำข้อความจากรูปถ่าย** เช่น JPEG, PNG หรือ BMP.  
- เคล็ดลับการจัดการกรณีขอบที่พบบ่อย เช่น ไฟล์โมเดลหายหรือรูปแบบภาพที่ไม่รองรับ.  
- ตัวอย่างเต็มที่สามารถรันได้ คุณสามารถวางลงใน Visual Studio และดูผลลัพธ์ได้ทันที.

### ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (API ที่ใช้ที่นี่ตั้งเป้าหมายที่ .NET Standard 2.0, ดังนั้นเวอร์ชันเก่าก็ทำงานได้).  
- ความคุ้นเคยพื้นฐานกับ C# และ Visual Studio (หรือ IDE ใดก็ได้ที่คุณชอบ).  
- ไลบรารี OCR ที่คุณใช้ (ส่วนโค้ดนี้สมมติว่ามีคลาส `OcrEngine` ที่มาพร้อมกับโมเดลภาษา).  
- โฟลเดอร์ที่มีไฟล์โมเดลภาษาที่จำเป็น—คิดว่าเป็น “สมอง” ที่ engine ใช้อ่านอักขระจีน.

> **เคล็ดลับ:** หากคุณยังไม่มีไฟล์โมเดลภาษาจีน, ดาวน์โหลดครั้งเดียวจากเว็บไซต์ของผู้จำหน่ายและวางไว้ในโฟลเดอร์เช่น `C:\OcrResources`. Engine จะไม่ต้องเชื่อมต่อออนไลน์อีกต่อไป.

---

![แผนภาพแสดงกระบวนการ OCR บนรูปถ่าย](path/to/ocr-diagram.png "แผนภาพแสดงกระบวนการ OCR บนรูปถ่าย")

## วิธีใช้ OCR: ตั้งค่า Engine

สิ่งแรกที่คุณต้องการคืออินสแตนซ์ของ OCR engine ที่กำหนดค่าภาษาที่คุณต้องการ. ในบทเรียนนี้เราตั้งเป้าหมายเป็น **ภาษาจีนตัวย่อ**, แต่การสลับ `OcrLanguage.ChineseSimplified` เป็น `OcrLanguage.English` (หรือค่า enum ใดก็ได้) เพียงบรรทัดเดียวเท่านั้น.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
การตั้งค่า `Language` บอก engine ว่าต้องคาดหวังชุดอักขระแบบใด. `ResourceFolder` คือที่ที่ engine มองหาไฟล์น้ำหนักของ neural‑network และพจนานุกรมภาษา—คิดว่าเป็นธนาคารความจำของสมอง. หากชี้ไปยังโฟลเดอร์ผิด, engine จะโยน `FileNotFoundException` และคุณจะติดอยู่.

## ดึงข้อความจากรูปภาพ – โหลดทรัพยากร

ก่อนที่ engine จะอ่านอะไรได้, คุณต้องโหลดไฟล์โมเดลเหล่านั้นเข้าสู่หน่วยความจำ. ขั้นตอนนี้ **สำคัญมาก** เพราะช่วยหลีกเลี่ยงการเรียกเครือข่ายทุกครั้งที่ประมวลผลภาพ.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**อะไรอาจผิดพลาดได้?**  
หากพาธโฟลเดอร์ไม่ถูกต้องหรือไฟล์เสียหาย, `LoadResources()` จะโยนข้อยกเว้น. บล็อก `try/catch` ด้านบนแสดงการจัดการข้อผิดพลาดอย่างอ่อนโยน—สิ่งที่คุณมักต้องการในสภาพแวดล้อมการผลิต.

## จดจำข้อความจากรูปถ่าย – การรัน OCR

ตอนนี้เป็นส่วนที่สนุก: ส่งไฟล์ภาพให้ engine แล้วรับข้อความที่จดจำได้กลับมา. นี่คือหัวใจของสถานการณ์ **รัน OCR บนรูปภาพ**, ไม่ว่าจะเป็น JPEG, PNG หรือแม้แต่ BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

เมธอด `RecognizeImage` จะคืนค่า `RecognitionResult` (หรือชื่อใดก็ตามที่ SDK ของคุณใช้) ซึ่งโดยทั่วไปจะมี:

- `Text` – การถอดข้อความเป็น plain‑text.  
- `Confidence` – คะแนนเชิงตัวเลขที่บ่งบอกว่า engine มีความมั่นใจแค่ไหนต่อแต่ละบรรทัด.  
- `BoundingBoxes` – พิกัดเลือก (optional) ที่บ่งบอกตำแหน่งของแต่ละคำในรูปภาพ.

**ทำไมคุณอาจสนใจคะแนนความมั่นใจ:**  
หากคุณกำลังสร้างเครื่องมืออัตโนมัติการป้อนข้อมูล, คุณสามารถตั้งค่าเกณฑ์ (เช่น 0.85) แล้วให้ผู้ใช้ยืนยันบรรทัดที่ความมั่นใจต่ำ. วิธีนี้จะเพิ่มความแม่นยำโดยรวมอย่างมาก.

## จดจำข้อความจาก JPG – การจัดการรูปแบบต่างๆ

นักพัฒนาหลายคนคิดว่า OCR ทำงานได้เฉพาะ PNG เท่านั้น, แต่ engine สมัยใหม่รองรับไฟล์ **JPG** ได้อย่างดี. สิ่งเดียวที่ต้องระวังคือการบีบอัด JPEG อาจสร้าง artefacts ที่ทำให้โมเดลสับสน.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

หากคุณไม่มีฟังก์ชัน `DenoiseAndDeskew` ช่วยเหลือ, ไลบรารีหลายตัว (เช่น OpenCvSharp) มีฟังก์ชันเหล่านี้ให้ใช้. สิ่งสำคัญคือ: **รัน OCR บนรูปภาพ** หลังจากทำความสะอาดเล็กน้อย หากภาพมาจากสแกนเนอร์หรือกล้องโทรศัพท์.

## รัน OCR บนรูปภาพ – เคล็ดลับ, กรณีขอบ, และแนวปฏิบัติที่ดีที่สุด

### 1. การจัดการหน่วยความจำ
การโหลดโมเดลภาษาใหญ่สามารถใช้หน่วยความจำหลายร้อยเมกะไบต์. อย่าลืมทำ `Dispose` กับ engine เมื่อใช้งานเสร็จ:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. การประมวลผลแบบกลุ่ม
หากต้องประมวลผลหลายสิบรูป, โหลดทรัพยากรครั้งเดียวแล้ววนลูป:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. สถานการณ์หลายภาษา
คุณสามารถสลับภาษาได้ทันทีโดยกำหนดค่าใหม่ให้ `ocrEngine.Language` แล้วเรียก `LoadResources()` อีกครั้ง. เพียงระวังเวลาการโหลดที่เพิ่มขึ้น.

### 4. การจัดการผลลัพธ์ว่าง
บางครั้ง engine จะคืนสตริงว่าง. ปกติหมายถึงภาพเบลอเกินไปหรือสีข้อความผสมกับพื้นหลัง. ตรวจสอบอย่างรวดเร็ว:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. ข้อควรระวังด้านความปลอดภัย
ห้ามส่งไฟล์ที่ผู้ใช้อัปโหลดโดยตรงเข้า OCR engine หากไม่ได้ตรวจสอบ. ขั้นพื้นฐานควรตรวจสอบนามสกุลไฟล์และขนาด, และพิจารณาสแกนหามัลแวร์.

---

## ตัวอย่างการทำงานที่สมบูรณ์

ด้านล่างเป็นโปรแกรมเดียวที่ทำงานได้เอง คุณสามารถคัดลอกไปยังโปรเจกต์ Console App ใหม่ได้. ตัวอย่างนี้สาธิต **วิธีใช้ OCR**, **ดึงข้อความจากรูปภาพ**, **จดจำข้อความจากรูปถ่าย**, **จดจำข้อความจาก JPG**, และ **รัน OCR บนรูปภาพ**—ทั้งหมดในขั้นตอนเดียว.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

ข้อความจริงของคุณจะต่างกันตามเนื้อหาของภาพ, แต่คุณควรเห็นบล็อกอักขระ Unicode แสดงบนคอนโซลพร้อมเปอร์เซ็นต์ความมั่นใจ.

## สรุป

เราได้อธิบาย **วิธีใช้ OCR** ใน C# ตั้งแต่ต้นจนจบ—การกำหนดค่า engine, การโหลดทรัพยากรภาษา, และสุดท้าย **จดจำข้อความจากรูปถ่าย** หรือ **JPG** โดยไม่ต้องเชื่อมต่ออินเทอร์เน็ต. ด้วยการทำตามขั้นตอนข้างต้นคุณสามารถ **ดึงข้อความจากรูปภาพ**, **รัน OCR บนรูปภาพ** assets, และจัดการกับปัญหาที่พบบ่อยที่สุดที่ทำให้ผู้เริ่มต้นติดขัด.

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองให้ engine ประมวลผลหน้า PDF ที่แปลงเป็นภาพ, หรือทดลองใช้แพ็คภาษาอื่นเพื่อดูว่าคะแนนความมั่นใจเปลี่ยนแปลงอย่างไร. คุณอาจ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
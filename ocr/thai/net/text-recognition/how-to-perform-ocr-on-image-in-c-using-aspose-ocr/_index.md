---
category: general
date: 2026-10-11
description: เรียนรู้วิธีทำ OCR บนรูปภาพใน C# ด้วย Aspose.OCR รวมถึงการติดตั้ง System.Drawing.Common
  และการสกัดข้อความจากไฟล์ JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: th
lastmod: 2026-10-11
og_description: ทำ OCR บนรูปภาพใน C# ด้วย Aspose.OCR คู่มือนี้จะแสดงวิธีการติดตั้ง
  System.Drawing.Common, โหลดรูปภาพเพื่อทำ OCR, และดึงข้อความจากไฟล์ JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: ทำ OCR บนภาพด้วย C# – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: วิธีทำ OCR บนรูปภาพใน C# ด้วย Aspose.OCR
url: /th/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บนรูปภาพใน C# ด้วย Aspose.OCR

หากคุณต้องการ **ทำ OCR บนรูปภาพ** ในแอปพลิเคชัน .NET คู่มือนี้จะแสดงวิธีแก้ไขแบบครบวงจร ด้วย Aspose.OCR คุณสามารถ **จดจำข้อความจากรูปภาพ** เช่นไฟล์ JPG ได้อย่างรวดเร็วและแสดงผลลัพธ์ในหน้าต่างคอนโซล

คุณจะได้เรียนรู้วิธี:

* **ติดตั้งแพคเกจ System.Drawing.Common** – ไลบรารีที่ให้คลาส `Image`,
* **โหลดรูปภาพสำหรับ OCR** – อ่านไฟล์ JPEG หรือ PNG เข้าไปในหน่วยความจำ,
* กำหนดโมเดลภาษา,
* **ทำ OCR บนรูปภาพ** และสุดท้าย,
* **สกัดข้อความจาก JPG** แล้วแสดงผล

ขั้นตอนเหล่านี้เขียนสำหรับ .NET 6+ แต่ก็ทำงานได้กับ .NET Framework 4.6.1 หรือใหม่กว่า

---

## ข้อกำหนดเบื้องต้น

| ความต้องการ | เหตุผลที่สำคัญ |
|-------------|----------------|
| .NET 6 SDK (หรือ .NET Framework 4.6.1+) | ให้ runtime สำหรับแอปคอนโซล C# |
| Visual Studio 2022 (หรือ IDE ใดก็ได้) | ทำให้การเพิ่มแพคเกจ NuGet และการรันโปรแกรมง่ายขึ้น |
| การเชื่อมต่ออินเทอร์เน็ต (ครั้งแรกเท่านั้น) | Aspose.OCR จะดาวน์โหลดโมดูลภาษาโดยอัตโนมัติ |
| ตัวอย่างรูปภาพที่มีข้อความ Cyrillic หรือ Latin (เช่น `sample_cyrillic.jpg`) | ใช้เพื่อสาธิต **สกัดข้อความจาก JPG** |

---

## ขั้นตอนที่ 1: ติดตั้งแพคเกจ System.Drawing.Common

แพคเกจ NuGet `System.Drawing.Common` ให้คลาส `Image` ที่คุณจะ **โหลดรูปภาพสำหรับ OCR** เปิด Package Manager Console แล้วรัน:

```powershell
Install-Package System.Drawing.Common
```

> **เคล็ดลับ:** ตั้งค่าเป้าหมายเป็น `net6.0-windows` หรือเพิ่ม `<UseWindowsForms>true</UseWindowsForms>` ไปในไฟล์โครงการ หากคุณเจอคำเตือนเฉพาะแพลตฟอร์มบน Linux/macOS

---

## ขั้นตอนที่ 2: เพิ่มแพคเกจ Aspose.OCR NuGet

Aspose.OCR มีเอนจิน OCR และโมเดลภาษา ติดตั้งโดยใช้:

```powershell
Install-Package Aspose.OCR
```

แพคเกจนี้มีขนาดเล็ก; ข้อมูลภาษาที่ต้องการ (เช่น Cyrillic) จะถูกดาวน์โหลดครั้งแรกที่คุณตั้งค่า `OcrEngine.Language`

---

## ขั้นตอนที่ 3: วิธีโหลดรูปภาพสำหรับ OCR

การโหลดรูปเป็นขั้นตอนแรกที่จำเป็นก่อนที่คุณจะ **ทำ OCR บนรูปภาพ** เมธอด `Image.FromFile` สามารถอ่านฟอร์แมตใดก็ได้ที่ GDI+ รองรับ รวมถึง JPG, PNG, BMP, และ TIFF

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*หากไฟล์ไม่พบ จะเกิด `FileNotFoundException` – ควรห่อการเรียกในบล็อก try/catch สำหรับโค้ดในสภาพการผลิต*

---

## ขั้นตอนที่ 4: กำหนดค่าเอนจินและ **ทำ OCR บนรูปภาพ**

สร้างอินสแตนซ์ `OcrEngine` เลือกโมเดลภาษา กำหนดรูปที่โหลดแล้ว แล้วเรียก `Recognize()`

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

เมธอด `Recognize()` จะคืนค่าอ็อบเจกต์ `OcrResult` ที่บรรจุข้อความที่สกัดออกมา คะแนนความเชื่อมั่น และกรอบขอบเขต โมดูลภาษา จะดาวน์โหลดอัตโนมัติในครั้งแรกที่ใช้ ดังนั้นไม่ต้องเตรียมไฟล์เพิ่มเติม

---

## ขั้นตอนที่ 5: **สกัดข้อความจาก JPG** และแสดงผล

ตอนนี้คุณสามารถ **จดจำข้อความจากรูปภาพ** และแสดงผลได้ คุณสมบัติ `Text` ของ `OcrResult` จะมีสตริงข้อความธรรมดา

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### ผลลัพธ์คอนโซลที่คาดหวัง

```
Recognized text:
Пример текста на кириллице
```

หากรูปต้นฉบับมีข้อความภาษาอังกฤษ ผลลัพธ์จะเป็นประโยคภาษาอังกฤษที่คุณใส่ไว้ในรูป

---

## กรณีขอบและเคล็ดลับปฏิบัติที่ดีที่สุด

| สถานการณ์ | คำแนะนำ |
|-----------|----------|
| **รูปภาพขนาดใหญ่ ( > 5 MB )** | ปรับขนาดรูปให้ ≤ 2000 px ที่ด้านยาวที่สุดก่อนทำ OCR เพื่อลดการใช้หน่วยความจำและเพิ่มความเร็ว |
| **หลายภาษาในรูปเดียว** | เรียก `ocrEngine.AddLanguage(OcrLanguage.English)` เพิ่มเติมจาก Cyrillic แล้วตั้ง `ocrEngine.Language = OcrLanguage.Multilingual` |
| **สแกนที่คอนทราสต์ต่ำ** | เพิ่มคอนทราสต์ด้วย `System.Drawing.Graphics` ก่อนส่งบิตแมปไปยังเอนจิน |
| **รันบน Linux/macOS** | ตรวจสอบให้แน่ใจว่าได้ติดตั้ง dependency เนทีฟ `libgdiplus` (`sudo apt-get install -y libgdiplus`) |
| **เรียก OCR ซ้ำหลายครั้ง** | ใช้อินสแตนซ์ `OcrEngine` เดียวกันและเปลี่ยนเฉพาะ `ocrEngine.Image` เพื่อหลีกเลี่ยงการโหลดโมดูลซ้ำ |

---

## โปรแกรมเต็มที่สามารถรันได้

ด้านล่างเป็นแอปคอนโซลที่รวมขั้นตอนทั้งหมดไว้แล้ว คัดลอกโค้ดไปยังโปรเจกต์คอนโซล C# ใหม่ แก้ไขเส้นทางรูปภาพ แล้วรัน

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**การรันโปรแกรม** จะพิมพ์สตริงที่จดจำได้ลงคอนโซล ยืนยันว่าคุณได้ **ทำ OCR บนรูปภาพ** และ **สกัดข้อความจาก JPG** อย่างสำเร็จ

---

## สรุป

ตอนนี้คุณรู้วิธี **ทำ OCR บนรูปภาพ** ใน C# ด้วย Aspose.OCR ตั้งแต่การติดตั้ง **แพคเกจ System.Drawing.Common** ไปจนถึง **การโหลดรูปภาพสำหรับ OCR**, การเลือกภาษาให้เหมาะสม, และสุดท้าย **การสกัดข้อความจาก JPG** ตัวอย่างครบวงจรนี้ให้พื้นฐานที่มั่นคงสำหรับการสร้าง pipeline การประมวลผลเอกสารที่ซับซ้อนยิ่งขึ้น เช่น การประมวลผลเป็นชุดของโฟลเดอร์รูปภาพหรือการรวม OCR เข้าไปใน Web API

### ขั้นตอนต่อไปคืออะไร?

* สำรวจ **การจดจำข้อความจากรูปภาพ** ใน PDF โดยแปลงแต่ละหน้าเป็นรูปก่อน
* ทดลองปรับคุณสมบัติของ `OcrEngine` เช่น `Resolution`, `Threshold` และ `MaxProcessingTime` เพื่อเพิ่มความแม่นยำบนสแกนที่มีเสียงรบกวน
* ผสานผลลัพธ์ OCR กับไลบรารีการประมวลผลภาษาธรรมชาติ เพื่อจัดหมวดหมู่เนื้อหาที่สกัดออกมาโดยอัตโนมัติ

คุณสามารถปรับโค้ดให้รองรับฟอร์แมตรูปอื่น ๆ เพิ่มการจัดการข้อผิดพลาด หรือรวมเข้ากับแอปพลิเคชันขนาดใหญ่ได้ตามต้องการ ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [สกัดข้อความจากรูปภาพใน C# – คู่มือ Aspose OCR ฉบับสมบูรณ์](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [สกัดข้อความจากรูปภาพ C# ด้วยการเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [วิธีทำการสกัดข้อความจากภาพจากสตรีมโดยใช้ Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
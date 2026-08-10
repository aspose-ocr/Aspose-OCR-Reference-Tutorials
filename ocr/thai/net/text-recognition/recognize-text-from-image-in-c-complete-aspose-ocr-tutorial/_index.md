---
category: general
date: 2026-05-06
description: เรียนรู้วิธีจดจำข้อความจากภาพด้วย Aspose OCR ใน C# ดึงข้อความจากใบเสร็จ
  โหลดภาพสำหรับ OCR และดูตัวอย่างเต็มของ Aspose OCR.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for OCR
- Aspose OCR example
language: th
og_description: เรียนรู้การจดจำข้อความจากภาพด้วย Aspose OCR, ดึงข้อความจากใบเสร็จ,
  และโหลดภาพสำหรับ OCR ด้วยคำแนะนำที่กระชับและเป็นขั้นตอน.
og_title: แยกข้อความจากภาพใน C# – บทเรียน Aspose OCR ฉบับสมบูรณ์
tags:
- C#
- OCR
- Aspose
title: แยกข้อความจากรูปภาพด้วย C# – บทเรียน Aspose OCR ฉบับสมบูรณ์
url: /th/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากรูปภาพใน C# – ตัวอย่าง Aspose OCR ครบถ้วน

เคยต้องการ **recognize text from image** แต่ไม่แน่ใจว่าจะเลือกไลบรารีไหน? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อต้องดึงตัวเลขจากใบเสร็จหรือสแกนแบบฟอร์ม ข่าวดีคือ Aspose OCR ทำให้กระบวนการทั้งหมดง่ายดาย และในบทเรียนนี้เราจะพาคุณผ่าน **complete Aspose OCR example** ที่ช่วยให้คุณ **extract text from receipt** จากรูปภาพได้ด้วยเพียงไม่กี่บรรทัดของ C#.

ในไม่กี่นาทีต่อไปคุณจะได้เรียนรู้วิธี **load image for OCR**, กำหนดพื้นที่ที่มีจำนวนเงินรวม, รันเอนจิน, และสุดท้ายแสดงผลลัพธ์ ไม่มีการอ้างอิงเอกสารภายนอกที่คลุมเครือ ไม่มีส่วนที่ขาดหาย—ทุกอย่างที่คุณต้องคัดลอก‑วางและรันพร้อมอยู่ที่นี่ เพียงตั้งค่าติดตั้งเล็กน้อยและทำตามขั้นตอนไม่กี่ขั้นตอน คุณก็จะสามารถจดจำข้อความจากไฟล์รูปภาพได้แบบเรียลไทม์

> **สิ่งที่คุณจะได้เรียนรู้**  
> * แอปคอนโซล C# ที่รันได้ซึ่งจดจำข้อความจากไฟล์รูปภาพ  
> * ความเข้าใจว่าทำไมคุณอาจต้องจำกัด OCR ให้กับสี่เหลี่ยมเฉพาะ (ความเร็วและความแม่นยำ)  
> * เคล็ดลับการจัดการกับกรณีขอบที่พบบ่อย เช่น ใบเสร็จเบลอหรือสแกนหมุน  

---

## ความต้องการเบื้องต้น

ก่อนที่เราจะเริ่มลงมือ ตรวจสอบให้แน่ใจว่าคุณมี:

| ความต้องการ | ทำไมจึงสำคัญ |
|-------------|----------------|
| .NET 6.0 SDK (หรือใหม่กว่า) | Aspose OCR มีรูปแบบเป็นไลบรารี .NET Standard 2.0 / .NET 5+ ดังนั้นรันไทม์ใด ๆ ที่เป็นรุ่นใหม่ก็ทำงานได้ |
| Visual Studio 2022 (หรือ VS Code) | IDE ที่สะดวกช่วยเร่งการดีบัก, แต่ใด ๆ ที่สามารถคอมไพล์ C# ก็ใช้ได้ |
| **Aspose.OCR for .NET** NuGet package | นี่คือไลบรารีหลักที่ทำหน้าที่จดจำข้อความจากรูปภาพ |
| ตัวอย่างรูปใบเสร็จ (`receipt.jpg`) | เราจะใช้ไฟล์นี้เพื่อสาธิต **extract text from receipt** |

คุณสามารถติดตั้งแพคเกจ NuGet ด้วยคำสั่งต่อไปนี้:

```bash
dotnet add package Aspose.OCR
```

เมื่อทำเสร็จแล้ว คุณพร้อมที่จะเริ่มโหลดรูปภาพสำหรับ OCR

---

## ขั้นตอนที่ 1: โหลดรูปภาพสำหรับ OCR

สิ่งแรกที่ต้องทำคือชี้เอนจินไปยังไฟล์ที่ต้องการวิเคราะห์ นี่คือจุดที่คีย์เวิร์ดรอง **load image for OCR** ปรากฏโดยธรรมชาติ

```csharp
using Aspose.OCR;
using System.Drawing;

// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the receipt image – replace the path with your own file location
ocrEngine.SetImage(@"C:\Images\receipt.jpg");
```

> **เคล็ดลับ:** หากรูปภาพอยู่ในโฟลเดอร์โปรเจกต์ คุณสามารถใช้เส้นทางสัมพัทธ์เช่น `ocrEngine.SetImage("receipt.jpg");` เพียงตรวจสอบให้ไฟล์ถูกคัดลอกไปยังไดเรกทอรีเอาต์พุต (`Copy to Output Directory = PreserveNewest`)

เมธอด `SetImage` รองรับรูปแบบใดก็ได้ที่ System.Drawing ถอดรหัสได้ (JPEG, PNG, BMP ฯลฯ) ดังนั้นคุณจึงไม่จำกัดอยู่แค่ไฟล์ประเภทเดียว

---

## ขั้นตอนที่ 2: กำหนดพื้นที่สนใจ – **extract text from receipt**

การสแกนภาพทั้งหมดจะทำให้ CPU ทำงานเปล่าและอาจสร้างสัญญาณรบกวนได้ โดยบอก Aspose OCR ว่าจำนวนเงินรวมอยู่ที่ไหน คุณจะเพิ่มความเร็วและความแม่นยำได้ นี่คือส่วนที่เราทำ **extract text from receipt**

```csharp
// Define a rectangle that covers the total amount on the receipt
// (x, y, width, height) – adjust these numbers for your own layout
var roi = new Rectangle(150, 500, 300, 80);
ocrEngine.SetRegionOfInterest(roi);
```

> **ทำไมต้องเป็นสี่เหลี่ยม?**  
> เอนจิน OCR ทำงานบนกริดพิกเซล เมื่อคุณจำกัดให้ทำงานในพื้นที่หนึ่ง มันจะละเลยส่วนอื่น—ไม่มีอักขระรบกวนจากโลโก้ร้านหรือบรรทัดหัวเรื่อง

หากคุณไม่แน่ใจพิกัดที่แน่นอน สามารถใช้โปรแกรมดูรูปที่แสดงตำแหน่งพิกเซล (เช่น Paint.NET) เพื่อประมาณค่าได้

---

## ขั้นตอนที่ 3: รันเอนจิน – **recognize text from image** (คีย์เวิร์ดหลัก)

ตอนนี้จุดสำคัญเกิดขึ้น คุณบอก Aspose ให้อ่านพิกเซลภายในสี่เหลี่ยมที่กำหนดไว้

```csharp
// Perform the recognition
OcrResult result = ocrEngine.Recognize();
```

`OcrResult` มีข้อความดิบ, คะแนนความมั่นใจ, และกล่องรอบคำแต่ละคำ สำหรับการสาธิตอย่างรวดเร็วเราจะพิมพ์ข้อความธรรมดาออกมา

```csharp
Console.WriteLine("Total amount detected: " + result.Text);
```

เมื่อคุณรันโปรแกรม ควรเห็นผลลัพธ์คล้ายดังนี้:

```
Total amount detected: $23.45
```

หากผลลัพธ์ดูเป็นอักขระผสมกัน ตรวจสอบพิกัด ROI อีกครั้งหรือเพิ่มความละเอียดของภาพ

---

## ขั้นตอนที่ 4: จัดการผลลัพธ์ – ปรับแต่ง **Aspose OCR example**

โซลูชันที่แข็งแรงทำมากกว่าการพิมพ์สตริงลงคอนโซล ด้านล่างเป็นตัวช่วยขนาดเล็กที่ตัดช่องว่าง, ลบการขึ้นบรรทัดที่ไม่จำเป็น, และตรวจสอบว่าค่าที่ดึงมามีรูปแบบเป็นจำนวนเงินหรือไม่

```csharp
static string CleanAmount(string raw)
{
    // Remove any non‑numeric characters except dot and comma
    var cleaned = new string(raw
        .Where(c => char.IsDigit(c) || c == '.' || c == ',')
        .ToArray());

    // Normalize decimal separator to dot
    cleaned = cleaned.Replace(',', '.');

    // If we end up with an empty string, return a friendly message
    return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
}

// ...

string amount = CleanAmount(result.Text);
Console.WriteLine($"Parsed amount: ${amount}");
```

ตัวช่วยนี้แสดง **Aspose OCR example** ที่เป็นรูปแบบจริงซึ่งคุณสามารถนำไปใช้ในระบบใบแจ้งหนี้ขนาดใหญ่ได้

---

## ขั้นตอนที่ 5: โปรแกรมเต็มที่รันได้ – ตัวอย่าง **extract text from receipt** สุดยอด

รวมทุกอย่างเข้าด้วยกันจะได้ไฟล์เดียวที่คัดลอก‑วางได้ บันทึกเป็น `Program.cs` แล้วรันด้วย `dotnet run`

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image for OCR
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage(@"C:\Images\receipt.jpg");   // <-- adjust path

        // 2️⃣ Define the region that holds the total amount
        var roi = new Rectangle(150, 500, 300, 80);
        ocrEngine.SetRegionOfInterest(roi);

        // 3️⃣ Run the engine – recognize text from image
        OcrResult result = ocrEngine.Recognize();

        // 4️⃣ Clean up the output
        string amount = CleanAmount(result.Text);
        Console.WriteLine($"Total amount detected: ${amount}");
    }

    // Helper that sanitises the OCR output
    static string CleanAmount(string raw)
    {
        var cleaned = new string(raw
            .Where(c => char.IsDigit(c) || c == '.' || c == ',')
            .ToArray());

        cleaned = cleaned.Replace(',', '.');
        return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

```
Total amount detected: $23.45
```

หากรูปใบเสร็จมืดกว่าหรือข้อความเอียง คุณอาจเห็นอย่างเช่น `Total amount detected: 23,45` เมธอด `CleanAmount` จะทำให้รูปแบบเป็นทศนิยมมาตรฐาน

---

## ข้อผิดพลาดทั่วไปเมื่อคุณ **recognize text from image**

### 1. พิกัด ROI ผิด
หากสี่เหลี่ยมเล็กเกินไป เอนจินจะตัดอักขระ; หากใหญ่เกินไปจะนำสัญญาณรบกวนกลับมา ใช้เครื่องมือดูภาพเพื่อปรับค่าตัวเลขให้แม่นยำ หรือใช้ไลบรารีประมวลผลภาพอย่างง่าย (เช่น OpenCV) เพื่อตรวจจับขอบใบเสร็จโดยอัตโนมัติ

### 2. สแกนความละเอียดต่ำ
ความแม่นยำของ OCR ลดลงอย่างมากเมื่อต่ำกว่า 150 dpi หากคุณควบคุมกระบวนการสแกน ควรตั้งค่าอย่างน้อย 300 dpi หากต้องทำงานกับไฟล์ความละเอียดต่ำ ให้ลอง `ocrEngine.SetResolution(300);` ก่อนเรียก `Recognize()`

### 3. ใบเสร็จเอียงหรือหมุน
Aspose OCR สามารถหมุนอัตโนมัติได้ แต่ต้องเปิดใช้งาน:

```csharp
ocrEngine.SetAutoRotate(true);
```

### 4. การตั้งค่าภาษา
ภาษาตั้งต้นคืออังกฤษ หากใบเสร็จของคุณมีอักษรอื่น ให้ตั้งค่าภาษาอย่างชัดเจน:

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
```

---

## กรณีขอบและการขยาย – ปรับปรุง **Aspose OCR example**

* **หลายฟิลด์:** อยากดึงวันที่และจำนวนภาษีด้วย? เพียงทำซ้ำขั้นตอน ROI ด้วยสี่เหลี่ยมใหม่และเรียก `Recognize()` อีกครั้ง (หรือรีเซ็ต ROI แล้วใช้เอนจินเดิม)  
* **ประมวลผลเป็นชุด:** ห่อโลจิกในลูป `foreach (var file in Directory.GetFiles(@"C:\Receipts"))` เพื่อจัดการไฟล์หลายสิบไฟล์โดยอัตโนมัติ  
* **การทำงานแบบอะซิงค์:** เมธอด `Recognize` ทำงานแบบซิงโครนัส แต่คุณสามารถย้ายไปทำงานบนเธรดแบ็กกราวด์ด้วย `Task.Run` หากกำลังสร้างแอป UI

---

## ตัวอย่างภาพ

![ตัวอย่างการจดจำข้อความจากรูปภาพ](/images/ocr-demo.png "ภาพหน้าจอแสดงผลลัพธ์ Aspose OCR – จดจำข้อความจากรูปภาพ")

*ภาพหน้าจอแสดงผลลัพธ์คอนโซลหลังจากรันโปรแกรมเต็ม*

---

## สรุป

เราเพิ่ง **recognize text from image** ด้วย Aspose OCR, ผ่านขั้นตอน **load image for OCR**, และสร้างเวิร์กโฟลว์ **extract text from receipt** ที่คุณสามารถนำไปใช้ในโปรเจกต์ .NET ใด ๆ ตัวอย่าง **Aspose OCR** ทั้งหมดใช้เพียงไม่กี่บรรทัด แต่ครอบคลุมสถานการณ์ที่พบบ่อยที่สุด: การเลือก ROI, การทำความสะอาดผลลัพธ์, และการจัดการกับข้อผิดพลาดทั่วไป

ขั้นตอนต่อไป? ลองเปลี่ยนสี่เหลี่ยมเป็นการตรวจจับแบบไดนามิก, ทดลองใช้หลายภาษา, หรือผสานผลลัพธ์เข้าฐานข้อมูลเพื่อการติดตามค่าใช้จ่ายอัตโนมัติ ไม่จำกัดแค่สิ่งที่ทำได้ในตอนนี้ ด้วยพื้นฐานที่คุณมีอยู่แล้ว การขยายต่อไปจะง่ายมาก

มีคำถามหรือใบเสร็จที่ทำให้คุณงง?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-29
description: สกัดข้อความจากภาพด้วย Aspose OCR ใน C# . เรียนรู้การหมุนอัตโนมัติของ
  OCR และวิธีแก้ไขการเอียงของภาพสแกนเพื่อผลลัพธ์ที่สมบูรณ์แบบ.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: th
og_description: ดึงข้อความจากภาพโดยใช้ Aspose OCR คู่มือนี้แสดงการหมุนอัตโนมัติของ
  OCR และวิธีการแก้ไขการเอียงของภาพสแกนใน C#
og_title: ดึงข้อความจากภาพใน C# – OCR ปรับหมุนอัตโนมัติและแก้ไขการเอียง
tags:
- C#
- OCR
- Aspose
- Image Processing
title: สกัดข้อความจากภาพใน C# – คู่มือการหมุนอัตโนมัติ OCR และการปรับแนวภาพ
url: /th/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากรูปภาพใน C# – คำแนะนำ Auto‑Rotate OCR & Deskew

เคยต้องการ **extract text from image** แต่ไฟล์มาที่มุมแปลก ๆ ไหม? มันเป็นปัญหาที่พบบ่อย—โดยเฉพาะเมื่อคุณต้องจัดการกับใบแจ้งหนี้ที่สแกน, ใบเสร็จที่ถ่ายรูป, หรือ PDF ที่เอียง. ข่าวดีคือคุณไม่ต้องเขียนอัลกอริทึมการหมุนเอง. โดยการใช้คุณสมบัติ *auto rotate OCR* ที่มาพร้อมกับ Aspose OCR คุณสามารถให้เอนจินจัดแนวรูปภาพและจากนั้น **extract text from image** ในขั้นตอนเดียวที่ราบรื่น.  

ในบทเรียนนี้เราจะเดินผ่านโปรแกรม C# ที่พร้อมรันเต็มรูปแบบที่:

* เริ่มต้น OCR engine ด้วยการจัดแนวอัตโนมัติและการ deskew,
* จดจำรูปภาพที่หมุนหรือเอียง,
* คืนค่ามุมการหมุนที่ตรวจพบและข้อความที่สกัดออกมา.

## สิ่งที่คุณต้องการ

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.6+) | Aspose OCR มีให้เป็นแพคเกจ NuGet ที่รองรับ runtime เหล่านี้. |
| Visual Studio 2022 (or any C# editor) | ทำให้การเพิ่มแพคเกจ NuGet และการรันแอปคอนโซลเป็นเรื่องง่าย. |
| A sample image (`rotated_document.jpg`) | ไฟล์ควรเป็น JPEG, PNG, BMP หรือ TIFF ที่ไม่ได้ตั้งตรงอย่างสมบูรณ์. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | ให้บริการ `OcrEngine`, `PreprocessingFilters` และประเภทที่เกี่ยวข้อง. |

หากคุณทำเครื่องหมายครบแล้ว คุณก็พร้อมเริ่มได้. หากยังไม่มีก็ให้ดาวน์โหลด Aspose OCR ล่าสุดจาก NuGet—​มันติดตั้งได้ด้วยคลิกเดียว.

---

## ขั้นตอนที่ 1 – Initialise the OCR Engine (Primary Keyword in Action)

สิ่งแรกที่เราทำคือสร้างอินสแตนซ์ `OcrEngine` แล้วบอกให้ **auto rotate OCR** และ **deskew** รูปภาพที่เข้ามา. ธงสองตัวนี้จะถูกรวมด้วยการทำ OR แบบบิต (`|`) เนื่องจาก `PreprocessingFilters` เป็น enum ที่มีแอตทริบิวต์ `[Flags]`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Why this matters:**  
> *Auto‑rotate OCR* ตรวจสอบ baseline ของข้อความในภาพ, ประมาณทิศทางที่ถูกต้อง, แล้วหมุนภาพภายในก่อนทำการจดจำ. *Auto‑deskew* ทำเช่นเดียวกันสำหรับการเอียงเล็กน้อยที่มักพบในเอกสารสแกน. การเปิดใช้งานทั้งสองจะทำให้คุณได้ผลลัพธ์ **extract text from image** ที่ดีที่สุดโดยไม่ต้องแก้ไขภาพด้วยตนเอง.

---

## ขั้นตอนที่ 2 – Recognise the Image and Retrieve the Result

ต่อไปเราจะส่งพาธไฟล์ให้กับ engine. เมธอด `RecognizeImage` จะคืนอ็อบเจ็กต์ `OcrResult` ที่บรรจุมุมการหมุนที่ตรวจพบ, คะแนนความเชื่อมั่น, และผลลัพธ์เป็นข้อความธรรมดา.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Tip:** หากคุณทำงานกับสตรีม (เช่นไฟล์ที่อัปโหลด), ใช้ `ocrEngine.RecognizeImage(Stream)` แทน. ธงการ preprocessing เดิมยังใช้ได้, ดังนั้นคุณยังคงได้รับประโยชน์จาก **auto rotate OCR**.

---

## ขั้นตอนที่ 3 – Display the Rotation Angle and the Extracted Text

สุดท้ายเราจะพิมพ์ข้อมูลสองส่วนไปยังคอนโซล: มุมที่ engine คิดว่าภาพต้องหมุน, และข้อความจริงที่ดึงออกมา.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัวเลขของคุณอาจแตกต่างตามภาพที่ใช้):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

หากภาพอยู่ในตำแหน่งตั้งตรงแล้ว มุมการหมุนจะเป็น `0°`, และคุณยังคงได้ข้อความที่สะอาดเนื่องจากอัลกอริทึม *auto‑deskew*.

---

## ขั้นตอนที่ 4 – Understanding How to Deskew Scanned Image (Secondary Keyword Deep‑Dive)

คุณอาจสงสัยว่า *how to deskew scanned image* เมื่อ OCR engine รายงานการหมุนที่ไม่เป็นศูนย์. ภายใต้ hood, Aspose OCR ใช้ **Hough transform** เพื่อตรวจจับทิศทางของเส้นข้อความที่โดดเด่นที่สุด. จากนั้นมันจะหมุนบิตแมพด้วยมุมตรงข้าม, ทำให้ข้อความตรงขึ้น.

**เมื่อใดที่สำคัญ?**  
* เครื่องสแกนที่ป้อนกระดาษด้วยมุมเล็กน้อย (พบทั่วไปในสำนักงาน).  
* ภาพถ่ายจากสมาร์ทโฟนที่ถ่ายด้วยมือ—​ขอบฟ้ามักไม่สมบูรณ์แบบ.  

**การจัดการกรณีขอบ:**  
หาก `RotationAngle` ของผลลัพธ์มีค่ามหาศาล (เช่น > 45°), engine อาจตีความภาพผิด (อาจเป็นโลโก้หรือกราฟิกที่ไม่มีข้อความ). ในกรณีนั้นคุณสามารถ:

1. หมุนภาพด้วยตนเองโดยใช้ `System.Drawing` ก่อนส่งให้ engine, หรือ  
2. ปิด `AutoRotate` และใช้เฉพาะ `AutoDeskew` หากคุณทราบว่าเอกสารตั้งตรงแล้ว.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## ขั้นตอนที่ 5 – Common Pitfalls & Pro Tips (E‑E‑A‑T in Action)

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Blurry or low‑resolution images** | ความแม่นยำของ OCR ลดลงอย่างมาก; การตรวจจับการหมุนอาจล้มเหลว. | ใช้สแกนที่มีความละเอียดอย่างน้อย 300 dpi; ใช้ฟิลเตอร์เพิ่มความคมก่อน OCR. |
| **Mixed languages** | Engine ตั้งค่าเป็นภาษาอังกฤษโดยอัตโนมัติ; ตัวอักษรต่างภาษาจะกลายเป็นอักขระเสีย. | ตั้งค่า `Language = Language.English | Language.Spanish` (หรือการผสมที่เหมาะสม). |
| **Large files (> 10 MB)** | ความกดดันของหน่วยความจำอาจทำให้เกิด `OutOfMemoryException`. | ลดขนาดภาพก่อน, หรือประมวลผลเป็นส่วนโดยใช้ `OcrEngine.RecognizeRegion`. |
| **Incorrect file path** | `FileNotFoundException` ทำให้โปรแกรมหยุด. | ใช้ `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` เพื่อความทนทาน. |

> **Pro tip:** ควรบันทึก `ocrResult.RotationAngle` และ `ocrResult.Confidence` (หากมี). ตัวชี้วัดเหล่านี้ช่วยให้คุณตัดสินใจว่าควรลองใหม่ด้วยการตั้งค่า preprocessing ที่ต่างออกไปหรือไม่.

---

## ขั้นตอนที่ 6 – Extending the Example (What’s Next?)

ตอนนี้คุณสามารถ **extract text from image** ด้วยการหมุนอัตโนมัติและ deskew แล้ว, ลองพิจารณาขั้นตอนต่อไปนี้:

* **Batch processing** – วนลูปผ่านโฟลเดอร์ของภาพ, เก็บผลลัพธ์แต่ละรายการในฐานข้อมูล, และทำเครื่องหมายภาพที่มี `RotationAngle > 5°` เพื่อการตรวจสอบด้วยมือ.  
* **PDF conversion** – ผสานข้อความที่สกัดกับภาพต้นฉบับเป็น PDF ที่ค้นหาได้โดยใช้ Aspose.PDF.  
* **Language detection** – ใช้ธง `AutoDetectLanguage` ของ Aspose.OCR เพื่อให้ engine เลือกภาษาที่เหมาะสมโดยอัตโนมัติ.  

แต่ละข้อเหล่านี้อิงหลักการเดียวกัน: ให้ไลบรารีจัดการการกำหนดทิศทาง, แล้วคุณโฟกัสที่ตรรกะธุรกิจของคุณ.

---

## ตัวอย่างทำงานเต็ม (Copy‑Paste Ready)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

บันทึกไฟล์เป็น `Program.cs`, รัน `dotnet add package Aspose.OCR`, แล้ว `dotnet run`. คุณจะเห็นมุมและข้อความที่สะอาดพิมพ์ออกมาที่คอนโซล.

---

## สรุป

เราได้สาธิตวิธี **extract text from image** ใน C# พร้อมให้ Aspose OCR ดูแล *auto rotate OCR* และปัญหา *how to deskew scanned image* ที่ซับซ้อน. ด้วยการเปิดใช้ธง preprocessing ทั้งสอง, engine จะจัดแนวภาพที่เอียงโดยอัตโนมัติ, ตรวจจับทิศทางที่ถูกต้อง, และให้ข้อความที่แม่นยำ—ไม่ต้องแก้ไขภาพด้วยตนเอง.

ลองทดลองกับชุดข้อมูลขนาดใหญ่, ภาษาอื่น ๆ, หรือแม้แต่ผสานผลลัพธ์เข้าสู่ PDF ที่ค้นหาได้. ความเป็นไปได้ไม่มีขีดจำกัดเมื่อ OCR engine ทำงานหนักให้คุณ.

**พร้อมจะยกระดับ pipeline เอกสารของคุณหรือยัง?** ดึงโค้ดไปใช้, ชี้ไปที่สแกนของคุณ, แล้วดูมุมการหมุนหายไป. หากเจออุปสรรคใด ๆ, แสดงความคิดเห็นด้านล่าง—ขอให้เขียนโค้ดสนุก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
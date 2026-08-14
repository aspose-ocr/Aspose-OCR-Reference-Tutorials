---
category: general
date: 2026-03-07
description: เรียนรู้วิธีอ่านข้อความจากไฟล์ PNG และดึงข้อความซีริลลิกโดยใช้ Aspose
  OCR, แปลงภาพเป็นข้อความ, และดาวน์โหลดแพ็คเกจภาษาซีริลลิก
draft: false
keywords:
- read text from png
- extract cyrillic text
- convert image to text
- load image for ocr
- download cyrillic language pack
language: th
og_description: เรียนรู้วิธีอ่านข้อความจากไฟล์ PNG, แยกข้อความซีริลลิก, และแปลงภาพเป็นข้อความโดยใช้
  Aspose OCR ใน C#
og_title: อ่านข้อความจาก PNG – แยกข้อความ Cyrillic ด้วย Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: อ่านข้อความจาก PNG – แยกข้อความ Cyrillic ด้วย Aspose OCR
url: /th/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# อ่านข้อความจาก png – แยกข้อความ Cyrillic ด้วย Aspose OCR

ต้องการ **อ่านข้อความจาก png** ไฟล์และดึงอักขระ Cyrillic หรือไม่? ในคู่มือนี้เราจะแสดงวิธีอ่านข้อความจาก png ด้วย Aspose OCR, แยกข้อความ Cyrillic, และ **แปลงภาพเป็นข้อความ** ด้วยเพียงไม่กี่บรรทัดของ C#.  

หากคุณเคยมองภาพหน้าจอของใบแจ้งหนี้ภาษารัสเซียและสงสัยว่าจะเอาคำเหล่านั้นไปเป็นสตริงที่สามารถค้นหาได้อย่างไร คุณมาถูกที่แล้ว เราจะอธิบายวิธี **ดาวน์โหลดแพ็คเกจภาษาซีริลลิก** โดยอัตโนมัติ เพื่อไม่ต้องตามหาไฟล์เพิ่มเติม.

## สิ่งที่คุณจะได้ทำ

* **โหลดภาพสำหรับ OCR** โดยตรงจากดิสก์หรือสตรีม.  
* ตั้งค่าเอนจินเป็น **ภาษาซีริลลิก** โดยไม่ต้องดาวน์โหลดด้วยตนเอง.  
* ทำการจดจำและ **แยกข้อความซีริลลิก** จากไฟล์ PNG.  
* ดูข้อความที่จดจำแล้วพิมพ์ออกที่คอนโซล – ผลลัพธ์ข้อความธรรมดาที่สะอาดซึ่งคุณสามารถนำไปใส่ในฐานข้อมูล, ดัชนีการค้นหา หรือเวิร์กโฟลว์อื่น ๆ.

ไม่มีบริการภายนอก, ไม่มีคีย์คลาวด์, เพียงแพ็คเกจ NuGet ของ Aspose OCR และไม่กี่บรรทัดของ C#.

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดทำงานบน .NET Core, .NET Framework, และ .NET 5+).  
* Visual Studio 2022 หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ.  
* แพ็คเกจ NuGet ของ Aspose.OCR (`dotnet add package Aspose.OCR`).  
* ภาพ PNG ที่มีอักขระซีริลลิก – ตัวอย่างเช่น `cyrillic_sample.png` ที่วางในโฟลเดอร์ชื่อ `YOUR_DIRECTORY`.

> **เคล็ดลับมืออาชีพ:** หากคุณใช้ Visual Studio, คลิกขวาที่โปรเจกต์ → **Manage NuGet Packages** → ค้นหา “Aspose.OCR” และติดตั้งเวอร์ชันเสถียรล่าสุด.

---

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR และสร้างเอนจิน

ก่อนอื่นเราต้องการอินสแตนซ์ของเอนจิน OCR. คลาส `OcrEngine` เป็นจุดเริ่มต้นสำหรับทุกการดำเนินการ.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Create an OCR engine – this object holds all settings and results
var ocrEngine = new OcrEngine();
```

> **ทำไมเรื่องนี้สำคัญ:** เอนจินรวมแพ็คเกจภาษา, ข้อมูลภาพ, และตัวเลือกการจดจำไว้ด้วยกัน การสร้างอินสแตนซ์หนึ่งครั้งและใช้ซ้ำกับหลายภาพสามารถเพิ่มประสิทธิภาพได้.

---

## ขั้นตอนที่ 2 – **โหลดภาพสำหรับ ocr** และตั้งค่าภาษา

ตอนนี้เราบอกเอนจินว่าภาพใดจะประมวลผลและภาษาที่ต้องการค้นหา การตั้งค่า `Language.Cyrillic` จะดาวน์โหลดแพ็คเกจภาษาที่จำเป็นโดยอัตโนมัติในครั้งแรกที่ทำงาน.

```csharp
// 1️⃣ Load the PNG that contains Cyrillic text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");

// 2️⃣ Tell Aspose we want to read Cyrillic characters
ocrEngine.Settings.Language = Language.Cyrillic;   // downloads pack if missing
```

> **กรณีขอบ:** หาก PNG ของคุณมีขนาดใหญ่ (เกิน 5 MB) คุณอาจต้องปรับขนาดก่อนเพื่อเร่งการจดจำ คุณสมบัติ `Image` ยังรับ `Stream` ได้เช่นกัน, ดังนั้นคุณสามารถโหลดจากหน่วยความจำ, คำขอเว็บ, หรือ Azure Blob โดยไม่ต้องสัมผัสระบบไฟล์.

---

## ขั้นตอนที่ 3 – **แปลงภาพเป็นข้อความ** ด้วยการเรียกครั้งเดียว

การจดจำง่ายเพียงแค่เรียก `Recognize()`. หลังจากการเรียกนี้คุณสมบัติ `Text` จะเก็บสตริงที่แยกออกมา.

```csharp
// Run the OCR engine – this does the heavy lifting
ocrEngine.Recognize();

// Grab the result; it’s plain Unicode text
string extractedText = ocrEngine.Text;
```

> **อะไรเกิดขึ้นเบื้องหลัง?** Aspose ใช้ตัวจำแนกแบบเครือข่ายประสาทที่ฝึกด้วย glyphs ซีริลลิกหลายล้านตัว. ไลบรารีทำให้ซับซ้อนทั้งหมดเป็นนามธรรม, ดังนั้นคุณจะได้ Unicode ที่สะอาด.

---

## ขั้นตอนที่ 4 – แสดงผลลัพธ์ (หรือส่งต่อไปที่อื่น)

เพื่อการสาธิต เราจะพิมพ์ข้อความไปที่คอนโซล, แต่คุณสามารถเขียนลงไฟล์, ฐานข้อมูล, หรือส่งต่อไปยังดัชนีการค้นหาได้อย่างง่ายดาย.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Cyrillic Text ===");
Console.WriteLine(extractedText);
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่า `cyrillic_sample.png` มีวลี “Привет мир”):

```
=== Recognized Cyrillic Text ===
Привет мир
```

หากผลลัพธ์ดูเป็นอักขระผิด, ตรวจสอบว่าภาพชัดเจนและคุณได้ตั้งค่า `Language.Cyrillic`. เอนจินโดยค่าเริ่มต้นเป็นภาษาอังกฤษ, ซึ่งจะถืออักขระซีริลลิกเป็นสัญลักษณ์ที่ไม่รู้จัก.

---

## ขั้นตอนที่ 5 – ตัวอย่างเต็มที่สามารถรันได้

รวมทุกอย่างเข้าด้วยกัน, นี่คือโปรแกรมแบบ self‑contained ที่คุณสามารถคัดลอกและวางลงในโปรเจกต์คอนโซลใหม่.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Load the PNG and select Cyrillic language
        // -------------------------------------------------
        // Replace the path with the location of your PNG
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");
        ocrEngine.Settings.Language = Language.Cyrillic; // auto‑downloads pack

        // -------------------------------------------------
        // 3️⃣ Perform recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

บันทึกไฟล์เป็น `Program.cs`, รัน `dotnet run`, และคุณควรเห็นข้อความซีริลลิกที่พิมพ์ออกมา.

---

## คำถามทั่วไป & การแก้ไขปัญหา

| Question | Answer |
|----------|--------|
| **ถ้าแพ็คเกจภาษาล้มเหลวในการดาวน์โหลด?** | ตรวจสอบว่าเครื่องมีการเชื่อมต่ออินเทอร์เน็ต. แพ็คเกจจะถูกแคชไว้ที่ `%USERPROFILE%\.Aspose\OCR\Languages`. การลบโฟลเดอร์นั้นจะบังคับให้ดาวน์โหลดใหม่. |
| **ฉันสามารถอ่านภาษาอื่น ๆ นอกจากซีริลลิกได้หรือไม่?** | แน่นอน – แทนที่ `Language.Cyrillic` ด้วย `Language.English`, `Language.Arabic` เป็นต้น. โลจิกการดาวน์โหลดอัตโนมัติเดียวกันจะทำงาน. |
| **PNG ของฉันมีสัญญาณรบกวน – ผลลัพธ์แย่ลง. ฉันทำอะไรได้บ้าง?** | ทำการประมวลผลล่วงหน้าภาพ: เพิ่มคอนทราสต์, แปลงเป็นระดับสีเทา, หรือใช้ฟิลเตอร์เมเดียน. Aspose OCR ยังมีตัวเลือก `Settings.ImagePreprocess`. |
| **มีวิธีใดบ้างที่จะรับกรอบรอบคำแต่ละคำ?** | ใช่, หลังจาก `Recognize()` คุณสามารถตรวจสอบ `ocrEngine.Regions` ซึ่งจะคืนค่าเรคตังเกิลสำหรับแต่ละคำที่ตรวจพบ. |
| **ฉันต้องการไลเซนส์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** | การประเมินฟรีทำงานได้สูงสุด 100 หน้า. สำหรับโครงการเชิงพาณิชย์ให้ซื้อไลเซนส์ – จะลบลายน้ำการประเมินและเปิดใช้งานการประมวลผลเป็นชุดความเร็วสูง. |

---

## ขั้นตอนต่อไป – ขยายโซลูชัน

* **Batch processing:** วนลูปผ่านโฟลเดอร์ของ PNGs, รวบรวมข้อความทั้งหมดลงในไฟล์ CSV.  
* **Integration with Azure Cognitive Search:** ทำดัชนีข้อความซีริลลิกที่แยกออกเพื่อการค้นหาอย่างรวดเร็ว.  
* **Combine with PDF conversion:** ใช้ Aspose.PDF เพื่อแปลง PDF สแกนเป็น PNG ก่อน, แล้วรันกระบวนการ OCR เดียวกัน.  

ทุกสถานการณ์เหล่านี้ใช้รูปแบบหลักที่เราเพิ่งครอบคลุม: **โหลดภาพสำหรับ OCR → ตั้งค่าภาษา → จดจำ → ใช้ข้อความ**.

---

## สรุป

ตอนนี้คุณรู้วิธี **อ่านข้อความจาก png**, **แยกข้อความซีริลลิก**, และ **แปลงภาพเป็นข้อความ** ด้วย Aspose OCR ใน C#. ขั้นตอนสำคัญคือการสร้างเอนจิน, โหลดภาพ, เลือกภาษาที่เหมาะสม (ซึ่งจะ **ดาวน์โหลดแพ็คเกจภาษาซีริลลิก** อัตโนมัติ), และสุดท้ายเรียก `Recognize()`.

ลองใช้กับภาพต่าง ๆ, ทดลองกับตัวเลือก `Settings`, และดูแอปพลิเคชันของคุณกลายเป็นที่ค้นหาได้, รองรับหลายภาษา, และฉลาดยิ่งขึ้น.  

ขอให้สนุกกับการเขียนโค้ด, และอย่าลังเลที่จะแสดงความคิดเห็นหากคุณเจออุปสรรค!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
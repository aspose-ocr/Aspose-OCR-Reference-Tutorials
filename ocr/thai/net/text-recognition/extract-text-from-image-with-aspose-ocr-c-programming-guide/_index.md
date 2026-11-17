---
category: general
date: 2026-03-13
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# เรียนรู้วิธีโหลดภาพสำหรับ OCR,
  รัน OCR บนภาพ, และดึงข้อความแบบ Cyrillic ด้วยโค้ดขั้นตอนที่ชัดเจน
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- extract cyrillic text
- recognize cyrillic text
language: th
og_description: ดึงข้อความจากภาพใน C# ด้วย Aspose OCR. บทเรียนนี้แสดงวิธีโหลดภาพสำหรับ
  OCR, รัน OCR บนภาพ, และดึงข้อความซีริลลิกอย่างมีประสิทธิภาพ.
og_title: ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือ C#
tags:
- Aspose OCR
- C#
- Image Processing
title: ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือการเขียนโปรแกรม C#
url: /th/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือการเขียนโปรแกรม C#

เคยต้องการ **extract text from image** แต่ไม่แน่ใจว่าห้องสมุดใดจะจัดการอักขระ Cyrillic ได้อย่างไม่มีปัญหาหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ—การสแกนใบแจ้งหนี้, การตรวจสอบหนังสือเดินทาง, หรือการจดบันทึกอย่างรวดเร็ว—การได้ข้อความที่เชื่อถือได้จากภาพเป็นสิ่งสำคัญ.  

ในคู่มือนี้เราจะอธิบายขั้นตอนที่แม่นยำเพื่อ **load image for OCR**, ตั้งค่า Aspose OCR, **run OCR on image**, และสุดท้าย **extract Cyrillic text** ด้วยเพียงไม่กี่บรรทัดของ C#. เมื่อเสร็จคุณจะมีโค้ดสั้น ๆ ที่พร้อมรันและพิมพ์ข้อความที่ถูกจดจำลงคอนโซล.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการติดตั้งและอ้างอิงแพ็กเกจ NuGet ของ Aspose OCR.  
- วิธีที่ถูกต้องในการชี้เอ็นจิ้นไปที่ทรัพยากร language‑pack.  
- ทำไมการเลือก `Language.Cyrillic` ถึงสำคัญสำหรับสคริปต์ที่ไม่ใช่ละติน.  
- ปัญหาที่พบบ่อย (ทรัพยากรหาย, รูปแบบภาพที่ไม่รองรับ) และวิธีหลีกเลี่ยง.  
- ตัวอย่างที่สมบูรณ์และสามารถรันได้ซึ่งคุณสามารถนำไปใช้ในโปรเจค .NET ใดก็ได้.

ไม่จำเป็นต้องมีประสบการณ์ OCR มาก่อน แต่ความคุ้นเคยพื้นฐานกับ C# และ Visual Studio จะทำให้การเรียนรู้เป็นไปอย่างราบรื่น.

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มลงลึก ตรวจสอบให้แน่ใจว่าคุณมี:

1. **.NET 6.0** หรือใหม่กว่า (โค้ดทำงานบน .NET Core และ .NET Framework).  
2. **Visual Studio 2022** (หรือโปรแกรมแก้ไขใด ๆ ที่รองรับ C#).  
3. แพ็กเกจ NuGet **Aspose.OCR**. ติดตั้งผ่าน Package Manager Console:  

   ```powershell
   Install-Package Aspose.OCR
   ```

4. โฟลเดอร์ที่มี language pack ของ OCR (ดาวน์โหลดได้จากเว็บไซต์ของ Aspose).  
5. ไฟล์รูปภาพ (`cyrillic.png` ในตัวอย่าง) ที่มีข้อความ Cyrillic ที่คุณต้องการอ่าน.

> **เคล็ดลับ:** เก็บโฟลเดอร์ language‑pack ไว้ข้างๆ ไดเรกทอรี `bin` ของโปรเจคของคุณ; จะทำให้การจัดการเส้นทางง่ายขึ้น.

## ขั้นตอนที่ 1 – โหลดรูปภาพสำหรับ OCR

สิ่งแรกที่คุณต้องทำคือให้เอ็นจิ้นมีบิตแมพเพื่อทำงาน Aspose OCR รองรับ `ImageStream` ซึ่งสามารถสร้างโดยตรงจากเส้นทางไฟล์.

```csharp
using Aspose.OCR;

// Step 1: Load the image you want to process
string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
ImageStream image = ImageStream.FromFile(imagePath);
```

*ทำไมเรื่องนี้สำคัญ:* การโหลดภาพตั้งแต่ต้นทำให้คุณตรวจสอบได้ว่าไฟล์มีอยู่และอยู่ในรูปแบบที่รองรับ (PNG, JPEG, BMP, ฯลฯ). หากไฟล์หาย การเรียก `FromFile` จะโยนข้อยกเว้นที่ชัดเจน ช่วยคุณหลีกเลี่ยงข้อผิดพลาด OCR ที่ไม่ชัดเจนในภายหลัง.

## ขั้นตอนที่ 2 – ตั้งค่า OCR Engine และทรัพยากร

ต่อไป สร้างอินสแตนซ์ของ OCR engine และชี้ไปยังโฟลเดอร์ที่เก็บ language pack. หากไม่มีทรัพยากรที่ถูกต้อง เอ็นจิ้นจะไม่รู้วิธีตีความ glyph ของ Cyrillic.

```csharp
// Step 2: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Tell Aspose where the language resources live
string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
ocrEngine.SetResourcesPath(resourcesPath);
```

*ทำไมเรื่องนี้สำคัญ:* เมธอด `SetResourcesPath` เป็นสะพานระหว่างโค้ดของคุณกับไฟล์ข้อมูลที่มีรูปแบบอักขระสำหรับแต่ละภาษาที่รองรับ. การลืมขั้นตอนนี้มักทำให้ผลลัพธ์เป็นข้อความเสียหายหรือเกิด `ResourceNotFoundException`.

## ขั้นตอนที่ 3 – เลือกภาษาและ **รัน OCR บนรูปภาพ**

ตอนนี้เราจะเลือกภาษาที่คาดว่าจะพบ. เนื่องจากตัวอย่างนี้เกี่ยวกับ Cyrillic เราตั้งค่า `Language.Cyrillic`. หากต้องการจัดการหลายสคริปต์ คุณสามารถรวมด้วยตัวดำเนินการ OR แบบบิต (`|`).

```csharp
// Step 3: Select the language you want to recognize
ocrEngine.Language = Language.Cyrillic;

// Assign the previously loaded image to the engine
ocrEngine.Image = image;

// Finally, perform the recognition
ocrEngine.Recognize();
```

*ทำไมเรื่องนี้สำคัญ:* การระบุภาษา จะทำให้พื้นที่ค้นหาของอัลกอริทึม OCR แคบลงอย่างมาก ทำให้ความเร็วและความแม่นยำดีขึ้นอย่างมาก. เมื่อคุณ **run OCR on image** ด้วยแฟล็กภาษาที่ถูกต้อง คุณจะพบการจดจำที่ผิดพลาดน้อยลงมาก.

## ขั้นตอนที่ 4 – ดึงและใช้ข้อความ Cyrillic ที่ได้

หลังจากการจดจำเสร็จสิ้น เอ็นจิ้นจะเก็บผลลัพธ์ไว้ในคุณสมบัติ `Text`. ตอนนี้คุณสามารถแสดงผล, เขียนลงไฟล์, หรือส่งต่อไปยังระบบอื่นได้.

```csharp
// Step 4: Output the recognized text
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== Extracted Cyrillic Text ===");
Console.WriteLine(recognizedText);
```

ผลลัพธ์ที่แสดงบนคอนโซลโดยทั่วไปจะเป็นดังนี้:

```
=== Extracted Cyrillic Text ===
Привет, мир! Это тестовое изображение.
```

หากผลลัพธ์มีสัญลักษณ์ที่ไม่คาดคิด ให้ตรวจสอบอีกครั้งว่า language pack ตรงกับเวอร์ชันของ Aspose OCR ที่คุณติดตั้ง.

## ตัวอย่างทำงานเต็มรูปแบบ – รวมทุกขั้นตอน

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกและวางลงในโปรเจคคอนโซลใหม่. แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางจริงบนเครื่องของคุณ.

```csharp
using System;
using Aspose.OCR;

namespace ExtractCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the image you want to process
            string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // 2️⃣ Initialize OCR engine and point to language resources
            OcrEngine ocrEngine = new OcrEngine();
            string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
            ocrEngine.SetResourcesPath(resourcesPath);

            // 3️⃣ Choose Cyrillic language and run OCR on image
            ocrEngine.Language = Language.Cyrillic;
            ocrEngine.Image = image;
            ocrEngine.Recognize();

            // 4️⃣ Extract and display the text
            string result = ocrEngine.Text;
            Console.WriteLine("=== Extracted Cyrillic Text ===");
            Console.WriteLine(result);
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมควรพิมพ์ข้อความที่ปรากฏใน `cyrillic.png` อย่างตรงกัน. หากภาพมีวลี “Привет, мир!” คุณจะเห็นบรรทัดนั้นบนคอนโซลโดยไม่มีสัญลักษณ์เพิ่มเติม.

## กรณีขอบและการแก้ไขปัญหา

| Situation | What to Check | Suggested Fix |
|-----------|---------------|---------------|
| **ไม่มี language packs** | เส้นทาง `resourcesPath` ชี้ไปยังโฟลเดอร์ที่มีไฟล์ `.dat` หรือไม่? | ดาวน์โหลด language packs ใหม่จาก Aspose แล้ววางไว้ในโฟลเดอร์ที่ระบุ. |
| **รูปแบบภาพที่ไม่รองรับ** | ไฟล์เป็น PNG, JPEG, BMP หรือ TIFF หรือไม่? | แปลงภาพเป็นหนึ่งในรูปแบบที่รองรับก่อนเรียก `FromFile`. |
| **อักขระเสียในผลลัพธ์** | คุณตั้งค่า `ocrEngine.Language` อย่างถูกต้องหรือไม่? | ใช้ `Language.Cyrillic` (หรือรวมแฟล็กสำหรับหลายภาษา). |
| **ความช้าของประสิทธิภาพกับภาพขนาดใหญ่** | ความละเอียดของภาพ > 3000 px หรือไม่? | ลดขนาดภาพให้เหมาะสม (เช่น ความกว้าง 1024 px) ก่อนทำ OCR. |

## หัวข้อที่เกี่ยวข้องที่คุณอาจสนใจต่อไป

- **Extract text from image** ใน PDF ด้วย Aspose PDF + OCR.  
- **Load image for OCR** จาก `Stream` (มีประโยชน์เมื่อภาพมาจากเว็บ API).  
- ใช้ **run OCR on image** แบบขนานเพื่อเร่งการประมวลผลเป็นชุด.  
- **Extract cyrillic text** จากบันทึกมือด้วยโหมดการเขียนมือของ Aspose OCR.  
- ผสานผลลัพธ์กับ **recognize cyrillic text** ในฐานข้อมูลเพื่อทำดัชนีการค้นหา.

## สรุป

เราได้แสดงวิธี **extract text from image** ด้วย Aspose OCR ครอบคลุมตั้งแต่การโหลดภาพจนถึงการพิมพ์อักขระ Cyrillic ที่จดจำได้ โปรแกรมสั้น ๆ ที่เป็นอิสระนี้แสดงโค้ดขั้นต่ำที่คุณต้องการ ในขณะที่ตารางการแก้ไขปัญหาช่วยคุณหลีกเลี่ยงปัญหาที่พบบ่อยที่สุด  

ลองใช้กับสกรีนช็อตของคุณเอง, เปลี่ยน language pack เป็น Arabic หรือ Chinese, แล้วดูว่ารูปแบบเดียวกันทำงานได้ทั่วโลกอย่างไร. ขอให้เขียนโค้ดอย่างสนุกและผลลัพธ์ OCR ของคุณใสเหมือนคริสตัล!

![Extract text from image example](extract-text-from-image.png "Extract text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
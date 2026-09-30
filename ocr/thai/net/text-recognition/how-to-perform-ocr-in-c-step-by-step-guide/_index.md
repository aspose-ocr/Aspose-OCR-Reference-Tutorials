---
category: general
date: 2026-02-14
description: วิธีทำ OCR ใน C# ด้วย Aspose.OCR – เรียนรู้การดึงข้อความจากรูปภาพ, โหลดรูปภาพจากไฟล์และรัน
  OCR บนรูปภาพอย่างรวดเร็ว.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: th
og_description: วิธีทำ OCR ใน C# ด้วย Aspose.OCR คู่มือนี้จะแสดงวิธีการดึงข้อความจากภาพ
  โหลดภาพจากไฟล์ และทำ OCR บนภาพอย่างมีประสิทธิภาพ
og_title: วิธีทำ OCR ใน C# – บทเรียนการเขียนโปรแกรมครบถ้วน
tags:
- OCR
- C#
- Aspose
- Image Processing
title: วิธีทำ OCR ใน C# – คู่มือแบบขั้นตอนต่อขั้นตอน
url: /th/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ใน C# – การสอนโปรแกรมเต็มรูปแบบ

เคยสงสัย **how to perform OCR** บนรูปภาพที่คุณถ่ายด้วยโทรศัพท์ของคุณหรือไม่? บางทีคุณอาจต้องดึงข้อความป้ายถนนจากไฟล์ JPEG สำหรับแอปนำทาง, หรือคุณมีชุดสัญญาที่สแกนแล้วและต้องการแปลงเป็นข้อความที่สามารถค้นหาได้ สรุปคือคุณต้องการ *extract text from image* โดยไม่ต้องส่งข้อมูลใด ๆ ไปยังคลาวด์

ข่าวดีคือคุณสามารถทำทั้งหมดนี้ได้แบบออฟไลน์ด้วย Aspose.OCR สำหรับ .NET ในบทเรียนนี้เราจะอธิบายการโหลดรูปภาพจากไฟล์, การจดจำข้อความจาก JPG, และสุดท้าย **run OCR on image** ไฟล์โดยสมบูรณ์แบบออฟไลน์ เมื่อเสร็จคุณจะได้โค้ดสั้นที่พร้อมรันซึ่งพิมพ์ข้อความอาหรับที่จดจำได้ลงคอนโซล

> **What you’ll get:** โปรแกรม C# ที่ทำงานได้เอง, คำอธิบายว่าทำไมแต่ละบรรทัดถึงสำคัญ, และเคล็ดลับการจัดการกับกรณีขอบที่พบบ่อย เช่น แหล่งข้อมูลหายหรือภาษาที่ไม่รองรับ

## Prerequisites

ก่อนที่เราจะดำเนินการต่อ, ตรวจสอบให้แน่ใจว่าคุณมี:

| ความต้องการ | เหตุผล |
|-------------|--------|
| .NET 6.0 หรือใหม่กว่า (หรือ .NET Framework 4.7+) | Aspose.OCR รองรับ .NET Standard 2.0, ดังนั้น runtime สมัยใหม่ใดก็ทำงานได้ |
| Visual Studio 2022 (หรือ VS Code พร้อมส่วนขยาย C#) | IDE ทำให้จัดการแพ็กเกจ NuGet และรันแอปคอนโซลง่ายขึ้น |
| แพ็กเกจ NuGet Aspose.OCR (`Aspose.OCR`) | นี่คือไลบรารีที่ทำงาน OCR จริง ๆ |
| โฟลเดอร์ที่มีทรัพยากร OCR แบบออฟไลน์ (ดาวน์โหลดจาก Aspose) | ทรัพยากรออฟไลน์ช่วยหลีกเลี่ยงการเรียก HTTP ใด ๆ ระหว่างการจดจำ |
| ไฟล์รูปภาพ (เช่น `arabic_sign.jpg`) | เราจะใช้ JPEG ที่มีข้อความอาหรับ, แต่ภาษาทุกภาษาใช้งานได้ |

หากคุณขาดสิ่งใดสิ่งหนึ่ง, ให้ดาวน์โหลดตอนนี้—ไม่มีประโยชน์ที่จะเริ่มบทเรียนแล้วเจอการพึ่งพาที่หายไปครึ่งทาง

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR และเตรียมทรัพยากร

แรกเริ่มให้เพิ่มแพ็กเกจ Aspose.OCR ลงในโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.OCR
```

หลังจากติดตั้งแพ็กเกจแล้ว, ดาวน์โหลด **offline OCR resource bundle** จากเว็บไซต์ Aspose. แตกไฟล์ไปยังโฟลเดอร์บนเครื่องของคุณ, ตัวอย่างเช่น:

```
C:\OCRResources\
```

> **Why this matters:** การโหลดทรัพยากรครั้งเดียวที่เริ่มต้นช่วยลดความล่าช้าของเครือข่ายและทำให้โซลูชันของคุณเป็นมิตรกับ GDPR เพราะไม่มีข้อมูลออกจากเครื่อง

## ขั้นตอนที่ 2: สร้าง OCR Engine และชี้ไปยังโฟลเดอร์ทรัพยากร

ตอนนี้เราจะสร้างอินสแตนซ์ของคลาส `Engine` และบอกตำแหน่งที่เก็บทรัพยากร นี่คือหัวใจของ **how to perform OCR** แบบออฟไลน์

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **Pro tip:** ห่อการเรียก `LoadResources` ด้วยบล็อก try‑catch หากคุณคาดว่าเส้นทางโฟลเดอร์อาจผิดพลาด ข้อยกเว้นจะบอกคุณว่าไฟล์ใดหายไป

## ขั้นตอนที่ 3: โหลดรูปภาพจากไฟล์

ต่อไปเราต้อง **load image from file** เพื่อให้ engine สามารถวิเคราะห์ได้ Aspose.OCR ทำงานกับตัวห่อ `ImageStream` ของมันเอง

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

หากรูปภาพของคุณอยู่ที่อื่น, เพียงเปลี่ยนเส้นทาง `ImageStream` จะทำหน้าที่แยกการจัดการบิตแมพพื้นฐานออก, ดังนั้นคุณไม่ต้องกังวลเรื่องความเข้ากันได้ของ GDI+

## ขั้นตอนที่ 4: จดจำข้อความจาก JPG ด้วยการตั้งค่าภาษา

ต่อไปคือหัวใจของ **how to perform OCR**—การจดจำอักขระจริง ๆ เราจะขอการจดจำภาษาอาหรับ, แต่คุณสามารถเปลี่ยน `Language.Arabic` เป็นภาษาอื่นที่รองรับได้

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **Why specify a language?** เครื่องมือ OCR ใช้พจนานุกรมและโมเดลอักขระที่เฉพาะเจาะจงตามภาษา การระบุภาษาที่ถูกต้องช่วยเพิ่มความแม่นยำอย่างมาก, โดยเฉพาะสคริปต์ที่มีรูปทรงซับซ้อนเช่นอาหรับ

## ขั้นตอนที่ 5: แสดงข้อความที่ดึงออกมา

สุดท้าย, ให้เรา **extract text from image** และพิมพ์ออกมา นี่เป็นวิธีที่ง่ายที่สุดในการตรวจสอบว่า OCR ทำงานสำเร็จ

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

เมื่อคุณรันโปรแกรม, คุณควรเห็นวลีอาหรับที่อยู่บนป้ายพิมพ์ในคอนโซล หากผลลัพธ์ดูเป็นอักขระผิด, ตรวจสอบอีกครั้งว่าภาษาได้ถูกเลือกอย่างถูกต้องและโฟลเดอร์ทรัพยากรมีไฟล์ข้อมูลอาหรับ

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมคอมไพล์ที่เชื่อมขั้นตอนทั้งหมดเข้าด้วยกัน คัดลอกและวางลงในโปรเจกต์คอนโซลใหม่ (`dotnet new console`) แล้วกด **F5**

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
=== OCR Result ===
مطار القاهره الدولي
```

หากคุณเปลี่ยนรูปภาพเป็นป้ายภาษาอังกฤษและตั้งค่า `Language.English`, โค้ดเดียวกันจะพิมพ์ข้อความภาษาอังกฤษ นั่นแสดงให้เห็นว่า **run OCR on image** มีความยืดหยุ่นแค่ไหน

## ดึงข้อความจากรูปภาพ – การจัดการกับสถานการณ์ทั่วไป

### 1. หลายหน้า หรือภาพหลายเฟรม

รูปแบบภาพบางประเภท (เช่น TIFF) สามารถมีหลายหน้าได้ เพื่อ **extract text from image** ในกรณีเช่นนี้ ให้วนลูปแต่ละเฟรม:

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. ภาพความละเอียดต่ำ

ความแม่นยำของ OCR ลดลงอย่างมากเมื่อความละเอียดต่ำกว่า 70 dpi หากผลลัพธ์ดูเบลอ, ควรพิจารณาขยายภาพก่อน:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. ไม่มีแพ็คเกจภาษา

หากคุณได้รับข้อยกเว้นเช่น *“Language data not found”*, ตรวจสอบอีกครั้งว่าไฟล์ `.dat` ที่สอดคล้องกันมีอยู่ใน `ResourceFolder` ของคุณหรือไม่ Aspose มีไฟล์ zip แยกสำหรับแต่ละภาษา

## รัน OCR บนรูปภาพ – เคล็ดลับประสิทธิภาพ

- **Cache the Engine:** การสร้าง `Engine` ใหม่สำหรับแต่ละภาพเพิ่มภาระงาน ควรเก็บอินสแตนซ์เดียวไว้ใช้สำหรับการประมวลผลเป็นชุด
- **Parallelize Safely:** `Engine` ปลอดภัยต่อการทำงานหลายเธรดสำหรับการดำเนินการแบบอ่านอย่างเดียวหลังจาก `LoadResources`. คุณสามารถสร้างหลายงานที่แต่ละงานเรียก `Recognize` บนภาพต่าง ๆ
- **Dispose When Done:** แม้ว่า `Engine` จะ implements `IDisposable`, .NET GC จะทำความสะอาดในที่สุด การเรียก `ocrEngine.Dispose()` อย่างชัดเจนในบล็อก `using` เป็นนิสัยที่ดี

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## จดจำข้อความจาก JPG – กรณีขอบที่ควรระวัง

| สถานการณ์ | สิ่งที่ต้องตรวจสอบ | วิธีแก้ |
|-----------|-------------------|---------|
| **JPEG เสียหาย** | `ImageStream.FromFile` ขว้าง `FileNotFoundException` หรือ `ArgumentException`. | ตรวจสอบความสมบูรณ์ของไฟล์, อาจบันทึกรูปภาพใหม่ด้วยโปรแกรมกราฟิก |
| **ภาษาไม่รองรับ** | `Language` enum ไม่มีภาษาที่คุณต้องการ. | อัปเดต Aspose.OCR เป็นเวอร์ชันล่าสุด; มีการเพิ่มภาษาตามประจำ |
| **ภาพหลายสคริปต์** (เช่น English + Arabic) | ตัวเลือกภาษาเดียวอาจพลาดสคริปต์ที่สอง. | รัน OCR สองครั้งด้วยตัวเลือกภาษาต่างกันและรวมผลลัพธ์ |

## สรุป – ตอนนี้คุณรู้วิธีทำ OCR ใน C# แล้ว

ในคู่มือนี้เราได้ครอบคลุม **how to perform OCR** ด้วย Aspose.OCR ตั้งแต่การติดตั้งแพ็กเกจ NuGet จนถึงการพิมพ์ข้อความที่จดจำได้ คุณได้เรียนรู้การ **load image from file**, **extract text from image**, **recognize text from jpg**, และการ **run OCR on image** อย่างปลอดภัยในรูปแบบพร้อมใช้งานสำหรับการผลิต

### สิ่งต่อไป?

- **ทดลองกับฟอร์แมตไฟล์อื่น** เช่น PNG หรือ BMP—แค่เปลี่ยนส่วนขยายไฟล์
- **รวมเข้ากับฐานข้อมูล** เพื่อเก็บผลลัพธ์ OCR สำหรับคลังข้อมูลที่สามารถค้นหาได้
- **ผสานกับคอมพิวเตอร์วิชั่น** (เช่น ตรวจจับพื้นที่ข้อความก่อน OCR) เพื่อเพิ่มความเร็ว

คุณสามารถปรับแต่งการตั้งค่าภาษา, ประมวลผลโฟลเดอร์เป็นชุด, หรือเชื่อมผลลัพธ์เข้ากับเว็บ API ได้ตามต้องการ OCR เป็นบล็อกพื้นฐาน; พลังที่แท้จริงจะมาจากการนำมันไปรวมกับกระบวนการทำงานที่ใหญ่ขึ้น

ขอให้สนุกกับการเขียนโค้ด, และขอให้รูปภาพของคุณใสเหมือนคริสตัลเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
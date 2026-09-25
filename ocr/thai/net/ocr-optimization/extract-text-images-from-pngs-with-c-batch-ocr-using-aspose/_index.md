---
category: general
date: 2026-02-09
description: ดึงข้อความจากรูปภาพอย่างรวดเร็วด้วย C# โดยตั้งค่าการทำงานพร้อมกันสูงสุดสำหรับ
  OCR แบบชุด – เรียนรู้การแปลงหน้าสแกน, จัดการ OCR หลายรูปภาพและอ่านข้อความจาก PNG
  อย่างมีประสิทธิภาพ.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: th
og_description: ดึงข้อความจากรูปภาพใน C# โดยกำหนดระดับการทำงานขนานสูงสุด บทเรียนนี้แสดงวิธีแปลงหน้าสแกน,
  รัน OCR หลายรูปภาพพร้อมกัน และอ่านข้อความจากไฟล์ PNG ด้วย Aspose OCR.
og_title: สกัดข้อความจากภาพ PNG ด้วย C# – คู่มือ OCR แบบแบตช์ครบวงจร
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: สกัดข้อความจากภาพ PNG ด้วย C# – OCR แบบแบตช์ด้วย Aspose OCR
url: /th/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากภาพ PNG ด้วย C# – การทำ OCR เป็นชุดโดยใช้ Aspose OCR

เคยต้อง **ดึงข้อความจากภาพ** จากโฟลเดอร์ที่มี PNG สแกนหลายไฟล์แล้วรู้สึกติดขัดที่คำถาม “จะทำให้เร็วขึ้นได้อย่างไร?” หรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการจริง ๆ นักพัฒนาต้อง **ตั้งค่าการทำงานขนานสูงสุด** เพื่อให้หลายสิบหน้าได้รับการประมวลผลในไม่กี่วินาทีแทนที่จะเป็นนาที  

ในคู่มือนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่ง **แปลงหน้าที่สแกน**, ทำ **OCR หลายภาพ**, และสุดท้าย **อ่านข้อความจาก PNG** โดยไม่ต้องเสียเวลา ไม่มีลิงก์ “ดูเอกสาร” ที่คลุมเครือ—เพียงโค้ดที่คุณคัดลอก‑วาง, คำอธิบายว่าทำไมบรรทัดแต่ละบรรทัดสำคัญ, และเคล็ดลับเพื่อหลีกเลี่ยงปัญหาที่พบบ่อย

> **เคล็ดลับระดับมืออาชีพ:** หากคุณใช้ Aspose OCR อยู่แล้ว คุณจะสังเกตเห็นว่า `OcrEngine` คลาสเดียวกันปรากฏที่นี่ แต่เราจะปรับแต่งการตั้งค่าของมันเพื่อการประมวลผลขนานที่แท้จริง

---

## สิ่งที่คุณต้องมี

- **.NET 6+** (หรือ .NET Framework 4.6+). API ทำงานเช่นเดียวกัน แต่ runtime ที่ใหม่กว่าให้การจัดการเธรดที่ดีกว่า  
- **Aspose.OCR for .NET** – ติดตั้งผ่าน NuGet: `Install-Package Aspose.OCR`  
- โฟลเดอร์ที่มีไฟล์ PNG สแกนอยู่หลายไฟล์ (`page1.png`, `page2.png`, …)  
- IDE หรือ editor ที่คุณถนัด (Visual Studio, Rider, VS Code…)

เท่านี้แค่นั้น ไม่ต้องใช้บริการเพิ่มเติม ไม่ต้องมีคีย์คลาวด์ เพียงการประมวลผลแบบโลคัล

---

## ดึงข้อความจากภาพ – ตั้งค่าการทำงานขนานสูงสุดสำหรับ Batch OCR

เมื่อคุณสั่ง OCR บนหลายไฟล์พร้อมกัน เอนจินจะใช้เธรดเดียวโดยค่าเริ่มต้น ซึ่งปลอดภัยแต่ช้าอย่างรุนแรง โดยการกำหนดค่า `MaxDegreeOfParallelism` คุณบอกเอนจินว่าจะสร้างเธรดพร้อมกันได้กี่เธรด

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**ทำไมต้องเป็น 4?**  
สี่เป็นค่าที่เหมาะสมสำหรับแล็ปท็อปสมัยใหม่ส่วนใหญ่—มีคอร์พอให้ CPU ทำงานเต็มที่ แต่ไม่มากจนทำให้กระบวนการอื่นขาดแคลน หากคุณรันบนเซิร์ฟเวอร์ที่มี 16 คอร์ ให้เพิ่มเป็น 12 หรือ 14 เพื่อเพิ่มความเร็วอย่างเห็นได้ชัด

---

## แปลงหน้าที่สแกน – สร้างคอลเลกชัน Image Stream

Aspose ต้องการภาพแต่ละไฟล์เป็น `ImageStream` ตัวช่วย `FromFile` จะอ่านไฟล์, เก็บไว้ในหน่วยความจำ, แล้วส่งต่อให้เอนจิน OCR คุณยังสามารถส่ง `MemoryStream` ได้หากภาพมาจากฐานข้อมูลหรือการตอบสนอง HTTP

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**กรณีขอบ:** หากไฟล์ใดหายหรือเสียหาย `FromFile` จะโยน `FileNotFoundException` ให้ห่อการสร้างใน `try/catch` หากคุณคาดว่าจะได้รับอินพุตที่ไม่เสถียร

---

## ทำ OCR หลายภาพ – การทำ Batch OCR

ตอนนี้งานหนักเริ่มทำงาน `RecognizeBatch` จะสปินเธรดตามจำนวนที่คุณตั้งไว้ก่อนหน้า, ประมวลผลแต่ละภาพ, และคืนรายการของอ็อบเจกต์ `OcrResult`

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

เบื้องหลังแต่ละเธรดจะโหลดภาพของตน, รันเครือข่ายประสาทเทียม, และดึงข้อความธรรมดาออกมา ผลลัพธ์จะเรียงตามลำดับของรายการอินพุต ดังนั้นคุณสามารถแมปหน้า 1 → ผลลัพธ์ 0 ได้อย่างปลอดภัย เป็นต้น

---

## อ่านข้อความ PNG – แสดงเนื้อหาที่ดึงออกมา

สุดท้ายเราวนลูปผ่านผลลัพธ์และพิมพ์ข้อความธรรมดาไปที่คอนโซล ที่นี่คุณสามารถส่งออกไปยังไฟล์, ฐานข้อมูล, หรือแม้กระทั่งบริการ NLP ต่อไป

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### ตัวอย่างผลลัพธ์บนคอนโซล

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

หากคุณเห็นส่วนที่เป็นค่าว่าง ตรวจสอบว่า PNG ไม่ใช่ภาพสีขาวทั้งหมด—OCR ต้องการความคอนทราสต์บ้าง

---

## เคล็ดลับปฏิบัติ & ปัญหาที่พบบ่อย

| สถานการณ์ | วิธีแก้ |
|-----------|--------|
| **ความกดดันของหน่วยความจำ** ในชุดข้อมูลขนาดใหญ่ | ประมวลผลภาพเป็นชิ้น ๆ 10‑20 ไฟล์ แล้วเรียก `GC.Collect()` หากสังเกตเห็นการกระโดดของเมมโมรี |
| **การตรวจจับภาษาผิด** | ตั้งค่า `ocrEngine.Configuration.Language = OcrLanguage.English;` (หรือภาษาที่ต้องการ) ก่อนเรียก `RecognizeBatch` |
| **ประสิทธิภาพช้าแม้มีการทำงานขนาน** | ตรวจสอบว่า SSD ของคุณไม่ได้จำกัด I/O; อ่านไฟล์ทั้งหมดเข้าสู่หน่วยความจำก่อน (เช่นที่ทำด้วย `ImageStream.FromFile`) |
| **อักขระหาย** | เพิ่มค่า `ocrEngine.Configuration.DPI = 300;` เพื่อประมวลผลความละเอียดสูงขึ้น |

---

## ขยายตัวอย่าง – จาก PNG ไปยัง PDF หรือ DOCX

หากในอนาคตคุณต้อง **แปลงหน้าที่สแกน** ให้เป็น PDF ที่ค้นหาได้ เพียงส่ง `ocrResults[i].PlainText` ไปยังไลบรารี PDF (เช่น Aspose.PDF) แล้ววางข้อความเป็นเลเยอร์โปร่งใส เทคนิคการทำงานขนานเดียวกันก็ใช้ได้ที่นั่นเช่นกัน

---

## โค้ดเต็ม (พร้อมคัดลอก‑วาง)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

บันทึกไฟล์นี้เป็น `BatchExample.cs`, รัน `dotnet run`, แล้วดูคอนโซลของคุณเต็มไปด้วยข้อความที่เคยซ่อนอยู่ใน PNG สแกนเหล่านั้น

---

## สรุปภาพรวม

![extract text images example](images/ocr-batch.png){alt="extract text images example"}

แผนภาพแสดงกระบวนการ: **ไฟล์ PNG → คอลเลกชัน ImageStream → OcrEngine (max parallelism) → ผลลัพธ์ OCR → คอนโซล / ที่เก็บข้อมูลต่อไป**  

---

## สรุป

ตอนนี้คุณมีสูตรครบวงจรสำหรับการ **ดึงข้อความจากภาพ** ด้วย C# พร้อมกับ **การตั้งค่าการทำงานขนานสูงสุด**, **การแปลงหน้าที่สแกน**, การจัดการ **OCR หลายภาพ**, และ **การอ่านข้อความ PNG** อย่างมีประสิทธิภาพ โค้ดเป็นอิสระ, คำอธิบายครอบคลุมทั้ง “วิธีทำ” และ “ทำไมต้องทำ”, และเคล็ดลับช่วยให้คุณหลีกเลี่ยงอาการเจ็บปวดทั่วไป

ต่อไปคุณจะทำอะไร? ลองเปลี่ยนรายการ PNG ให้เป็นลูป `Directory.GetFiles` แบบไดนามิก, ทดลองกับจำนวนเธรดต่าง ๆ, หรือส่งผลลัพธ์ไปยัง PDF ที่ค้นหาได้ รูปแบบเดียวกันสามารถสเกลได้หลายร้อยหน้าโดยแทบไม่มีโค้ดเพิ่ม

มีคำถามหรือกรณีขอบที่ซับซ้อน? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
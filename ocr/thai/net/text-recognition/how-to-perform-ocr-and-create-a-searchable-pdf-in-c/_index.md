---
category: general
date: 2026-02-14
description: เรียนรู้วิธีทำ OCR บนไฟล์ TIFF หรือรูปภาพและแปลง PDF ด้วย OCR เพื่อสร้าง
  PDF ที่ค้นหาได้—คู่มือ C# ทีละขั้นตอน
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: th
og_description: ค้นพบวิธีทำ OCR บนภาพ, แปลง PDF ด้วย OCR, และสร้าง PDF ที่ค้นหาได้ด้วย
  Aspose OCR ในบทแนะนำ C# ที่สั้นกระชับ.
og_title: วิธีทำ OCR และสร้าง PDF ที่ค้นหาได้ใน C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: วิธีทำ OCR และสร้าง PDF ที่สามารถค้นหาได้ใน C#
url: /th/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR และสร้าง PDF ที่สามารถค้นหาได้ใน C#

เคยต้อง **ทำ OCR** บนเอกสารสแกนแล้วไม่แน่ใจว่าจะเปลี่ยนผลลัพธ์ให้เป็น PDF ที่สามารถค้นหาได้อย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องจัดการกับคลัง TIFF เก่า หรือ PDF ที่มีเฉพาะรูปภาพ ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# และไลบรารี Aspose.OCR คุณสามารถแปลง TIFF หรือรูปภาพใด ๆ ให้เป็น PDF ที่ค้นหาได้เต็มรูปแบบภายในไม่กี่วินาที

ในบทเรียนนี้เราจะพาคุณผ่านทุกขั้นตอนที่ต้องรู้: ตั้งแต่การติดตั้งไลบรารี, การโหลด TIFF หลายหน้า, ไปจนถึงการเรียก `RecognizeToPdf` เพื่อที่คุณจะสามารถ **แปลง PDF ด้วย OCR** และ **สร้างไฟล์ PDF ที่ค้นหาได้** ที่ผู้ใช้ของคุณสามารถค้นหาได้จริง ๆ เมื่อเสร็จสิ้น คุณจะมีแอปคอนโซลที่พร้อมรันซึ่งสร้าง PDF ที่ค้นหาได้จากแหล่งรูปภาพ

## ข้อกำหนดเบื้องต้น

- **.NET 6.0** หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+ ด้วย)
- ใบอนุญาต **Aspose.OCR** ที่ถูกต้องหรือคีย์ประเมินผลชั่วคราว (รุ่นทดลองฟรีเพียงพอสำหรับการทดสอบ)
- Visual Studio 2022 (หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ) พร้อม **NuGet** package manager
- ไฟล์อินพุตชื่อ `input.tif` ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม — TIFF หลายหน้าจะทำงานได้ทันที

> **เคล็ดลับ:** หากคุณใช้ Windows ให้คัดลอกไฟล์ TIFF ไปไว้ในโฟลเดอร์เดียวกับไฟล์ `.exe` ที่คอมไพล์แล้ว เพื่อหลีกเลี่ยงปัญหาเกี่ยวกับเส้นทางไฟล์

## ขั้นตอนที่ 1: ติดตั้งแพ็กเกจ Aspose.OCR จาก NuGet

เปิดโฟลเดอร์โปรเจกต์ของคุณในเทอร์มินัลและรัน:

```bash
dotnet add package Aspose.OCR
```

คำสั่งนี้จะดึงเวอร์ชันล่าสุดที่เสถียร (ณ กุมภาพันธ์ 2026 คือ 23.10) และเพิ่ม dependencies ที่จำเป็นทั้งหมด หลังจากการกู้คืนเสร็จสิ้น คุณจะเห็น `Aspose.OCR` ปรากฏใต้ **Dependencies** ใน Solution Explorer

## ขั้นตอนที่ 2: สร้างแอปคอนโซลขนาดเล็กที่สุด

สร้างโปรเจกต์คอนโซลใหม่หากคุณยังไม่มี:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

แทนที่ไฟล์ `Program.cs` ที่สร้างอัตโนมัติด้วยโค้ดเต็มที่แสดงใน **ขั้นตอน 3** โปรแกรมจะทำสิ่งต่อไปนี้:

1. สร้างอินสแตนซ์ของ OCR engine
2. โหลดรูปภาพต้นฉบับ (หรือ TIFF หลายหน้า)
3. รัน OCR แล้วเขียนผลลัพธ์โดยตรงเป็น PDF ที่ค้นหาได้
4. แจ้งผู้ใช้ว่ากระบวนการสำเร็จ

## ขั้นตอนที่ 3: โค้ดทำงานเต็มรูปแบบ – จากรูปภาพสู่ PDF ที่ค้นหาได้

ด้านล่างเป็นไฟล์ซอร์ส **ทั้งหมด** คัดลอกและวางลงใน `Program.cs` คอมเมนต์ถูกใส่ไว้เพื่ออธิบายส่วนที่ไม่ชัดเจน

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**สิ่งที่คุณจะเห็น:** หลังจากรันโปรแกรม จะมีไฟล์ชื่อ `searchable.pdf` ปรากฏในโฟลเดอร์เป้าหมาย เปิดไฟล์ด้วย Adobe Reader หรือโปรแกรมดู PDF ใด ๆ แล้วลองค้นหาคำที่มีอยู่ใน TIFF ต้นฉบับ ข้อความควรพบได้ทันที แสดงว่าคุณได้ **สร้าง PDF ที่ค้นหาได้** จากรูปภาพสำเร็จแล้ว

### การรันแอป

```bash
dotnet run
```

หากทุกอย่างตั้งค่าอย่างถูกต้อง คุณจะได้รับผลลัพธ์ดังนี้:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

เปิด PDF กด `Ctrl+F` พิมพ์คำจากแหล่งต้นฉบับ แล้วดูการไฮไลท์กระโดดไปยังตำแหน่งที่ถูกต้อง

## ขั้นตอนที่ 4: ตัวแปรทั่วไปและกรณีขอบ

### แปลง PDF ปกติ (ที่มีเฉพาะรูปภาพ) ให้เป็น PDF ที่ค้นหาได้

หากแหล่งของคุณเป็น PDF ที่มีรูปสแกนแทนข้อความ คุณยังสามารถใช้วิธีเดียวกันได้ — เพียงเปลี่ยนแหล่ง `ImageStream`:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

วิธีนี้ตอบโจทย์ **แปลง PDF ด้วย OCR** โดยไม่ต้องเขียนโค้ดเพิ่มเติม

### จัดการกับเอกสารหลายหน้าขนาดใหญ่

สำหรับเอกสารที่มีหลายร้อยหน้า ควรพิจารณา:

- **เพิ่มขีดจำกัดหน่วยความจำ** (`Engine.MemoryLimit = 2_000; // MB`)
- **ประมวลผลเป็นชิ้นส่วน**: โหลดหน้าที่เป็นส่วนย่อย, เขียน PDF ชั่วคราว, แล้วรวมกันด้วยไลบรารี PDF (เช่น Aspose.PDF)

### รองรับภาษาที่ไม่ใช่ภาษาอังกฤษ

Aspose.OCR รองรับหลายภาษาโดยอัตโนมัติ ตั้งค่าภาษาก่อนทำการจดจำ:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

หากคุณต้องการ **tiff to searchable pdf** ในสคริปต์ที่ไม่ใช่ละติน ให้ตรวจสอบว่าติดตั้ง language pack ที่เหมาะสมแล้ว

### ถ้า PDF ที่ได้เป็นไฟล์เปล่า?

- ตรวจสอบว่าไฟล์อินพุตไม่เสียหาย
- ยืนยันว่า OCR engine มีใบอนุญาตที่ถูกต้อง — โหมดประเมินผลอาจจำกัดจำนวนหน้า
- ตรวจสอบว่าความละเอียดของรูปภาพอย่างน้อย 300 dpi; ความละเอียดต่ำอาจทำให้การจดจำไม่แม่นยำ

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์โดยโปรแกรม (ทางเลือก)

บางครั้งคุณอาจต้องยืนยันว่า PDF มีชั้นข้อความจริง ๆ คุณสามารถใช้ Aspose.PDF เพื่อดึงข้อความออกมาได้:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

หากตัวแปร `extracted` ไม่ว่างเปล่า แสดงว่าคุณได้ **สร้าง PDF ที่ค้นหาได้** สำเร็จแล้ว

## สรุป

เราได้อธิบาย **วิธีทำ OCR** บน TIFF (หรือรูปภาพใด ๆ) และแปลง **PDF ด้วย OCR** อย่างราบรื่นเพื่อสร้าง **PDF ที่ค้นหาได้** ที่ทำงานเหมือนเอกสารดั้งเดิม ขั้นตอนสำคัญคือ:

1. ติดตั้ง Aspose.OCR  
2. เริ่มต้น `Engine`  
3. โหลดรูปภาพผ่าน `ImageStream`  
4. เรียก `RecognizeToPdf`

จากนั้นคุณสามารถทดลองปรับตั้งค่าภาษา, ประมวลผลเป็นชุดใหญ่, หรือรวมผลลัพธ์กับงานจัดการ PDF อื่น ๆ รูปแบบเดียวกันนี้ทำงานได้กับ **tiff to searchable pdf**, **searchable pdf from image**, รวมถึง PDF ที่สแกนแล้วด้วย

พร้อมรับความท้าทายต่อไปหรือยัง? ลองฝัง OCR เข้าใน Web API เพื่อให้ผู้ใช้อัปโหลดสแกนและรับ PDF ที่ค้นหาได้ทันที หรือสำรวจ OCR สำหรับโน้ตมือเขียนโดยใช้การตั้งค่าขั้นสูงของ `OcrEngine` ความเป็นไปได้ไม่มีที่สิ้นสุด — Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
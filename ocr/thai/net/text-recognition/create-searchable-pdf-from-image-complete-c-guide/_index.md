---
category: general
date: 2026-02-13
description: สร้าง PDF ที่ค้นหาได้จากภาพโดยใช้ Aspose.OCR เรียนรู้การแปลงภาพเป็น PDF,
  การสกัดข้อความจากภาพ, การฝังฟอนต์ใน PDF และการจดจำข้อความจาก PNG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพด้วย Aspose.OCR คู่มือนี้แสดงวิธีแปลงภาพเป็น
  PDF, ฝังฟอนต์, และดึงข้อความจาก PNG อย่างง่ายดาย.
og_title: สร้าง PDF ที่ค้นหาได้จากภาพ – คู่มือ C# ทีละขั้นตอน
tags:
- C#
- OCR
- Aspose
- PDF generation
title: สร้าง PDF ที่ค้นหาได้จากรูปภาพ – คู่มือ C# ฉบับเต็ม
url: /th/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้จากรูปภาพ – คู่มือ C# ฉบับสมบูรณ์

เคยต้อง **สร้าง PDF ที่สามารถค้นหาได้** จากไฟล์ PNG ที่สแกนแล้วแต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการ—เช่น การแปลงใบแจ้งหนี้เป็นดิจิทัลหรือการเก็บรักษาคู่มือเก่า—การเปลี่ยนรูปภาพให้เป็น PDF ที่คุณสามารถค้นหาได้จริงเป็นการเปลี่ยนเกมอย่างมาก  

ในบทเรียนนี้เราจะเดินผ่านขั้นตอนที่แน่นอนเพื่อ **แปลงรูปภาพเป็น PDF**, **ดึงข้อความจากรูปภาพ**, ฝังฟอนต์ที่จำเป็น, และสุดท้ายได้ไฟล์ PDF ที่สามารถค้นหาได้อย่างเต็มรูปแบบ ไม่มีการอ้างอิงที่คลุมเครือ เพียงตัวอย่างที่ทำงานได้เต็มที่ที่คุณสามารถคัดลอก‑วางลงใน Visual Studio วันนี้

> **สิ่งที่คุณจะได้:** แอปคอนโซล C# ที่อ่าน `input.png`, ทำ OCR, ฝังฟอนต์, เก็บภาพราสเตอร์ต้นฉบับเป็นพื้นหลัง, และเขียนไฟล์ `output.pdf`. เมื่อจบคุณจะเข้าใจ *ทำไม* แต่ละบรรทัดถึงสำคัญและจะปรับแต่งอย่างไรสำหรับสถานการณ์ของคุณเอง

---

## ความต้องการเบื้องต้น

- .NET 6.0 SDK หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+ ด้วย)  
- Aspose.OCR for .NET – สามารถดาวน์โหลดจาก NuGet (`Install-Package Aspose.OCR`)  
- ตัวอย่างไฟล์ PNG (`input.png`) ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม  
- ความคุ้นเคยพื้นฐานกับโปรเจกต์คอนโซล C# (หากคุณยังไม่เคยสร้างโปรเจกต์, เพียงเปิด Visual Studio → **Create a new project** → **Console App** → **C#**)

> **เคล็ดลับ:** Aspose มีไลเซนส์ทดลองฟรี; เพียงวางไฟล์ `.lic` ข้างไฟล์ executable แล้วไลบรารีจะทำงานโดยไม่มีลายน้ำ

---

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine – จดจำข้อความจาก PNG

สิ่งแรกที่เราต้องการคือ OCR engine ที่สามารถอ่านอักขระในไฟล์ PNG ได้จริง Aspose.OCR ทำให้เรื่องนี้ง่ายดาย

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**ทำไมจึงสำคัญ:**  
การตั้งค่า `Language` บอกให้ engine รู้ว่าต้องคาดหวังชุดอักขระแบบใด หากข้ามขั้นตอนนี้ engine จะใช้โหมดทั่วไปที่อาจตีความอักขระที่มีสำเนียงหรือหมายเลขผิดพลาด สำหรับเอกสารหลายภาษา คุณสามารถส่งรายการคั่นด้วยคอมม่าเช่น `OcrLanguage.English | OcrLanguage.French`

---

## ขั้นตอนที่ 2: โหลดและจดจำภาพ – ดึงข้อความจากรูปภาพ

เมื่อ engine พร้อมแล้ว เราจะส่ง PNG ที่ต้องการประมวลผลให้มัน

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**กำลังเกิดอะไรขึ้นเบื้องหลัง?**  
`RecognizeImage` จะสแกนบิตแมพ, ระบุบล็อกข้อความ, และเก็บผลลัพธ์ไว้ใน `ocrEngine`. คุณสามารถเข้าถึง `ocrEngine.Text` หากต้องการสตริงดิบ, แต่สำหรับ PDF ที่สามารถค้นหาได้ เราจะให้ Aspose จัดการการแปลงโดยตรง

> **กรณีขอบ:** หาก PNG ของคุณมีขนาดใหญ่ (เกิน 10 MB) คุณอาจหมดหน่วยความจำ ในกรณีนั้นลองปรับขนาดภาพก่อนหรือใช้ `OcrEngine.RecognizeImage(Stream)` เพื่อสตรีมข้อมูล

---

## ขั้นตอนที่ 3: กำหนดค่า PDF Export Options – ฝังฟอนต์ใน PDF

PDF ที่สามารถค้นหาได้จะไม่มีประโยชน์หากฟอนต์ไม่ได้ถูกฝัง; เอกสารจะดูเสียหายบนเครื่องที่ไม่มีฟอนต์ที่ต้องการ Aspose ให้เราสลับการตั้งค่านี้ด้วยอ็อบเจกต์ options ง่าย ๆ

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**ทำไมต้องฝังฟอนต์?**  
เมื่อ `EmbedFonts` เป็น `true`, PDF จะบรรจุข้อมูลฟอนต์ไว้ภายในไฟล์ ทำให้ผู้ชมใด ๆ—Chrome, Adobe Reader หรือแอปมือถือ—แสดงข้อความได้ตรงตามที่ตั้งใจ แม้ระบบเป้าหมายจะไม่มีฟอนต์นั้น

**เมื่อใดที่คุณจะตั้งค่า `KeepOriginalImage` เป็น `false`?**  
หากคุณต้องการเพียงข้อความที่ดึงออกมาและต้องการไฟล์ขนาดเล็กลง, การปิดตัวเลือกนี้จะลบภาพพื้นหลัง, ทำให้ได้ PDF “สะอาด” ที่มีเฉพาะข้อความ

---

## ขั้นตอนที่ 4: ส่งออกเป็น PDF ที่สามารถค้นหาได้ – แปลงภาพเป็น PDF

เมื่อได้ผลลัพธ์ OCR และตั้งค่า PDF แล้ว ขั้นตอนสุดท้ายคือบรรทัดเดียวที่เขียน PDF ที่สามารถค้นหาได้ลงดิสก์

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**สิ่งที่คุณจะเห็น:**  
เปิด `output.pdf` ในโปรแกรมอ่านใด ๆ, คุณสามารถเลือกข้อความ, คัดลอก‑วาง, และแม้แต่ใช้การค้นหา (`Ctrl + F`) เพื่อหาคำที่เดิมอยู่เป็นพิกเซลใน PNG

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถคอมไพล์และรันได้ทันที แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่มี `input.png`

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**ผลลัพธ์ที่คาดว่าจะเห็นบนคอนโซล:**

```
Searchable PDF created.
```

เปิด `output.pdf` แล้วลองค้นหาคำที่คุณรู้ว่ามีอยู่ใน `input.png`. หากคำนั้นถูกไฮไลท์, คุณได้ **สร้าง PDF ที่สามารถค้นหาได้จากรูปภาพ** สำเร็จแล้ว

---

## คำถามที่พบบ่อย & เคล็ดลับระดับมืออาชีพ

### “ฉันสามารถประมวลผลหลายภาพในครั้งเดียวได้หรือไม่?”

ได้เลย. ห่อหุ้มตรรกะการจดจำและส่งออกไว้ในลูป, เช่นใช้ `Directory.GetFiles(..., "*.png")`. อย่าลืมตั้งชื่อ PDF ให้เป็นเอกลักษณ์สำหรับแต่ละไฟล์, เช่น `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### “เอกสารของฉันมีทั้งภาษาอังกฤษและสเปนเป็นอยู่?”

ตั้งค่าคุณสมบัติภาษาเป็นแฟล็กรวม:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Aspose จะพยายามตรวจจับอักขระจากทั้งสองอักษร

### “ไฟล์ PDF มีขนาดใหญ่—ฉันจะทำให้มันเล็กลงได้อย่างไร?”

สองเทคนิคเร็ว:

1. ตั้งค่า `pdfOptions.KeepOriginalImage = false` เพื่อลบภาพราสเตอร์พื้นหลัง  
2. ใช้ `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (ต้องเพิ่มคุณสมบัตินี้) เพื่อบีบอัดภาพที่ฝังอยู่

### “ฉันต้องการไลเซนส์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?”

ไลเซนส์ทดลองทำงานได้ดีสำหรับการทดสอบ, แต่สำหรับการใช้งานเชิงพาณิชย์คุณต้องซื้อไลเซนส์และลงทะเบียนในแอปของคุณตั้งแต่ต้น:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## การขยายโซลูชัน

เมื่อคุณรู้วิธี **สร้าง PDF ที่สามารถค้นหาได้**, คุณอาจต้องการ:

- **เพิ่มลายน้ำ** – ใช้ `PdfDocument` จาก Aspose.PDF เพื่อวางข้อความทับหลัง OCR  
- **ประมวลผลไฟล์ PDF เป็นชุด** – รวมหลาย PDF ที่สามารถค้นหาได้เป็นไฟล์เดียวด้วย `PdfFileEditor`  
- **ผสานกับ Azure Blob Storage** – อ่าน/เขียนสตรีมของภาพและ PDF โดยตรงจากคลาวด์, ลดการใช้ I/O ของไฟล์ท้องถิ่น

แต่ละส่วนขยายทำตามรูปแบบเดียวกัน: รับผลลัพธ์ OCR, ตั้งค่าห้องสมุดต่อไป, แล้วเชื่อมต่อการทำงานต่อกัน

---

## สรุป

คุณเพิ่งเรียนรู้วิธี **สร้าง PDF ที่สามารถค้นหาได้** จากไฟล์ PNG ด้วย Aspose.OCR ใน C#. โดยการเริ่มต้น OCR engine, จดจำข้อความ, ตั้งค่า `SearchablePdfOptions` เพื่อ **ฝังฟอนต์ใน PDF**, และส่งออก, คุณจะได้ไฟล์ที่เหมือนต้นฉบับแต่สามารถค้นหาได้เต็มที่  

จากนี้ต่อไปคุณสามารถทดลองแปลงเป็นชุด, ใช้ภาษาต่าง ๆ, หรือบีบอัดให้แคบลง—ตามที่เวิร์กโฟลว์ของคุณต้องการ หากเจอปัญหา, ฟอรั่มของ Aspose และเอกสาร API เป็นแหล่งข้อมูลที่ดี, แต่ขั้นตอนหลักข้างต้นจะครอบคลุมประมาณ 90 % ของกรณีการใช้งานทั่วไป

ขอให้เขียนโค้ดสนุกและ PDF ของคุณเป็น searchable เสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
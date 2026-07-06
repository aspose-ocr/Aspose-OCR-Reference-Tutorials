---
category: general
date: 2026-03-05
description: แปลงไฟล์ TIFF เป็นข้อความใน C# ด้วย Aspose OCR—ดึงข้อความจากไฟล์ภาพสแกนได้อย่างรวดเร็วและเรียนรู้วิธีโหลดไฟล์ภาพใน
  C# เพื่อการประมวลผล OCR
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: th
og_description: แปลงไฟล์ TIFF เป็นข้อความใน C# ด้วย Aspose OCR. เรียนรู้ขั้นตอนการทำงานทั้งหมดสำหรับการสกัดข้อความจากภาพสแกนและการโหลดไฟล์ภาพอย่างมีประสิทธิภาพ.
og_title: แปลง TIFF เป็นข้อความใน C# – ดึงข้อความจากภาพสแกน
tags:
- OCR
- C#
- Aspose
title: แปลง TIFF เป็นข้อความใน C# – ดึงข้อความจากภาพสแกน
url: /th/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง TIFF เป็นข้อความใน C# – ดึงข้อความจากภาพสแกน

ต้องการ **แปลง TIFF เป็นข้อความใน C#** หรือไม่? คุณไม่ได้เป็นคนเดียวที่ต้องต่อสู้กับภาพสแกนหลายหน้า ที่ไม่ยอมแปลงเป็นสตริงที่ค้นหาได้  
ในคู่มือนี้เราจะพาคุณผ่านโซลูชันที่สมบูรณ์พร้อมใช้งานที่รับไฟล์ TIFF, ส่งให้ Aspose OCR, แล้วแปลงเป็นข้อความธรรมดา—ไม่มีบริการเสริม ไม่มีเวทมนตร์ลับ

> **เคล็ดลับ:** หากคุณทำงานกับสแกนความละเอียดสูง การเปิดการประมวลผลด้วย GPU สามารถลดเวลาได้หลายวินาทีต่อหน้า

เราจะยังแสดงวิธี **ดึงข้อความจากไฟล์ภาพสแกน** และวิธีที่ดีที่สุดในการ **โหลดไฟล์ภาพ C#** เข้าไปในเครื่องมือ OCR เพื่อให้คุณสามารถฝังตรรกะนี้ลงในโปรเจกต์ .NET ใดก็ได้ทันที

---

## สิ่งที่คุณต้องการ

ก่อนที่เราจะดำเนินการต่อ ให้ตรวจสอบว่าคุณมีสิ่งต่อไปนี้บนเครื่องของคุณแล้ว:

| ความต้องการ | เหตุผล |
|-------------|--------|
| .NET 6.0+ (หรือ .NET Framework 4.7.2+) | Runtime สมัยใหม่ รองรับ `Span<T>` และ I/O แบบ async |
| Aspose.OCR for .NET (แพ็คเกจ NuGet `Aspose.OCR`) | Engine OCR ที่เราจะใช้ |
| ไฟล์ใบอนุญาต Aspose OCR ที่ถูกต้อง (`Aspose.OCR.lic`) | หากไม่มีคุณจะเจอข้อจำกัดของรุ่นทดลอง |
| ไฟล์ TIFF (หน้าเดียวหรือหลายหน้า) สำหรับทดสอบ | ตัวอย่างที่ใช้: `scanned_multi_page.tif` |
| GPU ที่รองรับ CUDA 11+ (ไม่บังคับ) | เร่งความเร็วการจดจำเมื่อ `EngineMode = Gpu` |

หากคุณขาดสิ่งใดสิ่งหนึ่ง ให้ดาวน์โหลดแพ็คเกจ NuGet ทันที:

```bash
dotnet add package Aspose.OCR
```

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้า Namespaces

สร้างแอปคอนโซลใหม่ (หรือเพิ่มโค้ดนี้ลงในโปรเจกต์ที่มีอยู่) สิ่งแรกที่เราทำคือการนำเข้าคลาสที่จำเป็น

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **ทำไมจึงสำคัญ:** การนำเข้า `Aspose.OCR.Image` จะให้เราเข้าถึงฟactory `ImageStream` ซึ่งสามารถอ่านไฟล์ TIFF โดยตรงจากดิสก์หรือสตรีมได้ การข้ามขั้นตอนนี้จะทำให้เกิดข้อผิดพลาดระหว่างการคอมไพล์

---

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine และเลือกโหมดการประมวลผล

ต้องกำหนดค่า OCR Engine **ก่อน** ที่จะกำหนดภาพใด ๆ นี่คือจุดที่เราตัดสินใจว่าจะรันบน CPU หรือใช้ GPU

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*หากคุณทำงานบนเซิร์ฟเวอร์แบบ headless ที่ไม่มีการ์ดกราฟิก ให้เปลี่ยน `Gpu` เป็น `Cpu` หรือ `Auto`*  
โหมดของ engine มีผลต่อการจัดสรรหน่วยความจำและความเร็ว; โหมด GPU สามารถเร็วขึ้น 2‑3× บน TIFF ขนาดใหญ่และความละเอียดสูง

---

## ขั้นตอนที่ 3: ใส่ใบอนุญาต Aspose OCR ของคุณ

การทำงานโดยไม่มีใบอนุญาตจะจำกัดจำนวนหน้าและเพิ่มลายน้ำ โหลดใบอนุญาตตั้งแต่เนิ่น ๆ เพื่อให้การดำเนินการต่อ ๆ ไปไม่มีข้อจำกัด

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **ข้อผิดพลาดทั่วไป:** การเรียก `SetLicense` หลังจาก `Recognize()` จะทำให้ engine กลับไปใช้โหมดทดลองสำหรับการเรียกนั้น

---

## ขั้นตอนที่ 4: โหลดไฟล์ TIFF – รองรับภาพหน้าเดียวและหลายหน้า

Aspose OCR สามารถอ่าน TIFF หลายหน้าได้โดยตรง แต่คุณต้องส่งสตรีมที่ถูกต้อง นี่คือตัวอย่างที่ทำงานได้ทั้งสองกรณี

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### ทำไมต้องใช้ `ImageStream.FromFile`?

- มันทำหน้าที่เป็นชั้นนามธรรมเหนือ `FileStream` ด้านใน จัดการการนับหน้าของ TIFF ให้โดยอัตโนมัติ  
- ยังทำงานกับ `MemoryStream` ได้เช่นกัน ทำให้คุณสามารถโหลดภาพจากฐานข้อมูลหรือ Web API ได้โดยไม่ต้องสัมผัสไฟล์ระบบ

### กรณีขอบ: TIFF ขนาดใหญ่มาก

หาก TIFF ของคุณเกิน 200 MB ให้พิจารณาโหลดทีละหน้าเพื่อหลีกเลี่ยงข้อยกเว้น out‑of‑memory:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์

เมื่อคุณรันโปรแกรม ควรเห็นผลลัพธ์คล้ายดังนี้:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

หากข้อความดูเป็นอักขระแปลก ๆ ให้ตรวจสอบสองครั้ง:

1. **Resolution** – OCR ทำงานได้ดีที่สุดที่ 300 dpi หรือสูงกว่า  
2. **EngineMode** – เปลี่ยนเป็น `Cpu` หากไดรเวอร์ GPU เก่าเกินไป  
3. **License** – ตรวจสอบว่าเส้นทางไฟล์ใบอนุญาตถูกต้องและไฟล์สามารถอ่านได้

---

## คำถามที่พบบ่อย (FAQ)

### วิธีนี้ทำงานกับรูปแบบภาพอื่นได้หรือไม่?

แน่นอน `ImageStream.FromFile` รองรับ JPEG, PNG, BMP และแม้กระทั่ง PDF (ผ่าน Aspose.PDF) เพียงเปลี่ยนนามสกุลไฟล์

### ถ้าฉันต้องประมวลผลภาพที่เก็บอยู่ในฐานข้อมูลล่ะ?

อ่าน BLOB เข้า `MemoryStream` แล้วส่งให้ `ImageStream.FromStream(memoryStream)` OCR Engine จะจัดการเหมือนกับสตรีมจากไฟล์

### ฉันสามารถรันบน Linux ได้หรือไม่?

ได้ — Aspose OCR รองรับหลายแพลตฟอร์ม ติดตั้ง .NET runtime ที่เหมาะสมและตรวจสอบให้แน่ใจว่ามีไลบรารีเนทีฟที่จำเป็นสำหรับ GPU (หากใช้) พร้อมใช้งาน

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมดพร้อมคอมไพล์ แทนที่ `YOUR_DIRECTORY` และเส้นทางไฟล์ใบอนุญาตด้วยตำแหน่งจริงของคุณ

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

บันทึกไฟล์นี้เป็น `Program.cs` รัน `dotnet run` แล้วดูข้อความที่แสดงออกมา

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
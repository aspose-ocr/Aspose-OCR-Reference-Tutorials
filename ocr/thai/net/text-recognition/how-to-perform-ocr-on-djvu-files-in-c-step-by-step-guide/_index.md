---
category: general
date: 2026-02-20
description: วิธีทำ OCR บนไฟล์ DjVu ด้วย C# เรียนรู้การจดจำข้อความจากภาพและแปลง DjVu
  เป็นข้อความอย่างรวดเร็วด้วย Aspose OCR.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: th
og_description: วิธีทำ OCR บนไฟล์ DjVu ด้วย C# บทเรียนนี้จะแสดงวิธีการจดจำข้อความจากภาพ
  อ่านไฟล์ DjVu และแปลง DjVu เป็นข้อความโดยใช้ Aspose OCR.
og_title: วิธีทำ OCR บนไฟล์ DjVu ด้วย C# – คู่มือครบถ้วน
tags:
- OCR
- C#
- DjVu
- Aspose
title: วิธีทำ OCR บนไฟล์ DjVu ด้วย C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บนไฟล์ DjVu ใน C# – คู่มือฉบับสมบูรณ์

เคยสงสัย **how to perform OCR** บนเอกสาร DjVu โดยไม่ต้องบิดหัวของคุณไหม? คุณไม่ได้เป็นคนเดียว นักพัฒนาจำนวนมากเจออุปสรรคเมื่อพวกเขาต้อง **recognize text from image** ที่อยู่ภายในคอนเทนเนอร์ DjVu ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# และไลบรารี Aspose OCR คุณสามารถดึงข้อความที่ซ่อนอยู่ได้อย่างรวดเร็ว.

ในบทแนะนำนี้ เราจะพาคุณผ่านทุกขั้นตอนที่จำเป็นเพื่อแปลงหน้า DjVu ให้เป็นข้อความธรรมดา เมื่อจบคุณจะรู้ **how to read DjVu**, วิธี **extract text from image** objects, และแม้กระทั่ง **convert DjVu to text** สำหรับการประมวลผลต่อไป ไม่ต้องใช้บริการภายนอก ไม่ต้องอ้างอิงที่คลุมเครือ—เพียงตัวอย่างที่ทำงานได้เอง

## ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK หรือเวอร์ชันใหม่กว่า (โค้ดนี้ทำงานกับ .NET Framework 4.8 ด้วย)
- Visual Studio 2022 หรือโปรแกรมแก้ไขใด ๆ ที่รองรับ C#
- ใบอนุญาต Aspose OCR สำหรับ .NET (รุ่นทดลองฟรีใช้สำหรับทดสอบ)
- ไฟล์ DjVu ตัวอย่าง (`sample.djvu`) ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้

การเตรียมสิ่งเหล่านี้ไว้ล่วงหน้าจะทำให้กระบวนการราบรื่น—ไม่มีความประหลาดใจเรื่อง “missing reference” ในภายหลัง

## วิธีทำ OCR บนหน้า DjVu

แนวคิดหลักง่าย ๆ: โหลดหน้า DjVu เป็นรูปภาพ ส่งให้เครื่อง OCR ทำงาน แล้วอ่านสตริงผลลัพธ์ เรามาแยกขั้นตอนกันทีละขั้นตอน

### ขั้นตอน 1: ติดตั้ง Aspose OCR

เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรัน:

```bash
dotnet add package Aspose.OCR
```

คำสั่งนี้จะดึงไบนารีล่าสุดของ Aspose OCR พร้อมกับ dependencies หากคุณชอบใช้ UI ของ NuGet Package Manager เพียงค้นหา **Aspose.OCR** แล้วคลิก **Install**

### ขั้นตอน 2: เริ่มต้น OCR Engine

การสร้างอินสแตนซ์ของ `OcrEngine` เป็นสิ่งแรกที่คุณทำเมื่อคุณต้องการ **perform OCR** คิดว่าเป็นการเปิดสมองของสแกนเนอร์

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **เคล็ดลับ:** การใช้ `OcrEngine` ตัวเดียวกันหลายหน้า ช่วยประหยัดหน่วยความจำและเร่งการประมวลผล

### ขั้นตอน 3: โหลดหน้า DjVu เป็นรูปภาพ

ไฟล์ DjVu ไม่ได้รับการสนับสนุนโดย API รูปภาพส่วนใหญ่โดยตรง แต่ Aspose สามารถจัดการแต่ละหน้าเป็นบิตแมพ ที่นี่เราใช้ `System.Drawing.Image` เพื่ออ่านไฟล์

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **ทำไมวิธีนี้ถึงได้ผล:** `Image.FromFile` จะถอดรหัสสตรีม DjVu เป็นรูปแบบแรสเตอร์ที่ OCR engine เข้าใจโดยอัตโนมัติ หากคุณต้องการประมวลผลหน้าที่เฉพาะจาก DjVu หลายหน้า ให้ใช้ Aspose PDF หรือ Aspose Imaging เพื่อดึงหน้าก่อน

### ขั้นตอน 4: Recognize Text from Image

ตอนนี้จุดมหัศจรรย์เกิดขึ้น เมธอด `Recognize` จะสแกนบิตแมพและคืนสตริงที่มีอักขระที่ตรวจพบ

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

ณ จุดนี้คุณได้ **recognized text from image** จากข้อมูลที่เดิมอยู่ในคอนเทนเนอร์ DjVu สตริงอาจมีการขึ้นบรรทัดใหม่ เครื่องหมายวรรคตอน และแม้แต่ตัวอักษร Unicode หากภาษาต้นทางรองรับ

### ขั้นตอน 5: แสดงหรือบันทึกผลลัพธ์

เพื่อการตรวจสอบอย่างรวดเร็ว เพียงพิมพ์ข้อความลงคอนโซล ในแอปจริงคุณอาจบันทึกลงไฟล์หรือฐานข้อมูล

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมที่สมบูรณ์และพร้อมรัน

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนเพื่อความกระชับ):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

หากคุณเห็นอักขระผิดรูป ตรวจสอบให้แน่ใจว่าไฟล์ DjVu ไม่ได้ถูกเข้ารหัสและคุณได้ตั้งค่าภาษาที่ถูกต้องใน `ocrEngine.Language` โดยค่าเริ่มต้นจะถือว่าเป็นภาษาอังกฤษ; คุณสามารถเปลี่ยนเป็นภาษาฝรั่งเศส, เยอรมัน ฯลฯ โดยกำหนด `ocrEngine.Language = Language.French;`

## Recognize Text from Image – ข้อผิดพลาดทั่วไป

แม้จะมีตัวอย่างที่ชัดเจน นักพัฒนาก็มักเจอกรณีขอบบางบางอย่าง:

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **Blank output** | ความละเอียดของภาพต่ำเกินไป (<300 dpi). | ใช้ `ocrEngine.ImageResolution = 300;` ก่อนเรียก `Recognize`. |
| **Wrong language** | OCR defaults to English. | ตั้งค่า `ocrEngine.Language = Language.Spanish;` (หรือภาษาอื่นที่รองรับ). |
| **Memory leak** | Large DjVu pages stay in memory after processing. | เรียก `djvuPage.Dispose();` เมื่อเสร็จ. |
| **Multi‑page DjVu** | Only the first page gets loaded. | วนลูปผ่านหน้าโดยใช้คลาส `DjvuImage` ของ Aspose Imaging. |

การแก้ไขปัญหาเหล่านี้ตั้งแต่ต้นจะช่วยคุณประหยัดเวลาการดีบักเป็นจำนวนมาก

## วิธีอ่านไฟล์ DjVu ใน C# – เกินกว่าการทำ OCR อย่างง่าย

หากโครงการของคุณต้องการมากกว่าหนึ่งหน้า คุณต้องดึงแต่ละหน้าเป็นรูปภาพก่อน Aspose Imaging ทำให้ขั้นตอนนี้ง่ายดาย:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

รูปแบบนี้ทำให้คุณสามารถ **convert DjVu to text** หน้าโดยหน้า เหมาะสำหรับการประมวลผลเป็นชุดของคลังข้อมูลขนาดใหญ่

## Extract Text from Image – ปรับแต่งความแม่นยำ

การตั้งค่า OCR เริ่มต้นทำงานได้ดีสำหรับสแกนที่สะอาด แต่คุณสามารถเพิ่มความแม่นยำได้:

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

การปรับแต่งเหล่านี้มีประโยชน์เป็นพิเศษเมื่อแหล่ง DjVu มีโน้ตมือหรือกราฟิกที่คอนทราสต์ต่ำ

## Convert DjVu to Text – ตัวอย่างเต็มขั้นตอน End‑to‑End

ด้านล่างเป็นเวอร์ชันย่อที่รวมทุกอย่างเข้าด้วยกัน: โหลด DjVu หลายหน้า, เตรียมแต่ละหน้า, ทำ OCR, และบันทึกผลลัพธ์เป็นไฟล์ `.txt`

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

การรันสคริปต์นี้จะสร้าง `sample_extracted.txt` ที่มีเนื้อหาของแต่ละหน้าถูกแยกอย่างเป็นระเบียบ นี่คือวิธีที่เร็วที่สุดในการ **convert DjVu to text** เพื่อการทำดัชนี, การค้นหา หรือการเก็บถาวร

## สรุป

เราได้อธิบาย **how to perform OCR** บนไฟล์ DjVu ตั้งแต่ต้นจนจบ และสำรวจวิธี **recognize text from**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-05
description: แปลง TIFF เป็นข้อความใน C# อย่างรวดเร็วด้วย Aspose OCR. เรียนรู้วิธีแสดงข้อความ
  OCR จากไฟล์ TIFF หลายหน้าในไม่กี่นาที.
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: th
og_description: แปลง TIFF เป็นข้อความใน C# ด้วย Aspose OCR คู่มือนี้จะแสดงวิธีการแสดงข้อความ
  OCR จากภาพ TIFF หลายหน้าแบบทีละขั้นตอน.
og_title: แปลง TIFF เป็นข้อความใน C# – คู่มือ Aspose OCR ฉบับสมบูรณ์
tags:
- Aspose
- OCR
- C#
- TIFF
title: แปลง TIFF เป็นข้อความใน C# ด้วย Aspose OCR
url: /th/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง TIFF เป็นข้อความใน C# ด้วย Aspose OCR

Need to **convert TIFF to text** in C#? You're not alone—many developers wrestle with extracting readable strings from multi‑page TIFF files. The good news is that Aspose OCR C# makes the job almost painless, and you can **display OCR text** on the console or feed it into another system in seconds.

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างที่พร้อมใช้งานเต็มรูปแบบ ซึ่งจะแสดงอย่างละเอียดว่าอย่างไรในการโหลดไฟล์ TIFF หลายหน้า, รัน OCR, และพิมพ์ข้อความของแต่ละหน้า ไม่มีขั้นตอนที่ซ่อนอยู่, ไม่มีการอ้างอิง “ดูเอกสาร” สั้น ๆ เพียงแค่ทำตามคุณจะได้โปรแกรมที่ทำงานอิสระซึ่งสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้

## สิ่งที่คุณต้องมี

- .NET 6.0 หรือใหม่กว่า (ตัวอย่างนี้ตั้งเป้าหมายที่ .NET 6, แต่ .NET 5 ก็ทำงานได้เช่นกัน)  
- ไฟล์ลิขสิทธิ์ Aspose OCR ที่ถูกต้อง (`Aspose.OCR.lic`). ไลบรารีสามารถทำงานได้โดยไม่มีลิขสิทธิ์ แต่คุณจะเจอลายน้ำทดลอง 20 วินาที  
- ไฟล์ TIFF หลายหน้าที่คุณต้องการประมวลผล (เราจะเรียกมันว่า `multipage.tif`)  
- Visual Studio 2022 หรือเครื่องมือแก้ไขใด ๆ ที่คุณชอบ—ไม่มีอะไรพิเศษ

ถ้าคุณมีทั้งหมดนี้แล้ว, มาเริ่มกันเลย

## ขั้นตอนที่ 1: ติดตั้งแพคเกจ NuGet ของ Aspose OCR

ก่อนที่โค้ดใด ๆ จะทำงาน, คุณต้องมีไลบรารีนี้ก่อน เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรันคำสั่ง:

```bash
dotnet add package Aspose.OCR
```

บรรทัดเดียวนี้จะดึงเวอร์ชันล่าสุดที่เสถียร (ณ มีนาคม 2026 เวอร์ชันคือ 23.9)  

> **เคล็ดลับ:** ควรอัปเดตแพคเกจให้เป็นรุ่นล่าสุดเสมอ; รุ่นใหม่มักมีการปรับปรุงประสิทธิภาพสำหรับ TIFF ขนาดใหญ่

## ขั้นตอนที่ 2: ตั้งค่าลิขสิทธิ์ Aspose OCR C# (ไม่บังคับแต่แนะนำ)

การรัน OCR โดยไม่มีลิขสิทธิ์เป็นไปได้, แต่ผลลัพธ์จะมีข้อความเตือนการทดลองอยู่ข้างหน้า หากต้องการหลีกเลี่ยง ให้ชี้เครื่องมือไปที่ไฟล์ `.lic` ของคุณ:

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

ถ้าคุณข้ามขั้นตอนนี้, โค้ดยังทำงานได้—แค่ต้องจำว่าข้อความเพิ่มเติมจะปรากฏในผลลัพธ์

## ขั้นตอนที่ 3: โหลดและทำการจดจำ TIFF หลายหน้า

ตอนนี้เราจะ **แปลง TIFF เป็นข้อความ** จริง ๆ ตัวช่วย `ImageStream.FromFile` จะอ่านไฟล์และแปลงเป็นรูปแบบที่เครื่องยนต์เข้าใจ หลังจากนั้นเราจะเรียก `Recognize()` ซึ่งจะคืนค่าอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความของแต่ละหน้า

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **ทำไมเรื่องนี้สำคัญ:** `Recognize()` ทำงานหนักทั้งหมด—การวิเคราะห์พิกเซล, การตรวจจับภาษา, และการสร้างบรรทัดข้อความ—ทั้งหมดในโค้ด C# ดั้งเดิม ผลลัพธ์ที่ได้ให้คุณเข้าถึงข้อความหน้า‑ต่อ‑หน้า, ซึ่งเหมาะอย่างยิ่งสำหรับการ **แสดงข้อความ OCR** ต่อไป

## ขั้นตอนที่ 4: วนลูปผ่านหน้าและ **แสดงข้อความ OCR**

เมื่อได้ผลลัพธ์แล้ว เราเพียงแค่วนลูปผ่านหน้าและพิมพ์แต่ละหน้า นี่คือส่วนที่คุณจะเห็นการแปลงจากภาพเป็นข้อความธรรมดา

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

การรันโปรแกรมจะให้ผลลัพธ์คล้ายกับตัวอย่างต่อไปนี้ (ข้อความจริงของคุณจะต่างกันตามเนื้อหาใน TIFF):

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

เท่านี้—คุณได้ **แปลง TIFF เป็นข้อความ** และ **แสดงข้อความ OCR** สำหรับทุกหน้าเรียบร้อยแล้ว

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ (`dotnet new console`). รวมถึงการใช้ไดเรกทิฟทั้งหมด, การจัดการลิขสิทธิ์, และการตรวจสอบข้อผิดพลาด

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนเพื่อความกระชับ) แสดงไว้ก่อนหน้านี้ หากคุณเห็นลายน้ำทดลอง, ตรวจสอบให้แน่ใจว่าเส้นทางลิขสิทธิ์ถูกต้อง

## ปัญหาที่พบบ่อยเมื่อแปลง TIFF เป็นข้อความ

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **Out‑of‑memory on huge TIFFs** | The engine loads the whole image into RAM. | Use `ImageStream.FromFile(..., loadOnlyFirstPage: false)` and process pages in batches, or increase the process’s memory limit. |
| **Garbage characters** | Low‑resolution source images confuse the OCR engine. | Pre‑process the TIFF (e.g., increase DPI to 300) before feeding it to Aspose OCR. |
| **License not applied** | `SetLicense` throws an exception you ignore. | Wrap the call in a try/catch (as shown) and log the error. |
| **Missing language data** | By default OCR assumes English. | Set `ocrEngine.Language = OcrLanguage.French;` (or any supported language) before `Recognize()`. |

การจัดการกับกรณีเหล่านี้จะทำให้การแปลงของคุณทำงานได้อย่างราบรื่นในสภาพแวดล้อมการผลิต

## ขั้นตอนต่อไป: ไปไกลกว่าการแสดงผลแบบง่าย

ตอนนี้คุณสามารถ **แปลง TIFF เป็นข้อความ** และ **แสดงข้อความ OCR** แล้ว, คุณอาจต้องการ:

- **บันทึกข้อความที่ดึงมา** ลงไฟล์ `.txt` หรือฐานข้อมูลเพื่อการวิเคราะห์ต่อไป  
- **รวมหลาย TIFF** เป็น PDF ที่ค้นหาได้ด้วย Aspose.PDF  
- **ทำการประมวลผลต่อ** (ตรวจสอบการสะกด, ทำความสะอาดด้วย regex) เพื่อเพิ่มความแม่นยำ  

ส่วนขยายเหล่านี้ทั้งหมดอิงจากรูปแบบหลักที่เราเพิ่งครอบคลุม

---

### TL;DR

เราได้อธิบายวิธีแก้ปัญหา C# อย่างครบถ้วนที่ **แปลง TIFF เป็นข้อความ** ด้วย Aspose OCR C#. โค้ดสร้าง `OcrEngine`, โหลดลิขสิทธิ์ (ถ้ามี), อ่าน TIFF หลายหน้า, รัน OCR, และ **แสดงข้อความ OCR** หน้า‑ต่อ‑หน้า ด้วยตัวอย่างเต็มที่ให้ไว้ คุณสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้และเริ่มดึงข้อความได้ทันที

มีคำถามเกี่ยวกับประสิทธิภาพ, การสนับสนุนภาษา, หรือการรวมกับผลิตภัณฑ์ Aspose อื่น ๆ? แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
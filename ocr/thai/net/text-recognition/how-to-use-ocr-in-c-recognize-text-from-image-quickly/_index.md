---
category: general
date: 2026-02-16
description: วิธีใช้ OCR ใน C# เพื่อจดจำข้อความจากรูปภาพ ดึงข้อความจากไฟล์ JPEG และแปลงรูปภาพเป็นข้อความด้วย
  Aspose OCR คู่มือขั้นตอนโดยละเอียด.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from jpeg
- convert image to text
- how to extract text
language: th
og_description: เรียนรู้วิธีใช้ OCR ใน C# เพื่อจดจำข้อความจากภาพ ดึงข้อความจาก JPEG
  และแปลงภาพเป็นข้อความ พร้อมโค้ดเต็มและเคล็ดลับรวมอยู่ด้วย
og_title: วิธีใช้ OCR ใน C# – แยกข้อความจากรูปภาพ
tags:
- C#
- Aspose OCR
- Image Processing
title: วิธีใช้ OCR ใน C# – แยกข้อความจากภาพอย่างรวดเร็ว
url: /th/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – แยกข้อความจากรูปภาพอย่างรวดเร็ว

เคยสงสัย **วิธีใช้ OCR** ในโครงการ .NET เพื่อดึงข้อความออกจากรูปภาพหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาหลายคนเจออุปสรรคเมื่อต้อง *แยกข้อความจากรูปภาพ* โดยเฉพาะไฟล์ JPEG และมักจะค้นหาโค้ด “มหัศจรรย์” ที่ทำงานได้เลย

เรื่องนี้คือ—Aspose OCR ทำให้กระบวนการทั้งหมดเป็นเรื่องง่าย ในบทแนะนำนี้เราจะพาคุณผ่านทุกอย่างที่คุณต้องการเพื่อ **แปลงรูปภาพเป็นข้อความ**, ดึงข้อความจาก JPEG, และ—ใช่—คุณจะเห็นผลลัพธ์ที่แน่นอนบนคอนโซลของคุณ ไม่มีการอ้างอิงที่คลุมเครือ เพียงตัวอย่างที่สมบูรณ์และสามารถรันได้

## สิ่งที่คุณจะได้เรียนรู้

- ติดตั้งแพ็กเกจ NuGet ของ Aspose OCR.
- เริ่มต้น OCR engine ใน **online mode** เพื่อให้ดาวน์โหลด language pack ที่ขาดหายโดยอัตโนมัติ.
- โหลดโมเดลภาษาซิริลิก (หรือภาษาอื่นที่คุณต้องการ).
- ส่งภาพ JPEG ไปยัง engine และ **recognize text from image**.
- จัดการกับปัญหาทั่วไปเช่นไฟล์หายหรือรูปแบบที่ไม่รองรับ.
- ดูโค้ดเต็มที่คุณสามารถ copy‑paste ไปยัง Visual Studio ได้ทันที.

> **เคล็ดลับ:** หากคุณทำงานกับ PDF ที่สแกน คุณสามารถดึงแต่ละหน้าเป็นภาพและส่งให้ engine เดียวกัน—ไม่มีการเปลี่ยนแปลงใด ๆ ในโค้ด.

---

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมี:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Aspose OCR รองรับ runtime สมัยใหม่ |
| Visual Studio 2022 (or any IDE you like) | ช่วยในการดีบักและ IntelliSense อย่างสะดวก |
| A JPEG image containing text (e.g., `cyrillic_sample.jpg`) | เราจะ **extract text from JPEG** ในการสาธิต |
| Internet connection (for the first run) | Engine จะดาวน์โหลด language pack ใน **online mode**. |

หากขาดรายการใดรายการหนึ่ง บทแนะนำนี้ยังคงคอมไพล์ได้ แต่ OCR engine อาจโยน exception เมื่อไม่พบ language model

## ขั้นตอนที่ 1 – ติดตั้งแพ็กเกจ NuGet ของ Aspose OCR

สิ่งแรกที่คุณต้องการคือไลบรารีเอง เปิด **Package Manager Console** แล้วรัน:

```powershell
Install-Package Aspose.OCR
```

หรือถ้าคุณชอบใช้ UI ให้ค้นหา “Aspose.OCR” ใน NuGet Package Manager แล้วคลิก **Install**. การทำเช่นนี้จะดึง DLL ที่จำเป็นทั้งหมด รวมถึง core OCR engine และ language model ที่สามารถดึงตามต้องการ

> **ทำไมขั้นตอนนี้สำคัญ:** หากไม่มีแพ็กเกจ คลาสเช่น `OcrEngine` หรือ `LanguageModel` จะไม่มีอยู่ ดังนั้นโค้ดของคุณจะไม่คอมไพล์

## ขั้นตอนที่ 2 – เริ่มต้น OCR Engine (Primary Keyword)

เมื่อไลบรารีพร้อมใช้งาน เราสามารถ **how to use OCR** โดยการสร้างอินสแตนซ์ของ `OcrEngine`. การใช้ `ResourceMode.Online` บอก Aspose ให้ดึง language pack ที่ขาดหายโดยอัตโนมัติ ซึ่งเหมาะสำหรับการทำต้นแบบอย่างรวดเร็ว

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine in online mode.
// This will download language packs if they aren’t already present.
OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);
```

> **อะไรที่เกิดขึ้นเบื้องหลัง?** Engine จะติดต่อ CDN ของ Aspose ตรวจสอบ language model ที่คุณร้องขอ แล้วดึงไฟล์ที่จำเป็นไปยังแคชในเครื่อง การรันครั้งต่อไปจะทำงานแบบออฟไลน์ ทำให้การประมวลผลเร็วขึ้น

## ขั้นตอนที่ 3 – โหลด Language Model ที่ต้องการ

หากคุณทำงานกับข้อความภาษาอังกฤษ `LanguageModel.English` เป็นค่าเริ่มต้น ในตัวอย่างของเราจะโหลด **Cyrillic** แต่คุณสามารถเปลี่ยนเป็นภาษาอื่นที่รองรับได้

```csharp
// Load the Cyrillic language model so the engine knows which characters to look for.
ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
```

> **กรณีขอบ:** หากคุณพยายามโหลดภาษาที่ไม่รองรับ (เช่น `LanguageModel.Klingon`) จะเกิด `UnsupportedLanguageException`. ควรห่อการเรียกในบล็อก try‑catch หากคุณสร้าง UI ที่ให้ผู้ใช้เลือกภาษาแบบเรียลไทม์

## ขั้นตอนที่ 4 – ระบุภาพ (Secondary Keyword: extract text from jpeg)

ที่นี่เราชี้ engine ไปที่ไฟล์ JPEG ที่มีข้อความที่เราต้องการอ่าน `ImageStream.FromFile` รองรับรูปแบบภาพใด ๆ ที่ Aspose สามารถถอดรหัสได้ แต่ JPEG เป็นรูปแบบที่พบบ่อยที่สุดสำหรับภาพถ่ายและสกรีนช็อต

```csharp
// Replace the path with the actual location of your JPEG image.
string imagePath = @"C:\Images\cyrillic_sample.jpg";

if (!File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Load the image into the OCR engine.
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **ทำไมเรื่องนี้สำคัญ:** การระบุพาธที่ไม่มีอยู่จะทำให้เกิด `FileNotFoundException`. เงื่อนไขตรวจสอบด้านบนจะป้องกันโปรแกรมจากการหยุดทำงานและให้ข้อความที่ชัดเจนแก่ผู้ใช้

## ขั้นตอนที่ 5 – แยกข้อความจากรูปภาพและแสดงผล

หัวใจของ **how to use OCR** คือเมธอด `Recognize`. มันจะคืนค่าเป็นสตริงธรรมดาที่มีอักขระที่ตรวจพบทั้งหมด พร้อมรักษาการขึ้นบรรทัดใหม่เมื่อเป็นไปได้

```csharp
try
{
    // Perform the OCR operation.
    string recognizedText = ocrEngine.Recognize();

    // Output the extracted text to the console.
    Console.WriteLine("📝 Recognized Text:");
    Console.WriteLine(recognizedText);
}
catch (Exception ex)
{
    Console.WriteLine($"⚠️ OCR failed: {ex.Message}");
}
```

### ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล

หาก JPEG มีวลี “Привет мир” (Hello world ในภาษารัสเซีย) คุณจะเห็นประมาณนี้:

```
📝 Recognized Text:
Привет мир
```

หากภาพเบลอ ผลลัพธ์อาจมีอักขระผิดรูป—นี่คือจุดที่การทำพรีโพรเซส (เช่น เพิ่มคอนทราสต์) สามารถช่วยได้ ซึ่งเราจะพูดถึงต่อไป

## ขั้นตอนที่ 6 – ตัวอย่างทำงานเต็ม (รวมทุกขั้นตอน)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกไปยังโปรเจกต์ **Console App** ใหม่ได้ มันรวมทุกอย่างตั้งแต่การติดตั้งแพ็กเกจจนถึงการจัดการข้อผิดพลาด ทำให้คุณสามารถรันได้ทันที

```csharp
// ------------------------------------------------------------
// Complete OCR Example – How to use OCR in C#
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine (online mode auto‑downloads language packs)
            OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);

            // 2️⃣ Load the language model you need (Cyrillic in this demo)
            try
            {
                ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
            }
            catch (Exception langEx)
            {
                Console.WriteLine($"❌ Language load error: {langEx.Message}");
                return;
            }

            // 3️⃣ Provide the image – this is where we **extract text from jpeg**
            string imagePath = @"YOUR_DIRECTORY\cyrillic_sample.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Cannot find image at {imagePath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Recognize text – the heart of **how to use OCR**
            try
            {
                string recognizedText = ocrEngine.Recognize();

                // 5️⃣ Output – **convert image to text** and display it
                Console.WriteLine("📝 Recognized Text:");
                Console.WriteLine(recognizedText);
            }
            catch (Exception ocrEx)
            {
                Console.WriteLine($"⚠️ OCR operation failed: {ocrEx.Message}");
            }
        }
    }
}
```

> **ทดสอบเร็ว:** แทนที่ `YOUR_DIRECTORY\cyrillic_sample.jpg` ด้วยพาธจริงของ JPEG ที่มีข้อความชัดเจน รันโปรเจกต์ (F5) แล้วดูคอนโซลพิมพ์สตริงที่ดึงออกมา

## ขั้นตอนที่ 7 – เคล็ดลับ, กรณีขอบ, และคำถามทั่วไป

### ฉันจะ **recognize text from image** ไฟล์ที่ไม่ใช่ JPEG ได้อย่างไร?

Aspose OCR รองรับ PNG, BMP, TIFF, และแม้กระทั่งหน้า PDF (เมื่อคุณแปลงเป็นภาพก่อน). เพียงเปลี่ยนส่วนขยายไฟล์ใน `ImageStream.FromFile`. โค้ดเดียวกันทำงานได้—ไม่ต้องตั้งค่าเพิ่ม

### ถ้าภาพมีความละเอียดต่ำจะทำอย่างไร?

OCR accuracy drops dramatically below 300 dpi. You can improve results by:

1. ขยายภาพด้วยไลบรารีเช่น **ImageSharp**.
2. ใช้การตั้งค่า binary threshold เพื่อเพิ่มคอนทราสต์.
3. ตั้งค่า `ocrEngine.Settings.Deskew = true` เพื่อทำให้ข้อความเอียงตรงขึ้น.

```csharp
ocrEngine.Settings.Deskew = true; // Auto‑corrects rotated text
```

### ฉันสามารถ **convert image to text** เป็นกลุ่มได้หรือไม่?

ได้เลย. ห่อโลจิกการแยกข้อความในลูป `foreach` ที่วนผ่านโฟลเดอร์ของภาพ. จำไว้ว่าให้ใช้ `OcrEngine` อินสแตนซ์เดียวกัน—มันแคช language pack และเร่งการประมวลผลแบบแบตช์

```csharp
string[] files = Directory.GetFiles(@"C:\Images", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string txt = ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), txt);
}
```

### โค้ดนี้ทำงานบน Linux/macOS หรือไม่?

ใช่. Aspose OCR เป็นข้ามแพลตฟอร์มตราบใดที่คุณติดตั้ง .NET runtime. สิ่งเดียวที่อาจเป็นอุปสรรคคือ dependencies เนทีฟสำหรับการถอดรหัสภาพ ซึ่งรวมอยู่ในแพ็กเกจ NuGet

### ฉันจะ **extract text from jpeg** พร้อมรักษาเลย์เอาต์ได้อย่างไร?

ตั้งค่า `ocrEngine.Settings.PreserveFormatting = true`. การตั้งค่านี้จะรักษาการขึ้นบรรทัดใหม่และตารางง่าย ๆ ทำให้ผลลัพธ์อ่านง่ายขึ้น

```csharp
ocrEngine.Settings.PreserveFormatting = true;
```

## สรุป

ในไม่กี่ขั้นตอน เราได้แสดง **how to use OCR** ใน C# เพื่อ **recognize text from image**, **extract text from JPEG**, และ **convert image to text** ด้วย Aspose OCR ตัวอย่างเต็มทำงานทันที จัดการไฟล์ที่หายไป และให้ฟีดแบ็คทันทีบนคอนโซล

จากนี้คุณสามารถ:

- เปลี่ยน `LanguageModel.Cyrillic` เป็นภาษาอื่นใดก็ได้ (English, Arabic, Chinese, ฯลฯ).
- ประมวลผลภาพเป็นกลุ่มเพื่ออัตโนมัติการกรอกข้อมูล.
- รวม OCR กับการประมวลผลภาษาธรรมชาติเพื่อทำดัชนีเอกสารที่สแกน

ดังนั้นลองเลย—ทดลองโค้ด, ทดลองกับคุณภาพภาพต่าง ๆ, และให้ engine ทำงานหนักแทนคุณ หากเจอปัญหา ชุมชน (และเอกสารของ Aspose) อยู่แค่การค้นหาเดียวเท่านั้น. ขอให้เขียนโค้ดอย่างสนุก!

---

![ตัวอย่างการใช้ OCR](placeholder-image.png "ตัวอย่างการใช้ OCR ใน C#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-29
description: วิธีใช้ OCR กับ Aspose เพื่อดึงข้อความจากไฟล์ PNG และแปลงภาพเป็นข้อความ
  เรียนรู้การทำ OCR แบบอะซิงโครนัสขั้นตอนต่อขั้นตอนใน C#
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: th
og_description: วิธีใช้ OCR กับ Aspose ใน C# เพื่อดึงข้อความจากไฟล์ PNG คู่มือนี้จะพาคุณผ่านการทำ
  OCR แบบอะซิงโครนัส โค้ด และเคล็ดลับ
og_title: วิธีใช้ OCR ใน C# – ดึงข้อความจากภาพ PNG
tags:
- OCR
- C#
- Aspose
title: วิธีใช้ OCR ใน C# – ดึงข้อความจากภาพ PNG อย่างรวดเร็ว
url: /th/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – ดึงข้อความจากภาพ PNG อย่างรวดเร็ว

เคยสงสัย **วิธีใช้ OCR** เพื่อดึงข้อความออกจากภาพ PNG สกรีนช็อตไม่กี่ภาพหรือไม่? บางทีคุณอาจมีใบเสร็จสแกน, ใบแจ้งหนี้, หรือโมเก็ต UI และต้องการข้อความนั้นในรูปแบบที่ค้นหาได้ ข่าวดีคือ ด้วย Aspose.OCR คุณสามารถแปลงภาพเป็นข้อความได้ด้วยเพียงไม่กี่บรรทัดของโค้ด C# แบบ asynchronous  

ในบทเรียนนี้เราจะแสดงให้คุณเห็นขั้นตอนการดึงข้อความจากไฟล์ PNG อย่างละเอียด, อธิบายว่าทำไมแต่ละขั้นตอนถึงสำคัญ, และให้โปรแกรมพร้อมรันที่พิมพ์ข้อความที่รับรู้ได้สำหรับทุกหน้า. เมื่อจบคุณจะสามารถ **ดึงข้อความจากภาพ** ได้โดยไม่ต้องค้นหาในเอกสารอื่น ๆ

## สิ่งที่คุณจะได้เรียนรู้

- ติดตั้งและอ้างอิงแพ็กเกจ NuGet ของ Aspose.OCR  
- เริ่มต้น OCR engine และตั้งค่าภาษา (อังกฤษในตัวอย่างนี้)  
- ส่งอาร์เรย์ของไฟล์ PNG ไปยัง `RecognizeImagesAsync` เพื่อการประมวลผลที่เร็วและไม่บล็อก  
- วนลูปผ่านอ็อบเจ็กต์ `OcrResult` และแสดงสตริงที่ดึงออกมา  

ไม่มีบริการภายนอก, ไม่มี callback ซับซ้อน—แค่ C# async ที่สะอาดและทำงานบน .NET 6+

---

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผล |
|-------------|--------|
| .NET 6 SDK (or later) | ฟีเจอร์ภาษาใหม่ ๆ เช่น `async Main` |
| Visual Studio 2022 or VS Code | IDE สำหรับคอมไพล์และรันโค้ด |
| Aspose.OCR NuGet package (`Aspose.OCR`) | ให้คลาส `OcrEngine` ที่ใช้ในตัวอย่าง |
| A few PNG images (`page1.png`, `page2.png`, …) | ไฟล์อินพุตสำหรับกระบวนการ OCR |

ถ้าคุณมีโปรเจกต์ .NET อยู่แล้ว เพียงรัน `dotnet add package Aspose.OCR`. หากยังไม่มี ให้สร้างคอนโซลแอปใหม่ด้วย `dotnet new console -n OcrDemo`.

---

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR และตั้งค่าโปรเจกต์

แรกสุดให้เพิ่มไลบรารี OCR เข้าไปในโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.OCR
```

ทำไมขั้นตอนนี้สำคัญ: Aspose.OCR รวมเอา OCR engine แบบ native, language packs, และ API ที่เรียบง่ายไว้ด้วยกัน. การดึงผ่าน NuGet ทำให้คุณมั่นใจว่าเวอร์ชันเข้ากันได้และอัปเดตอัตโนมัติ

---

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine และเลือกภาษา

Engine ต้องรู้ว่าจะมองหาภาษาอะไร. ภาษาอังกฤษเป็นภาษาที่ใช้บ่อยที่สุด, แต่คุณสามารถสลับเป็น `Language.Spanish`, `Language.French` ฯลฯ ได้

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **เคล็ดลับ:** ควรตั้งค่าภาษาอย่างชัดเจนเสมอ; การปล่อยให้เป็นค่าเริ่มต้นอาจทำให้ความแม่นยำลดลงและเพิ่มเวลาประมวลผล

---

## ขั้นตอนที่ 3: เตรียมรายการไฟล์ PNG

คุณสามารถส่งไฟล์เดียวหรืออาร์เรย์ได้. การส่งอาร์เรย์ทำให้ engine สามารถประมวลผลเป็นชุดแบบ asynchronous, เหมาะสำหรับหลายหน้า

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

หากภาพของคุณอยู่ในโฟลเดอร์ย่อย ให้เพิ่มพาธสัมพัทธ์ (`"images/page1.png"`). Engine จะโยน `FileNotFoundException` ที่ชัดเจนหากพาธผิด—ดังนั้นตรวจสอบชื่อไฟล์ให้แน่ใจ

---

## ขั้นตอนที่ 4: รัน OCR แบบ Asynchronous บนทุกภาพ

เมธอด `RecognizeImagesAsync` จะคืนค่าอาร์เรย์ของ `OcrResult`. เนื่องจากเป็น async, UI (หรือคอนโซล) จะยังคงตอบสนองขณะ OCR ทำงานในพื้นหลัง

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**ทำไมต้อง async?**  
หากคุณนำ OCR ไปใช้ในเว็บ API หรือแอปเดสก์ท็อป, คุณไม่ต้องการให้เธรดบล็อกขณะ engine สแกนพิกเซลแต่ละจุด. `await` จะปล่อยเธรดกลับไปยัง thread pool, ช่วยเพิ่มความสามารถในการขยาย

---

## ขั้นตอนที่ 5: แสดงข้อความที่ดึงออกมาสำหรับแต่ละหน้า

ตอนนี้เรามีผลลัพธ์แล้ว, ให้วนลูปผ่านและพิมพ์ข้อความที่รับรู้ได้. คุณสมบัติ `Text` มีข้อความแบบ plain‑text พร้อมใช้ต่อ (เช่น บันทึกลงฐานข้อมูล)

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `page1.png` มีข้อความ “Invoice #12345” และ `page2.png` มี “Total: $89.99”, คุณจะเห็นประมาณนี้:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

หาก OCR ไม่พบข้อความใดเลย, คุณสมบัติ `Text` จะเป็นสตริงว่าง—ในโค้ดจริงควรตรวจสอบด้วย `string.IsNullOrWhiteSpace`

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน `Program.cs`. รวมทุก using directive, async `Main`, และคอมเมนต์ที่อธิบายแต่ละขั้นตอน

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

บันทึกไฟล์, วาง PNG ของคุณไว้ข้างไฟล์ executable (หรือปรับพาธ), แล้วรัน:

```bash
dotnet run
```

คุณควรเห็นข้อความที่ดึงออกมาปรากฏในคอนโซล, ยืนยันว่าคุณได้ **แปลงภาพเป็นข้อความ** สำเร็จแล้ว

---

## การจัดการกรณีขอบทั่วไป

| สถานการณ์ | วิธีทำ |
|-----------|------------|
| **PNG ความละเอียดต่ำ** | เพิ่ม `ocrEngine.ImageProcessingOptions.Dpi` ก่อนทำการรับรู้ |
| **หลายภาษา** | ตั้งค่า `ocrEngine.Language = Language.English | Language.Spanish;` (OR แบบบิต) |
| **แบชขนาดใหญ่ (หลายร้อยไฟล์)** | ประมวลผลเป็นชิ้นส่วน (เช่น 20 ไฟล์ต่อการเรียก `RecognizeImagesAsync`) เพื่อลดการใช้หน่วยความจำ |
| **ต้องการคะแนนความเชื่อมั่น** | ใช้ `ocrResults[i].Confidence` (ค่า float ระหว่าง 0‑1) เพื่อตัดผลลัพธ์คุณภาพต่ำ |

การปรับแต่งเหล่านี้ช่วยให้ pipeline OCR ของคุณแข็งแรง, โดยเฉพาะเมื่อย้ายจากเดโมสู่การผลิต

---

## โบนัส: บันทึกผลลัพธ์ลงไฟล์ข้อความ

หากคุณต้องการสำเนาถาวรแทนการพิมพ์บนคอนโซล, เพิ่มฟังก์ชันช่วยเล็ก ๆ นี้:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

ตอนนี้คุณมีไฟล์เดียวที่ **ดึงข้อความจากภาพ** สำหรับการประมวลผลต่อไป—เหมาะสำหรับการทำดัชนี, การค้นหา, หรือป้อนให้กับโมเดลภาษา

---

## สรุป

เราได้อธิบาย **วิธีใช้ OCR** ใน C# ด้วย Aspose เพื่อ **ดึงข้อความจาก PNG** และ **แปลงภาพเป็นข้อความ** อย่างมีประสิทธิภาพ. วิธี async ทำให้แอปของคุณตอบสนองได้ดี, ส่วน API ที่ตรงไปตรงมาช่วยให้โค้ดอ่านง่ายและบำรุงรักษาได้ง่าย  

ลองใช้กับเอกสารของคุณ, ทดลองกับภาษาต่าง ๆ, หรือแม้กระทั่งต่อผลลัพธ์เข้าไปยังดัชนีการค้นหา หรือบริการสรุปข้อความ. เมื่อคุณสามารถเปลี่ยนรูปภาพเป็นสตริงที่ค้นหาได้แล้ว โอกาสก็ไม่มีที่สิ้นสุด

---

### ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

- **ดึงข้อความจากภาพ** ในรูปแบบอื่น (JPEG, TIFF) – เพียงเปลี่ยนนามสกุลไฟล์  
- **ประมวลผลแบชด้วย Parallel.ForEach** สำหรับงานจำนวนมาก  
- **ทำความสะอาดผลลัพธ์หลัง OCR** ด้วย regular expressions เพื่อทำให้วันที่, จำนวนเงิน, หรือรหัสต่าง ๆ มีรูปแบบเดียวกัน  
- **รวมกับ Azure Cognitive Services** หากต้องการ OCR บนคลาวด์พร้อมฟีเจอร์เพิ่มเติม  

หากคุณเจอปัญหาใด ๆ หรืออยากแชร์วิธีที่ขยายจากกระบวนการพื้นฐานนี้, อย่าลังเลที่จะคอมเมนต์. Happy coding!   (Image: ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="how to use OCR example output"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
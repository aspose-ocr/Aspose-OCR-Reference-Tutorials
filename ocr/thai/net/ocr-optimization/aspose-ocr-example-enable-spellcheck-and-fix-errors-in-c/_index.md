---
category: general
date: 2026-03-07
description: ตัวอย่าง Aspose OCR ที่แสดงวิธีเปิดใช้งานการตรวจสอบการสะกด, เพิ่มพจนานุกรมกำหนดเอง,
  โหลด OCR ของรูปภาพและแก้ไขข้อผิดพลาดของ OCR อย่างรวดเร็ว.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: th
og_description: ตัวอย่าง Aspose OCR ที่แนะนำขั้นตอนการเปิดใช้งานการตรวจสอบการสะกด,
  เพิ่มพจนานุกรมกำหนดเอง, โหลดภาพสำหรับ OCR และแก้ไขข้อผิดพลาด OCR ที่พบบ่อย
og_title: ตัวอย่าง Aspose OCR – เปิดใช้งานการตรวจสอบการสะกดและแก้ไขข้อผิดพลาด
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: ตัวอย่าง Aspose OCR – เปิดใช้งานการตรวจสอบการสะกดและแก้ไขข้อผิดพลาดใน C#
url: /th/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตัวอย่าง Aspose OCR – เปิดใช้งานการตรวจสอบการสะกดและแก้ไขข้อผิดพลาดใน C#

เคยต้องการ **ตัวอย่าง Aspose OCR** ที่ไม่เพียงแค่อ่านข้อความจากรูปภาพ แต่ยังทำความสะอาดข้อผิดพลาดการสะกดที่น่ารำคาญด้วยหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ ผลลัพธ์ OCR ดิบมักเต็มไปด้วยคำที่พิมพ์ผิด โดยเฉพาะเมื่อภาพต้นทางมีฟอนต์ที่คอนทราสต์ต่ำหรือเป็นโน้ตมือ

ข่าวดีคือ? ด้วย Aspose.OCR คุณสามารถ **เปิดใช้งานการตรวจสอบการสะกด**, ใส่พจนานุกรมของคุณเอง, และได้สตริงที่เรียบร้อยในเพียงไม่กี่บรรทัดของโค้ด ด้านล่างคุณจะได้เห็น **วิธีเปิดใช้งานการตรวจสอบการสะกด**, **วิธีเพิ่มพจนานุกรม**, และ **วิธีโหลด OCR ของรูปภาพ** เพื่อที่คุณจะได้ **แก้ไขข้อผิดพลาด OCR** โดยไม่ต้องบีบผม

ในบทเรียนนี้เราจะครอบคลุมทุกอย่างที่คุณต้องการ — ตั้งแต่การติดตั้ง NuGet จนถึงโปรแกรมที่ทำงานได้เต็มรูปแบบและพิมพ์ข้อความที่แก้ไขแล้ว เมื่อจบคุณจะมี **ตัวอย่าง Aspose OCR** ที่พร้อมใส่ลงในโครงการ .NET ใดก็ได้

## ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core และ .NET Framework ด้วย)
- Visual Studio 2022 หรือ IDE ที่รองรับ C#
- ไฟล์รูปภาพ (`typed_text.png`) ที่มีข้อความภาษาอังกฤษพิมพ์ชัดเจน
- การเชื่อมต่ออินเทอร์เน็ตเพื่อดาวน์โหลดแพ็กเกจ Aspose.OCR NuGet

ไม่มีไลบรารีของบุคคลที่สามอื่น ๆ ที่จำเป็น

---

## ขั้นตอนที่ 1 – ติดตั้งแพ็กเกจ Aspose.OCR NuGet (Load Image OCR)

ก่อนที่เราจะเขียนโค้ดใด ๆ เราต้องมีไลบรารีที่เป็นหัวใจของเครื่องมือ OCR

```bash
dotnet add package Aspose.OCR
```

> **เคล็ดลับ:** หากคุณใช้ Visual Studio ให้คลิกขวาที่โครงการ → *Manage NuGet Packages* → ค้นหา **Aspose.OCR** แล้วกด *Install*  

การติดตั้งแพ็กเกจจะทำให้คุณเข้าถึง `OcrEngine`, `ImageStream` และยูทิลิตี้การตรวจสอบการสะกดที่มีมาให้ซึ่งเราจะใช้ต่อไป เมื่อแพ็กเกจพร้อมแล้ว คุณก็พร้อมที่จะ **load image OCR** แล้ว

## ขั้นตอนที่ 2 – สร้างอินสแตนซ์ของ OCR Engine

การสร้างเอนจินเป็นขั้นตอนแรกที่ชัดเจนใน **ตัวอย่าง Aspose OCR** ใคร่คิดว่า `OcrEngine` คือสมองที่วิเคราะห์บิตแมปและสกัดข้อความออกมา

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

คอนสตรัคเตอร์ของ `OcrEngine` ไม่ต้องการพารามิเตอร์ใด ๆ ทำให้มันเรียบง่ายและเหมาะกับการทำต้นแบบอย่างรวดเร็ว

## ขั้นตอนที่ 3 – วิธีเปิดใช้งานการตรวจสอบการสะกด (และทำไมถึงสำคัญ)

ผลลัพธ์ OCR ดิบมักมีคำที่ถูกจำแนกผิด เช่น “teh” แทน “the” การเปิดใช้งานตัวตรวจสอบการสะกดในตัวจะทำให้ Aspose แก้ไขคำเหล่านั้นโดยอัตโนมัติเป็นการสะกดที่น่าจะถูกต้องที่สุด

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **ทำไมต้องเปิดใช้งานการตรวจสอบการสะกด?**  
> - **ความแม่นยำ:** การตรวจสอบการสะกดหลังการประมวลผลสามารถเพิ่มความแม่นยำของข้อความโดยรวมได้ 10‑15 % สำหรับเอกสารที่พิมพ์  
> - **ประสบการณ์ผู้ใช้:** ข้อความที่สะอาดหมายถึงการทำความสะอาดขั้นต่อไปที่น้อยลงเมื่อคุณนำผลลัพธ์ไปใส่ในดัชนีการค้นหาหรือสายงานวิเคราะห์ข้อมูล

## ขั้นตอนที่ 4 – วิธีเพิ่มพจนานุกรม (คำศัพท์เฉพาะ)

บางครั้งพจนานุกรมเริ่มต้นไม่รู้จักชื่อแบรนด์, รหัสสินค้า, หรือศัพท์เฉพาะด้านของคุณ นั่นคือเหตุผลที่ **วิธีเพิ่มพจนานุกรม** มีความสำคัญ

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

คุณสามารถใส่เป็นอาเรย์, รายการ, หรือแม้กระทั่งอ่านจากไฟล์หากมีคำศัพท์จำนวนมาก ตัวตรวจสอบการสะกดจะถือรายการเหล่านี้ว่าเป็นคำที่ถูกต้องและไม่ทำการแก้ไขผิดพลาด

## ขั้นตอนที่ 5 – โหลดรูปภาพสำหรับ OCR (Load Image OCR)

เมื่อเอนจินตั้งค่าเรียบร้อยแล้ว เราต้องชี้ให้มันไปที่รูปภาพที่ต้องการอ่าน `ImageStream.FromFile` ช่วยซ่อนรายละเอียดการอ่านไฟล์ไว้ให้

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **เคล็ดลับ:** หากรูปภาพของคุณอยู่ในโฟลเดอร์ย่อยของโครงการ ให้ตั้งค่าคุณสมบัติ *Copy to Output Directory* เป็น *Copy always* เพื่อให้เส้นทางสามารถแก้ไขได้ในขณะรันไทม์

## ขั้นตอนที่ 6 – ทำการจดจำและแก้ไขข้อผิดพลาด OCR

เมื่อทุกอย่างพร้อม การเรียก `Recognize()` ครั้งเดียวจะรันไพป์ไลน์ OCR, ใช้การตรวจสอบการสะกด, และเก็บผลลัพธ์ที่ทำความสะอาดไว้ใน `ocrEngine.Text`

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `typed_text.png` มีประโยค `The quick brown fox jumps over teh lazy dog` คอนโซลจะพิมพ์:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

สังเกตว่า “teh” ถูกแก้เป็น “the” โดยอัตโนมัติ หากคุณได้เพิ่ม “OCRify” ลงในพจนานุกรมเฉพาะและรูปภาพมีคำนั้น เอนจินก็จะคงไว้โดยไม่แก้ไข

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถวางลงในโปรเจกต์คอนโซลใหม่ได้ รวมทุกขั้นตอนข้างต้นพร้อมคอมเมนต์อธิบายสั้น ๆ

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

บันทึกไฟล์นี้เป็น `Program.cs`, รัน `dotnet run` แล้วคุณจะเห็นประโยคที่แก้ไขแล้วแสดงบนคอนโซล

---

## คำถามที่พบบ่อย & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ถ้าภาพเป็น PDF แบบหลายหน้า จะทำอย่างไร?** | Aspose.OCR สามารถจัดการหน้า PDF เป็นภาพได้ ใช้ `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` แล้ววนลูปผ่านหน้าต่าง ๆ |
| **สามารถเปลี่ยนภาษาเป็นนอกเหนือจากอังกฤษได้หรือไม่?** | ทำได้แน่นอน ตั้งค่า `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (หรือภาษาอื่นที่รองรับ) |
| **พจนานุกรมของฉันมีขนาดใหญ่ — จะส่งผลต่อประสิทธิภาพหรือไม่?** | การเพิ่มคำหลายพันคำจะใช้เวลาเตรียมเล็กน้อย แต่การค้นหาเป็น O(1) เนื่องจากใช้ hash‑set ภายใน หากมีคำศัพท์มหาศาล ควรโหลดครั้งเดียวเมื่อตัวแอปเริ่มทำงาน |
| **ถ้าเอนจิน OCR โยนข้อยกเว้นเมื่อรูปภาพเสียหายจะทำอย่างไร?** | ห่อ `Recognize()` ด้วย try‑catch แล้วตรวจสอบ `ocrEngine.LastError` คุณยังสามารถตรวจสอบขนาดภาพล่วงหน้าด้วย `ocrEngine.Image.Width` และ `Height` |
| **ต้องมีลิขสิทธิ์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** | เวอร์ชันประเมินผลฟรีใช้ได้สำหรับการทดสอบ แต่ลิขสิทธิ์เชิงพาณิชย์จะลบลายน้ำการประเมินและเปิดประสิทธิภาพเต็มรูปแบบ |

---

## สรุป

คุณมี **ตัวอย่าง Aspose OCR** ครบถ้วนที่แสดง **วิธีเปิดใช้งานการตรวจสอบการสะกด**, **วิธีเพิ่มพจนานุกรม**, **วิธีโหลด OCR ของรูปภาพ**, และ **วิธีแก้ไขข้อผิดพลาด OCR** อย่างเป็นระบบและพร้อมใช้งานในสภาพแวดล้อมการผลิต การตั้งค่าตัวตรวจสอบการสะกดและใส่รายการคำเฉพาะจะช่วยปรับปรุงคุณภาพของข้อความที่สกัดได้อย่างมหาศาลโดยไม่ต้องเขียนโค้ดหลังการประมวลผลเอง

พร้อมก้าวต่อไปหรือยัง? ลองเปลี่ยนภาษาเป็นสเปน, ใส่ PDF หลายหน้า, หรือผสานผลลัพธ์เข้ากับดัชนี Azure Cognitive Search ที่ค้นหาได้ รูปแบบเดียวกันนี้ใช้ได้—แค่ปรับแฟล็กภาษาและอาจขยายพจนานุกรมเฉพาะ

ถ้าคุณพบว่าคู่มือฉบับนี้มีประโยชน์ อย่าลืมให้ดาวน์โหลดดาวน์โหลดบน GitHub, แบ่งปันกับทีม, หรือแสดงความคิดเห็นด้านล่าง ขอให้เขียนโค้ดอย่างสนุกและผลลัพธ์ OCR ของคุณปราศจากข้อผิดพลาดเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
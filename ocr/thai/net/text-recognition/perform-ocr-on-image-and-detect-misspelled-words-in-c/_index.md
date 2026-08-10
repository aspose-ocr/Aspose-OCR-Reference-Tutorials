---
category: general
date: 2026-06-03
description: ทำการ OCR บนภาพและดึงข้อความจากภาพโดยใช้ Aspose.OCR เรียนรู้วิธีตรวจจับคำที่สะกดผิดและรับคำแนะนำการสะกดในตัวอย่าง
  C# เดียว
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: th
og_description: ทำ OCR บนรูปภาพเพื่อดึงข้อความจากรูปภาพ แล้วตรวจหาคำที่สะกดผิดและรับคำแนะนำการสะกดด้วย
  Aspose.OCR ใน C#
og_title: ทำ OCR บนภาพและตรวจจับคำที่สะกดผิดใน C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: ทำ OCR บนภาพและตรวจจับคำที่สะกดผิดใน C#
url: /th/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพและตรวจหาคำที่สะกดผิดใน C#

เคยสงสัยไหมว่าจะ **ทำ OCR บนรูปภาพ** อย่างไรโดยไม่ต้องบีบหัว? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังดิจิไทซ์จดหมายเก่า สแกนใบเสร็จ หรือสร้างเวิร์กโฟลว์เอกสารอัจฉริยะ การสกัดข้อความที่สะอาดจากรูปภาพเป็นอุปสรรคแรก ข่าวดีคือ ด้วย Aspose.OCR คุณสามารถสร้างโซลูชันได้ในไม่กี่นาที และคุณยังสามารถ **ตรวจหาคำที่สะกดผิด** และ **รับข้อเสนอแนะการสะกด** ในการทำงานเดียวกันได้อีกด้วย

ในบทแนะนำนี้เราจะเดินผ่านแอปคอนโซล C# ที่พร้อม‑รันเต็มรูปแบบซึ่ง **สกัดข้อความจากรูปภาพ**, รันตัวตรวจสอบการสะกดภาษาอังกฤษ, และพิมพ์แต่ละข้อผิดพลาดพร้อมแนวคิดการแก้ไขที่เป็นประโยชน์ เมื่อจบคุณจะรู้ **วิธีสกัดข้อความ**, วิธีเชื่อมต่อกับ API ตรวจสอบการสะกด, และรูปแบบผลลัพธ์คอนโซลที่คาดหวัง

## สิ่งที่คุณจะสร้าง

- โหลดบิตแมป (หรือ PNG) ที่มีข้อผิดพลาดการพิมพ์  
- รัน Aspose.OCR เพื่อ **ทำ OCR บนรูปภาพ** และรับข้อมูลสตริงดิบ  
- เริ่มต้นตัวตรวจสอบการสะกดภาษาอังกฤษในตัว  
- **ตรวจหาคำที่สะกดผิด** และ **รับข้อเสนอแนะการสะกด** สำหรับแต่ละคำ  
- พิมพ์รายงานที่เป็นระเบียบลงคอนโซล

ไม่มีบริการภายนอก ไม่มีการเรียก HTTP ที่ยุ่งยาก—เพียงแพ็กเกจ NuGet เดียวและไม่กี่บรรทัดโค้ด

## ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+)  
- Visual Studio 2022 (หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ)  
- แพ็กเกจ NuGet Aspose.OCR for .NET (`Aspose.OCR`)  
- ไฟล์รูปภาพ (`letter_with_typos.png`) ที่วางไว้ในตำแหน่งที่คุณสามารถอ้างอิงจากโปรเจกต์ได้

หากคุณยังไม่เคยใช้ Aspose มาก่อน ไม่ต้องกังวล—การติดตั้งแพ็กเกจง่ายเหมือนรันคำสั่ง:

```bash
dotnet add package Aspose.OCR
```

ตอนนี้มาดำเนินการลงรายละเอียดการทำงานกัน

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และติดตั้ง Aspose.OCR

สร้างโปรเจกต์คอนโซลใหม่และดึงไลบรารี OCR เข้ามา:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

หลังจากการกู้คืนเสร็จสิ้น ให้เปิด `Program.cs` เราจะเปลี่ยนเนื้อหาเริ่มต้นเป็นโค้ดตัวอย่างเต็มภายหลัง แต่ก่อนนั้นมาพูดถึงเหตุผลที่แต่ละ namespace มีความสำคัญ

- `Aspose.OCR` – เอนจิน OCR หลักและการจัดการรูปภาพ  
- `Aspose.OCR.SpellCheck` – ยูทิลิตี้ตรวจสอบการสะกดที่มาพร้อมกับไลบรารี  
- `System` – คลาสพื้นฐานของ .NET (เช่น `Console`)

## ขั้นตอนที่ 2: โหลดรูปภาพและทำ OCR บนรูปภาพ

งานจริงแรกคือการป้อนรูปภาพให้กับเอนจิน OCR Aspose.OCR รองรับหลายรูปแบบ (PNG, JPEG, TIFF) นี่คือส่วนที่ทำงานหนัก:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **ทำไมส่วนนี้สำคัญ:** `OcrImage.FromFile` จัดการรายละเอียดระดับพิกเซลให้คุณ, ส่วน `OcrEngine.Recognize` รันโมเดลประสาทเทียมที่ฝึกแล้วเพื่อแปลง glyph ที่มองเห็นเป็นอักขระ Unicode. คุณสมบัติ `ocrResult.Text` ตอนนี้ถือสตริงดิบ—สิ่งที่คุณต้องการเพื่อ **สกัดข้อความจากรูปภาพ**  

> **เคล็ดลับ:** หากรูปภาพของคุณมีหลายภาษา คุณสามารถตั้งค่า `ocrEngine.Language = OcrLanguage.Multilingual;` ก่อนเรียก `Recognize`

## ขั้นตอนที่ 3: เริ่มต้นตัวตรวจสอบการสะกดภาษาอังกฤษ

Aspose.OCR มาพร้อมกับเอนจินตรวจสอบการสะกดในตัวที่เข้าใจภาษาอังกฤษโดยอัตโนมัติ การเริ่มต้นเพียงบรรทัดเดียว:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **ทำไมขั้นตอนนี้สำคัญ:** ผลลัพธ์จาก OCR อาจมีอักขระที่รับรู้ผิด (เช่น “l” กับ “1”) หรือข้อผิดพลาดการพิมพ์จริงจากเอกสารต้นฉบับ ตัวตรวจสอบการสะกดจะสแกนสตริง, ค้นหาโทเคนที่สงสัย, และเสนอทางเลือก

## ขั้นตอนที่ 4: ตรวจหาคำที่สะกดผิดและรับข้อเสนอแนะการสะกด

ต่อไปเราจะส่งข้อความ OCR ให้กับตัวตรวจสอบ:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` คือคอลเลกชันที่แต่ละรายการประกอบด้วยคำที่ผิดและอาร์เรย์ของการแก้ไขที่เป็นไปได้

## ขั้นตอนที่ 5: แสดงผลลัพธ์

สุดท้าย เราจะวนลูปคอลเลกชันและพิมพ์รายงานที่อ่านง่าย:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### ผลลัพธ์คอนโซลที่คาดหวัง

สมมติว่า `letter_with_typos.png` มีประโยค:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

การรันตัวอย่างจะให้ผลลัพธ์ประมาณนี้:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

สังเกตว่าข้อผิดพลาดแต่ละคำจะจับคู่กับข้อเสนอการแก้ไขหลายรายการ—สิ่งที่คุณต้องการเมื่อสร้าง UI การแก้ไขที่เป็นมิตรกับผู้ใช้

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรม **พร้อมคัดลอก‑วาง** ทั้งหมด แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริงของไฟล์รูปภาพของคุณ

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **กรณีขอบที่ควรพิจารณา**  
> - **รูปภาพว่าง:** หากเอนจิน OCR คืนสตริงว่าง `spellChecker.Check` จะคืนคอลเลกชันว่าง—ไม่มีการขัดข้อง  
> - **ข้อความไม่ใช่ภาษาอังกฤษ:** เปลี่ยน `OcrLanguage.English` เป็น `OcrLanguage.French` (หรือภาษาอื่นที่รองรับ) เพื่อ **ตรวจหาคำที่สะกดผิด** ในภาษานั้น ๆ  
> - **เอกสารขนาดใหญ่:** สำหรับ PDF หลายหน้า คุณจะต้องวนลูปแต่ละหน้า, ทำ OCR, แล้วรวมผลลัพธ์ก่อนตรวจสอบการสะกด

## ภาพรวมเชิงภาพ (Alt Text)

![Diagram showing the flow to perform OCR on image, extract text from image, and then detect misspelled words with spelling suggestions](perform-ocr-on-image-flow.png)

*แผนภาพด้านบนแสดงกระบวนการจากต้นจนจบ: รูปภาพ → เอนจิน OCR → ข้อความดิบ → ตัวตรวจสอบการสะกด → ข้อเสนอแนะ*

## คำถามที่พบบ่อย & เคล็ดลับขั้นสูง

| Question | Answer |
|----------|--------|
| **Do I need an internet connection?** | No. Aspose.OCR runs entirely locally; perfect for offline or secure environments. |
| **How accurate is the spell‑checker?** | It uses a dictionary of ~150k English words and fuzzy matching, so most common typos are caught. |
| **Can I customize the dictionary?** | Yes. `SpellChecker.AddUserDictionary("custom.txt")` lets you load domain‑specific terms (e.g., product names). |
| **What if the image is skewed?** | The OCR engine auto‑detects orientation, but you can manually call `ocrEngine.ImagePreprocessing.Rotate(angle)` for stubborn cases. |
| **Is there a way to highlight suggestions in UI?** | After you have the `misspellings` collection, you can map each `entry.Word` back to its position in `ocrResult.Text` and underline it in a RichTextBox or web view. |

## สรุป

เราได้แสดงให้คุณเห็น **วิธีทำ OCR บนรูปภาพ**, **สกัดข้อความจากรูปภาพ**, แล้ว **ตรวจหาคำที่สะกดผิด** พร้อม **รับข้อเสนอแนะการสะกด** ทั้งหมดด้วยแอปคอนโซล C# สั้น ๆ แนวคิดหลักคือให้ Aspose.OCR จัดการการรับรู้ตัวอักษรหนัก ๆ แล้วให้ตัวตรวจสอบการสะกดในตัวทำความสะอาดผลลัพธ์ จากนี้คุณสามารถขยายตัวอย่างเป็นบริการประมวลผลเอกสารเต็มรูปแบบ, ผสานกับ Web API, หรือเชื่อมต่อกับแอปเดสก์ท็อป

พร้อมก้าวต่อไปหรือยัง? ลองเปลี่ยนภาษาเป็นสเปน, ป้อน PDF หลายหน้า, หรือสร้าง Front‑end WPF เล็ก ๆ ที่ให้ผู้ใช้คลิกคำเพื่อยอมรับข้อเสนอแนะ. บล็อกพื้นฐานพร้อมใช้งานแล้ว—เพียงทดลองต่อไป

หากคุณเจออุปสรรคหรือมีไอเดียต่อยอด, ฝากคอมเมนต์ด้านล่างได้เลย. Happy coding!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
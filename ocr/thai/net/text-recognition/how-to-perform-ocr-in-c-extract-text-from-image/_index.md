---
category: general
date: 2026-04-03
description: เรียนรู้วิธีทำ OCR ใน C# และสกัดข้อความจากภาพโดยใช้ Aspose OCR พร้อมการตรวจสอบการสะกดสำหรับภาษารัสเซีย
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: th
og_description: เรียนรู้วิธีทำ OCR ด้วย C# และดึงข้อความจากภาพโดยใช้ Aspose OCR พร้อมตรวจสอบการสะกดสำหรับภาษารัสเซีย
og_title: วิธีทำ OCR ใน C# – แยกข้อความจากภาพ
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: วิธีทำ OCR ด้วย C# – ดึงข้อความจากภาพ
url: /th/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ใน C# – แยกข้อความจากรูปภาพ

เคยสงสัย **วิธีทำ OCR** บนรูปถ่ายของโน้ตมือเขียนบ้างไหม? หรือคุณอาจมีใบเสร็จสแกน, ป้ายในภาษาต่างประเทศ, หรือหน้า PDF ที่ไม่สามารถคัดลอก‑วางได้ ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของ C# และไลบรารี Aspose OCR คุณก็สามารถเปลี่ยนรูปภาพนั้นให้เป็นข้อความที่แก้ไขได้ในพริบตา  

ในบทแนะนำนี้เราจะไม่เพียงแสดง **วิธีทำ OCR** เท่านั้น แต่ยังอธิบาย **การแยกข้อความจากรูปภาพ**, **การแปลงรูปภาพเป็นข้อความ**, และแม้กระทั่ง **วิธีตรวจสอบการสะกด** ผลลัพธ์เมื่อคุณทำงานกับเอกสารภาษารัสเซีย ฟังดูเยอะไหม? อย่ากังวล – เราจะอธิบายทุกขั้นตอนอย่างละเอียด

## สิ่งที่คุณจะได้เรียนรู้

เมื่อจบบทแนะนำนี้คุณจะสามารถ:

* ตั้งค่า Aspose OCR เพื่อรองรับภาษารัสเซีย  
* โหลดไฟล์รูปภาพและรันการจดจำอักขระเชิงแสงเพื่อ **แยกข้อความจากรูปภาพ**  
* ใช้ตัวตรวจสอบการสะกดที่มีมาให้เพื่อแก้ไขคำที่พิมพ์ผิดโดยอัตโนมัติ – คำตอบที่สมบูรณ์สำหรับ “**วิธีตรวจสอบการสะกด**” ของผลลัพธ์ OCR  
* พิมพ์สตริงที่ทำความสะอาดแล้วออกทางคอนโซล พร้อมใช้ต่อในกระบวนการหรือการจัดเก็บอื่น ๆ

**ข้อกำหนดเบื้องต้น** – คุณจะต้องมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.8 ด้วย)  
* ไลเซนส์ Aspose OCR ที่ถูกต้องหรือคีย์ประเมินผลชั่วคราว  
* ไฟล์รูปภาพที่มีข้อความภาษารัสเซีย (สำหรับตัวอย่างเราจะใช้ชื่อ `russian_note.jpg`)  

หากคุณไม่คุ้นเคยกับสิ่งใดข้างต้น ไม่ต้องกังวล ขั้นตอนต่อไปจะรวมคำสั่ง NuGet ที่ต้องใช้เพื่อดึง Aspose OCR มา และโค้ดทั้งหมดเป็นแบบ self‑contained

![ตัวอย่างวิธีทำ OCR](/images/ocr-demo.png "ตัวอย่างวิธีทำ OCR ใน C#")

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR และเพิ่ม Namespaces

ก่อนอื่นคุณต้องมีไลบรารีนี้ เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรัน:

```bash
dotnet add package Aspose.OCR
```

คำสั่งนี้จะดึงเวอร์ชันล่าสุดที่เสถียร (ณ เมษายน 2026 เวอร์ชัน 22.9) หลังจากแพ็กเกจถูกกู้คืนแล้ว ให้เพิ่ม `using` directives ที่จำเป็นที่ด้านบนของไฟล์ C# ของคุณ:

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*เคล็ดลับ:* หากคุณใช้ Visual Studio IDE จะเสนอให้เพิ่มเหล่านี้อัตโนมัติเมื่อคุณพิมพ์ชื่อคลาสแรก

## ขั้นตอนที่ 2 – เริ่มต้น OCR Engine สำหรับภาษารัสเซีย

ส่วน **วิธีทำ OCR** เริ่มจากการสร้างอินสแตนซ์ `OcrEngine` โดยระบุ `OcrLanguage.Russian` เพื่อบอกให้เอนจินโหลดชุดอักขระ Cyrillic และอัลกอริทึมเฉพาะภาษา

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

ทำไมต้องทำเช่นนี้? หากไม่ตั้งค่าภาษา เอนจินจะใช้ค่าเริ่มต้นเป็นอังกฤษและจะตีความอักขระ Cyrillic ผิดพลาด ทำให้ผลลัพธ์เป็นข้อความเสียหาย การกำหนดภาษาชัดเจนช่วยเพิ่มความแม่นยำอย่างมาก

## ขั้นตอนที่ 3 – โหลดรูปภาพและ **แปลงรูปภาพเป็นข้อความ**

ต่อไปเรานำรูปภาพเข้ามาในหน่วยความจำ เมธอด `Image.FromFile` รองรับรูปแบบที่พบบ่อย (JPG, PNG, BMP) หลังจากโหลดแล้ว เราเรียก `Recognize` เพื่อ **แปลงรูปภาพเป็นข้อความ**

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

ตัวแปร `rawText` ตอนนี้เก็บผลลัพธ์ OCR ดิบ ซึ่งอาจยังมีการพิมพ์ผิดหรืออักขระที่จดจำผิด คุณสามารถพิมพ์ออกมาดูว่าเอนจินจับอะไรได้บ้าง:

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## ขั้นตอนที่ 4 – **วิธีตรวจสอบการสะกด** ผลลัพธ์ OCR

OCR ภาษารัสเซียมักมีเสียงรบกวน โดยเฉพาะสแกนความละเอียดต่ำ Aspose มีคลาส `SpellChecker` ที่มาพร้อมพจนานุกรมรัสเซียโดยอัตโนมัติ นี่คือตัวอย่างการเรียกใช้:

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

เมธอด `CheckAndCorrect` จะคืนสตริงใหม่ที่แทนที่คำที่สะกดผิดด้วยคำที่คาดว่าถูกต้องที่สุด อีกทั้งยังรักษาเครื่องหมายวรรคตอนไว้ ทำให้คุณไม่ต้องเจอข้อความเป็นก้อนเดียว

*กรณีพิเศษ:* หากผลลัพธ์ OCR ว่างเปล่า (เช่นรูปภาพเป็นสีขาวทั้งหมด) `CheckAndCorrect` จะคืนค่าว่างเปล่าเช่นกัน ควรตรวจสอบก่อนบันทึกผลลัพธ์ลงไฟล์

## ขั้นตอนที่ 5 – แสดงผลลัพธ์ที่ทำความสะอาดแล้ว

สุดท้ายเราจะพิมพ์สตริงที่แก้ไขแล้วออกทางคอนโซล ในแอปพลิเคชันจริงคุณอาจบันทึกลงฐานข้อมูล, ส่งเป็น JSON API, หรือเขียนลงเอกสาร Word สำหรับการสาธิตนี้ การพิมพ์ลงคอนโซลก็เพียงพอแล้ว:

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

เมื่อคุณรันโปรแกรม คุณควรเห็นผลลัพธ์ประมาณนี้:

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

สังเกตว่าตัวตรวจสอบการสะกดได้เปลี่ยน “Привeт” (อักษรละติน ‘e’ ผสม) ให้เป็น Cyrillic ที่ถูกต้อง “Привет” นั่นแหละคือความมหัศจรรย์ของ **วิธีตรวจสอบการสะกด** OCR

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และสามารถรันได้ ซึ่งรวมทุกขั้นตอนไว้ด้วยกัน คัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่แล้วกด **F5**

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมด้วยรูปถ่ายลายมือรัสเซียที่ชัดเจนและความละเอียดสูงมักให้ประโยคที่อ่านง่าย หากรูปภาพเบลอ คุณอาจได้คำบางส่วนที่ยังไม่สมบูรณ์ แต่ตัวตรวจสอบการสะกดจะช่วยแก้ไขข้อผิดพลาดที่ชัดเจนส่วนใหญ่

## ข้อผิดพลาดทั่วไปและเคล็ดลับ

| ปัญหา | สาเหตุ | วิธีแก้ / ป้องกัน |
|-------|--------|-------------------|
| **อักขระแปลก** | DPI ต่ำหรือพื้นหลังมีเสียงรบกวน | ทำการพรี‑โปรเซสภาพ (เพิ่มคอนทราสต์, ปรับขนาดเป็น ≥300 dpi) ก่อนส่งให้ `Recognize` |
| **ผลลัพธ์ว่าง** | เส้นทางไฟล์ผิดหรือฟอร์แมตไม่รองรับ | ตรวจสอบเส้นทางและใช้ `Image.FromFile` ภายใน `try/catch` เพื่อแสดงข้อผิดพลาด |
| **ตัวตรวจสอบการสะกดพลาด** | คำหายากไม่อยู่ในพจนานุกรม | ขยายพจนานุกรมโดยโหลดรายการคำของคุณเองผ่าน `spellChecker.AddUserDictionary("mywords.txt")` |
| **ความช้าเมื่อประมวลผลหลายไฟล์** | OCR ใช้ CPU มาก | รัน OCR บนเธรดแบ็กกราวด์หรือใช้ `Parallel.ForEach` สำหรับหลายรูปภาพ |
| **ข้อยกเว้นไลเซนส์** | ใช้เวอร์ชันประเมินผลเกินระยะทดลอง | ซื้อไลเซนส์และเรียก `License license = new License(); license.SetLicense("Aspose.Total.lic");` ก่อนสร้าง `OcrEngine` |

## ขั้นตอนต่อไป – ไปไกลกว่า OCR เบื้องต้น

เมื่อคุณเชี่ยวชาญ **วิธีทำ OCR** แล้ว ลองขยายความสามารถต่อไปนี้:

* **การประมวลผลเป็นชุด** – วนลูปโฟลเดอร์ของรูปภาพและบันทึกข้อความที่แก้ไขแต่ละไฟล์เป็น `.txt`  
* **การแปลงเป็น PDF** – ใช้ Aspose PDF เพื่อฝังข้อความที่ดึงมาไว้ใน PDF ที่ค้นหาได้  
* **การตรวจจับภาษา** – หากต้องจัดการหลายภาษา ให้ตรวจสอบผล OCR ก่อนและสลับ `OcrLanguage` ตามความเหมาะสม  
* **การรวมกับ Azure Cognitive Services** – เปรียบเทียบผลของ Aspose กับ OCR API ของ Microsoft เพื่อวิธีแบบไฮบริด  

หัวข้อทั้งหมดนี้ล้วนเกี่ยวข้องกับคีย์เวิร์ดรอง **extract text from image**, **convert image to text**, และ **how to spell check**, ดังนั้น

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
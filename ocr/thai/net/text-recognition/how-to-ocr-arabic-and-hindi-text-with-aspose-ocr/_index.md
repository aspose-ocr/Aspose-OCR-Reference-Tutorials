---
category: general
date: 2026-01-15
description: เรียนรู้วิธีทำ OCR ข้อความภาษาอาหรับและจดจำข้อความภาษาฮินดีด้วย Aspose
  OCR คู่มือขั้นตอนนี้จะแสดงให้คุณเห็นวิธีดึงข้อความจากภาพและแปลงภาพเป็นข้อความอย่างมีประสิทธิภาพ
draft: false
keywords:
- how to ocr arabic
- recognize arabic text
- extract text from image
- convert image to text
- recognize hindi text
language: th
og_description: วิธีทำ OCR ข้อความภาษาอาหรับและจดจำข้อความภาษาฮินดีในโปรแกรม C# เดียวกัน.
  ทำตามคู่มือฉบับเต็มนี้เพื่อดึงข้อความจากภาพและแปลงภาพเป็นข้อความ.
og_title: วิธีทำ OCR ข้อความภาษาอาหรับและฮินดีด้วย Aspose OCR
tags:
- Aspose OCR
- C#
- Multilingual OCR
title: วิธีทำ OCR ข้อความภาษาอาหรับและฮินดีด้วย Aspose OCR
url: /th/net/text-recognition/how-to-ocr-arabic-and-hindi-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ข้อความภาษาอาหรับและฮินดีด้วย Aspose OCR

เคยสงสัยไหมว่า **how to ocr arabic** ตัวอักษรที่ไหลจากขวาไปซ้าย, พร้อมกับดึง glyph ของฮินดีจากใบเสร็จ? คุณไม่ได้อยู่คนเดียว. นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อพวกเขาต้อง **recognize arabic text** และ **recognize hindi text** ในขั้นตอนเดียวกัน.  

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่าง C# ที่สมบูรณ์และสามารถรันได้ ซึ่งจะแสดงวิธี **extract text from image** ไฟล์, **convert image to text**, และจัดการสคริปต์ภาษาอาหรับและฮินดีด้วย Aspose OCR. ไม่มีการอ้างอิงที่คลุมเครือ—เพียงโค้ดที่คุณสามารถคัดลอก‑วาง พร้อมเหตุผลเบื้องหลังแต่ละบรรทัด.

> **เคล็ดลับ:** หากคุณยังไม่เคยใช้ Aspose OCR มาก่อน ให้ติดตั้งแพ็กเกจ NuGet `Aspose.OCR` ก่อน. มันเป็นการดำเนินการคลิกเดียวใน Visual Studio, และจะดึงไบนารีเนทีฟทั้งหมดที่คุณต้องการสำหรับการจดจำด้วย CPU.

---

![ตัวอย่างการทำ OCR ภาษาอาหรับ](/images/arabic-ocr-sample.png "ทำ OCR ภาษาอาหรับ – ตัวอย่างป้ายภาษาอาหรับ")

*ข้อความแทนภาพ:* **ทำ OCR ภาษาอาหรับ – ตัวอย่างป้ายภาษาอาหรับ**  

---

## วิธีทำ OCR ภาษาอาหรับ – การตั้งค่าสภาพแวดล้อม

ก่อนที่เราจะลงลึกในโค้ด, มาตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาพร้อมแล้ว.

1. **Target framework** – .NET 6.0 หรือใหม่กว่า. เวอร์ชันเก่าจะยังคอมไพล์ได้, แต่คุณจะพลาดฟีเจอร์ภาษาใหม่ล่าสุด.  
2. **Package** – รัน `dotnet add package Aspose.OCR` ในเทอร์มินัล, หรือใช้ UI ของ NuGet Package Manager.  
3. **Images** – วางรูปตัวอย่างสองภาพในโฟลเดอร์ที่คุณอ้างอิง, เช่น `C:\OCRSamples\arabic_sign.jpg` และ `C:\OCRSamples\hindi_receipt.png`. ภาพภาษาอาหรับควรมีอักขระอาหรับที่ชัดเจนและคอนทราสต์สูง; ภาพภาษาฮินดีอาจเป็นใบเสร็จสแกนหรือภาพถ่ายของป้าย.

เท่านี้—ไม่มีไฟล์การกำหนดค่าเพิ่มเติม, ไม่มีไดรเวอร์ GPU, เพียงเครื่องมือ OCR ที่ทำงานบน CPU อย่างตรงไปตรงมา.

---

## จดจำข้อความภาษาอาหรับ – การโหลดและประมวลผล

ตอนนี้เราจะ **recognize arabic text** จริงๆ. สิ่งสำคัญคือบอกเครื่องมือว่าคาดหวังภาษาชนิดใด; มิฉะนั้นเครื่องมือจะใช้ค่าเริ่มต้นเป็นอักขระละตินและคุณจะได้ผลลัพธ์ที่อ่านไม่ออก.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (CPU‑based by default)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load an image that contains Arabic script
        var arabicImage = OcrImage.FromFile(@"C:\OCRSamples\arabic_sign.jpg");

        // 3️⃣ Recognize the Arabic text – note the Language.Arabic enum
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);

        // 4️⃣ Print the result to the console
        System.Console.WriteLine("Arabic: " + arabicResult.Text);
```

**ทำไมวิธีนี้ถึงได้ผล:**  
* `OcrEngine` จัดการงานหนักทั้งหมด—การเตรียมข้อมูลล่วงหน้า, การแบ่งส่วน, และการจำแนกอักขระ.  
* โดยการส่ง `Language.Arabic`, เราเปิดใช้งานเอนจินจัดวางจากขวาไปซ้ายและชุดอักขระอาหรับ. หากไม่ทำเช่นนี้, เอนจินจะถือภาพเป็นข้อความละตินจากซ้ายไปขวา, ทำให้สูญเสียเครื่องหมายวรรณยุกต์และคำที่แตกหัก.

**ผลลัพธ์ที่คาดหวัง** (ข้อความจริงของคุณอาจแตกต่างตามภาพ):

```
Arabic: مرحبا بكم في متجرنا
```

หากคุณเห็นสตริงว่าง, ตรวจสอบอีกครั้งว่าภาพไม่ได้มืดเกินไปและเส้นทางไฟล์ถูกต้อง.  

---

## ดึงข้อความจากภาพ – การจัดการสคริปต์ขวาไปซ้าย

ภาษาอาหรับไม่ใช่สคริปต์เดียวที่ต้องการการจัดการพิเศษ. ภาษาขวาไปซ้าย (RTL) ต้องการให้เอนจิน OCR กลับลำดับการแสดงผลหลังการจดจำ. Aspose ทำเช่นนี้โดยอัตโนมัติเมื่อคุณระบุ `Language.Arabic`, แต่ควรจำไว้สำหรับการขยายในอนาคต (เช่น ฮีบรู).

*เคล็ดลับ:* เมื่อคุณแสดงผลลัพธ์ OCR ใน UI, ตรวจสอบให้แน่ใจว่าคอนโทรลสนับสนุนการเรนเดอร์ RTL; มิฉะนั้นข้อความจะดูสับสน.

---

## แปลงภาพเป็นข้อความ – ทำงานกับฮินดี

เปลี่ยนหัวข้อ, เรามา **convert image to text** สำหรับใบเสร็จฮินดี. กระบวนการคล้ายกับการทำงานของอาหรับ, แต่เราจะใช้ `Language.Hindi` แทน.

```csharp
        // 5️⃣ Load the Hindi (Devanagari) image
        var hindiImage = OcrImage.FromFile(@"C:\OCRSamples\hindi_receipt.png");

        // 6️⃣ Recognize Hindi text – Language.Hindi tells the engine to use Devanagari models
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);

        // 7️⃣ Output the Hindi OCR result
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**ทำไมเราจึงใช้ instance `ocrEngine` เดียวกัน:**  
การสร้างเอนจินใหม่สำหรับแต่ละภาษา จะทำให้ใช้หน่วยความจำและเวลาเริ่มต้นมากเกินไป. เอนจินของ Aspose ปลอดภัยต่อเธรดสำหรับการเรียกแบบต่อเนื่อง, ดังนั้นการใช้ซ้ำจึงมีประสิทธิภาพและสะอาด.

**ตัวอย่างผลลัพธ์คอนโซล** (อีกครั้ง, ขึ้นอยู่กับภาพของคุณ):

```
Hindi: कुल राशि: ₹ 1,250.00
```

หากข้อความฮินดีแสดงเป็นอักขระละตินที่อ่านไม่ออก, คุณอาจลืมระบุ enum ของภาษา หรือความละเอียดของภาพต่ำเกินไป (<300 dpi). การขยายภาพหรือใช้ฟิลเตอร์ไบนารีอย่างง่ายสามารถเพิ่มความแม่นยำได้อย่างมาก.

---

## จดจำข้อความฮินดี – ปัญหาทั่วไปและกรณีขอบ

แม้จะตั้งค่า language flag ถูกต้องแล้ว, ยังมีปัญหาเล็กน้อยที่อาจทำให้คุณติดขัด:

| ปัญหา | อาการ | วิธีแก้ |
|-------|---------|-----|
| คอนทราสต์ต่ำ |หลายอักขระกลายเป็น “?” หรือหายไป |ทำการเตรียมล่วงหน้าด้วย `OcrImage.AdjustContrast(1.5)` |
| ภาพเอียง |ข้อความหมุน, OCR คืนค่าสตริงว่าง |เรียก `ocrEngine.PreprocessImage(arabicImage, ImageProcessingOptions.Rotate)` |
| หลายภาษา |บรรทัดอาหรับตามด้วยตัวเลขภาษาอังกฤษ |ทำสองรอบ: ครั้งแรกใช้ `Language.Arabic`, จากนั้นใช้ `Language.English` บนภาพเดียวกันและต่อผลลัพธ์ |
| ไฟล์ขนาดใหญ่ |การจดจำช้า หรือเกิดข้อผิดพลาด out‑of‑memory |ลดขนาดลงสูงสุด 2000 px ความกว้างด้วย `OcrImage.Resize(2000, 0)` |

เคล็ดลับเหล่านี้ช่วยให้คุณ **extract text from image** ไฟล์ที่ไม่ได้สแกนอย่างสมบูรณ์, ซึ่งเป็นเรื่องทั่วไปในโครงการจริง.

---

## รวมทุกอย่างเข้าด้วยกัน – ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกโดยตรงไปยังโปรเจกต์คอนโซลใหม่. ไม่มีการพึ่งพาที่ซ่อนอยู่, ไม่มีการกำหนดค่าเพิ่มเติม—เพียง C# แท้.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // Initialize the OCR engine (CPU‑based)
        var ocrEngine = new OcrEngine();

        // -------------------- Arabic --------------------
        var arabicPath = @"C:\OCRSamples\arabic_sign.jpg";
        var arabicImage = OcrImage.FromFile(arabicPath);
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);
        System.Console.WriteLine("Arabic: " + arabicResult.Text);

        // -------------------- Hindi --------------------
        var hindiPath = @"C:\OCRSamples\hindi_receipt.png";
        var hindiImage = OcrImage.FromFile(hindiPath);
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**การรันโปรแกรม** จะพิมพ์สตริงภาษาอาหรับและฮินดีทั้งสองไปยังคอนโซล, ยืนยันว่าคุณได้ **recognize arabic text** และ **recognize hindi text** สำเร็จในรอบเดียว.  

---

## สรุป

ตอนนี้คุณมีคำตอบครบวงจรสำหรับคำถาม **how to ocr arabic** พร้อมกับการจัดการฮินดี. ด้วยการสร้าง `OcrEngine` ตัวเดียว, โหลดแต่ละภาพ, และส่ง `Language` enum ที่เหมาะสม, คุณสามารถ **extract text from image**, **convert image to text**, และ **recognize arabic text** รวมถึง **recognize hindi text** ได้โดยไม่ต้องใช้ไลบรารีเพิ่มเติม.  

จากนี้คุณอาจสำรวจต่อ:

* **Batch processing** – วนลูปผ่านโฟลเดอร์ของภาพและเก็บผลลัพธ์ในฐานข้อมูล.  
* **Post‑processing** – ใช้ regular expressions เพื่อลบสัญลักษณ์สกุลเงินในใบเสร็จฮินดี.  
* **Hybrid language detection** – ส่ง bitmap ดิบไปยังโมเดลตรวจจับภาษา ก่อนเลือก enum.  

ลองทำดู, ปรับขั้นตอนการเตรียมล่วงหน้า, แล้วคุณจะเห็นความแม่นยำของ OCR เพิ่มขึ้นอย่างรวดเร็ว. หากคุณเจอปัญหาใดๆ, ส่ง

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
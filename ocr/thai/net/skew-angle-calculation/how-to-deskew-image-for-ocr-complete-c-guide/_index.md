---
category: general
date: 2026-01-06
description: เรียนรู้วิธีการแก้ไขการเอียงของภาพ, กำจัดสัญญาณรบกวน, และสกัดข้อความด้วย
  Aspose OCR. คู่มือแบบขั้นตอนยังแสดงวิธีโหลดภาพสำหรับ OCR.
draft: false
keywords:
- how to deskew image
- how to extract text
- how to remove noise
- recognize text from image
- load image for ocr
language: th
og_description: เรียนรู้วิธีการแก้ไขการเอียงของภาพ, กำจัดสัญญาณรบกวน, และสกัดข้อความด้วย
  Aspose OCR. คู่มือแบบทีละขั้นตอนยังแสดงวิธีการโหลดภาพสำหรับ OCR.
og_title: วิธีแก้ไขการเอียงของภาพสำหรับ OCR – คู่มือ C# ฉบับสมบูรณ์
tags:
- OCR
- C#
- Image Processing
title: วิธีแก้ไขการเอียงของภาพสำหรับ OCR – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/skew-angle-calculation/how-to-deskew-image-for-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพสำหรับ OCR – คู่มือ C# ฉบับสมบูรณ์

เคยสงสัย **วิธีแก้ไขการเอียงของภาพ** ก่อนนำไปให้เครื่อง OCR หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่มักเจออุปสรรคเดียวกันเมื่อภาพสแกนมีการเอียงเล็กน้อย มีสัญญาณรบกวน หรืออ่านยาก ข่าวดีคือด้วย Aspose OCR คุณสามารถทำให้ภาพตรงขึ้น ทำความสะอาด แล้วดึงข้อความออกได้ในไม่กี่บรรทัดของ C#  

ในบทเรียนนี้เราจะอธิบาย **วิธีดึงข้อความ**, **วิธีลบสัญญาณรบกวน**, และแน่นอน **วิธีแก้ไขการเอียงของภาพ** เพื่อให้ผลลัพธ์ของ OCR แม่นยำที่สุด ตอนจบคุณจะรู้ **วิธีโหลดภาพสำหรับ OCR** และได้สตริงที่สะอาดพร้อมค้นหาใช้ในแอปของคุณ

---

## สิ่งที่คุณต้องเตรียม

- **Aspose.OCR for .NET** (เวอร์ชัน 23.12 หรือใหม่กว่า) ชื่อแพคเกจ NuGet คือ `Aspose.OCR`
- .NET 6+ (runtime ใดก็ได้ที่ทันสมัย)
- ตัวอย่างภาพที่เอียงหรือมีจุดรบกวน เช่น `skewed_photo.jpg`
- Visual Studio, Rider หรือเครื่องมือแก้ไขที่คุณชอบ

ไม่มีไลบรารีเนทีฟเพิ่มเติม—Aspose ดูแลทุกอย่างภายในกระบวนการ

---

## ขั้นตอนที่ 1 – ตั้งค่า OCR Engine (จดจำข้อความจากภาพ)

ก่อนที่เราจะ **โหลดภาพสำหรับ OCR** เราต้องมีอินสแตนซ์ของเอนจินและกำหนดภาษาที่ต้องการอ่าน

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine and tell it we’re reading English text.
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

**ทำไมเรื่องนี้สำคัญ:** `OcrEngine` คือหัวใจของกระบวนการ การตั้งค่า `Language` ตั้งแต่ต้นทำให้ الگوریتمการจดจำใช้ชุดอักขระที่ถูกต้อง ซึ่งช่วยเพิ่มความแม่นยำอย่างมาก

---

## ขั้นตอนที่ 2 – โหลดภาพของคุณ (โหลดภาพสำหรับ OCR)

ตอนนี้เราชี้เอนจินไปที่ไฟล์บนดิสก์ นี่คือจุดที่หลายบทเรียนหยุดไว้ แต่เราจะพูดถึงข้อผิดพลาดที่พบบ่อยด้วย

```csharp
// Load the image you want to process.
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");
```

> **เคล็ดลับ:** ใช้เส้นทางแบบ absolute ระหว่างการทดสอบ แล้วเปลี่ยนเป็นเส้นทางแบบ relative หรือ embedded resource สำหรับการใช้งานจริง นอกจากนี้ต้องแน่ใจว่าภาพอยู่ในฟอร์แมตที่รองรับ (JPEG, PNG, BMP, TIFF) หากเจอข้อผิดพลาด “Unsupported format” ให้ตรวจสอบนามสกุลไฟล์และ MIME type อีกครั้ง

---

## ขั้นตอนที่ 3 – การเตรียมล่วงหน้า: แก้เอียงและลบจุดรบกวน (วิธีแก้ไขการเอียงของภาพ & วิธีลบสัญญาณรบกวน)

เอกสารที่เอียงเป็นปัญหา OCR คลาสสิก Aspose มี `DeskewFilter` ที่ตรวจจับการหมุนอัตโนมัติได้ถึงมุมที่กำหนดได้ คู่กับ `DespeckleFilter` เพื่อทำความสะอาดสัญญาณ “เกลือและพริกไทย”

```csharp
// 1️⃣ Deskew – correct rotation up to 15° (adjust as needed)
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

// 2️⃣ Despeckle – reduce noise; Strength 1‑5 (3 is moderate)
ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });
```

### วิธีทำงานของ Deskew Filter
ฟิลเตอร์สแกนภาพเพื่อหาบรรทัดข้อความหลัก คำนวณมุมเอียง แล้วหมุนบิตแมพตามนั้น หากภาพอยู่ระดับแล้ว ฟิลเตอร์จะไม่ทำอะไร—จึงปลอดภัยที่จะใส่ไว้ใน pipeline ใดก็ได้

### วิธีที่ Despeckle Filter ช่วย
สัญญาณรบกวนมักปรากฏเป็นพิกเซลสีดำหรือสีขาวแยกเดี่ยว อัลกอริทึม despeckle ใช้ median filter ที่รักษาขอบ (เช่น เส้นของอักขระ) ขณะทำให้จุดรบกวนหายไป ความแรงมากเกินไปอาจทำให้รายละเอียดละเอียดเบลอได้ ดังนั้นเริ่มต้นที่ `Strength = 3` แล้วปรับตามวัสดุต้นฉบับของคุณ

> **หมายเหตุ:** หากภาพของคุณมีการหมุนมาก (>15°) ให้เพิ่มค่า `MaxAngle` หากสแกนภาพกลับหัวอาจต้องทำการหมุนด้วยตนเองก่อนใช้ Deskew Filter

---

## ขั้นตอนที่ 4 – เรียกใช้การจดจำ (จดจำข้อความจากภาพ)

เมื่อเตรียมล่วงหน้าเสร็จ เราก็สั่งให้เอนจินอ่านข้อความ

```csharp
if (ocrEngine.Recognize())
{
    // The recognized text is now stored in ocrEngine.Text
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(ocrEngine.Text);
}
else
{
    Console.WriteLine("Recognition failed – check the image quality.");
}
```

### สิ่งที่เกิดขึ้นภายใน?
1. **Binarization:** แปลงภาพเป็นสีขาว‑ดำ เพิ่มคอนทราสต์
2. **Segmentation:** แบ่งบิตแมพเป็นบรรทัด, คำ, และอักขระ
3. **Classification:** เปรียบเทียบอักขระกับโมเดลที่ฝึกไว้ (อักษรอังกฤษ, ตัวเลข, เครื่องหมายวรรคตอน)
4. **Post‑processing:** ใช้กฎภาษา (เช่น ตรวจสอบการสะกด) เพื่อปรับปรุงความอ่านง่าย

เพราะเรา **ได้แก้เอียงภาพ** และ **ลบสัญญาณรบกวน** แล้ว แต่ละขั้นตอนจึงได้รับข้อมูลที่สะอาดขึ้น ทำให้การจดจำผิดพลาดน้อยลง

---

## ขั้นตอนที่ 5 – ตรวจสอบและทำความสะอาดผลลัพธ์ (วิธีดึงข้อความอย่างมีประสิทธิภาพ)

สตริงดิบอาจมีการขึ้นบรรทัดใหม่หรือช่องว่างเกินมา การทำความสะอาดอย่างรวดเร็วทำให้ข้อมูลพร้อมสำหรับการประมวลผลต่อไป

```csharp
string raw = ocrEngine.Text;

// Trim leading/trailing whitespace and collapse multiple newlines.
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(raw, @"\s+", " ")
    .Trim();

Console.WriteLine("\n=== Cleaned Text ===");
Console.WriteLine(cleaned);
```

**ทำไมต้องทำความสะอาด?** ไลบรารี OCR ส่วนใหญ่จะรักษาเลย์เอาต์เดิมไว้ ซึ่งดีสำหรับ PDF แต่ทำให้ข้อความธรรมดาเป็นเสียงรบกวน การทำให้ช่องว่างเป็นมาตรฐานช่วยให้คุณเก็บผลลัพธ์ในฐานข้อมูลหรือส่งต่อไปยังดัชนีการค้นหาได้โดยไม่ต้องทำงานเพิ่มเติม

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วางทั้งหมดที่เชื่อมทุกขั้นตอนเข้าด้วยกัน บันทึกเป็น `Program.cs` เพิ่มแพคเกจ Aspose.OCR แล้วรัน

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to process
        //    (this demonstrates how to load image for OCR)
        ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");

        // 3️⃣ Add preprocessing filters
        //    - Deskew up to 15° (how to deskew image)
        //    - Despeckle with moderate strength (how to remove noise)
        ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
        ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });

        // 4️⃣ Perform recognition (recognize text from image)
        if (ocrEngine.Recognize())
        {
            // 5️⃣ Output raw and cleaned text (how to extract text)
            Console.WriteLine("=== Raw OCR Output ===");
            Console.WriteLine(ocrEngine.Text);

            string cleaned = System.Text.RegularExpressions.Regex
                .Replace(ocrEngine.Text, @"\s+", " ")
                .Trim();

            Console.WriteLine("\n=== Cleaned OCR Output ===");
            Console.WriteLine(cleaned);
        }
        else
        {
            Console.WriteLine("OCR failed – verify the image path and quality.");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าภาพตัวอย่างมีข้อความ “Hello World”):

```
=== Raw OCR Output ===
Hello World

=== Cleaned OCR Output ===
Hello World
```

หากภาพเอียงมาก คุณจะเห็นผลลัพธ์ดิบมีอักขระแปลกก่อนเพิ่ม `DeskewFilter` หลังจากใช้ฟิลเตอร์แล้วข้อความจะอ่านได้ชัดเจน—ตรงกับเป้าหมายที่เราตั้งไว้

---

## คำถามที่พบบ่อย & กรณีเฉพาะ

| คำถาม | คำตอบ |
|----------|--------|
| *ภาพของฉันหมุนมากกว่า 15° จะทำอย่างไร?* | เพิ่มค่า `MaxAngle` ใน `DeskewFilter` ค่าที่ปลอดภัยถึง 45° แต่มุมสุดโต่งอาจต้องหมุนด้วยตนเองก่อน (`Image.Rotate(angle)`) |
| *OCR ยังพลาดตัวอักษรหลังจาก despeckling* | ลองเพิ่ม `Strength` (4‑5) หรือเพิ่ม `ContrastFilter` ก่อน despeckling |
| *ฉันสามารถประมวลผล PDF โดยตรงได้หรือไม่?* | ได้—ใช้ `PdfDocument` แปลงแต่ละหน้าเป็นภาพ แล้วส่งบิตแมพแต่ละหน้าเข้าสู่ pipeline เดียวกัน |
| *เอนจินนี้ปลอดภัยต่อการทำงานหลายเธรดหรือไม่?* | ควรสร้าง `OcrEngine` แยกสำหรับแต่ละเธรด; คลาสเองไม่ได้รับประกันความปลอดภัยต่อหลายเธรด |
| *จะจัดการกับเอกสารหลายภาษายังไง?* | ตั้งค่า `ocrEngine.Language = OcrLanguage.Multilingual` หรือสลับภาษาตามหน้า |

---

## เคล็ดลับสำหรับ OCR ที่พร้อมใช้งานใน Production

1. **Batch Processing:** วนลูปผ่านโฟลเดอร์ของภาพ ใช้ `OcrEngine` ตัวเดียวซ้ำเพื่อประหยัดค่าโอเวอร์เฮด
2. **Logging:** ตรวจสอบ `ocrEngine.LastError` เมื่อ `Recognize()` คืนค่า false; มักบ่งบอกฟอร์แมตที่ไม่รองรับหรือไฟล์เสีย
3. **Performance:** ขั้นตอน deskew ใช้ CPU มากที่สุด หากมั่นใจว่าภาพอยู่ระดับแล้วสามารถข้ามฟิลเตอร์นี้ได้
4. **Memory Management:** ปล่อย `ImageStream` หลังการใช้ (`ocrEngine.Image.Dispose()`) เพื่อหลีกเลี่ยง memory leak ในบริการที่ทำงานต่อเนื่อง

---

## สรุป

เราได้ครอบคลุม **วิธีแก้ไขการเอียงของภาพ**, **วิธีลบสัญญาณรบกวน**, **วิธีโหลดภาพสำหรับ OCR**, และ **วิธีดึงข้อความ** ด้วย Aspose OCR ใน C# การเตรียมล่วงหน้าด้วย `DeskewFilter` และ `DespeckleFilter` ช่วยเพิ่มโอกาสที่ `Recognize()` จะคืนสตริงที่สะอาดและค้นหาได้  

ตั้งแต่บรรทัดโค้ดแรกจนถึงผลลัพธ์ที่ทำความสะอาดแล้ว ขั้นตอนทั้งหมดง่ายต่อการทำตาม แต่มีพลังพอสำหรับสถานการณ์จริง ไม่ว่าจะเป็นบริการจัดเก็บเอกสาร, แอปสแกนใบเสร็จบนมือถือ, หรือระบบประมวลผลแบบ batch  

พร้อมรับความท้าทายต่อไปหรือยัง? ลองเพิ่มขั้นตอน **การตรวจจับภาษา** หรือทดลอง **พจนานุกรม OCR แบบกำหนดเอง** เพื่อเพิ่มความแม่นยำสำหรับคำศัพท์เฉพาะอุตสาหกรรม ตอนนี้คุณมีพื้นฐานที่มั่นคงแล้วสำหรับการต่อยอดต่อไป  

ขอให้เขียนโค้ดสนุกและภาพของคุณเป็นเส้นตรงเสมอ!  

![ภาพตัวอย่างเอกสารที่แก้ไขแล้วหลังการเอียง](deskewed_example.png "วิธีแก้ไขการเอียงของภาพ")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
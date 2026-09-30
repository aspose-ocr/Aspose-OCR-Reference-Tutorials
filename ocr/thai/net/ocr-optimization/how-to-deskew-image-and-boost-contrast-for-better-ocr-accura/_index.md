---
category: general
date: 2025-12-30
description: วิธีแก้ไขการเอียงของภาพอย่างรวดเร็วและเรียนรู้วิธีเพิ่มความคมชัดขณะสกัดข้อความจากภาพเพื่อปรับปรุงความแม่นยำของ
  OCR.
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: th
og_description: วิธีแก้ไขการเอียงของภาพอย่างรวดเร็วและเรียนรู้วิธีเพิ่มคอนทราสต์ขณะสกัดข้อความจากภาพเพื่อปรับปรุงความแม่นยำของ
  OCR.
og_title: วิธีแก้ไขการเอียงของภาพและเพิ่มคอนทราสต์เพื่อความแม่นยำของ OCR ที่ดียิ่งขึ้น
tags:
- OCR
- C#
- Image Processing
title: วิธีแก้ไขการเอียงของภาพและเพิ่มความคอนทราสต์เพื่อความแม่นยำของ OCR ที่ดียิ่งขึ้น
url: /th/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพและเพิ่มคอนทราสต์เพื่อความแม่นยำของ OCR ที่ดียิ่งขึ้น

เคยสงสัย **วิธีแก้ไขการเอียงของภาพ** ที่ได้จากสแกนเนอร์หรือสมาร์ทโฟนหรือไม่?  
คุณไม่ได้อยู่คนเดียว—นักพัฒนาส่วนใหญ่มักเจอปัญหาเมื่อภาพต้นฉบับเอียงหรือมีสัญญาณรบกวน ทำให้ผลลัพธ์ของ OCR กลายเป็นข้อความที่สับสนกัน  

ข่าวดีคือด้วยเพียงไม่กี่บรรทัดของ C# คุณสามารถทำให้ภาพตรงขึ้น ทำความสะอาดพื้นหลัง และเพิ่มคอนทราสต์ให้เครื่องอ่านข้อความได้อย่างมืออาชีพ ในคู่มือนี้เราจะสาธิตวิธี **ดึงข้อความจากไฟล์ภาพ** และ **จดจำเนื้อหาภาพข้อความ** ด้วย Aspose.OCR พร้อมเน้น **การปรับปรุงความแม่นยำของ OCR** เป็นเป้าหมายหลัก

## สิ่งที่คุณต้องเตรียม

- **.NET 6.0** หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้บน .NET Framework 4.7+)  
- แพคเกจ NuGet **Aspose.OCR** (เวอร์ชัน 23.12 หรือใหม่กว่า) – ติดตั้งด้วยคำสั่ง `dotnet add package Aspose.OCR`  
- ตัวอย่างภาพที่เอียงและมีสัญญาณรบกวน (เช่น `noisy_rotated.jpg`)  
- Visual Studio, VS Code หรือ IDE ใดก็ได้ที่คุณชอบ  

เท่านี้—ไม่ต้องใช้ไลบรารีเนทีฟเพิ่มเติม ไม่ต้องผูกกับ OpenCV ที่หนักหน่วง เพียงโค้ดที่จัดการโดย .NET เท่านั้น

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้า Namespaces

เริ่มต้นด้วยการสร้างแอปคอนโซลใหม่และนำ Namespaces ที่จำเป็นเข้ามาในสโคป ขั้นตอนนี้เป็นพื้นฐานสำหรับทุกอย่างที่ตามมา

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**ทำไมต้องทำเช่นนี้:**  
`Aspose.OCR` ให้คลาส `OcrEngine` ส่วน `Aspose.OCR.Filters` มีฟิลเตอร์การประมวลผลล่วงหน้าอย่าง `DeskewFilter` และ `ContrastBoostFilter` การนำเข้าล่วงหน้าช่วยให้โค้ดดูเป็นระเบียบและบอกคอมไพเลอร์ว่าเราตั้งใจจะใช้อะไร

---

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine และเพิ่ม Deskew Filter

ตอนนี้เราจะทำ **วิธีแก้ไขการเอียงของภาพ** จริง ๆ `DeskewFilter` จะตรวจจับมุมการหมุนโดยอัตโนมัติ (สูงสุดตามที่คุณกำหนด) แล้วหมุนบิตแมพกลับเป็นแนวนอน

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**สิ่งที่เกิดขึ้นเบื้องหลัง:**  
ฟิลเตอร์สแกนภาพเพื่อหาเส้นข้อความแนวนอนที่ยาวที่สุด ประเมินมุมเอียง แล้วทำการหมุนย้อนกลับ การจำกัด `MaxAngle` ไว้ที่ 15° จะช่วยหลีกเลี่ยงการแก้ไขเกินความจำเป็นสำหรับภาพที่อยู่ในแนวตรงแล้ว

> **เคล็ดลับ:** หากภาพต้นทางอาจกลับหัว ให้ตั้งค่า `MaxAngle` เป็น 180°—ฟิลเตอร์ยังคงหาทิศทางที่ถูกต้องได้

---

## ขั้นตอนที่ 3: ลดสัญญาณรบกวนด้วย Denoise Filter

การสแกนที่มีสัญญาณรบกวนอาจทำให้ OCR สับสน การเพิ่ม `DenoiseFilter` จะทำให้จุดรบกวนหายไปโดยไม่ทำลายรายละเอียดสำคัญ

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**ทำไมต้องใช้:**  
สัญญาณรบกวนสร้างขอบเท็จที่อัลกอริทึม OCR อาจตีความเป็นอักขระ ค่า `Strength` ที่ 0.7 ถือเป็นจุดที่เหมาะสมสำหรับเอกสารสแกนส่วนใหญ่; คุณสามารถปรับเพิ่มหรือลดตามความสะอาดของภาพ

---

## ขั้นตอนที่ 4: เพิ่มคอนทราสต์ – “วิธีเพิ่มคอนทราสต์” ในการทำงาน

นี่คือส่วนที่ตอบคีย์เวิร์ดรอง **วิธีเพิ่มคอนทราสต์** `ContrastBoostFilter` จะขยายความแตกต่างระหว่างข้อความสีดำกับพื้นหลังสีอ่อน ทำให้ตัวอักษรเด่นชัดขึ้น

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**เหตุผล:**  
คอนทราสต์ที่สูงช่วยลดโอกาสที่เส้นอักษรบาง ๆ จะพลาด การตั้งค่า `Level` ที่ 1.3 ทำงานได้ดีสำหรับเอกสารสีดำบนพื้นขาวทั่วไป; สำหรับภาพสีอาจต้องเพิ่มเป็น 1.5 หรือมากกว่า

---

## ขั้นตอนที่ 5: รัน OCR และดึงข้อความออกมา

เมื่อภาพผ่านการเตรียมแล้ว เราจะ **ดึงข้อความจากภาพ** ด้วยเมธอด `Recognize` ผลลัพธ์จะเป็นอ็อบเจ็กต์ `OcrResult` ที่บรรจุสตริงดิบและคะแนนความเชื่อมั่น

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**สิ่งที่คุณจะได้:**  
`ocrResult.Text` จะเก็บข้อความแบบ plain‑text ของทุกอย่างที่เครื่องอ่านได้ หากต้องการความเชื่อมั่นระดับคำ สามารถสำรวจ `ocrResult.Regions`—แต่ละ region มีคุณสมบัติ `Confidence`

---

## ตัวอย่างเต็มที่พร้อมคัดลอก‑วาง

ด้านล่างเป็นโปรแกรมครบชุดที่คุณสามารถวางลงใน `Program.cs` ได้ อย่าลืมตั้งค่าเส้นทางภาพให้ชี้ไปยังไฟล์จริงบนเครื่องของคุณ

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

หากผลลัพธ์ดูเป็นอักขระผสม ให้ตรวจสอบคุณภาพของภาพ ปรับ `Strength` หรือ `Level` หรือเพิ่ม `MaxAngle` เพื่อทำการแก้ไขเอียงอย่างเข้มข้นขึ้น

---

## คำถามที่พบบ่อยและกรณีขอบ

### หากภาพกลับหัวจะทำอย่างไร?

ตั้งค่า `MaxAngle = 180` ใน `DeskewFilter` ฟิลเตอร์จะตรวจจับการหมุน 180° แล้วพลิกภาพให้ถูกต้อง

### เอกสารของฉันเป็นสี (เช่น แบบฟอร์มสแกนที่มีไฮไลท์สีน้ำเงิน)

ลองเพิ่ม `ColorFilter` ก่อนทำคอนทราสต์ หรือแปลงภาพเป็นระดับสีเทาด้วยตนเอง:

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### ต้องประมวลผลไฟล์หลายไฟล์เป็นชุด

ห่อหุ้มตรรกะ OCR ไว้ในลูป `foreach` ที่วนผ่านโฟลเดอร์:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### จะตรวจสอบความเชื่อมั่นของ OCR ได้อย่างไร?

ตรวจสอบ `ocrResult.Regions`:

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

ค่าความเชื่อมั่นที่สูง (ใกล้ 100%) มักบ่งบอกว่าขั้นตอนการเตรียมภาพสำเร็จ

---

## เคล็ดลับเพื่อเพิ่มความแม่นยำของ OCR

| เคล็ดลับ | ทำไมจึงช่วย |
|-----|--------------|
| **ใช้รูปแบบภาพที่ไม่เสียคุณภาพ** (PNG, TIFF) | การบีบอัด JPEG อาจทำให้ขอบเบลอและลดประสิทธิภาพการจดจำ |
| **รักษา DPI ที่ 300+** | พิกเซลต่ออักขระมากขึ้นทำให้เอ็นจิ้นมีข้อมูลมากพอ |
| **ตัดขอบที่ไม่เกี่ยวข้องออก** | ลดสัญญาณรบกวนและเร่งการประมวลผล |
| **ใช้การแปลงเป็นไบนารี (ขาว‑ดำ)** หลังเพิ่มคอนทราสต์สำหรับเอกสารข้อความล้วน | ทำให้ภาพเหลือเพียงสองสี ซึ่ง OCR ส่วนใหญ่ชอบ |
| **ทดสอบกับตัวอย่างขนาดเล็กก่อน** | ช่วยให้คุณปรับ `Strength` และ `Level` อย่างแม่นยำก่อนขยายการใช้งาน |

---

## สรุป

เราได้อธิบาย **วิธีแก้ไขการเอียงของภาพ**, **วิธีเพิ่มคอนทราสต์**, และขั้นตอนเต็มเพื่อ **ดึงข้อความจากภาพ** ด้วย Aspose.OCR โดยการเชื่อมต่อ `DeskewFilter`, `DenoiseFilter`, และ `ContrastBoostFilter` ก่อนเรียก `Recognize` คุณจะเห็นการปรับปรุงที่ชัดเจนใน **การปรับปรุงความแม่นยำของ OCR** สำหรับการสแกนในโลกจริงหลายกรณี  

ลองรันโค้ด ปรับพารามิเตอร์ของฟิลเตอร์ให้เข้ากับลักษณะเอกสารของคุณ แล้วคุณจะได้ข้อความที่สะอาดจากภาพที่ยุ่งยากที่สุดในเวลาอันสั้น หากต้องการต่อยอด สามารถเพิ่มพจนานุกรมตามภาษา หรือส่งผลลัพธ์ไปยังตัวตรวจสอบการสะกดเพื่อทำ post‑processing  

ขอให้เขียนโค้ดสนุกและ OCR ของคุณออกมาคมชัดเสมอ! 

--- 

![ตัวอย่างวิธีแก้ไขการเอียงของภาพ](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-18
description: วิธีแก้การเอียงของภาพและลดสัญญาณรบกวนในไฟล์สแกน เรียนรู้การโหลดภาพจากไฟล์
  สกัดข้อความจากไฟล์ TIFF และจดจำข้อความจากภาพด้วย Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: th
og_description: วิธีแก้ไขการเอียงของภาพอย่างรวดเร็วด้วย Aspose OCR คู่มือนี้จะแสดงวิธีลดสัญญาณรบกวน
  โหลดภาพจากไฟล์ และดึงข้อความจากไฟล์ TIFF ด้วย C#
og_title: วิธีแก้การเอียงของภาพ – คอร์ส OCR ด้วย C# อย่างเต็มรูปแบบ
tags:
- OCR
- C#
- Image Processing
title: วิธีปรับแนวภาพและทำความสะอาดสแกน – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพ – คู่มือ OCR ด้วย C# เต็มรูปแบบ

เคยสงสัย **วิธีแก้ไขการเอียงของภาพ** ที่ดูเหมือนถูกรับจากสแกนเนอร์ที่สั่นไหวหรือไม่? คุณไม่ได้อยู่คนเดียว นักพัฒนาส่วนใหญ่เจอปัญหานี้เมื่อต้นฉบับ TIFF มีการเอียงเล็กน้อยและผลลัพธ์ OCR กลายเป็นความยุ่งเหยิง ข่าวดีคือ ด้วยเพียงไม่กี่บรรทัดของ C# คุณสามารถทำให้ภาพตรงขึ้น กำจัดพื้นหลังที่เป็นเม็ดฝุ่น และดึงข้อความที่ค้นหาได้อย่างสะอาดจากไฟล์

ในคู่มือนี้เราจะเดินผ่าน **วิธีลดสัญญาณรบกวน**, **การโหลดภาพจากไฟล์**, และสุดท้าย **การจดจำข้อความจากภาพ** ด้วย Aspose OCR. เมื่อจบคุณจะสามารถ **ดึงข้อความจาก tiff** ได้โดยไม่ต้องลำบาก

> **เคล็ดลับ:** หากคุณใช้ Aspose OCR อยู่แล้วในโปรเจกต์อื่น คุณสามารถเพิ่มฟิลเตอร์เหล่านี้ได้โดยไม่ต้องกังวลเรื่องลิขสิทธิ์เพิ่มเติม

---

## สิ่งที่คุณต้องมี

- .NET 6 หรือใหม่กว่า (โค้ดทำงานบน .NET Core ได้เช่นกัน)  
- แพคเกจ NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- ไฟล์ TIFF ที่สแกนแล้วมีการเอียงหรือมีสัญญาณรบกวนเล็กน้อย (เราจะใช้ `skewed_scanned_doc.tif` เป็นตัวอย่าง)  
- โปรแกรมแก้ไขข้อความหรือ IDE (Visual Studio, VS Code, Rider – เลือกตามสะดวก)

ไม่มีไลบรารีเพิ่มเติมที่จำเป็น; ฟิลเตอร์ที่เราจะใช้ถูกรวมไว้ใน Aspose OCR แล้ว

---

## ขั้นตอนที่ 1 – สร้าง OCR Engine (วิธีแก้ไขการเอียงของภาพ)

สิ่งแรกที่คุณทำคือสร้าง `OcrEngine`. คิดว่าเป็นสมองที่จะอ่านอักขระให้คุณในภายหลัง

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

ทำไมต้องสร้าง engine ล่วงหน้า? เพราะมันเป็นจุดเดียวที่คุณสามารถแนบฟิลเตอร์การเตรียมภาพ, แพ็คภาษาต่าง ๆ, และตัวเลือกการส่งออกได้ หากข้ามขั้นตอนนี้และเรียก `OcrEngine.Recognize` ตรง ๆ คุณจะพลาดโอกาสทำความสะอาดภาพก่อน ซึ่งเป็นเหตุผลหลักที่เราต้องการแก้ไขการเอียง

---

## ขั้นตอนที่ 2 – เพิ่มฟิลเตอร์ Deskew และ Noise‑Reduction (วิธีลดสัญญาณรบกวน)

ตอนนี้เราจะแนบฟิลเตอร์สองตัว:

| Filter | สิ่งที่ทำ | ทำไมจึงสำคัญ |
|--------|----------|--------------|
| `AutoDeskewFilter` | ตรวจจับและแก้ไขการหมุน | ทำให้บรรทัดข้อความตรงขึ้นเพื่อให้ OCR engine อ่านได้อย่างถูกต้อง |
| `NoiseReductionFilterV2` | ลบจุดสีและเม็ดฝุ่นพื้นหลัง | พิกเซลที่สะอาดหมายถึงการจดจำที่ผิดพลาดน้อยลง |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

คุณสามารถเปลี่ยน `NoiseReductionFilterV2` เป็นเวอร์ชันเก่าได้ แต่แอลกอริธึม v2 ทำงานได้ดีกับสแกนเนอร์สมัยใหม่ หากเอกสารของคุณเรียบแบนอยู่แล้ว ฟิลเตอร์ deskew จะเพียงแค่ส่งภาพผ่านโดยไม่มีการเปลี่ยนแปลง—ไม่มีผลเสียใด ๆ

---

## ขั้นตอนที่ 3 – โหลดภาพจากไฟล์ (Load Image from File)

Aspose มีตัวช่วย `ImageStream.FromFile` ที่อ่านหลายรูปแบบรวมถึง TIFF, JPEG, PNG, และ BMP นี่คือตัวอย่างการดึงไฟล์เข้าสู่หน่วยความจำ:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

แทนที่ `YOUR_DIRECTORY` ด้วยพาธที่แท้จริงบนเครื่องของคุณ หากใช้พาธแบบ relative ให้แน่ใจว่าไฟล์อยู่ข้าง ๆ executable หรือกำหนด working directory ให้ตรงกัน

---

## ขั้นตอนที่ 4 – รัน OCR บนภาพที่ผ่านการเตรียม (Recognize Text from Image)

เมื่อฟิลเตอร์พร้อมและภาพถูกโหลดแล้ว เราก็ขอให้ Aspose อ่านอักขระ:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

เบื้องหลัง engine จะรันอัลกอริธึม deskew, กำจัดสัญญาณรบกวน, แล้วใช้ recognizer แบบ neural‑network. ผลลัพธ์จะถูกห่อในอ็อบเจ็กต์ `OcrResult` ที่ให้ข้อความดิบ, คะแนนความเชื่อมั่น, และแม้แต่ bounding box หากคุณต้องการใช้ต่อในภายหลัง

---

## ขั้นตอนที่ 5 – แสดงหรือบันทึกข้อความที่ดึงออกมา (Extract Text from TIFF)

สำหรับการสาธิตอย่างรวดเร็ว เราเพียงแค่พิมพ์ข้อความลงคอนโซล แต่คุณก็สามารถบันทึกลงไฟล์, ฐานข้อมูล, หรือส่งต่อไปยัง workflow ถัดไปได้

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่าง, จะต่างกันตามเอกสารของคุณ):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

หากผลลัพธ์ยังมีอักขระผิดเพี้ยน ตรวจสอบว่า TIFF ต้นฉบับมีความละเอียดต่ำเกินไปหรือไม่ (แนะนำขั้นต่ำ 300 dpi) และตรวจสอบว่าตั้งภาษาถูกต้องใน `ocrEngine.Settings.Language`

---

## ตัวอย่างทำงานเต็มรูปแบบ (All Steps in One Place)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่และรันได้ทันที

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

บันทึกไฟล์เป็น `Program.cs`, รัน `dotnet run`, คุณควรเห็นข้อความที่ทำความสะอาดแล้วปรากฏในเทอร์มินัลของคุณ

---

## คำถามที่พบบ่อย & กรณีขอบ

### ถ้า TIFF ของฉันมีหลายหน้า จะทำอย่างไร?
Aspose OCR สามารถประมวลผลภาพหลายหน้าโดยวนลูป `image.GetPages()` (หรือใช้ `image.Pages`). แต่ละหน้าจะคืน `OcrResult` ของตนเอง รวมผลลัพธ์ด้วย `StringBuilder` หากต้องการเป็นสตริงเดียว

### ฟิลเตอร์ deskew ทำงานกับภาพที่หมุนมากได้หรือไม่?
มันรองรับการหมุนประมาณ ±15°. หากเกินกว่านั้นคุณอาจต้องหมุนภาพล่วงหน้าด้วยไลบรารีกราฟิก (เช่น `System.Drawing` หรือ `SkiaSharp`) ก่อนส่งให้ Aspose

### จะเพิ่มความแม่นยำสำหรับข้อความที่ไม่ใช่ภาษาอังกฤษอย่างไร?
ตั้งค่าภาษาอย่างชัดเจน:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

คุณยังสามารถโหลดแพ็คภาษาที่กำหนดเองได้หากแพ็คในตัวไม่ครอบคลุมอักษรของคุณ

### สามารถรันบน Linux ได้หรือไม่?
ทำได้แน่นอน Aspose OCR รองรับหลายแพลตฟอร์ม; เพียงตรวจสอบให้แน่ใจว่ามี native dependencies ที่จำเป็น (ส่วนใหญ่ไม่มีสำหรับเวอร์ชัน .NET แท้) ใช้ `dotnet publish -r linux-x64` เพื่อสร้างไบนารีแบบ self‑contained

---

## โบนัส: แสดงภาพที่ผ่านการ Deskew

หากต้องการดูภาพที่แก้ไขแล้วก่อน OCR คุณสามารถบันทึกกลับไปยังดิสก์ได้:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![ตัวอย่างการแก้ไขการเอียงของภาพ](https://example.com/deskew-demo.png "ตัวอย่างการแก้ไขการเอียงของภาพ")

*ข้อความแทนภาพ:* **ตัวอย่างการแก้ไขการเอียงของภาพ** – แสดงภาพก่อน/หลังของ TIFF ที่หมุนแล้วถูกแก้ไขโดย AutoDeskewFilter

---

## สรุป

เราได้ครอบคลุม **วิธีแก้ไขการเอียงของภาพ**, **วิธีลดสัญญาณรบกวน**, และขั้นตอนทั้งหมดเพื่อ **จดจำข้อความจากภาพ**, **โหลดภาพจากไฟล์**, และ **ดึงข้อความจาก tiff** ด้วย Aspose OCR ใน C#. สิ่งที่ควรจำคือ การเพิ่มฟิลเตอร์เตรียมภาพสองตัวสามารถเปลี่ยนสแกนที่สั่นและเม็ดฝุ่นให้กลายเป็นเอกสารที่คมชัดและค้นหาได้โดยไม่ต้องใช้เครื่องมือภายนอก

พร้อมก้าวต่อไปหรือยัง? ลองสลับ `AutoDeskewFilter` เป็น `AutoRotateFilter` หากเอกสารของคุณกลับหัว, หรือทดลอง `ContrastEnhancementFilter` สำหรับพิมพ์ที่ซีดจาง รูปแบบเดียวกัน—engine → filters → load → recognize—ใช้ได้กับทุกสถานการณ์ของ Aspose OCR, ดังนั้นคุณสามารถนำโครงสร้างนี้ไปใช้กับ PDF, PNG, หรือแม้แต่รูปถ่ายจากกล้องได้

ขอให้เขียนโค้ดสนุกและ OCR ของคุณแม่นยำเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-02-09
description: วิธีใช้ OCR ใน C# เพื่อจดจำข้อความจากภาพ ดึงข้อความออก และแปลงภาพเป็นข้อความด้วย
  Aspose OCR คู่มือเต็มขั้นตอนโดยละเอียด
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: th
og_description: วิธีใช้ OCR ใน C# เพื่อจดจำข้อความจากภาพ ดึงข้อความ และแปลงภาพเป็นข้อความด้วย
  Aspose OCR คู่มือฉบับสมบูรณ์พร้อมโค้ด
og_title: วิธีใช้ OCR ใน C# – แยกข้อความจากภาพ
tags:
- C#
- Aspose OCR
- Image Processing
title: วิธีใช้ OCR ใน C# – แยกข้อความจากรูปภาพ
url: /th/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – การจดจำข้อความจากรูปภาพ

เคยสงสัย **วิธีใช้ OCR** เพื่อแปลงภาพหน้าจอให้เป็นข้อความที่แก้ไขได้หรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาจำนวนมากเจออุปสรรคเมื่อจำเป็นต้อง *จดจำข้อความจากรูปภาพ* แต่ไม่มีตัวอย่างที่ชัดเจนและพร้อมใช้งาน  

ในบทเรียนนี้เราจะพาคุณผ่านกระบวนการทั้งหมด—การโหลดไลเซนส์, การสร้างเอนจิน, การป้อนสตรีมภาพ, และสุดท้ายการดึงข้อความธรรมดาออกมา เมื่อจบคุณจะสามารถ **extract text from image**, **convert image to text**, และแม้แต่เข้าใจรายละเอียดของการ **load image stream** ได้

> **สิ่งที่คุณจะได้รับ:** โปรแกรม C# ที่ทำงานได้เต็มรูปแบบโดยใช้ Aspose.OCR, คำอธิบายของแต่ละขั้นตอน, และเคล็ดลับเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป.

---

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (API ยังทำงานกับ .NET Framework 4.6+ ด้วย)  
- แพคเกจ NuGet ของ Aspose.OCR สำหรับ .NET (`Aspose.OCR`) ที่ติดตั้งแล้ว  
- ไฟล์ไลเซนส์ Aspose OCR ที่ถูกต้อง (`Aspose.OCR.lic`) – เวอร์ชันทดลองใช้งานได้แต่จะมีลายน้ำ  
- รูปภาพ (`sample.jpg`) ที่มีข้อความที่อ่านได้ชัดเจน

> **เคล็ดลับ:** หากคุณใช้ Visual Studio คำสั่งคอนโซล NuGet คือ  
> `Install-Package Aspose.OCR -Version 23.10` (เปลี่ยนเป็นเวอร์ชันล่าสุด).

---

## วิธีใช้ OCR: โหลดไลเซนส์และเริ่มต้นเอนจิน

สิ่งแรกที่คุณต้องทำคือบอก Aspose ว่าคุณมีไลเซนส์ การข้ามขั้นตอนนี้โปรแกรมยังทำงานได้ แต่จะมีลายน้ำปรากฏในผลลัพธ์และคุณจะเสียเวลาในการประมวลผลกับการตรวจสอบโหมดทดลอง

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**ทำไมสิ่งนี้ถึงสำคัญ:** วัตถุ `License` ปิดการแสดงลายน้ำเวอร์ชันทดลองและปลดล็อกคุณสมบัติเต็มชุด ซึ่งรวมถึงโมเดลที่แม่นยำสูงและการสนับสนุนหลายภาษา.  

> **เคล็ดลับระดับมืออาชีพ:** เก็บไฟล์ไลเซนส์ให้อยู่ไกลจากที่เก็บซอร์สโค้ดของคุณ ใช้ตัวแปรสภาพแวดล้อมหรือ vault ที่ปลอดภัยเพื่อใส่เส้นทางในเวลารัน

---

## ขั้นตอนที่ 2 – โหลด Image Stream (และทำไมมันดีกว่าการใช้ไฟล์พาธ)

เมื่อคุณ *load image stream* แทนการส่งพาธไฟล์ดิบ คุณจะได้ความยืดหยุ่น: ภาพสามารถมาจากฐานข้อมูล, คำขอเว็บ, หรืออาร์เรย์ไบต์ในหน่วยความจำ.  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**คำอธิบาย:** `ImageStream` ทำหน้าที่เป็นนามธรรมของแหล่งข้อมูลพื้นฐาน ทำให้ OCR engine ประมวลผลทุกอย่างอย่างสม่ำเสมอ หากคุณเปลี่ยนไปใช้ bucket ของคลาวด์ในภายหลัง คุณเพียงเปลี่ยนวิธีสร้าง `ImageStream` เท่านั้น; ส่วนอื่นของโค้ดยังคงเหมือนเดิม

---

## ขั้นตอนที่ 3 – Recognize Text from Image

ต่อไปคือหัวใจของเรื่อง: **recognize text from image** เมธอด `OcrEngine.Recognize` จะรันโมเดลเครือข่ายประสาทเทียมที่มาพร้อมกับ Aspose และคืนค่าอ็อบเจกต์ `OcrResult` ที่มีคุณสมบัติต่าง ๆ ที่เป็นประโยชน์

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**สิ่งที่อยู่ใน `OcrResult`?**  
- `PlainText` – สตริงเดียวที่รวมอักขระที่ตรวจจับทั้งหมด  
- `Words` – คอลเลกชันของอ็อบเจกต์คำพร้อมกล่องขอบเขต (มีประโยชน์สำหรับการไฮไลท์)  
- `Lines` – การจัดกลุ่มระดับบรรทัด, สะดวกสำหรับการรักษาการแบ่งย่อหน้า  

หากคุณต้องการเพียงข้อความดิบ `PlainText` เป็นทางที่เร็วที่สุด สำหรับสถานการณ์ที่ซับซ้อนกว่า (เช่น การวางผลลัพธ์บนภาพต้นฉบับ) ให้สำรวจ `Words` และ `Lines`.

---

## ขั้นตอนที่ 4 – แสดงหรือบันทึกข้อความที่สกัดออกมา

สุดท้าย เราจะพิมพ์ข้อความที่จดจำได้ออกไปยังคอนโซล ในแอปจริงคุณอาจบันทึกลงฐานข้อมูล, ไฟล์, หรือส่งผ่าน API

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**ผลลัพธ์ที่คาดหวัง:**  
หาก `sample.jpg` มีประโยค *“Hello World!”* คุณจะเห็น:

```
=== OCR Output ===
Hello World!
==================
```

เมื่อใช้ไลเซนส์ทดลอง ผลลัพธ์จะมีลายน้ำ “Aspose OCR Demo” เล็ก ๆ ปรากฏที่ส่วนท้ายของข้อความ หากใช้ไลเซนส์เต็ม ลายน้ำจะหายไปอย่างสมบูรณ์

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมด พร้อมคอมไพล์แล้ว แทนที่พาธด้วยตำแหน่งของคุณเองและพร้อมใช้งาน

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **จำไว้:** โค้ดด้านบน **extracts text from image** และ **converts image to text** ในหนึ่งการเรียกใช้ ไม่มีลูปเพิ่มเติม ไม่มีการจัดการพิกเซลด้วยตนเอง—Aspose ทำงานหนักให้

---

## คำถามทั่วไป & กรณีขอบ

### ถ้าภาพของฉันเบลอหรือคอนทราสต์ต่ำ?

Aspose OCR มีตัวเลือกการเตรียมข้อมูลล่วงหน้า (เช่น `ocrEngine.ImagePreprocessor`). คุณสามารถเปิดใช้งานการทำไบนารีหรือการแก้ไขการเอียงก่อนการจดจำได้:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### ฉันจะจัดการหลายภาษาอย่างไร?

ตั้งค่าคุณสมบัติ `Language` บนเอนจิน:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

เอนจินจะพยายามตรวจจับทั้งสองภาษาโดยอัตโนมัติ

### ฉันสามารถประมวลผล PDF แทน JPEG ได้หรือไม่?

ได้—Aspose OCR สามารถอ่าน PDF โดยตรงได้ แต่คุณต้องใช้ไลบรารี Aspose.PDF เพื่อแยกแต่ละหน้าเป็นภาพก่อน แล้วจึงป้อนสตรีมภาพเข้าสู่ OCR engine

### แล้วกรณีต้องประมวลผลเป็นชุดใหญ่ล่ะ?

ใส่ตรรกะการจดจำไว้ในลูปและใช้ตัวอย่าง `OcrEngine` เดียวกันซ้ำ การสร้างเอนจินใหม่ต่อภาพจะเพิ่มภาระที่ไม่จำเป็น

---

## เคล็ดลับระดับมืออาชีพสำหรับ OCR ที่พร้อมใช้งานใน Production

- **Cache the license object**: โหลดไลเซนส์เพียงครั้งเดียวเมื่อแอปเริ่มต้น ไม่ต้องโหลดใหม่ต่อคำขอ  
- **Reuse `OcrEngine`**: เอนจินเก็บบัฟเฟอร์ภายใน การใช้ซ้ำช่วยลดภาระ GC  
- **Limit image size**: ภาพขนาดใหญ่มาก (>5 MP) จะเพิ่มเวลาประมวลผลอย่างมาก ลดขนาดลงเป็น 150‑300 DPI หากไม่ต้องการความละเอียดสูง  
- **Validate output**: OCR ไม่สมบูรณ์แบบ; ทำการตรวจสอบความเชื่อมั่นอย่างง่าย (`ocrResult.Words.Average(w => w.Confidence)`) และทำเครื่องหมายผลลัพธ์ที่ความเชื่อมั่นต่ำเพื่อการตรวจสอบด้วยมือ  
- **Thread safety**: `OcrEngine` ไม่ปลอดภัยต่อหลายเธรด สร้างอินสแตนซ์แยกต่อเธรดหรือใช้แพทเทิร์นพูล

---

## สรุป

เราได้อธิบาย **how to use OCR** ใน C# ตั้งแต่การโหลดไลเซนส์จนถึงการสกัดข้อความที่สะอาดและค้นหาได้ ด้วยการทำตามขั้นตอนข้างต้นคุณสามารถ **recognize text from image**, **extract text from image**, และแปลงภาพเป็นข้อความได้อย่างง่ายดาย พร้อมกับเชี่ยวชาญรูปแบบ **load image stream** ที่ทำให้โค้ดของคุณยืดหยุ่นต่อแหล่งข้อมูลในอนาคต  

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองเพิ่มการครอปส่วนที่สนใจ, ผสานกับ Azure Blob storage, หรือส่งผลลัพธ์ OCR ไปยัง pipeline การประมวลผลภาษาธรรมชาติ ไม่จำกัดอะไรเลย และตอนนี้คุณมีพื้นฐานที่มั่นคงเพื่อสร้างต่อ

---

![แผนภาพแสดงกระบวนการ OCR: โหลดไลเซนส์ → สร้างเอนจิน → โหลด image stream → จดจำ → แสดงข้อความผลลัพธ์](image-placeholder.png "วิธีใช้ OCR เพื่อจดจำข้อความจากรูปภาพ")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
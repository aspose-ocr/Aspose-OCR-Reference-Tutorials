---
category: general
date: 2026-02-27
description: วิธีเปิดใช้งาน OCR ใน C# เพื่อแปลง PDF เป็นข้อความ . เรียนรู้วิธีดึงข้อความจาก
  PDF หลายภาษาโดยใช้ Aspose OCR.
draft: false
keywords:
- how to enable ocr
- convert pdf to text
- how to extract text
- how to recognize pdf
- recognize pdf text c#
language: th
og_description: วิธีเปิดใช้งาน OCR ใน C# และแปลง PDF เป็นข้อความ คู่มือขั้นตอนต่อขั้นตอนในการดึงและจดจำข้อความ
  PDF ด้วย Aspose OCR.
og_title: วิธีเปิดใช้งาน OCR ใน C# – แปลง PDF เป็นข้อความ
tags:
- OCR
- C#
- PDF
- Aspose
title: วิธีเปิดใช้งาน OCR ใน C# – แปลง PDF เป็นข้อความได้ง่าย ๆ
url: /th/net/ocr-configuration/how-to-enable-ocr-in-c-convert-pdf-to-text-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน OCR ใน C# – แปลง PDF เป็นข้อความได้ง่าย

วิธีเปิดใช้งาน OCR ใน C# เป็นคำถามที่นักพัฒนาหลายคนถามเมื่อจำเป็นต้องดึงข้อความออกจาก PDF หากคุณเคยมองใบแจ้งหนี้สแกนแล้วคิดว่า *“จะดึงข้อความนั้นออกโดยไม่ต้องพิมพ์ใหม่ทั้งหมดได้อย่างไร?”* คุณมาถูกที่แล้ว ในบทเรียนนี้เราจะพาคุณผ่านโซลูชันที่พร้อมรันครบวงจร ซึ่งไม่เพียงแต่แสดง **วิธีเปิดใช้งาน OCR** แต่ยังสาธิต **วิธีแปลง PDF เป็นข้อความ**, **วิธีดึงข้อความ** จากเอกสารหลายภาษา, และ **วิธีจดจำเนื้อหา PDF** ด้วย C#  

เราจะใช้ไลบรารี Aspose.OCR ซึ่งรองรับหลายสิบภาษาโดยไม่ต้องตั้งค่าเพิ่มเติม ดังนั้นคุณจะไม่ต้องสลับเอ็นจิ้นต่าง ๆ สำหรับอังกฤษ, อาหรับ, ญี่ปุ่น หรือสคริปต์อื่น ๆ ใบสุดท้ายของคู่มือนี้คุณจะมีเมธอดเดียวที่ **จดจำข้อความ PDF ด้วย C#** พิมพ์ผลลัพธ์ลงคอนโซล และสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้

## ข้อกำหนดเบื้องต้น – สิ่งที่ต้องมีก่อนเริ่ม

- .NET 6.0 SDK หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core และ .NET Framework ด้วย)
- Visual Studio 2022 (หรือเครื่องมือแก้ไขอื่นที่คุณชอบ)
- ไลเซนส์หรือทดลองใช้ **Aspose.OCR for .NET** – สามารถรับคีย์ชั่วคราวจากเว็บไซต์ Aspose
- ตัวอย่าง PDF ที่มีหลายภาษา (เราจะเรียกไฟล์นี้ว่า `multilang.pdf`)

หากขาดอย่างใดอย่างหนึ่ง ให้ดาวน์โหลด SDK จากเว็บไซต์ Microsoft แล้วติดตั้งแพ็กเกจ NuGet:

```bash
dotnet add package Aspose.OCR
```

เท่านี้ก็พร้อมแล้ว เริ่มกันเลย

## วิธีเปิดใช้งาน OCR ใน C# – การตั้งค่าและกำหนดค่า

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ของ OCR engine และบอกให้มันรู้ว่าคุณคาดหวังภาษาอะไร นี่คือขั้นตอน **วิธีเปิดใช้งาน OCR** ที่เป็นหัวใจของกระบวนการทั้งหมด

```csharp
using Aspose.OCR;
using System;

public class OcrDemo
{
    public static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Enable the languages you need (English, Arabic, Japanese)
        ocrEngine.Language = OcrLanguage.English |
                             OcrLanguage.Arabic |
                             OcrLanguage.Japanese;

        // Step 3: Recognize text from the PDF file
        string recognizedText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

        // Step 4: Output the extracted text
        Console.WriteLine(recognizedText);
    }
}
```

**ทำไมขั้นตอนนี้สำคัญ:** การกำหนดค่า `Language` อย่างชัดเจนช่วยให้ engine จัดสรรโมเดลอักขระที่เหมาะสม ซึ่งเพิ่มความแม่นยำอย่างมาก—โดยเฉพาะสำหรับ PDF ที่มีสคริปต์ผสมกัน หากข้ามขั้นตอนนี้ (หรือปล่อยเป็นค่าเริ่มต้น) engine จะต้องเดาเอง ซึ่งมักทำให้ผลลัพธ์เป็นข้อความเสียหาย

> **เคล็ดลับ:** หากเอกสารของคุณมีเพียงภาษาเดียว ให้จำกัด flag ไว้ที่ภาษานั้น จะทำให้การประมวลผลเร็วขึ้นถึง 30 %

### รูปภาพ – ภาพรวมการเปิดใช้งาน OCR  
![Screenshot of OCR engine configuration showing how to enable OCR in C#](/images/enable-ocr-csharp.png)

*Alt text: Diagram illustrating how to enable OCR in C# using Aspose.OCR.*

## แปลง PDF เป็นข้อความด้วย Aspose OCR

เมื่อ **วิธีเปิดใช้งาน OCR** ถูกตั้งค่าแล้ว เรามาพูดถึงการแปลงจริง ๆ เมธอด `RecognizeFromFile` ทำหน้าที่หลัก: เปิด PDF, รัน OCR engine บนแต่ละหน้า, และคืนสตริงที่มีอักขระที่ดึงออกมาทั้งหมด

### สิ่งที่เกิดขึ้นภายในเมธอด

1. **การเรสเตอร์หน้า** – แต่ละหน้าของ PDF จะถูกแปลงเป็นบิตแมพ เพราะ OCR ทำงานบนภาพ
2. **การเลือกโมเดลภาษา** – ตาม flag ที่ตั้งไว้ก่อนหน้า engine จะเลือกเครือข่ายประสาทที่เหมาะสม
3. **การตรวจจับบรรทัดข้อความ** – engine ค้นหาบรรทัดของข้อความ แม้จะเอียงก็ตาม
4. **การถอดรหัสอักขระ** – สุดท้ายจะแมปรูปแบบพิกเซลเป็นอักขระ Unicode

เนื่องจากเมธอดคืนค่าเป็นสตริงธรรมดา คุณสามารถ **แปลง PDF เป็นข้อความ** ได้ในบรรทัดเดียวของโค้ด หากต้องการการประมวลผลแบบละเอียด (เช่น หน้าต่อหน้า) สามารถเรียก `RecognizeFromStream` ภายในลูปได้

## วิธีดึงข้อความจาก PDF หลายภาษา

สมมติว่า PDF ของคุณมีหัวข้อภาษาอังกฤษ, เนื้อความภาษาอาหรับ, และเชิงอรรถภาษาญี่ปุ่น โค้ดที่แสดงก่อนหน้านี้รองรับสถานการณ์นี้แล้ว แต่คุณอาจอยากรู้ **วิธีดึงข้อความ** เฉพาะส่วนของภาษาใดภาษาเดียว

คุณสามารถกรองผลลัพธ์ด้วยการจัดการสตริงหรือ regex ง่าย ๆ ตัวอย่างต่อไปนี้ดึงเฉพาะส่วนภาษาอังกฤษออกมา:

```csharp
using System.Text.RegularExpressions;

// After recognizing the whole document...
string allText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

// Regex to keep only ASCII characters (roughly English)
string englishOnly = Regex.Replace(allText, @"[^\u0000-\u007F]+", string.Empty);

Console.WriteLine("English extracted:");
Console.WriteLine(englishOnly);
```

**ทำไมต้องกรอง?** ในหลายกระบวนการธุรกิจคุณอาจต้องการส่วนที่เป็นสคริปต์ละตินเพื่อทำดัชนี ส่วนที่เหลือเก็บไว้ที่อื่น ตัวอย่างนี้แสดง **วิธีดึงข้อความ** อย่างมีประสิทธิภาพโดยไม่ต้องทำ OCR ครั้งที่สอง

## วิธีจดจำ PDF – จัดการกับกรณีขอบ

แม้ OCR ที่ดีที่สุดก็อาจเจอปัญหาในบาง PDF ด้านล่างเป็นปัญหาที่พบบ่อยและวิธีแก้

| ปัญหา | อาการ | วิธีแก้ |
|-------|-------|--------|
| การสแกนความละเอียดต่ำ (<150 dpi) | ตัวอักษรหายหรือคำแสดงเป็นอักขระเสีย | เตรียม PDF ล่วงหน้าด้วย `ocrEngine.ImageProcessingOptions.Dpi = 300;` |
| หน้าเอกสารหมุน | ข้อความแสดงแนวนอน | ตั้งค่า `ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;` |
| PDF ป้องกันด้วยรหัสผ่าน | `RecognizeFromFile` โยนข้อยกเว้น | ส่งรหัสผ่านเข้าไป: `ocrEngine.RecognizeFromFile(path, "myPassword");` |
| ไฟล์ขนาดใหญ่ (>100 หน้า) | แครชจากการใช้หน่วยความจำ | ประมวลผลเป็นชิ้นส่วน: โหลด 10 หน้าในแต่ละครั้งแล้วต่อผลลัพธ์ |

การปรับแต่งเหล่านี้ทำให้โซลูชันของคุณ **จดจำ PDF** ได้อย่างเชื่อถือได้ แม้จะมีข้อบกพร่องต่าง ๆ

```csharp
// Example of handling low‑resolution and rotation
ocrEngine.ImageProcessingOptions.Dpi = 300;
ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;
```

## Recognize PDF Text C# – ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมแบบ self‑contained ที่คุณสามารถคัดลอก‑วางลงในแอปคอนโซลได้ มันสาธิต **วิธีเปิดใช้งาน OCR**, **แปลง PDF เป็นข้อความ**, **ดึงส่วนภาษาเฉพาะ**, และ **จัดการกับกรณีขอบทั่วไป**

```csharp
using Aspose.OCR;
using System;
using System.Text.RegularExpressions;

namespace PdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable languages (English, Arabic, Japanese)
            ocrEngine.Language = OcrLanguage.English |
                                 OcrLanguage.Arabic |
                                 OcrLanguage.Japanese;

            // Optional: improve accuracy for low‑res PDFs
            ocrEngine.ImageProcessingOptions.Dpi = 300;
            ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;

            // 3️⃣ Path to your multi‑language PDF
            string pdfPath = @"C:\Docs\multilang.pdf";

            // 4️⃣ Recognize all text
            string fullText = ocrEngine.RecognizeFromFile(pdfPath);
            Console.WriteLine("=== Full extracted text ===");
            Console.WriteLine(fullText);
            Console.WriteLine();

            // 5️⃣ Extract only English (as an example of how to extract text)
            string englishOnly = Regex.Replace(fullText, @"[^\u0000-\u007F]+", string.Empty);
            Console.WriteLine("=== English‑only excerpt ===");
            Console.WriteLine(englishOnly);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัดบางส่วนเพื่อความกระชับ):

```
=== Full extracted text ===
Welcome to our report…
مرحبا بكم في تقريرنا…
ようこそ、私たちのレポートへ…

=== English‑only excerpt ===
Welcome to our report...
```

รันโปรแกรม, ชี้ไปที่ PDF ของคุณ, แล้วคุณจะเห็นคอนโซลพิมพ์ข้อความหลายภาษาทั้งหมดและส่วนภาษาอังกฤษที่กรองแล้ว

## คำถามที่พบบ่อย (และคำตอบสั้น)

- **ทำงานกับ .NET Framework 4.7 ได้หรือไม่?**  
  ใช่. แพ็กเกจ NuGet ของ Aspose.OCR รองรับ .NET Standard 2.0 ซึ่งเข้ากันได้กับ .NET Core และ .NET Framework

- **ถ้าต้อง OCR รูปภาพแทน PDF จะทำอย่างไร?**  
  ใช้ `ocrEngine.RecognizeFromImage("image.png")`. การตั้งค่า flag ภาษาเหมือนเดิม ดังนั้นคุณยังคงทำ **วิธีเปิดใช้งาน OCR** ได้เช่นกัน

- **สามารถบันทึกผลลัพธ์เป็นไฟล์ .txt ได้ไหม?**  
  แน่นอน. แทนที่ `Console.WriteLine(fullText);` ด้วย `File.WriteAllText("output.txt", fullText);`

- **มีวิธีดูคะแนนความเชื่อมั่นหรือไม่?**  
  Aspose.OCR มีอ็อบเจ็กต์ `OcrResult` ที่ให้ค่า `Confidence` ต่อคำ ตรวจสอบเอกสาร API สำหรับ `RecognizeFromFile(..., out OcrResult result)`

## สรุป

เราได้ครอบคลุม **วิธีเปิดใช้งาน OCR** ใน C#, แสดง **วิธีแปลง PDF เป็นข้อความ**, อธิบาย **วิธีดึงข้อความ** จากส่วนภาษาเฉพาะ, และสาธิต **วิธีจดจำ PDF** อย่างเชื่อถือได้ด้วย Aspose OCR โค้ดที่ทำงานได้เต็มรูปแบบด้านบนให้พื้นฐานที่มั่นคงสำหรับการรวม OCR เข้าในแอป .NET ใด ๆ ไม่ว่าจะเป็นระบบจัดการเอกสาร, ตัวประมวลผลใบแจ้งหนี้อัตโนมัติ, หรือดัชนีการค้นหาหลายภาษา  

ขั้นตอนต่อไป? ลองเปลี่ยน flag ภาษาเพื่อรวมจีนหรือเกาหลี, ทดลอง `ImageProcessingOptions` สำหรับสแกนที่มีเสียงรบกวน, หรือส่งข้อความที่ดึงมาเข้าสู่ pipeline การประมวลผลภาษาธรรมชาติ ทั้งหมดยังคงอิงหลักการเดียวกัน: **วิธีเปิดใช้งาน OCR** อย่างถูกต้องตั้งแต่ต้น

ขอให้เขียนโค้ดสนุกและ PDF ของคุณค้นหาได้เสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
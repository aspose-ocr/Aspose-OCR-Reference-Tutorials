---
category: general
date: 2026-02-22
description: วิธีทำ OCR รูปภาพด้วย Aspose OCR – ลบสัญญาณรบกวนของรูปภาพ, เพิ่มความคมชัดของรูปภาพ,
  และดึงข้อความจากรูปภาพใน C# อย่างรวดเร็ว.
draft: false
keywords:
- how to ocr image
- remove image noise
- boost image contrast
- extract text image
- recognize image text
language: th
og_description: เรียนรู้วิธีทำ OCR รูปภาพด้วย Aspose OCR ทำความสะอาดสัญญาณรบกวน เพิ่มคอนทราสต์
  และดึงข้อความจากรูปภาพใน C# พร้อมตัวอย่างที่สมบูรณ์และพร้อมใช้งาน
og_title: วิธี OCR รูปภาพ – เพิ่มคอนทราสต์และลบสัญญาณรบกวน
tags:
- OCR
- C#
- Image Processing
title: 'วิธีทำ OCR รูปภาพ: เพิ่มความคมชัด, กำจัดสัญญาณรบกวน'
url: /th/net/ocr-optimization/how-to-ocr-image-boost-contrast-remove-noise/
---

ตัวอย่างการ OCR รูปภาพ". But need to keep same format: ![how to ocr image example]...{alt="how to ocr image example"} The alt attribute is inside curly braces after image. Should translate both alt text inside brackets and alt attribute? Probably yes. We'll translate alt text and alt attribute.

Also translate headings, paragraphs, bullet points, etc. Keep code block placeholders unchanged.

We must not translate URLs, file paths, variable names, function names. So in code placeholders we keep as is.

Let's produce final content with same structure.

We need to keep the shortcodes at top and bottom unchanged.

Let's translate.

We'll produce Thai translation.

Be careful with markdown links: none present except maybe none. There's no markdown links.

Let's translate.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR รูปภาพ – เพิ่มคอนทราสต์และลบนอยส์ใน C#

เคยสงสัยไหมว่า **วิธีทำ OCR รูปภาพ** ที่เอียง มีนอยส์ หรืออ่านยาก? คุณไม่ได้อยู่คนเดียว ในหลายโครงการจริง—เช่น การสแกนใบเสร็จหรือดิจิไทซ์เอกสารเก่า—ภาพดิบมักไม่สมบูรณ์ ข่าวดีคือ ด้วยบรรทัดโค้ด C# ไม่กี่บรรทัดและ Aspose OCR คุณสามารถ **ลบนอยส์ของภาพ**, **เพิ่มคอนทราสต์ของภาพ**, และสุดท้าย **ดึงข้อความจากภาพ** ได้โดยไม่ต้องลำบาก

ในบทเรียนนี้เราจะเดินผ่านโซลูชันแบบครบวงจร ตั้งแต่การตั้งค่า OCR engine, ทำความสะอาดภาพที่มีนอยส์, จนถึง **การจดจำข้อความในภาพ** เพื่อให้คุณสามารถส่งผลลัพธ์ไปยังที่ต้องการได้ ไม่ต้องอ้างอิงแบบคลุมเครือ มีตัวอย่างโค้ดที่รันได้และเหตุผลของการเลือกแต่ละขั้นตอน

## สิ่งที่คุณต้องมี

- .NET 6+ (หรือ .NET Core 3.1+ – API เหมือนกัน)
- แพคเกจ NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- ตัวอย่างภาพที่เอียงและมีนอยส์ (เช่น `skewed_noisy.jpg`)
- IDE ใดก็ได้ที่คุณชอบ – Visual Studio, Rider, หรือ VS Code ก็ใช้ได้

เท่านี้เอง ถ้าคุณมีทั้งหมดนี้ เราก็พร้อมจะกระโดดเข้าสู่โค้ดได้เลย

![วิธีทำ OCR รูปภาพ ตัวอย่าง](/images/ocr-demo.png){alt="วิธีทำ OCR รูปภาพ ตัวอย่าง"}

## ขั้นตอนที่ 1: เริ่มต้น OCR Engine – วิธีทำ OCR รูปภาพอย่างถูกต้อง  

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ของ `OcrEngine` และบอกให้มันรู้ว่าต้องคาดหวังภาษาอะไร ภาษาอังกฤษเป็นภาษาที่ใช้บ่อยที่สุด แต่ Aspose รองรับหลายสิบภาษาโดยอัตโนมัติ

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Create the OCR engine and set the language to English.
        var ocrEngine = new OcrEngine { Language = Language.English };
```

**ทำไมเรื่องนี้สำคัญ:** Engine ต้องรู้ชุดอักขระ มิฉะนั้นมันจะเสียเวลาเดาและความแม่นยำจะลดลง การตั้งค่าภาษาไว้ล่วงหน้าช่วยลดการใช้หน่วยความจำด้วย เพราะ engine จะโหลดเฉพาะข้อมูลภาษาที่จำเป็นเท่านั้น

## ขั้นตอนที่ 2: โหลดภาพและเริ่มลบนอยส์ของภาพ  

ต่อไปเราจะดึงรูปจากดิสก์ ในหลายกรณีไฟล์เป็น JPEG หรือ PNG ที่มีนอยส์มาก การโหลดเข้าอ็อบเจ็กต์ `Image` ทำให้เรามีตัวจัดการที่สามารถส่งผ่านฟิลเตอร์ได้

```csharp
        // Load the input image (skewed and noisy)
        var inputImage = Image.Load(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

**เคล็ดลับ:** หากภาพของคุณอยู่ในคลาวด์บัคเก็ต คุณสามารถสตรีมโดยตรงด้วย `Image.Load(Stream)` วิธีนี้จะช่วยหลีกเลี่ยงการสร้างไฟล์ชั่วคราว

## ขั้นตอนที่ 3: ใช้สายฟิลเตอร์ – เพิ่มคอนทราสต์ของภาพและทำความสะอาดนอยส์  

Aspose OCR มาพร้อมกับ pipeline ฟิลเตอร์ที่สะดวก ที่นี่เราจะเชื่อมต่อฟิลเตอร์สามตัว:

1. **DeskewFilter** – แก้ไขการเอียงเพื่อให้ข้อความอยู่ในแนวนอน  
2. **DenoiseFilter** – ลบนอยส์โดยไม่ทำให้ตัวอักษรเบลอ  
3. **ContrastFilter** – เพิ่มความแตกต่างระหว่างพื้นหน้าและพื้นหลัง ทำให้ตัวอักษรที่จางขึ้นเด่นชัดขึ้น

```csharp
        // Pre‑process the image with a chain of filters
        var processedImage = inputImage
            .Apply(new DeskewFilter())          // correct rotation
            .Apply(new DenoiseFilter())         // reduce grain
            .Apply(new ContrastFilter(1.5f));   // boost contrast
```

**ทำไมต้องใช้ฟิลเตอร์เหล่านี้?**  
- **Deskew** เป็นสิ่งจำเป็นสำหรับ OCR ที่แม่นยำ; การเอียงเพียงไม่กี่องศาก็อาจทำให้อัตราการจดจำลดลงครึ่งหนึ่ง  
- **Denoise** แก้ปัญหา “ลบนอยส์ของภาพ” ที่มักพบกับการสแกนจากกล้องโทรศัพท์  
- **Contrast** คือสูตรลับสำหรับเอกสารที่คอนทราสต์ต่ำ—เช่น ใบเสร็จที่ซีด  

คุณสามารถปรับค่า `ContrastFilter` factor (ค่าเริ่มต้นคือ `1.0f`) ค่าเหนือ `1.5f` อาจทำให้ภาพสว่างเกินไป ดังนั้นลองทดลองหลายค่า

## ขั้นตอนที่ 4: จดจำข้อความในภาพ – หัวใจของวิธีทำ OCR รูปภาพ  

เมื่อภาพสะอาดแล้ว เราจะส่งให้ OCR engine ทำงาน

```csharp
        // Recognize text from the processed image
        var ocrResult = ocrEngine.Recognize(processedImage);
```

เมธอด `Recognize` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่บรรจุสตริงที่ดึงออกมา, คะแนนความเชื่อมั่น, และแม้กระทั่ง bounding boxes หากคุณต้องการไฮไลท์ข้อความ

**กรณีขอบ:** หากภาพมีหลายภาษา คุณสามารถตั้งค่า `ocrEngine.Language = Language.English | Language.Spanish;` Engine จะพยายามใช้พจนานุกรมทั้งสอง

## ขั้นตอนที่ 5: แสดงผลและตรวจสอบ – ดึงข้อความจากภาพสำหรับแอปของคุณ  

สุดท้าย เราแสดงข้อความบนคอนโซล ในแอปจริงคุณอาจบันทึกลงฐานข้อมูล, ไฟล์, หรือส่งต่อไปยัง pipeline NLP ต่อไป

```csharp
        // Display the extracted text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  

```
=== OCR Result ===
Invoice #12345
Date: 2024‑01‑15
Total: $256.78
Thank you for your business!
```

หากเห็นอักขระแปลก ๆ ให้กลับไปที่ขั้นตอน 3 และปรับพารามิเตอร์ของฟิลเตอร์ บ่อยครั้งการเพิ่มค่า contrast หรือเพิ่ม `SharpenFilter` จะช่วยได้

## คำถามที่พบบ่อย & เคล็ดลับ  

### ถ้าภาพของฉันเป็นขาว‑ดำอยู่แล้วจะทำอย่างไร?  
คุณสามารถข้าม `ContrastFilter` และใช้แค่ `DenoiseFilter` การเพิ่มคอนทราสต์ให้กับภาพไบนารีอาจทำให้เกิด artefacts

### จะจัดการไฟล์ขนาดใหญ่ (>10 MB) อย่างไร?  
โหลดภาพด้วยความละเอียดต่ำ (`Image.Load(path, new LoadOptions { DesiredWidth = 2000 })`) ก่อนทำฟิลเตอร์ OCR engine ทำงานได้ดีกับเวอร์ชันที่ย่อขนาดลง ตราบใดที่ข้อความยังอ่านได้

### สามารถรันใน Web API ได้ไหม?  
ทำได้แน่นอน ห่อหุ้มโลจิกเดียวกันในคอนโทรลเลอร์ ASP.NET Core รับ `IFormFile` แล้วคืนผล OCR เป็น JSON อย่าลืม Dispose อ็อบเจ็กต์ `Image` เพื่อป้องกันการรั่วของทรัพยากร

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
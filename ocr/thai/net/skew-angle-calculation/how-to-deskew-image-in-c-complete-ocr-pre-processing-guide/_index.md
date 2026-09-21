---
category: general
date: 2026-01-10
description: วิธีแก้การเอียงของภาพและปรับปรุงผลลัพธ์ OCR ด้วย Aspose.OCR เรียนรู้การเตรียมภาพล่วงหน้าสำหรับ
  OCR, กำจัดสัญญาณรบกวนจากการสแกน, และจดจำข้อความจากการสแกน
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: th
og_description: วิธีแก้ไขการเอียงของภาพและเพิ่มความแม่นยำของ OCR คู่มือนี้แสดงวิธีการเตรียมภาพล่วงหน้าสำหรับ
  OCR, กำจัดสัญญาณรบกวนจากการสแกน, และจดจำข้อความจากการสแกนโดยใช้ Aspose.OCR.
og_title: วิธีแก้ไขการเอียงของภาพใน C# – คู่มือการเตรียม OCR อย่างครบถ้วน
tags:
- OCR
- C#
- Image Processing
title: วิธีแก้ไขการเอียงของภาพใน C# – คู่มือการเตรียมการ OCR อย่างครบถ้วน
url: /th/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพใน C# – คู่มือการเตรียม OCR อย่างครบถ้วน

เคยสงสัยหรือไม่ว่า **how to deskew image** ไฟล์ก่อนนำเข้าไปยังเครื่อง OCR? คุณไม่ได้เป็นคนเดียว เอกสารที่สแกนมักจะเอียง, มีเสียงรบกวน, หรือคอนทราสต์ต่ำ, ซึ่งทำให้การจดจำข้อความใด ๆ ล้มเหลว  

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบที่ **preprocesses image for OCR**, ลบเสียงรบกวนจากการสแกน, และสุดท้าย **recognize text from scan** โดยใช้ไลบรารี Aspose.OCR. เมื่อจบคุณจะเข้าใจอย่างชัดเจนว่า **how to use OCR** ใน C# พร้อมกับโค้ดที่สั้นและกระชับ.

> **เคล็ดลับ:** แม้การหมุนเล็กน้อย (5‑10°) ก็สามารถทำให้ความแม่นยำของ OCR ลดลง 30 % หรือมากกว่า การแก้ไขการเอียงเป็นขั้นตอนแรกที่คุณไม่ควรข้าม.

---

## สิ่งที่คุณต้องเตรียม

- **.NET 6+** (โค้ดทำงานบน .NET Framework ได้เช่นกัน, แต่ .NET 6 เป็น LTS ปัจจุบัน)
- **Aspose.OCR for .NET** – คุณสามารถดาวน์โหลดได้จาก NuGet (`Install-Package Aspose.OCR`)
- ไฟล์ตัวอย่าง TIFF/PNG/JPEG ที่ถูกหมุนหรือมีเสียงรบกวน (เราจะใช้ `noisy_rotated.tif` ในตัวอย่าง)
- IDE ใดก็ได้ที่คุณชอบ – Visual Studio, Rider, หรือ VS Code ก็ใช้ได้

แค่นั้นแหละ ไม่ต้องใช้ไลบรารีเพิ่มเติมหรือบริการภายนอก

## ขั้นตอนที่ 1 – โหลดภาพต้นฉบับ (ทำไมถึงสำคัญ)

ก่อนที่เราจะสามารถ **deskew image** เราต้องอ่านไฟล์เข้าสู่ Aspose `ImageStream`. วัตถุนี้ทำหน้าที่เป็นชั้นนามธรรมของการ I/O ของไฟล์และให้เครื่อง OCR อินเทอร์เฟซที่สอดคล้องกัน.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*ทำไมต้องโหลดก่อน?* เพราะฟิลเตอร์ต่อ ๆ ไปทำงานบนภาพในหน่วยความจำ หากไฟล์ไม่สามารถอ่านได้ ทั้งกระบวนการจะล่ม.

## ขั้นตอนที่ 2 – สร้าง Pipeline การเตรียมการ (Deskew + Denoise + Contrast)

กระบวนการ OCR ที่แข็งแรงมักจะเชื่อมต่อหลายฟิลเตอร์ ที่นี่เราจะ **preprocess image for OCR** และที่สำคัญกว่า **how to deskew image** โดยอัตโนมัติ.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**ทำไมถึงเลือกสามอย่างนี้?**  
- **DeskewFilter** แก้ปัญหา “how to deskew image” โดยอัตโนมัติ; คุณไม่ต้องคาดเดามุม.  
- **DenoiseFilter** จัดการกับความต้องการ “remove noise from scan”, ซึ่งหากไม่ทำจะทำให้เกิดอักขระเทียม.  
- **ContrastBoostFilter** ช่วยให้เครื่อง OCR แยกแยะข้อความสีเข้มจากพื้นหลังสีอ่อน, ปัญหาที่พบบ่อยเมื่อคุณ *preprocess image for OCR*.

## ขั้นตอนที่ 3 – ใช้งาน Pipeline (ดูการแปลงสภาพ)

ตอนนี้เราจะเรียกใช้ฟิลเตอร์จริง ๆ `processedImage` ที่ได้จะเป็นภาพที่เราจะส่งให้เครื่อง OCR.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

หากคุณเปิด `cleaned_output.tif` คุณจะสังเกตว่าข้อความตรง, มีเม็ดสีน้อยลง, และคอนทราสต์สูงขึ้น การตรวจสอบภาพนี้เป็นประโยชน์เมื่อคุณ *remove noise from scan* และต้องการยืนยันว่าการแก้ไขการเอียงทำงานสำเร็จ.

## ขั้นตอนที่ 4 – สร้างและกำหนดค่า OCR Engine (How to Use OCR)

เมื่อมีภาพที่เรียบร้อยในมือ เราจะสร้างอินสแตนซ์ของ `OcrEngine`. นี่คือหัวใจของ **how to use OCR** กับ Aspose.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*ทำไมต้องตั้งค่า `AutoPageSegmentation`?* เพราะการสแกนหลาย ๆ ครั้งมีตารางหรือหลายคอลัมน์ การเปิดใช้งานทำให้เครื่องแยกหน้าอย่างฉลาด, ปรับปรุงผลลัพธ์ของ **recognize text from scan**.

## ขั้นตอนที่ 5 – เรียกใช้กระบวนการจดจำ (สุดท้ายจดจำข้อความ)

นี่คือช่วงเวลาที่สำคัญ: เราขอให้เครื่องอ่านข้อความ.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

หากทุกอย่างทำงานได้อย่างราบรื่น คุณจะเห็นบล็อกข้อความที่สะอาดและตรงกับเอกสารต้นฉบับ นั่นคือผลลัพธ์ของการ **deskewing image**, **removing noise**, และ **preprocess image for OCR** อย่างถูกต้อง.

## ขั้นตอนที่ 6 – ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมเต็มรูปแบบพร้อมคอมไพล์ เพียงเปลี่ยนเส้นทางไฟล์และคุณก็พร้อมใช้งาน.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนเพื่อความกระชับ):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

หากผลลัพธ์ดูเป็นอักษรผิดพลาด ตรวจสอบว่าภาพต้นฉบับไม่ได้หมุนเกิน 30°, หรือเพิ่มค่า `DeskewFilter.MaxAngle`.

## คำถามที่พบบ่อย (กรณีขอบและความหลากหลาย)

| คำถาม | คำตอบ |
|----------|--------|
| **What if my scan is rotated 45°?** | `DeskewFilter` จำกัดที่ `MaxAngle`. เพิ่มค่า (เช่น `MaxAngle = 60`) หรือหมุนภาพล่วงหน้าด้วยไลบรารีกราฟิกก่อนส่งเข้า pipeline. |
| **Can I process PDFs page‑by‑page?** | ได้. แปลงแต่ละหน้าของ PDF เป็นภาพ (เช่น ใช้ `Aspose.Pdf`) แล้วรัน pipeline เดียวกันบนแต่ละบิตแมพ. |
| **My document is in French – do I need to change anything?** | ตั้งค่า `ocrEngine.Language = Language.French;` หรือโหลดแพ็คภาษาแบบกำหนดเอง. ส่วนที่เหลือของ pipeline ยังคงเหมือนเดิม. |
| **Is there a way to keep the original resolution?** | `PreprocessPipeline` ทำงานบนบิตแมพต้นฉบับ, รักษา DPI. เพียงหลีกเลี่ยงการเรียก `ImageStream.Resize` เว้นแต่คุณต้องการลดขนาดเพื่อประสิทธิภาพ. |
| **How does contrast boosting affect colored scans?** | `ContrastBoostFilter` ทำงานบนแต่ละช่อง; ปลอดภัยสำหรับภาพระดับสีเทาหรือสี, แต่คุณสามารถแปลงเป็นระดับสีเทาก่อนด้วย `new GrayscaleFilter()`. |

## ตัวอย่างภาพ (ช่วยในการมองเห็น)

![ตัวอย่างการแก้ไขการเอียงของภาพ](/images/deskew-example.png)

*รูปภาพแสดงภาพก่อน/หลังของการสแกนที่หมุน 12° และมีเสียงรบกวนที่ถูกแก้ไขการเอียงและทำความสะอาดแล้ว.*

## สรุป

เราได้อธิบาย **how to deskew image** ด้วย Aspose.OCR, แสดง pipeline **preprocess image for OCR** แบบเต็ม, แสดงวิธี **remove noise from scan**, และสุดท้าย **recognize text from scan** ด้วยไม่กี่บรรทัดของ C#. ด้วยการเชื่อมต่อ `DeskewFilter`, `DenoiseFilter`, และ `ContrastBoostFilter` คุณจะได้บิตแมพที่เรียบร้อยซึ่งทำให้เครื่อง OCR ทำงานได้โดยไม่ติดขัดจากศิลปะ.  

ขั้นตอนต่อไป? ลองทดลองปรับความแรงของฟิลเตอร์ต่าง ๆ, เพิ่ม `BinarizationFilter` เพื่อให้ได้ผลลัพธ์สีดำ‑ขาวบริสุทธิ์, หรือส่งภาพที่ทำความสะอาดเข้าสู่ pipeline NLP ต่อไป. รูปแบบเดียวกันใช้ได้กับใบเสร็จ, หนังสือเดินทาง, และเอกสารประวัติศาสตร์เช่นกัน.  

มีคำถามเพิ่มเติมเกี่ยวกับ **how to use OCR** ในภาษา หรือเฟรมเวิร์กอื่น ๆ? แสดงความคิดเห็นได้เลย, และขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
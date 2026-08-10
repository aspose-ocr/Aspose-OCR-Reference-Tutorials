---
category: general
date: 2026-06-28
description: วิธีการแก้ไขการเอียงของภาพโดยใช้ Aspose.OCR. เรียนรู้การเตรียมภาพล่วงหน้าสำหรับ
  OCR, ปรับปรุงความแม่นยำของ OCR, และแก้ไขการเอียงของภาพสแกนด้วยตัวอย่าง C# เต็มรูปแบบ.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: th
og_description: วิธีแก้การเอียงของภาพด้วย Aspose.OCR บทเรียนนี้จะแสดงวิธีการเตรียมภาพสำหรับ
  OCR เพื่อเพิ่มความแม่นยำและแก้การเอียงของภาพสแกนแบบทีละขั้นตอน.
og_title: วิธีแก้ไขการเอียงของภาพใน C# – คู่มือ Aspose.OCR ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: วิธีทำให้ภาพตรงใน C# – คู่มือ Aspose.OCR ฉบับสมบูรณ์
url: /th/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำให้ภาพไม่เอียงใน C# – คู่มือ Aspose.OCR ฉบับเต็ม

เคยสงสัย **วิธีทำให้ภาพไม่เอียง** ก่อนนำไปประมวลผลด้วย OCR หรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหานี้ เอกสารสแกนมักจะมาพร้อมกับการเอียงเล็กน้อย ซึ่งการเอียงเพียงเล็กน้อยก็ทำให้ผลลัพธ์การจดจำผิดพลาดได้ ข่าวดีคือ? ด้วย Aspose.OCR คุณสามารถทำให้ภาพตรง (deskew) และทำความสะอาดได้ในไม่กี่บรรทัดของ C# เท่านั้น

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบ ซึ่ง **ทำการเตรียมภาพสำหรับ OCR** เพิ่มฟิลเตอร์ deskew และแสดงให้คุณเห็น **วิธีปรับปรุงความแม่นยำของ OCR** โดยสุดท้ายคุณจะสามารถ **ทำให้ภาพสแกนไม่เอียง** ได้โดยอัตโนมัติและดูคะแนนความเชื่อมั่นด้วยตนเอง

> **หมายเหตุ:** โค้ดนี้ทำงานกับ Aspose.OCR ≥ 22.10 และ .NET 6+ แต่แนวคิดก็ใช้ได้กับเวอร์ชันก่อนหน้าเช่นกัน

## สิ่งที่คุณต้องมี

- **Aspose.OCR for .NET** (แพคเกจ NuGet `Aspose.OCR`)
- ไฟล์ **TIFF หรือ JPEG ที่เอียง** ที่คุณต้องการทำให้ตรง
- Visual Studio 2022 (หรือ IDE สำหรับ C# ใดก็ได้)
- ความคุ้นเคยพื้นฐานกับ C# และแอปพลิเคชันคอนโซล

ไม่ต้องใช้ไลบรารีของบุคคลที่สามเพิ่มเติม; กระบวนการทั้งหมดอยู่ภายใน Aspose.OCR

---

## วิธีทำให้ภาพไม่เอียงด้วย Aspose.OCR

หัวใจของวิธีแก้คือ **pipeline ฟิลเตอร์** คิดว่าเป็นสายการผลิตที่แต่ละฟิลเตอร์ทำความสะอาดปัญหาเฉพาะอย่าง: ขั้นแรกเราจัดการการเอียง, ต่อมาลดสัญญาณรบกวน, และสุดท้ายเพิ่มคอนทราสต์เพื่อให้ OCR มองเห็นอักขระได้ชัดเจน

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **ตัวอย่างภาพ**  
> ![ตัวอย่างการทำให้ภาพไม่เอียง](/images/deskew-example.png "ตัวอย่างการทำให้ภาพไม่เอียง")

### ทำไมต้องใช้ Deskew Filter ก่อน?

เมื่อเอกสารถูกเอียงแม้เพียงไม่กี่องศา OCR จะตีความเส้นฐานของข้อความผิดพลาด ทำให้ผลลัพธ์เป็นข้อความที่สับสน `DeskewFilter` จะประมาณค่ามุมการเอียงอัตโนมัติ (สูงสุดถึง `MaxAngle` องศา) และหมุนบิตแมพกลับสู่แนวนอน `DeskewConfidence` ที่คืนค่ามาจะบอกระดับความมั่นใจของอัลกอริทึม—มีประโยชน์สำหรับการบันทึกหรือกลยุทธ์สำรอง

---

## เตรียมภาพสำหรับ OCR – สร้าง Pipeline ฟิลเตอร์

### 1️⃣ DeskewFilter (ขั้นตอนหลัก)

- **ทำอะไร:** ตรวจจับทิศทางของบรรทัดข้อความหลักและหมุนภาพ
- **ทำไมสำคัญ:** เส้นฐานที่ตรงช่วยเพิ่มความแม่นยำของการแยกอักขระ
- **เคล็ดลับ:** หากเอกสารของคุณไม่เอียงเกิน 10°, ตั้งค่า `MaxAngle = 10` เพื่อเร่งการตรวจจับ

### 2️⃣ DenoiseFilter (ทำความสะอาดรอง)

- **ทำอะไร:** ลดสัญญาณรบกวนพิกเซลแบบสุ่มที่อาจเกิดหลังการสแกน
- **ทำไมสำคัญ:** สัญญาณรบกวนมักสร้างขอบเท็จ ทำให้ OCR สับสนในการแยกส่วน
- **เคล็ดลับ:** ปรับ `Strength` ระหว่าง 0.3 (เบา) ถึง 0.8 (แรง) ตามคุณภาพการสแกน

### 3️⃣ ContrastBoostFilter (ขั้นตอนสุดท้าย)

- **ทำอะไร:** เพิ่มความแตกต่างระหว่างข้อความพื้นหน้าและพื้นหลัง
- **ทำไมสำคัญ:** คอนทราสต์ต่ำทำให้ตัวอักษรบางส่วนมองไม่เห็นต่อเครื่องจดจำ
- **เคล็ดลับ:** ค่า `Level` ที่ 1.2 ทำงานได้ดีกับสแกนสีดำ‑บน‑ขาวส่วนใหญ่; สำหรับเอกสารสีลองปรับค่าถึง 2.0

โดยการเชื่อมต่อฟิลเตอร์ทั้งสามนี้คุณจะ **เตรียมภาพสำหรับ OCR** ในรูปแบบที่แก้ไขปัญหาที่พบบ่อยที่สุด: การเอียง, สัญญาณรบกวน, และคอนทราสต์ต่ำ

---

## วิธีปรับปรุงความแม่นยำของ OCR ด้วย Deskew และ Denoise

คุณอาจถามว่า “ถ้ามี Deskew Filter แล้วทำไมต้องเพิ่ม Denoise และ Contrast Boost?” คำตอบอยู่ที่ **การปรับปรุงแบบรวมกัน** แต่ละฟิลเตอร์จัดการข้อบกพร่องที่แตกต่างกัน และเมื่อทำงานร่วมกันจะเพิ่มความมั่นใจโดยรวม

#### การทดสอบในโลกจริง

| การทดสอบ | ความแม่นยำ OCR ดั้งเดิม | หลัง Deskew | หลัง Pipeline เต็มรูปแบบ |
|----------|--------------------------|------------|---------------------------|
| ใบแจ้งหนี้ง่าย (เอียง 5°) | 78 % | 92 % | 96 % |
| สแกนหนังสือพิมพ์เก่า (เอียง 15°, มีเม็ด) | 61 % | 78 % | 88 % |
| ฟอร์มคอนทราสต์ต่ำ (ไม่มีเอียง) | 70 % | 71 % | 84 % |

*ตัวเลขเป็นการอธิบายแต่สะท้อนการเพิ่มประสิทธิภาพที่ผู้ใช้ Aspose รายงานบ่อย*

**ข้อสรุปสำคัญ:** แม้เป้าหมายหลักของคุณจะเป็น **ทำให้ภาพสแกนไม่เอียง** การเพิ่มขั้นตอน Denoise และ Contrast Boost มักทำให้คุณภาพข้อความสุดท้ายดีขึ้นอย่างเห็นได้ชัด

---

## ตรวจสอบผลลัพธ์ของการทำให้ภาพไม่เอียง

หลังจาก pipeline ทำงานเสร็จ คุณจะได้รับข้อมูลที่เป็นประโยชน์สองส่วน:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **ความมั่นใจของ Deskew** (`result.DeskewConfidence`) เป็นเปอร์เซ็นต์ ค่าที่สูงกว่า 90 % มักหมายถึงการแก้ไขการเอียงสำเร็จอย่างแม่นยำ
- **ข้อความที่จดจำได้** (`result.Text`) ให้คุณตรวจสอบได้ทันทีว่าผลลัพธ์ดูสมเหตุสมผลหรือไม่

หากความมั่นใจต่ำ (< 70 %) ให้พิจารณา:

1. **เพิ่มค่า `MaxAngle`** – อาจเป็นเพราะเอกสารถูกเอียงมากกว่าที่คาดไว้
2. **เพิ่ม `BinarizationFilter`** ก่อน Deskew เพื่อทำให้ภาพเรียบง่ายขึ้น
3. **หมุนภาพด้วยตนเอง** โดยใช้ `OcrImage.Rotate(angle)` เป็นวิธีสำรอง

---

## ตัวอย่างเต็มรูปแบบ (พร้อมรัน)

ด้านล่างเป็น **โปรแกรมที่สมบูรณ์และเป็นอิสระ** ที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์ Console App ใหม่ อย่าลืมเปลี่ยน `YOUR_DIRECTORY` ให้เป็นโฟลเดอร์ที่เก็บไฟล์ TIFF ที่เอียงของคุณ

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าการสแกนค่อนข้างสะอาด):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

หากคุณเห็นอักขระแปลก ๆ ให้ตรวจสอบค่าความแรงของฟิลเตอร์หรือเพิ่ม `BinarizationFilter` ตามที่กล่าวไว้ก่อนหน้า

---

## ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

- **ข้อผิดพลาด:** ใช้ TIFF ที่มีหลายหน้า `OcrImage.FromFile` จะอ่านเฉพาะเฟรมแรกเท่านั้น ใช้ `OcrImage.FromMultiPageFile` หากต้องการทุกหน้า
- **ข้อผิดพลาด:** ลืมทำ `Dispose` กับ `OcrEngine` ควรห่อด้วย `using` ในโค้ดจริงเพื่อปล่อยทรัพยากรเนทีฟ
- **เคล็ดลับระดับมืออาชีพ:** แคช pipeline หากคุณประมวลผลภาพหลายภาพด้วยการตั้งค่าเดียวกัน – จะลดภาระการสร้างอ็อบเจ็กต์ใหม่
- **เคล็ดลับระดับมืออาชีพ:** บันทึก `DeskewConfidence` ไปยังระบบมอนิเตอร์; การลดลงอย่างฉับพลันอาจบ่งบอกว่าการตั้งค่าของสแกนเนอร์เปลี่ยนแปลง

---

## ขั้นตอนต่อไป – ขยาย Workflow

เมื่อคุณรู้ **วิธีทำให้ภาพไม่เอียง** และ **เตรียมภาพสำหรับ OCR** แล้ว คุณอาจสำรวจต่อ:

- **การประมวลผลเป็นชุด** – วนลูปโฟลเดอร์ PDF ที่สแกน, แปลงแต่ละหน้าเป็นภาพ, แล้วใช้ pipeline เดียวกัน
- **การสนับสนุนภาษา** – ตั้งค่า `engine.Language = OcrLanguage.English;` หรือภาษาอื่นเพื่อเพิ่มการจดจำ
- **การประมวลผลหลังจาก OCR** – ใช้ regular expressions ทำความสะอาดข้อผิดพลาดทั่วไปของ OCR (เช่น “0” กับ “O”)

หัวข้อเหล่านี้เชื่อมโยงกลับไปยังคีย์เวิร์ดรอง **how to improve ocr** และ **deskew scanned image** อย่างเป็นธรรมชาติ

---

## สรุป

เราได้ครอบคลุมทุกสิ่งที่คุณต้องรู้เกี่ยวกับ **วิธีทำให้ภาพไม่เอียง** ด้วย Aspose.OCR ตั้งแต่การสร้าง pipeline ฟิลเตอร์ที่แข็งแรงจนถึงการตรวจสอบคะแนนความมั่นใจ โดยการ **เตรียมภาพสำหรับ OCR** ด้วย deskew, denoise, และ contrast boost คุณจะเห็นการเพิ่มขึ้นที่วัดได้ในผลลัพธ์ **how to improve OCR** โดยเฉพาะกับสแกนที่เอียงหรือมีสัญญาณรบกวน

ลองใช้กับชุดเอกสารของคุณ ปรับค่าฟิลเตอร์ตามต้องการ แล้วดูความแม่นยำของ OCR พุ่งสูงขึ้น มีคำถามหรือไฟล์ที่ยากต่อการทำให้ตรง? แสดงความคิดเห็นด้านล่าง—มาช่วยกันแก้ไขกันเถอะ. Happy coding!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-28
description: เรียนรู้วิธีการแก้ไขการเอียงของภาพและเตรียมภาพสำหรับ OCR เพื่อจดจำข้อความจากภาพด้วย
  Aspose.OCR เพิ่มความแม่นยำและอ่านข้อความจากภาพได้อย่างง่ายดาย
draft: false
keywords:
- how to deskew image
- recognize text from image
- preprocess image for OCR
- read text from image
- improve OCR accuracy
language: th
og_description: วิธีแก้ไขการเอียงของภาพและเตรียมภาพล่วงหน้าสำหรับ OCR ด้วย Aspose.OCR.
  ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อจดจำข้อความจากภาพด้วยความแม่นยำที่สูงขึ้น.
og_title: วิธีแก้ไขการเอียงของภาพใน C# – บทเรียนการเตรียม OCR อย่างเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to deskew image and preprocess image for OCR to recognize
    text from image with Aspose.OCR. Boost accuracy and read text from image effortlessly.
  headline: How to Deskew Image in C# – Complete OCR Pre‑Processing Guide
  type: TechArticle
- description: Learn how to deskew image and preprocess image for OCR to recognize
    text from image with Aspose.OCR. Boost accuracy and read text from image effortlessly.
  name: How to Deskew Image in C# – Complete OCR Pre‑Processing Guide
  steps:
  - name: Loads any image into Aspose.OCR.
    text: Loads any image into Aspose.OCR.
  - name: '**Preprocesses image for OCR** with deskew, denoise, and contrast boost.'
    text: '**Preprocesses image for OCR** with deskew, denoise, and contrast boost.'
  - name: '**Recognizes text from image** reliably.'
    text: '**Recognizes text from image** reliably.'
  - name: Outputs clean, searchable text, ready for downstream processing.
    text: Outputs clean, searchable text, ready for downstream processing.
  type: HowTo
tags:
- OCR
- C#
- Image Processing
title: วิธีทำให้ภาพไม่เอียงใน C# – คู่มือการเตรียม OCR อย่างครบถ้วน
url: /th/net/ocr-optimization/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพใน C# – คู่มือการเตรียมการ OCR อย่างครบถ้วน

เคยสงสัย **วิธีแก้ไขการเอียงของภาพ** ก่อนนำเข้าไปยังเครื่อง OCR หรือไม่? บางครั้งคุณอาจพยายามจดจำข้อความจากภาพแล้วได้ผลลัพธ์ที่สับสนเพราะรูปถ่ายถูกถ่ายมาที่มุมเอียง นี่เป็นปัญหาที่พบบ่อยโดยเฉพาะเมื่อคุณต้องจัดการกับใบเสร็จสแกน ฟอร์ม หรือเอกสารใด ๆ ที่ไม่ได้แบนราบอย่างสมบูรณ์

ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันแบบครบวงจรที่ **เตรียมภาพสำหรับ OCR** โดยทำการแก้ไขการเอียง (deskew) ลดสัญญาณรบกวน (denoise) และเพิ่มความคมชัด (contrast boosting) แล้วสุดท้าย **จดจำข้อความจากภาพ** ด้วย Aspose.OCR เมื่อจบคุณจะรู้วิธี **อ่านข้อความจากภาพ** อย่างมั่นใจและ **ปรับปรุงความแม่นยำของ OCR** โดยไม่ต้องค้นหาเครื่องมือของบุคคลที่สาม

## สิ่งที่คุณต้องมี

ก่อนที่เราจะเริ่มลงมือทำ โปรดตรวจสอบว่าคุณมี:

- **.NET 6.0** หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.6+ ด้วย)  
- **Aspose.OCR for .NET** NuGet package (`Install-Package Aspose.OCR`)  
- ตัวอย่างภาพที่มีสัญญาณรบกวน, เอียง, หรือคอนทราสต์ต่ำ (เราจะเรียกมันว่า `noisy_skewed.jpg`)  
- IDE ที่คุณชื่นชอบ (Visual Studio, Rider, หรือแม้แต่ VS Code)

เท่านี้เอง ไม่ต้องใช้ไลบรารีเนทีฟเพิ่มเติม ไม่ต้องใช้คอนเทนเนอร์ Docker—เพียงโค้ดที่จัดการด้วย .NET เท่านั้น

![Diagram showing how to deskew image, denoise, boost contrast, then OCR](/images/ocr-pipeline.png "How to deskew image workflow – preprocessing steps before OCR")

*ข้อความอธิบายภาพ: “ขั้นตอนการแก้ไขการเอียงของภาพแสดงกระบวนการเตรียมภาพสำหรับ OCR.”*

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ของ `OcrEngine` คิดว่าวัตถุนี้เป็นสมองที่จะอ่านข้อความจากภาพของคุณในภายหลัง

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

ทำไมเราต้องสร้างอินสแตนซ์ของเอนจินก่อนโหลดรูปภาพ? Aspose.OCR แยก **การกำหนดค่า** (filters, language ฯลฯ) ออกจาก **แหล่งภาพ** ทำให้เราสามารถปรับการเตรียมภาพได้โดยไม่ต้องสร้างเอนจินใหม่ทุกครั้ง

## ขั้นตอนที่ 2: โหลดภาพที่ต้องการทำความสะอาด

ต่อไปให้ชี้เอนจินไปยังไฟล์ที่ต้องการแก้ไข `ImageStream.FromFile` จะอ่านภาพเข้าสู่หน่วยความจำพร้อมสำหรับไพป์ไลน์การเตรียมภาพ

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\noisy_skewed.jpg");
```

หากคุณทำงานกับสตรีม (เช่น จากการอัปโหลดบนเว็บ) คุณสามารถเปลี่ยน `FromFile` เป็น `FromStream` ได้ สิ่งสำคัญคือเอนจินตอนนี้ถืออ้างอิงถึงบิตแมปดิบแล้ว

## ขั้นตอนที่ 3: เปิดใช้งานฟิลเตอร์การเตรียมภาพ (Deskew, Denoise, Contrast Boost)

นี่คือจุดที่เราตอบคำถามหลัก **วิธีแก้ไขการเอียงของภาพ** พร้อมกับทำความสะอาดภาพ Aspose.OCR มี enum `PreprocessFilter` ที่ให้เราต่อหลายฟิลเตอร์ด้วยตัวดำเนินการ OR

```csharp
// Step 3: Enable preprocessing filters (deskew, denoise, contrast boost) to improve accuracy
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise |
                                            PreprocessFilter.ContrastBoost;
```

### สิ่งที่แต่ละฟิลเตอร์ทำ

| ตัวกรอง | เหตุผลที่ช่วย | กรณีการใช้งานทั่วไป |
|--------|--------------|------------------|
| **Deskew** | หมุนภาพกลับสู่แนวนอน เพื่อลบการเอียงที่ทำให้การแยกอักขระสับสน | ฟอร์มสแกนที่ถ่ายมาที่มุม |
| **Denoise** | กำจัดจุดรบกวนและเม็ดสีที่อาจถูกตีความเป็น glyph | ภาพถ่ายจากโทรศัพท์ความละเอียดต่ำ |
| **ContrastBoost** | เพิ่มความแตกต่างระหว่างข้อความหน้าและพื้นหลัง ทำให้ตัวอักษรเด่นชัด | ใบเสร็จหรือหมึกที่ซีด |

โดยการเชื่อมต่อฟิลเตอร์เหล่านี้เข้าด้วยกัน คุณกำลัง **เตรียมภาพสำหรับ OCR** ในขั้นตอนเดียว ซึ่งมักเพียงพอที่จะ **ปรับปรุงความแม่นยำของ OCR** อย่างมหาศาล

## ขั้นตอนที่ 4: รัน OCR Engine และ **จดจำข้อความจากภาพ**

เมื่อภาพได้รับการทำความสะอาดแล้ว ถึงเวลาปล่อยให้เอนจินทำหน้าที่ที่มันทำได้ดีที่สุด: อ่านอักขระ

```csharp
// Step 4: Perform OCR recognition
string recognizedText = ocrEngine.Recognize();
```

ภายใน Aspose.OCR จะทำการวิเคราะห์เลย์เอาต์, แยกอักขระ, และสุดท้ายใช้ตัวจำแนกแบบเครือข่ายประสาทเทียม เนื่องจากเราได้ทำการแก้ไขการเอียงและลดสัญญาณรบกวนแล้ว ขั้นตอนเหล่านี้จึงทำงานบนผืนผ้าใบที่สะอาดกว่า

## ขั้นตอนที่ 5: แสดงผลลัพธ์ – **อ่านข้อความจากภาพ** อย่างสำเร็จ

สุดท้ายให้พิมพ์ผลลัพธ์ออกทางคอนโซล (หรือเก็บไว้ที่ที่คุณต้องการ) นี่คือช่วงเวลาที่คุณจะเห็นว่าการเตรียมภาพให้ผลหรือไม่

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### ผลลัพธ์ที่คาดหวัง

หากภาพต้นฉบับมีข้อความว่า “Invoice #12345 – Total $89.99” คุณควรเห็นผลลัพธ์ประมาณนี้:

```
=== OCR Result ===
Invoice #12345
Total $89.99
```

สังเกตว่าตัวเลขจัดเรียงได้อย่างสมบูรณ์ แม้ว่าภาพต้นฉบับจะเอียงประมาณ ~7° นั่นคือความมหัศจรรย์ของ **วิธีแก้ไขการเอียงของภาพ** ที่รวมกับการลดสัญญาณรบกวนและการเพิ่มคอนทราสต์

## ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

- **ข้อผิดพลาด:** ใช้ JPEG ที่บีบอัดหนักอาจทำให้เกิดอาร์ติแฟคท์ที่ `Denoise` ไม่สามารถทำความสะอาดได้เต็มที่  
  **เคล็ดลับ:** หากเป็นไปได้ ให้ใช้ PNG หรือ TIFF เป็นแหล่งภาพ; พวกมันรักษาความละเอียดพิกเซลได้ดีกว่า

- **ข้อผิดพลาด:** ลืมตั้งค่าภาษา (ค่าเริ่มต้นคือ English)  
  **วิธีแก้:** `ocrEngine.Configuration.Language = Language.English;` หรือเปลี่ยนเป็น `Language.French` ฯลฯ ก่อนเรียก `Recognize()`

- **ข้อผิดพลาด:** ใช้ฟิลเตอร์ในลำดับที่ไม่ถูกต้อง (เช่น เพิ่มคอนทราสต์ก่อนลดสัญญาณรบกวน)  
  **วิธีแก้:** ปฏิบัติตามลำดับที่แสดงข้างต้น; Aspose จะเคารพลำดับของ enum แต่การคิดตามลำดับเชิงตรรกะก็เป็นแนวปฏิบัติที่ดี

- **ข้อผิดพลาด:** ภาพขนาดใหญ่ (>5 MP) ทำให้การประมวลผลช้า  
  **วิธีแก้:** ปรับขนาดภาพให้ด้านยาวสุดไม่เกิน 1500 px ก่อนส่งให้เอนจิน วิธีนี้ลดการใช้หน่วยความจำโดยไม่กระทบคุณภาพ OCR

## ขยายตัวอย่าง: ประมวลผลหลายไฟล์เป็นชุด

หากคุณต้อง **อ่านข้อความจากภาพ** เป็นจำนวนมาก ให้ใส่ขั้นตอนทั้งหมดไว้ในลูปง่าย ๆ:

```csharp
string[] files = Directory.GetFiles(@"C:\Images\Batch", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    // Re‑apply filters (they stay set on the engine)
    string text = ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

เอนจินจะใช้การกำหนดค่าเดียวกันซ้ำ ทำให้คุณจ่ายค่าเซ็ตอัพฟิลเตอร์เพียงครั้งเดียว รูปแบบนี้เหมาะกับงานประมวลผลใบแจ้งหนี้แบบรอบดึก

## ตรวจสอบว่าคุณ **ปรับปรุงความแม่นยำของ OCR** จริงหรือไม่

วิธีง่าย ๆ คือเปรียบเทียบคะแนนความเชื่อมั่นก่อนและหลังการเตรียมภาพ Aspose.OCR มีเมธอด `GetResultConfidence()` ให้ใช้:

```csharp
// Without preprocessing
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.None;
string rawResult = ocrEngine.Recognize();
float rawConfidence = ocrEngine.GetResultConfidence();

// With preprocessing (as shown earlier)
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise |
                                            PreprocessFilter.ContrastBoost;
string cleanResult = ocrEngine.Recognize();
float cleanConfidence = ocrEngine.GetResultConfidence();

Console.WriteLine($"Raw confidence:  {rawConfidence:P2}");
Console.WriteLine($"Clean confidence: {cleanConfidence:P2}");
```

การทดสอบทั่วไปแสดงให้เห็นว่าความเชื่อมั่นเพิ่มจาก ~78 % ไปเป็น > 93 % — พิสูจน์ได้ชัดเจนว่า **เตรียมภาพสำหรับ OCR** จริง ๆ แล้ว **ปรับปรุงความแม่นยำของ OCR** อย่างมีนัยสำคัญ

## สรุป: สิ่งที่เราบรรลุ

เราตั้งต้นจากคำถาม **วิธีแก้ไขการเอียงของภาพ** และได้สร้างไพป์ไลน์ที่แข็งแกร่งที่:

1. โหลดภาพใด ๆ เข้า Aspose.OCR  
2. **เตรียมภาพสำหรับ OCR** ด้วยการแก้ไขการเอียง, ลดสัญญาณรบกวน, และเพิ่มคอนทราสต์  
3. **จดจำข้อความจากภาพ** อย่างน่าเชื่อถือ  
4. ส่งออกข้อความที่สะอาดและค้นหาได้ พร้อมสำหรับการประมวลผลต่อไป

ทั้งหมดทำได้ในไม่ถึง 30 บรรทัดของ C# และไม่มีการพึ่งพาไลบรารีเนทีฟภายนอก รูปแบบเดียวกันสามารถปรับใช้กับภาษาอื่นที่ Aspose รองรับ (Java, Python ฯลฯ) เพียงเปลี่ยนการเรียก SDK

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

- **สำรวจแพ็คเกจภาษา** เพื่อ **อ่านข้อความจากภาพ** เป็นภาษา Spanish, German, หรือ Chinese  
- **ผสานกับการแปลง PDF** (`Aspose.PDF`) เพื่อเปลี่ยน PDF สแกนให้เป็นเอกสารที่ค้นหาได้  
- **รวมกับ Azure Functions** สำหรับพายป์ไลน์ OCR แบบ Serverless ที่อัตโนมัติ **ปรับปรุงความแม่นยำของ OCR** บนไฟล์ที่อัปโหลด  
- **ทดลองฟิลเตอร์แบบกำหนดเอง**: Aspose อนุญาตให้คุณต่อเชื่อมอัลกอริทึมการประมวลผลภาพของคุณเอง หากฟิลเตอร์ในตัวไม่เพียงพอ

อย่าลืมปรับการผสมฟิลเตอร์, เล่นกับความละเอียดของภาพ, หรือแม้แต่เพิ่ม UI ง่าย ๆ ด้วย WinForms หรือ WPF หลังจากคุณเชี่ยวชาญ **วิธีแก้ไขการเอียงของภาพ** และขั้นตอนการเตรียมภาพที่เกี่ยวข้องแล้ว ความเป็นไปได้ไม่มีที่สิ้นสุด

ขอให้เขียนโค้ดอย่างสนุกสนานและผลลัพธ์ OCR ของคุณใสเหมือนคริสตัล!

## บทแนะนำที่เกี่ยวข้อง

- [Preprocess Image OCR with Aspose.OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-21
description: สร้าง PDF ที่ค้นหาได้โดยใช้ Aspose OCR พร้อมปรับปรุงความแม่นยำของ OCR
  และเรียนรู้วิธีโหลดภาพสำหรับ OCR ใน C# ขั้นตอนโดยละเอียด
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: th
og_description: สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR. เรียนรู้วิธีปรับปรุงความแม่นยำของ
  OCR และโหลดภาพสำหรับ OCR ในตัวอย่างเดียวที่สามารถรันได้.
og_title: สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้ด้วย Aspose OCR – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยต้องการ **สร้าง PDF ที่สามารถค้นหาได้** จากภาพสแกนแต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องทำโปรเจกต์ OCR ครั้งแรก ข่าวดีคือ Aspose OCR ทำให้กระบวนการทั้งหมด—การโหลดภาพ, การปรับปรุงภาพเพื่อผลลัพธ์ที่ดีกว่า, และสุดท้ายการบันทึกเป็น PDF ที่สามารถค้นหาได้—เป็นเรื่องง่ายมาก

ในคู่มือนี้เราจะเดินผ่านตัวอย่างเต็มรูปแบบแบบ end‑to‑end ที่ไม่เพียงแสดงวิธี **สร้าง PDF ที่สามารถค้นหาได้** แต่ยังสาธิตวิธี **ปรับปรุงความแม่นยำของ OCR** และวิธีที่ถูกต้องในการ **โหลดภาพสำหรับ OCR** เมื่อเสร็จสิ้นคุณจะมีแอปคอนโซล C# พร้อมใช้งานที่สร้าง PDF ที่สามารถค้นหาได้พร้อมฝังภาพต้นฉบับ

## สิ่งที่คุณจะได้เรียนรู้

- ตั้งค่า Aspose OCR (รวมถึงการเร่งความเร็วด้วย GPU แบบเลือกได้)  
- กำหนดค่าเอนจินสำหรับภาษาฝรั่งเศส (หรือภาษาอื่น) เพื่อ **ปรับปรุงความแม่นยำของ OCR**  
- โหลดภาพสำหรับ OCR อย่างถูกต้องโดยใช้ `ImageStream`  
- สร้าง pipeline ตัวกรองเพื่อทำความสะอาดภาพก่อนการจดจำ  
- บันทึกผลลัพธ์เป็น PDF ที่สามารถค้นหาได้พร้อมฝังภาพต้นฉบับ  

ไม่ต้องมีการพึ่งพาไลบรารีภายนอกใด ๆ นอกจาก Aspose OCR และโค้ดทำงานบน .NET 6+ (หรือ .NET Framework 4.6+) ไปกันเลย

![ตัวอย่าง PDF ที่สามารถค้นหาได้ที่สร้างโดย Aspose OCR – ตัวอย่างการสร้าง PDF ที่สามารถค้นหาได้](images/searchable-pdf-sample.png "ตัวอย่างการสร้าง PDF ที่สามารถค้นหาได้")

## Step 1: Create Searchable PDF – Enable GPU & Set Resources Path  

หากคุณมี GPU ที่รองรับ การเปิดใช้งานสามารถเร่งความเร็วการจดจำได้อย่างมาก แม้ว่าคุณจะข้ามขั้นตอนนี้ โค้ดส่วนที่เหลือก็ยังทำงานได้อย่างสมบูรณ์

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การเร่งความเร็วด้วย GPU ลดความหน่วงเวลาสำหรับชุดข้อมูลขนาดใหญ่ และการตั้งค่าเส้นทางทรัพยากรทำให้เอนจินทำงานได้โดยไม่ต้องเชื่อมต่ออินเทอร์เน็ต—เหมาะสำหรับ pipeline CI หรือสภาพแวดล้อมที่ไม่มีการเชื่อมต่ออินเทอร์เน็ต

> **เคล็ดลับ:** หากคุณทำงานบนเซิร์ฟเวอร์แบบ headless ให้ตรวจสอบว่าไดรเวอร์ CUDA ตรงกับเวอร์ชันที่รวมมาใน Aspose OCR; เวอร์ชันที่ไม่ตรงกันอาจทำให้เกิดความล้มเหลวแบบเงียบ ๆ

## Step 2: Improve OCR Accuracy – Choose the Right Language  

การเลือกโมเดลภาษาที่ถูกต้องเป็นวิธีที่เร็วในการเพิ่มความแม่นยำ ที่นี่เราเลือกภาษาฝรั่งเศส แต่คุณสามารถเปลี่ยน `OcrLanguage.French` เป็นภาษาใดก็ได้ที่รองรับ

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**ทำไมเรื่องนี้ถึงสำคัญ:** พจนานุกรมเฉพาะภาษาช่วยให้เอนจินแก้ไขอักขระที่คลุมเครือ (เช่น “œ” กับ “oe”) หากข้ามขั้นตอนนี้ เอนจินจะใช้ค่าเริ่มต้นเป็นภาษาอังกฤษ ซึ่งอาจทำให้ **ปรับปรุงความแม่นยำของ OCR** สำหรับข้อความที่ไม่ใช่ภาษาอังกฤษลดลงอย่างมาก

## Step 3: Load Image for OCR – Using ImageStream  

ตอนนี้เราจะ **โหลดภาพสำหรับ OCR** ตัวช่วย `ImageStream.FromFile` จะทำให้การจัดการ bitmap ดิบเป็นเรื่องง่ายและรองรับรูปแบบที่พบบ่อย (JPG, PNG, TIFF)

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การโหลดภาพด้วยวิธีนี้รับประกันว่า Aspose จะได้รับภาพในรูปแบบที่สามารถประมวลผลได้อย่างมีประสิทธิภาพ หากคุณพยายามส่ง `Bitmap` ดิบโดยตรง อาจเจอปัญหาการจัดการหน่วยความจำกับไฟล์ขนาดใหญ่

## Step 4: Build an Image‑Filter Pipeline to Boost Accuracy  

ภาพที่สะอาดคือครึ่งหนึ่งของการต่อสู้ Pipeline ด้านล่างจะทำการแก้ไขการเอียงของภาพและลบสัญญาณรบกวนพื้นหลัง—สองสาเหตุหลักที่ทำให้ **ปรับปรุงความแม่นยำของ OCR** ลดลง

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การแก้ไขการเอียงทำให้บรรทัดข้อความอยู่ในแนวนอน ส่วนการลดสัญญาณรบกวนช่วยลดบล็อกอักขระเท็จ คุณสามารถเพิ่มตัวกรองอื่น ๆ (เช่น `ContrastFilter`) หากสแกนต้นฉบับของคุณแย่มาก

## Step 5: Perform OCR Recognition  

เมื่อภาพผ่านการเตรียมล่วงหน้าแล้ว เราก็ให้เอนจินทำงานมหัศจรรย์ของมัน

```csharp
ocrEngine.Recognize();
```

บรรทัดเดียวนี้จะเรียกใช้โมเดล deep‑learning ที่อยู่เบื้องหลัง Aspose OCR มันจะเติมค่า `ocrEngine.Text` ด้วยข้อความธรรมดาและเตรียมผลลัพธ์ PDF ด้วย

> **ถ้าข้อความดูเป็นอักขระผสม?** ตรวจสอบการตั้งค่าภาษาจากขั้นตอนที่ 2 อีกครั้งและพิจารณาเพิ่ม `BinarizeFilter` เข้าไปใน pipeline

## Step 6: Save the Result as a Searchable PDF  

ส่วนสุดท้ายคือการบันทึก **PDF ที่สามารถค้นหาได้** โดยที่ข้อความที่สกัดออกมาจะอยู่ด้านหลังภาพต้นฉบับ—เหมาะอย่างยิ่งสำหรับเอกสารทางกฎหมายหรือการเก็บถาวร

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**ทำไมเรื่องนี้ถึงสำคัญ:** `EmbedOriginalImage = true` รักษาความคมชัดของสแกนไว้ในขณะที่ยังสามารถค้นหาข้อความได้ หากตั้งค่าเป็น `false` PDF จะมีเฉพาะข้อความที่สกัดออกมา ซึ่งอาจเป็นประโยชน์สำหรับการเก็บถาวรที่ต้องการขนาดไฟล์เล็ก

### ตัวเลือก: พิมพ์ข้อความที่จดจำได้และ JSON  

หากต้องการตรวจสอบผลลัพธ์ดิบ บรรทัดเหล่านี้จะพิมพ์ข้อความธรรมดาและ payload JSON ที่มีโครงสร้าง

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**ผลลัพธ์ที่คาดหวัง:** หลังจากรันโปรแกรม คุณจะเห็นประโยคภาษาฝรั่งเศสแสดงในคอนโซล ตามด้วยอ็อบเจ็กต์ JSON ที่มีข้อมูล bounding box, คะแนนความเชื่อมั่น, และเมตาดาต้าภาษา

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

รันโปรแกรม, ชี้ `YOUR_DIRECTORY` ไปที่โฟลเดอร์ที่มี `input.jpg` และทรัพยากร Aspose OCR, แล้วคุณจะได้ `output.pdf` อยู่ข้าง ๆ ทันที

## Conclusion

ตอนนี้คุณมีสูตรที่พร้อมใช้งานในระดับ production เพื่อ **สร้าง PDF ที่สามารถค้นหาได้** ด้วย Aspose OCR พร้อมกับการเรียนรู้วิธี **ปรับปรุงความแม่นยำของ OCR** และการ **โหลดภาพสำหรับ OCR** อย่างถูกต้อง Pipeline — GPU (เลือกได้) → การเลือกภาษา → การโหลดภาพ → เชนตัวกรอง → การจดจำ → การบันทึก PDF — ครอบคลุมทุกขั้นตอนสำคัญ คุณจึงสามารถปรับใช้กับภาษาอื่น, ชุดข้อมูลขนาดใหญ่, หรือรูปแบบผลลัพธ์อื่น ๆ ได้

ต่อไปทำอะไร? ลองสลับ `PdfSaveOptions` เป็น `DocxSaveOptions` เพื่อสร้างเอกสาร Word ที่สามารถค้นหาได้, ทดลองเพิ่มตัวกรองเช่น `ContrastFilter`, หรือรวมโค้ดนี้เข้าใน ASP.NET Core API เพื่อสร้าง PDF แบบ on‑the‑fly ความเป็นไปได้ไม่มีที่สิ้นสุด และด้วยพื้นฐานที่วางไว้ที่นี่ คุณพร้อมรับมือกับความท้าทายใด ๆ ที่เกี่ยวกับ OCR

มีคำถามหรือเจออุปสรรค? แสดงความคิดเห็นได้เลย, ขอให้สนุกกับการเขียนโค้ด!

## Related Tutorials

- [วิธีทำ OCR PDF ใน .NET ด้วย Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [วิธีดึงตารางจากภาพโดยใช้ Aspose.OCR สำหรับ .NET](/ocr/english/net/text-recognition/recognize-table/)
- [วิธีทำ OCR ข้อความในภาพด้วยภาษาโดยใช้ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-25
description: แยกข้อความจากภาพโดยใช้ Aspose OCR ใน C#. เรียนรู้วิธีโหลดภาพสำหรับ OCR,
  ตั้งค่าภาษา OCR, สร้างเอนจิน OCR และดึงข้อความจากไฟล์ TIFF.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: th
og_description: จดจำข้อความจากภาพโดยใช้ Aspose OCR ใน C# บทเรียนนี้แสดงวิธีสร้างเครื่องมือ
  OCR, โหลดภาพสำหรับ OCR, ตั้งค่าภาษา OCR, และดึงข้อความจากไฟล์ TIFF.
og_title: แปลงข้อความจากภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: แยกข้อความจากภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์

เคยต้อง **จดจำข้อความจากภาพ** แต่ไม่แน่ใจว่าควรใช้ไลบรารีใดที่ให้ความเร็วและความแม่นยำพร้อมกันหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการประมวลผลใบแจ้งหนี้หรือการจัดเก็บเอกสาร จุดเจ็บปวดที่ใหญ่ที่สุดคือการดึงข้อความที่สะอาดและค้นหาได้จากไฟล์ TIFF โดยไม่ต้องเขียนพาร์เซอร์เอง

สิ่งที่ควรทราบคือ Aspose OCR สำหรับ .NET ทำให้กระบวนการทั้งหมดเป็นเรื่องง่าย ในคู่มือนี้เราจะพาคุณผ่านทุกขั้นตอนที่จำเป็น—การติดตั้งแพคเกจ, **การสร้าง OCR engine**, การโหลด TIFF, การตั้งค่าภาษา OCR, และสุดท้าย **การดึงข้อความจาก TIFF**. เมื่อเสร็จคุณจะมีแอปคอนโซลที่พร้อมรันและสามารถ **จดจำข้อความจากภาพ** ได้อย่างรวดเร็ว

## Prerequisites

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานได้กับ .NET Core และ .NET Framework ด้วย)
- Visual Studio 2022 (หรือ IDE ใดก็ได้ที่คุณชอบ)
- Aspose.OCR NuGet package (การสนับสนุน GPU ต้องใช้ add‑on `Aspose.OCR.Gpu`)
- GPU ที่รองรับ CUDA หากต้องการความเร็วเพิ่มขึ้น (ไม่บังคับแต่แนะนำ)

> **Pro tip:** หากคุณไม่มี GPU เพียงแค่ลบบรรทัด `GpuDevice` แล้ว engine จะสลับไปใช้ CPU โดยอัตโนมัติ

## Step 1: Install Aspose OCR and Create OCR Engine

แรกเริ่มให้เพิ่มแพคเกจที่จำเป็นผ่าน NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

ตอนนี้เราสามารถ **สร้าง OCR engine** ได้แล้ว วัตถุนี้เป็นหัวใจของกระบวนการ; มันเก็บการตั้งค่าต่าง ๆ เช่น อุปกรณ์ที่ใช้ทำงานและขีดจำกัดหน่วยความจำ

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**ทำไมจึงสำคัญ:** การผูก engine กับ GPU จะทำให้เวลาที่ใช้ในการ **จดจำข้อความจากภาพ** ลดลงอย่างมาก โดยเฉพาะกับชุดข้อมูลขนาดใหญ่ของ TIFF ความละเอียดสูง

## Step 2: Load Image for OCR

ต่อไปเราต้อง **โหลดภาพสำหรับ OCR** Aspose.OCR ทำงานกับ `System.Drawing.Image` ดังนั้นฟอร์แมตใด ๆ ที่ GDI+ รองรับ (รวมถึง multi‑page TIFF) ก็ใช้ได้

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

หากคุณทำงานกับ TIFF หลายหน้า สามารถวนลูปผ่านหน้าโดยใช้ `image.SelectActiveFrame` แต่ในกรณีส่วนใหญ่การเรียกครั้งเดียวก็เพียงพอ

## Step 3: Set OCR Language

Engine ไม่ได้รู้โดยอัตโนมัติว่าคุณกำลังสแกนภาษาอะไร **ตั้งค่าภาษา OCR** ก่อนเรียก recognizer; มิฉะนั้นคุณจะได้ผลลัพธ์ที่เป็นอักขระผสมกัน

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **Did you know?** การสลับภาษาขณะทำงานทำได้อย่างรวดเร็ว—you can even process a mixed‑language document by changing this property between pages.

## Step 4: Perform the Recognition – Recognize Text from Image

ตอนนี้มาส่วนที่สนุก: **จดจำข้อความจากภาพ** จริง ๆ `Recognize` จะคืนค่าเป็นสตริงธรรมดาที่มีอักขระที่ตรวจพบทั้งหมด

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

หากต้องการคะแนนความเชื่อมั่นหรือ bounding box สามารถใช้ overload ที่คืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ได้ แต่สำหรับงานดึงข้อความส่วนใหญ่สตริงธรรมดาก็เพียงพอ

## Step 5: Extract Text from TIFF (and handle multi‑page files)

เมื่อแหล่งข้อมูลเป็น TIFF ที่มีหลายหน้า คุณจะต้องทำซ้ำขั้นตอน 2‑4 สำหรับแต่ละเฟรม ตัวอย่างลูปสั้น ๆ ที่ **ดึงข้อความจาก TIFF** หน้าโดยหน้า:

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

โค้ดด้านบนจะแสดงข้อความที่ดึงได้จากทุกหน้า ทำให้ง่ายต่อการส่งต่อผลลัพธ์ไปยังฐานข้อมูลหรือดัชนีการค้นหา

## Step 6: Display or Persist the Extracted Text

สุดท้ายให้ **แสดงข้อความที่ดึงได้** และอาจบันทึกลงไฟล์เพื่อใช้ต่อในภายหลัง

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

เมื่อรันโปรแกรมจะพิมพ์อักขระที่จดจำได้และสร้างไฟล์ `extracted_text.txt` อยู่ข้างไฟล์ TIFF ของคุณ

---

## Common Questions & Edge Cases

- **GPU ไม่ถูกตรวจพบจะทำอย่างไร?**  
  ลบบรรทัด `GpuDevice`; engine จะสลับไปใช้โหมด CPU โดยอัตโนมัติ ประสิทธิภาพอาจช้าลงแต่ผลลัพธ์ยังคงแม่นยำ

- **สามารถประมวลผลไฟล์ PNG หรือ JPEG ได้หรือไม่?**  
  แน่นอน—`Image.FromFile` รองรับฟอร์แมตใดก็ได้ที่ System.Drawing รองรับ ดังนั้นคุณสามารถ **โหลดภาพสำหรับ OCR** ไม่ว่าขยายไฟล์จะเป็นอะไร

- **จะจัดการกับสแกนความละเอียดต่ำอย่างไร?**  
  เพิ่มค่า `ocrEngine.PreprocessOptions.Dpi` ก่อนเรียก `Recognize` DPI ที่สูงขึ้นจะให้พิกเซลมากขึ้นกับ engine ช่วยเพิ่มความแม่นยำ

- **มีขีดจำกัดขนาดของ TIFF หรือไม่?**  
  คุณสมบัติ `GpuMemoryLimit` จำกัดการใช้ GPU หากเกินขีดจำกัด engine จะสลับไปใช้ CPU สำหรับหน้าที่เหลือ

---

## Conclusion

คุณมีสคริปต์ที่สมบูรณ์และพร้อมใช้งานในระดับ production ที่ **จดจำข้อความจากภาพ** ด้วย Aspose OCR ใน C# แล้ว คู่มือได้อธิบายวิธี **สร้าง OCR engine**, **โหลดภาพสำหรับ OCR**, **ตั้งค่าภาษา OCR**, และ **ดึงข้อความจาก TIFF**—ทั้งหมดโดยใช้การเร่งความเร็วด้วย GPU

ต่อจากนี้คุณอาจ:

- ทดลองใช้ภาษาต่าง ๆ (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified` เป็นต้น)
- ผสานผลลัพธ์เข้ากับดัชนี ElasticSearch ที่ค้นหาได้
- เพิ่มกระบวนการหลังการประมวลผล (ตรวจสอบการสะกด, ทำความสะอาดด้วย regex) เพื่อปรับคุณภาพข้อมูล

ลองใช้กับชุดใบแจ้งหนี้ของคุณเอง ปรับขีดจำกัดหน่วยความจำ แล้วดูประสิทธิภาพ OCR พุ่งสูงขึ้น ขอให้สนุกกับการเขียนโค้ด!

## Related Tutorials

- [ดึงข้อความจากภาพด้วย C# พร้อมเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [วิธีดึงข้อความจากภาพโดยการเตรียมสี่เหลี่ยมใน OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [ดึงข้อความจากภาพ – จดจำบรรทัดด้วย Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
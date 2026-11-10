---
category: general
date: 2026-02-13
description: เรียนรู้วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากไฟล์รูปภาพ, เปิดใช้งานการประมวลผลด้วย
  GPU, และแปลงการสแกนเป็นข้อความอย่างรวดเร็ว.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: th
og_description: วิธีใช้ OCR ใน C#? คู่มือนี้จะแสดงวิธีดึงข้อความจากไฟล์รูปภาพ, เปิดใช้งานการประมวลผลด้วย
  GPU, และแปลงการสแกนเป็นข้อความ.
og_title: วิธีใช้ OCR ใน C# – แยกข้อความจากรูปภาพด้วย GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: วิธีใช้ OCR ใน C# – แยกข้อความจากภาพด้วย GPU
url: /th/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – ดึงข้อความจากรูปภาพด้วย GPU

เคยสงสัย **วิธีใช้ OCR** เพื่อดึงข้อความออกจากเอกสารสแกนโดยไม่ต้องเหนื่อยไหม? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักถามว่า “ฉันจะดึงข้อความจากไฟล์รูปภาพได้อย่างมีประสิทธิภาพอย่างไร?” ข่าวดีคือด้วย Aspose.OCR คุณทำได้เช่นนั้น และคุณยังสามารถ **เปิดใช้งานการประมวลผลด้วย GPU** เพื่อเพิ่มความเร็วที่เห็นได้ชัดบนฮาร์ดแวร์ที่รองรับ

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างครบวงจรที่แสดงให้คุณเห็น **วิธีใช้ OCR**, วิธี **ดึงข้อความจากรูปภาพ**, วิธี **แปลงสแกนเป็นข้อความ**, และวิธีจัดการเมื่อ GPU ไม่พร้อมใช้งาน เมื่อเสร็จคุณจะมีแอปคอนโซล C# ที่พร้อมรันซึ่งพิมพ์ข้อความที่จดจำได้และบอกว่ามีการใช้ GPU จริงหรือไม่

## สิ่งที่คุณต้องการ

- .NET 6 SDK หรือรุ่นใหม่กว่า (โค้ดทำงานกับ .NET Core ด้วย)  
- Visual Studio 2022 หรือโปรแกรมแก้ไขที่คุณชอบ  
- แพ็กเกจ Aspose.OCR สำหรับ .NET (สามารถติดตั้งผ่าน NuGet)  
- ไฟล์รูปภาพความละเอียดสูง (เช่น `highres_scan.tif`) สำหรับทดสอบ  

ไม่ต้องตั้งค่าซับซ้อน—แค่รันคำสั่ง NuGet ไม่กี่คำสั่งแล้วคุณก็พร้อมใช้งาน

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR และเตรียมโปรเจกต์

ก่อนอื่นคุณต้องนำไลบรารี OCR เข้ามาในโปรเจกต์ของคุณ เปิดเทอร์มินัลในโฟลเดอร์โซลูชันและรัน:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

คำสั่งนี้จะสร้างโปรเจกต์คอนโซลใหม่ชื่อ **OcrDemo** และเพิ่มแพ็กเกจ `Aspose.OCR` ผ่าน NuGet ไลบรารีนี้มีคลาส `OcrEngine` ที่เราจะใช้

> **Pro tip:** หากคุณใช้เครื่องที่มี GPU แยกเฉพาะ โปรดตรวจสอบให้แน่ใจว่าติดตั้งไดรเวอร์กราฟิกล่าสุดแล้ว; มิฉะนั้นไลบรารีจะย้อนกลับไปใช้โหมด CPU โดยอัตโนมัติ

## ขั้นตอนที่ 2: เขียนโค้ด OCR แบบครบถ้วน

ตอนนี้เปิดไฟล์ `Program.cs` แล้วแทนที่เนื้อหาด้วยโค้ดต่อไปนี้ ทุกบรรทัดมีคอมเมนต์เพื่อให้คุณเห็น *ทำไม* เราถึงทำเช่นนั้น

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

- **ProcessingMode = Gpu** บอกเอนจินให้ลองใช้ GPU ก่อน ไลบรารีจะจัดการการเรียก CUDA/OpenCL ระดับต่ำให้คุณ ไม่ต้องจัดการคอนเท็กซ์อุปกรณ์เอง  
- **IsGpuEnabled** เป็นบูลีนที่ยืนยันว่าเส้นทาง GPU ทำงานสำเร็จหรือไม่ หากคุณเห็น `false` เอนจินจะย้อนกลับไปใช้ CPU โดยอัตโนมัติ—ไม่มีอะไรต้องกังวล  
- **RecognizeImage** ทำงานหนักทั้งหมด: โหลดรูปภาพ, รันโมเดล OCR, และคืนผลลัพธ์เป็นข้อความธรรมดา ไม่จำเป็นต้องทำการพรีโพรเซสภาพบิตแมพด้วยตนเอง เว้นแต่คุณมีความต้องการพิเศษ (เช่น การแก้ไขการเอียง)

## ขั้นตอนที่ 3: รันแอปพลิเคชันและตรวจสอบผลลัพธ์

คอมไพล์และเรียกใช้:

```bash
dotnet run
```

หากทุกอย่างตั้งค่าอย่างถูกต้อง คุณจะเห็นข้อความประมาณนี้:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

หาก GPU ไม่พร้อมใช้งาน บรรทัดแรกจะเป็น `GPU used: False` แต่ข้อความที่ดึงออกมาจะยังคงปรากฏ—ขอบคุณการย้อนกลับอย่างราบรื่น

> **Common question:** *ถ้ารูปของฉันเป็น JPEG แทน TIFF จะทำอย่างไร?*  
> เมธอด `RecognizeImage` รองรับรูปแบบใดก็ได้ที่ .NET’s `System.Drawing` รองรับ (JPEG, PNG, BMP ฯลฯ) เพียงเปลี่ยนนามสกุลไฟล์ใน `imagePath`

## ขั้นตอนที่ 4: ตัวเลือก – ปรับการตั้งค่าเพื่อความแม่นยำที่ดีกว่า

Aspose.OCR มีตัวเลือกให้คุณปรับได้หลายอย่าง:

| การตั้งค่า | ทำอะไร | เมื่อใดควรใช้ |
|-----------|--------|--------------|
| `ocrEngine.Language` | บังคับใช้ภาษาที่ระบุ (เช่น `OcrLanguage.English`) | หากคุณรู้ภาษาของเอกสาร |
| `ocrEngine.PageSegMode` | ควบคุมวิธีที่เอนจินแยกหน้าเป็นบล็อก | สำหรับเลย์เอาต์หลายคอลัมน์ |
| `ocrEngine.DetectOrientation` | หมุนข้อความอัตโนมัติเมื่อไม่ตรงแนวตั้ง | การสแกนที่อาจกลับหัว |

คุณสามารถตั้งค่าคุณสมบัติเหล่านี้ก่อนเรียก `RecognizeImage` ตัวอย่างเช่น:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## ขั้นตอนที่ 5: แสดงภาพกระบวนการ (รูปภาพพร้อมข้อความแทน)

ด้านล่างเป็นแผนภาพง่าย ๆ ที่อธิบาย **วิธีใช้ OCR** พร้อมการเร่งความเร็วด้วย GPU (ไม่จำเป็นต่อการทำงานของโค้ด) แต่ช่วยให้คุณมองเห็นภาพรวมได้ชัดเจน

![แผนภาพแสดงวิธีใช้ OCR พร้อมการประมวลผลด้วย GPU](/images/ocr-gpu-flow.png)

*ข้อความแทน:* *แผนภาพแสดงวิธีใช้ OCR พร้อมการประมวลผลด้วย GPU, เน้นการย้อนกลับไปใช้ CPU เมื่อจำเป็น.*

## กรณีขอบและการแก้ไขปัญหา

1. **Out‑of‑Memory on GPU** – รูปภาพขนาดใหญ่มากอาจเกินหน่วยความจำของ GPU ในกรณีนั้น ไลบรารีจะย้อนกลับไปใช้ CPU โดยอัตโนมัติ คุณสามารถปรับขนาดรูปภาพล่วงหน้าเพื่อให้การใช้หน่วยความจำน้อยลง  
2. **Unsupported Image Format** – หาก `RecognizeImage` โยน *NotSupportedException* ให้ตรวจสอบนามสกุลไฟล์และตรวจสอบว่ารูปภาพไม่เสียหาย การแปลงเป็น PNG มักแก้ปัญหาได้  
3. **Low Confidence Scores** – เมื่อผล OCR มีอักขระที่อ่านไม่ออกหลายตัว ให้พิจารณาการพรีโพรเซส (เช่น การทำไบนารีเซชัน, การกำจัดสัญญาณรบกวน) หรือสแกนด้วยความละเอียดสูงกว่า  

## สรุป: สิ่งที่เราได้ทำ

เราได้อธิบาย **วิธีใช้ OCR** ในแอปคอนโซล C# แสดงวิธี **ดึงข้อความจากรูปภาพ** และแสดงวิธี **เปิดใช้งานการประมวลผลด้วย GPU** เพื่อให้ได้ผลลัพธ์ที่เร็วขึ้น ตอนนี้คุณรู้วิธี **แปลงสแกนเป็นข้อความ**, ตรวจสอบว่า GPU ถูกใช้จริงหรือไม่, และปรับการตั้งค่าบางอย่างสำหรับกรณีขอบ

### ขั้นตอนต่อไป

- ลองนำผลลัพธ์ไปใส่ใน **ดัชนีการค้นหา** (เช่น Elasticsearch) เพื่อให้ PDF ที่สแกนของคุณสามารถค้นหาได้  
- ทดลอง **การประมวลผลเป็นชุด** — วนลูปผ่านโฟลเดอร์ของรูปภาพและบันทึกผลแต่ละไฟล์เป็นไฟล์ `.txt`  
- ผสาน OCR กับ **API การแปลภาษา** เพื่อแปลเอกสารสแกนภาษาต่างประเทศโดยอัตโนมัติ  

มีคำถามเพิ่มเติมหรือไม่? ทิ้งคอมเมนต์ไว้ได้เลย, ขอให้เขียนโค้ดสนุก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
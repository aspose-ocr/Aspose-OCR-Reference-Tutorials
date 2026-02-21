---
category: general
date: 2026-02-20
description: จดจำข้อความจากภาพอย่างรวดเร็วด้วยการเร่งความเร็วด้วย GPU ของ Aspose OCR.
  เรียนรู้วิธีดึงข้อความจากการสแกนใน C# ด้วยตัวอย่างที่สมบูรณ์และสามารถรันได้.
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: th
og_description: จดจำข้อความจากภาพโดยใช้การเร่งด้วย GPU. บทเรียนนี้จะแสดงวิธีการดึงข้อความจากการสแกนใน
  C# โดยใช้ Aspose OCR พร้อมด้วยโค้ดและเคล็ดลับครบถ้วน.
og_title: แยกข้อความจากภาพโดยใช้ Aspose OCR GPU – คู่มือ C#
tags:
- Aspose
- OCR
- C#
- GPU
title: แยกข้อความจากภาพโดยใช้ Aspose OCR GPU ใน C#
url: /th/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

.

Also keep the "Pro tip:" etc.

Make sure to keep markdown syntax.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากภาพโดยใช้ Aspose OCR GPU ใน C#

เคยต้อง **จดจำข้อความจากภาพ** แต่ไฟล์ใหญ่จน CPU ทำงานช้าไหม? บางทีคุณอาจลองใช้ไลบรารี OCR ธรรมดาแล้วต้องรอนาน หรือผลลัพธ์ออกมาขาดตกบกพร่อง ข่าวดีคืออะไร? ด้วยการเร่งความเร็วด้วย GPU ของ Aspose OCR คุณสามารถแปลงไฟล์ TIFF สแกนขนาดใหญ่ให้เป็นข้อความที่ค้นหาได้ในไม่กี่วินาที

ในบทความนี้เราจะพาคุณผ่านตัวอย่างเต็มรูปแบบที่พร้อมคัดลอก‑วาง ซึ่งจะแสดงวิธี **ดึงข้อความจากไฟล์สแกน** บนเครื่องที่เปิดใช้งาน GPU ไม่ต้องอ้างอิงแบบคลุมเครือ เพียงโค้ดที่คุณต้องการ เหตุผลที่แต่ละบรรทัดสำคัญ และข้อควรระวังบางอย่างเพื่อไม่ให้คุณต้องบิดหัว

## สิ่งที่คุณต้องเตรียม

- **.NET 6+** (หรือ .NET Framework 4.7+ – API ทำงานเหมือนกัน)
- **Aspose.OCR for .NET** NuGet package (เวอร์ชัน 23.12 หรือใหม่กว่า)
- **GPU** ที่รองรับ CUDA (ไม่บังคับ แต่เร็วมาก)
- ภาพสแกนความละเอียดสูง (เช่น `large_doc.tif`)

หากคุณไม่มี GPU เngine จะสลับไปใช้ CPU โดยอัตโนมัติ – คุณยังสามารถรันตัวอย่างได้ แต่อาจช้ากว่านิดหน่อย

## ขั้นตอนที่ 1 – ติดตั้งแพ็กเกจ Aspose.OCR

เปิดเทอร์มินัลหรือ Package Manager Console แล้วรัน:

```bash
dotnet add package Aspose.OCR
```

หรือใน Visual Studio’s NuGet UI ค้นหา **Aspose.OCR** แล้วคลิก *Install* ซึ่งจะดึงไลบรารี OCR หลักพร้อมกับ assembly สำหรับการเร่งความเร็วด้วย GPU

> **เคล็ดลับ:** หลังติดตั้งแล้วตรวจสอบโฟลเดอร์ `packages` เพื่อหา `Aspose.OCR.Acceleration.dll` ไฟล์นี้จำเป็นสำหรับการสนับสนุน GPU; หากคุณรันบนเซิร์ฟเวอร์แบบ headless สามารถละเว้นได้และโค้ดยังคงคอมไพล์ได้

## ขั้นตอนที่ 2 – เริ่มต้น GPU‑Accelerated OCR Engine

คลาส `GpuOcrEngine` จะตรวจจับ GPU ที่เข้ากันได้โดยอัตโนมัติ หากมีอุปกรณ์หลายตัวคุณสามารถเลือกได้ แต่ส่วนใหญ่ผู้พัฒนาจะปล่อยให้มันตัดสินใจเอง

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**ทำไมต้องทำเช่นนี้:** การเริ่มต้น engine ครั้งเดียวช่วยลดค่าโอเวอร์เฮด หากคุณสร้างและทำลาย engine ซ้ำ ๆ ภายในลูป จะสูญเสียประสิทธิภาพที่ได้จาก GPU

## ขั้นตอนที่ 3 – โหลดภาพสแกนความละเอียดสูงของคุณ

Aspose OCR ทำงานกับ `System.Drawing.Image` ตรวจสอบให้แน่ใจว่าเส้นทางไฟล์ชี้ไปยังภาพจริง มิฉะนั้นจะเกิด `FileNotFoundException`

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **กรณีขอบ:** หากภาพใหญ่กว่า 10 000 × 10 000 px ควรทำการ down‑sampling ก่อน เพราะหน่วยความจำของ GPU มีข้อจำกัด และการโหลดบิตแมปขนาดมหาศาลอาจทำให้เกิด `OutOfMemoryException`

## ขั้นตอนที่ 4 – ทำ OCR ด้วยการตั้งค่าภาษาเริ่มต้น (Latin)

เมธอด `Recognize` จะคืนค่าเป็นสตริงธรรมดา คุณสามารถส่งอ็อบเจกต์ `OcrOptions` หากต้องการภาษาอื่นหรือการประมวลผลล่วงหน้าแบบกำหนดเอง

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**ทำไมค่าตั้งต้นถึงใช้ได้:** เอกสารสแกนส่วนใหญ่—สัญญา, ใบแจ้งหนี้, รายงาน—ใช้ตัวอักษรละติน หากต้องการ Cyrillic, Arabic หรือ Chinese ให้ตั้งค่า `ocrEngine.Language = "ru"` (หรือรหัส ISO ที่เหมาะสม) ก่อนเรียก `Recognize`

## ขั้นตอนที่ 5 – แสดงหรือบันทึกข้อความที่ดึงออกมา

เพื่อเช็คอย่างเร็ว เราจะเขียนผลลัพธ์ลงคอนโซล ในแอปจริงคุณอาจบันทึกลงฐานข้อมูล, ไฟล์ `.txt` หรือส่งต่อไปยังดัชนีการค้นหา

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หาก `large_doc.tif` มีย่อหน้าง่าย ๆ เช่น “Hello, world!” คุณจะเห็น:

```
Hello, world!
```

สำหรับสแกนหลายหน้า engine จะต่อข้อความตามลำดับการอ่าน คุณสามารถแยกหน้าได้ภายหลังโดยใช้การขึ้นบรรทัดใหม่ (`\n`) หากต้องการกำหนดขอบเขตหน้า

## การจัดการกับปัญหาที่พบบ่อย

| ปัญหา | อาการ | วิธีแก้ |
|-------|---------|-----|
| **ไม่พบ GPU** | `ocrEngine.Device` เป็น `null` และการประมวลผลช้า | ติดตั้งไดรเวอร์ NVIDIA ล่าสุดและ CUDA Toolkit (v11+) ตรวจสอบด้วย `nvidia-smi` |
| **การเก็บกวาดหน่วยความจำล่าช้า** | หน่วยความจำพุ่งขึ้นหลังประมวลผลหลายภาพ | เรียก `scannedImage.Dispose()` หลัง OCR หรือห่อภาพด้วยบล็อก `using` |
| **ภาษาไม่ถูกต้อง** | ตัวอักษรแสดงเป็นอักขระผิด | ตั้งค่า `ocrEngine.Language` ให้เป็นรหัส ISO 639‑1 ที่ถูกต้องก่อน `Recognize` |
| **ไฟล์ใหญ่มาก** | `OutOfMemoryException` | ลดขนาดด้วย `Image.GetThumbnailImage` หรือแบ่งสแกนเป็นหลายส่วน (tiles) |

## ตัวอย่างเต็มพร้อมรัน

ด้านล่างเป็นโปรแกรมทั้งหมด — รวม `using` directives, การจัดการข้อผิดพลาด, และบล็อก `using` ที่เรียบร้อยสำหรับภาพ:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### สิ่งที่โค้ดนี้ทำ

1. **สร้าง** `GpuOcrEngine` ที่เลือก GPU ที่ดีที่สุดโดยอัตโนมัติ  
2. **โหลด** ไฟล์ TIFF เป้าหมายภายในบล็อก `using` เพื่อรับประกันการทำลายทรัพยากร  
3. **เรียก** `Recognize` เพื่อแปลงบิตแมปเป็นสตริง  
4. **เขียน** ผลลัพธ์ลงคอนโซลและไฟล์ `.txt` ที่อยู่ข้างไฟล์ต้นฉบับ  
5. **ดักจับ** ข้อยกเว้นใด ๆ และพิมพ์ข้อความแสดงข้อผิดพลาดที่เป็นมิตร  

## ก้าวต่อไป – จาก “recognize text from image” สู่ Pipeline เอกสารระดับเต็ม

เมื่อคุณสามารถ **ดึงข้อความจากไฟล์สแกน** ได้แล้ว ลองทำตามขั้นตอนต่อไปนี้:

- **ประมวลผลเป็นชุด:** วนลูปโฟลเดอร์ของ TIFFs แล้วรวมผลลัพธ์เป็นดัชนีที่ค้นหาได้หนึ่งเดียว  
- **ตรวจจับภาษาอัตโนมัติ:** ใช้ `ocrEngine.DetectLanguage()` (ถ้ามี) เพื่อสลับภาษาโดยอัตโนมัติ  
- **หลังการประมวลผล:** ส่งผลลัพธ์ผ่านตัวตรวจสอบการสะกดหรือฟิลเตอร์ regex เพื่อทำความสะอาด artefacts ของ OCR  
- **รวมกับ Azure Cognitive Search:** ส่งข้อความที่ดึงออกไปยังดัชนีคลาวด์ที่ค้นหาได้ทันที  

แต่ละขั้นตอนล้วนอิงกับรูปแบบหลักเดียวกันที่คุณเพิ่งเห็น — เริ่มต้นครั้งเดียว, ป้อนภาพ, รวบรวมข้อความ

## สรุป

คุณเพิ่งเรียนรู้วิธี **จดจำข้อความจากภาพ** ด้วย engine ที่เร่งด้วย GPU ของ Aspose OCR ใน C# ตัวอย่างที่สมบูรณ์และรันได้แสดงให้เห็นวิธีตั้งค่า engine, โหลดสแกนความละเอียดสูง, ทำ OCR, และจัดการผลลัพธ์ ด้วยเคล็ดลับและการจัดการกรณีขอบด้านบน คุณจะหลีกเลี่ยงปัญหาที่พบบ่อยและได้ผลลัพธ์ที่เชื่อถือได้ ไม่ว่าจะรันบนแล็ปท็อปของนักพัฒนาหรือเซิร์ฟเวอร์ผลิต

พร้อมที่จะเปลี่ยนสแกนเพิ่มเติมให้เป็นข้อมูลที่ค้นหาได้หรือยัง? ลองประมวลผลทั้งโฟลเดอร์, ทดลองกับภาษาที่ไม่ใช่ละติน, หรือส่งผลลัพธ์ไปยังเครื่องมือค้นหาแบบเต็มข้อความ ความเป็นไปได้ไม่มีที่สิ้นสุด และโค้ดที่คุณเพิ่งเขียนเป็นพื้นฐานที่มั่นคงที่คุณต้องการ

Happy coding! 🚀

![recognize text from image example](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-26
description: เรียกใช้ OCR บนรูปภาพด้วยการสนับสนุน GPU ของ Aspose OCR ใน C# เรียนรู้วิธีโหลดรูปภาพสำหรับ
  OCR ตั้งค่า ID ของอุปกรณ์ GPU และดึงข้อความจากรูปภาพอย่างรวดเร็ว.
draft: false
keywords:
- run OCR on image
- extract text from image
- load image for OCR
- recognize text from document
- set GPU device ID
language: th
og_description: เรียกใช้ OCR บนภาพด้วย Aspose OCR GPU ใน C# คู่มือนี้แสดงวิธีโหลดภาพสำหรับ
  OCR ตั้งค่า ID ของอุปกรณ์ GPU และสกัดข้อความจากภาพอย่างมีประสิทธิภาพ
og_title: รัน OCR บนภาพด้วย GPU ใน C# – คู่มือฉบับสมบูรณ์
tags:
- C#
- OCR
- GPU
- Aspose
title: เรียกใช้ OCR บนภาพด้วย GPU ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/ocr-optimization/run-ocr-on-image-with-gpu-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เรียกใช้ OCR บนรูปภาพด้วย GPU ใน C# – คู่มือการเขียนโปรแกรมเต็ม

เคยต้องการ **run OCR on image** ไฟล์แต่พบว่าเวอร์ชัน CPU ช้าอย่างเจ็บปวดไหม? คุณไม่ได้เป็นคนเดียว ในแอปพลิเคชันจริงหลาย ๆ ตัว—เช่น เครื่องสแกนใบแจ้งหนี้หรือคลังเอกสารขนาดใหญ่—คอขวดคือเอนจิน OCR เอง  

ในบทเรียนนี้เราจะพาคุณผ่าน **complete, runnable example** ที่แสดงวิธี **load image for OCR**, ตั้งค่า **GPU device ID** (ถ้าต้องการ) และสุดท้าย **extract text from image** ด้วย API ที่เร่งด้วย GPU ของ Aspose OCR. เมื่อจบคุณจะสามารถ **recognize text from document** จากรูปภาพได้ในส่วนหนึ่งของเวลาที่วิธีใช้ CPU อย่างเดียวต้องใช้

## สิ่งที่คุณจะได้เรียนรู้

- วิธีติดตั้งและอ้างอิงแพคเกจ Aspose.OCR และ Aspose.OCR.Gpu  
- ขั้นตอนที่แม่นยำเพื่อ **run OCR on image** ด้วยการเร่งด้วย GPU  
- ทำไมการเลือก **GPU device ID** ที่ถูกต้องจึงสำคัญบนเครื่องที่มีหลาย GPU  
- เคล็ดลับในการจัดการไฟล์ขนาดใหญ่, กลยุทธ์ fallback, และข้อผิดพลาดทั่วไป  

### ข้อกำหนดเบื้องต้น

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 or later | คุณลักษณะของภาษาแบบสมัยใหม่และประสิทธิภาพที่ดีกว่า |
| Visual Studio 2022 (or any C# IDE) | เพื่อการตั้งค่าโปรเจกต์ที่ง่าย |
| NVIDIA GPU with CUDA support (optional) | จำเป็นเฉพาะเมื่อคุณต้องการการเร่งความเร็วด้วย GPU |
| Aspose.OCR & Aspose.OCR.Gpu NuGet packages | ให้คลาส `GpuOcrEngine` |

หากคุณไม่มี GPU อย่าตื่นตระหนก—โค้ดจะย้อนกลับไปใช้เอนจิน CPU อย่างอ่อนโยน ซึ่งเราจะอธิบายในส่วนต่อไป

---

## ขั้นตอนที่ 1: ติดตั้งแพคเกจ Aspose OCR

ก่อนที่คุณจะ **run OCR on image** ได้ คุณต้องมีไลบรารีเหล่านี้ เปิดเทอร์มินัล (หรือ Package Manager Console) แล้วรันคำสั่ง:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

แพคเกจสองตัวนี้จะนำเอาเอนจิน OCR หลักและส่วนขยายเฉพาะ GPU มาให้ หลังจากติดตั้งแล้ว คุณจะเห็นการอ้างอิงต่อไปนี้ในไฟล์ `.csproj` ของคุณ:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
  <PackageReference Include="Aspose.OCR.Gpu" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** ควรรักษาเวอร์ชันของแพคเกจให้ตรงกัน; เวอร์ชันที่ไม่ตรงกันอาจทำให้เกิดข้อผิดพลาดขณะรัน

---

## ขั้นตอนที่ 2: สร้าง GPU‑Enabled OCR Engine

ตอนนี้ไลบรารีพร้อมแล้ว ให้เรา **run OCR on image** ด้วย GPU คลาส `GpuOcrEngine` คือจุดเริ่มต้นสำหรับการประมวลผลที่เร่งด้วย GPU

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Instantiate the GPU OCR engine
        var gpuEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Choose which GPU to use – 0 = first GPU
        // This is where the "set GPU device ID" keyword comes into play.
        gpuEngine.DeviceId = 0;

        // The rest of the workflow continues in the following steps...
```

**Why a GPU?**  
คอร์ของ GPU มีประสิทธิภาพสูงในการทำงานแบบขนานกับพิกเซล ซึ่งตรงกับความต้องการของ OCR เมื่อสแกนภาพความละเอียดสูง โดยการตั้งค่า `DeviceId` คุณบอกไลบรารีว่าต้องใช้การ์ดใด—สะดวกมากบนเครื่องที่มีหลาย GPU

---

## ขั้นตอนที่ 3: Load Image for OCR

ก่อนทำการจดจำ คุณต้อง **load image for OCR** Aspose มีเมธอดสเตติกที่สะดวกซึ่งรองรับหลายรูปแบบ (JPEG, PNG, TIFF, ฯลฯ)

```csharp
        // Step 3: Load the image you want to recognize
        // Replace the path with your actual file location.
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");

        // Quick sanity check – ensure the image was loaded.
        if (ocrImage == null)
        {
            Console.WriteLine("Failed to load image. Check the file path.");
            return;
        }
```

> **Edge case:** หากภาพมีขนาดใหญ่กว่า 10 MB ควรทำการลดขนาดลงก่อนเพื่อหลีกเลี่ยงการใช้หน่วยความจำของ GPU จนเต็ม คุณสามารถทำได้ด้วย `ocrImage.Resize(width, height)` ก่อนทำการจดจำ

---

## ขั้นตอนที่ 4: Recognize Text from Document

เมื่อเอนจินพร้อมและภาพถูกโหลดแล้ว ถึงเวลาที่จะ **recognize text from document** เมธอด `Recognize` จะคืนค่าอ็อบเจ็กต์ `OcrResult` ที่มีข้อความแบบ plain‑text และเมตาดาต้าเพิ่มเติม

```csharp
        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);

        // Verify that OCR succeeded
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR failed or returned empty result.");
            return;
        }
```

**What’s happening under the hood?**  
เอนจิน GPU จะส่งข้อมูลพิกเซลไปยังคอร์ด CUDA ซึ่งทำการไบนารีเซชัน, แบ่งอักขระ, และการสรุปผลด้วยเครือข่ายประสาทเทียม—all แบบขนาน นี่คือเหตุผลที่คุณสามารถ **run OCR on image** ที่โดยปกติอาจใช้เวลาหลายนาทีบน CPU

---

## ขั้นตอนที่ 5: Extract Text from Image and Output

สุดท้าย เรา **extract text from image** และแสดงผล คุณยังสามารถบันทึกผลลัพธ์ลงไฟล์, ฐานข้อมูล, หรือส่งต่อไปยัง pipeline NLP ต่อไปได้

```csharp
        // Step 5: Output the recognized plain‑text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // Optional: Save to a .txt file for later processing
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }
}
```

**Expected output** (ตัดทอนเพื่อความกระชับ):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

หากคุณรันโปรแกรมและเห็นบล็อกคล้ายกัน แสดงว่าคุณได้ **run OCR on image** ด้วยการเร่งด้วย GPU สำเร็จแล้ว!  

---

## Handling Situations Without a GPU (Fallback)

ถ้าเครื่องที่คุณจะดีพลอยไม่มี GPU ที่รองรับ คอนสตรัคเตอร์ `GpuOcrEngine` จะโยน `GpuNotSupportedException` ให้ห่อการเริ่มต้นด้วย try‑catch แล้ว fallback ไปใช้ `OcrEngine` (CPU) แบบนี้:

```csharp
        try
        {
            var gpuEngine = new GpuOcrEngine { DeviceId = 0 };
            // Continue with GPU workflow...
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not available – switching to CPU OCR.");
            var cpuEngine = new OcrEngine();
            OcrResult result = cpuEngine.Recognize(ocrImage);
            Console.WriteLine(result.Text);
        }
```

รูปแบบนี้ทำให้แอปของคุณทำงานได้แม้ไม่มีฮาร์ดแวร์ GPU ซึ่งเป็นข้อพิจารณาที่สำคัญสำหรับการดีพลอยบนคลาวด์

---

## Full Working Example (Copy‑Paste Ready)

ด้านล่างเป็น **entire program**—ไม่มีส่วนที่ขาดหาย เพียงเปลี่ยนเส้นทางไฟล์ให้เป็นของคุณเอง

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Create a GPU‑enabled OCR engine
        GpuOcrEngine gpuEngine;
        try
        {
            gpuEngine = new GpuOcrEngine { DeviceId = 0 }; // set GPU device ID
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not detected. Falling back to CPU engine.");
            var cpuEngine = new OcrEngine();
            RunCpuOcr(cpuEngine);
            return;
        }

        // 2️⃣ Load image for OCR
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        if (ocrImage == null)
        {
            Console.WriteLine("Unable to load image – check the path.");
            return;
        }

        // 3️⃣ Recognize text from document
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR returned no text.");
            return;
        }

        // 4️⃣ Extract text from image and output
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }

    // Helper for CPU fallback
    static void RunCpuOcr(OcrEngine cpuEngine)
    {
        var img = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        var result = cpuEngine.Recognize(img);
        Console.WriteLine("=== CPU OCR Result ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Note:** โค้ดข้างต้นจะ **extracts text from image** อัตโนมัติและเขียนผลลัพธ์ลงใน `ocr_result.txt` ปรับเส้นทางตามต้องการ

---

## Frequently Asked Questions & Tips

| Question | Answer |
|----------|--------|
| *Do I need a specific NVIDIA driver?* | ใช่—แนะนำให้ใช้ CUDA 11.x หรือใหม่กว่า ตรวจสอบ release notes ของ Aspose เพื่อความเข้ากันได้ที่แน่นอน |
| *Can I process multiple images concurrently?* | ได้แน่นอน ห่อการเรียก OCR ด้วยลูป `Parallel.ForEach` แต่ต้องระวังขีดจำกัดหน่วยความจำของ GPU |
| *What if the OCR result contains garbled characters?* | ลองปรับการเตรียมภาพก่อนจดจำ: `ocrImage.Binarize()` หรือ `ocrImage.Deskew()` |
| *Is there a way to limit the language model?* | ตั้งค่า `gpuEngine.Language = OcrLanguage.English;` เพื่อเร่งการประมวลผลหากคุณต้องการเฉพาะภาษาอังกฤษ |

---

## Conclusion

คุณมี **complete, end‑to‑end solution** เพื่อ **run OCR on image  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-18
description: ตั้งค่าอุปกรณ์ GPU ใน Aspose OCR เพื่อดึงข้อความจากภาพอย่างรวดเร็ว เรียนรู้วิธีโหลดภาพสำหรับ
  OCR จดจำภาพใบเสร็จและได้ผลลัพธ์ที่แม่นยำ
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: th
og_description: ตั้งค่าอุปกรณ์ GPU ใน Aspose OCR เพื่อดึงข้อความจากภาพอย่างรวดเร็ว
  ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อโหลดภาพสำหรับ OCR และจดจำภาพใบเสร็จ
og_title: ตั้งค่าอุปกรณ์ GPU สำหรับ OCR ใน C# – คู่มือการเขียนโปรแกรมครบถ้วน
tags:
- OCR
- C#
- GPU
- Aspose
title: ตั้งค่าอุปกรณ์ GPU สำหรับ OCR ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่า GPU Device สำหรับ OCR ใน C# – คู่มือการเขียนโปรแกรมเต็มรูปแบบ

ต้องการ **set GPU device** เพื่อให้การประมวลผล OCR เร็วขึ้นหรือไม่? ในคู่มือนี้เราจะพาคุณผ่านขั้นตอนการตั้งค่า GPU device ด้วย Aspose OCR แล้วดึงข้อความจากรูปใบเสร็จในไม่กี่บรรทัดของโค้ด  

หากคุณเคยเจอปัญหา **load image for OCR** หรือสงสัย *how to extract text* จากสแกนความละเอียดสูง คุณมาถูกที่แล้ว เมื่อจบคุณจะได้โปรแกรมที่รันได้ซึ่งจดจำภาพใบเสร็จ พิมพ์ข้อความธรรมดาออกมา และสลับไปใช้ CPU อย่างราบรื่นหากไม่มี GPU

## สิ่งที่บทเรียนนี้ครอบคลุม

เราจะอธิบายทุกอย่างที่คุณต้องรู้:

* การติดตั้งแพคเกจ NuGet ของ Aspose OCR (เป็น dependency ภายนอกเพียงอย่างเดียว)  
* การตั้งค่า GPU device (`set GPU device`) และเลือกดัชนี GPU อื่นได้ตามต้องการ  
* การ **load image for OCR** – ใช่, ขั้นตอนที่หลายคนเริ่มต้นมักพลาด  
* การรันเอนจินจดจำเพื่อ **recognize receipt image**  
* การดึงสตริงผลลัพธ์เพื่อให้คุณ **extract text from image** และนำไปใช้ในแอปของคุณ  

ไม่มีเวทมนตร์ ไม่มีลิงก์เอกสารลับ – เพียงโซลูชันครบถ้วนที่คุณคัดลอก‑วางไปยัง Visual Studio แล้วรันได้ทันที

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานบน .NET Core และ .NET Framework ด้วย)  
* เครื่องที่มี GPU รองรับพร้อมติดตั้งไดรเวอร์ที่เหมาะสม – หากไม่มีไลบรารีจะสลับไปใช้โหมด CPU อัตโนมัติ  
* ตัวอย่างรูปใบเสร็จ (เช่น `receipt_highres.png`) ที่วางไว้ในตำแหน่งที่คุณสามารถอ้างอิงด้วยพาธเต็ม  

เท่านี้ หากยังไม่มีแพคเกจ NuGet ให้รัน `dotnet add package Aspose.OCR` ในโฟลเดอร์โปรเจกต์ของคุณ

---

## ขั้นตอนที่ 1 – Set GPU Device ใน Aspose OCR

สิ่งแรกที่ต้องทำคือ **set GPU device** บน OCR engine ซึ่งบอกให้ Aspose ย้ายงานหนักไปที่การ์ดจอแทน CPU

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**ทำไมจึงสำคัญ:**  
เมื่อเอนจินทำงานใน `ProcessingMode.Gpu` คอร์ CUDA ที่อยู่เบื้องหลังจะเร่งการแยกอักขระและการประมวลผลเครือข่ายประสาทอย่างมหาศาล บน RTX 3080 สมัยใหม่คุณจะเห็นเวลา OCR ลดจากหลายวินาทีเป็นระดับต่ำกว่า 1 วินาทีสำหรับใบเสร็จความละเอียดสูง

> **Pro tip:** หากไม่แน่ใจว่าจะใช้ดัชนี GPU ใด ให้เรียก `OcrEngine.GetAvailableGpuDevices()` (มีในเวอร์ชันใหม่) แล้วเลือกอันที่มีหน่วยความจำว่างมากที่สุด

---

## ขั้นตอนที่ 2 – Load Image for OCR

เมื่อเอนจินตั้งค่าเรียบร้อยแล้ว เราต้อง **load image for OCR** Aspose มีตัวห่อ `ImageStream` ที่สะดวกซึ่งทำหน้าที่เป็น abstraction ของการ I/O ไฟล์และรองรับสตรีมจากหน่วยความจำ เครือข่าย หรือดิสก์

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**อะไรอาจผิดพลาด?**  
หากพาธไฟล์ผิดหรือภาพเสียหาย `FromFile` จะโยน `FileNotFoundException` การตรวจสอบ `File.Exists(imagePath)` ก่อนสร้างสตรีมจะช่วยป้องกันการพังของโปรแกรม

---

## ขั้นตอนที่ 3 – Recognize Receipt Image

เมื่อได้ภาพแล้ว เราเรียก `Recognize` นี่คือขั้นตอนที่จริง ๆ แล้ว **recognize receipt image** ด้วย pipeline ที่เร่งด้วย GPU ที่ตั้งค่าไว้ก่อนหน้า

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**เบื้องหลัง:**  
เอนจินจะเปลี่ยนภาพเป็นบิตแมประดับสีเทาปกติ แล้วรันโมเดล deep‑learning ที่คาดการณ์ความน่าจะเป็นของอักขระ เนื่องจากทำงานบน GPU โมเดลจะประมวลผลบิตแมปทั้งหมดพร้อมกัน ทำให้ใบเสร็จขนาดใหญ่เสร็จเร็วขึ้น

---

## ขั้นตอนที่ 4 – Extract Text from Image and Verify Output

สุดท้าย เราดึงผลลัพธ์เป็นข้อความธรรมดาจาก `OcrResult` แล้วเขียนออกคอนโซล นี่คือจังหวะที่คุณ **extract text from image** และสามารถส่งต่อไปยังตรรกะต่อไป (เช่น การแยกรายการ)

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

หากข้อความดูเป็นอักขระแปลก ๆ ให้ตรวจสอบว่าภาพมีความละเอียดสูงและไดรเวอร์ GPU เป็นเวอร์ชันล่าสุด คุณยังสามารถสลับ `ocrEngine.Settings.PreprocessMode` เพื่อเพิ่มคอนทราสต์ให้กับใบเสร็จที่แสงน้อยได้อีกด้วย

---

## ขั้นตอนที่ 5 – Fallback to CPU (Edge Case Handling)

ถ้าเครื่องเป้าหมายไม่มี GPU ที่รองรับ จะทำอย่างไร? แทนที่จะพัง คุณสามารถตรวจจับสถานการณ์และสลับไปใช้การประมวลผลด้วย CPU

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**ทำไมต้องใส่ส่วนนี้:**  
ใน pipeline CI หรือคอนเทนเนอร์คลาวด์มักรันบนเซิร์ฟเวอร์ไรหัวที่ไม่มี GPU การลดคุณภาพอย่างราบรื่นทำให้โค้ดเดียวทำงานได้ทุกที่

---

## ข้อผิดพลาดทั่วไปและเคล็ดลับปฏิบัติ

| Pitfall | How to Avoid |
|---------|--------------|
| Forgetting to set `ProcessingMode` before loading the image. | Always configure the engine first (Step 1). |
| Using the wrong GPU index (`GpuDeviceId`). | Query available devices or stick with the default `0`. |
| Loading a low‑resolution image, which reduces OCR accuracy. | Aim for at least 300 DPI for receipts. |
| Not disposing `ImageStream` – leads to file locks. | Wrap the stream in a `using` block or call `Dispose()` manually. |
| Ignoring the `IsGpuAvailable` flag on machines without CUDA. | Add the fallback logic from Step 5. |

---

## ตัวอย่างเต็มที่ทำงานได้ (Copy‑Paste Ready)

ด้านล่างเป็นโปรแกรมทั้งหมดพร้อมคอมไพล์ บันทึกเป็น `Program.cs` เพิ่มแพคเกจ Aspose OCR แล้วรัน

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

เมื่อรันโปรแกรมจะพิมพ์ข้อความใบเสร็จที่ดึงออกมาบนคอนโซล เหมือนที่แสดงไว้ก่อนหน้านี้ คุณสามารถนำสตริงนั้นไปใส่ใน parser, ฐานข้อมูล หรือตรรกะธุรกิจอื่น ๆ ที่ต้องการได้

---

## สรุป

เราได้แสดงวิธี **set GPU device** ใน Aspose OCR, **load image for OCR**, และ **recognize receipt image** เพื่อให้คุณ **extract text from image** ด้วยความเร็วสูง ตัวอย่างที่ครบถ้วนและรันได้แสดง “วิธีทำ” และ “ทำไมถึงทำเช่นนั้น” ให้คุณมีพื้นฐานมั่นคงสำหรับโครงการ OCR ด้วย C# ที่ต้องการเร่งด้วย GPU  

พร้อมก้าวต่อไปหรือยัง? ลองทดลองกับ:

* การประมวลผลหลายภาพพร้อมกันด้วย `Parallel.ForEach`  
* การปรับ `ocrEngine.Settings.PreprocessMode` เพื่อผลลัพธ์ที่ดีกว่าในสแกนที่คอนทราสต์ต่ำ  
* การส่งออกผล OCR เป็น JSON เพื่อการวิเคราะห์ต่อไป  

หากมีคำถามหรือเจออุปสรรคใด ๆ อย่าลังเลที่จะคอมเมนต์ และขอให้เขียนโค้ดอย่างสนุกสนาน!

![Diagram showing how to set GPU device for OCR processing](set-gpu-device.png "set GPU device")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
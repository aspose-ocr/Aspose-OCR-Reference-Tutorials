---
category: general
date: 2026-04-03
description: กำหนดขีดจำกัดหน่วยความจำ GPU ด้วย Aspose OCR ใน C#. เรียนรู้วิธีตั้งค่าหน่วยความจำ
  GPU, การจดจำข้อความภาษารัสเซีย, และหลีกเลี่ยงข้อผิดพลาดทั่วไป.
draft: false
keywords:
- set gpu memory limit
- Aspose OCR GPU
- C# GPU OCR
- GPU memory management
- Aspose OcrEngine settings
- limit GPU memory usage
language: th
og_description: ตั้งค่าขีดจำกัดหน่วยความจำ GPU ด้วย Aspose OCR ใน C# บทเรียนนี้แสดงขั้นตอนโดยละเอียดว่าตั้งค่า
  GPU memory อย่างไร, รัน OCR, และจัดการกรณีขอบเขต.
og_title: ตั้งค่าขีดจำกัดหน่วยความจำ GPU ด้วย Aspose OCR – คู่มือ GPU สำหรับ C#
tags:
- Aspose
- OCR
- C#
- GPU
title: ตั้งค่าขีดจำกัดหน่วยความจำ GPU ด้วย Aspose OCR – คู่มือ GPU สำหรับ C#
url: /th/net/ocr-configuration/set-gpu-memory-limit-with-aspose-ocr-c-gpu-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่าขีดจำกัดหน่วยความจำ GPU ด้วย Aspose OCR – คำแนะนำเต็ม C#

เคยต้องการ **ตั้งค่าขีดจำกัดหน่วยความจำ GPU** สำหรับงาน OCR แล้วไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาจำนวนมากเจอปัญหาเมื่อ GPU ของพวกเขาเต็มหน่วยความจำขณะประมวลผลใบเสร็จหรือใบแจ้งหนี้ความละเอียดสูง ข่าวดีคือการสนับสนุน GPU ของ Aspose OCR ช่วยให้คุณจำกัดการใช้หน่วยความจำได้ด้วยไม่กี่บรรทัดของโค้ด เพื่อให้แอปของคุณทำงานเสถียรและยังคงได้รับประโยชน์จากความเร็วของการเร่งด้วยฮาร์ดแวร์

ในคู่มือนี้เราจะพาคุณผ่านขั้นตอนทั้งหมด: การติดตั้ง Aspose OCR พร้อมการสนับสนุน GPU, การกำหนดค่า **GpuSettings** เพื่อ **ตั้งค่าขีดจำกัดหน่วยความจำ GPU**, การรันงาน OCR ภาษารัสเซีย, และการแก้ไขปัญหาที่พบบ่อยที่สุด หลังจากเสร็จคุณจะมีแอปคอนโซล C# ที่สามารถรันได้ซึ่งเคารพข้อจำกัดหน่วยความจำของคุณและคืนข้อความที่สะอาด

## ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK หรือรุ่นที่ใหม่กว่า (API ทำงานกับ .NET Core และ .NET Framework)
- GPU ที่รองรับ CUDA (NVIDIA) หรือ DirectX 12 (Windows)
- Visual Studio 2022 หรือ IDE ใดก็ได้ที่คุณชอบ
- ไฟล์รูปภาพ (`receipt.png`) ที่คุณต้องการประมวลผล
- แพ็กเกจ NuGet **Aspose.OCR** (รุ่นที่เปิดใช้งาน GPU)

> **เคล็ดลับ:** หากคุณอยู่บนเครื่องพัฒนาที่มี GPU RAM จำกัด ให้เริ่มต้นด้วย `MaxMemory = 512` MB และเพิ่มตามความจำเป็นเท่านั้น.

## ขั้นตอนที่ 1: ติดตั้ง Aspose OCR พร้อมการสนับสนุน GPU

ขั้นแรกให้เพิ่มไลบรารี Aspose OCR ที่รวมการเชื่อมต่อ GPU

```bash
dotnet add package Aspose.OCR.Gpu
```

คำสั่งนี้จะดึงทั้ง `Aspose.OCR` และ wrapper ของ GPU (`Aspose.OCR.Gpu`) ไม่จำเป็นต้องติดตั้งไดรเวอร์ระดับระบบเพิ่มเติมนอกจากชุดเครื่องมือ CUDA ที่คุณมีอยู่แล้ว

## ขั้นตอนที่ 2: โหลดภาพที่คุณต้องการประมวลผล

เราจะใช้ `System.Drawing.Image` เพื่ออ่านไฟล์ใบเสร็จ ตรวจสอบให้แน่ใจว่าพาธชี้ไปยังไฟล์ที่มีอยู่จริง; มิฉะนั้นโปรแกรมจะโยน `FileNotFoundException`

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support namespace

class GpuDemo
{
    static void Main()
    {
        // Load the image from disk
        Image receiptImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");
```

**ทำไมเรื่องนี้สำคัญ:** การโหลดภาพตั้งแต่ต้นช่วยให้เราตรวจสอบว่าไฟล์สามารถเข้าถึงได้ก่อนที่เราจะจัดสรรทรัพยากร GPU ใดๆ

## ขั้นตอนที่ 3: สร้าง OCR Engine และ **ตั้งค่าขีดจำกัดหน่วยความจำ GPU**

ตอนนี้เป็นส่วนสำคัญของบทเรียน—การกำหนดค่า `GpuSettings` เพื่อให้ OCR engine **ตั้งค่าขีดจำกัดหน่วยความจำ GPU** เป็นค่าที่ปลอดภัย คุณสมบัติ `MaxMemory` รับค่าเป็นเมกะไบต์

```csharp
        // Initialize the OCR engine with GPU settings
        OcrEngine ocrEngine = new OcrEngine(new GpuSettings
        {
            // Primary keyword in action: set GPU memory limit to 1024 MB
            MaxMemory = 1024,               // limit GPU memory usage (in MB)
            AutoDownloadResources = true   // automatically fetch language packs
        });
```

สังเกตว่าเรา **ตั้งค่าขีดจำกัดหน่วยความจำ GPU** ภายในอ็อบเจกต์ `GpuSettings` นี้บอก Aspose OCR ให้จัดสรรไม่เกิน 1 GB ของ GPU RAM เพื่อป้องกันการล่มจากหน่วยความจำเต็มบน GPU ที่มีขนาดเล็ก

## ขั้นตอนที่ 4: เลือกภาษาการจดจำ

Aspose OCR รองรับภาษากว่า 100 ภาษา สำหรับการสาธิตนี้เราจะจดจำข้อความภาษารัสเซีย แต่คุณสามารถเปลี่ยน `OcrLanguage.Russian` เป็นค่า enum ที่รองรับอื่นได้

```csharp
        // Select the language for OCR
        ocrEngine.Language = OcrLanguage.Russian;
```

หากต้องการประมวลผลหลายภาษาในครั้งเดียว คุณสามารถใช้ `OcrLanguage.Multilingual` หรือรวมแฟล็กต่างๆ

## ขั้นตอนที่ 5: รันกระบวนการ OCR

เมื่อกำหนดค่า engine แล้ว ให้เรียก `Recognize` และส่งภาพที่โหลดไว้ เมธอดจะคืนสตริงที่สกัดออกมา

```csharp
        // Perform OCR on the image
        string recognizedText = ocrEngine.Recognize(receiptImage);

        // Show the result in the console
        Console.WriteLine("GPU OCR result:");
        Console.WriteLine(recognizedText);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนเพื่อความกระชับ):

```
GPU OCR result:
Кассовый чек № 12345
Дата: 03/04/2026
Сумма: 1 250,00 ₽
```

หากขีดจำกัดหน่วยความจำ GPU ของคุณต่ำเกินไป Aspose OCR จะสลับไปประมวลผลด้วย CPU โดยอัตโนมัติ ซึ่งคุณจะเห็นคำเตือนในล็อกคอนโซล

## ขั้นตอนที่ 6: ตรวจสอบว่าขีดจำกัดหน่วยความจำถูกปฏิบัติตาม

Aspose OCR จะเขียนข้อมูลการวินิจฉัยไปยังเอาต์พุตมาตรฐานเมื่อเปิดใช้งาน `AutoDownloadResources` ค้นหาบรรทัดที่คล้ายกับ:

```
[INFO] GPU memory allocated: 987 MB (requested max: 1024 MB)
```

หากปริมาณที่จัดสรรเกินค่าการตั้งค่า `MaxMemory` ของคุณ ให้ตรวจสอบอีกครั้งว่าคุณใช้เวอร์ชันที่ถูกต้องของแพ็กเกจ GPU และไดรเวอร์ของคุณรองรับ API จำกัดหรือไม่

## ข้อผิดพลาดทั่วไป & เคล็ดลับ (คีย์เวิร์ดรองในแอคชัน)

### 1. **Aspose OCR GPU** ไม่ได้รับการจดจำ

- ตรวจสอบว่าคุณได้ import `Aspose.OCR.Gpu` ที่ส่วนหัวของไฟล์แล้ว
- ยืนยันว่าเวอร์ชันของแพ็กเกจ NuGet ตรงกับ .NET runtime ของคุณ (เช่น 23.10 หรือใหม่กว่า)

### 2. **C# GPU OCR** โยน `DllNotFoundException`

- ปกติหมายความว่าห้องสมุด CUDA แบบเนทีฟไม่ได้อยู่ใน `PATH` ของระบบ ติดตั้งชุดเครื่องมือ CUDA ล่าสุดหรือคัดลอก `cudart64_*.dll` ไปยังโฟลเดอร์ที่เป็น executable ของคุณ

### 3. จัดการ **GPU memory management** ด้วยตนเอง

- คุณสามารถเปลี่ยน `MaxMemory` ระหว่างการทำงานได้หากประมวลผลชุดข้อมูลขนาดต่างกัน เพียงสร้าง `OcrEngine` ใหม่ด้วย `GpuSettings` ใหม่ก่อนแต่ละชุด

### 4. ใช้ **Aspose OcrEngine settings** สำหรับการประมวลผลแบบชุด

```csharp
foreach (var file in Directory.GetFiles(@"batch_folder", "*.png"))
{
    Image img = Image.FromFile(file);
    ocrEngine.Language = OcrLanguage.English; // switch language per batch
    string text = ocrEngine.Recognize(img);
    // store or log `text` as needed
}
```

### 5. **จำกัดการใช้หน่วยความจำ GPU** สำหรับเซิร์ฟเวอร์หลายผู้ใช้

- เมื่อหลายบริการแชร์ GPU เดียวกัน ให้จัดสรรส่วนของแต่ละบริการโดยตั้งค่า `MaxMemory` เป็นส่วนหนึ่งของ VRAM ทั้งหมด (เช่น `MaxMemory = totalVRAM / servicesCount`)

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วางเต็มรูปแบบที่ **ตั้งค่าขีดจำกัดหน่วยความจำ GPU**, รัน OCR, และพิมพ์ผลลัพธ์ บันทึกเป็น `Program.cs` แล้วรัน `dotnet run`

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support

class GpuDemo
{
    static void Main()
    {
        // Step 1: Load the image
        Image receiptImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // Step 2: Create OCR engine with GPU settings (set GPU memory limit)
        OcrEngine ocrEngine = new OcrEngine(new GpuSettings
        {
            MaxMemory = 1024,               // limit GPU memory usage to 1 GB
            AutoDownloadResources = true   // fetch language data automatically
        });

        // Step 3: Choose language (Russian in this example)
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 4: Perform OCR
        string recognizedText = ocrEngine.Recognize(receiptImage);

        // Step 5: Display result
        Console.WriteLine("GPU OCR result:");
        Console.WriteLine(recognizedText);
    }
}
```

รันโปรแกรมแล้วคุณจะเห็นข้อความ OCR แสดงบนคอนโซล โดยที่ขีดจำกัดหน่วยความจำ GPU ถูกปฏิบัติตามตลอดการทำงาน

## สรุป

เราเพิ่งสาธิตวิธี **ตั้งค่าขีดจำกัดหน่วยความจำ GPU** เมื่อใช้เครื่องยนต์ GPU ของ Aspose OCR จาก C# โดยการกำหนดค่า `GpuSettings.MaxMemory` คุณจะได้การควบคุมการใช้ VRAM อย่างละเอียด ป้องกันการล่มบน GPU ระดับต่ำ และยังคงได้รับประโยชน์จากประสิทธิภาพของการเร่งด้วยฮาร์ดแวร์ คู่มือได้ครอบคลุมการติดตั้ง, การอธิบายโค้ด, การตรวจสอบ, และเคล็ดลับปฏิบัติสำหรับ **Aspose OCR GPU**, **C# GPU OCR**, และ **GPU memory management**

ต่อไปคุณจะทำอะไร? ลองทดลองกับภาพขนาดใหญ่ขึ้น, ภาษาอื่นๆ, หรือแม้กระทั่งการทำงานพร้อมกันของหลายอินสแตนซ์ `OcrEngine`—แค่จำไว้ว่าต้องทำให้ `MaxMemory` ของแต่ละอินสแตนซ์อยู่ในงบประมาณ VRAM ทั้งหมด หากคุณพบว่าคู่มือนี้เป็นประโยชน์ แชร์ให้ทีมของคุณหรือแสดงความคิดเห็นหากเจอปัญหาใดๆ

ขอให้สนุกกับการเขียนโค้ด และขอให้ GPU ของคุณเย็นสบาย!

![set gpu memory limit example](placeholder-image.png "set gpu memory limit example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
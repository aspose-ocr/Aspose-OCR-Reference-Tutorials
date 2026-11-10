---
category: general
date: 2026-01-13
description: เรียนรู้วิธีจดจำข้อความจากภาพและดึงข้อความจากใบเสร็จอย่างรวดเร็วด้วย
  Aspose OCR รวมขั้นตอนการโหลดภาพสำหรับ OCR และการตั้งค่า GPU device ID
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: th
og_description: จดจำข้อความจากภาพได้ทันทีด้วย Aspose OCR. ทำตามคู่มือขั้นตอนต่อขั้นตอนเพื่อโหลดภาพสำหรับ
  OCR, ตั้งค่า GPU device ID, และดึงข้อความจากใบเสร็จ.
og_title: แยกข้อความจากภาพ – คู่มือ C# ที่เร่งด้วย GPU อย่างครบถ้วน
tags:
- Aspose OCR
- C#
- GPU computing
title: แยกข้อความจากภาพด้วย Aspose OCR – การสอน C# ที่เร่งด้วย GPU
url: /th/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากภาพ – คู่มือ C# ที่เร่งด้วย GPU อย่างครบถ้วน

เคยต้องการ **recognize text from image** แต่พบว่าเวอร์ชัน CPU ช้าอย่างเจ็บปวดไหม? บางทีคุณอาจกำลังพยายาม **extract text from receipt** ไฟล์และความหน่วงทำลายประสบการณ์ผู้ใช้ของคุณ ข่าวดีคือคุณไม่จำเป็นต้องยอมรับประสิทธิภาพที่ช้า—แพ็กเกจ GPU ของ Aspose OCR สามารถเร่งกระบวนการได้ และโค้ดมีเพียงไม่กี่บรรทัดเท่านั้น.

ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างเต็มที่สามารถรันได้ซึ่งแสดงวิธี **load image for OCR**, ตั้งค่า GPU ด้วย **set GPU device ID**, และในที่สุดดึงผลลัพธ์เป็นข้อความธรรมดาออกมา เมื่อจบคุณจะมีสแนปช็อตพร้อมใช้งานที่ทำงานบนเครื่อง Windows หรือ Linux สมัยใหม่ใด ๆ ที่มีการ์ด NVIDIA ที่รองรับ.

---

## สิ่งที่คุณต้องการ

- **.NET 6+** (หรือ .NET Framework 4.7.2+) – API ทำงานได้กับทั้งสอง.
- แพคเกจ NuGet **Aspose.OCR** **plus** **Aspose.OCR.Gpu** add‑on.
- GPU ของ NVIDIA ที่มี VRAM อย่างน้อย 2 GB (การสาธิตจำกัดการใช้ที่ 1 GB).
- ตัวอย่างภาพ เช่น ใบเสร็จสแกน (`receipt.jpg`).

หากคุณมีโปรเจกต์อยู่แล้ว เพียงรัน `dotnet add package Aspose.OCR` และ `dotnet add package Aspose.OCR.Gpu`. ไม่จำเป็นต้องมีไลบรารีเนทีฟเพิ่มเติม; SDK จะมาพร้อมกับไบนารี CUDA ที่จำเป็น.

## การดำเนินการแบบขั้นตอน

### ## วิธีการ recognize text from image ด้วย Aspose OCR และ GPU

ด้านล่างเป็น **complete, self‑contained program**. คัดลอกและวางลงในโปรเจกต์คอนโซลใหม่และกด `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Pro tip:** หากเครื่องของคุณมี GPU หลายตัว ให้เปลี่ยน `DeviceId` เป็น `1`, `2` เป็นต้น เพื่อเลือกการ์ดที่ไม่ค่อยใช้งาน. SDK จะโยน `GpuDeviceNotFoundException` ที่ชัดเจนหาก ID อยู่นอกช่วง.

### ### ขั้นตอนที่ 1: Load image for OCR

`OcrImage.FromFile` ทำมากกว่าการอ่าน bitmap—มันทำการพรี‑โปรเซสภาพ (deskew, binarization) ตาม heuristic ภายใน. นี่คือเหตุผลที่ **load image for OCR** เป็นขั้นตอนแยก: คุณสามารถสลับเป็น `MemoryStream` หากภาพของคุณอยู่ในฐานข้อมูล.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

หากคุณต้องการ **recognize text from image** ที่อยู่ในหน่วยความจำแล้ว:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### ขั้นตอนที่ 2: Set GPU device ID and memory limits

ทรัพยากร GPU มีจำนวนจำกัด. โดยการเปิดเผย `DeviceId` และ `MaxMemoryMb`, Aspose ให้คุณ **set GPU device ID** อย่างปลอดภัย, ป้องกันไม่ให้กระบวนการหนึ่งครอบงำการ์ดทั้งหมด.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

หากคุณเกินขีดจำกัดหน่วยความจำ, เอนจินจะสลับไปใช้ RAM ของระบบโดยอัตโนมัติ, ซึ่งช้ากว่าแต่ป้องกันการครช.

### ### ขั้นตอนที่ 3: Extract text from receipt (recognize text from image)

เมธอด `Recognize` ทำงานหนัก. คุณสามารถส่งภาษาใดก็ได้ที่ Aspose OCR รองรับ; สำหรับใบเสร็จ, ภาษาอังกฤษทำงานได้ส่วนใหญ่, แต่คุณยังสามารถเพิ่ม `OcrLanguage.Spanish` หรือแพ็คเกจภาษาที่กำหนดเอง.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Expected output** (ตัวอย่าง):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## ความแปรผันทั่วไป & กรณีขอบ

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Multiple receipts in one image** | เรียก `ocrEngine.Recognize` ในแต่ละส่วนที่ครอป (ใช้ `OcrImage.Crop`) | เพิ่มความแม่นยำเนื่องจากเอนจินเห็นพื้นที่ที่เล็กและสะอาดกว่า. |
| **Low‑resolution scans (<150 dpi)** | ทำการอัปสเกลล่วงหน้าด้วย `receiptImage.Resize(2.0)` ก่อนทำการจดจำ | ความหนาแน่นพิกเซลที่สูงขึ้นให้ข้อมูลมากขึ้นแก่ GPU. |
| **Non‑English receipts** | ส่ง `OcrLanguage.French` (หรือไฟล์ `.traineddata` ที่กำหนดเอง) | โมเดลเฉพาะภาษา ลดผลบวกเท็จ. |
| **GPU not available** | สำรองเป็น `OcrEngine` (CPU) ภายในบล็อก try‑catch | รับประกันว่าแอปยังทำงานได้บนเซิร์ฟเวอร์แบบไม่มี UI. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

## เคล็ดลับสำหรับ OCR ที่พร้อมใช้งานใน Production

- **Batch processing:** ห่อวงจรการจดจำด้วย `Parallel.ForEach` แต่จำกัดระดับความขนานตามจำนวนสตรีม GPU ที่คุณสามารถจัดสรรได้ (โดยปกติ 1‑2 ต่อการ์ด).
- **Memory hygiene:** ทำการ Dispose วัตถุ `OcrImage` ทันที (`receiptImage.Dispose()`), โดยเฉพาะเมื่อประมวลผลใบเสร็จหลายพันใบ.
- **Logging:** เก็บ `ocrResult.Confidence` สำหรับแต่ละบรรทัด; ความเชื่อมั่นต่ำอาจกระตุ้นกระบวนการตรวจสอบด้วยมือ.
- **Security:** เมื่อต้องจัดการใบเสร็จที่เป็นข้อมูลสำคัญ, ให้แน่ใจว่าไฟล์ภาพถูกเก็บในโฟลเดอร์ชั่วคราวที่เข้ารหัสและลบหลังการประมวลผล.

## สรุป

ตอนนี้คุณมี **complete, runnable example** ที่แสดงวิธี **recognize text from image** ด้วยการเร่ง GPU ของ Aspose OCR, **load image for OCR**, **set GPU device ID**, และสุดท้าย **extract text from receipt** ในไม่กี่ขั้นตอนสั้น ๆ. โค้ดพร้อมคัดลอกและวาง, และคำอธิบายให้บริบทเพียงพอที่จะปรับใช้กับหลายภาษา, หลาย GPU, หรือสถานการณ์ที่ต้องการ throughput สูง.

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองส่งสตรีมวิดีโอสดเข้า `GpuOcrEngine` เพื่อสแกนใบเสร็จแบบเรียลไทม์, หรือผสานผลลัพธ์เข้ากับ API การทำบัญชี. ไม่มีขีดจำกัดเมื่อคุณรวม OCR GPU ที่เร็วกับการออกแบบ C# ที่สะอาด.

*ขอให้เขียนโค้ดอย่างสนุกสนาน, และขอให้ OCR ของคุณเร็วเสมอ!*

![recognize text from image demo screenshot](placeholder-image.png "recognize text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
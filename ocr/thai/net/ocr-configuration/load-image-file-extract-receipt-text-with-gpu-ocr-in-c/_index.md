---
category: general
date: 2026-02-14
description: โหลดไฟล์รูปภาพและดึงข้อความจากใบเสร็จโดยใช้ Aspose OCR GPU engine. เรียนรู้การตั้งค่าหน่วยความจำ
  GPU สูงสุด, กำหนดค่าหน่วยความจำ GPU และรัน OCR บนรูปภาพอย่างมีประสิทธิภาพ.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: th
og_description: โหลดไฟล์รูปภาพและดึงข้อความจากใบเสร็จโดยใช้ Aspose OCR GPU engine
  คู่มือนี้แสดงวิธีตั้งค่าหน่วยความจำ GPU สูงสุดและรัน OCR บนรูปภาพใน C#
og_title: โหลดไฟล์รูปภาพและดึงข้อความใบเสร็จด้วย GPU OCR ใน C#
tags:
- C#
- OCR
- Aspose
- GPU
title: โหลดไฟล์รูปภาพและดึงข้อความใบเสร็จด้วย GPU OCR ใน C#
url: /th/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# โหลดไฟล์รูปภาพและดึงข้อความจากใบเสร็จด้วย GPU OCR ใน C#

เคยต้อง **load image file** แล้วดึงข้อความที่ตรงจากใบเสร็จแต่รู้สึกติดขัดที่ขั้นตอน OCR หรือไม่? คุณไม่ได้เป็นคนเดียว ในแอปพลิเคชันจริงหลายประเภท—เช่น ตัวติดตามค่าใช้จ่าย ระบบสินค้าคงคลัง หรือแม้แต่บอทสแกนใบเสร็จแบบง่าย—ความสามารถในการอ่านภาพใบเสร็จอย่างรวดเร็วสามารถเปลี่ยนเกมได้  

ข่าวดีคืออะไร? ด้วย GPU‑accelerated engine ของ Aspose.OCR คุณสามารถ **load image file**, **set max GPU memory**, และ **run OCR on image** ได้ทั้งหมดในไม่กี่บรรทัดของ C# ด้านล่างเราจะพาคุณผ่านกระบวนการทั้งหมด ตั้งแต่การกำหนดค่า GPU จนถึงการพิมพ์ข้อความที่สกัดออกมาเป็น plain‑text

## สิ่งที่คุณจะได้เรียนรู้

ในบทเรียนนี้คุณจะได้ค้นพบวิธี:

* **Load image file** จากดิสก์โดยใช้ `ImageStream` ของ Aspose
* **Configure GPU memory** เพื่อให้เอนจินไม่กิน RAM มากเกินกว่าที่คุณกำหนด
* **Run OCR on image** และดึงอักขระทุกตัวจากใบเสร็จ
* จัดการกับปัญหาที่พบบ่อย—เช่นข้อผิดพลาด out‑of‑memory หรือสแกนที่เบลอ
* ตรวจสอบผลลัพธ์และปรับตั้งค่าเพื่อความแม่นยำที่ดียิ่งขึ้น

ไม่มีบริการภายนอก ไม่มีเทคนิคลับ—แค่โค้ด C# บริสุทธิ์ที่คุณสามารถใส่ลงในโปรเจกต์ .NET 6+ ใดก็ได้

---

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึก โปรดตรวจสอบว่าคุณมี:

* .NET 6 SDK หรือใหม่กว่า
* ใบอนุญาต Aspose.OCR ที่ถูกต้อง (หรือคุณสามารถใช้โหมดประเมินผลฟรี)
* แพ็กเกจ NuGet `Aspose.OCR` และ `Aspose.OCR.Gpu` ที่เพิ่มเข้าไปในโปรเจกต์ของคุณ
* ตัวอย่างรูปใบเสร็จ (`receipt.png`) พร้อมอยู่บนดิสก์

หากสิ่งใดในรายการนี้ยังไม่คุ้นเคย ให้หยุดพักสักครู่และติดตั้งแพ็กเกจ:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

เท่านี้—ไม่ต้องมีไลบรารีเนทีฟเพิ่มเติม เพราะการสนับสนุน GPU ถูกฝังไว้ในแพ็กเกจ NuGet แล้ว

---

## โหลดไฟล์รูปภาพและเตรียม GPU Engine

สิ่งแรกที่คุณต้องทำคือ **load image file** เข้าไปใน `ImageStream` วัตถุนี้จะทำหน้าที่แยกรายละเอียดของระบบไฟล์ออกและให้ OCR engine ได้รับการแสดงผลภาพในหน่วยความจำที่สะอาด

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
*Loading the image file* ผ่าน `ImageStream.FromFile` รับประกันว่าเอนจินจะเห็นข้อมูลพิกเซลที่ตรงกันเต็มที่ รักษา DPI และความลึกของสีไว้ หากข้ามขั้นตอนนี้หรือป้อนสตรีมที่เสียหาย OCR จะพลาดอักขระหรือเกิดข้อยกเว้น

> **Pro tip:** หากคุณจัดการไฟล์ที่ผู้ใช้อัปโหลด ให้ห่อ `FromFile` ด้วยบล็อก try‑catch และตรวจสอบขนาดไฟล์ก่อน ภาพขนาดใหญ่สามารถทำให้หน่วยความจำ GPU พุ่งสูงได้หากคุณยังไม่ได้ **configure GPU memory** อย่างเหมาะสม

---

## ตั้งค่า Max GPU Memory เพื่อประสิทธิภาพที่ดีที่สุด

ทรัพยากร GPU มีค่าโดยเฉพาะอย่างยิ่งบนเซิร์ฟเวอร์ที่แชร์หรือแล็ปท็อปที่มี VRAM จำกัด คุณสมบัติ `MaxDeviceMemory` บอก Aspose ว่าให้ใช้หน่วยความจำของ GPU มากเท่าไหร่ได้อย่างปลอดภัย

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

เมื่อคุณ **set max GPU memory** เอนจินจะอัตโนมัติเปลี่ยนไปใช้การประมวลผลด้วย CPU หากไม่สามารถตอบสนองคำขอได้—ช่วยป้องกันการพังของแอป นี่คือวิธีที่ปลอดภัยที่สุดในการ **configure GPU memory** โดยไม่ต้องกำหนดขีดจำกัดเฉพาะอุปกรณ์

**เมื่อควรปรับค่า:**  
* หากคุณพบ `OutOfMemoryException` ระหว่างการประมวลผลชุดใหญ่ ให้ลดขีดจำกัดลง  
* หากใบเสร็จของคุณมีความละเอียดสูง (300 DPI ขึ้นไป) ให้เพิ่มเป็น 2 GB เพื่อรักษาความเร็ว

---

## รัน OCR บนรูปภาพเพื่อดึงข้อความจากใบเสร็จ

ตอนนี้มาถึงส่วนที่สนุก—จริง ๆ แล้ว **run OCR on image** และดึงข้อความจากใบเสร็จ `Recognize` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่มีคุณสมบัติ `Text` ซึ่งเป็นผลลัพธ์ plain‑text

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

คอนโซลจะแสดงผลประมาณนี้:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**ทำไมวิธีนี้ถึงได้ผล:**  
GPU engine รันโมเดล deep‑learning ที่ฝึกฝนบนรูปแบบเอกสารหลากหลาย โดยการป้อนภาพที่โหลดอย่างถูกต้องและสะอาด คุณให้โมเดลโอกาสดีที่สุดในการ **extract text from receipt** อย่างแม่นยำ

---

## ตรวจสอบผลลัพธ์และข้อผิดพลาดทั่วไป

แม้จะมีเอนจินที่ทรงพลัง OCR ก็ไม่ได้เป็นเวทมนตร์ นี่คือสิ่งที่ควรระวัง:

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| ตัวอักษรบิดเบี้ยว | คอนทราสต์ต่ำหรือภาพเบลอ | ทำการ Pre‑process ด้วย `ImageProcessor` ของ Aspose เพื่อเพิ่มคอนทราสต์ |
| ขาดบรรทัด | รูปภาพถูกตัดส่วนเกินเกินไป | ตรวจสอบให้แน่ใจว่าใบเสร็จเต็มอยู่ในขอบเขตของรูปภาพ |
| ข้อผิดพลาดหน่วยความจำไม่พอ | `MaxDeviceMemory` ต่ำเกินไปสำหรับขนาดรูปภาพ | เพิ่มค่า `MaxDeviceMemory` หรือย่อขนาดรูปภาพก่อน |
| ภาษาไม่ถูกต้อง | ใบเสร็จมีข้อความที่ไม่ใช่ภาษาอังกฤษ | ตั้งค่า `gpuEngine.Language = OcrLanguage.Spanish;` (หรือภาษาอื่นที่เหมาะสม) |

หากเจอข้อใดข้อหนึ่ง วิธีแก้ด่วนคือปรับขนาดรูปภาพให้มีความยาวด้านที่ยาวที่สุดไม่เกิน 2000 px—จะลดภาระ GPU อย่างมากโดยไม่เสียความอ่านได้สำหรับใบเสร็จส่วนใหญ่

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมดพร้อมคอมไพล์ แค่เปลี่ยนเส้นทางไฟล์ให้เป็นตำแหน่งใบเสร็จของคุณเอง

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ผลลัพธ์คอนโซลที่คาดหวัง** (ใบเสร็จของคุณอาจแตกต่างแน่นอน):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

รันโปรแกรมด้วย `dotnet run` หากเห็นข้อความแสดงบนคอนโซล ยินดีด้วย—คุณได้ทำ **load image file**, **set max GPU memory**, และ **run OCR on image** เพื่อ **extract text from receipt** สำเร็จแล้ว

---

## คำถามที่พบบ่อย

**Q: Does this work on machines without a dedicated GPU?**  
A: ใช่. Aspose.OCR จะเปลี่ยนไปใช้โหมด CPU อย่างอ่อนโยนหากไม่พบ GPU ที่เข้ากันได้ คุณยังคงสามารถ **load image file** และ **run OCR on image** ได้ แม้จะช้ากว่าเล็กน้อย

**Q: Can I process multiple receipts in a batch?**  
A: แน่นอน. ให้ใส่โค้ดการจดจำไว้ในลูป `foreach` แต่จำไว้ว่าให้ใช้อินสแตนซ์ `GpuEngine` เดียวกันซ้ำ—จะช่วยหลีกเลี่ยงการเริ่มต้นทรัพยากร GPU ใหม่สำหรับแต่ละไฟล์

**Q: What if my receipt is in a language other than English?**  
A: ตั้งค่าภาษาให้ตรงก่อนเรียก `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

เอนจินจะใช้ชุดอักขระที่เหมาะสมตามภาษาที่กำหนด

---

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

ตอนนี้คุณได้เชี่ยวชาญพื้นฐานแล้ว ลองสำรวจต่อ:

* **Fine‑tuning OCR accuracy** – ทดลองกับ `gpuEngine.RecognitionOptions` เช่น `EnableDeskew` หรือ `ContrastEnhancement`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
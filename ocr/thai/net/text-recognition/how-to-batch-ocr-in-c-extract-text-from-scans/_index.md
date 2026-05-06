---
category: general
date: 2026-05-06
description: เรียนรู้วิธีทำ OCR แบบเป็นชุดใน C# และดึงข้อความจากการสแกนอย่างรวดเร็วด้วย
  Aspose OCR Batch. ทำตามคู่มือขั้นตอนเต็มรูปแบบพร้อมโค้ด เคล็ดลับ และการจัดการกรณีขอบ.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: th
og_description: วิธีทำ OCR เป็นชุดใน C#? คู่มือนี้จะแสดงวิธีดึงข้อความจากการสแกนอย่างมีประสิทธิภาพด้วย
  Aspose OCR, การสนับสนุน GPU, และการประมวลผลแบบขนาน.
og_title: วิธีทำ OCR แบบชุดใน C# – ดึงข้อความจากการสแกน
tags:
- C#
- OCR
- Aspose
title: วิธีทำ OCR แบบชุดใน C# – ดึงข้อความจากการสแกน
url: /th/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ด้วย C# – ดึงข้อความจากการสแกน

เคยสงสัย **วิธีทำ Batch OCR** เมื่อคุณมีโฟลเดอร์ที่เต็มไปด้วย PDF หรือ JPEG ที่สแกนไว้หรือไม่? คุณไม่ได้เป็นคนเดียวที่มองเห็นภาพจำนวนมากและคิดว่า “ต้องมีวิธีที่เร็วกว่าในการดึงข้อความออกมา” ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันที่ใช้งานได้จริง ซึ่งไม่เพียงแต่ช่วย **ดึงข้อความจากการสแกน** แต่ยังเร่งความเร็วด้วยการเร่งด้วย GPU และการประมวลผลแบบขนาน

ความจริงคือ การทำ OCR ทีละไฟล์เป็นการเสียเวลามาก โดยเฉพาะเมื่อคุณต้องจัดการกับหลายสิบหรือหลายร้อยหน้า เมื่ออ่านจนจบคุณจะได้แอปคอนโซล C# ที่พร้อมรันซึ่งจะประมวลผลโฟลเดอร์ทั้งหมดด้วยคำสั่งเดียว ให้คุณได้ไฟล์ข้อความที่สะอาดพร้อมสำหรับการทำดัชนี การค้นหา หรืออะไรก็ตามที่ตามมา

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มลงลึก โปรดตรวจสอบว่าคุณมี:

- **.NET 6.0 หรือใหม่กว่า** (โค้ดใช้คุณสมบัติ C# รุ่นใหม่)
- **ลิขสิทธิ์สำหรับ Aspose.OCR** (รุ่นทดลองฟรีใช้ได้สำหรับการทดสอบ)
- เครื่องที่รองรับ **GPU** หากคุณต้องการเปิดใช้งาน `UseGpu`; หากไม่มีไลบรารีจะกลับไปใช้ CPU
- ความคุ้นเคยพื้นฐานกับ **C# console applications**

ไม่มีบริการภายนอก ไม่มีไฟล์กำหนดค่าที่ซ่อนอยู่—แค่ SDK และโฟลเดอร์รูปภาพเท่านั้น

## ขั้นตอนที่ 1: ติดตั้งแพ็กเกจ NuGet ของ Aspose.OCR

แรกเริ่มให้เพิ่มไลบรารี Aspose OCR เข้าไปในโปรเจกต์ของคุณ เปิดเทอร์มินัลในโฟลเดอร์โซลูชันและรัน:

```bash
dotnet add package Aspose.OCR
```

คำสั่งนี้จะดึง `Aspose.OCR` และเนมสเปซ batch ที่เราจะใช้สำหรับ **batch OCR** ต่อไป

> **เคล็ดลับ:** หากคุณใช้ Visual Studio คุณสามารถเพิ่มแพ็กเกจผ่าน UI ของ NuGet Package Manager ได้เช่นกัน

## ขั้นตอนที่ 2: สร้างโครงสร้างแอปคอนโซล

มาสร้างแอปคอนโซลขนาดเล็กที่ใช้เป็นโฮสต์ให้กับตัวประมวลผล batch ของเรา สร้างไฟล์ใหม่ชื่อ `Program.cs` แล้ววางโครงสร้างต่อไปนี้:

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

ทำไมต้องห่อโลจิกไว้ใน `Main`? เพราะแอปคอนโซลให้ฟีดแบ็กทันทีผ่าน `Console.WriteLine` เหมาะสำหรับการตรวจสอบอย่างรวดเร็วว่าการทำ **batch OCR** เสร็จสมบูรณ์หรือไม่

## ขั้นตอนที่ 3: ตั้งค่า OcrBatchProcessor

นี่คือส่วนสำคัญของโซลูชัน เราจะสร้างอินสแตนซ์ `OcrBatchProcessor` ชี้ไปที่โฟลเดอร์อินพุต ระบุที่เก็บผลลัพธ์ และปรับค่าประสิทธิภาพบางอย่าง

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### ทำไมการตั้งค่าเหล่านี้ถึงสำคัญ

| Setting | สิ่งที่ทำ | เมื่อคุณอาจต้องเปลี่ยน |
|---------|-----------|------------------------|
| `InputFolder` | เส้นทางไปยังไฟล์สแกนที่ต้องการประมวลผล | ใช้เส้นทางสัมพัทธ์เพื่อความพกพา |
| `OutputFolder` | ที่ที่ข้อความที่ดึงจากแต่ละรูปจะถูกบันทึกเป็นไฟล์ `.txt` | ชี้ไปยังแชร์เครือข่ายหากต้องการเก็บศูนย์กลาง |
| `Language` | โมเดลภาษาของ OCR; เราเลือก Spanish เพื่อแสดงการสนับสนุนหลายภาษา | เปลี่ยนเป็น `OcrLanguage.English` หรือภาษาที่รองรับอื่น |
| `UseGpu` | ส่งการคำนวณเมทริกซ์หนักไปยัง GPU | ตั้งเป็น `false` บนเซิร์ฟเวอร์ไม่มี GPU |
| `MaxDegreeOfParallelism` | ควบคุมจำนวนรูปที่ประมวลผลพร้อมกัน | ลดค่าในเครื่องที่ CPU ต่ำเพื่อหลีกเลี่ยงการคอขวด |

## ขั้นตอนที่ 4: รันการทำงานแบบ Batch พร้อมการจัดการข้อผิดพลาด

การรัน batch เพียงเรียก `Execute()` แต่เราจะห่อไว้ในบล็อก try‑catch เพื่อให้คุณได้รับข้อความช่วยเหลือหากมีอะไรผิดพลาด (เช่น โฟลเดอร์หาย หรือรูปแบบไฟล์ที่ไม่รองรับ)

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

เมื่อโปรเซสเซอร์ทำงานเสร็จ คุณจะเห็น **Batch completed.** ในคอนโซล และแต่ละรูปต้นฉบับจะมีไฟล์ `.txt` ที่สอดคล้องกันใน `OcrResults` ชื่อไฟล์จะเหมือนกับต้นฉบับ ทำให้แมปกลับไปยังสแกนต้นฉบับได้ง่าย

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ – สิ่งที่ควรคาดหวัง

หลังจากโปรแกรมทำงาน เปิดไฟล์ใดไฟล์หนึ่งใน `YOUR_DIRECTORY/OcrResults` คุณควรเห็นข้อความธรรมดาที่ดึงจากรูปที่สอดคล้องกัน เช่น:

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

หากผลลัพธ์ดูเป็นอักขระแปลก ๆ ให้ตรวจสอบว่า `Language` ตรงกับภาษาของสแกนของคุณ Aspose OCR รองรับมากกว่า 100 ภาษา ดังนั้นคุณสามารถสลับ `OcrLanguage.Spanish` เป็นภาษาที่ต้องการได้

## การจัดการกรณีขอบและข้อผิดพลาดทั่วไป

### 1. GPU ไม่พร้อมใช้งาน

หากเครื่องของคุณไม่มี GPU ที่รองรับ `UseGpu = true` จะสลับไปใช้โหมด CPU โดยไม่มีการแจ้งเตือน แต่คุณจะเสียความเร็วเพิ่มขึ้น หากต้องการให้ชัดเจน คุณสามารถตรวจจับความสามารถของ GPU ได้:

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. ไฟล์ขนาดใหญ่เกินความจำ

เมื่อต้องจัดการกับ TIFF หรือ PDF ขนาดใหญ่ ให้พิจารณาแยกไฟล์เป็นรูปย่อยก่อน Aspose OCR สามารถจัดการ PDF หลายหน้าได้ แต่การใช้หน่วยความจำจะเพิ่มตามจำนวนหน้า ขั้นตอนการพรี‑โปรเซสด้วย `Aspose.Imaging` สามารถตัดเอกสารเป็นชิ้นส่วนที่จัดการได้ง่ายขึ้น

### 3. ไฟล์ที่ไม่ใช่รูปภาพในโฟลเดอร์อินพุต

ตัวประมวลผล batch จะละเว้นไฟล์ที่ไม่สามารถพาร์สได้ แต่การทำให้โฟลเดอร์สะอาดเป็นแนวปฏิบัติที่ดี คุณสามารถกรองตามส่วนขยายได้:

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(หมายเหตุ: `FileFilter` เป็นคุณสมบัติสมมติ; แทนที่ด้วย API จริงหากมี)*

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วางทั้งหมด แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางเต็มบนเครื่องของคุณ

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล

```
Batch completed.
```

และใน `C:\OcrResults` คุณจะพบไฟล์ `.txt` สำหรับทุกรูปใน `C:\MyScans`

## สรุป

ตอนนี้คุณมีวิธีที่มั่นคงและพร้อมใช้งานในระดับ production เพื่อ **ทำ Batch OCR** ด้วย C# และ **ดึงข้อความจากการสแกน** โดยไม่ต้องเปิดไฟล์ทีละไฟล์ ด้วยการใช้ batch API ของ Aspose, การเร่งด้วย GPU, และการปรับระดับการทำงานแบบขนาน โซลูชันนี้สามารถขยายจากไม่กี่หน้าไปจนถึงหลายพันหน้าได้

ต่อไปคุณอาจลองทำสิ่งต่อไปนี้:

- **เชื่อมต่อกับดัชนีการค้นหา** (เช่น Elasticsearch) เพื่อทำให้ข้อความที่ดึงออกมาสามารถค้นหาได้
- **เพิ่มขั้นตอนหลังการประมวลผล** เช่น การตรวจสอบการสะกดหรือการตรวจจับภาษา
- **ห่อแอปคอนโซลเป็น Windows Service** เพื่อเฝ้าติดตามโฟลเดอร์ดรอปแบบต่อเนื่อง

ลองปรับแต่งระดับการทำงานแบบขนานหรือสลับโมเดลภาษาได้ตามต้องการ หากเจออุปสรรคใด ๆ คอมเมนต์ไว้ด้านล่าง—ขอให้สนุกกับการ OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
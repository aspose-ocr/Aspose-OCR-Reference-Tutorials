---
category: general
date: 2026-02-19
description: เรียนรู้วิธีทำ OCR แบบเป็นชุดด้วย Aspose.OCR ใน C# คู่มือนี้จะแสดงวิธีดึงข้อความจากภาพและแปลงภาพเป็นไฟล์
  txt อย่างมีประสิทธิภาพ
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: th
og_description: วิธีทำ OCR แบบกลุ่มด้วย Aspose.OCR ใน C# ดึงข้อความจากรูปภาพและแปลงรูปภาพเป็นไฟล์
  txt ในไม่กี่ขั้นตอนง่าย ๆ
og_title: วิธีทำ OCR แบบชุดใน C# – การแปลงภาพเป็นข้อความอย่างรวดเร็ว
tags:
- OCR
- C#
- Aspose
title: วิธีทำ OCR แบบกลุ่มใน C# – ดึงข้อความจากรูปภาพอย่างรวดเร็ว
url: /th/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ใน C# – คู่มือเต็มขั้นตอน

เคยสงสัย **วิธีทำ batch OCR** โฟลเดอร์รูปภาพทั้งหมดโดยไม่ต้องเขียนโปรแกรมแยกสำหรับแต่ละไฟล์หรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาจำนวนมากเจออุปสรรคเมื่อจำเป็นต้องดึงข้อความจากหลายสิบหรือแม้แต่หลายพันหน้าเอกสารสแกน ใบเสร็จ หรือภาพหน้าจอ ข่าวดีคือ? ด้วย Aspose.OCR คุณสามารถอัตโนมัติกระบวนการทั้งหมด, **ดึงข้อความจากรูปภาพ**, และ **แปลงรูปภาพเป็น txt** เพียงไม่กี่บรรทัด

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบ ซึ่งแสดงให้เห็นอย่างชัดเจนว่าตั้งค่า OCR batch processor อย่างไร, ปรับการเตรียมข้อมูลล่วงหน้า, จัดการการทำงานแบบขนาน, และบันทึกผลลัพธ์แต่ละไฟล์เป็นไฟล์ `.txt` สุดท้ายคุณจะได้แอปคอนโซลที่ทำงานอิสระซึ่งสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานบน .NET Core และ .NET Framework ด้วย)
- แพ็คเกจ NuGet Aspose.OCR for .NET (`Aspose.OCR`)  
- โฟลเดอร์ที่เต็มไปด้วยไฟล์รูปภาพ (`.png`, `.jpg`, ฯลฯ) ที่ต้องการประมวลผล
- RAM ปริมาณพอใช้; ตัวอย่างใช้ 4 เธรดขนานแต่คุณสามารถปรับได้

ไม่มีบริการภายนอก, ไม่มีไฟล์กำหนดค่าที่ซ่อนอยู่—เพียงโค้ด C# แท้ ๆ ที่คุณสามารถคอมไพล์และรันได้ทันที

![Diagram illustrating how to batch ocr processing flow](/images/how-to-batch-ocr-flow.png "how to batch ocr flow diagram")

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR และตั้งค่าโปรเจกต์

ขั้นแรกให้เพิ่มแพ็คเกจ Aspose.OCR เข้าในโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.OCR
```

ทำไมถึงสำคัญ: Aspose.OCR มีเอนจิน OCR, ข้อมูลภาษา, และยูทิลิตี้การเตรียมข้อมูลล่วงหน้าในตัว ทำให้คุณไม่ต้องใช้ไบนารีของบุคคลที่สาม หลังจากติดตั้งแพ็คเกจแล้ว สร้างแอปคอนโซลใหม่ (หรือเพิ่มโค้ดนี้ลงในแอปที่มีอยู่) แล้วนำเข้า namespace ที่จำเป็น:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

คำสั่ง `using` เหล่านี้ทำให้คุณเข้าถึงคลาส batch processor และตัวช่วย I/O ที่สะดวก

## ขั้นตอนที่ 2: กำหนดค่า OCR Batch Processor

ต่อไปเราจะสร้างอินสแตนซ์ `OcrBatchProcessor` และบอกให้มันรู้ว่าต้องค้นหาภาษาอะไร, ทำความสะอาดภาพอย่างไร, และใช้จำนวนเธรดขนานเท่าไหร่ นี่คือหัวใจของ **วิธีทำ batch OCR** อย่างมีประสิทธิภาพ

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**ทำไมต้องเปิด Deskew?** เอกสารสแกนหลายฉบับไม่ได้จัดเรียงอย่างสมบูรณ์; อัลกอริทึม deskew จะหมุนภาพกลับสู่เส้นฐานตรง ซึ่งมักเพิ่มอัตราการรับรู้ได้ประมาณ 10‑15 %

## ขั้นตอนที่ 3: เชื่อมต่อ Callback เพื่อบันทึกไฟล์ข้อความ

Batch processor จะส่งอีเวนต์เมื่อประมวลผลภาพเสร็จแต่ละภาพ เราจะสมัครรับ `ResultProcessed` เพื่อเขียนผล OCR แต่ละรายการลงไฟล์ `.txt`—ทำให้ **แปลงรูปภาพเป็น txt** ได้ทันที

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

เคล็ดลับสั้น: หากต้องการรักษาโครงสร้างโฟลเดอร์เดิม คุณสามารถปรับ `txtPath` ให้รวมโฟลเดอร์ย่อยหรือไดเรกทอรีเอาต์พุตแยกต่างหาก

## ขั้นตอนที่ 4: รัน Batch บนโฟลเดอร์รูปภาพของคุณ

เหลือแค่ชี้ตัวประมวลผลไปที่โฟลเดอร์ที่เก็บรูปภาพที่คุณต้องการ **ดึงข้อความจากรูปภาพ** เมธอด `ProcessFolder` จะสแกนโฟลเดอร์ย่อยแบบเรียกซ้ำ ดังนั้นคุณสามารถวางโครงสร้างสแกนทั้งหมดและให้ไลบรารีจัดการส่วนที่เหลือได้

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

เมื่อคุณรันโปรแกรม จะเห็นผลลัพธ์บนคอนโซลเช่น:

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

แต่ละรูปภาพจะมีไฟล์ `.txt` คู่กันที่บรรจุข้อความที่สกัดออกมา

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

- สำหรับทุกไฟล์ `*.png` หรือ `*.jpg` ในไดเรกทอรีต้นทาง จะมีไฟล์ `*.txt` ที่สอดคล้องกันปรากฏข้างเคียง
- คอนโซลจะแสดงบรรทัดต่อไฟล์เพื่อให้คุณเห็นฟีดแบ็กแบบเรียลไทม์
- หากไม่สามารถอ่านภาพได้ (ไฟล์เสีย, ฟอร์แมตไม่รองรับ) Aspose.OCR จะบันทึกข้อผิดพลาดแล้วดำเนินการต่อกับไฟล์ที่เหลือ—ขอบคุณความทนทานในตัวของ batch engine

## คำถามทั่วไป & กรณีขอบ

### ถ้าต้องการประมวลผล PDF แทนรูปภาพล่ะ?

Aspose.OCR สามารถรับหน้า PDF เป็นภาพภายในได้ แต่คุณต้องแปลง PDF เป็นภาพแรสเตอร์ก่อน (เช่น ใช้ Aspose.PDF) เมื่อได้ไฟล์ PNG แล้ว โค้ด batch เดิมจะทำงานโดยไม่ต้องแก้ไข

### สามารถเปลี่ยนภาษาได้ระหว่างการทำงานหรือไม่?

ได้. คุณสมบัติ `Language` ยอมรับค่าใด ๆ ของ enum `Language` (Spanish, French, Chinese, ฯลฯ) หากมีเอกสารหลายภาษา ให้พิจารณารันสองรอบ—หนึ่งต่อภาษา—หรือใช้ `Language.AutoDetect`

### จะจำกัด batch ให้ทำงานเฉพาะประเภทไฟล์บางประเภทได้อย่างไร?

`ProcessFolder` รองรับพารามิเตอร์ `SearchOption` และ `string[] extensions` ตัวอย่าง:

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### เรื่องการเร่งความเร็วด้วย GPU ล่ะ?

Aspose.OCR รองรับ GPU ผ่านการตั้งค่า `OcrEngine` แต่ `MaxDegreeOfParallelism` ของ batch processor ยังคงเป็นตัวควบคุมหลักสำหรับความพร้อมทำงานพร้อมกัน หากมี GPU ที่เข้ากันได้ ให้เปิดใช้งานในตั้งค่า engine ก่อนสร้าง `OcrBatchProcessor`

### จะจัดการโฟลเดอร์ขนาดใหญ่มาก (หลายหมื่นไฟล์) อย่างไร?

- เพิ่ม `MaxDegreeOfParallelism` อย่างระมัดระวัง; เธรดมากเกินไปอาจทำให้หน่วยความจำหมด
- ใช้โฟลเดอร์เอาต์พุตแยกเพื่อหลีกเลี่ยงความรก
- ทำการ flush logs ไปยังดิสก์เป็นระยะเพื่อป้องกันการบวมของหน่วยความจำ

## เคล็ดลับระดับมืออาชีพสำหรับ OCR คุณภาพสูง

- **DPI มีความสำคัญ**: ภาพที่ 300 DPI หรือสูงกว่าให้ความแม่นยำดีที่สุด หากสแกนของคุณต่ำกว่า ให้พิจารณาขยายขนาดด้วยฟิลเตอร์ bicubic ก่อนประมวลผล
- **ลดสัญญาณรบกวน**: เปิด `Preprocessing.NoiseRemoval` หากภาพต้นทางมีลักษณะเม็ดสี
- **การตั้งชื่อไฟล์**: ใช้ชื่อไฟล์สั้นและเป็นอักษรและตัวเลข; อักขระพิเศษอาจทำให้โลจิกของ callback พลาดได้
- **การบันทึก**: แทนที่ `Console.WriteLine` ด้วย logger ที่เหมาะสม (เช่น `Serilog`) สำหรับงานระดับผลิต

## ขั้นตอนต่อไป

ตอนนี้คุณได้เชี่ยวชาญ **วิธีทำ batch OCR** แล้ว อาจอยากทำต่อ:

- **ดึงข้อความจากรูปภาพ** แล้วส่งผลลัพธ์ไปยังดัชนีการค้นหา (เช่น Elasticsearch) เพื่อการค้นหาเต็มข้อความ
- **แปลงรูปภาพเป็น txt** แล้วใช้การประมวลผลภาษาธรรมชาติ (NLP) เพื่อจัดประเภทเอกสารอัตโนมัติ
- ทดลอง **แพ็คภาษาแตกต่าง** หรือพจนานุกรมกำหนดเองสำหรับคำศัพท์เฉพาะอุตสาหกรรม

หากคุณสนใจการประมวลผลต่อเนื่อง ให้ดูบทเรียน “Parsing OCR output with regular expressions” หรือ “Storing OCR results in a SQL database”

---

**Happy coding!** ปรับค่าการทำงานแบบขนาน, เพิ่มขั้นตอนการเตรียมข้อมูลล่วงหน้า, หรือห่อหุ้มทั้งหมดใน Windows service เพื่อการตรวจสอบอย่างต่อเนื่องได้เลย ท้องฟ้าเป็นขีดจำกัดเมื่อคุณผสานความสามารถ batch ของ Aspose.OCR กับความคิดสร้างสรรค์ของ .NET

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
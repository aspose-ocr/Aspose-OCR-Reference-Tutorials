---
category: general
date: 2026-04-03
description: เรียนรู้วิธีทำ OCR แบบกลุ่มด้วย Aspose.OCR ใน C# คู่มือนี้จะแสดงวิธีดึงข้อความจากภาพ
  PNG และแปลงภาพเป็นข้อความอย่างมีประสิทธิภาพ.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: th
og_description: ค้นพบวิธีทำ OCR แบบกลุ่มใน C# เพื่อดึงข้อความจากภาพ PNG และแปลงภาพเป็นข้อความโดยใช้
  Aspose.OCR พร้อมโค้ดเต็มให้ใช้งาน.
og_title: วิธีทำ OCR แบบแบตช์ใน C# – คู่มือสั้น
tags:
- OCR
- C#
- Aspose
title: วิธีทำ OCR แบบกลุ่มใน C# – วิธีเร็วในการดึงข้อความจากไฟล์ PNG
url: /th/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ใน C# – วิธีเร็วในการดึงข้อความจากไฟล์ PNG

เคยสงสัยไหมว่า **how to batch OCR** โฟลเดอร์เต็มของภาพหน้าจอโดยไม่ต้องเขียนลูปสำหรับแต่ละไฟล์? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ—เช่นการแปลงใบแจ้งหนี้เป็นดิจิทัลหรือการเก็บบันทึกใบเสร็จสแกน—คุณอาจมีหลายสิบหรือหลายร้อยไฟล์ PNG ที่ต้องดึงข้อความออก ข่าวดีคือ? ด้วย Aspose.OCR คุณสามารถ **extract text PNG** ภาพได้แบบขนาน และกระบวนการทั้งหมดสามารถทำให้เสร็จในไม่กี่บรรทัดของ C#.

ในบทแนะนำนี้ เราจะเดินผ่านตัวอย่างที่สมบูรณ์และพร้อมรันที่แสดงให้คุณเห็นวิธี **convert images to text** ด้วยการใช้ batch processor เราจะครอบคลุมข้อกำหนดเบื้องต้น อธิบายว่าทำไมแต่ละบรรทัดถึงสำคัญ และยังใส่เคล็ดลับบางอย่างเพื่อให้คุณหลีกเลี่ยงข้อผิดพลาดทั่วไปในภายหลัง.

## ข้อกำหนดเบื้องต้น

- **.NET 6.0** (หรือเวอร์ชันใหม่กว่า) ติดตั้งบนเครื่องของคุณ เวอร์ชันเก่าก็ทำงานได้ แต่เวอร์ชันล่าสุดให้ประสิทธิภาพที่ดีกว่าและรองรับ async
- แพคเกจ **Aspose.OCR for .NET** คุณสามารถติดตั้งได้ผ่าน NuGet: `dotnet add package Aspose.OCR`.
- โฟลเดอร์ที่เต็มไปด้วยภาพ **PNG** ที่คุณต้องการประมวลผล เราจะอ้างอิงเป็น `YOUR_DIRECTORY` ตลอดคู่มือ
- RAM ปริมาณปานกลาง—batch OCR อาจกินหน่วยความจำมากหากเพิ่มการทำงานแบบขนาน แต่การใช้ `Environment.ProcessorCount` จะทำให้ปลอดภัย

> **Pro tip:** หากคุณอยู่ใน pipeline ของ CI/CD ให้เพิ่มไฟล์ลิขสิทธิ์ Aspose เป็น secret เพื่อหลีกเลี่ยงข้อจำกัด 20 หน้า ของการประเมินฟรี.

ตอนนี้มาเริ่มทำกันเลย.

## ขั้นตอนที่ 1: ตั้งค่า Batch OCR Processor (Primary Keyword in Header)

สิ่งแรกที่คุณต้องการคืออินสแตนซ์ของ `BatchOcrProcessor` คลาสนี้จะซ่อนตรรกะการทำงานหลายเธรดและให้คุณโฟกัสที่การทำงานกับแต่ละภาพ

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**ทำไมสิ่งนี้ถึงสำคัญ:**  
- `Engine = new OcrEngine()` ให้คุณได้ OCR engine ใหม่สำหรับแต่ละเธรด เพื่อหลีกเลี่ยงการแย่งกันใช้ทรัพยากร  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` ปรับขนาดอัตโนมัติตามจำนวนคอร์ ให้คุณได้อัตราการประมวลผลที่ดีที่สุดโดยไม่ต้องปรับค่าเอง

## ขั้นตอนที่ 2: เชื่อมต่อกับเหตุการณ์ Progress (Helps Track Extraction)

การเห็นความคืบหน้าเป็นสิ่งสำคัญเมื่อประมวลผลหลายร้อยไฟล์ เหตุการณ์ `ProgressChanged` จะเกิดขึ้นหลังจากแต่ละไฟล์เสร็จสิ้น ทำให้คุณสามารถบันทึกสถานะได้

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**ทำไมคุณจะชอบมัน:**  
- การตอบสนองแบบเรียลไทม์ช่วยป้องกันไม่ให้คุณสงสัยว่าแอปค้างหรือไม่  
- หากคุณต้องการหยุดหรือยกเลิก คุณก็มี hook ที่จะตรวจสอบ `e.Current` กับ `e.Total` อยู่แล้ว

## ขั้นตอนที่ 3: กำหนดการสแกนโฟลเดอร์และรูปแบบไฟล์ (Extract Text PNG)

ตอนนี้เราบอก processor ว่าจะมองหาไฟล์ที่ไหนและไฟล์ประเภทใดที่จะดึงมา รูปแบบ `"*.png"` ทำให้เราจัดการเฉพาะภาพ PNG เท่านั้น

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**ทำไมสิ่งนี้ถึงสำคัญ:**  
- การใช้ glob pattern ทำให้โค้ดยืดหยุ่น; เปลี่ยน `*.png` เป็น `*.jpg` หากต้องการจัดการ JPEG ในภายหลัง  
- คอลแบ็กจะรับทั้งเส้นทางภาพและข้อความที่จดจำได้ ให้คุณควบคุมการทำงานต่อไปได้เต็มที่

## ขั้นตอนที่ 4: บันทึกข้อความที่จดจำไว้ข้างไฟล์ต้นฉบับ (Convert Images to Text)

ภายในคอลแบ็ก เราจะเขียนผลลัพธ์ OCR ลงไฟล์ `.txt` ที่อยู่ติดกับไฟล์ PNG ดั้งเดิม นี่เป็นวิธีที่ง่ายที่สุดในการ **convert images to text** สำหรับการประมวลผลต่อไป

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**ทำไมเราถึงเลือกไฟล์ `.txt` ข้างเคียง:**  
- ทำให้ความสัมพันธ์ชัดเจน—เปิด PNG แล้วเปิด TXT เพื่อเปรียบเทียบ  
- ไม่ต้องใช้ฐานข้อมูลหรือชั้นเก็บข้อมูลเพิ่มเติมในโครงการขนาดเล็ก

## ขั้นตอนที่ 5: สรุปด้วยข้อความเสร็จสิ้นที่เป็นมิตร

ข้อความคอนโซลที่เรียบร้อยจะแจ้งให้คุณทราบเมื่อทุกอย่างเสร็จสิ้น

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

เมื่อคุณรันโปรแกรม คุณจะเห็นผลลัพธ์เช่น

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

แต่ละไฟล์ PNG ตอนนี้จะมีไฟล์ `.txt` คู่ที่บรรจุข้อความที่ดึงออกมา

## ตัวอย่างทำงานเต็มรูปแบบ (All Steps Combined)

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ได้ ไม่มีส่วนใดหาย—เพียงแทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางเต็มของภาพของคุณ

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

- สำหรับแต่ละ `image.png` ใน `C:\MyImages` จะมี `image.txt` ปรากฏข้างเคียง
- คอนโซลจะแสดงบรรทัดความคืบหน้า ทำให้ติดตามแบตช์ขนาดใหญ่ได้ง่าย
- ไม่ต้องเขียนลูปหรือจัดการเธรดด้วยตนเอง—`BatchOcrProcessor` จัดการทั้งหมด

## คำถามทั่วไป & กรณีขอบ

### ถ้าภาพของฉันไม่ใช่ PNG?

เพียงเปลี่ยนอาร์กิวเมนต์ที่สองใน `ProcessFolder` เป็น `"*.jpg"` หรือ `"*.*"` เพื่อรวมไฟล์ทั้งหมด เครื่องมือ OCR ทำงานกับรูปแบบแรสเตอร์ส่วนใหญ่

### ใช้หน่วยความจำเท่าไหร่?

`BatchOcrProcessor` โหลดภาพหนึ่งภาพต่อเธรด ด้วย `Environment.ProcessorCount` ตั้งเป็นเช่น 8 คอร์ คุณจะมีภาพแปดภาพในหน่วยความจำพร้อมกัน หากเกิดข้อยกเว้น OutOfMemory ให้ลดระดับการทำงานแบบขนานลง:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### ฉันสามารถปรับแต่งภาษาของ OCR ได้หรือไม่?

ได้เลย หลังจากสร้าง engine ให้ตั้งค่า property `Language` ของมัน:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose รองรับหลายภาษา; เพียงเพิ่มแพคเกจ NuGet ที่เหมาะสมหากจำเป็น

### แล้วการจัดการข้อผิดพลาดล่ะ?

ห่อคอลแบ็กด้วยบล็อก try/catch แล้วบันทึกความล้มเหลว Processor จะดำเนินการต่อกับไฟล์ถัดไป ป้องกันไม่ให้ภาพที่เสียหายหนึ่งไฟล์ทำให้การรันทั้งหมดหยุด

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## เคล็ดลับระดับมืออาชีพสำหรับการขยายขนาด

- **Chunk the folder**: หากคุณมีไฟล์หลายหมื่นไฟล์ ให้แยกเป็นโฟลเดอร์ย่อยและรันหลายงาน batch ตามลำดับ
- **Use a cloud VM**: เครื่องที่มีคอร์มากกว่า (เช่น 32‑core) จะทำงานเสร็จเร็วมาก เพียงจำไว้ว่าต้องปรับขีดจำกัดลิขสิทธิ์
- **Post‑process the text**: หลังการดึงข้อมูล คุณอาจต้องใช้ regex เพื่อดึงหมายเลขใบแจ้งหนี้หรือวันที่ ไฟล์ `.txt` เป็นอินพุตที่สมบูรณ์สำหรับ pipeline ดังกล่าว

## สรุป

ตอนนี้คุณมีสูตรที่มั่นคงและพร้อมใช้งานในระดับ production สำหรับ **how to batch OCR** ไดเรกทอรีของ PNG, **extract text PNG** ไฟล์, และ **convert images to text** ด้วย Aspose.OCR ใน C# ตัวอย่างนี้เป็นอิสระ ครอบคลุมเหตุผล “ทำไม” ของแต่ละบรรทัด และรวมเคล็ดลับสำหรับการจัดการงานที่ใหญ่ขึ้นหรือประเภทไฟล์ที่ต่างกัน

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเปลี่ยนคอลแบ็กให้ผลลัพธ์ส่งไปยังฐานข้อมูล หรือเพิ่มการประมวลผลภาพล่วงหน้า (เช่น การแก้ไขการเอียง) ก่อน OCR รูปแบบนี้ขยายได้ดี คุณจึงสามารถปรับใช้กับสถานการณ์ batch‑processing ใด ๆ ที่เจอ

ขอให้เขียนโค้ดอย่างสนุกสนาน และขอให้ pipeline OCR ของคุณเร็วและปราศจากข้อผิดพลาด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
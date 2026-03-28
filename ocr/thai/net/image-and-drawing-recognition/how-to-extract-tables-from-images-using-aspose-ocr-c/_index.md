---
category: general
date: 2026-03-28
description: เรียนรู้วิธีดึงตารางจากภาพด้วย Aspose OCR ใน C# คู่มือนี้ครอบคลุมการตรวจจับตารางในภาพ,
  การโหลดภาพสำหรับ OCR และการดึงตารางจากไฟล์ PNG.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: th
og_description: บทแนะนำแบบขั้นตอนต่อขั้นตอนเกี่ยวกับวิธีการดึงตารางจากภาพด้วย Aspose
  OCR ใน C#. รวมถึงโค้ด คำอธิบาย และเคล็ดลับสำหรับการตรวจจับตารางในไฟล์ภาพ.
og_title: วิธีดึงตารางจากภาพโดยใช้ Aspose OCR (C#)
tags:
- Aspose OCR
- C#
- Table Extraction
title: วิธีดึงตารางจากภาพโดยใช้ Aspose OCR (C#)
url: /th/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการสกัดตารางจากรูปภาพโดยใช้ Aspose OCR (C#)

เคยสงสัย **วิธีสกัดตาราง** จากใบแจ้งหนี้ที่สแกนหรือภาพหน้าจอของสเปรดชีตหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ เราต้องแปลงรูปภาพของตารางให้เป็นข้อมูลที่สามารถสืบค้นได้—โดยทั่วไปเป็น CSV หรือ DataTable ข่าวดีคือ Aspose OCR ทำให้เรื่องนี้ง่ายเหมือนเค้ก และคุณสามารถทำได้ในไม่กี่บรรทัดของ C#  

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งแต่ **load image for OCR**, ไปจนถึง **detect tables in image**, และสุดท้าย **extract table from image** พร้อมบันทึกเป็นไฟล์ CSV เมื่อเสร็จคุณจะได้แอปคอนโซลพร้อมใช้งานที่สามารถ **extract tables from PNG** (หรือบิตแมปที่รองรับ) ได้อย่างไม่มีปัญหา

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม โปรดตรวจสอบว่าคุณมี:

- .NET 6.0 SDK หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Framework ด้วย)
- Visual Studio 2022 (หรือ IDE ที่คุณชอบ)
- ไฟล์ลิขสิทธิ์ Aspose.OCR for .NET (คุณสามารถเริ่มด้วยรุ่นทดลองฟรี)
- ตัวอย่างรูปภาพที่มีตาราง (เช่น `invoice_table.png`)

หากรายการใดดูแปลกใหม่ อย่ากังวล—เพียงติดตั้ง .NET SDK แล้วดาวน์โหลดแพคเกจ NuGet แล้วคุณก็พร้อมใช้งาน

## ภาพรวมของโซลูชัน

ในระดับสูง กระบวนการทำงานมีดังนี้:

1. **โหลดรูปภาพ** ที่ต้องการประมวลผล
2. **รันการจดจำ OCR** เพื่อให้เครื่องรู้ว่าข้อความอยู่ที่ไหน
3. **สร้าง TableExtractor** เพื่อสแกนผลลัพธ์ OCR หาโครงสร้างแบบตาราง
4. **สกัดตารางที่ตรวจพบทั้งหมด** แล้วเลือกตารางที่ต้องการ
5. **บันทึกตาราง** เป็น CSV (หรือรูปแบบอื่นที่คุณต้องการ)

แต่ละขั้นตอนจะอธิบายรายละเอียดต่อไป พร้อมโค้ดตัวอย่างที่คุณสามารถคัดลอก‑วางได้

<img src="table_extraction_example.png" alt="how to extract tables from image example" width="600">

*(ภาพด้านบนแสดงตัวอย่างตารางใบแจ้งหนี้ที่เราจะสกัด)*

## ขั้นตอนที่ 1 – โหลดรูปภาพสำหรับ OCR

สิ่งแรกที่ต้องทำคือบอก Aspose OCR ว่าไฟล์ใดจะอ่าน ไลบรารีรองรับ PNG, JPEG, BMP, TIFF และรูปแบบอื่น ๆ นี่คือโค้ดขั้นต่ำ:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**ทำไมขั้นตอนนี้สำคัญ:**  
`Image.FromFile` ทำการถอดรหัส PNG (หรือบิตแมปใด ๆ) ให้เป็นรูปแบบที่เครื่อง OCR เข้าใจ หากข้ามขั้นตอนนี้หรือส่งไฟล์ที่เสียหาย การเรียก `Recognize()` ต่อไปจะโยนข้อยกเว้น

> **Pro tip:** หากคุณต้องจัดการกับ PDF ขนาดใหญ่ ให้แยกแต่ละหน้าเป็นรูปภาพก่อน—ไม่เช่นนั้นเครื่อง OCR จะหมดหน่วยความจำ

## ขั้นตอนที่ 2 – จดจำหน้า (จำเป็นก่อนการตรวจจับตาราง)

การจดจำแปลงข้อมูลพิกเซลดิบให้เป็นเลย์เอาต์ข้อความที่ค้นหาได้ หากไม่มีขั้นตอนนี้ `TableExtractor` จะไม่มีข้อมูลทำงาน

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**อะไรเกิดขึ้นเบื้องหลัง?**  
Aspose OCR รันตัวตรวจจับข้อความแบบ neural‑network แล้วสร้างโครงสร้างลำดับชั้นของอ็อบเจกต์ `Page`, `Paragraph`, และ `Word` ตัวตรวจจับตารางจะตรวจสอบความสัมพันธ์เชิงพื้นที่ระหว่างคำเหล่านั้น

หากคุณประมวลผลรูปภาพหลายรูปในลูป ควรใช้อินสแตนซ์ `OcrEngine` เดียวแล้วสลับคุณสมบัติ `Image`—วิธีนี้ช่วยลดภาระการจัดสรรหน่วยความจำ

## ขั้นตอนที่ 3 – สร้าง TableExtractor และตรวจจับตารางในรูปภาพ

เมื่อมีข้อมูล OCR แล้ว เราสามารถให้ Aspose ค้นหาตารางได้ คลาส `TableExtractor` ทำหน้าที่นี้โดยตรง

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**ทำไมต้องใช้ `ExtractAll()`?**  
รูปภาพหนึ่งภาพอาจมีหลายตาราง (เช่น รายงานหลายส่วน) `ExtractAll()` คืนค่า `List<Table>` เพื่อให้คุณวนลูป เลือกตารางที่ต้องการ หรือแม้แต่รวมตารางเข้าด้วยกันในภายหลัง

หากคุณต้องการตารางแรกเท่านั้น สามารถใช้ `extractedTables[0]` ได้อย่างปลอดภัย แต่ควรตรวจสอบให้แน่ใจว่ารายการไม่ว่างเพื่อหลีกเลี่ยง `IndexOutOfRangeException`

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## ขั้นตอนที่ 4 – บันทึกตารางที่สกัดเป็น CSV (หรือรูปแบบอื่น)

Aspose ทำการส่งออกได้อย่างง่ายดาย คลาส `Table` มีเมธอด `SaveCsv`, `SaveXls`, และ `SaveJson` ในตัว นี่คือตัวอย่างการเขียนไฟล์ CSV:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**CSV จะมีลักษณะอย่างไร?**  
สมมติว่าภาพต้นฉบับมีตาราง 4 × 3 เซลล์ CSV ที่ได้อาจเป็นดังนี้:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

คุณสามารถเปิดไฟล์นี้ใน Excel, Power BI หรือส่งต่อโดยตรงเข้าสู่ pipeline ข้อมูลของคุณ

## ตัวอย่างเต็มขั้นตอน End‑to‑End

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และทำงานได้เอง คัดลอกไปใส่ในโปรเจกต์คอนโซลใหม่ (`dotnet new console`) แล้วรัน ตรวจสอบให้แน่ใจว่าได้ติดตั้งแพคเกจ NuGet `Aspose.OCR` (`dotnet add package Aspose.OCR`)

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรันโปรแกรม ควรเห็นข้อความประมาณนี้:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

เปิด `invoice_table.csv` คุณจะพบแถวและคอลัมน์ที่ตรงกับรูปภาพต้นฉบับ

## คำถามทั่วไป & กรณีขอบ

### ถ้ารูปภาพเป็น JPEG แทน PNG จะทำอย่างไร?

โค้ดเดียวกันทำงานได้—เพียงเปลี่ยนนามสกุลไฟล์ใน `Image.FromFile` Aspose OCR ตรวจจับรูปแบบโดยอัตโนมัติ ดังนั้น **extract tables from png** ไม่ใช่เงื่อนไขที่เข้มงวด; มันทำงานกับบิตแมปที่รองรับทุกประเภท

### ตารางของฉันมีเซลล์ที่รวมกัน จะถูกเก็บไว้หรือไม่?

เซลล์ที่รวมกันจะถูกจัดเป็นคอลัมน์แยกในผลลัพธ์ CSV เนื่องจาก CSV ไม่รองรับการรวมเซลล์ หากต้องการรูปแบบที่เก็บการรวมเซลล์ไว้ (เช่น Excel) ให้ใช้ `SaveXls` แทน:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### การตรวจจับพลาดคอลัมน์หนึ่ง ควรทำอย่างไรเพื่อเพิ่มความแม่นยำ?

- เพิ่มความละเอียดของรูปภาพ (≥300 dpi เป็นค่าที่เหมาะสม)
- ก่อนประมวลผล: แปลงเป็นสีเทา, เพิ่มคอนทราสต์, หรือใช้ฟิลเตอร์ deskew
- ปรับตั้งค่า Aspose OCR เช่น `PageSegMode` หรือ `Language` หากตารางมีอักขระที่ไม่ใช่ละติน

### สามารถสกัดตารางจาก PDF โดยตรงได้หรือไม่?

ทำได้ โดยแปลงแต่ละหน้าของ PDF เป็นรูปภาพก่อน (ใช้ `Aspose.PDF` หรือไลบรารีแปลง PDF‑to‑image ใดก็ได้) แล้วส่งรูปภาพเหล่านั้นเข้าสู่ workflow เดียวกัน

## เคล็ดลับสำหรับการใช้งานในระดับ Production

1. **ห่อ OCR ด้วย try/catch** – สภาพแวดล้อมที่ใช้ลิขสิทธิ์แบบเครือข่ายอาจโยนข้อยกเว้นเรื่องลิขสิทธิ์
2. **Dispose อ็อบเจกต์ `Image`** – ใช้บล็อก `using` เพื่อปล่อยทรัพยากรเนทีฟ
3. **บันทึกคะแนนความเชื่อมั่น** – `TableExtractor` มีคุณสมบัติ `Table.Confidence` ที่คุณสามารถเก็บไว้เพื่อตรวจสอบคุณภาพ
4. **ประมวลผลแบบแบตช์** – เมื่อต้องจัดการกับใบแจ้งหนี้หลายร้อยใบ ให้ทำการเรียก OCR แบบขนาน แต่ต้องปฏิบัติตามแนวทางความปลอดภัยของเธรดในลิขสิทธิ์

## ขั้นตอนต่อไป

ตอนนี้คุณรู้แล้วว่า **วิธีสกัดตาราง** จากรูปภาพแล้ว คุณอาจอยากสำรวจต่อ:

- **Detect tables in image** บนวิดีโอ (ใช้ `TableExtractor` ของ Aspose กับแต่ละเฟรม)
- **Load image for OCR** จาก Web API เพื่อสร้างบริการสกัดตารางบนคลาวด์
- **Extract tables from PNG** ที่เก็บใน Azure Blob Storage พร้อมบูรณาการกับ Azure Functions สำหรับการประมวลผลแบบ Serverless

ทดลองกับรูปแบบไฟล์ต่าง ๆ ปรับตั้งค่า OCR หรือส่งออก CSV ตรงเข้าสู่ฐานข้อมูลได้เลย ท้องฟ้าเป็นขอบเขตของคุณ

---

*Happy coding! หากคุณเจออุปสรรคหรือมีไอเดียปรับปรุงใด ๆ ฝากคอมเมนต์ไว้ด้านล่าง เราจะร่วมกันหาทางแก้ไข*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
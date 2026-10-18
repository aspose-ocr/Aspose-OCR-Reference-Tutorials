---
category: general
date: 2026-02-28
description: สร้าง PDF ที่ค้นหาได้ใน C# โดยการรวมภาพในแนวตั้ง เรียนรู้วิธีการจัดเรียงภาพในแนวตั้งและแปลงหน้า
  PDF ที่สแกนด้วย Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้ใน C# โดยการรวมภาพในแนวตั้ง คู่มือฉบับนี้แสดงวิธีการจัดเรียงภาพในแนวตั้งและแปลงหน้า
  PDF ที่สแกนโดยใช้ Aspose OCR.
og_title: สร้าง PDF ที่ค้นหาได้ใน C# – รวมภาพในแนวตั้ง
tags:
- Aspose OCR
- C#
- PDF generation
title: สร้าง PDF ที่ค้นหาได้ใน C# – รวมภาพในแนวตั้ง
url: /th/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้ใน C# – รวมภาพในแนวตั้ง

เคยต้องการ **create searchable PDF** จากภาพ PNG ที่สแกนหลายไฟล์แต่ไม่แน่ใจว่าจะเริ่มอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการอัตโนมัติเอกสาร จุดเจ็บปวดที่ใหญ่ที่สุดคือการแปลงกองไฟล์ภาพให้เป็น PDF ที่เรียบร้อยและค้นหาได้ซึ่งคุณสามารถทำดัชนีและแชร์ได้.

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์พร้อมรันที่แสดงให้คุณเห็น **how to stack images vertically**, **combine images vertically**, และสุดท้าย **convert scanned pages PDF** เป็นเอกสารที่ค้นหาได้เดียวโดยใช้เครื่องมือ GPU‑accelerated ของ Aspose.OCR. เมื่อจบคุณจะมีโปรแกรมที่เป็นอิสระซึ่งสามารถใส่ลงในโซลูชัน .NET ใดก็ได้.

> **สิ่งที่คุณจะได้เรียนรู้**
> - เริ่มต้น OCR engine ด้วยการสนับสนุน GPU.
> - ประมวลผลชุดภาพแบบขนาน.
> - **Combine images vertically** เพื่อจำลองการสแกนหลายหน้า.
> - ส่งออก PDF ที่ค้นหาได้และรายงาน JSON รายละเอียดสำหรับการวิเคราะห์ต่อไป.

## ข้อกำหนดเบื้องต้น

- .NET 6+ (โค้ดคอมไพล์ได้กับ .NET 6, .NET 7 หรือ .NET 8)
- แพคเกจ NuGet ของ Aspose.OCR (`Install-Package Aspose.OCR`)
- เครื่องที่เปิดใช้งาน GPU หากคุณต้องการใช้การตั้งค่า `ProcessingMode.Gpu` (สามารถใช้โหมด CPU แทนได้)
- โฟลเดอร์ที่มีไฟล์ PNG/JPEG ที่สแกนอยู่ไม่กี่ไฟล์ (ตัวอย่างใช้ `page1.png`, `page2.png`, `page3.png`)

ไม่มีบริการภายนอก ไม่มีไฟล์การกำหนดค่าที่ซ่อนอยู่—เพียงแค่ C# ธรรมดา.

## ขั้นตอนที่ 1 – ตั้งค่า OCR Engine เพื่อ **Create Searchable PDF**

ก่อนอื่นเราจะสร้าง `OcrEngine`, เปิดการเร่งความเร็วด้วย GPU, เลือกภาษาอังกฤษเป็นภาษาที่ใช้, และเพิ่มฟิลเตอร์การเตรียมข้อมูลสองตัว ฟิลเตอร์เหล่านี้ช่วยเพิ่มความแม่นยำโดยการทำให้หน้าที่เอียงตรง (`DeskewFilter`) และกำจัดสัญญาณรบกวน (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Why this matters:** OCR engine ทำงานหนักในการจดจำข้อความ การเปิดใช้งาน `ProcessingMode.Gpu` สามารถลดเวลาการจดจำลงครึ่งหนึ่งบนการ์ดกราฟิกสมัยใหม่, ในขณะที่ฟิลเตอร์ช่วยลดศิลปะการสแกนที่พบบ่อยซึ่งอาจทำให้ผลลัพธ์เป็นข้อความที่อ่านไม่ออก.

## ขั้นตอนที่ 2 – ตั้งค่า Batch Processor เพื่อ **Convert Scanned Pages PDF** อย่างมีประสิทธิภาพ

การประมวลผลแต่ละหน้าทีละหน้าเป็นวิธีที่ดีสำหรับภาพไม่กี่ภาพ, แต่โครงการในโลกจริงมักมีหลายสิบหรือหลายร้อยหน้า Aspose.OCR’s `OcrBatchProcessor` ให้เรารันการจดจำแบบขนาน, ทำให้ขั้นตอน **convert scanned pages pdf** เร็วขึ้นอย่างมาก.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Pro tip:** หากคุณใช้เครื่องที่มี CPU เท่านั้น, ตั้งค่า `ProcessingMode = ProcessingMode.Cpu`. Batch processor ยังจะเคารพ `MaxDegreeOfParallelism`, ดังนั้นคุณสามารถปรับให้เหมาะสมเพื่อหลีกเลี่ยงการโหลดเครื่องเกิน.

## ขั้นตอนที่ 3 – รัน OCR บน Batch และรวบรวมผลลัพธ์

ตอนนี้เราจดจำข้อความจริง ๆ เมธอด `Recognize` จะคืนรายการของอ็อบเจกต์ `OcrResult`, แต่ละอ็อบเจกต์มีทั้งภาพต้นฉบับและข้อความที่สกัดออกมา.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

ในขั้นตอนนี้คุณมีทุกอย่างที่ต้องการเพื่อ **create searchable PDF**: ภาพ (ยังอยู่ในหน่วยความจำ) และเลเยอร์ข้อความที่เกี่ยวข้อง.

## ขั้นตอนที่ 4 – **Combine Images Vertically** และสร้าง Searchable PDF

เอกสารที่สแกนส่วนใหญ่เป็น PDF หลายหน้า, ดังนั้นเราต้องเชื่อมต่อภาพแต่ละหน้าต่างเป็นภาพสูงหนึ่งภาพที่สะท้อนการจัดเรียงแบบกองจริง Aspose.OCR มีเมธอด `Image.CombineVertical` สำหรับจุดประสงค์นี้โดยเฉพาะ.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

ไฟล์ที่ได้ (`combined_searchable.pdf`) จะมีข้อความที่สามารถเลือกและค้นหาได้ใต้ภาพแต่ละหน้า—ตรงกับสิ่งที่คุณต้องการเพื่อ **create searchable PDF** จากแหล่งสแกน.

![ตัวอย่างการสร้าง searchable PDF](/images/create-searchable-pdf.png "ตัวอย่างการสร้าง searchable pdf")

*ข้อความแทนภาพ: ตัวอย่างการสร้าง searchable pdf แสดง PDF ที่รวมกับข้อความที่ค้นหาได้.*

**Why vertical stacking?** ไลบรารี OCR จำนวนมากถือแต่ละภาพเป็นหน้าที่แยกกัน. โดยการจัดเรียงแนวตั้ง เราจะรักษาลำดับหน้าของ PDF ไว้ครบถ้วนพร้อมยังใช้การรัน OCR ครั้งเดียวสำหรับเอกสารทั้งหมด.

## ขั้นตอนที่ 5 – ส่งออก JSON รายละเอียดสำหรับหน้าแรก (เหมาะสำหรับกระบวนการต่อเนื่อง)

บางครั้งคุณต้องการมากกว่า PDF; บางทีคุณอาจต้องการส่งข้อมูล OCR ไปยังฐานข้อมูลหรือ pipeline ของการเรียนรู้ของเครื่อง Aspose.OCR ให้คุณแปลงแต่ละ `OcrResult` เป็น JSON, คงบ็อกซ์ขอบเขต, คะแนนความเชื่อมั่น, และอื่น ๆ.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**ตัวอย่าง JSON ที่คาดหวัง (ตัดทอน):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

ตอนนี้คุณสามารถส่ง JSON นี้ไปยังระบบต่อเนื่องใดก็ได้—ไม่ว่าจะเป็นการทำดัชนีข้อความใน Elasticsearch หรือส่งไปยังแดชบอร์ดวิเคราะห์ที่กำหนดเอง.

---

## วิธีการ **Stack Images Vertically** – สรุปสั้น

หากคุณสงสัย **how to stack images vertically** โดยไม่ใช้ Aspose, คุณสามารถใช้ `System.Drawing` เพื่อสร้างบิตแมพใหม่และวาดแต่ละหน้าต่อกัน. อย่างไรก็ตาม `Image.CombineVertical` ที่มาพร้อมกับ Aspose จะจัดการ DPI, รูปแบบพิกเซล, และการจัดการหน่วยความจำให้คุณ, ทำให้เป็นตัวเลือกที่เชื่อถือได้ที่สุดสำหรับโค้ดการผลิต.

### ทางเลือก: ใช้ `System.Drawing` (แค่เพื่อความสนใจ)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

วิธีการแบบแมนนวลทำงานได้, แต่คุณจะสูญเสียความสะดวกของการจัดการ DPI อัตโนมัติและความสามารถในการส่งผลลัพธ์กลับไปยัง `RecognizeToPdf` โดยตรง. ควรใช้ `CombineVertical` เว้นแต่คุณมีความต้องการเฉพาะที่แคบมาก.

## ปัญหาที่พบบ่อยและวิธีหลีกเลี่ยง

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑memory errors** เมื่อประมวลผลหลายสิบสแกนความละเอียดสูง | แต่ละภาพคงอยู่ในหน่วยความจำจนกว่า PDF จะถูกเขียน | ทำการ Dispose อ็อบเจกต์ `Image` ทันทีเมื่อเสร็จ (`using` blocks) หรือปรับขนาดภาพลงก่อนการรวม |
| **Garbage text** หลัง OCR | สแกนเอียงหรือคอนทราสต์ต่ำ | คงไว้ `DeskewFilter` และ `DenoiseFilter`; พิจารณาเพิ่ม `ContrastFilter` หากจำเป็น |
| **Missing searchable layer** | ใช้ `Recognize` แทน `RecognizeToPdf` | ตรวจสอบว่าคุณเรียก `ocrEngine.RecognizeToPdf` บนภาพที่รวมแล้ว |
| **GPU fallback fails** บนเครื่องที่ไม่มีไดรเวอร์ที่เหมาะสม | `ProcessingMode.Gpu` ทำให้เกิดข้อยกเว้น | ห่อการสร้าง engine ด้วย try/catch แล้วใช้ fallback ไปยัง `ProcessingMode.Cpu` |

## ขั้นตอนต่อไป – ขยาย Workflow

ตอนนี้คุณรู้วิธี **create searchable PDF**, คุณอาจต้องการ:

- **Batch‑process entire folders** ด้วย `Directory.GetFiles` และลูป `foreach`.
- **Add watermarks** ให้แต่ละหน้าก่อนการรวม (ใช้ `ImageProcessor` จาก Aspose.Imaging).
- **Split the searchable PDF back into individual pages** หากคุณต้องการ PDF แยกตามหน้าในภายหลัง (`PdfDocument.Split` จาก Aspose.PDF).
- **Integrate with Azure Blob Storage** เพื่อดึงภาพจากคลาวด์และอัปโหลด PDF สุดท้ายกลับไป.

การขยายเหล่านี้ทั้งหมดใช้แนวคิดหลักเดียวกัน: การตั้งค่า OCR, การจัดการภาพ, และการส่งออก PDF.

---

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **create searchable PDF** จากชุดภาพสแกนใน C#. ด้วยการเริ่มต้น `OcrEngine` ที่เปิดใช้งาน GPU, รัน batch แบบขนานด้วย `OcrBatchProcessor`, **combining images vertically**, และสุดท้ายเรียก `RecognizeToPdf`, คุณจะได้เอกสารที่เรียบร้อยและค้นหาได้พร้อมสำหรับการเก็บถาวรหรือทำดัชนี การส่งออก JSON เพิ่มเติมทำให้คุณมองเห็นผลลัพธ์ OCR อย่างเต็มที่, เปิดโอกาสสำหรับการวิเคราะห์หรือ workflow ที่กำหนดเอง.

ลองใช้งาน, ทดลองกับฟิลเตอร์ต่าง ๆ, แล้วคุณจะเห็น pipeline การอัตโนมัติเอกสารของคุณทำงานได้ราบรื่นขึ้นมาก. หากคุณพบปัญหาใด ๆ, แสดงความคิดเห็นได้—ขอให้เขียนโค้ดอย่างสนุก!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
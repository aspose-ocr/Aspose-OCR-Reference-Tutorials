---
category: general
date: 2025-12-27
description: สร้างตัวบันทึกคอนโซลใน C# และเปิดใช้งานการดาวน์โหลดอัตโนมัติไปยังตารางที่แก้ไขโดยใช้
  AsposeAI. เรียนรู้วิธีแสดงผลตารางที่แก้ไขได้ในไม่กี่ขั้นตอน.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: th
og_description: สร้างตัวบันทึกคอนโซลใน C# และเปิดใช้งานการดาวน์โหลดอัตโนมัติไปยังตารางที่แก้ไขโดยใช้
  AsposeAI. ทำตามคู่มือนี้เพื่อแสดงผลลัพธ์ของตารางที่แก้ไขอย่างรวดเร็ว.
og_title: สร้างตัวบันทึกคอนโซลและแก้ไขตารางด้วย AsposeAI
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: สร้างคอนโซลล็อกเกอร์และแก้ไขตารางด้วย AsposeAI
url: /th/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง console logger และแก้ไขตารางด้วย AsposeAI

เคยต้อง **สร้าง console logger** สำหรับ pipeline AI ด้วย C# แต่ไม่รู้จะเริ่มจากตรงไหนหรือไม่? ในคู่มือนี้เราจะพาคุณผ่านกระบวนการทั้งหมด—วิธีสร้าง console logger, เปิดใช้งานการดาวน์โหลดอัตโนมัติสำหรับไฟล์โมเดล, และสุดท้าย **วิธีแก้ไขตาราง** ที่ได้จาก OCR. เมื่อเสร็จแล้วคุณจะสามารถ **แสดงผลตารางที่แก้ไขแล้ว** ใน console ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด.

เราจะครอบคลุมทุกอย่างตั้งแต่การตั้งค่า logger ขั้นต้นจนถึงการทำความสะอาดขั้นสุดท้าย, เพื่อให้คุณไม่ต้องค้นหาเอกสารกระ散. ไม่จำเป็นต้องมีประสบการณ์กับ AsposeAI มาก่อน; ความเข้าใจพื้นฐานของ C# และ .NET ก็พอ. ระหว่างทางเราจะสอดแทรกเคล็ดลับเกี่ยวกับ **การตั้งค่า console logger** ที่ดีที่สุด, พูดถึงกรณีขอบ, และแสดงตัวอย่างผลลัพธ์ที่คาดว่าจะได้.

---

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้พร้อมใช้งาน:

- .NET 6.0 หรือใหม่กว่า (โค้ดใช้คุณลักษณะภาษาแบบสมัยใหม่)
- Visual Studio 2022 หรือ IDE ใด ๆ ที่รองรับโปรเจกต์ C#
- แพคเกจ NuGet **Aspose.AI** ติดตั้งแล้ว (`Install-Package Aspose.AI`)
- แพคเกจ NuGet **Aspose.OCR** ติดตั้งแล้ว (`Install-Package Aspose.OCR`)
- วัตถุผลลัพธ์ OCR ตัวอย่าง (`ocrResult`) จากการเรียก Aspose.OCR ก่อนหน้า

หากขาดสิ่งใดสิ่งหนึ่ง, ให้หยุดชั่วคราวและจัดเตรียมให้เรียบร้อย—คุณจะขอบคุณตัวเองในภายหลัง.

---

## ขั้นตอนที่ 1: สร้าง console logger และ initialise AsposeAI

สิ่งแรกที่เราต้องการคือ logger ที่เขียนตรงไปยัง console. สิ่งนี้ทำให้การดีบักเป็นเรื่องง่ายและให้ฟีดแบ็กแบบเรียลไทม์ขณะ engine AI ทำงาน.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**ทำไมจึงสำคัญ:**  
`ConsoleLogger` implements the `ILogger` interface, so any internal messages from AsposeAI (model loading, post‑processor status) appear instantly in your terminal. It’s the simplest way to **setup console logger** without pulling in external logging frameworks.

> **Pro tip:** หากคุณต้องการบันทึกลงไฟล์ในภายหลัง, เพียงเปลี่ยน `ConsoleLogger` เป็น logger ที่กำหนดเองซึ่ง implements `ILogger`—ส่วนอื่นของโค้ดจะไม่ต้องแก้ไข.

---

## ขั้นตอนที่ 2: เปิดใช้งานการดาวน์โหลดอัตโนมัติสำหรับโมเดล AI

AsposeAI สามารถดึงไฟล์โมเดลที่จำเป็นแบบ on‑the‑fly. การเปิดใช้งานนี้ช่วยคุณหลีกเลี่ยงการดาวน์โหลดไฟล์ไบนารีขนาดใหญ่ด้วยตนเอง.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**อะไรอาจผิดพลาด?**  
หาก `DirectoryModelPath` ชี้ไปยังตำแหน่งที่อ่าน‑อย่าง‑เดียว, การดาวน์โหลดอัตโนมัติจะล้มเหลวและคุณจะเห็น exception ใน console. ตรวจสอบให้แน่ใจว่าโฟลเดอร์มีอยู่และแอปของคุณมีสิทธิ์เขียน.

---

## ขั้นตอนที่ 3: สร้าง table post‑processor (วิธีแก้ไขตาราง)

ตารางที่ดึงจาก OCR มักจะยุ่งยาก—เซลล์รวม, ขอบหาย, หรือข้อความที่จัดตำแหน่งไม่ตรง. `TableAIProcessor` ของ AsposeAI สามารถทำความสะอาดได้โดยอัตโนมัติ.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**ทำไมต้องใช้ AUTO mode?**  
`AITableDetectionMode.AUTO` ให้ engine ตรวจสอบผลลัพธ์ OCR และตัดสินใจว่าต้องการการแก้ไขหรือไม่. หากคุณต้องการควบคุมด้วยตนเอง, สามารถใช้ `MANUAL` และเรียก `RunCorrection()` เองได้.

---

## ขั้นตอนที่ 4: ผูก post‑processor กับการตั้งค่าของมัน

ตอนนี้เราจะเชื่อมทุกอย่างเข้าด้วยกัน—logger, การตั้งค่าโมเดล, และตัวประมวลผลตาราง.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

ในขั้นตอนนี้ engine AI จะรู้ *ที่ไหน* ที่จะเก็บโมเดล, *อย่างไร* ที่จะบันทึก, และ *อะไร* ที่จะทำ post‑processing. การแยกความรับผิดชอบแบบนี้ทำให้การเปลี่ยนแปลงในอนาคตทำได้ง่ายดาย.

---

## ขั้นตอนที่ 5: รัน post‑processor บนผลลัพธ์ OCR ของคุณ

สมมติว่าคุณมี `ocrResult` จาก Aspose.OCR อยู่แล้ว, เพียงส่งต่อให้ engine.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**แจ้งเตือนกรณีขอบ:**  
หาก `ocrResult` ไม่มีตาราง, processor จะข้ามการแก้ไขโดยไม่มีการแจ้งเตือน. คุณสามารถตรวจสอบ `tableProcessor.GetResult().Count` หลังจากรันเพื่อยืนยันว่ามีการประมวลผลจริงหรือไม่.

---

## ขั้นตอนที่ 6: ดึงและ **แสดงตารางที่แก้ไขแล้ว** ออกมา

สุดท้าย, เราจะดึงข้อความตารางที่ทำความสะอาดแล้วและพิมพ์ลง console.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

ผลลัพธ์จะมีลักษณะประมาณนี้ (ขึ้นอยู่กับภาพต้นฉบับของคุณ):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

หากคุณเห็นสตริงว่าง, ให้ตรวจสอบว่า OCR ตรวจจับตารางจริงหรือไม่และว่า `AllowAutoDownload` ทำงานสำเร็จหรือไม่.

---

## ขั้นตอนที่ 7: ทำความสะอาดทรัพยากร

การเป็นผู้ใช้ที่ดีหมายถึงการทำลายวัตถุหนักเมื่อใช้งานเสร็จ.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

การข้ามขั้นตอนนี้อาจทำให้ไฟล์แฮนด์เดิลเปิดค้างอยู่, โดยเฉพาะบน Windows ที่ไฟล์โมเดลจะถูกล็อก.

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมครบชุดที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์ console ใหม่. แทนที่ `"YOUR_DIRECTORY"` ด้วยพาธจริงและตรวจสอบให้แน่ใจว่า `ocrResult` ถูกเติมข้อมูลก่อนเรียก `RunPostprocessor`.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**ผลลัพธ์ที่คาดว่าจะเห็นใน console** (สมมติว่าภาพเป็นตารางง่าย):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

---

## คำถามที่พบบ่อย

- **ต้องการการเชื่อมต่ออินเทอร์เน็ตสำหรับการดาวน์โหลดอัตโนมัติหรือไม่?**  
  ใช่. ครั้งแรกที่ร้องขอโมเดล, AsposeAI จะติดต่อ CDN ของมัน. หลังจากไฟล์ถูกเก็บไว้ใน `DirectoryModelPath`, การรันต่อไปสามารถทำแบบออฟไลน์ได้.

- **ถ้าตารางของฉันมีเซลล์รวมจะทำอย่างไร?**  
  โมเดล AI จะพยายามแยกเซลล์ที่รวมกันโดยอิงจากสัญญาณภาพ. หากผลลัพธ์ไม่ตรง, ควรทำการพรี‑โปรเซสภาพ (เพิ่มคอนทราสต์, ปรับการหมุนให้ตรง) ก่อนทำ OCR.

- **สามารถประมวลผลหลายตารางพร้อมกันได้หรือไม่?**  
  ทำได้. `tableProcessor.GetResult()` คืนค่าเป็นรายการ; คุณสามารถวนลูปเพื่อพิมพ์แต่ละตารางได้.

- **`ConsoleLogger` ปลอดภัยต่อการทำงานหลายเธรดหรือไม่?**  
  มันเขียนโดยตรงไปยัง `System.Console`, ซึ่งปลอดภัยต่อการเขียนแบบง่ายหลายเธรด. สำหรับสถานการณ์ที่มีการเขียนหนักหลายเธรด, ควรใช้ logger ที่กำหนดเองพร้อมการซิงโครไนซ์.

---

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

ตอนนี้คุณรู้ **วิธีแก้ไขตาราง** แล้ว, คุณอาจต้องการ:

- **เปิดใช้งานการดาวน์โหลดอัตโนมัติ** สำหรับโมเดล AsposeAI อื่น ๆ (เช่น การแปลภาษา).
- **ตั้งค่า console logger** ด้วยระดับล็อกต่าง ๆ (Info, Warning, Error) เพื่อควบคุมละเอียดขึ้น.
- สำรวจการ **แสดงตารางที่แก้ไขแล้ว** ใน GUI (WinForms หรือ WPF) แทน console.
- ผสานการแก้ไขตารางกับ **การสกัดข้อมูล** เพื่อนำเข้าโดยตรงสู่ฐานข้อมูล.

แต่ละหัวข้อนี้ต่อยอดจากพื้นฐานที่เราตั้งไว้, ดังนั้นอย่ากลัวที่จะทดลอง.

---

## สรุป

เราได้เดินผ่านวงจรทั้งหมดของ **การสร้าง console logger**, การเปิดใช้งานการดาวน์โหลดอัตโนมัติ, และ **การแก้ไขตาราง** ด้วย AsposeAI, จบด้วยวิธีที่สะอาดในการ **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
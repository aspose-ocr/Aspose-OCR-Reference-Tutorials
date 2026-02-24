---
category: general
date: 2026-02-24
description: ทำการ OCR รูปภาพเป็นชุดอย่างรวดเร็วด้วย Aspose.OCR ใน C# เรียนรู้วิธีอ่านไฟล์จากไดเรกทอรี
  แยกข้อความจากรูปภาพ และแปลงรูปภาพเป็นข้อความในไม่กี่ขั้นตอน.
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: th
og_description: ทำการ OCR รูปภาพเป็นชุดใน C# ด้วย Aspose.OCR บทเรียนนี้แสดงวิธีอ่านไฟล์จากไดเรกทอรี,
  จำแนกข้อความจากรูปภาพและแปลงรูปภาพเป็นข้อความอย่างมีประสิทธิภาพ.
og_title: การทำ OCR รูปภาพเป็นชุดใน C# – คู่มือขั้นตอนเต็มแบบละเอียด
tags:
- C#
- OCR
- Aspose
title: OCR รูปภาพเป็นชุดใน C# – คู่มือเต็มสำหรับการสกัดข้อความ
url: /th/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การทำ OCR รูปภาพเป็นชุดใน C# – คู่มือเต็มเพื่อสกัดข้อความ

เคยต้องการ **batch OCR images** แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อลอง **extract text from images** เป็นจำนวนมากครั้งแรก ข่าวดีคือด้วยไม่กี่บรรทัดของ C# และ Aspose.OCR คุณสามารถแปลงโฟลเดอร์ที่เต็มไปด้วยรูปภาพให้เป็นไฟล์ `.txt` ที่เรียบร้อยได้อย่างรวดเร็ว

ในบทแนะนำนี้ เราจะพาคุณผ่านกระบวนการทั้งหมด: อ่านไฟล์จากไดเรกทอรี, ส่งรูปแต่ละรูปให้กับ OCR engine, และสุดท้าย **convert image to text** ไฟล์ที่คุณสามารถทำดัชนี, ค้นหา, หรือส่งต่อไปยัง pipeline ต่อไปได้ เมื่อเสร็จคุณจะมีแอปคอนโซลที่ทำงานอิสระซึ่งสามารถใส่ลงในโซลูชัน .NET ใดก็ได้

## สิ่งที่คุณต้องมี

- **.NET 6+** (ตัวอย่างคอมไพล์ด้วย .NET 6, แต่เวอร์ชันล่าสุดใดก็ทำงานได้)
- **Aspose.OCR** NuGet package (`Install-Package Aspose.OCR`)
- โฟลเดอร์ของไฟล์รูปภาพ (`.png`, `.jpg`, เป็นต้น) ที่คุณต้องการประมวลผล
- Visual Studio, Rider, หรือโปรแกรมแก้ไขที่คุณชื่นชอบ

ไม่มีไฟล์การกำหนดค่าเพิ่มเติม, ไม่มีบริการภายนอก—เพียงโค้ด C# ธรรมดาที่ทำงานบนเครื่องเท่านั้น

## การทำ OCR รูปภาพเป็นชุด – การตั้งค่าโปรเจกต์

ขั้นแรก, สร้างโปรเจกต์คอนโซลใหม่:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

คำสั่งนั้นจะสร้างโครงสร้างโปรเจกต์ขั้นต่ำและดึงไลบรารี OCR เข้ามา หลังจากการกู้คืนเสร็จสิ้นคุณพร้อมที่จะเพิ่มตรรกะหลัก

### อ่านไฟล์จากไดเรกทอรี

เราต้องบอกแอปของเราว่าไฟล์รูปภาพต้นทางอยู่ที่ไหนและไฟล์ข้อความผลลัพธ์ควรจะเก็บไว้ที่ไหน การใช้ `System.IO` ทำให้เรื่องนี้ง่ายดาย

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **ทำไมขั้นตอนนี้ถึงสำคัญ:** หากไดเรกทอรีผลลัพธ์ไม่มีอยู่ โปรแกรมจะโยนข้อยกเว้นเมื่อพยายามเขียนไฟล์ `.txt` `CreateDirectory` เป็นฟังก์ชันที่ทำงานแบบ idempotent—จะไม่ทำอะไรหากโฟลเดอร์มีอยู่แล้ว ดังนั้นจึงปลอดภัยที่จะเรียกใช้ทุกครั้งที่รัน

### จดจำข้อความจากรูปภาพและแปลงรูปภาพเป็นข้อความ

ตอนนี้เราจะเปิด OCR engine และวนลูปผ่านไฟล์ทุกไฟล์ที่พบ ลูปใช้ `Directory.GetFiles` พร้อมไวล์การ์ด (`*.*`) เพื่อดึงไฟล์ *ทั้งหมด* แต่คุณสามารถจำกัดตัวกรองเป็น `*.png` หรือ `*.jpg` หากต้องการ

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**เกิดอะไรขึ้นที่นี่?**  
- `ocrEngine.RecognizeImage(imagePath)` อ่านบิตแมพ, รันอัลกอริทึม OCR, และคืนค่าอ็อบเจกต์ `OcrResult`  
- `ocrResult.Text` มีการแทนข้อความแบบ plain‑text ของทุกอย่างที่ engine สามารถอ่านได้  
- `File.WriteAllText` สร้างไฟล์ใหม่ (หรือเขียนทับไฟล์ที่มีอยู่) ด้วยข้อความที่สกัดออกมา  

นี่คือ pipeline **batch OCR images** ทั้งหมดในน้อยกว่า 30 บรรทัดของโค้ด

## เคล็ดลับระดับมืออาชีพ & กรณีขอบ

| สถานการณ์ | คำแนะนำ |
|-----------|----------|
| รูปภาพมีขนาดใหญ่ ( > 5 MB ) | ปรับขนาดล่วงหน้าให้กว้างประมาณ ~1500 px เพื่อเร่งการจดจำโดยไม่สูญเสียความแม่นยำ |
| คุณต้องการรองรับ PDF | แปลงแต่ละหน้า PDF เป็นรูปภาพก่อน (เช่น ใช้ `Aspose.PDF`) แล้วส่งเข้าไปในลูปเดียวกัน |
| ไฟล์บางไฟล์ไม่ใช่รูปภาพ (เช่น `.txt`) | เพิ่มตัวกรองง่าย ๆ: `if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| คุณต้องการการสนับสนุนหลายภาษา | ตั้งค่า `ocrEngine.Language = Language.English | Language.Spanish;` ก่อนลูป |
| คุณต้องการรายงานความคืบหน้า | เขียน `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` ภายใน foreach |

> **เคล็ดลับระดับมืออาชีพ:** ห่อการเรียก OCR ด้วย `try/catch` บางครั้งภาพที่เสียหายอาจทำให้ `RecognizeImage` โยนข้อยกเว้น; การจัดการจะป้องกันไม่ให้ชุดทั้งหมดหยุดทำงาน

## ผลลัพธ์ที่คาดหวัง

เมื่อโปรแกรมทำงานเสร็จ, `outputFolder` จะมีไฟล์ `.txt` สำหรับแต่ละรูปภาพต้นฉบับ:

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

แต่ละไฟล์จะบรรจุข้อความดิบที่ engine สกัดออกมา, ตัวอย่างเช่น:

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

คุณสามารถส่งไฟล์เหล่านี้เข้าไปในดัชนีการค้นหา, ทำการวิเคราะห์ความรู้สึก, หรือเก็บเป็นเอกสารเพื่อการปฏิบัติตามกฎระเบียบได้

## คำถามที่พบบ่อย

**Q: นี้ทำงานบน Linux ได้หรือไม่?**  
A: แน่นอน. Aspose.OCR รองรับหลายแพลตฟอร์ม, และ API `System.IO` ที่ใช้ที่นี่เป็นแบบ OS‑agnostic. เพียงปรับเส้นทางโฟลเดอร์ (`/home/user/images`).

**Q: ถ้าฉันต้องการ **read files from directory** อย่างเรียกซ้ำ จะทำอย่างไร?**  
A: เปลี่ยน `SearchOption.TopDirectoryOnly` เป็น `SearchOption.AllDirectories`. ระวังปัญหาการอนุญาตในโฟลเดอร์ที่ลึกกว่า

**Q: OCR มีความแม่นยำแค่ไหน?**  
A: ความแม่นยำขึ้นอยู่กับคุณภาพของภาพ, ฟอนต์, และภาษา. เพื่อผลลัพธ์ที่ดีที่สุด, ใช้การสแกนความละเอียดสูงและพื้นหลังที่สะอาด. คุณยังสามารถปรับ `ocrEngine.Config` เพื่อเปิดใช้งานการแก้ไขการเอียงหรือการลดสัญญาณรบกวนได้.

## สรุป

คุณเพิ่งเรียนรู้วิธี **batch OCR images** ใน C# ด้วย Aspose.OCR, ตั้งแต่การอ่านไฟล์จากไดเรกทอรีจนถึง **recognize text from image** และสุดท้าย **convert image to text** ไฟล์ที่คุณสามารถเก็บหรือประมวลผลต่อไป ตัวอย่างที่ทำงานได้เต็มรูปแบบข้างต้นควรทำงานได้ทันที, และส่วนเคล็ดลับให้แผนที่สำหรับการขยายหรือปรับแต่งโซลูชัน

ขั้นตอนต่อไป? ลองเพิ่ม UI อย่างง่ายด้วย WinForms หรือ WPF, ผสานผลลัพธ์กับ Azure Cognitive Search, หรือทดลองใช้ภาษาอื่นที่ Aspose.OCR รองรับ. ไม่มีขีดจำกัดเมื่อคุณเชี่ยวชาญลูปหลักแล้ว

ขอให้สนุกกับการเขียนโค้ด, และขอให้ชุด OCR ของคุณปราศจากข้อผิดพลาด!

![แผนภาพของกระบวนการ OCR รูปภาพเป็นชุด](batch-ocr-images-diagram.png "ขั้นตอนการทำงานของ Batch OCR images")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
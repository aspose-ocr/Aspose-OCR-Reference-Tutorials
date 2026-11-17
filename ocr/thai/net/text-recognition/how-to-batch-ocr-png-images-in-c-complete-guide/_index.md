---
category: general
date: 2026-03-17
description: วิธีทำ OCR รูป PNG แบบเป็นชุดใน C# อย่างรวดเร็ว เรียนรู้การดึงข้อความจากไฟล์
  PNG, แปลง PNG เป็นข้อความ, และอ่านรูปจากโฟลเดอร์ด้วยสคริปต์ง่าย ๆ.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: th
og_description: วิธีทำ OCR รูป PNG เป็นชุดใน C# ด้วยโค้ดทีละขั้นตอน ดึงข้อความจากไฟล์
  PNG แปลง PNG เป็นข้อความ และอ่านรูปจากไดเรกทอรีได้อย่างง่ายดาย
og_title: วิธีทำ OCR รูป PNG แบบเป็นชุดใน C# – คู่มือฉบับสมบูรณ์
tags:
- OCR
- C#
- Image Processing
title: วิธีทำ OCR รูปภาพ PNG แบบแบตช์ใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR แบบกลุ่มสำหรับไฟล์ PNG ใน C# – คู่มือครบถ้วน

เคยสงสัย **วิธีทำ OCR แบบกลุ่ม** สำหรับโฟลเดอร์ที่เต็มไปด้วยภาพหน้าจอโดยไม่ต้องเปิดไฟล์ทีละไฟล์หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักถามวิธีทำ OCR แบบกลุ่มสำหรับคอลเลกชัน PNG จำนวนมาก โดยเฉพาะเมื่อเป้าหมายคือการ **ดึงข้อความจากไฟล์ PNG** เพื่อการวิเคราะห์ต่อไป  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่าง C# ที่พร้อมรันซึ่ง **ดึงข้อความจากไฟล์ PNG** , **แปลง PNG เป็นข้อความ** , และแสดงวิธีที่ดีที่สุดในการ **อ่านภาพจากไดเรกทอรี**. เมื่อเสร็จคุณจะมีสคริปต์เดียวที่สร้างไฟล์ `.txt` ข้าง ๆ ทุกภาพ ช่วยคุณประหยัดเวลานานหลายชั่วโมงจากการคัดลอก‑วางด้วยตนเอง

## สิ่งที่คุณจะได้ทำ

- เริ่มต้นเครื่องมือ OCR ครั้งเดียวและใช้ซ้ำสำหรับทั้งชุด  
- สแกนทุก `*.png` ในโฟลเดอร์ที่กำหนดโดยไม่ต้องเขียนลูปเอง  
- เขียนผล OCR ของแต่ละไฟล์ลงในไฟล์ข้อความของมันเอง โดยคงชื่อไฟล์เดิมไว้  
- จัดการกรณีขอบทั่วไป เช่น โฟลเดอร์ว่างหรือไฟล์ที่ไม่ใช่ภาพอย่างราบรื่น

### ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานบน .NET Core และ .NET Framework ด้วย)  
- ไลบรารี OCR ที่มีประเภท `OcrEngine`, `ImageStream`, และ `OcrResult` (เช่น SDK **FastOCR** สมมติที่ใช้ในโค้ดตัวอย่าง)  
- ความรู้พื้นฐาน C#—ไม่ต้องใช้แพทเทิร์นขั้นสูง

---

## วิธีทำ OCR แบบกลุ่มสำหรับไฟล์ PNG – ภาพรวม

ด้านล่างเป็น **โปรแกรมที่สมบูรณ์และสามารถรันได้**. คัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่, แทนที่เส้นทาง placeholder, แล้วกด **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **ผลลัพธ์ที่คาดหวัง:** สำหรับทุก `image01.png` คุณจะพบไฟล์ `image01.txt` ที่มีอักขระที่ถูกจดจำไว้ คอนโซลจะแสดงชื่อไฟล์แต่ละไฟล์ขณะเขียน

![วิธีทำ OCR แบบกลุ่ม diagram](how-to-batch-ocr-diagram.png "แผนภาพแสดงวิธีทำ OCR แบบกลุ่มสำหรับไฟล์ PNG ด้วย C#")

---

## คำอธิบายทีละขั้นตอน

### 1. เริ่มต้น OCR Engine – หัวใจของกระบวนการ  

บรรทัด `var ocrEngine = new OcrEngine();` สร้างอินสแตนซ์ของเอนจินหนึ่งตัวที่ใช้ซ้ำสำหรับทั้งชุด การใช้ซ้ำเอนจินเป็น **สิ่งสำคัญ** เพราะไลบรารี OCR ส่วนใหญ่จะจัดสรรทรัพยากรหนัก (เช่น โมเดลภาษา) ตอนสร้างอินสแตนซ์ การเริ่มต้นครั้งเดียวจึงทำให้ประสิทธิภาพดีขึ้นอย่างมาก—โดยเฉพาะเมื่อคุณมี PNG หลายสิบหรือหลายร้อยไฟล์

> **เคล็ดลับ:** หากต้องการภาษาอื่นนอกจากอังกฤษ ให้ตั้งค่า `ocrEngine.Config.Language = Language.Spanish;` (หรือ enum ที่รองรับอื่น)

### 2. อ่านภาพจากไดเรกทอรี – ค้นหา PNG ทุกไฟล์  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` ทำหน้าที่ตรงตามคีย์เวิร์ดรอง *read images from directory* มันคืนอาเรย์ของพาธแบบเต็มที่เราจะส่งต่อให้ OCR engine  

> **ทำไมไม่ใช้ `SearchOption.AllDirectories`?** หากภาพของคุณอยู่ในโฟลเดอร์ย่อย คุณสามารถสลับเป็น `GetFiles(path, "*.png", SearchOption.AllDirectories)` ได้ แต่ต้องจำไว้ว่า การสแกนลึกอาจนำไฟล์ที่ไม่ต้องการเข้ามา ดังนั้นควรกรองต่อ

### 3. แปลงพาธไฟล์เป็นอ็อบเจ็กต์ ImageStream  

OCR SDK ส่วนใหญ่คาดหวังสตรีมแทนพาธดิบ นิพจน์ LINQ `Select(path => ImageStream.FromFile(path)).ToList()` จะสร้าง **รายการสตรีม** ที่ตัวรับรู้แบบกลุ่มสามารถใช้ได้ในครั้งเดียว ขั้นตอนนี้ยังทำให้ไฟล์เปิดเพียงครั้งเดียว ลดภาระ I/O

> **กรณีขอบ:** หากไฟล์เสียหาย `ImageStream.FromFile` อาจโยนข้อยกเว้น ควรห่อการแปลงใน `try/catch` หากต้องการความทนทาน

### 4. จดจำข้อความในชุดทั้งหมด  

`ocrEngine.RecognizeBatch(imageStreams)` คือจุดที่เหมาะสมสำหรับ *how to batch OCR* แทนการวนลูปแต่ละภาพและเรียกเมธอดแบบภาพเดียว เราให้คอลเลกชันทั้งหมดแก่เอนจิน ภายในไลบรารีอาจทำงานแบบขนานให้คุณได้ความเร็วเพิ่มบนเครื่องหลายคอร์

> **เคล็ดลับ:** หาก OCR library ของคุณไม่มีเมธอด batch คุณยังคงได้ประสิทธิภาพคล้ายกันโดยใช้ `Parallel.ForEach` รอบเมธอด `Recognize` แบบภาพเดียว

### 5. เขียนผล OCR แต่ละไฟล์ – แปลง PNG เป็นข้อความ  

ลูป `for` สุดท้ายเขียน `ocrResults[i].Text` ลงไฟล์ `.txt` ที่ชื่อสอดคล้องกับ PNG ดั้งเดิม นี่คือสิ่งที่คีย์เวิร์ดรอง *convert PNG to text* อธิบายไว้ `Path.Combine` ทำให้แน่ใจว่าโฟลเดอร์ผลลัพธ์มีอยู่และป้องกันบั๊กการ traversal ของพาธ

> **ข้อผิดพลาดทั่วไป:** ลืมสร้างโฟลเดอร์ผลลัพธ์ก่อนจะทำให้เกิด `DirectoryNotFoundException` บรรทัด `Directory.CreateDirectory(outputFolder);` แก้ปัญหานี้ล่วงหน้า

---

## การจัดการกับความแปรผันในโลกจริง

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน | เหตุผล |
|-----------|-------------------|--------|
| **โฟลเดอร์อินพุตว่าง** | รักษาเงื่อนไข `if (imagePaths.Length == 0)` ตั้งแต่ต้น | ป้องกันการเรียก OCR ที่ไม่จำเป็นและแสดงข้อความเป็นมิตร |
| **ไฟล์หลายประเภท** | ใช้ `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | รับประกันว่าจะประมวลผลเฉพาะ PNG เท่านั้น ตรงกับ *extract text png* โดยไม่มีข้อผิดพลาด |
| **ภาพขนาดใหญ่ (> 5 MB)** | ลดขนาดก่อนส่งให้ OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (ถ้า API รองรับ) | ลดความกดดันของหน่วยความจำและมักทำให้ความแม่นยำดีขึ้น |
| **ภาษา OCR แตกต่าง** | ตั้งค่า `ocrEngine.Config.Language = Language.French;` | ทำให้เอนจินสอดคล้องกับภาษาของภาพต้นฉบับ |

---

## คำถามที่พบบ่อย (FAQ)

**ถาม: โค้ดนี้ทำงานกับไฟล์ JPEG หรือ TIFF ได้หรือไม่?**  
ตอบ: หลักการเดียวกัน—เปลี่ยน pattern การค้นหาเป็น `"*.jpg"` หรือ `"*.tif"` และตรวจสอบว่า OCR library รองรับฟอร์แมตเหล่านั้น

**ถาม: จะประมวลผลภาพหลายพันไฟล์โดยไม่ใช้หน่วยความจำหมดได้อย่างไร?**  
ตอบ: แทนที่การเรียก batch ด้วยวิธีสตรีม—ประมวลผลเป็นชิ้น ๆ เช่น 50 ภาพต่อครั้ง แล้วปล่อยสตรีมก่อนโหลดชิ้นต่อไป

**ถาม: ต้องการคะแนนความเชื่อมั่นของ OCR จะหาได้จากไหน?**  
ตอบ: `OcrResult` ส่วนใหญ่มี property `Confidence` คุณสามารถขยายขั้นตอนการเขียนได้ดังนี้:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## สรุป

เราได้ครอบคลุม **วิธีทำ OCR แบบกลุ่ม** สำหรับไฟล์ PNG ใน C# ตั้งแต่ต้นจนจบ โดยการเริ่มต้นเอนจินเดียว, อ่านภาพจากไดเรกทอรี, แปลงเป็นสตรีม, จดจำทั้งหมดใน batch, และสุดท้ายเขียนผลลัพธ์แต่ละไฟล์เป็นข้อความ ตอนนี้คุณมีแพทเทิร์นพร้อมผลิตภัณฑ์สำหรับงาน **extract text PNG**, **convert PNG to text**, และ **read images from directory**  

ต่อไปคุณอาจลองสลับผู้ให้บริการ OCR, เพิ่มการประมวลผลหลังจากหลายเธรด (เช่น การตรวจสอบการสะกด), หรือส่งไฟล์ `.txt` ไปยังดัชนีการค้นหา ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณเชี่ยวชาญ workflow แบบ batch  

มีเทคนิคหรือไอเดียอยากแชร์? แสดงความคิดเห็นได้เลย, และขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
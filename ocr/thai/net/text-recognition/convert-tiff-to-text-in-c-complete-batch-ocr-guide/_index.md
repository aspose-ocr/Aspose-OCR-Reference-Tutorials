---
category: general
date: 2026-05-25
description: แปลงไฟล์ TIFF เป็นข้อความโดยใช้ Aspose.OCR ใน C# เรียนรู้การแปลงภาพเป็นข้อความแบบชุดและสกัดข้อความจากไฟล์
  TIFF อย่างมีประสิทธิภาพ
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: th
og_description: แปลง TIFF เป็นข้อความด้วย Aspose.OCR คู่มือนี้แสดงการแปลงภาพเป็นข้อความเป็นชุดและวิธีดึงข้อความจากไฟล์
  TIFF ด้วยไม่กี่บรรทัดของ C#
og_title: แปลง TIFF เป็นข้อความใน C# – คู่มือ OCR แบบแบตช์ครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: แปลง TIFF เป็นข้อความใน C# – คู่มือ OCR แบบแบตช์ครบวงจร
url: /th/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง TIFF เป็นข้อความใน C# – คู่มือ OCR แบบแบตช์เต็มรูปแบบ

เคยต้อง **แปลง TIFF เป็นข้อความ** แต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจอปัญหา OCR แบบแบตช์เมื่อทำงานกับเอกสารสแกน ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันเชิงปฏิบัติที่ **ดึงข้อความจากไฟล์ TIFF** ด้วย Aspose.OCR และเราจะทำแบบขนานเพื่อให้โฟลเดอร์ขนาดใหญ่เสร็จในไม่กี่วินาที

เรายังจะพูดถึงแนวปฏิบัติที่ดีที่สุดของ **การแปลงรูปภาพเป็นข้อความแบบแบตช์** ด้วย ดังนั้นเมื่อจบคุณจะได้สคริปต์ที่ใช้ซ้ำได้ซึ่งเปลี่ยนไดเรกทอรีทั้งหมดของรูปสแกนเป็นไฟล์ *.txt* ที่เรียบร้อย—เหมาะสำหรับการทำดัชนี การค้นหา หรือการป้อนเข้าสู่การวิเคราะห์ต่อเนื่อง

## สิ่งที่คุณต้องเตรียม

- **.NET 6.0** หรือใหม่กว่า (โค้ดยังคอมไพล์บน .NET Framework ได้เช่นกัน)  
- **Aspose.OCR for .NET** NuGet package (`Install-Package Aspose.OCR`)  
- โฟลเดอร์ที่มีไฟล์ *.tif* หนึ่งไฟล์หรือมากกว่า (รูปแบบสแกน TIFF คลาสสิก)  
- IDE ที่คุณชอบ (Visual Studio, VS Code, Rider—อะไรก็ตามที่คุณถนัด)

แค่นั้นแหละ ไม่ต้องใช้บริการภายนอก ไม่ต้องมี API key เพียงแค่ C# แท้ ๆ กับ Aspose

![Screenshot of a TIFF file being processed and the resulting text file](/images/ocr-result.png "OCR result showing converted TIFF to text output")

*(ข้อความแทนภาพ: ภาพหน้าจอแสดงการแปลง TIFF เป็นข้อความบนหน้าจอ)*

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine – แปลง TIFF เป็นข้อความ

ก่อนอื่นเราต้องมีอินสแตนซ์ `OcrEngine` ที่รู้ว่าจะอ่านอักขระภาษาอังกฤษ เครื่องนี้คือหัวใจของการแปลง; การตั้งค่าให้ถูกต้องจะทำให้ได้ผลลัพธ์ที่เชื่อถือได้

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*ทำไมเรื่องนี้ถึงสำคัญ:*  
Aspose.OCR รองรับหลายสิบภาษา หากคุณต้องจัดการกับสแกนหลายภาษา เพียงเปลี่ยน `OcrLanguage.English` เป็นค่า enum ที่เหมาะสม การไม่กำหนดภาษาจะทำให้เครื่องเข้าสู่โหมดตรวจจับอัตโนมัติ ซึ่งอาจช้ากว่าและแม่นยำน้อยลง

## ขั้นตอนที่ 2: รวบรวมไฟล์ TIFF ทั้งหมด – ดึงข้อความจาก TIFF อย่างมีประสิทธิภาพ

ต่อไปเราจะดึงไฟล์ *.tif* ทุกไฟล์จากโฟลเดอร์ที่คุณระบุ การใช้ `Directory.GetFiles` จะให้แอเรย์ที่สะอาดซึ่งเราสามารถส่งต่อให้ตัวประมวลผลแบตช์ได้

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*เคล็ดลับมืออาชีพ:* ธง `SearchOption.AllDirectories` สามารถใช้ได้หากสแกนของคุณอยู่ในโฟลเดอร์ย่อย จำไว้ว่าการทำซ้ำลึกอาจเพิ่มการใช้หน่วยความจำในขั้นตอนแบตช์

## ขั้นตอนที่ 3: ทำ OCR แบบขนาน – การแปลงรูปภาพเป็นข้อความแบบแบตช์

ตอนนี้เป็นส่วนที่สนุก Aspose.OCR มีตัวช่วยแบบสแตติก `BatchOcr.RecognizeAll` ที่รับอาร์เรย์ของพาธไฟล์, engine, และคำแนะนำ `parallelism` เราจะเปิดใช้สี่เธรด ซึ่งบนแล็ปท็อปคอร์ดสี่คอร์สมัยใหม่ให้ความเร็วที่เกือบเชิงเส้น

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*ทำไมต้องใช้การทำงานขนาน?*  
การสแกนแบตช์ของ TIFF ความละเอียดสูงอาจใช้ CPU มาก การกระจายงานไปหลายเธรดทำให้ทุกคอร์ทำงานเต็มที่ ลดระยะเวลาการทำงานอย่างมาก หากคุณรันบนเซิร์ฟเวอร์ที่มีคอร์มากขึ้น ให้เพิ่มค่า `parallelism` ตามจำนวนคอร์

## ขั้นตอนที่ 4: เขียนผลลัพธ์ – แปลงรูปสแกนเป็นไฟล์ TXT

สุดท้ายเราจะวนลูปผ่านดิกชันนารีและเขียนข้อความแต่ละส่วนลงไฟล์ *.txt* ที่ใช้ชื่อฐานเดียวกับไฟล์ต้นฉบับ นี่คือจุดที่ **convert scanned images txt** กลายเป็นความจริง

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### สิ่งที่โค้ดทำ, อธิบายเป็นภาษาอังกฤษง่าย ๆ

1. **สร้าง** อินสแตนซ์ของ OCR engine ที่ตั้งค่าเป็นภาษาอังกฤษ.  
2. **รวบรวม** ไฟล์ TIFF ทุกไฟล์จากโฟลเดอร์เป้าหมาย.  
3. **เรียกใช้** `BatchOcr.RecognizeAll` ด้วยสี่เธรด, แปลงแต่ละภาพเป็นสตริง.  
4. **วนลูป** ผลลัพธ์, แทนที่นามสกุล `.tif` ด้วย `.txt` และเขียนสตริงลงดิสก์.

นี่คือเวิร์กโฟลว์ **convert TIFF to text** ทั้งหมดภายในไม่เกิน 50 บรรทัดของโค้ด

## จัดการกับกรณีขอบ – เมื่อสิ่งต่าง ๆ ไม่เป็นไปตามที่คาด

- **ไฟล์ TIFF ที่หายหรือเสีย** – `BatchOcr` จะโยน `OcrException` ให้ห่อการเรียกใน `try / catch` หากต้องการการทำงานแบบล่ม gracefully.  
- **เอกสารที่ไม่ใช่ภาษาอังกฤษ** – เปลี่ยน `OcrLanguage.English` เป็น `OcrLanguage.Spanish`, `OcrLanguage.French` เป็นต้น หรือใช้ `OcrLanguage.AutoDetect`.  
- **ภาพขนาดใหญ่มาก** – พิจารณาลด DPI ก่อน OCR (`ocrEngine.ImagePreprocessing.Dpi = 200`) เพื่อประหยัดหน่วยความจำ แม้อาจสูญเสียความแม่นยำบ้าง.  
- **การเข้ารหัสผลลัพธ์** – หากต้องการ code page เฉพาะ (เช่น Windows‑1252) ให้ส่งผ่านไปยัง `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`.

## เคล็ดลับมืออาชีพสำหรับการแปลงแบตช์ที่มั่นคง

- **บันทึกความล้มเหลว**: สร้าง `List<string> failedFiles` แล้วเพิ่มไฟล์ที่เกิดข้อผิดพลาด; เขียนรายการนี้ลงไฟล์ล็อกหลังลูป.  
- **ใช้ engine ซ้ำ**: อินสแตนซ์ `OcrEngine` เดียวกันสามารถใช้ซ้ำได้หลายไฟล์; อย่าสร้างใหม่ภายในลูป.  
- **ตรวจสอบผลลัพธ์**: การตรวจ `if (string.IsNullOrWhiteSpace(extractedText))` อย่างรวดเร็วสามารถระบุสแกนที่ว่างหรืออ่านไม่ออก.  
- **รวมกับ PDF**: หากแหล่งของคุณเป็น PDF หลายหน้า ให้แปลงแต่ละหน้าเป็น TIFF ก่อน (Aspose.PDF ทำได้) แล้วรันแบตช์นี้ต่อ.

## ขั้นตอนต่อไป – ไปไกลกว่าการแปลงแบบง่าย

เมื่อคุณสามารถ **ดึงข้อความจากไฟล์ TIFF** เป็นจำนวนมากได้แล้ว คุณอาจต้องการ:

- ป้อนไฟล์ *.txt* ไปยังดัชนีการค้นหา (Elasticsearch, Azure Cognitive Search).  
- รันการตรวจจับภาษาในแต่ละผลลัพธ์เพื่อส่งเอกสารไปยัง pipeline ตามภาษาที่เหมาะสม.  
- สร้าง PDF ที่ค้นหาได้โดยวางข้อความ OCR กลับบนภาพต้นฉบับ (ใช้ Aspose.PDF อีกครั้ง).  

ทุกสถานการณ์เหล่านี้อิงจากแนวคิดหลักเดียวกัน: **batch image to text conversion** เป็นบล็อกสร้างระบบประมวลผลเอกสารที่ใหญ่ขึ้น

---

### สรุป

คุณเพิ่งเรียนรู้วิธี **แปลง TIFF เป็นข้อความ** ด้วย Aspose.OCR, ประมวลผลโฟลเดอร์ทั้งหมดแบบขนาน, และบันทึกผลลัพธ์แต่ละไฟล์เป็น *.txt* ที่เรียบร้อย โซลูชันนี้เบา, ปรับแต่งได้เต็มที่, พร้อมใช้งานในโปรดักชัน—ไม่ว่าจะเป็นการดิจิไทซ์ใบแจ้งหนี้เก่า, การเก็บสำเนาสัญญาที่สแกน, หรือการขับเคลื่อนเครื่องมือค้นหาข้อความ  

ลองใช้ ปรับค่า parallelism ตามต้องการ แล้วเริ่มป้อนไฟล์ข้อความใหม่เหล่านี้เข้าสู่ workflow ที่คุณต้องการ Happy OCRing!

---


## บทแนะนำที่เกี่ยวข้อง

- [ดึงข้อความจากรูปภาพโดยใช้การทำ OCR บนโฟลเดอร์](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [ดึงข้อความจากรูปภาพ – การปรับแต่ง OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)
- [ดึงข้อความจากรูปภาพด้วย C# พร้อมการเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
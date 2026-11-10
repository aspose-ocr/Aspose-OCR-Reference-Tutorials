---
category: general
date: 2026-03-13
description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากการสแกน เรียนรู้การแปลง TIFF เป็นข้อความด้วย
  Aspose OCR, การเร่งความเร็วด้วย GPU, และโค้ดขั้นตอนต่อขั้นตอน
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: th
og_description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากการสแกน คู่มือนี้จะแสดงวิธีแปลงไฟล์
  TIFF เป็นข้อความด้วย Aspose OCR และการเร่งความเร็วด้วย GPU.
og_title: วิธีใช้ OCR ใน C# – ดึงข้อความจากการสแกนอย่างรวดเร็ว
tags:
- OCR
- C#
- Aspose
- Image Processing
title: วิธีใช้ OCR ใน C# – ดึงข้อความจากการสแกนอย่างรวดเร็ว
url: /th/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – ดึงข้อความจากการสแกนอย่างรวดเร็ว

เคยสงสัย **วิธีใช้ OCR** เพื่อดึงข้อความที่อ่านได้ออกจากกองไฟล์ TIFF ที่สแกนไว้หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—เช่น การแปลงใบแจ้งหนี้เป็นดิจิทัล, การเก็บถาวรเอกสารประวัติศาสตร์, หรือเพียงแค่ทำให้ PDF สามารถค้นหาได้—นักพัฒนาต้องการวิธีที่เชื่อถือได้ในการ **ดึงข้อความจากการสแกน** โดยไม่ต้องเหนื่อยใจ

ข่าวดีคืออะไร? ด้วย Aspose OCR และบรรทัดโค้ด C# เพียงไม่กี่บรรทัด คุณสามารถแปลง TIFF เป็นข้อความได้ในไม่กี่วินาที แม้บนเครื่องทำงานระดับปานกลาง ด้านล่างคุณจะได้ตัวอย่างที่พร้อมรันเต็มรูปแบบ พร้อมเหตุผลเบื้องหลังแต่ละการเลือก เพื่อให้คุณปรับใช้กับเวิร์กโฟลว์ของตนเองได้

## สิ่งที่คุณต้องการ

ก่อนที่เราจะลงลึก ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้พร้อมใช้งาน:

| ข้อกำหนด | ทำไมจึงสำคัญ |
|--------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | แพคเกจ NuGet ของ Aspose OCR รองรับ runtime .NET รุ่นใหม่ |
| Visual Studio 2022 (or any IDE you like) | ให้คุณใช้ IntelliSense และการดีบักที่ง่าย |
| A CUDA‑compatible GPU & driver (optional) | ทำให้ `ocrEngine.UseGpu = true` สามารถเพิ่มความเร็วอย่างเห็นได้ชัดสำหรับชุดข้อมูลขนาดใหญ่ |
| A folder of TIFF images you want to process | บทเรียนนี้ใช้ไฟล์ `*.tif` แต่คุณสามารถปรับรูปแบบได้ |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | ไลบรารีหลักที่ทำงานหนัก |

หากคุณขาดสิ่งใดสิ่งหนึ่งเหล่านี้ ให้ดาวน์โหลดและติดตั้งทันที—ไม่มีประโยชน์ที่จะอ่านต่อแล้วเจอการพึ่งพาที่หายไปในภายหลัง

## ภาพรวมของโซลูชัน

ในระดับสูง โปรแกรมทำสามอย่าง:

1. **สร้าง OCR engine** และเปิดการเร่งด้วย GPU ตามต้องการ  
2. **วนลูปผ่านไฟล์ TIFF ทุกไฟล์** ในไดเรกทอรี, ทำการจดจำ, และเก็บข้อความที่ได้เป็น plain‑text  
3. **เขียนข้อความ** ลงไฟล์ `.txt` ที่อยู่ข้างไฟล์ภาพต้นฉบับ  

เท่านี้เอง โค้ดถูกออกแบบให้สั้นที่สุดเท่าที่จะทำได้ แต่ยังแสดงแนวปฏิบัติที่ดีที่สุด เช่น การเลือกภาษาอย่างชัดเจน, การจัดการทรัพยากรอย่างเหมาะสม, และการจัดการข้อผิดพลาดสำหรับกรณีขอบที่พบบ่อย

![ตัวอย่างการใช้ OCR ใน C#](/images/how-to-use-ocr-csharp.png "ภาพประกอบการใช้ OCR ใน C# เพื่อดึงข้อความจากการสแกน")

## ขั้นตอนที่ 1: เริ่มต้น OCR Engine (วิธีใช้ OCR)

สิ่งแรกที่คุณต้องมีคืออินสแตนซ์ของ `OcrEngine` วัตถุนี้เป็นประตูสู่ฟังก์ชันทั้งหมดของ Aspose OCR โดยค่าเริ่มต้นทำงานบน CPU แต่การตั้งค่า `UseGpu = true` จะสั่งให้ไลบรารีย้ายการคำนวณเมทริกซ์หนักไปยังการ์ดกราฟิกของคุณ—หากคุณมีไดรเวอร์ที่รองรับ CUDA ติดตั้งอยู่

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**ทำไมเรื่องนี้สำคัญ:**  
- **การเร่งด้วย GPU** สามารถลดเวลาการประมวลผลได้ถึง 70 % สำหรับการสแกนความละเอียดสูง  
- **การเลือกภาษาอย่างชัดเจน** ช่วยหลีกเลี่ยงการเดาของเอนจินและเพิ่มความแม่นยำ โดยเฉพาะสำหรับสคริปต์ที่ไม่ใช่ละติน  

## ขั้นตอนที่ 2: ชี้ Engine ไปยังไฟล์สแกนของคุณ (แปลง TIFF เป็นข้อความ)

ต่อไปเราบอกโปรแกรมว่าจะมองหาไฟล์รูปภาพที่ไหน การใช้ `Directory.GetFiles` พร้อมฟิลเตอร์ `*.tif` ทำให้ตรรกะง่ายและหลีกเลี่ยงการดึงไฟล์ที่ไม่เกี่ยวข้องเช่น `.jpg` หรือ `.png`

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**หมายเหตุกรณีขอบ:** หากไดเรกทอรีว่าง ลูปด้านล่างจะไม่ทำงานเลย ซึ่งเป็นเรื่องปกติ คุณจะเห็นข้อความ “No files found” ที่เป็นมิตรในภายหลัง

## ขั้นตอนที่ 3: ประมวลผลไฟล์ TIFF แต่ละไฟล์ (ดึงข้อความจากการสแกน)

นี่คือหัวใจของโปรแกรม: โหลดแต่ละภาพ, รัน OCR, และบันทึกผลลัพธ์ `ImageStream.FromFile` ช่วยสตรีมไฟล์โดยตรงเข้าสู่หน่วยความจำ ซึ่งมีประสิทธิภาพมากกว่าการโหลดเป็น `Bitmap` ก่อน

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**ทำไมเราถึงห่อการทำงานแต่ละรอบด้วย `try/catch`:**  
การสแกนชุดเอกสารเป็นงานที่ยุ่งยาก; TIFF ที่เสียหายหรือการหยุดทำงานจากหน่วยความจำไม่ควรทำให้การทำงานทั้งหมดหยุดลง บล็อก `catch` จะบันทึกปัญหาและดำเนินต่อไป ทำให้ไพพ์ไลน์คงทน

### ผลลัพธ์ที่คาดหวัง

สำหรับแต่ละไฟล์ `example.tif` คุณจะพบไฟล์ `example.txt` ที่อยู่ข้างเคียงซึ่งอาจมีเนื้อหาเช่น:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

หาก OCR engine ไม่สามารถอ่านบรรทัดได้ จะปล่อยบรรทัดว่างหรืออักขระที่ผิดรูป—ไม่มีการขัดข้อง

## ขั้นตอนที่ 4: ทำความสะอาดและปล่อยทรัพยากร (แนวปฏิบัติที่ดีที่สุด)

`OcrEngine` implements `IDisposable` ดังนั้นจึงควรปล่อยทรัพยากรเนทีฟเมื่อเสร็จสิ้น ในแอปคอนโซลสั้น ๆ คุณอาจพึ่งพา GC ได้ แต่การทำลายอย่างชัดเจนเป็นนิสัยที่ควรฝึก

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถวางลงในโปรเจกต์ Console App ใหม่ได้ มันจะคอมไพล์ได้ทันที หากคุณได้เพิ่มแพคเกจ Aspose.OCR NuGet แล้ว

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### เช็คลิสต์ด่วน

- **GPU flag** – ลบหรือตั้งค่าเป็น `false` หากคุณไม่มีไดรเวอร์ CUDA  
- **Language** – เปลี่ยน `Language.English` เป็นภาษาอื่นที่รองรับ  
- **File pattern** – เปลี่ยน `"*.tif"` เป็น `"*.png"` หรือ `"*.*"` หากสแกนของคุณอยู่ในรูปแบบอื่น  

## ข้อผิดพลาดทั่วไป & เคล็ดลับมืออาชีพ (c# OCR tutorial)

| ข้อผิดพลาด | วิธีหลีกเลี่ยง |
|------------|----------------|
| **Out‑of‑memory errors** on huge batches | ประมวลผลไฟล์เป็นส่วนย่อย ๆ หรือเรียก `GC.Collect()` หลังจากทุก 50 ไฟล์ (ส่วนใหญ่ไม่จำเป็น) |
| **GPU not detected** but `UseGpu = true` | เอนจินจะกลับไปใช้ CPU อย่างเงียบ ๆ แต่คุณสามารถตรวจสอบ `ocrEngine.IsGpuAvailable` หลังจากสร้างได้ |
| **Wrong language pack** leads to garbled output | ควรตั้งค่า `ocrEngine.Language` อย่างชัดเจนเสมอ; ค่าเริ่มต้นอาจเป็น `Language.Unknown` |
| **File path contains Unicode characters** | ใช้ `Path.GetFullPath` เพื่อทำให้เป็นมาตรฐาน, หรือเพิ่มคำนำหน้า `@"\\?\"` บน Windows หากเส้นทางยาวเกิน |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
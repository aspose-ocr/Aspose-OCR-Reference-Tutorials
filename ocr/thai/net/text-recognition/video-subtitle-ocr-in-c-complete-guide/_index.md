---
category: general
date: 2026-06-03
description: บทเรียน OCR คำบรรยายวิดีโอที่แสดงวิธีการดึงเฟรมจากวิดีโอและอ่านข้อความจากไฟล์วิดีโอเช่น
  MP4 ด้วย Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: th
og_description: เรียนรู้การทำ OCR คำบรรยายวิดีโอด้วย Aspose.OCR ดึงเฟรมจากวิดีโอ อ่านข้อความจากวิดีโอ
  และดึงข้อความจากไฟล์ MP4 ภายในไม่กี่นาที.
og_title: OCR คำบรรยายวิดีโอใน C# – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: การทำ OCR คำบรรยายวิดีโอใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR คำบรรยายวิดีโอใน C# – คู่มือฉบับสมบูรณ์

เคยต้องการ **video subtitle ocr** แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว ไม่ว่าคุณจะกำลังแปลงบันทึกการบรรยายเป็นดิจิทัล, ดึงคำบรรยายจากวิดีโอการฝึกอบรม, หรือแค่สนใจการอ่านข้อความจากวิดีโอ, บทเรียนนี้จะแสดงให้คุณเห็นขั้นตอนการทำด้วย C# และ Aspose.OCR อย่างชัดเจน  

ในไม่กี่นาทีต่อไปเราจะดึงเฟรมจากวิดีโอ, รัน OCR บนเฟรมนั้น, และสุดท้ายแสดงข้อความคำบรรยายเฟรมต่อเฟรม. เมื่อจบคุณจะสามารถ **read text from video** ไฟล์—including MP4—โดยไม่ต้องค้นหาเครื่องมือของบุคคลที่สาม.

## สิ่งที่คุณจะสร้าง

เราจะสร้างแอปคอนโซลเล็ก ๆ ที่:

1. ถอดรหัส MP4 (หรือฟอร์แมตที่รองรับอื่น) เป็นเฟรม `Bitmap` แยกแต่ละอัน.  
2. จำกัดพื้นที่ OCR ไว้ที่แถบคำบรรยายเพื่อไม่ให้เอนจินเสียสมาธิจากภาพทั้งหมด.  
3. ประมวลผลแต่ละเฟรมด้วย `VideoOcrProcessor` ของ Aspose.  
4. พิมพ์ข้อความคำบรรยายที่ได้รับการจดจำลงคอนโซล.

ไม่มีส่วนเกิน, เพียงตัวอย่างทำงานจากต้นจนจบที่คุณสามารถนำไปใช้ในโปรเจกต์จริงได้.

## ข้อกำหนดเบื้องต้น

- **.NET 6.0** หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – ติดตั้งผ่าน NuGet: `Install-Package Aspose.OCR`.  
- ไฟล์วิดีโอ (MP4 ทำงานได้ดี).  
- วิธีถอดรหัสเฟรมวิดีโอ – ตัวอย่างใช้เมธอด placeholder, แต่คุณสามารถต่อเข้ากับ FFmpeg, OpenCV, หรือไลบรารีใดก็ได้ที่คืนค่าเป็นอ็อบเจกต์ `Bitmap`.  

> Pro tip: หากคุณใช้ Windows, แพ็กเกจ `System.Drawing.Common` ทำงานได้ดีสำหรับ `Bitmap`. บน Linux/macOS คุณจะต้องติดตั้ง dependency `libgdiplus` ที่เป็น native.

## ขั้นตอนที่ 1 – ดึงเฟรมจากวิดีโอ

อุปสรรคแรกคือการแปลงภาพเคลื่อนไหวให้เป็นภาพนิ่ง. เมธอด `GetVideoFrames` ด้านล่างถูกเว้นไว้ให้คุณเติมด้วยตัวถอดรหัสที่ชื่นชอบ. ตัวอย่างสเก็ตช์สั้น ๆ ด้วย FFmpeg‑Core (เพื่อแสดงโครงสร้างข้อมูล):

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การดึงเฟรมทำให้ OCR engine มีภาพคงที่ทำงานด้วย, ซึ่งช่วยเพิ่มความแม่นยำอย่างมากเมื่อเทียบกับการพยายามอ่านโดยตรงจากสตรีมวิดีโอ.

## ขั้นตอนที่ 2 – ตั้งค่า VideoOcrProcessor

เมื่อเรามีลำดับของอ็อบเจกต์ `Bitmap` แล้ว เราสามารถส่งให้ Aspose.OCR ได้. `VideoOcrProcessor` ให้เรากำหนด **Region of Interest (ROI)** – เหมาะสำหรับคำบรรยายที่มักอยู่ด้านบนหรือด้านล่างของเฟรม.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **ทำไมต้องจำกัด ROI?** การละเลยส่วนที่เหลือของภาพช่วยลดสัญญาณรบกวน, ลดเวลาประมวลผล, และหลีกเลี่ยงผลบวกเท็จจากกราฟิกพื้นหลัง.

## ขั้นตอนที่ 3 – รัน OCR บนลำดับเฟรม

เมื่อโปรเซสเซอร์พร้อม, การป้อนเฟรมทำได้ด้วยบรรทัดเดียว. เมธอด `Process` จะคืนค่า enumerable ของอ็อบเจกต์ `OcrResult`, แต่ละอันมีข้อความที่จดจำได้สำหรับเฟรมนั้น.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **เกิดอะไรขึ้นเบื้องหลัง?** Aspose.OCR จะทำการ normalize แต่ละ bitmap, รัน recognizer ที่ใช้ neural‑network, แล้วทำ post‑process ผลลัพธ์เพื่อปรับปรุงเครื่องหมายวรรคตอนและการแบ่งบรรทัด.

## ขั้นตอนที่ 4 – แสดงข้อความที่สกัดออกมา

สุดท้าย เราจะวนลูปผลลัพธ์และพิมพ์แต่ละบรรทัดคำบรรยาย. คุณอาจบันทึกเป็นไฟล์ SRT, ฐานข้อมูล, หรือส่งต่อให้บริการแปลภาษาได้เช่นกัน.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### ตัวอย่างทำงานเต็มรูปแบบ

นำทุกส่วนมารวมกันจะได้โปรแกรมคอนโซลที่ทำงานได้อย่างอิสระ:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

หาก OCR มีปัญหากับเฟรมใดเฟรมหนึ่ง คุณจะเห็นสตริงว่าง – นั่นเป็นสัญญาณให้คุณปรับ ROI หรือเพิ่มอัตราการดึงเฟรม.

## ปัญหาที่พบบ่อย & วิธีแก้

| ปัญหา | ทำไมจึงเกิด | วิธีแก้ |
|-------|-------------|--------|
| **อักขระแปลก** | เฟรมความละเอียดต่ำหรือบีบอัดหนัก | ดึงเฟรมที่บิตเรตสูงขึ้น, หรือ upscale bitmap ก่อน OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **ไม่มีข้อความคืนค่า** | ROI ไม่ครอบแถบคำบรรยายจริง | ตรวจสอบพิกัดสี่เหลี่ยม (ใช้เครื่องมือ screenshot วัด). |
| **คอขวดประสิทธิภาพ** | ประมวลผลทุกเฟรมที่ 30 fps มากเกินไป | ลดอัตราเป็น 1‑2 fps สำหรับส่วนใหญ่ของสตรีมคำบรรยาย; ยังคงจับการเปลี่ยนแปลงคำบรรยายได้. |
| **ไม่พบ FFmpeg** | `ffmpeg.exe` ไม่อยู่ใน `PATH` | ระบุพาธเต็มใน `ProcessStartInfo.FileName` หรือทำการติดตั้ง FFmpeg อย่างทั่วโลก. |

## การขยายโซลูชัน

- **ส่งออกเป็น SRT** – รวม timestamps กับข้อความ OCR แล้วเขียนไฟล์ SubRip.  
- **รองรับหลายภาษา** – ตั้งค่า `ocrProcessor.Language = OcrLanguage.Spanish` (หรือภาษาอื่นที่รองรับ).  
- **ประมวลผลแบบเรียลไทม์** – ส่งเฟรมโดยตรงจากสตรีมสดแทนการอ่านจากดิสก์.  

ทั้งหมดนี้ยังคงอิงกับแนวคิดหลักของ **extract frames from video**, **read text from video**, และ **extract text from mp4**.

## สรุป

เราได้เดินผ่านเวิร์กโฟลว์ **video subtitle ocr** อย่างครบถ้วนใน C#. ด้วยการดึงเฟรมจากวิดีโอ, โฟกัส OCR ไปที่แถบคำบรรยาย, และวนลูปผลลัพธ์, คุณสามารถ **read text from video** ไฟล์เช่น MP4 ได้อย่างเชื่อถือได้. โค้ดพร้อมคัดลอก‑วาง, และการออกแบบแบบโมดูลาร์ทำให้คุณเปลี่ยนตัวถอดรหัสเฟรมตามที่ต้องการได้ง่าย.

ขั้นตอนต่อไป? ลองส่งออกผลลัพธ์เป็นไฟล์ SRT, ทดลองขนาด ROI ต่าง ๆ, หรือส่งคำบรรยายไปยัง API แปลภาษาเพื่อสร้างคำบรรยายหลายภาษา. ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณครอบคลุมพื้นฐานการสกัดข้อความจากวิดีโอแล้ว.

ขอให้สนุกกับการเขียนโค้ด, และขอให้คำบรรยายของคุณชัดเจนเสมอ!

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณเอง.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
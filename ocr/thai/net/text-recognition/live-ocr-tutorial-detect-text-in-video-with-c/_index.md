---
category: general
date: 2026-03-13
description: บทเรียน OCR สดแสดงวิธีตั้งค่าภาษา OCR และตรวจจับข้อความจากสตรีมวิดีโอแบบเรียลไทม์โดยใช้
  Aspose.OCR. ปฏิบัติตามคำแนะนำทีละขั้นตอน.
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: th
og_description: บทเรียน OCR สดอธิบายวิธีตั้งค่าภาษา OCR และตรวจจับข้อความจากสตรีมวิดีโอโดยใช้
  Aspose.OCR Live ใน C# พร้อมโค้ดเต็มรวมไว้ด้วย
og_title: 'สอน OCR สด: การตรวจจับข้อความแบบเรียลไทม์ในวิดีโอ'
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 'การสอน OCR สด: ตรวจจับข้อความในวิดีโอด้วย C#'
url: /th/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

language** but original bullet had **set OCR language**. Good.

Now produce final content with all translations and placeholders.

Let's construct final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# บทแนะนำ Live OCR: ตรวจจับข้อความในวิดีโอด้วย C#

เคยต้องการ **live OCR tutorial** ที่ทำงานได้จริงบนวิดีโอฟีดหรือไม่? บางทีคุณอาจกำลังสร้างแอปกล้องอัจฉริยะหรือโอเวอร์เลย์การแปลแบบเรียลไทม์และติดอยู่ที่ “จะดึงข้อความจากแต่ละเฟรมอย่างไร?” ข่าวดีคือคุณไม่ต้องสร้างใหม่จากศูนย์ ในคู่มือนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่ง **sets OCR language**, ดึงเฟรมจากกล้อง, และ **detects text video** สตรีมแบบเรียลไทม์

เราจะใช้คลาส `LiveOcr` ของ Aspose.OCR ซึ่งออกแบบมาสำหรับสถานการณ์ที่ต้องการความหน่วงต่ำ เมื่ออ่านจบบทความนี้คุณจะมีแอปคอนโซลที่พิมพ์ข้อความแรกที่พบแล้วออกจากโปรแกรม—เหมาะเป็นจุดเริ่มต้นสำหรับ pipeline ที่ซับซ้อนยิ่งขึ้น

## ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK (หรือเวอร์ชัน .NET ล่าสุดใดก็ได้)  
- Visual Studio 2022 หรือ VS Code (IDE ที่คุณชอบ)  
- NuGet package `Aspose.OCR` (ติดตั้งโดยใช้ `dotnet add package Aspose.OCR`)  
- เว็บแคมหรือแหล่งวิดีโอใดก็ได้ที่สามารถให้เฟรม `Bitmap`  

ไม่ต้องการไลบรารีเนทีฟเพิ่มเติม; Aspose.OCR มาพร้อมกับทุกอย่างที่คุณต้องการ.

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR และเพิ่ม Namespaces

ก่อนเขียนโค้ดใด ๆ ให้แน่ใจว่าได้อ้างอิงไลบรารี Aspose OCR แล้ว เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรัน:

```bash
dotnet add package Aspose.OCR
```

จากนั้น ที่ส่วนบนของไฟล์ `Program.cs` ให้เพิ่มการนำเข้า namespaces ที่เราจะใช้:

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **เคล็ดลับ:** หากคุณใช้ Visual Studio, IDE จะเสนอคำสั่ง `using` ให้โดยอัตโนมัติหลังจากคุณพิมพ์ชื่อคลาส.

## ขั้นตอนที่ 2: สร้างและกำหนดค่า LiveOcr Instance

หัวใจของบทแนะนำคืออ็อบเจ็กต์ `LiveOcr` เราต้องบอกให้มันรู้ว่าต้องมองหาภาษาใดและอาจใช้ฟิลเตอร์การเตรียมข้อมูลล่วงหน้า (เช่น deskewing) เพื่อเพิ่มความแม่นยำ.

```csharp
// Step 2: Initialize LiveOcr with English language and a deskew filter
LiveOcr liveOcr = new LiveOcr
{
    // This is where we **set OCR language** to English.
    Language = Language.English,

    // Pre‑processing helps when the camera isn’t perfectly aligned.
    PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
};
```

ทำไมต้องตั้งค่าภาษา? เครื่องมือ OCR ใช้พจนานุกรมและโมเดลอักขระที่เฉพาะเจาะจงตามภาษา; การระบุ English จะลดผลบวกเท็จและเพิ่มความเร็วในการจดจำ หากต้องการภาษาอื่น เพียงเปลี่ยน `Language.English` เป็น `Language.Spanish`, `Language.French` เป็นต้น

## ขั้นตอนที่ 3: ดึงเฟรมจากกล้องของคุณ

ในโครงการจริงคุณจะต้องแทนที่เมธอด placeholder `CaptureFrameFromCamera()` ด้วยตรรกะการจับภาพจริง—อาจใช้ `AForge.Video`, `OpenCvSharp` หรือ Windows Media Capture API เพื่อความสะดวกในบทแนะนำนี้เราจะเก็บเมธอดเป็นแบบนามธรรม แต่จะแสดงตัวอย่างสั้น ๆ ด้วย `AForge`.

```csharp
// Simple wrapper that returns a Bitmap from the default webcam.
// You can replace this with any library that gives you a Bitmap.
static Bitmap CaptureFrameFromCamera()
{
    // NOTE: This is a minimal example. In production you should
    // manage the video source lifecycle and dispose objects properly.
    var videoSource = new AForge.Video.DirectShow.VideoCaptureDevice(
        new AForge.Video.DirectShow.FilterInfoCollection(
            AForge.Video.DirectShow.FilterCategory.VideoInputDevice)[0].MonikerString);

    Bitmap frame = null;
    var waitHandle = new AutoResetEvent(false);

    videoSource.NewFrame += (sender, eventArgs) =>
    {
        frame = (Bitmap)eventArgs.Frame.Clone();
        waitHandle.Set(); // signal that we have a frame
    };

    videoSource.Start();
    waitHandle.WaitOne(1000); // wait up to 1 second for a frame
    videoSource.SignalToStop();
    videoSource.WaitForStop();

    return frame;
}
```

> **กรณีขอบ:** หากกล้องไม่พร้อมใช้งาน `CaptureFrameFromCamera` จะคืนค่า `null`. ควรตรวจสอบเสมอในโค้ดการผลิต

## ขั้นตอนที่ 4: ประมวลผลแต่ละเฟรมจนกว่าจะพบข้อความ

ตอนนี้เราจะวนลูปจำนวนเฟรมที่กำหนด (หรือไม่จำกัด) และส่งแต่ละ bitmap ไปยัง `LiveOcr.ProcessFrame` ทันทีที่ได้สตริงที่ไม่ว่างเปล่า เราจะพิมพ์และออกจากลูป.

```csharp
// Step 4: Scan up to 100 frames or until text appears
for (int frameIndex = 0; frameIndex < 100; frameIndex++)
{
    Bitmap cameraFrame = CaptureFrameFromCamera();

    // Guard against a failed capture
    if (cameraFrame == null)
    {
        Console.WriteLine("Failed to capture a frame. Retrying...");
        Thread.Sleep(100);
        continue;
    }

    // Run OCR on the current frame
    string recognizedText = liveOcr.ProcessFrame(cameraFrame);

    // If we detected something, show it and stop
    if (!string.IsNullOrEmpty(recognizedText))
    {
        Console.WriteLine($"Detected text: {recognizedText}");
        break;
    }

    // Small pause to avoid hammering the CPU
    Thread.Sleep(30);
}
```

### ทำไมต้องหยุดชั่วคราว?

`Thread.Sleep(30)` ให้ไดรเวอร์กล้องได้พักและลดการใช้ CPU ในสถานการณ์ประสิทธิภาพสูงคุณอาจแทนที่ด้วยตัวควบคุมอัตราเฟรมที่ซับซ้อนกว่า

## ขั้นตอนที่ 5: รวมทุกอย่างในแอปคอนโซล

รวมทั้งหมดเข้าด้วยกัน นี่คือโปรแกรมที่พร้อมคัดลอกและวางทั้งหมด บันทึกเป็น `Program.cs` ภายในโปรเจกต์คอนโซลใหม่ (`dotnet new console`) แล้วรัน `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System;
using System.Drawing;
using System.Threading;

// Optional: using AForge for demo capture (install AForge.Video via NuGet)
// using AForge.Video.DirectShow;

class Program
{
    static void Main()
    {
        // Initialize LiveOcr – **set OCR language** to English
        LiveOcr liveOcr = new LiveOcr
        {
            Language = Language.English,
            PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
        };

        Console.WriteLine("Starting live OCR… Press Ctrl+C to abort.");

        // Loop through frames – **detect text video** in real time
        for (int i = 0; i < 100; i++)
        {
            Bitmap frame = CaptureFrameFromCamera();

            if (frame == null)
            {
                Console.WriteLine("No frame captured, retrying...");
                Thread.Sleep(100);
                continue;
            }

            string text = liveOcr.ProcessFrame(frame);

            if (!string.IsNullOrEmpty(text))
            {
                Console.WriteLine($"Detected text: {text}");
                break; // stop after first successful detection
            }

            Thread.Sleep(30); // throttle loop
        }

        Console.WriteLine("Live OCR session ended.");
    }

    // -----------------------------------------------------------------
    // Replace this stub with your own capture logic.
    // -----------------------------------------------------------------
    static Bitmap CaptureFrameFromCamera()
    {
        // Placeholder implementation – returns a solid‑color bitmap.
        // In a real app you would pull frames from a webcam or video file.
        Bitmap dummy = new Bitmap(640, 480);
        using (Graphics g = Graphics.FromImage(dummy))
        {
            g.Clear(Color.Black);
            g.DrawString(DateTime.Now.ToString("hh:mm:ss"), 
                new Font("Arial", 24), Brushes.White, new PointF(10, 10));
        }
        return dummy;
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อกล้องเห็นข้อความภาษาอังกฤษที่อ่านได้ (เช่น ป้ายพิมพ์) คุณจะเห็นอย่างนี้:

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

หากไม่มีอะไรอยู่ในมุมมอง ลูปจะจบหลังจาก 100 ครั้งและพิมพ์ “Live OCR session ended.” คุณสามารถเพิ่มจำนวนรอบหรือแทนที่ลูป `for` ด้วย `while (true)` เพื่อการตรวจสอบไม่สิ้นสุด

## คำถามทั่วไป & ปัญหาที่พบบ่อย

| Question | Answer |
|----------|--------|
| **ฉันสามารถประมวลผลหลายภาษาได้พร้อมกันหรือไม่?** | ได้. ตั้งค่า `Language = Language.English | Language.Spanish;` (bitwise OR) เพื่อเปิดใช้งานพจนานุกรมหลายภาษา. |
| **ถ้าเฟรมของฉันใหญ่และ OCR ช้าเป็นอย่างไร?** | ลดขนาด bitmap ก่อนเรียก `ProcessFrame`. ตัวอย่าง: `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **ฉันต้องการไลเซนส์สำหรับ Aspose.OCR หรือไม่?** | ไลเซนส์ทดลองชั่วคราวใช้งานได้สูงสุด 30 วัน สำหรับการผลิตควรซื้อไลเซนส์เพื่อเอาวอเตอร์มาร์คออก. |
| **ฉันจะจัดการกับข้อความที่หมุนได้อย่างไร?** | `DeskewFilter` แก้ไขการหมุนเล็กน้อยแล้ว. หากมุมหมุนมาก ให้เพิ่ม `RotateFilter` เข้าไปใน pipeline. |
| **วิธีนี้ปลอดภัยต่อการทำงานหลายเธรดหรือไม่?** | อินสแตนซ์ `LiveOcr` ไม่ปลอดภัยต่อหลายเธรด. สร้างหนึ่งอินสแตนซ์ต่อเธรดหรือป้องกันการเข้าถึงด้วย lock. |

## การต่อยอดบทแนะนำ

เมื่อคุณมีพื้นฐาน **live OCR tutorial** แล้ว ลองพิจารณาขั้นตอนต่อไปนี้:

1. **Stream to a UI** – แสดงวิดีโอสดพร้อมผลลัพธ์ OCR ที่ซ้อนทับโดยใช้ `Windows Forms` หรือ `WPF`.  
2. **Batch processing** – ส่งเฟรมเข้าแคชและรัน OCR บนพูล worker เบื้องหลังเพื่อเพิ่มอัตราการประมวลผล.  
3. **Language detection** – ผสานรวมไลบรารีการตรวจจับภาษาเพื่อสลับ `LiveOcr.Language` แบบเรียลไทม์.  
4. **Persist results** – เขียนสตริงที่ตรวจพบลงในฐานข้อมูลหรือไฟล์ CSV เพื่อการวิเคราะห์.  

แต่ละการต่อยอดนี้ยังคงอิงกับแนวคิดหลักที่เราได้กล่าวถึง: การเริ่มต้น `LiveOcr`, **setting OCR language**, และ **detecting text video** เฟรมแบบเรียลไทม์.

### สรุปย่อ

- ติดตั้ง Aspose.OCR ผ่าน NuGet.  
- สร้างอ็อบเจ็กต์ `LiveOcr`, **set OCR language** (English ในตัวอย่าง).  
- ดึงเฟรม `Bitmap` จากกล้อง.  
- วนลูปผ่านเฟรม, เรียก `ProcessFrame`, และหยุดเมื่อพบข้อความ.  
- โปรแกรมเต็มที่แสดงด้านบนพร้อมรันและเป็นฐานที่มั่นคงสำหรับโครงการตรวจจับข้อความแบบเรียลไทม์ใด ๆ.

ลองทำดู ปรับแต่ง pipeline การเตรียมข้อมูลล่วงหน้า แล้วดูแอปของคุณเริ่มอ่านโลกทีละเฟรม ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
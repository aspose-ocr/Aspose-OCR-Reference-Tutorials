---
category: general
date: 2026-03-05
description: วิธีทำ OCR อย่างรวดเร็วด้วย Aspose.OCR และจดจำข้อความจากสตรีมในไม่กี่ขั้นตอนง่าย
  ๆ เรียนรู้โค้ด C# เต็มรูปแบบและเคล็ดลับสำหรับการสตรีมข้อมูลภาพ
draft: false
keywords:
- how to get OCR
- recognize text from stream
- Aspose OCR
- streaming OCR C#
- image chunk processing
language: th
og_description: วิธีใช้ OCR ใน C# และจดจำข้อความจากสตรีมด้วย Aspose.OCR ติดตามบทแนะนำขั้นตอนต่อขั้นตอนเพื่อรับโซลูชันที่พร้อมใช้งาน.
og_title: วิธีใช้ OCR ใน C# – คู่มือการจดจำสตรีมอย่างครบถ้วน
tags:
- OCR
- C#
- Aspose
title: วิธีทำ OCR ใน C# – แยกข้อความจากสตรีม
url: /th/net/text-recognition/how-to-get-ocr-in-c-recognize-text-from-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – จดจำข้อความจากสตรีม

เคยสงสัยไหมว่า **วิธีทำให้ OCR** ทำงานในแอป .NET โดยไม่ต้องบันทึกรูปภาพทั้งหมดลงดิสก์ก่อน? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนต้องการ **จดจำข้อความจากสตรีม** — เช่นเมื่อประมวลผลภาพที่มาจากเครือข่าย, ฟีดกล้อง, หรือ API ของคลาวด์สตอเรจ  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และพร้อมรันที่แสดงให้เห็นอย่างชัดเจน เมื่อเสร็จคุณจะมีโปรแกรม C# ที่ทำงานอิสระซึ่งสร้าง Aspose OCR engine, ส่งชิ้นส่วนภาพเข้าไปเป็นสตรีม, และพิมพ์ข้อความที่สกัดออกมาที่คอนโซล ไม่ต้องใช้เครื่องมือภายนอกที่ลึกลับ เพียงโค้ดที่ชัดเจนและเคล็ดลับที่ใช้งานได้จริงไม่กี่ข้อ

## สิ่งที่คุณจะได้เรียนรู้

- วิธีติดตั้งและเปิดใช้งานไลบรารี Aspose.OCR
- วิธีป้อนข้อมูลภาพเป็นชิ้นส่วนโดยใช้เมธอด `AppendChunk`
- วิธีเริ่มและจบรอบการจดจำ (`BeginRecognize` / `EndRecognize`)
- วิธีจัดการกับกรณีขอบทั่วไป เช่น ชิ้นส่วนไม่สมบูรณ์หรือข้อผิดพลาดของไลเซนส์
- รูปแบบของผลลัพธ์และวิธีตรวจสอบ

### ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Core และ .NET Framework ด้วย)
- ไฟล์ไลเซนส์ Aspose OCR ที่ถูกต้อง (`Aspose.OCR.lic`) คุณสามารถรับเวอร์ชันทดลองฟรีจากเว็บไซต์ Aspose
- ความคุ้นเคยพื้นฐานกับ C# และ `async`/`await` หากต้องการอ่านจากสตรีมแบบอะซิงโครนัส (ตัวอย่างใช้สตับแบบซิงโครนัสเพื่อความชัดเจน)

> **ทำไมเรื่องนี้สำคัญ:** การทำ OCR แบบสตรีมช่วยให้คุณใช้หน่วยความจำน้อยลงและลดความหน่วงเวลาขณะจัดการกับภาพขนาดใหญ่หรือฟีดวิดีโอต่อเนื่อง นี่เป็นรูปแบบที่คุณจะพบในเครื่องสแกนเอกสารแบบเรียลไทม์, แอปมือถือ, และไพป์ไลน์การประมวลผลฝั่งเซิร์ฟเวอร์

## ขั้นตอน 1: ตั้งค่าโปรเจกต์และเพิ่ม Aspose.OCR

เริ่มต้นด้วยการสร้างโปรเจกต์คอนโซลใหม่และดึงแพ็กเกจ Aspose.OCR จาก NuGet

```bash
dotnet new console -n StreamOcrDemo
cd StreamOcrDemo
dotnet add package Aspose.OCR
```

> **เคล็ดลับ:** หากคุณใช้ Visual Studio ให้คลิกขวาที่โปรเจกต์ → *Manage NuGet Packages* → ค้นหา “Aspose.OCR” แล้วติดตั้งเวอร์ชันเสถียรล่าสุด

จากนั้นเพิ่มไฟล์ไลเซนส์ลงในโฟลเดอร์รากของโปรเจกต์และตั้งค่าคุณสมบัติ **Copy to Output Directory** เป็น **Copy always** เพื่อให้ไฟล์พร้อมใช้งานขณะรัน

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอน 2: เริ่มต้น OCR Engine และใช้ไลเซนส์

การสร้าง engine ทำได้ง่าย แต่การใช้ไลเซนส์ **ต้องทำก่อน** เรียกเมธอดจดจำใด ๆ ไม่เช่นนั้นคุณจะเจอข้อจำกัดของโหมดทดลอง

```csharp
static OcrEngine InitializeOcrEngine()
{
    var engine = new OcrEngine();

    // Load the license – adjust the path if your file lives elsewhere
    string licensePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Aspose.OCR.lic");
    if (!File.Exists(licensePath))
    {
        Console.Error.WriteLine("License file not found at " + licensePath);
        Environment.Exit(1);
    }

    engine.SetLicense(licensePath);
    return engine;
}
```

> **เหตุผลที่ทำเช่นนี้:** การตั้งค่าไลเซนส์ตั้งแต่ต้นทำให้การเรียก API ทั้งหมดทำงานในโหมดเต็มฟีเจอร์ หลีกเลี่ยงลายน้ำ “evaluation version”

## ขั้นตอน 3: จำลองแหล่งข้อมูลสตรีม

ในแอปจริงคุณอาจอ่านจาก `NetworkStream`, `FileStream` หรือ SDK ของกล้อง สำหรับการสาธิตนี้เราจะจำลองสตรีมด้วยฟังก์ชันช่วยที่คืนอาร์เรย์ไบต์ซึ่งเป็นชิ้นส่วน JPEG

```csharp
static byte[] GetNextChunk()
{
    // Replace this with your actual streaming logic.
    // Here we simply read the whole file and pretend it’s a single chunk.
    string sampleImagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
    if (!File.Exists(sampleImagePath))
    {
        Console.Error.WriteLine("Sample image not found at " + sampleImagePath);
        Environment.Exit(1);
    }

    return File.ReadAllBytes(sampleImagePath);
}
```

> **หมายเหตุกรณีขอบ:** หากคุณได้รับชิ้นส่วนขนาดเล็กหลาย ๆ ชิ้น คุณสามารถเรียก `engine.Image.AppendChunk(chunk)` ซ้ำได้หลายครั้งก่อนจบการจดจำ Engine จะบัฟเฟอร์ภายในจนมีข้อมูลพอที่จะเริ่มประมวลผล

## ขั้นตอน 4: ป้อนข้อมูลภาพเป็นชิ้นส่วนและรัน OCR

ต่อไปเราจะรวมทุกอย่างเข้าด้วยกัน ลำดับการทำงานคือ:

1. `BeginRecognize()` – แจ้ง engine ว่าคุณกำลังจะป้อนข้อมูล
2. `AppendChunk()` – เพิ่มอาร์เรย์ไบต์แต่ละอัน (คุณอาจวนลูปผ่านหลายชิ้นส่วน)
3. `EndRecognize()` – บอกว่าได้ส่งชิ้นส่วนสุดท้ายแล้วและเริ่มการจดจำจริง

```csharp
static string PerformOcr(OcrEngine engine, byte[] imageChunk)
{
    // Start the recognition session
    engine.BeginRecognize();

    // Feed the image data. If you have multiple chunks, call this in a loop.
    engine.Image.AppendChunk(imageChunk);

    // End the session – the engine now processes the accumulated data.
    engine.EndRecognize();

    // Retrieve the result object; .Text holds the plain string.
    return engine.GetResult().Text;
}
```

## ขั้นตอน 5: รวมทั้งหมดใน `Main`

นี่คือตัวอย่างเมธอด `Main` เต็มรูปแบบที่เชื่อมต่อทุกอย่าง, พิมพ์ข้อความที่จดจำได้, และทำการ Dispose engine อย่างถูกต้อง

```csharp
static void Main(string[] args)
{
    // 1️⃣ Initialize OCR engine with license
    var ocrEngine = InitializeOcrEngine();

    try
    {
        // 2️⃣ Get a chunk of image data (replace with your streaming source)
        byte[] imageChunk = GetNextChunk();

        // 3️⃣ Run OCR on the streamed data
        string recognizedText = PerformOcr(ocrEngine, imageChunk);

        // 4️⃣ Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
    catch (Exception ex)
    {
        // Helpful error handling – you’ll often see OCR exceptions when the image is corrupted.
        Console.Error.WriteLine("OCR failed: " + ex.Message);
    }
    finally
    {
        // Release any native resources held by the engine.
        ocrEngine.Dispose();
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หาก `sample.jpg` มีข้อความ “Hello, World!” คุณควรเห็น:

```
=== Recognized Text ===
Hello, World!
```

หากภาพเบลอหรือชิ้นส่วนไม่สมบูรณ์ ผลลัพธ์อาจว่างเปล่าหรือมีอักขระผิดรูป – นี่คือเหตุผลที่การจัดการชิ้นส่วนอย่างถูกต้อง (ส่งชิ้นส่วนสุดท้าย) มีความสำคัญ

## การจัดการหลายชิ้นส่วน (ขั้นสูง)

เมื่อทำงานกับข้อมูลสตรีมจริง ๆ คุณมักจะได้รับชิ้นส่วนเล็ก ๆ จำนวนมาก โค้ดด้านล่างแสดงวิธีวนลูปจนกว่าจะถึงจุดสิ้นสุดของแหล่งข้อมูล

```csharp
static string OcrFromStream(OcrEngine engine, Stream source)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192]; // 8 KB per read – adjust as needed
    int bytesRead;
    while ((bytesRead = source.Read(buffer, 0, buffer.Length)) > 0)
    {
        // If the last read returned fewer bytes, copy only that many.
        if (bytesRead < buffer.Length)
        {
            byte[] chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

> **ทำไมวิธีนี้ช่วยได้:** การสตรีมโดยตรงจาก `NetworkStream` หรือ `FileStream` ทำให้คุณไม่ต้องโหลดภาพทั้งหมดเข้าสู่หน่วยความจำ ซึ่งเป็นประโยชน์อย่างยิ่งสำหรับ PDF ขนาดใหญ่หรือภาพความละเอียดสูง

## ปัญหาที่พบบ่อย & วิธีหลีกเลี่ยง

| ปัญหา | อาการ | วิธีแก้ |
|---------|----------|-----|
| ไม่พบไลเซนส์ | `SetLicense` ขว้าง `FileNotFoundException` | ตรวจสอบเส้นทางและตั้งค่า *Copy to Output Directory* เป็น *Copy always* |
| ผลลัพธ์ว่าง | ไม่พบข้อความพิมพ์ออก | ตรวจสอบว่าคุณได้เรียก `BeginRecognize` **ก่อน** `AppendChunk` และ `EndRecognize` **หลัง** ชิ้นส่วนสุดท้าย |
| รั่วไหลหน่วยความจำ | แอปช้าลงหลังจากเรียก OCR หลายครั้ง | ทำการ `Dispose` `OcrEngine` หลังการใช้แต่ละครั้ง หรือใช้ instance เดียวโดยเรียก `Dispose` อย่างเหมาะสม |
| ชิ้นส่วนเสียหาย | อักขระแปลก ๆ | ตรวจสอบขนาดชิ้นส่วน; สำหรับ JPEG/PNG ไบต์แรกควรเริ่มด้วย `0xFF 0xD8` หรือ `0x89 0x50` |

## โบนัส: ใช้สตรีมแบบอะซิงโครนัส

หากแหล่งข้อมูลของคุณเป็นสตรีมตอบกลับจาก `HttpClient` คุณสามารถปรับลูปให้ `await` การอ่านได้:

```csharp
static async Task<string> OcrFromAsyncStream(OcrEngine engine, Stream asyncSource)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192];
    int bytesRead;
    while ((bytesRead = await asyncSource.ReadAsync(buffer, 0, buffer.Length)) > 0)
    {
        if (bytesRead < buffer.Length)
        {
            var chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

วิธีนี้ทำให้ UI ของแอปเดสก์ท็อปหรือมือถือตอบสนองได้ดีขึ้นและเพิ่มอัตราการผ่านข้อมูลบนเซิร์ฟเวอร์

## สรุป

คุณมี **โซลูชันครบวงจรและอิสระ** สำหรับ **วิธีใช้ OCR** ใน C# และ **จดจำข้อความจากสตรีม** ด้วย Aspose.OCR บทเรียนนี้ครอบคลุมตั้งแต่การตั้งค่าไลเซนส์และการเริ่มต้นจนถึงการป้อนชิ้นส่วนภาพ, การจัดการกรณีขอบ, และแม้แต่เวอร์ชันอะซิงโครนัส  

ลองใช้งาน – แทนที่ `sample.jpg` ด้วยฟีดกล้องสด, ภาพที่เก็บบนคลาวด์, หรือการอัปโหลด HTTP แบบ multipart เมื่อคุณคุ้นเคยแล้ว ลองสำรวจฟีเจอร์ขั้นสูงเช่น language packs, การพรี‑โปรเซสแบบกำหนดเอง, หรือการประมวลผลหลายสตรีมพร้อมกัน  

**ขั้นตอนต่อไป:**  
- ทดลอง OCR บน PDF โดยแปลงแต่ละหน้าเป็นภาพก่อน  
- ทดลองปรับ `engine.Config` เพื่อเพิ่มความแม่นยำสำหรับฟอนต์เฉพาะ  
- ผสานกับ Azure Functions หรือ AWS Lambda เพื่อสร้างไพป์ไลน์การสกัดข้อความแบบ serverless  

ขอให้เขียนโค้ดสนุกและสตรีมของคุณคมชัดเสมอ ผลลัพธ์ OCR ของคุณก็จะไม่มีที่ติ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
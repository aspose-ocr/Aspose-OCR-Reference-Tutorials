---
category: general
date: 2026-03-05
description: วิธีใช้ OCR ใน C# เพื่อสกัดข้อความจากภาพ เรียนรู้การแปลงภาพเป็นข้อความ
  อ่านอักขระภาษาเกาหลี และโหลดภาพสำหรับ OCR อย่างรวดเร็ว
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: th
og_description: วิธีใช้ OCR ใน C# และดึงข้อความจากภาพได้ทันที คู่มือนี้แสดงวิธีแปลงภาพเป็นข้อความ
  อ่านอักษรเกาหลี และโหลดภาพสำหรับ OCR
og_title: วิธีใช้ OCR ใน C# – แยกข้อความจากรูปภาพ
tags:
- OCR
- C#
- Aspose
title: วิธีใช้ OCR ใน C# – ดึงข้อความจากรูปภาพ
url: /th/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – แยกข้อความจากรูปภาพ

เคยสงสัย **วิธีใช้ OCR** เมื่อคุณมีภาพหน้าจอที่เต็มไปด้วยข้อความภาษาเกาหลีและต้องการสตริงธรรมดากลับมาไหม? คุณไม่ได้เป็นคนเดียวที่งงกับเรื่องนี้ ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์พร้อมทำงานได้ทันทีที่ **แยกข้อความจากรูปภาพ**, **แปลงรูปภาพเป็นข้อความ**, และแม้กระทั่งแสดงวิธี **อ่านอักขระภาษาเกาหลี** ด้วย Aspose.OCR  

เราจะครอบคลุมขั้นตอนที่มักถูกมองข้ามคือ **การโหลดภาพสำหรับ OCR** เพื่อให้คุณไม่เจอข้อผิดพลาด “ไฟล์ไม่พบ” ในภายหลัง สุดท้ายคุณจะได้โปรแกรมที่ทำงานได้เองซึ่งสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้

## สิ่งที่คุณต้องเตรียม

- .NET 6+ (หรือ .NET Framework 4.7.2 ขึ้นไป) – โค้ดทำงานได้ทั้งสองเวอร์ชัน  
- Aspose.OCR for .NET – สามารถดาวน์โหลดเวอร์ชันทดลองฟรีจากเว็บไซต์ Aspose  
- ตัวอย่างรูปภาพ (`korean_doc.png`) ที่มีข้อความภาษาเกาหลี  
- IDE ที่คุณชื่นชอบ (Visual Studio, Rider, VS Code – ตามที่คุณถนัด)

ไม่ต้องใช้ไลบรารีของบุคคลที่สามอื่นใด

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่ม Aspose.OCR

แรกสุด สร้างแอปคอนโซลใหม่:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

จากนั้นเพิ่มแพคเกจ NuGet ของ Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

> **เคล็ดลับ:** หากคุณมีไฟล์ลิขสิทธิ์ ให้วางไว้ที่โฟลเดอร์รากของโปรเจกต์; หากไม่มี เวอร์ชันทดลองจะทำงานได้แต่จะใส่น้ำลายน้ำในผลลัพธ์

## ขั้นตอนที่ 2: วิธีใช้ OCR – เริ่มต้น Engine

ต่อไปเราจะเขียนโค้ด C# สิ่งแรกที่ต้องทำเมื่อ **วิธีใช้ OCR** คือสร้างอินสแตนซ์ของ `OcrEngine` วัตถุนี้เป็นหัวใจของไลบรารี; มันเก็บการตั้งค่าต่าง ๆ ที่คุณจะต้องใช้ต่อไป

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**ทำไมจึงสำคัญ:** หากไม่มีอินสแตนซ์ของ engine ที่ถูกต้อง คุณจะไม่สามารถตั้งค่าภาษา, โหลดภาพ, หรือดึงผลลัพธ์ได้ Engine ยังจัดการทรัพยากรภายในด้วย การสร้างครั้งเดียวแล้วใช้ซ้ำจะมีประสิทธิภาพกว่าการสร้างใหม่ทุกครั้ง

## ขั้นตอนที่ 3: เลือกภาษา – อ่านอักขระภาษาเกาหลี

บรรทัดต่อไปบอก engine ว่าจะมองหาภาษาอะไร เนื่องจากเป้าหมายของเราคือ **อ่านอักขระภาษาเกาหลี** เราจึงตั้งค่า `OcrLanguage.Korean` คุณสามารถเปลี่ยนเป็น Arabic, Thai, Gujarati ฯลฯ ตามกรณีการใช้งานของคุณ

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**ทำไมถึงสำคัญ:** การเลือกภาษาอย่างถูกต้องช่วยเพิ่มความแม่นยำอย่างมาก OCR engine จะใช้พจนานุกรมและโมเดลอักขระเฉพาะภาษา; การใส่ภาษาผิดอาจทำให้ผลลัพธ์เป็นข้อความอ่านไม่ออก

## ขั้นตอนที่ 4: โหลดภาพสำหรับ OCR – แปลงรูปภาพเป็นข้อความ

ก่อนที่ engine จะทำงานใด ๆ คุณต้อง **โหลดภาพสำหรับ OCR** เมธอด `ImageStream.FromFile` จะอ่านไฟล์เข้าสู่รูปแบบที่ engine เข้าใจ

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

หากภาพอยู่ในโฟลเดอร์อื่น ให้ปรับพาธให้ตรง อย่าลืมตั้งค่า *Build Action* ของไฟล์เป็น “Copy if newer” เพื่อให้ไฟล์สามารถถูกค้นพบในขณะรันไทม์

> **ข้อผิดพลาดทั่วไป:** การใส่พาธที่มีเครื่องหมายแบ็คสแลช (`\`) ในสตริงลิเทรัลโดยไม่ทำการ escape จะทำให้คอมไพล์ล้มเหลว ใช้สองแบ็คสแลช (`\\`) หรือสตริงแบบ verbatim (`@"C:\path\file.png"`)

## ขั้นตอนที่ 5: ทำ OCR – แยกข้อความจากรูปภาพ

ตอนนี้งานหนักเริ่มทำงาน การเรียก `Recognize()` จะรันอัลกอริทึม OCR และคุณสมบัติ `Text` จะให้สตริงดิบที่ได้

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

ณ จุดนี้คุณได้ **แยกข้อความจากรูปภาพ** และโดยอ้อม **แปลงรูปภาพเป็นข้อความ** ผลลัพธ์อาจมีอักขระขึ้นบรรทัดใหม่หากเลย์เอาต์ต้นฉบับมีการแบ่งบรรทัด

## ขั้นตอนที่ 6: แสดงผลลัพธ์ – ตรวจสอบเอาต์พุต

สุดท้าย ให้พิมพ์ผลลัพธ์ลงคอนโซลเพื่อยืนยันว่าโปรแกรมทำงานถูกต้อง

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

รันโปรแกรม:

```bash
dotnet run
```

### ผลลัพธ์ที่คาดหวัง

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

หากคุณเห็นอักขระภาษาเกาหลีที่คล้ายกับในภาพ ยินดีด้วย—คุณได้เชี่ยวชาญ **วิธีใช้ OCR** กับ Aspose.OCR แล้ว!

![how to use OCR example diagram](image.png)

*ข้อความแทนภาพ: แผนผังตัวอย่างวิธีใช้ OCR แสดงขั้นตอนตั้งแต่การโหลดภาพจนถึงการพิมพ์ข้อความที่ถูกจดจำ*

## กรณีขอบและการปรับใช้

### 1. การจัดการหลายหน้า

หากต้อง **แยกข้อความจากรูปภาพ** ที่มีหลายหน้า (เช่น TIFF หลายหน้า) ให้วนลูปแต่ละหน้าและเรียก `Recognize()` สำหรับแต่ละอินสแตนซ์ของ `ImageStream`

### 2. การจัดการสแกนคุณภาพต่ำ

ภาพความละเอียดต่ำอาจทำให้ความแม่นยำลดลง ก่อนเรียก `Recognize()` คุณสามารถปรับปรุงภาพด้วยเครื่องมือ preprocessing ของ Aspose:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. การสลับภาษาแบบไดนามิก

สมมติว่าคุณมีเอกสารหลายภาษา คุณสามารถเปลี่ยน `ocrEngine.Language` ระหว่างการจดจำได้:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. การบันทึกผลลัพธ์ลงไฟล์

หากต้องการ **แปลงรูปภาพเป็นข้อความ** แล้วเก็บไว้ เพียงเขียนสตริงลงไฟล์ `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## คำถามที่พบบ่อย

- **ต้องมีลิขสิทธิ์เพื่อรันโค้ดนี้หรือไม่?**  
  ไม่จำเป็น เวอร์ชันทดลองทำงานได้สำหรับการทดลอง แต่จะใส่น้ำลายน้ำในผลลัพธ์ ลิขสิทธิ์ที่ซื้อจะลบน้ำลายน้ำและเปิดประสิทธิภาพเต็มที่

- **สามารถใช้บน Linux ได้หรือไม่?**  
  ได้เลย Aspose.OCR รองรับหลายแพลตฟอร์ม; เพียงตรวจสอบให้มี dependency เนทีฟที่จำเป็น (libgdiplus สำหรับ .NET Core บน Linux)

- **ถ้าภาพของฉันอยู่ในสตรีมแทนไฟล์จะทำอย่างไร?**  
  ใช้ `ImageStream.FromStream(yourStream)` – API รองรับ `System.IO.Stream` ใด ๆ

## สรุป

เราได้พาคุณผ่าน **วิธีใช้ OCR** ใน C# เพื่อ **แยกข้อความจากรูปภาพ**, **แปลงรูปภาพเป็นข้อความ**, และ **อ่านอักขระภาษาเกาหลี** พร้อมกับการ **โหลดภาพสำหรับ OCR** อย่างถูกต้อง ตัวอย่างที่สมบูรณ์และพร้อมรันข้างต้นควรทำงานได้ทันที และเคล็ดลับเพิ่มเติมจะช่วยให้คุณต่อยอดไปสู่สถานการณ์ที่ซับซ้อนยิ่งขึ้น

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองสลับภาษาอื่น, ประมวลผล PDF ทีละหน้า, หรือรวมการเรียก OCR เข้าไปใน Web API เพื่อให้ผู้ใช้อัปโหลดรูปแล้วรับข้อความทันที ความเป็นไปได้ไม่มีที่สิ้นสุด และตอนนี้คุณมีพื้นฐานที่มั่นคงเพื่อสร้างต่อได้แล้ว

Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
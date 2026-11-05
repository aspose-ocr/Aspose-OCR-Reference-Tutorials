---
category: general
date: 2026-04-06
description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความธรรมดาจากภาพ JPG รวมถึงอักขระซีริลลิก
  เรียนรู้การโหลดภาพสำหรับ OCR, การจดจำข้อความจาก JPG และการได้ผลลัพธ์ที่เชื่อถือได้.
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: th
og_description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความธรรมดาจากไฟล์ JPG คู่มือนี้แสดงวิธีโหลดภาพสำหรับ
  OCR, จดจำข้อความใน JPG, และจัดการข้อความภาษาซิริลิก
og_title: วิธีใช้ OCR ใน C# – แยกข้อความธรรมดาจากภาพ
tags:
- C#
- OCR
- Aspose
- Image Processing
title: วิธีใช้ OCR ใน C# – แยกข้อความธรรมดาจากรูปภาพ
url: /th/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – ดึงข้อความธรรมดาจากรูปภาพ

เคยสงสัย **วิธีใช้ OCR** ในโปรเจกต์ .NET โดยไม่ต้องต่อสู้กับไลบรารีเนทีฟหรือไม่? บางทีคุณอาจมีโฟลเดอร์ที่เก็บใบเสร็จสแกน, ภาพหน้าจอหลายภาพที่มีคำบรรยายเป็นภาษาซิริลิก, หรือแค่ต้องการดึงข้อความจากไฟล์ JPEG เพื่อการวิเคราะห์อย่างรวดเร็ว ข่าวดีคือ Aspose OCR ทำให้กระบวนการทั้งหมดเป็นเรื่องง่าย

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งจะแสดง **วิธีใช้ OCR** เพื่อ **ดึงข้อความธรรมดา** จากภาพ JPEG, **โหลดภาพสำหรับ OCR**, และแม้กระทั่ง **ดึงข้อความภาษาซิริลิก** เมื่อแหล่งภาษานั้นไม่ใช่ละติน สิ้นสุดคุณจะได้แอปคอนโซลขนาดเล็กที่พิมพ์ข้อความที่จดจำได้โดยตรงไปที่คอนโซล—ไม่มีไฟล์เพิ่มเติม, ไม่มีผลข้างเคียงที่ลึกลับ

> **สิ่งที่คุณจะได้รับ**  
> * คู่มือขั้นตอน‑ต่อ​ขั้นตอนที่คุณสามารถคัดลอก‑วางลงใน Visual Studio ได้  
> * คำอธิบาย *ทำไม* แต่ละบรรทัดจึงสำคัญ, ไม่ใช่แค่ *ทำอะไร*  
> * เคล็ดลับสำหรับการจัดการภาพขนาดใหญ่, หลายภาษา, และข้อผิดพลาดทั่วไป

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึก, โปรดตรวจสอบว่าคุณมี:

* .NET 6 SDK หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Core และ .NET Framework ด้วย)  
* Visual Studio 2022 (หรือเครื่องมือแก้ไขใด ๆ ที่คุณชอบ)  
* การเชื่อมต่ออินเทอร์เน็ตในครั้งแรกที่รันตัวอย่าง—Aspose OCR จะดาวน์โหลดแพ็คภาษาตามความต้องการ  

หากคุณยังไม่มีแพคเกจ NuGet ของ Aspose OCR, เราจะครอบคลุมขั้นตอนแรกให้

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR ผ่าน NuGet (และทำไมจึงสำคัญ)

ขั้นตอน **โหลดภาพสำหรับ OCR** ไม่สามารถทำได้จนกว่าจะมีไลบรารีอยู่ การใช้ NuGet รับประกันว่าคุณจะได้ไบนารีที่อัปเดตล่าสุด, มีการแพตช์ความปลอดภัย, และดึง dependencies ที่จำเป็นโดยอัตโนมัติ

```bash
dotnet add package Aspose.OCR
```

*ทำไมจึงสำคัญ*: Aspose OCR มีเพียง core DLL ขนาดเล็กและดึงข้อมูลภาษาตามที่คุณร้องขอเท่านั้น ทำให้แอปของคุณเบาและหลีกเลี่ยงการบรรจุไฟล์ภาษาที่ไม่ได้ใช้หลายเมกะไบต์

## ขั้นตอนที่ 2 – เริ่มต้น OCR Engine (หัวใจของ **วิธีใช้ OCR**)

การสร้างอินสแตนซ์ `OcrEngine` เป็นบรรทัดโค้ดแรกที่สำคัญสำหรับ **วิธีใช้ OCR** เอนจินตั้งค่าเป็นโหมด “on‑demand” โดยอัตโนมัติ ซึ่งหมายความว่าจะดาวน์โหลดแพ็คภาษาครั้งแรกที่คุณร้องขอภาษาเฉพาะ

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **เคล็ดลับระดับมืออาชีพ**: หากคุณทำงานอยู่หลังพร็อกซีขององค์กร, ตั้งค่า `OcrEngine.Proxy` ก่อนการเรียกจดจำครั้งแรกเพื่อให้การดาวน์โหลดสำเร็จ

## ขั้นตอนที่ 3 – เลือกภาษา – **ดึงข้อความซิริลิก** เมื่อจำเป็น

Aspose OCR รองรับสคริปต์หลายสิบแบบ เพื่อ **ดึงข้อความซิริลิก**, เพียงตั้งค่า property `Language` เป็น `OcrLanguage.Cyrillic` ครั้งแรกที่บรรทัดนี้ทำงาน โมดูลซิริลิก (≈ 5 MB) จะถูกดึงจาก CDN ของ Aspose

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

หากภาพของคุณมีเฉพาะอักขระละติน, คุณสามารถเปลี่ยน `Cyrillic` เป็น `English` ได้ รูปแบบเดียวกันทำงานกับภาษาที่รองรับทุกภาษา

## ขั้นตอนที่ 4 – **โหลดภาพสำหรับ OCR** – จากดิสก์หรือสตรีม

ตอนนี้เราจะ **โหลดภาพสำหรับ OCR** จริง ๆ คลาส `System.Drawing.Image` รองรับรูปแบบที่พบบ่อย (JPG, PNG, BMP) หากคุณอยู่บนแพลตฟอร์มที่ไม่ใช่ Windows, พิจารณาใช้ `ImageSharp` แทน, แต่สำหรับบทแนะนำนี้ชนิดที่มาพร้อมระบบก็เพียงพอ

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **ทำไมจึงสำคัญ**: การโหลดภาพภายในบล็อก `using` รับประกันว่าทรัพยากร GDI+ ที่ไม่ได้จัดการจะถูกปล่อยอย่างทันท่วงที, ป้องกันการรั่วของหน่วยความจำในบริการที่ทำงานต่อเนื่อง

## ขั้นตอนที่ 5 – **จดจำข้อความ JPG** – รันกระบวนการ OCR

เมื่อเอ็นจินตั้งค่าแล้วและภาพถูกโหลด, เราจึง **จดจำข้อความ jpg** สุดท้าย เมธอด `Recognize` จะคืนค่า `OcrResult` ที่มีสตริงธรรมดา, คะแนนความมั่นใจ, และแม้กระทั่ง bounding box หากคุณต้องการใช้ต่อไป

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

หากต้องการปรับความแม่นยำ, คุณสามารถแก้ไข `ocrEngine.Config` (เช่น เปิด `AutoRotate` หรือกำหนด `TextOrientation`) สำหรับสถานการณ์ง่าย ๆ ค่าเริ่มต้นทำงานได้ดีอย่างน่าประหลาดใจ

## ขั้นตอนที่ 6 – **ดึงข้อความธรรมดา** – แสดงผลลัพธ์

ส่วนสุดท้ายของ **วิธีใช้ OCR** คือการดึงสตริงที่จดจำได้จาก `ocrResult` และทำบางอย่างกับมัน ที่นี่เราจะเขียนลงคอนโซล ซึ่งยังแสดงวิธี **ดึงข้อความธรรมดา** จากอ็อบเจกต์ผลลัพธ์

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### ผลลัพธ์ที่คาดหวัง

หาก `cyrillic_sample.jpg` มีประโยค “Привет мир” (Hello world), คุณควรเห็น:

```
=== Recognized Text ===
Привет мир
```

หากภาพเบลอหรือข้อความเล็กเกินไป, ผลลัพธ์อาจมีข้อผิดพลาด; คุณสามารถตรวจสอบ `ocrResult.Confidence` เพื่อพิจารณาว่าจะลองใหม่ด้วยแหล่งที่มีความละเอียดสูงขึ้นหรือไม่

## ตัวอย่างเต็มที่พร้อมรัน

ด้านล่างเป็นโปรแกรมทั้งหมด คัดลอกไปในโปรเจกต์ Console App ใหม่ (`dotnet new console`) แล้วรัน ไม่ต้องมีไฟล์เพิ่มเติมนอกจากภาพที่คุณระบุ

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **หมายเหตุ**: แทนที่ `YOUR_DIRECTORY\cyrillic_sample.jpg` ด้วยพาธจริงของไฟล์ JPEG ของคุณ

## คำถามทั่วไป & กรณีขอบ

### ถ้าฉันต้อง **จดจำข้อความ jpg** จากสตรีมแทนไฟล์ล่ะ?

คุณสามารถส่ง `MemoryStream` โดยตรงได้:

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### จะจัดการหลายภาษาในภาพเดียวอย่างไร?

ตั้งค่า `ocrEngine.Language` เป็น `OcrLanguage.Multilingual` เอ็นจินจะพยายามตรวจจับแต่ละสคริปต์โดยอัตโนมัติ, ซึ่งสะดวกเมื่อใบเสร็จผสม English กับ Cyrillic

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### ภาพของฉันใหญ่เกิน (มากกว่า 5 MP) จะทำให้เอ็นจินทำงานช้าไหม?

ภาพขนาดใหญ่เพิ่มการใช้หน่วยความจำและอาจทำให้การจดจำช้าลง การปรับขนาดล่วงหน้าอย่างรวดเร็วช่วยได้:

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### สามารถรับคะแนนความมั่นใจสำหรับแต่ละบรรทัดได้ไหม?

ได้—`ocrResult.Lines` มี `Confidence` ต่อบรรทัด การวนลูปผ่านพวกมันทำให้คุณกรองผลลัพธ์ที่ความมั่นใจต่ำออกได้

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## เคล็ดลับระดับมืออาชีพสำหรับ OCR ที่พร้อมใช้งานใน Production

* **แคชแพ็คภาษ** – การดาวน์โหลดครั้งแรกอาจใช้หลายวินาที; เก็บไฟล์ไว้ในโฟลเดอร์ที่รู้จักและตั้งค่า `ocrEngine.LanguageDataPath` เพื่อใช้ซ้ำ  
* **ประมวลผลเป็นชุด** – ใช้อินสแตนซ์ `OcrEngine` เดียวสำหรับหลายภาพ; การสร้างเอ็นจินใหม่ต่อไฟล์เพิ่มภาระที่ไม่จำเป็น  
* **การจัดการข้อผิดพลาด** – ห่อการเรียก `Recognize` ด้วย try/catch. Aspose จะโยน `OcrException` สำหรับภาพเสียหายหรือฟอร์แมตที่ไม่รองรับ  
* **การบันทึก** – บันทึก `ocrResult.Confidence` เพื่อให้คุณสามารถตรวจสอบภายหลังว่าหน้าหนึ่งต้องการการตรวจสอบด้วยมือหรือไม่

## สรุป

เราได้ครอบคลุม **วิธีใช้ OCR** ใน C# เพื่อ **ดึงข้อความธรรมดา** จาก JPEG, แสดงขั้นตอน **โหลดภาพสำหรับ OCR**, แสดงวิธี **จดจำข้อความ jpg**, และแม้กระทั่งดึง **ข้อความซิริลิก** จากรูปภาพ ตัวอย่างทำงานเต็มรูปแบบ, ต้องการเพียงแพคเกจ NuGet เดียว, และสามารถขยายเพื่อรองรับเอกสารหลายภาษา, งานแบบแบตช์, หรือการสแกนแบบเรียลไทม์ได้

พร้อมรับความท้าทายต่อไปหรือยัง? ลองสลับภาษาซิริลิกเป็น Arabic, ทดลองกับแฟล็ก `AutoRotate`, หรือผสานผลลัพธ์เข้ากับดัชนีการค้นหา ความเป็นไปได้ไม่มีที่สิ้นสุด

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
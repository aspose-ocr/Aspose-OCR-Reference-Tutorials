---
category: general
date: 2026-03-05
description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากภาพใบเสร็จ เรียนรู้วิธีโหลดภาพสำหรับ
  OCR และจดจำภาพใบเสร็จในไม่กี่นาที
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: th
og_description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากใบเสร็จ ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อโหลดภาพสำหรับ
  OCR และจดจำภาพใบเสร็จอย่างมีประสิทธิภาพ
og_title: วิธีใช้ OCR ใน C# – การสกัดข้อความใบเสร็จอย่างรวดเร็ว
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: วิธีใช้ OCR ใน C# – ดึงข้อความจากใบเสร็จอย่างรวดเร็ว
url: /th/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – ดึงข้อความจากใบเสร็จอย่างรวดเร็ว

เคยสงสัย **วิธีใช้ OCR** เพื่อดึงข้อมูลโดยตรงจากรูปถ่ายใบเสร็จของร้านขายของชำหรือไม่? คุณไม่ได้เป็นคนเดียว ในแอปธุรกิจขนาดเล็กหลาย ๆ แห่ง ปัญหาคอขวดคือการแปลงไฟล์ PNG ที่เบลอให้เป็นข้อความที่มีโครงสร้างและสามารถนำไปใช้งานได้จริง  

ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# และ Aspose.OCR คุณสามารถ **โหลดรูปภาพสำหรับ OCR** รันเอนจินและ **จดจำภาพใบเสร็จ** ได้ภายในไม่ถึงหนึ่งนาที ด้านล่างคุณจะเห็นตัวอย่างที่สมบูรณ์พร้อมรัน รวมถึงเคล็ดลับสำหรับส่วนที่ซับซ้อนซึ่งบทแนะนำส่วนใหญ่มักมองข้าม

## สิ่งที่คู่มือนี้ครอบคลุม

เราจะเดินผ่านทุกอย่างที่คุณต้องรู้:

* การติดตั้งแพคเกจ Aspose.OCR NuGet.  
* การตั้งค่า OCR engine – แกนหลักของ **วิธีใช้ OCR** อย่างถูกต้อง.  
* การโหลดไฟล์ใบเสร็จ (ขั้นตอน **โหลดรูปภาพสำหรับ OCR**).  
* การรันกระบวนการจดจำและดึงข้อมูลทั้งในรูปแบบ JSON และ XML.  
* การจัดการกับปัญหาทั่วไป เช่น ใบอนุญาตที่หายไปหรือรูปแบบภาพที่ไม่รองรับ.  

เมื่อเสร็จสิ้น คุณจะมีโปรแกรมที่ทำงานอิสระซึ่งดึงข้อความจากใบเสร็จใด ๆ ที่คุณวางลงในโฟลเดอร์ ไม่ต้องพึ่งบริการภายนอก ไม่มีเวทมนตร์ลับ

## ข้อกำหนดเบื้องต้น

* .NET 6 SDK หรือรุ่นที่ใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ .NET Core ด้วย).  
* ไฟล์ใบอนุญาต Aspose.OCR ที่ถูกต้อง (`Aspose.OCR.lic`). คุณสามารถรับเวอร์ชันทดลองฟรีจาก Aspose หากยังไม่มี.  
* ตัวอย่างรูปภาพใบเสร็จ – `receipt.png` ใช้งานได้ดี แต่รูปแบบ raster ทั่วไปใดก็ได้ก็ใช้ได้.  

หากคุณมีทั้งหมดแล้ว เยี่ยม – ไปต่อกันเลย.

![ตัวอย่างวิธีใช้ OCR](https://example.com/ocr-receipt.png "ตัวอย่างวิธีใช้ OCR")

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR และสร้างโปรเจคใหม่

สิ่งแรกที่ต้องทำคือคุณต้องมีไลบรารีที่ทำงานหนักจริง ๆ เปิดเทอร์มินัลในโฟลเดอร์โปรเจคของคุณและรัน:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

คำสั่งนั้นจะสร้างแอปคอนโซลและดึงแพคเกจ Aspose.OCR ล่าสุดเข้ามา จากประสบการณ์ของผม การตั้งชื่อโปรเจคให้สั้นทำให้เส้นทางที่สร้างขึ้นอ่านง่ายขึ้น โดยเฉพาะเมื่อคุณเริ่มจัดการหลายแอปสาธิต

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine – ใจกลางของ **วิธีใช้ OCR**

ตอนนี้เราจะเขียนโค้ดที่ตอบคำถาม “**วิธีใช้ OCR** ใน C#” เปิดไฟล์ `Program.cs` แล้วแทนที่เนื้อหาด้วยโค้ดตัวอย่างด้านล่าง โปรดสังเกตคอมเมนต์ – พวกมันอธิบาย *เหตุผล* ของแต่ละบรรทัด ไม่ใช่แค่ *สิ่งที่ทำ*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

* **`OcrEngine`** คือจุดเริ่มต้น; มันเก็บการตั้งค่าทั้งหมดที่คุณอาจปรับเปลี่ยนในภายหลัง (ภาษา, DPI, ฯลฯ).  
* **`SetLicense`** ลบลายน้ำการประเมิน – ขั้นตอนสำคัญเมื่อคุณวางแผนจะเผยแพร่โค้ด.  
* **`ImageStream.FromFile`** ทำหน้าที่ **โหลดรูปภาพสำหรับ OCR** รองรับ PNG, JPEG, BMP, TIFF และอื่น ๆ.  
* **`Recognize()`** คือเมธอดที่จริง ๆ แล้ว **จดจำภาพใบเสร็จ** ภายในทำการไบนารีเซชัน, แบ่งส่วน, และการจำแนกอักขระ.  
* การส่งออกเป็น JSON และ XML ให้คุณทั้งข้อมูลที่มนุษย์อ่านได้และโครงสร้างที่เครื่องอ่านได้ซึ่งคุณสามารถส่งต่อให้ตัวแยกข้อมูลต่อไป.

## ขั้นตอนที่ 3: รันตัวอย่างและตรวจสอบผลลัพธ์

Compile and execute:

```bash
dotnet run
```

If everything is wired correctly you’ll see something like:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

คอนโซลจะแสดงข้อความธรรมดา ส่วน `receipt.json` และ `receipt.xml` จะมีข้อมูลการจัดวางอย่างละเอียด (พิกัด, คะแนนความมั่นใจ ฯลฯ) ไฟล์เหล่านี้มีประโยชน์หากคุณต้องการแมปแต่ละบรรทัดไปยังฟิลด์ฐานข้อมูลในภายหลัง

## กรณีขอบและเคล็ดลับระดับมืออาชีพ

### 1️⃣ ใบอนุญาตหายหรือไม่ถูกต้อง
หาก `SetLicense` ล้มเหลว เอนจินจะกลับไปใช้โหมดทดลองและคุณจะเห็นลายน้ำในผลลัพธ์ ห่อหุ้มการเรียกใน try/catch และบันทึกข้อความที่เป็นมิตร:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ รูปแบบภาพที่ไม่รองรับ
Aspose.OCR รองรับรูปแบบ raster ส่วนใหญ่ แต่หากคุณป้อน PDF หรือ TIFF หลายหน้า คุณต้องแปลงหน้าที่ต้องการเป็นภาพก่อน ไลบรารี `Aspose.PDF` สามารถทำการแปลงนี้ได้.

### 3️⃣ ใบเสร็จขนาดใหญ่และประสิทธิภาพ
การประมวลผลภาพขนาด 10 MB อาจช้า ลดความละเอียดก่อนส่งให้เอนจิน:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

เมธอด `Resize` จะรักษาอัตราส่วน (`0` สำหรับความสูง) และลดขนาดไฟล์อย่างมากโดยไม่ทำให้ความแม่นยำของ OCR ลดลงสำหรับใบเสร็จทั่วไป.

### 4️⃣ ปัญหาภาษาและฟอนต์
ใบเสร็จอาจมีอักขระพิเศษ (€, ¥, ฯลฯ) ตั้งค่าภาษาอย่างชัดเจนหากคุณรู้โลคัล:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

สำหรับใบเสร็จที่มีหลายภาษา คุณสามารถเปิดโหมดหลายภาษาได้:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ การสกัดข้อมูลเชิงโครงสร้าง
ข้อความดิบมีประโยชน์ แต่แอปส่วนใหญ่ต้องการฟิลด์เชิงโครงสร้าง (วันที่, ยอดรวม, รายการ) โครงสร้าง JSON มีพิกัด `BoundingBox` สำหรับแต่ละคำ คุณสามารถประมวลผลต่อได้ดังนี้:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถรันนี้บน Linux ได้หรือไม่?**  
ตอบ: ได้เลย Aspose.OCR รองรับหลายแพลตฟอร์ม; เพียงติดตั้ง .NET runtime บนเครื่อง Linux ของคุณ แล้วโค้ดเดียวกันก็ทำงานได้.

**ถาม: ถ้าฉันต้องประมวลผลหลายสิบใบเสร็จต่อหนึ่งนาทีจะทำอย่างไร?**  
ตอบ: สร้างลูป `Parallel.ForEach` และใช้ instance `OcrEngine` เดียวซ้ำ – มันปลอดภัยต่อเธรดสำหรับการอ่านอย่างเดียว อย่าลืมจัดการขีดจำกัดการใช้ใบอนุญาตพร้อมกัน.

**ถาม: วิธีนี้ทำงานกับรูปถ่ายจากมือถือที่ถ่ายเอียงได้หรือไม่?**  
ตอบ: เอนจินมีฟังก์ชัน deskew พื้นฐาน แต่สำหรับภาพที่เอียงมาก คุณอาจต้องทำการประมวลผลล่วงหน้าด้วยไลบรารีประมวลผลภาพ (เช่น OpenCV) เพื่อทำให้ใบเสร็จตรงก่อน.

## ตัวอย่างทำงานเต็ม (คัดลอก‑วาง)

ด้านล่างเป็นโปรแกรม *ทั้งหมด* ที่คุณสามารถวางลงใน `Program.cs` ไม่ต้องมีไฟล์อื่นนอกจากใบอนุญาตและรูปภาพใบเสร็จ.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
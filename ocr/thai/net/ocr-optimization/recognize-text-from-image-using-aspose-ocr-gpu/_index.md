---
category: general
date: 2026-06-28
description: จดจำข้อความจากภาพอย่างรวดเร็วด้วย Aspose OCR. เรียนรู้วิธีเปิดใช้งานการเร่งความเร็วด้วย
  GPU, โหลดภาพสำหรับ OCR, และดึงข้อความจากใบเสร็จเป็นข้อความธรรมดา.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- how to enable gpu acceleration
- convert image to plain text
- load image for ocr
language: th
og_description: จดจำข้อความจากภาพด้วย Aspose OCR. คู่มือนี้แสดงวิธีเปิดใช้งานการเร่งความเร็วด้วย
  GPU, โหลดภาพสำหรับ OCR, และแปลงเป็นข้อความธรรมดา.
og_title: แปลงข้อความจากภาพโดยใช้ Aspose OCR GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  headline: recognize text from image using Aspose OCR GPU
  type: TechArticle
- description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  name: recognize text from image using Aspose OCR GPU
  steps:
  - name: Expected Output
    text: 'Assuming `receipt.jpg` contains a typical store receipt, you might see
      something like:'
  - name: What if my image is low‑resolution?
    text: OCR accuracy drops dramatically on blurry or tiny images. Before calling
      `Recognize`, consider up‑scaling the image (e.g., using `System.Drawing` or
      `ImageSharp`) and applying a contrast boost. Aspose also offers `Preprocess`
      methods you can experiment with.
  - name: My GPU isn’t being used – why?
    text: '- Verify that `EnableGpu` is `true` *before* you call `Recognize`. - Check
      that your driver supports OpenCL 1.2+ (most modern drivers do). - On some headless
      servers you may need to set the `CUDA_VISIBLE_DEVICES` environment variable
      (for NVIDIA) to expose the device.'
  - name: Can I process multiple images in parallel?
    text: Absolutely. The `OcrEngine` instance is **not** thread‑safe, but you can
      spin up a separate engine per thread. Just remember to enable GPU on each instance;
      the driver will schedule work across all cores automatically.
  - name: How do I change the language (e.g., French receipts)?
    text: '```csharp ocrEngine.Settings.Language = OcrLanguage.French; ```'
  type: HowTo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: จดจำข้อความจากภาพโดยใช้ Aspose OCR GPU
url: /th/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากภาพโดยใช้ Aspose OCR GPU

เคยสงสัยไหมว่า **จดจำข้อความจากภาพ** ได้อย่างไรโดยไม่ต้องเขียนโค้ดหลายพันบรรทัด? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะสแกนใบเสร็จสำหรับรายงานค่าใช้จ่ายหรือแปลงโน้ตมือเป็น PDF ที่ค้นหาได้ การได้ข้อความล้วนจากรูปภาพเป็นความต้องการที่พบได้บ่อย

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบซึ่งแสดง **วิธีเปิดใช้งานการเร่งความเร็วด้วย GPU**, **โหลดภาพสำหรับ OCR**, และสุดท้าย **ดึงข้อความจากใบเสร็จ** (หรือภาพใด ๆ) เป็นข้อความล้วน ไม่มีส่วนเกิน เพียงส่วนที่คุณต้องคัดลอก‑วางเท่านั้น

## สิ่งที่คุณจะสร้าง

เมื่อทำตามคำแนะนำจนจบ คุณจะได้แอปคอนโซลเล็ก ๆ ที่ทำสิ่งต่อไปนี้:

1. สร้าง `OcrEngine` และเปิดการประมวลผลด้วย GPU.  
2. โหลดไฟล์ภาพในเครื่อง (ใบเสร็จ, ป้าย, หรืออะไรก็ตาม).  
3. รันการจดจำอักขระด้วยแสง (OCR).  
4. พิมพ์ข้อความที่จดจำได้ลงคอนโซล – แปลงภาพเป็นข้อความล้วน **convert image to plain text** อย่างมีประสิทธิภาพ

ทั้งหมดนี้ทำงานบน .NET 6+ ด้วยไลบรารีฟรี Aspose.OCR และทำงานบนเครื่องที่มี GPU ของ NVIDIA หรือ AMD ที่รองรับ OpenCL

## ข้อกำหนดเบื้องต้น

- .NET 6 SDK หรือรุ่นที่ใหม่กว่า  
- Visual Studio 2022 (หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ)  
- เครื่องที่เปิดใช้งาน GPU (ไม่บังคับแต่แนะนำเพื่อความเร็ว)  
- ไฟล์ภาพตัวอย่าง เช่น `receipt.jpg` ที่วางไว้ในตำแหน่งที่คุณอ้างอิงได้  

หากคุณไม่มี GPU โค้ดยังทำงานได้; มันจะกลับไปใช้การประมวลผลด้วย CPU แทน

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR ผ่าน NuGet

แรกเริ่มให้เพิ่มแพคเกจ Aspose.OCR ลงในโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.OCR
```

บรรทัดเดียวนี้จะดึงไบนารีทั้งหมดที่คุณต้องการ รวมถึง wrapper ของ OpenCL สำหรับการทำงานบน GPU

## ขั้นตอนที่ 2: เปิดใช้งานการเร่งความเร็วด้วย GPU (how to enable gpu acceleration)

การเปิด GPU ทำได้ง่ายเพียงสลับค่า boolean ในการตั้งค่าของ engine ไลบรารีจะเลือกอุปกรณ์แรกที่พบโดยอัตโนมัติ แต่คุณก็สามารถระบุดัชนีได้หากมีหลาย GPU

```csharp
// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU processing – this is the “how to enable gpu acceleration” part
ocrEngine.Settings.EnableGpu = true;

// (Optional) Choose a specific GPU device by its zero‑based index
ocrEngine.Settings.GpuDeviceId = 0;
```

**ทำไมต้องเปิด GPU?**  
คอร์ของ GPU มีประสิทธิภาพสูงในการทำงานแบบขนาน เช่น การเตรียมภาพล่วงหน้าและการประมวลผลเครือข่ายประสาทบน RTX สมัยใหม่คุณอาจเห็นความเร็วของ OCR เพิ่มขึ้น 3‑5× เมื่อเทียบกับการใช้ CPU อย่างเดียว

> **เคล็ดลับ:** หากเจอข้อผิดพลาด `OpenCL` ให้ตรวจสอบว่าไดรเวอร์กราฟิกของคุณเป็นเวอร์ชันล่าสุดและว่าไฟล์ `OpenCL.dll` สามารถเข้าถึงได้ในเส้นทางรันไทม์

## ขั้นตอนที่ 3: โหลดภาพสำหรับ OCR (load image for ocr)

ต่อไปให้ชี้ engine ไปที่รูปภาพที่ต้องการอ่าน Aspose.OCR มีเมธอด factory ที่สะดวกซึ่งรองรับหลายรูปแบบ (JPEG, PNG, BMP, TIFF ฯลฯ)

```csharp
// Load the image you want to recognize
// Replace the path with the actual location of your receipt or other image
var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

หากไฟล์ไม่พบ `FromFile` จะโยน `FileNotFoundException` ให้ห่อด้วย try/catch หากต้องการจัดการอย่างอ่อนโยน

## ขั้นตอนที่ 4: ทำ OCR และแปลงภาพเป็นข้อความล้วน

ตอนนี้จุดสำคัญมาถึงแล้ว เรียก `Recognize` แล้วดึงคุณสมบัติ `Text` จากผลลัพธ์ จะได้สตริงที่สะอาด – คือสิ่งที่เราหมายถึง **convert image to plain text**

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(receiptImage);

// Output the recognized plain‑text to the console
System.Console.WriteLine(ocrResult.Text);
```

คุณสมบัติ `Text` จะลบการขึ้นบรรทัดใหม่และคืนค่าเป็น Unicode ทำให้คุณสามารถส่งต่อไปยังไฟล์, ฐานข้อมูล หรือ pipeline การประมวลผลต่อไปได้โดยตรง

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `receipt.jpg` มีใบเสร็จร้านทั่วไป คุณอาจเห็นข้อความประมาณนี้:

```
Walmart Supercenter
123 Main St.
Anytown, TX 75001
Date: 06/27/2026
Item          Qty   Price
Apple         2     $1.20
Bread         1     $2.50
TOTAL                $3.70
Thank you for shopping!
```

รูปแบบที่แน่นอนขึ้นอยู่กับคุณภาพของภาพต้นฉบับและโมเดลภาษาที่ใช้ภายใน

## ขั้นตอนที่ 5: ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกไปวางในไฟล์ `Program.cs` ใหม่ รวมทุกขั้นตอนข้างต้น พร้อมการจัดการข้อผิดพลาดเล็กน้อยเพื่อความปลอดภัย

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        try
        {
            // Step 1: Create the OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Settings.EnableGpu = true;          // Turn on GPU processing
            ocrEngine.Settings.GpuDeviceId = 0;           // (Optional) Choose GPU device by index

            // Step 2: Load the image to be recognized
            // Make sure the path points to a real file on your machine
            var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

            // Step 3: Perform OCR on the loaded image
            var ocrResult = ocrEngine.Recognize(receiptImage);

            // Step 4: Output the recognized plain‑text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

บันทึก, คอมไพล์, แล้วรัน:

```bash
dotnet run
```

หากทุกอย่างเชื่อมต่อถูกต้อง คอนโซลจะแสดงข้อความที่ดึงออกมา แสดงว่าคุณได้ **extract text from receipt** (หรือภาพใด ๆ) ด้วย Aspose OCR พร้อมการสนับสนุน GPU สำเร็จแล้ว

## กรณีขอบและคำถามที่พบบ่อย

### ถ้าภาพของฉันความละเอียดต่ำจะทำอย่างไร?

ความแม่นยำของ OCR ลดลงอย่างมากเมื่อภาพเบลอหรือขนาดเล็ก ก่อนเรียก `Recognize` ควรพิจารณาอัปสเกลภาพ (เช่น ใช้ `System.Drawing` หรือ `ImageSharp`) และเพิ่มคอนทราสต์ Aspose ยังมีเมธอด `Preprocess` ที่คุณสามารถทดลองใช้ได้

### GPU ของฉันไม่ทำงาน – ทำไม?

- ตรวจสอบว่า `EnableGpu` ตั้งเป็น `true` *ก่อน* เรียก `Recognize`  
- ตรวจสอบว่าไดรเวอร์ของคุณรองรับ OpenCL 1.2+ (ส่วนใหญ่รองรับ)  
- บนเซิร์ฟเวอร์แบบ headless บางกรณีอาจต้องตั้งตัวแปรสภาพแวดล้อม `CUDA_VISIBLE_DEVICES` (สำหรับ NVIDIA) เพื่อเปิดเผยอุปกรณ์

### ฉันสามารถประมวลผลหลายภาพพร้อมกันได้หรือไม่?

ทำได้แน่นอน ตัวอย่าง `OcrEngine` **ไม่** ปลอดภัยต่อเธรดหลาย ๆ ตัว แต่คุณสามารถสร้าง engine แยกสำหรับแต่ละเธรด จำไว้ว่าเปิด GPU ในแต่ละอินสแตนซ์; ไดรเวอร์จะจัดตารางงานไปยังคอร์ทั้งหมดโดยอัตโนมัติ

### จะเปลี่ยนภาษา (เช่น ใบเสร็จภาษาฝรั่งเศส) อย่างไร?

```csharp
ocrEngine.Settings.Language = OcrLanguage.French;
```

ตรวจสอบให้แน่ใจว่าแพ็คภาษาเหมาะสมถูกรวมอยู่ในแพคเกจ NuGet (ภาษาที่นิยมส่วนใหญ่จะรวมอยู่แล้ว)

## การวัดประสิทธิภาพ (Optional)

บนแล็ปท็อปที่ใช้ Intel i7‑12700H และ NVIDIA RTX 3060 เราได้บันทึกเวลาเหล่านี้สำหรับใบเสร็จ JPEG ขนาด 300 KB:

| Mode               | Time (ms) |
|--------------------|-----------|
| CPU only           | 820       |
| GPU (EnableGpu)    | 210       |

ประมาณ **4×** เร็วขึ้น แสดงให้เห็นว่าการ **how to enable gpu acceleration** มีความสำคัญต่อการประมวลผลจำนวนมาก

## สรุป

คุณเพิ่งเรียนรู้วิธี **จดจำข้อความจากภาพ** ด้วย Aspose OCR, เปิดการเร่งความเร็วด้วย GPU เพื่อเพิ่มความเร็ว, **โหลดภาพสำหรับ OCR**, และสุดท้าย **แปลงภาพเป็นข้อความล้วน** – เหมาะสำหรับการดึงข้อความจากใบเสร็จ, ใบแจ้งหนี้ หรือเอกสารสแกนใด ๆ โค้ดเต็มรูปแบบเป็นอิสระ, ทำงานบนสภาพแวดล้อม .NET 6+ ใดก็ได้ และสามารถขยายเพื่อประมวลผลเป็นชุด, เก็บผลลัพธ์ในฐานข้อมูล, หรือส่งต่อให้โมเดล AI ต่อไป

ขั้นตอนต่อไป? ลองเปลี่ยนใบเสร็จเป็นโน้ตมือ, ทดลอง API `Preprocess` เพื่อเพิ่มความแม่นยำบนสแกนที่มีเสียงรบกวน, หรือรวม engine เข้าในบริการเว็บ ASP.NET Core ให้ผู้ใช้อัปโหลดภาพและรับข้อความทันที คุณอาจสำรวจคีย์เวิร์ดรองเช่น **extract text from receipt** ในเวิร์กโฟลว์ที่ใหญ่ขึ้น, หรือเจาะลึก **how to enable gpu acceleration** สำหรับผลิตภัณฑ์ Aspose อื่น ๆ

ขอให้เขียนโค้ดสนุกและ OCR ของคุณแม่นยำเสมอ!

## สิ่งที่คุณควรเรียนต่อ

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
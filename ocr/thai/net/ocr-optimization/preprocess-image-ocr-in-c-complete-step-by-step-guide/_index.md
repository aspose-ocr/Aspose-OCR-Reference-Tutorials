---
category: general
date: 2026-02-20
description: ทำการประมวลผลล่วงหน้าภาพ OCR ด้วย Aspose.OCR ใน C# เรียนรู้วิธีใช้ฟิลเตอร์มัธยฐาน
  ลดสัญญาณรบกวนของภาพ และสกัดข้อความจากภาพอย่างมีประสิทธิภาพ.
draft: false
keywords:
- preprocess image OCR
- apply median filter
- extract text image
- reduce image noise
- c# ocr example
language: th
og_description: ทำการประมวลผลล่วงหน้า OCR ของภาพด้วย Aspose.OCR. บทเรียนนี้แสดงวิธีการใช้ฟิลเตอร์มัธยฐาน,
  ลดสัญญาณรบกวนของภาพ, และสกัดข้อความจากภาพโดยใช้ C#.
og_title: การเตรียมการประมวลผล OCR ของภาพใน C# – คู่มือครบถ้วน
tags:
- OCR
- C#
- Image Processing
title: การเตรียมภาพ OCR ด้วย C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/ocr-optimization/preprocess-image-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การเตรียมภาพ OCR ใน C# – คู่มือขั้นตอนเต็ม

เคยต้อง **preprocess image OCR** เพราะรูปสแกนของคุณกลับให้ข้อความเป็นอักขระผสมกันหรือเปล่า? คุณไม่ได้เป็นคนเดียวที่เจอปัญหานี้ ในหลายโครงการจริง—เช่น ใบเสร็จ, บัตรประชาชน, หรือโน้ตมือเขียน—ภาพดิบมักไม่พร้อมสำหรับการจดจำโดยตรง ข่าวดีคือ ขั้นตอนการเตรียมภาพง่าย ๆ สามารถเพิ่มความแม่นยำได้อย่างมาก และคุณสามารถทำทั้งหมดนี้ใน C# ด้วย Aspose.OCR

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างเชิงปฏิบัติที่แสดงวิธี **apply median filter**, **reduce image noise**, และสุดท้าย **extract text image** ให้ได้ผลลัพธ์ที่สะอาดและอ่านง่าย ภายในไม่กี่ขั้นตอนคุณจะได้แอปคอนโซล C# ที่พร้อมรันและสามารถใส่ลงในโซลูชัน .NET ใดก็ได้ ไม่มีการอ้างอิงที่คลุมเครือ เพียงโค้ดที่คุณต้องการและ “เหตุผล” ของแต่ละบรรทัด

---

## สิ่งที่คุณต้องเตรียม

- **Aspose.OCR for .NET** (เวอร์ชันล่าสุด ณ เวลาที่เขียน, 23.12) คุณสามารถติดตั้งผ่าน NuGet: `Install-Package Aspose.OCR`.
- .NET 6.0 หรือใหม่กว่า (ตัวอย่างใช้คอนโซลแอป แต่ตรรกะเดียวกันทำงานได้ใน ASP.NET, WPF ฯลฯ)
- ตัวอย่างรูปภาพที่ต้องทำความสะอาด—เช่น `skewed_photo.jpg`.  
- ความรู้พื้นฐานของ C# ระดับกลาง; แนวคิดทั้งหมดง่ายต่อการเข้าใจแม้สำหรับนักพัฒนาระดับจูเนียร์

> **Pro tip:** หากคุณทำงานบนเครื่องขององค์กร ตรวจสอบให้แน่ใจว่า NuGet feed ของคุณตั้งค่าให้อนุญาตแพ็กเกจภายนอก มิฉะนั้นการติดตั้งจะล้มเหลว

---

## Step 1 – Create the OCR Engine Instance  

สิ่งแรกที่ทำคือสร้าง `OcrEngine` วัตถุนี้เก็บการตั้งค่าการจดจำและจะใช้ประมวลผลบิตแมพที่ผ่านการเตรียมล่วงหน้า

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image handling
using System;

class PreprocessExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is the core component that will read text.
        OcrEngine ocrEngine = new OcrEngine();

        // ... we’ll continue with loading and preprocessing the image below.
```

**Why?**  
การสร้างเอนจินครั้งเดียวแล้วใช้ซ้ำหลายภาพช่วยลดภาระการทำงาน นอกจากนี้ยังทำให้คุณปรับเปลี่ยนภาษา หรือโหมดการจดจำได้ในภายหลังโดยไม่ต้องสร้าง pipeline ใหม่ทั้งหมด

---

## Step 2 – Load the Source Image  

คุณต้องมีอ็อบเจกต์ `System.Drawing.Image` ที่ชี้ไปยังไฟล์ดิบของคุณ ในโครงการจริงคุณอาจรับสตรีมเข้ามาได้ แต่เพื่อความชัดเจนเราจะอ่านจากดิสก์

```csharp
        // Load the image that requires preprocessing.
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");
```

> **Note:** แทนที่ `YOUR_DIRECTORY` ด้วยพาธโฟลเดอร์จริง หากไฟล์ไม่พบ จะเกิด `FileNotFoundException` — ให้จับข้อยกเว้นนี้หากต้องการจัดการข้อผิดพลาดอย่างอ่อนโยน

---

## Step 3 – Deskew and Rotate the Image  

เอกสารสแกนส่วนใหญ่จะมีการเอียงเล็กน้อย ฟิลเตอร์ `DeskewAndRotate` จะตรวจจับมุมเอียงโดยอัตโนมัติและหมุนภาพให้ตั้งตรง

```csharp
        // Correct orientation – crucial for accurate OCR.
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());
```

**Why does this matter?**  
เอนจิน OCR สมมติว่าบรรทัดข้อความอยู่ในแนวนอน แม้เพียงการเอียง 2 องศาก็อาจทำให้ความแม่นยำลดลง 15‑20 % การทำ Deskew เป็นวิธีที่ง่ายและคุ้มค่าที่สุดในการเพิ่มประสิทธิภาพ

---

## Step 4 – Apply Median Filter to Reduce Image Noise  

สัญญาณรบกวนปรากฏเป็นจุดหรือพิกเซลสุ่ม โดยเฉพาะในภาพที่ถ่ายในแสงน้อย ฟิลเตอร์ median จะทำให้สัญญาณรบกวนเหล่านั้นหายไปในขณะที่คงขอบไว้ ซึ่งเป็นสิ่งที่ต้องการก่อนทำ OCR

```csharp
        // Reduce noise – radius of 2 is a good balance for most photos.
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));
```

**Why a median filter?**  
ต่างจากฟิลเตอร์ค่าเฉลี่ย (mean) ฟิลเตอร์ median จะแทนค่าพิกเซลแต่ละจุดด้วยค่ามีเดียนของเพื่อนบ้าน หมายความว่ารบกวนที่แยกเดี่ยวจะถูกกำจัดโดยไม่ทำให้เส้นข้อความเบลอ—เทคนิคคลาสสิกสำหรับ **reduce image noise**

---

## Step 5 – Enhance Contrast with Stretching  

หลังจากกำจัดสัญญาณรบกวน ขั้นตอนต่อไปคือเพิ่มความแตกต่างระหว่างข้อความและพื้นหลัง การทำ Contrast Stretch จะกระจายความเข้มของพิกเซลให้ครอบคลุมช่วง 0‑255 ทั้งหมด

```csharp
        // Stretch contrast to make dark text pop against a light background.
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());
```

**Why stretch?**  
เอนจิน OCR ต้องการการแยกแยะระหว่างพื้นหน้า‑พื้นหลังที่ชัดเจน หากภาพซีดเกินไป เอนจินอาจตีข้อความว่าเป็นพื้นหลัง การทำ Contrast Stretch แก้ปัญหานี้ได้โดยไม่ต้องตั้งค่า Threshold ด้วยตนเอง

---

## Step 6 – Perform OCR on the Preprocessed Image  

เมื่อภาพตั้งตรง, สะอาด, และคอนทราสต์สูง เราจึงส่งต่อให้เอนจิน OCR ทำงาน

```csharp
        // Recognize the text from the cleaned image.
        string extractedText = ocrEngine.Recognize(processedImage);
```

**What you get:**  
`extractedText` จะมีสตริง Unicode ดิบที่ Aspose.OCR ตรวจจับได้ คุณสามารถทำ post‑process เพิ่มเติม (trim, regex ฯลฯ) ได้ตามต้องการ

---

## Step 7 – Output the Recognized Text  

สุดท้ายให้เขียนผลลัพธ์ลงคอนโซลหรือไฟล์—ตามที่ workflow ของคุณต้องการ

```csharp
        // Show the result in the console.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

### Expected Output

หาก `skewed_photo.jpg` มีข้อความ “Hello World” คุณจะเห็นผลลัพธ์ประมาณนี้:

```
=== Extracted Text ===
Hello World
```

หากภาพยังมีสัญญาณรบกวน คุณอาจเจออักขระผสมกัน—ให้กลับไปที่ Step 4 เพิ่มรัศมีของ median filter หรือทดลองใช้ฟิลเตอร์เพิ่มเติมเช่น `GaussianBlur`

---

## Full Working Example (Copy‑Paste Ready)

ด้านล่างเป็นโปรแกรมทั้งหมดพร้อมคอมไพล์ ไม่ขาดส่วนใด—เพียงแทนที่พาธไฟล์

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class PreprocessExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image that needs preprocessing
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");

        // Step 3: Deskew and rotate the image to correct orientation
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());

        // Step 4: Reduce noise with a median filter (radius = 2)
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));

        // Step 5: Enhance contrast using contrast stretching
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());

        // Step 6: Perform OCR on the preprocessed image
        string extractedText = ocrEngine.Recognize(processedImage);

        // Step 7: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Edge case tip:** หากภาพของคุณมีข้อความสีบนพื้นหลังสี ให้แปลงเป็นระดับสีเทาก่อนทำ `ContrastStretch` คุณทำได้ด้วย `Preprocess.Grayscale()` ใน pipeline

---

## Common Questions & Variations  

### What if the image is upside‑down?  
`DeskewAndRotate` ตรวจจับการหมุน 180 องศาโดยอัตโนมัติ แต่คุณสามารถบังคับให้หมุนด้วย `Preprocess.Rotate(angle: 180)` ก่อนทำ Deskew ได้

### Can I skip the median filter?  
ได้, แต่คุณอาจสูญเสียประโยชน์จาก **reduce image noise** ไป ในสแกนความละเอียดสูง ฟิลเตอร์อาจไม่จำเป็น; แต่ในภาพถ่ายมือถือแสงน้อยมักต้องใช้

### How does this differ from a simple `Apply(Preprocess.Binarize())`?  
Binarization แปลงภาพเป็นสีดำ‑ขาวล้วน ซึ่งอาจทำให้ฟอนต์บางเส้นหายไป วิธีของเรารักษารายละเอียดระดับสีเทาไว้แล้วค่อย Stretch คอนทราสต์—มักให้ผลดีกว่าสำหรับฟอนต์ขนาดผสม

### Is there a way to **apply median filter** only to a region of interest?  
`Apply` ของ Aspose.OCR ทำงานกับบิตแมพทั้งหมด แต่คุณสามารถครอปภาพก่อน (`sourceImage.Clone(new Rectangle(...), sourceImage.PixelFormat)`) แล้วจึงใช้ฟิลเตอร์กับภาพย่อยนั้นได้

---

## Next Steps – Going Beyond Basic Preprocessing  

- **Language Packs:** หากต้องการสกัดอักขระภาษาฝรั่งเศสหรือญี่ปุ่น ให้โหลดโมเดลภาษาที่เหมาะสมผ่าน `ocrEngine.Language = Language.French;`.
- **Custom Thresholding:** สำหรับสแกนที่คอนทราสต์ต่ำมาก ลองใช้ `Preprocess.AdaptiveThreshold()` หลังจาก median filter
- **Batch Processing:** ห่อขั้นตอนทั้งหมดไว้ในลูป `foreach (string file in Directory.GetFiles(...))` แล้วเขียนผลลัพธ์แต่ละไฟล์เป็น `.txt`
- **Performance Tuning:** ใช้ `OcrEngine` ตัวเดียวและจัดสรรบัฟเฟอร์ `Bitmap` ล่วงหน้า เพื่อหลีกเลี่ยงการกระตุ้น GC เมื่อประมวลผลภาพหลายพันรูป

---

## Conclusion  

เราได้แสดงวิธี **preprocess image OCR** ใน C# ตั้งแต่ต้นจนจบ: โหลดภาพ, Deskew, **apply median filter**, เพิ่มคอนทราสต์, และสุดท้าย **extract text image** ด้วย Aspose.OCR โค้ดเต็มพร้อมใช้งานสามารถใส่ลงในโปรเจกต์ใดก็ได้ และคำอธิบายให้คุณเข้าใจ “ทำไม” ของแต่ละการแปลง เพื่อให้คุณปรับพารามิเตอร์ให้เหมาะกับกรณีของตนเอง

ลองใช้กับภาพหลายแบบ ปรับรัศมีของฟิลเตอร์ แล้วดูความแม่นยำของ OCR พุ่งสูงขึ้น เมื่อคุณคุ้นเคยแล้ว ให้สำรวจเทคนิคขั้นสูงที่กล่าวไว้ด้านบน แล้วคุณจะกลายเป็นผู้เชี่ยวชาญด้าน pipeline OCR ที่สะอาดในทีมของคุณ

Happy coding, and may your OCR always read clean! 

![preprocess image OCR example](/images/preprocess-image-ocr.png "preprocess image OCR – before and after processing")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-04-17
description: วิธีแก้ไขการเอียงของภาพอย่างรวดเร็วด้วย Aspose.OCR – เรียนรู้การโหลดภาพ
  OCR, การเตรียมภาพ OCR, และการจดจำข้อความในภาพด้วยความแม่นยำสูง.
draft: false
keywords:
- how to deskew image
- recognize text image
- improve ocr accuracy
- load image ocr
- preprocess image ocr
language: th
og_description: วิธีแก้ไขการเอียงของภาพและปรับปรุงความแม่นยำของ OCR ใน C# เรียนรู้การโหลดภาพ
  OCR, การเตรียมภาพ OCR, และการจดจำข้อความจากภาพด้วย Aspose.OCR.
og_title: วิธีแก้ไขการเอียงของภาพ – คอร์สสอน OCR ด้วย C# อย่างครบถ้วน
tags:
- Aspose.OCR
- C#
- Image Processing
title: วิธีแก้ไขการเอียงของภาพและเพิ่มความแม่นยำของ OCR ใน C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/ocr-optimization/how-to-deskew-image-and-boost-ocr-accuracy-in-c-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการแก้ไขการเอียงของภาพและเพิ่มความแม่นยำของ OCR ใน C#

**How to deskew image** เป็นอุปสรรคทั่วไปเมื่อคุณต้องดึงข้อความจากภาพถ่ายที่ไม่ได้จัดเรียงอย่างสมบูรณ์แบบ ในคู่มือนี้เราจะอธิบายขั้นตอนการโหลดภาพ, การทำพรีโพรเซส, และสุดท้าย **recognize text image** โดยใช้ฟิลเตอร์เชนที่ทรงพลังของ Aspose.OCR

หากคุณเคยใช้กล้องโทรศัพท์ถ่ายใบเสร็จ, ป้าย, หรือแบบฟอร์มสแกนแล้วได้ผลลัพธ์เป็นอักขระบิดเบี้ยวและอ่านไม่ออก คุณคงรู้ว่ามันน่าหงุดหงิดแค่ไหน ข่าวดีคือ เพียงไม่กี่บรรทัดของโค้ด C# ก็สามารถทำให้ภาพตรงขึ้น, กำจัดสัญญาณรบกวน, และให้สตริงที่สะอาดพร้อมใช้งานได้ เราจะพูดถึงวิธี **improve OCR accuracy** ด้วยการปรับขั้นตอนพรีโพรเซสด้วยเช่นกัน

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Core ด้วย)  
- ใบอนุญาตหรือสำเนาประเมินของ **Aspose.OCR** (สามารถดาวน์โหลดได้ผ่าน NuGet)  
- ไฟล์ภาพที่มีการเอียงเล็กน้อยหรือมีสัญญาณรบกวน (เช่น `skewed_photo.png`)  

ไม่ต้องใช้เครื่องมือของบุคคลที่สามที่ซับซ้อน—แค่ไลบรารี Aspose.OCR และความรู้พื้นฐานของ C#  

![ตัวอย่างการแก้ไขการเอียงของภาพ](/images/deskew-demo.png "การแก้ไขการเอียงของภาพ – ดั้งเดิม vs ปรับปรุง")

---

## ขั้นตอนที่ 1 – โหลดภาพ OCR: เตรียมไฟล์ต้นฉบับ

ก่อนที่เราจะทำให้ภาพตรงขึ้น เราต้องนำภาพเข้าสู่หน่วยความจำก่อน วิธี `OcrImage.FromFile` ทำหน้าที่นี้โดยตรง

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image you want to process
var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");
```

> **Why this matters:** การโหลดภาพเป็น `OcrImage` ทำให้เครื่อง OCR เข้าถึงข้อมูลพิกเซลโดยตรง ซึ่งจำเป็นสำหรับขั้นตอน **preprocess image OCR** ถ้าเส้นทางไฟล์ผิดคุณจะเจอ `FileNotFoundException` ดังนั้นตรวจสอบตำแหน่งไฟล์ให้แน่นอน

## ขั้นตอนที่ 2 – พรีโพรเซสภาพ OCR: สร้างฟิลเตอร์เชนสำหรับการแก้ไขการเอียง

ตอนนี้เรามาถึงหัวใจของ **how to deskew image** Aspose.OCR มาพร้อมกับคอลเลกชันฟิลเตอร์ที่คุณสามารถเรียงลำดับได้ตามต้องการ สำหรับภาพถ่ายในโลกจริงส่วนใหญ่คุณอาจต้องการ:

1. **Deskew** – แก้ไขการหมุน  
2. **Denoise** – กำจัดจุดรบกวนแบบเกลือและพริกไทย  
3. **ContrastEnhance** – ทำให้ตัวอักษรที่จางชัดเจนขึ้น  

```csharp
// Create a chain of preprocessing filters
var filterChain = new ImageFilterCollection
{
    new DeskewFilter(),          // Detects and corrects rotation
    new DenoiseFilter(),        // Reduces noise
    new ContrastEnhanceFilter() // Boosts contrast for faint text
};

// Apply the filter chain to obtain a cleaned image
var filteredImage = filterChain.Apply(ocrImage);
```

> **Pro tip:** หากภาพของคุณเปิดแสงได้ดีแล้ว คุณสามารถละ `ContrastEnhanceFilter` ได้ การประมวลผลน้อยลงหมายถึงการทำงานที่เร็วขึ้น

### กรณีขอบ

- **Extreme rotation (>45°):** `DeskewFilter` ทำงานได้ดีที่สุดจนถึงประมาณ 30° หากมุมใหญ่กว่านี้อาจต้องหมุนภาพด้วยตนเองก่อน (`filteredImage.Rotate(…)`)  
- **Colored backgrounds:** แปลงเป็นระดับสีเทาก่อนทำ Denoise เพื่อผลลัพธ์ที่ดีกว่า (`filteredImage = filteredImage.ToGrayscale();`)

## ขั้นตอนที่ 3 – Recognize Text Image: รันเครื่อง OCR

เมื่อมีบิตแมปที่สะอาดและตรงอยู่ในมือแล้ว ถึงเวลาดึงอักขระออกมา

```csharp
// Create an OCR engine instance
using var ocrEngine = new OcrEngine();

// Recognize text from the filtered image
var ocrResult = ocrEngine.Recognize(filteredImage);

// Display the recognized text
Console.WriteLine(ocrResult.Text);
```

> **What’s happening under the hood?** `OcrEngine` ทำงานด้วย recognizer แบบ neural‑network ที่คาดหวังภาพที่อยู่ในแนวตั้งเกือบตรงและคอนทราสต์สูง นั่นคือเหตุผลที่ขั้นตอน **preprocess image OCR** ก่อนหน้านี้สำคัญต่อการ **improve OCR accuracy**

### ผลลัพธ์ที่คาดหวัง

หากภาพต้นฉบับมีข้อความ “Invoice #12345 – Total $89.99” คอนโซลจะพิมพ์อะไรคล้าย ๆ นี้

```
Invoice #12345 – Total $89.99
```

หากคุณเห็นอักขระผิดรูป ให้ตรวจสอบฟิลเตอร์เชนอีกครั้ง — บางทีอาจต้องเพิ่มการ Sharpen (`new SharpenFilter()`)

## ขั้นตอนที่ 4 – ปรับจูนเพื่อเพิ่มความแม่นยำของ OCR

แม้หลังจากทำ Deskew แล้ว OCR ยังอาจสับสนกับฟอนต์บางแบบหรือสแกนความละเอียดต่ำ นี่คือเคล็ดลับเล็ก ๆ ที่ช่วยได้:

| Issue | Fix |
|-------|-----|
| ขนาดฟอนต์เล็ก (<10 pt) | Upscale the image (`filteredImage = filteredImage.Resize(2.0);`) |
| ข้อความสีเทาอ่อนบนพื้นสีขาว | Increase contrast further (`new ContrastEnhanceFilter(1.5)`) |
| ข้อความหลายภาษา | Set `ocrEngine.Language = OcrLanguage.Multilingual;` |

การปรับเหล่านี้ช่วย **improve OCR accuracy** โดยไม่ต้องเปลี่ยนโครงสร้างหลักของโค้ด

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมรันครบถ้วนรวมทุกขั้นตอนที่กล่าวมา คัดลอกไปในโปรเจกต์คอนโซลใหม่และกด **F5**

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Load the image you want to process
        var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");

        // Step 2: Build a chain of preprocessing filters
        var filterChain = new ImageFilterCollection
        {
            new DeskewFilter(),          // Detects and corrects rotation
            new DenoiseFilter(),        // Reduces salt‑and‑pepper noise
            new ContrastEnhanceFilter() // Improves faint characters
        };

        // Step 3: Apply the filter chain to obtain a cleaned image
        var filteredImage = filterChain.Apply(ocrImage);

        // Step 4: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Optional: set language or other engine options here
        // ocrEngine.Language = OcrLanguage.English;

        // Step 5: Recognize text from the filtered image
        var ocrResult = ocrEngine.Recognize(filteredImage);

        // Step 6: Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

รันโปรแกรมแล้วคุณจะเห็นข้อความที่ทำความสะอาดและแก้เอียงแล้วแสดงบนคอนโซล

## คำถามที่พบบ่อย & คำตอบ

**Q: Does this work on PDFs?**  
A: ใช่. แปลงแต่ละหน้า PDF เป็นภาพ (เช่น ใช้ `Aspose.PDF`) แล้วส่งบิตแมปที่ได้เข้าไปในฟิลเตอร์เชนเดียวกัน

**Q: What if my image is already perfectly aligned?**  
A: `DeskewFilter` จะตรวจจับมุมใกล้ศูนย์และปล่อยภาพไว้โดยไม่เปลี่ยนแปลง — ไม่มีผลเสีย

**Q: Can I process multiple images in a batch?**  
A: แน่นอน. ห่อโค้ดด้วยลูป `foreach (var path in Directory.GetFiles(...))` แล้วเก็บ `ocrResult.Text` แต่ละรายการในลิสต์หรือไฟล์

---

## สรุป

เราได้แสดง **how to deskew image** ด้วยโปรแกรม, ผ่านขั้นตอน **load image OCR**, ใช้พายป์ไลน์ **preprocess image OCR** ที่แข็งแรง, และสุดท้าย **recognize text image** ด้วย Aspose.OCR โดยการปรับฟิลเตอร์และอาจเพิ่มการสเกลหรือ Sharpen คุณสามารถ **improve OCR accuracy** สำหรับสถานการณ์จริงหลากหลาย

พร้อมรับความท้าทายต่อไปหรือยัง? ลองนำพายป์ไลน์นี้ไปผสานกับ Web API, หรือทดลองจดจำโน้ตมือเขียนโดยเพิ่ม `new BinarizationFilter()` ก่อน Deskew ความเป็นไปได้ไม่มีที่สิ้นสุด — Happy coding!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
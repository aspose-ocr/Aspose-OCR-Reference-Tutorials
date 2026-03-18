---
category: general
date: 2026-03-18
description: สร้าง PDF ที่ค้นหาได้โดยใช้ Aspose OCR ใน C# แปลงภาพเป็น PDF, เพิ่มชั้นข้อความ
  OCR, และเขียนไบต์ของ PDF ไปยังไฟล์ในไม่กี่ขั้นตอนง่าย ๆ.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: th
og_description: สร้าง PDF ที่ค้นหาได้อย่างรวดเร็วด้วย Aspose OCR ใน C# เรียนรู้วิธีแปลงภาพเป็น
  PDF, เพิ่มชั้นข้อความ OCR, และเขียนไบต์ PDF ลงไฟล์.
og_title: สร้าง PDF ที่ค้นหาได้จากรูปภาพ – คู่มือ OCR C# อย่างรวดเร็ว
tags:
- OCR
- PDF
- C#
- Aspose
title: สร้าง PDF ที่ค้นหาได้จากรูปภาพด้วย OCR – คู่มือ C#
url: /th/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้จากรูปภาพด้วย OCR – คู่มือ C#

เคยต้อง **สร้าง PDF ที่ค้นหาได้** จากรูปสแกนหรือไม่? ด้วย Aspose OCR คุณทำได้ในไม่กี่บรรทัดโดยไม่ต้องพึ่งไลบรารีขนาดใหญ่ ในบทเรียนนี้เราจะ **แปลงรูปภาพเป็น PDF**, ใส่ **ชั้นข้อความ OCR** ด้านบน, และสุดท้าย **เขียนไบต์ของ PDF ลงไฟล์** เพื่อให้ได้เอกสาร PDF/A‑2b ที่เป็นมาตรฐานซึ่งผู้ใช้ของคุณสามารถค้นหาได้จริง

หากคุณสงสัยว่าทำไมต้องสร้าง PDF ที่ค้นหาได้แทนไฟล์รูปภาพธรรมดา ลองคิดถึงประสบการณ์ผู้ใช้: PDF ที่ค้นหาได้ทำให้คนสามารถคัดลอก, เลือก, และทำดัชนีข้อความได้—เหมาะสำหรับคลังข้อมูล, เอกสารกฎหมาย, หรือกระบวนการทำงานใด ๆ ที่ต้องการสกัดข้อความในภายหลัง มาเริ่มกันเลย

## สิ่งที่คุณต้องมี

- .NET 6 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+ ด้วย)
- แพคเกจ Aspose.OCR NuGet (`Aspose.OCR` เวอร์ชัน 23.10 หรือใหม่กว่า)
- รูปภาพ raster (`.png`, `.jpg`, ฯลฯ) ที่คุณต้องการแปลงเป็น PDF ที่ค้นหาได้
- ความรู้พื้นฐานของ C# เพียงเล็กน้อย—ไม่ต้องซับซ้อน

เท่านี้เอง ไม่ต้องใช้เครื่องมือภายนอก ไม่ต้องแปลงไฟล์เพิ่มเติม งานหนักทั้งหมดทำโดยเอนจิน OCR ของ Aspose

## สร้าง PDF ที่ค้นหาได้ – ภาพรวม

ก่อนจะลงลึกในโค้ด เรามาดูขั้นตอนโดยสรุป:

1. **Instantiate** เอนจิน OCR – วัตถุนี้รู้วิธีอ่านข้อความจากรูปภาพ  
2. **Load** ภาพต้นฉบับ – เราจะส่ง `ImageStream` ให้เอนจิน  
3. **Configure** ตัวเลือกการบันทึก PDF/A‑2b – บอก Aspose ให้ฝังข้อความที่จดจำได้เป็นชั้นที่ซ่อนอยู่  
4. **Run** OCR และ **capture** ไบต์ของ PDF ที่ได้  
5. **Write** ไบต์เหล่านั้นลงดิสก์ เพื่อสร้างไฟล์ PDF ที่ค้นหาได้ขั้นสุดท้าย

แต่ละขั้นตอนตรงกับบรรทัดหรือสองบรรทัดของ C# ทำให้กระบวนการทั้งหมดรู้สึกเหมือนสคริปต์เล็ก ๆ ไม่ใช่โครงการขนาดใหญ่

## ขั้นตอนที่ 1: แปลงรูปภาพเป็น PDF – โหลดรูปภาพ

อันดับแรก เราต้องให้เอนจิน OCR มีอะไรให้อ่าน `ImageStream.FromFile` ช่วยโหลดไฟล์เข้าสู่สตรีมที่ Aspose สามารถประมวลผลได้

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **เคล็ดลับ:** ให้ความละเอียดของรูปภาพอยู่ที่ 300 dpi หรือสูงกว่า; ความแม่นยำของ OCR ลดลงอย่างมากเมื่อสแกนความละเอียดต่ำ

## ขั้นตอนที่ 2: จดจำข้อความจากรูปภาพและเพิ่มชั้นข้อความ OCR

ต่อไปเราจะสร้างเอนจิน OCR และบอกให้จดจำข้อความ ผลลัพธ์จะถูกผสานกับ `PdfSaveOptions` ที่มี `IncludeTextLayer = true` ธงนี้บังคับให้ Aspose ฝังอักขระที่สกัดออกมาเป็นชั้นข้อความที่มองไม่เห็น ซึ่งเป็นสิ่งทำให้ PDF สามารถค้นหาได้

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

ทำไมต้องใช้ PDF/A‑2b? มันเป็นรูปแบบมาตรฐาน ISO สำหรับการเก็บรักษาเอกสารระยะยาวและสำคัญสำหรับเรา เพราะบังคับให้ PDF มีชั้นข้อความที่ค้นหาได้ หากคุณไม่ต้องการความสอดคล้องตามมาตรฐานการเก็บรักษา คุณสามารถลบ `PdfCompliance` ออกได้เลย แต่การใส่ไว้ก็ไม่มีค่าใช้จ่ายเพิ่มเติม

## ขั้นตอนที่ 3: เขียนไบต์ของ PDF ลงไฟล์ – บันทึกผลลัพธ์

เมื่อเอนจินพร้อมและตั้งค่าต่าง ๆ แล้ว เราจะรันการจดจำและขอให้ Aspose ส่ง PDF กลับมาเป็น `byte[]` จากนั้นเราก็เขียนไบต์เหล่านั้นลงดิสก์ด้วย `File.WriteAllBytes` ง่าย ๆ แต่ทรงพลัง

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

บรรทัด `Console.WriteLine` นั้นเป็นออปชันเสริม แต่ช่วยให้คุณเห็นผลตอบรับทันทีเมื่อรันโปรแกรมจากเทอร์มินัล

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมที่พร้อมรัน คัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่, แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริง, แล้วกด **F5**

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

- จะมีไฟล์ชื่อ `output.pdf` ปรากฏในโฟลเดอร์ที่คุณระบุ  
- เปิดไฟล์ด้วย Adobe Acrobat Reader หรือโปรแกรมดู PDF ใดก็ได้และลองเลือกข้อความ—ถ้าคุณสามารถคัดลอกคำได้ แสดงว่าคุณ **สร้าง PDF ที่ค้นหาได้** สำเร็จแล้ว  
- เอกสารจะผ่านการตรวจสอบ PDF/A‑2b เนื่องจากเราใช้ธงความสอดคล้องที่ถูกต้อง

## คำถามที่พบบ่อย & กรณีขอบ

**ถ้ารูปภาพของฉันมีหลายหน้า จะทำอย่างไร?**  
ห่อแต่ละหน้าใน `ImageStream` ของตนเองและส่งต่อให้ `OcrEngine` อย่างต่อเนื่อง Aspose จะรวมหน้าต่าง ๆ เข้าด้วยกันเป็น PDF ไฟล์เดียวโดยอัตโนมัติ

**เปลี่ยนภาษาของ OCR ได้หรือไม่?**  
ทำได้เลย ตั้งค่า `ocrEngine.Language = Language.English;` (หรือภาษาที่รองรับอื่น) ก่อนเรียก `Recognize`

**เรื่องการใช้หน่วยความจำสำหรับไฟล์ขนาดใหญ่ล่ะ?**  
ถ้าคุณประมวลผลสแกนขนาดกิกะไบต์ ควรสตรีมผลลัพธ์โดยตรงไปยัง `FileStream` แทนการเก็บ `byte[]` ทั้งหมดในหน่วยความจำ:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**ต้องมีลิขสิทธิ์หรือไม่?**  
Aspose มีรุ่นทดลองฟรีไม่มีลายน้ำ สำหรับการใช้งานในผลิตภัณฑ์จริง ควรซื้อไลเซนส์เพื่อเอาแบนเนอร์การทดลองออกและเปิดฟีเจอร์เต็ม

## เคล็ดลับเพื่อเพิ่มความแม่นยำของ OCR

- **Pre‑process** รูปภาพ: แก้ไขการเอียง, กำจัดจุดรบกวน, และเพิ่มคอนทราสต์  
- **ใช้รูปแบบที่ไม่สูญเสียคุณภาพ** เช่น PNG; ศิลปะแบบ JPEG อาจทำให้เอนจินสับสน  
- **หลีกเลี่ยงพื้นหลังสี**; พื้นหลังสีขาวเรียบจะให้ผลดีที่สุด

## ขั้นตอนต่อไป

เมื่อคุณสามารถ **สร้าง PDF ที่ค้นหาได้** แล้ว คุณอาจต้องการ:

- **ประมวลผลเป็นชุด** โฟลเดอร์ของรูปภาพด้วย `Directory.GetFiles`  
- **สกัดข้อความที่ซ่อนอยู่** ภายหลังด้วย API ของ `PdfDocument` เพื่อทำดัชนี  
- **ผสาน OCR กับลายเซ็นดิจิทัล** เพื่อสร้างคลังข้อมูลที่ตรวจสอบการดัดแปลงได้  

ทั้งหมดนี้อิงตามรูปแบบหลักที่เราได้อธิบายไว้: โหลด, จดจำ, ตั้งค่า, บันทึก

---

*พร้อมที่จะเปลี่ยนคลังสแกนของคุณให้เป็น PDF ที่ค้นหาได้หรือยัง? ดึงโค้ดมาใช้, ชี้ไปที่รูปภาพของคุณ, แล้วให้ Aspose ทำงานหนักให้คุณ. Happy coding!*

![สร้างตัวอย่าง PDF ที่ค้นหาได้](/images/create-searchable-pdf.png "ภาพประกอบของ PDF ที่ค้นหาได้ที่สร้างจากรูปภาพ")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
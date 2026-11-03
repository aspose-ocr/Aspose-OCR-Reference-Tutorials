---
category: general
date: 2026-04-04
description: สร้าง PDF ที่ค้นหาได้จากภาพ TIF ด้วย C# – เรียนรู้วิธีแปลงภาพเป็น PDF,
  เพิ่มเมตาดาต้า PDF, และสร้างเอกสารที่ค้นหาได้โดยใช้ Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: th
og_description: สร้าง PDF ที่สามารถค้นหาได้จากไฟล์ TIF ด้วย C# แปลงภาพเป็น PDF เพิ่มเมตาดาต้า
  PDF และสร้างเอกสารที่สามารถค้นหาได้โดยใช้ Aspose.OCR
og_title: สร้าง PDF ที่ค้นหาได้จากไฟล์ TIF – คู่มือขั้นตอนโดยละเอียด
tags:
- Aspose.OCR
- C#
- PDF generation
title: สร้าง PDF ที่ค้นหาได้จาก TIF – แปลงภาพเป็น PDF, เพิ่มเมตาดาต้า PDF
url: /th/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้จากไฟล์ TIF – คู่มือเต็ม C#

เคยต้อง **สร้าง PDF ที่สามารถค้นหาได้** จากใบแจ้งหนี้ที่สแกนแล้วแต่ไม่แน่ใจว่าจะทำให้ข้อความค้นหาได้และเมตาดาต้าไฟล์เป็นระเบียบอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการอัตโนมัติ PDF ต้องเป็นทั้งแบบเครื่องอ่านได้และมีการแท็กข้อมูลอย่างชื่อเรื่อง, ผู้เขียน, และเกณฑ์ความเชื่อมั่นอย่างเหมาะสม  

ในคู่มือนี้เราจะเดินผ่านโซลูชันครบวงจรที่ **แปลงภาพเป็น PDF**, แทรก **เมตาดาต้า PDF**, และกรองผลลัพธ์ OCR ที่ความเชื่อมั่นต่ำ—ทั้งหมดด้วยไลบรารี Aspose.OCR. เมื่อเสร็จคุณจะได้สแนปช็อตที่พร้อมใช้งานซึ่งสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้ พร้อมกับเคล็ดลับหลายอย่างสำหรับการจัดการกรณีขอบ.

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานบน .NET Framework 4.6+ ด้วย)  
- แพคเกจ NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- ไฟล์ภาพ TIF ที่ต้องการแปลงเป็น PDF ที่ค้นหาได้ (เช่น `input.tif`)  
- ความคุ้นเคยพื้นฐานกับ C# และ Visual Studio (หรือ IDE ที่คุณชื่นชอบ)

ไม่ต้องใช้บริการภายนอกอื่นใด—กระบวนการทั้งหมดทำงานแบบออฟไลน์บนเครื่องของคุณ.

## ขั้นตอนที่ 1 – ตั้งค่า OCR Engine (Create Searchable PDF Core)

สิ่งแรกที่เราต้องการคืออินสแตนซ์ `OcrEngine` ที่รู้ว่าจะจดจำภาษาอะไร ในกรณีส่วนใหญ่ของธุรกิจภาษาอังกฤษก็เพียงพอ, แต่คุณสามารถสลับ `Language.English` เป็นภาษาอื่นที่รองรับได้.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**ทำไมจึงสำคัญ:** OCR engine ทำหน้าที่แปลงพิกเซลแบบแรสเตอร์เป็นข้อความ Unicode. การตั้งค่าภาษาอย่างถูกต้องช่วยเพิ่มความแม่นยำและลดจำนวนคำที่ความเชื่อมั่นต่ำซึ่งจะถูกกรองออกในขั้นตอนต่อไป.

> **เคล็ดลับ:** หากคุณต้องประมวลผลเอกสารหลายภาษา, ให้สร้างหลาย engine หรือใช้ `Language.Multilingual` เพื่อให้ Aspose ตรวจจับภาษาโดยอัตโนมัติ.

## ขั้นตอนที่ 2 – โหลดภาพ TIF (Create PDF from TIF)

ต่อไปเราชี้ engine ไปที่ไฟล์ต้นฉบับ. ตัวช่วย `ImageStream.FromFile` จะอ่านภาพเข้าสู่สตรีมที่ OCR engine สามารถใช้ได้.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

คุณอาจสงสัย, *“ฉันสามารถใส่ JPEG หรือ PNG แทนได้ไหม?”* แน่นอน—Aspose.OCR รองรับรูปแบบแรสเตอร์ส่วนใหญ่ เพียงเปลี่ยนนามสกุลไฟล์และคุณก็พร้อมใช้งาน.

## ขั้นตอนที่ 3 – ตั้งค่า PDF Options (Add Metadata to PDF)

ก่อนทำการแปลง เราต้องสร้างอ็อบเจกต์ `PdfOptions`. ที่นี่เราจะ **เพิ่มเมตาดาต้า PDF** เช่น ชื่อเรื่องและผู้เขียน, และยังบอก engine ให้ละเว้นคำที่ความเชื่อมั่นต่ำกว่าค่าที่กำหนด.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**กำลังทำอะไรอยู่?**  
- `Title` และ `Author` จะกลายเป็นส่วนหนึ่งของพจนานุกรมข้อมูลเอกสาร PDF, ทำให้ไฟล์ง่ายต่อการทำดัชนีในระบบจัดการเอกสาร.  
- `MinConfidence` เป็นเกณฑ์คัดกรอง: OCR มักอ่านอักขระที่จางผิด; การกรองคำเหล่านี้ช่วยให้ชั้นข้อความที่ค้นหาได้สะอาดและทำให้การสกัดข้อความต่อไปแม่นยำขึ้น.

หากต้องการเมตาดาต้าพิเศษ (เช่น `Subject`, `Keywords`) คุณสามารถตั้งค่าได้ผ่าน `PdfOptions.CustomProperties`.

## ขั้นตอนที่ 4 – แปลงภาพเป็น PDF ที่ค้นหาได้ (Convert Image to PDF)

เมื่อ engine พร้อมและตั้งค่า options แล้ว คำสั่งสุดท้ายจะทำการแปลง. มันจะเขียน PDF ที่ค้นหาได้ลงดิสก์, ฝังชั้นข้อความ OCR ไว้ใต้ภาพต้นฉบับ.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

หลังจากบรรทัดนี้ทำงานเสร็จ, `output.pdf` จะมี:
- ภาพ TIF ดั้งเดิมเป็นพื้นหลังแบบภาพ  
- ชั้นข้อความที่มองไม่เห็นซึ่งเครื่องมือค้นหาและการคัดลอก‑วางสามารถอ่านได้  
- เมตาดาต้าที่เรากำหนดไว้ก่อนหน้า (ชื่อเรื่อง, ผู้เขียน, ฯลฯ)

### ผลลัพธ์ที่คาดหวัง

เปิด PDF ที่สร้างขึ้นใน Adobe Reader หรือโปรแกรมดู PDF ใดก็ได้และลองเลือกข้อความ. คุณควรจะสามารถคัดลอกประโยคที่ตรงกับสแกนต้นฉบับได้. กล่องโต้ตอบ **Properties** ของเอกสารจะแสดงชื่อเรื่อง “Invoice #12345” และผู้เขียน “MyCompany”.

## ขั้นตอนที่ 5 – ตรวจสอบการกรองความเชื่อมั่น (Why MinConfidence Helps)

เป็นประโยชน์ที่จะยืนยันว่าคำที่ความเชื่อมั่นต่ำถูกลบจริงหรือไม่. คุณสามารถตรวจสอบข้อความซ่อนใน PDF ด้วยเครื่องมืออย่าง `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

หากคำไม่ปรากฏ, ตัวกรอง `MinConfidence` ทำงานตามที่ตั้งค่าไว้. ปรับค่าเกณฑ์ (เช่น `0.7f`) หากต้องการกรองอย่างเข้มข้นหรืออ่อนโยนกว่า.

## ขั้นตอนที่ 6 – จัดการหลายหน้า (Create Searchable PDF from Multi‑Page TIF)

ใบแจ้งหนี้หลายฉบับมักเป็นไฟล์ TIFF หลายหน้า. Aspose.OCR จะถือแต่ละเฟรมเป็นหน้าแยกโดยอัตโนมัติ. เพียงชี้ engine ไปที่ไฟล์หลายหน้า; คำสั่ง `ConvertToSearchablePdf` เดียวกันจะสร้าง PDF ที่ค้นหาได้หลายหน้า.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**กรณีขอบ:** หากหน้าว่าง, OCR อาจยังสร้างชั้นข้อความว่างเปล่า ซึ่งไม่มีผลเสีย. อย่างไรก็ตามคุณสามารถข้ามหน้าว่างได้โดยตรวจสอบ `ocrEngine.HasText` ก่อนทำการแปลง.

## ขั้นตอนที่ 7 – รวมตัวอย่างเต็ม (All Steps Together)

ด้านล่างเป็นโปรแกรมเดียวที่พร้อมรันซึ่งรวมทุกขั้นตอนเข้าด้วยกัน. แทนที่ `YOUR_DIRECTORY` ด้วยพาธโฟลเดอร์จริงบนเครื่องของคุณ.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

เรียกใช้โปรแกรม (`dotnet run` หรือกด **F5** ใน Visual Studio) แล้วคุณจะเห็นข้อความยืนยัน. PDF ที่สร้างขึ้นจะอยู่ข้างไฟล์ภาพต้นฉบับ, พร้อมสำหรับการทำดัชนีหรือการจัดเก็บถาวร.

## คำถามที่พบบ่อย & สิ่งที่ควรระวัง

| คำถาม | คำตอบ |
|----------|--------|
| **ฉันสามารถเพิ่มฟอนต์กำหนดเองให้ชั้นที่ค้นหาได้หรือไม่?** | ชั้น OCR ใช้ Unicode; ลักษณะการแสดงผลถูกกำหนดโดยภาพพื้นฐาน, ดังนั้นไม่จำเป็นต้องฝังฟอนต์เพิ่มเติม. |
| **ถ้า TIF ของฉันเป็นสีล่ะ?** | Aspose.OCR จะเปลี่ยนภาพสีเป็นระดับสีเทาอัตโนมัติสำหรับ OCR, แต่คุณสามารถคงสีเดิมใน PDF ได้โดยตั้งค่า `PdfOptions.PreserveColor = true`. |
| **ไลบรารีนี้ปลอดภัยต่อการทำงานหลายเธรดหรือไม่?** | แต่ละอินสแตนซ์ `OcrEngine` ควรใช้โดยเธรดเดียว. หากต้องการประมวลผลแบบขนาน, สร้าง engine แยกสำหรับแต่ละเธรด. |
| **ฉันจะเข้ารหัส PDF อย่างไร?** | ใช้ `PdfOptions.Security` เพื่อตั้งรหัสผ่านและสิทธิ์หลังจากการแปลง OCR. |

## ขั้นตอนต่อไป (Expand Your PDF Toolkit)

- **ประมวลผลเป็นชุด:** วนลูปโฟลเดอร์ของ TIFF และสร้าง PDF ที่ค้นหาได้สำหรับแต่ละไฟล์.  
- **หลังการแปลง:** ใช้ Aspose.PDF เพื่อรวม PDF ที่สร้างขึ้นเป็นเอกสารหลักเดียว.  
- **เมตาดาต้าขั้นสูง:** เติมฟิลด์ XMP ที่กำหนดเองเพื่อการผสานที่ดีกับ SharePoint หรือระบบ ECM.  

ทั้งหมดนี้ต่อยอดจากรูปแบบหลักที่เราได้อธิบาย: **สร้าง PDF ที่ค้นหาได้**, **แปลงภาพเป็น PDF**, และ **เพิ่มเมตาดาต้า PDF**.

---

*ขอให้สนุกกับการเขียนโค้ด! หากเจอปัญหาใด ๆ, แสดงความคิดเห็นด้านล่างหรือดูเอกสาร Aspose.OCR สำหรับการอัปเดต API ล่าสุด.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
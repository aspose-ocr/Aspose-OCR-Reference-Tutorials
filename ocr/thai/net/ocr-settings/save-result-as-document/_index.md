---
description: เรียนรู้วิธีบันทึกผลลัพธ์ OCR ด้วย Aspose.OCR สำหรับ .NET – แปลงภาพเป็น
  PDF, ดึงข้อความจาก PNG, และบันทึกข้อความที่จดจำได้เป็น DOCX, TXT, PDF หรือ XLSX.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: วิธีบันทึกผล OCR เป็นเอกสาร
url: /th/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีบันทึกผลลัพธ์ OCR เป็นเอกสาร

## บทนำ

ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีบันทึก OCR** โดยใช้ Aspose.OCR สำหรับ .NET เราจะอธิบายขั้นตอนการจดจำข้อความในภาพ แล้วแปลงข้อความนั้นเป็นรูปแบบเอกสารที่นิยม เช่น DOCX, TXT, PDF และ XLSX เมื่อเสร็จสิ้นคุณจะสามารถอัตโนมัติการสกัดข้อมูลจากรูปภาพและเก็บเป็นไฟล์ที่ค้นหาได้และแก้ไขได้—เหมาะสำหรับการเก็บถาวร การรายงาน หรือการประมวลผลต่อไป

## คำตอบสั้น
- **“วิธีบันทึก ocr” หมายถึงอะไร?** หมายถึงการบันทึกข้อความที่จดจำจากภาพลงในรูปแบบไฟล์ เช่น DOCX, PDF ฯลฯ  
- **รูปแบบใดบ้างที่ฉันสามารถส่งออกได้?** รองรับ DOCX, TXT, PDF และ XLSX โดยไม่ต้องตั้งค่าเพิ่มเติม  
- **ฉันต้องมีลิขสิทธิ์หรือไม่?** รุ่นทดลองใช้งานฟรีสำหรับการประเมินผล; ต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **ฉันสามารถแปลงภาพเป็น PDF โดยตรงได้หรือไม่?** ได้—บันทึกผลลัพธ์ OCR เป็น PDF เพื่อให้ได้เอกสาร PDF ที่ค้นหาได้  
- **รองรับ PNG หรือไม่?** แน่นอน; คุณสามารถ **สกัดข้อความจากภาพ PNG** ด้วย API เดียวกัน  

## OCR คืออะไรและทำไมต้องบันทึกผลลัพธ์เป็นเอกสาร?

Optical Character Recognition (OCR) แปลงข้อความที่พิมพ์หรือเขียนด้วยมือในภาพให้เป็นสตริงที่เครื่องคอมพิวเตอร์อ่านได้ การบันทึกสตริงเหล่านั้นเป็นเอกสารทำให้คุณสามารถ:

* สร้าง PDF ที่ค้นหาได้สำหรับการปฏิบัติตามข้อกำหนด  
* เติมข้อมูลในสเปรดชีต (XLSX) เพื่อการวิเคราะห์ข้อมูล  
* สร้างรายงานที่แก้ไขได้ (DOCX)  
* เก็บบันทึกข้อความธรรมดา (TXT) เพื่อการค้นหาอย่างรวดเร็ว  

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มต้น ตรวจสอบว่าคุณมี:

- Aspose.OCR สำหรับ .NET ติดตั้งแล้ว คุณสามารถดาวน์โหลดได้ **[ที่นี่](https://releases.aspose.com/ocr/net/)**.  
- โฟลเดอร์บนเครื่องของคุณที่จะเก็บรูปภาพต้นฉบับและเอกสารผลลัพธ์ ปรับค่า `dataDir` ในโค้ดให้ชี้ไปยังโฟลเดอร์นี้  

## นำเข้า Namespaces

เราต้องการ .NET namespaces บางส่วนเพื่อเข้าถึงการทำงานไฟล์ I/O และคลาสของ Aspose OCR  

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### ขั้นตอนที่ 1: เริ่มต้น Aspose.OCR

ตั้งค่าเส้นทางไปยังไดเรกทอรีทำงานของคุณและสร้างอินสแตนซ์ของเครื่อง OCR  

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### ขั้นตอนที่ 2: จดจำภาพ

ส่งไฟล์ภาพ (เช่น PNG) ไปยังตัวจดจำ นี่คือขั้นตอนที่เราจะ **จดจำข้อความในภาพ** และแปลงเป็น `RecognitionResult`  

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### ขั้นตอนที่ 3: บันทึกผลลัพธ์ในรูปแบบต่าง ๆ

ตอนนี้เราจะส่งออกข้อความที่จดจำ เลือกรูปแบบที่เหมาะกับกระบวนการทำงานของคุณ—ไม่ว่าจะต้อง **แปลงภาพเป็น PDF**, **สกัดข้อความจาก PNG**, หรือสร้างสเปรดชีต  

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### ขั้นตอนที่ 4: แสดงข้อความสำเร็จ

ข้อความคอนโซลง่าย ๆ จะยืนยันว่ากระบวนการเสร็จสมบูรณ์โดยไม่มีข้อผิดพลาด  

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## ข้อผิดพลาดทั่วไปและเคล็ดลับ

- **เส้นทางไฟล์:** ควรใช้เส้นทางแบบเต็มเสมอ หรือให้แน่ใจว่า `dataDir` ลงท้ายด้วยตัวคั่นเส้นทาง (`\` หรือ `/`).  
- **คุณภาพภาพ:** ภาพความละเอียดสูงช่วยเพิ่มความแม่นยำ; พิจารณาการทำก่อนประมวลผล (deskew, denoise) เพื่อผลลัพธ์ที่ดีกว่า  
- **โหมดลิขสิทธิ์:** ในโหมดประเมินผลผลลัพธ์อาจมีลายน้ำ; ใช้ลิขสิทธิ์ที่ถูกต้องเพื่อกำจัดลายน้ำ  

## คำถามที่พบบ่อย

**Q1. Aspose.OCR รองรับรูปแบบภาพต่าง ๆ หรือไม่?**  
A1: ใช่, Aspose.OCR รองรับรูปแบบภาพหลายประเภท ทำให้คุณมีความยืดหยุ่นในการทำ OCR  

**Q2: ฉันสามารถปรับแต่งการตั้งค่าการจดจำเพื่อความแม่นยำที่ดีกว่าได้หรือไม่?**  
A2: แน่นอน! Aspose.OCR มี `RecognitionSettings` ให้ปรับจูนกระบวนการ OCR ตามความต้องการของคุณ  

**Q3: มีรุ่นทดลองใช้งานฟรีหรือไม่?**  
A3: มี, คุณสามารถเริ่มต้นด้วยรุ่นทดลองฟรี **[ที่นี่](https://releases.aspose.com/)**  

**Q4: ฉันจะขอรับลิขสิทธิ์ชั่วคราวสำหรับ Aspose.OCR ได้อย่างไร?**  
A4: สามารถขอรับลิขสิทธิ์ชั่วคราวได้ **[ที่นี่](https://purchase.aspose.com/temporary-license/)**  

**Q5: ฉันจะหาความช่วยเหลือหรือเชื่อมต่อกับชุมชนได้จากที่ไหน?**  
A5: เข้าร่วมชุมชน Aspose.OCR ที่ **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** เพื่อรับการสนับสนุนและการสนทนา  

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
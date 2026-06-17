---
category: general
date: 2026-04-01
description: วิธีแปลงผลลัพธ์ OCR เป็น JSON และ XML ใน C# – เรียนรู้การดึงข้อความจากภาพและเขียนไฟล์
  JSON ด้วย C# โดยใช้ Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: th
og_description: วิธีแปลงผล OCR ให้เป็นไฟล์ JSON และ XML ที่มีโครงสร้างด้วย C# คู่มือขั้นตอนต่อขั้นตอนในการดึงข้อความจากภาพและเขียนไฟล์
  JSON ด้วย C#
og_title: วิธีแปลง OCR เป็น JSON และ XML ใน C# – เขียนไฟล์ JSON
tags:
- OCR
- C#
- Aspose
title: วิธีแปลง OCR เป็น JSON และ XML ใน C# – เขียนไฟล์ JSON
url: /th/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแปลง OCR เป็น JSON & XML ด้วย C# – เขียนไฟล์ JSON

**วิธีแปลงผลลัพธ์ OCR** ให้เป็นสิ่งที่คุณสามารถใช้งานได้จริงเป็นคำถามที่นักพัฒนาหลายคนถามกัน ในคู่มือนี้เราจะสาธิตวิธีดึงข้อความจากรูปภาพ, แปลงผลลัพธ์ OCR ให้เป็น JSON และ XML ที่จัดรูปแบบสวยงาม, แล้วเขียนไฟล์เหล่านั้นลงดิสก์ด้วย C#  

ถ้าคุณเคยมองที่สตริง OCR ดิบแล้วคิดว่า “ต้องมีวิธีที่ดีกว่าในการเก็บข้อมูลนี้” คุณมาถูกที่แล้ว เมื่อจบบทความคุณจะได้โปรแกรมที่ทำงานได้เต็มรูปแบบ ไม่เพียง **ดึงข้อความจากไฟล์รูปภาพ** เท่านั้น แต่ยังรู้วิธี **เขียนไฟล์ JSON ด้วย C#** และ **เขียนไฟล์ XML ด้วย C#** อย่างง่ายดาย

## สิ่งที่คุณต้องเตรียม

- **.NET 6.0** หรือเวอร์ชันใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+ ด้วย)  
- แพคเกจ NuGet **Aspose.OCR** – ติดตั้งด้วยคำสั่ง `dotnet add package Aspose.OCR`  
- รูปภาพที่มีข้อความ (เช่น `invoice.png`)  
- IDE ใดก็ได้ที่คุณชอบ – Visual Studio, Rider หรือ VS Code ก็ใช้ได้  

> **เคล็ดลับ:** เก็บไฟล์รูปภาพไว้ในโฟลเดอร์เฉพาะ (เช่น `Resources/`) เพื่อให้เส้นทางไฟล์เป็นระเบียบ

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine – วิธีแปลง OCR

ก่อนอื่นเราจะสร้างอินสแตนซ์ของ `OcrEngine` และบอกภาษาที่ต้องการตรวจจับ ในหลายกรณีภาษาอังกฤษก็เพียงพอ แต่คุณสามารถสลับ `Language.English` เป็นภาษาอื่นที่รองรับได้

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **ทำไมจึงสำคัญ:** การเริ่มต้น engine ด้วยภาษาที่ถูกต้องช่วยเพิ่มความแม่นยำอย่างมาก โดยเฉพาะกับสคริปต์ที่ไม่ใช่ละติน

## ขั้นตอนที่ 2: จดจำข้อความ – ดึงข้อความจากรูปภาพ

ต่อไปเราจะส่งรูปภาพให้ engine วิธี `Recognize` จะคืนค่าเป็นอ็อบเจกต์ `OcrResult` ที่บรรจุข้อความดิบและข้อมูลตำแหน่ง

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

หากไม่พบไฟล์รูปภาพ `Recognize` จะโยน `FileNotFoundException` เพื่อความเรียบง่ายของตัวอย่าง เราจะสมมติว่าเส้นทางไฟล์ถูกต้อง แต่ในงานจริงคุณควรห่อด้วย `try‑catch`  

## ขั้นตอนที่ 3: แปลงผลลัพธ์เป็น JSON – เขียนไฟล์ JSON C#

Aspose.OCR ทำการซีเรียลไลซ์ได้ง่ายมาก วิธี `ToJson` รับพารามิเตอร์ `indent` เพื่อสร้างผลลัพธ์ที่จัดรูปแบบสวยงาม เหมาะกับการเปิดในโปรแกรมแก้ไขข้อความ

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### ตัวอย่าง JSON ที่คาดหวัง

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **วิธีดึงข้อความ:** คุณสามารถใช้คุณสมบัติ `Text` เพื่อรับสตริงธรรมดาที่นำไปใช้กับบริการอื่น ๆ (เช่น ดัชนีการค้นหา, ฐานข้อมูล ฯลฯ)

## ขั้นตอนที่ 4: บันทึก JSON – เขียนไฟล์ JSON C# (ต่อ)

เมื่อได้สตริง JSON แล้ว เราก็เขียนลงไฟล์ด้วย `File.WriteAllText` ซึ่งโดยค่าเริ่มต้นจะใช้การเข้ารหัส UTF‑8

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

ตอนนี้คุณจะมีไฟล์ `invoice.json` อยู่ข้าง ๆ รูปภาพ พร้อมสำหรับการประมวลผลต่อไป

## ขั้นตอนที่ 5: แปลงผลลัพธ์เป็น XML – เขียนไฟล์ XML C#

หากคุณต้องการ XML สำหรับระบบเก่า วิธี `ToXml` จะทำหน้าที่เดียวกันเช่นเดียวกับ `ToJson` และยังรองรับการจัดรูปแบบสวยงามอีกด้วย

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### ตัวอย่าง XML ที่คาดหวัง

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## ขั้นตอนที่ 6: บันทึก XML – เขียนไฟล์ XML C# (ต่อ)

การบันทึก XML ทำได้เช่นเดียวกับขั้นตอน JSON เพียงเปลี่ยนนามสกุลเป็น `.xml`

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### ตัวอย่างโปรแกรมทำงานเต็มรูปแบบ

รวมทุกขั้นตอนเข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอกไปวางในแอปคอนโซลได้

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

รันโปรแกรมแล้วคุณจะพบไฟล์ใหม่สองไฟล์ – `invoice.json` และ `invoice.xml` – อยู่ในตำแหน่งที่คุณระบุ เปิดไฟล์เหล่านั้นเพื่อยืนยันโครงสร้างตรงกับตัวอย่างข้างต้น

## คำถามที่พบบ่อย & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ถ้ารูปภาพมีหลายภาษา จะทำอย่างไร?** | สร้างอินสแตนซ์ `OcrEngine` แยกสำหรับแต่ละภาษา หรือใช้ `Language.Multi` หากรองรับ |
| **สามารถควบคุมรูปแบบผลลัพธ์ (เช่น ไม่รวมข้อมูลตำแหน่ง) ได้หรือไม่?** | ได้ ทั้ง `ToJson` และ `ToXml` มีพารามิเตอร์เลือกกรองฟิลด์; ดูเอกสาร Aspose.OCR สำหรับ `ExportOptions` |
| **จะจัดการกับ PDF ขนาดใหญ่ที่มีหลายหน้าอย่างไร?** | ประมวลผลแต่ละหน้าแยกกัน แล้วรวมผลลัพธ์ก่อนทำการซีเรียลไลซ์ |
| **ผลลัพธ์ปลอดภัยต่อ UTF‑8 หรือไม่?** | แน่นอน – Aspose.OCR ใช้ Unicode ภายใน และ `File.WriteAllText` เขียนเป็น UTF‑8 โดยค่าเริ่มต้น |
| **เรื่องประสิทธิภาพล่ะ?** | OCR ใช้ CPU มาก สำหรับงานแบบแบตช์ควรพิจารณา parallel processing หรือใช้ Aspose Cloud API |

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีแปลงผลลัพธ์ OCR** ให้เป็นทั้ง JSON และ XML ด้วย C# โดยทำตามขั้นตอนข้างต้นคุณสามารถ **ดึงข้อความจากรูปภาพ**, แล้ว **เขียนไฟล์ JSON ด้วย C#** และ **เขียนไฟล์ XML ด้วย C#** เพียงไม่กี่บรรทัด วิธีนี้เร็ว, เชื่อถือได้, และทำงานกับรูปภาพทุกประเภทที่ Aspose.OCR รองรับ  

พร้อมรับความท้าทายต่อไปหรือยัง? ลองนำผลลัพธ์ไปใช้ต่อในโครงการของคุณ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
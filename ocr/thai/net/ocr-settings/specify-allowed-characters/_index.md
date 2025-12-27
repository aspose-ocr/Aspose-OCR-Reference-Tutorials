---
date: 2025-12-27
description: เรียนรู้วิธีใช้การแปลงภาพ OCR เป็นข้อความด้วย Aspose.OCR สำหรับ .NET
  โดยระบุอักขระที่อนุญาตและปรับแต่งการตั้งค่าการจดจำ OCR อย่างละเอียด รวมถึงโค้ดสำหรับการจดจำภาพตัวเลข
linktitle: 'ocr image to text: Specify Allowed Characters in OCR'
second_title: Aspose.OCR .NET API
title: 'OCR ภาพเป็นข้อความ: ระบุอักขระที่อนุญาตใน OCR'
url: /th/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to text: ระบุอักขระที่อนุญาตใน OCR

## Introduction

ในยุคที่เทคโนโลยีพัฒนาอย่างต่อเนื่อง การจดจำอักขระด้วยแสง (Optical Character Recognition - OCR) – หรือการแปลง **ocr image to text** – ได้กลายเป็นเครื่องมือที่เปลี่ยนแปลงวิธีการทำงานของเครื่องจักรให้สามารถเข้าใจข้อความจากภาพได้ Aspose.OCR สำหรับ .NET โดดเด่นในฐานะโซลูชันที่ทรงพลัง ให้การบูรณาการที่ไร้รอยต่อสำหรับนักพัฒนาที่ต้องการความสามารถ OCR ที่แข็งแกร่งในแอปพลิเคชัน .NET ของตน

## Quick Answers
- **“Specify Allowed Characters” ทำอะไร?** มันจำกัดผลลัพธ์ของ OCR ให้เป็นชุดสัญลักษณ์ที่กำหนดไว้ เช่น เฉพาะตัวเลขเท่านั้น  
- **เมธอดใดที่ดึงบรรทัดเดียวของข้อความ?** `RecognizeLine` จะคืนค่าบรรทัดแรกที่ตรวจพบ  
- **ฉันสามารถเปลี่ยนการตั้งค่า OCR ระหว่างการทำงานได้หรือไม่?** ได้ – ใช้ `RecognitionSettings` เพื่อปรับตัวเลือกเช่น `AllowedCharacters`  
- **มีรุ่นทดลองหรือไม่?** มีแน่นอน ดาวน์โหลดรุ่นทดลองฟรีจากเว็บไซต์ Aspose  
- **รองรับเวอร์ชัน .NET ใดบ้าง?** รองรับ .NET Framework สมัยใหม่ทั้งหมด รวมถึง .NET Core/5/6

## Prerequisites

ก่อนเริ่มทำตามบทเรียน โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้พร้อมอยู่แล้ว:

- ความรู้พื้นฐานในการพัฒนา .NET  
- ไลบรารี Aspose.OCR สำหรับ .NET คุณสามารถดาวน์โหลดได้จาก [ที่นี่](https://releases.aspose.com/ocr/net/)  
- ความคุ้นเคยกับ Visual Studio หรือสภาพแวดล้อมการพัฒนา .NET ที่คุณชื่นชอบ

## Import Namespaces

ในโครงการ .NET ของคุณ ให้นำเข้า namespace ที่จำเป็นเพื่อใช้ฟังก์ชันของ Aspose.OCR สำหรับ .NET อย่างเต็มประสิทธิภาพ:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

ตอนนี้เราจะแบ่งขั้นตอนการสอนออกเป็นชุดของขั้นตอนที่ครอบคลุม:

## Step 1: Specify Allowed Characters in ocr image to text

เพื่อเริ่มต้น ตั้งค่าพาธไปยังไดเรกทอรีเอกสารของคุณ:

```csharp
string dataDir = "Your Document Directory";
```

## Step 2: Initialize Aspose.OCR with Allowed Symbols (recognize digits image)

สร้างอินสแตนซ์ของ `AsposeOcr` โดยระบุสัญลักษณ์ที่อนุญาต ในกรณีนี้เราจะอนุญาตเฉพาะตัวเลข (0‑9) เท่านั้น:

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Step 3: Recognize Image

ใช้อินสแตนซ์ `AsposeOcr` เพื่อจดจำข้อความจากภาพ:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Step 4: Display Recognized Text

พิมพ์ข้อความที่จดจำได้ลงคอนโซล:

```csharp
Console.WriteLine(result);
```

## Step 5: Second Case – Recognize Image with Specific OCR Recognition Settings

สร้างอินสแตนซ์ `AsposeOcr` อีกหนึ่งตัว โดยใช้การตั้งค่าที่เจาะจงมากขึ้นเพื่อสาธิตการใช้ **ocr recognition settings**:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Step 6: Display Second Case Recognized Text

พิมพ์ข้อความที่จดจำได้จากกรณีที่สองลงคอนโซล:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Step 7: Successful Execution

สุดท้าย ยืนยันว่าการทำงานของบทเรียน **SpecifyAllowedCharacters** สำเร็จเรียบร้อย:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

โดยทำตามขั้นตอนเหล่านี้ คุณได้เปิดใช้งานความสามารถในการ **specify allowed characters** ในการจดจำภาพ OCR ด้วย Aspose.OCR สำหรับ .NET ทำให้การแปลง **ocr image to text** สำหรับกรณีที่ต้องการตัวเลขเท่านั้นเป็นไปอย่างแม่นยำ

## Why Use Allowed‑Character Filtering?

- **ความแม่นยำสูงขึ้น:** การจำกัดชุดอักขระช่วยลดการจดจำผิดพลาด โดยเฉพาะในภาพที่มีสัญญาณรบกวน  
- **เพิ่มประสิทธิภาพ:** เครื่องมือ OCR จะข้าม glyph ที่ไม่เกี่ยวข้อง ทำให้การประมวลผลเร็วขึ้น  
- **การปฏิบัติตามมาตรฐาน:** บังคับใช้รูปแบบข้อมูล (เช่น หมายเลขใบแจ้งหนี้, รหัสซีเรียล) ตั้งแต่ขั้นตอน OCR

## Common Pitfalls & Tips

- **Pitfall:** การส่งสตริงว่างสำหรับอักขระที่อนุญาตจะทำให้การกรองถูกปิดใช้งาน  
  **Tip:** ต้องส่งสตริงที่ไม่ว่างเปล่าหรือใช้ enum `CharactersAllowedType`  

- **Pitfall:** การใช้ `RecognizeLine` กับเอกสารหลายบรรทัดอาจทำให้ข้อมูลบางส่วนหายไป  
  **Tip:** เปลี่ยนเป็น `RecognizeImage` พร้อมตั้งค่า `RecognizeSingleLine = false` เพื่อดึงข้อความเต็มหน้า  

- **Pitfall:** ลืมรวมพาธไดเรกทอรีอย่างถูกต้องอาจทำให้เกิด `FileNotFoundException`  
  **Tip:** ใช้ `Path.Combine(dataDir, "file.jpg")` เพื่อให้พาธทำงานได้บนทุกแพลตฟอร์ม

## Frequently Asked Questions

**Q: Aspose.OCR สำหรับ .NET เหมาะกับทั้งผู้เริ่มต้นและนักพัฒนาที่มีประสบการณ์หรือไม่?**  
A: แน่นอน! API มีความเป็นมิตรต่อผู้เริ่มต้นในขณะเดียวกันก็มีการตั้งค่าขั้นสูงสำหรับผู้ใช้ระดับมืออาชีพ

**Q: ฉันสามารถใช้ Aspose.OCR สำหรับ .NET เพื่อจดจำอักขระในหลายภาษาได้หรือไม่?**  
A: ได้, Aspose.OCR รองรับภาษาหลากหลาย คุณยังสามารถรวมแพ็คเกจภาษาต่าง ๆ เพื่อโครงการหลายภาษาได้อีกด้วย

**Q: Aspose.OCR สำหรับ .NET มีการอัปเดตบ่อยแค่ไหน?**  
A: มีการปล่อยอัปเดตอย่างสม่ำเสมอเพื่อให้สอดคล้องกับการเปิดตัว .NET เวอร์ชันใหม่และการปรับปรุง OCR ตรวจสอบ [documentation](https://reference.aspose.com/ocr/net/) เพื่อดูเวอร์ชันล่าสุด

**Q: มีรุ่นทดลองฟรีสำหรับ Aspose.OCR สำหรับ .NET หรือไม่?**  
A: มี, คุณสามารถสำรวจความสามารถได้โดยดาวน์โหลด [free trial](https://releases.aspose.com/)

**Q: ฉันจะหาความช่วยเหลือหรือเชื่อมต่อกับชุมชนเพื่อรับการสนับสนุนได้จากที่ไหน?**  
A: เยี่ยมชม [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) เพื่อพูดคุยกับผู้เชี่ยวชาญและนักพัฒนาคนอื่น ๆ

---

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
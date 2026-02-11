---
date: 2025-12-25
description: ปรับปรุงความแม่นยำของ OCR ด้วย Aspose OCR สำหรับ .NET โดยใช้การตรวจสอบการสะกดและการสนับสนุนภาษาเพื่อแก้ไขคำที่สะกดผิดและปรับแต่งพจนานุกรมเพื่อการจดจำข้อความที่ไม่มีข้อผิดพลาด
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: ปรับปรุงความแม่นยำของ OCR ด้วยการตรวจสอบการสะกดในภาพ
url: /th/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ปรับปรุงความแม่นยำของ OCR ด้วยการตรวจสอบการสะกดในรูปภาพ

## บทนำ

เมื่อคุณทำงานกับ Optical Character Recognition (OCR) เป้าหมายสูงสุดคือ **ปรับปรุงความแม่นยำของ OCR** เพื่อให้ข้อความที่สกัดออกมาตรงกับภาพต้นฉบับอย่างสมบูรณ์ คำที่สะกดผิดเป็นแหล่งที่มาของข้อผิดพลาดทั่วไป โดยเฉพาะเมื่อภาพต้นทางมีสัญญาณรบกวนหรือใช้ฟอนต์แปลก Aspose.OCR for .NET มีความสามารถในการตรวจสอบการสะกดในตัวที่ไม่เพียงแก้ไขข้อผิดพลาดเหล่านั้น แต่ยังให้คุณขยายเอนจินด้วยพจนานุกรมที่กำหนดเอง ในบทเรียนนี้คุณจะได้เรียนรู้วิธีใช้การตรวจสอบการสะกดเพื่อเพิ่มผลลัพธ์ของ OCR ดูผลลัพธ์ก่อนและหลังการแก้ไข และค้นพบวิธีปรับกระบวนการแก้ไขให้ตรงกับความต้องการของภาษาที่คุณใช้

## คำตอบสั้น
- **การตรวจสอบการสะกดทำอะไรให้ OCR?** มันจะตรวจจับคำที่สะกดผิดในผลลัพธ์ของ OCR โดยอัตโนมัติและแทนที่ด้วยคำที่เป็นไปได้ที่ถูกต้องที่สุด  
- **ไลบรารีใดให้ฟีเจอร์นี้?** Aspose.OCR for .NET มี API ตรวจสอบการสะกดที่พร้อมใช้  
- **ต้องการการเชื่อมต่ออินเทอร์เน็ตหรือไม่?** ไม่จำเป็น เครื่องตรวจสอบการสะกดทำงานแบบออฟไลน์ทั้งหมด  
- **ฉันสามารถเพิ่มคำศัพท์ของฉันเองได้หรือไม่?** ได้ คุณสามารถใส่พจนานุกรมผู้ใช้ที่กำหนดเองเพื่อจัดการกับคำเฉพาะโดเมน  
- **รองรับภาษาอะไรบ้าง?** ดูส่วน “aspose ocr language support” สำหรับรายละเอียด

## การตรวจสอบการสะกดใน OCR คืออะไร?

การตรวจสอบการสะกดจะตรวจสอบข้อความดิบที่ OCR ส่งออก, ระบุโทเคนที่ไม่ตรงกับคำที่รู้จักในพจนานุกรมของภาษาที่เลือก, และเสนอหรือทำการแก้ไขขั้นตอนนี้เป็นสิ่งสำคัญสำหรับ **ปรับปรุงความแม่นยำของ OCR** โดยเฉพาะเมื่อประมวลผลเอกสารสแกน, ใบเสร็จ, หรือแบบฟอร์มที่ OCR อาจตีความอักขระผิดพลาด

## ทำไมต้องใช้ Aspose OCR Language Support?

Aspose.OCR มาพร้อมกับแพ็คภาษาอย่างครบถ้วนและอนุญาตให้คุณต่อพจนานุกรมเพิ่มเติม การใช้ **aspose ocr language support** หมายความว่าคุณสามารถจัดการเอกสารหลายภาษาโดยไม่ต้องเขียนพาร์เซอร์เอง และคุณจะได้เข้าถึงกฎเฉพาะภาษาที่ช่วยเพิ่มคุณภาพการจดจำต่อไป

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึกในเวทมนตร์การตรวจสอบการสะกด, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้พร้อมใช้งาน:

- Aspose.OCR for .NET Library: ดาวน์โหลดและติดตั้งไลบรารี Aspose.OCR จาก [release page](https://releases.aspose.com/ocr/net/)

- Document Directory: ตรวจสอบว่าคุณมีโฟลเดอร์ที่กำหนดไว้สำหรับเอกสารของคุณ แทนที่ `"Your Document Directory"` ในโค้ดด้วยพาธจริง

## นำเข้า Namespaces

เริ่มต้นด้วยการนำเข้า namespaces ที่จำเป็นในโปรเจกต์ .NET ของคุณ:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## ขั้นตอนที่ 1: เริ่มต้น Aspose.OCR

สร้างอินสแตนซ์ของ Aspose.OCR เพื่อเริ่มกระบวนการ OCR

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 2: จดจำภาพ

ต่อไปให้จดจำข้อความในภาพด้วย Aspose.OCR ตัวอย่างโค้ดต่อไปนี้แสดงกระบวนการนี้:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## ขั้นตอนที่ 3: ก่อนการแก้ไข

ดึงผลลัพธ์ OCR ก่อนการแก้ไขเพื่อเปรียบเทียบกับเวอร์ชันที่แก้ไขแล้ว

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## ขั้นตอนที่ 4: หลังการแก้ไข

ใช้การตรวจสอบการสะกดเพื่อรับผลลัพธ์ที่แก้ไขแล้ว โค้ดต่อไปนี้แสดงขั้นตอนนี้:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## ขั้นตอนที่ 5: คำที่สะกดผิดและคำแนะนำ

รับรายการคำที่สะกดผิดพร้อมคำแนะนำการแก้ไขโดยใช้โค้ดต่อไปนี้:

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## ขั้นตอนที่ 6: แก้ไขข้อความของผู้ใช้

แก้ไขข้อความที่ผู้ใช้ระบุโดยใช้ไลบรารี Aspose.OCR:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## ขั้นตอนที่ 7: การแก้ไขด้วยพจนานุกรมผู้ใช้

เพิ่มประสิทธิภาพการแก้ไขโดยรวมพจนานุกรมผู้ใช้ที่กำหนดเองเข้าไป:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| ไม่ได้คำแนะนำใด ๆ | พ็อกเกจภาษาไม่ได้โหลดหรือข้อความสั้นเกินไป | ตรวจสอบว่า `RecognitionSettings(Language.Eng)` ตรงกับภาษาของภาพต้นทางและผลลัพธ์ OCR มีอักขระเพียงพอ |
| พจนานุกรมกำหนดเองไม่ทำงาน | พาธหรือรูปแบบไฟล์ไม่ถูกต้อง | ยืนยันว่า `dictionary.txt` มีอยู่ที่ตำแหน่งที่ระบุและใช้รูปแบบหนึ่งคำต่อบรรทัด |
| ตัวตรวจสอบการสะกดทำงานช้ากับเอกสารขนาดใหญ่ | การประมวลผลแต่ละคำแยกกันเพิ่มภาระ | ประมวลผลหน้าเป็นชุดหรือเพิ่มหน่วยความจำหากรันบน .NET Core |

## คำถามที่พบบ่อย

### Q1: ฉันสามารถใช้ Aspose.OCR กับภาษาอื่นนอกจากอังกฤษได้หรือไม่?

A1: ได้, Aspose.OCR รองรับหลายภาษา ปรับการตั้งค่าภาษาให้ตรงตามที่ต้องการ

### Q2: ฉันจะรวม Aspose.OCR เข้าในโปรเจกต์ .NET ของฉันอย่างไร?

A2: ดูที่ [documentation](https://reference.aspose.com/ocr/net/) สำหรับขั้นตอนการรวมอย่างละเอียด

### Q3: มีเวอร์ชันทดลองใช้สำหรับ Aspose.OCR หรือไม่?

A3: มี, คุณสามารถสำรวจฟีเจอร์ต่าง ๆ ด้วย [free trial version](https://releases.aspose.com/)

### Q4: ฉันสามารถอัปโหลดพจนานุกรมกำหนดเองสำหรับการตรวจสอบการสะกดได้หรือไม่?

A4: แน่นอน! บทเรียนนี้แสดงวิธีเพิ่มประสิทธิภาพการแก้ไขด้วยพจนานุกรมที่ผู้ใช้จัดเตรียม

### Q5: ฉันจะหาการสนับสนุนสำหรับ Aspose.OCR ได้จากที่ไหน?

A5: เยี่ยมชม [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) เพื่อรับการสนับสนุนจากชุมชนและคำแนะนำ

---

**Last Updated:** 2025-12-25  
**Tested With:** Aspose.OCR for .NET latest version  
**Author:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

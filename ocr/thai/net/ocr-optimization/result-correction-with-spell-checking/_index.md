---
title: การแก้ไขผลลัพธ์ด้วยการตรวจสอบการสะกดในการจดจำรูปภาพ OCR
linktitle: การแก้ไขผลลัพธ์ด้วยการตรวจสอบการสะกดในการจดจำรูปภาพ OCR
second_title: Aspose.OCR .NET API
description: เพิ่มความแม่นยำของ OCR ด้วย Aspose.OCR สำหรับ .NET แก้ไขการสะกด ปรับแต่งพจนานุกรม และรับรู้ข้อความที่ปราศจากข้อผิดพลาดได้อย่างง่ายดาย
weight: 13
url: /th/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การแก้ไขผลลัพธ์ด้วยการตรวจสอบการสะกดในการจดจำรูปภาพ OCR

## การแนะนำ

ในขอบเขตของการรู้จำอักขระด้วยแสง (OCR) การได้ผลลัพธ์ที่แม่นยำเป็นสิ่งสำคัญอย่างยิ่งในการดึงข้อมูลที่มีความหมายจากรูปภาพ ความท้าทายทั่วไปประการหนึ่งคือการจัดการกับคำที่สะกดผิดในกระบวนการจดจำ โชคดีที่ Aspose.OCR สำหรับ .NET มอบโซลูชันอันทรงพลังเพื่อปรับปรุงผลลัพธ์ OCR ผ่านการตรวจสอบการสะกด

บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการแก้ไขผลลัพธ์ด้วยการตรวจตัวสะกดโดยใช้ Aspose.OCR สำหรับ .NET ในตอนท้าย คุณจะพร้อมที่จะปรับปรุงความถูกต้องของข้อความที่ได้มาจาก OCR เพื่อให้มั่นใจว่าได้ผลลัพธ์ที่ละเอียดและปราศจากข้อผิดพลาดมากขึ้น

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกเรื่องเวทมนตร์ตรวจสอบการสะกด ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

-  Aspose.OCR สำหรับ .NET Library: ดาวน์โหลดและติดตั้งไลบรารี Aspose.OCR จาก[หน้าปล่อย](https://releases.aspose.com/ocr/net/).

- ไดเร็กทอรีเอกสาร: ตรวจสอบให้แน่ใจว่าคุณมีไดเร็กทอรีที่กำหนดสำหรับเอกสารของคุณ แทนที่ "Your Document Directory" ในข้อมูลโค้ดด้วยเส้นทางจริง

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นในโครงการ .NET ของคุณ:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## ขั้นตอนที่ 1: เริ่มต้น Aspose.OCR

เริ่มต้นอินสแตนซ์ของ Aspose.OCR เพื่อเริ่มต้นกระบวนการ OCR

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";

// เริ่มต้นอินสแตนซ์ของ AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 2: จดจำรูปภาพ

จากนั้น จดจำข้อความในรูปภาพโดยใช้ Aspose.OCR นี่เป็นตัวอย่างที่สาธิตกระบวนการนี้:

```csharp
// รับรู้ถึงภาพ
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## ขั้นตอนที่ 3: ก่อนการแก้ไข

ดึงผลลัพธ์ OCR ก่อนการแก้ไขเพื่อเปรียบเทียบกับเวอร์ชันที่แก้ไข

```csharp
// รับผล
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## ขั้นตอนที่ 4: หลังการแก้ไข

ใช้การตรวจสอบการสะกดเพื่อให้ได้ผลลัพธ์ที่ถูกต้อง ข้อมูลโค้ดต่อไปนี้แสดงให้เห็นขั้นตอนนี้:

```csharp
// รับผลการแก้ไข
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## ขั้นตอนที่ 5: คำและข้อเสนอแนะที่สะกดผิด

รับรายการคำที่สะกดผิดพร้อมกับการแก้ไขที่แนะนำโดยใช้รหัสต่อไปนี้:

```csharp
// รับรายการคำที่สะกดผิดพร้อมคำแนะนำ
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

## ขั้นตอนที่ 6: แก้ไขข้อความผู้ใช้

แก้ไขข้อความที่ผู้ใช้ระบุโดยใช้ไลบรารี Aspose.OCR:

```csharp
// ข้อความผู้ใช้ที่ถูกต้อง
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## ขั้นตอนที่ 7: การแก้ไขด้วยพจนานุกรมผู้ใช้

ปรับปรุงการแก้ไขเพิ่มเติมโดยการรวมพจนานุกรมผู้ใช้แบบกำหนดเอง:

```csharp
// รับผลลัพธ์ที่ถูกต้องด้วยพจนานุกรมผู้ใช้
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## บทสรุป

ยินดีด้วย! คุณได้สำรวจความสามารถในการตรวจสอบการสะกดของ Aspose.OCR สำหรับ .NET เรียบร้อยแล้ว คุณสมบัตินี้ช่วยให้คุณปรับแต่งผลลัพธ์ OCR เพื่อให้มั่นใจถึงความแม่นยำและขจัดข้อผิดพลาด

## คำถามที่พบบ่อย

### คำถามที่ 1: ฉันสามารถใช้ Aspose.OCR สำหรับภาษาอื่นที่ไม่ใช่ภาษาอังกฤษได้หรือไม่

A1: ใช่ Aspose.OCR รองรับหลายภาษา ปรับการตั้งค่าภาษาให้เหมาะสม

### คำถามที่ 2: ฉันจะรวม Aspose.OCR เข้ากับโปรเจ็กต์ .NET ของฉันได้อย่างไร

 A2: โปรดดูที่[เอกสารประกอบ](https://reference.aspose.com/ocr/net/) สำหรับขั้นตอนการบูรณาการโดยละเอียด

### คำถามที่ 3: Aspose.OCR มีเวอร์ชันทดลองใช้งานหรือไม่

 A3: ใช่ คุณสามารถสำรวจคุณสมบัติต่างๆ ได้ด้วย[รุ่นทดลองใช้ฟรี](https://releases.aspose.com/).

### คำถามที่ 4: ฉันสามารถอัปโหลดพจนานุกรมที่กำหนดเองสำหรับการตรวจตัวสะกดได้หรือไม่

A4: แน่นอน! บทช่วยสอนสาธิตวิธีการปรับปรุงการแก้ไขโดยใช้พจนานุกรมที่ผู้ใช้จัดเตรียมไว้ให้

### คำถามที่ 5: ฉันจะขอรับการสนับสนุนสำหรับ Aspose.OCR ได้ที่ไหน

 A5: เยี่ยมชม[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) สำหรับการสนับสนุนและคำแนะนำจากชุมชน
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

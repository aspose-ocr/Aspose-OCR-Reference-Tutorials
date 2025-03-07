---
title: การแสดง OCR ด้วยการเลือกภาษาใน Aspose.OCR
linktitle: การแสดง OCR ด้วยการเลือกภาษาใน Aspose.OCR
second_title: Aspose.OCR Java API
description: ปลดล็อกการแยกข้อความจากรูปภาพอย่างแม่นยำด้วย Aspose.OCR สำหรับ Java ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อ OCR ที่แม่นยำพร้อมการเลือกภาษา
weight: 11
url: /th/java/ocr-operations/perform-ocr-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การแสดง OCR ด้วยการเลือกภาษาใน Aspose.OCR

## การแนะนำ

ในภูมิทัศน์ของเทคโนโลยีที่เปลี่ยนแปลงตลอดเวลา Optical Character Recognition (OCR) มีบทบาทสำคัญในการดึงข้อมูลที่มีความหมายจากรูปภาพ Aspose.OCR สำหรับ Java โดดเด่นในฐานะเครื่องมืออันทรงพลังที่ช่วยให้นักพัฒนาสามารถรวมความสามารถ OCR เข้ากับแอปพลิเคชัน Java ของตนได้อย่างราบรื่น ในคำแนะนำทีละขั้นตอนนี้ เราจะสำรวจวิธีดำเนินการ OCR ด้วยการเลือกภาษาโดยใช้ Aspose.OCR เพื่อปลดล็อกศักยภาพในการประมวลผลเนื้อหาที่หลากหลายด้วยความแม่นยำ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java บนระบบของคุณ และสภาพแวดล้อมการพัฒนาของคุณได้รับการตั้งค่าแล้ว

-  ไลบรารี Aspose.OCR: ดาวน์โหลดและติดตั้งไลบรารี Aspose.OCR สำหรับ Java คุณสามารถค้นหาห้องสมุดและเอกสารที่เกี่ยวข้อง[ที่นี่](https://reference.aspose.com/ocr/java/).

- ไฟล์รูปภาพ: เตรียมไฟล์รูปภาพที่มีข้อความที่คุณต้องการแยก ตัวอย่างเช่น ลองใช้ไฟล์ชื่อ "p3.png"

## แพ็คเกจนำเข้า

ในโปรเจ็กต์ Java ของคุณ ให้นำเข้าแพ็คเกจที่จำเป็นเพื่อใช้ประโยชน์จากฟังก์ชันการทำงานของ Aspose.OCR เพิ่มบรรทัดต่อไปนี้ที่จุดเริ่มต้นของไฟล์ Java ของคุณ:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเร็กทอรีเอกสารของคุณ

```java
// เส้นทางไปยังไดเร็กทอรีเอกสาร
String dataDir = "Your Document Directory";
```

แทนที่ "Your Document Directory" ด้วยเส้นทางจริงไปยังไดเร็กทอรีที่มีไฟล์รูปภาพของคุณ

## ขั้นตอนที่ 2: กำหนดเส้นทางรูปภาพ

```java
// เส้นทางภาพ
String file = dataDir + "p3.png";
```

ปรับตัวแปรไฟล์ให้ชี้ไปที่ไฟล์ภาพเฉพาะของคุณ

## ขั้นตอนที่ 3: สร้างอินสแตนซ์ Aspose.OCR API

```java
// สร้างอินสแตนซ์ API
AsposeOCR api = new AsposeOCR();
```

เริ่มต้นวัตถุ AsposeOCR เพื่อเข้าถึงคุณสมบัติต่างๆ

## ขั้นตอนที่ 4: ตั้งค่าตัวเลือกการจดจำ

```java
// ตั้งค่าตัวเลือกการจดจำ
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

ปรับแต่งการตั้งค่าการจดจำตามความต้องการของคุณ ปรับพารามิเตอร์ เช่น การเอียง ภาษา และพื้นที่การจดจำ

## ขั้นตอนที่ 5: ดำเนินการ OCR และดึงผลลัพธ์

```java
// รับวัตถุผลลัพธ์
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

ดำเนินการ OCR โดยใช้ไฟล์รูปภาพและการตั้งค่าที่ระบุ บันทึกผลลัพธ์ในวัตถุ RecognitionResult

## ขั้นตอนที่ 6: พิมพ์และใช้ประโยชน์จากผลลัพธ์

```java
// พิมพ์ผล
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

พิมพ์ข้อความที่แยกออกมา พื้นที่การจดจำ การแสดง JSON มุมเอียง และคำเตือนใดๆ ใช้ผลลัพธ์ตามความจำเป็นในแอปพลิเคชันของคุณ

## บทสรุป

ในบทช่วยสอนนี้ เราได้เจาะลึกเกี่ยวกับการผสานรวม Aspose.OCR สำหรับ Java อย่างราบรื่นเพื่อดำเนินการ OCR ด้วยการเลือกภาษา ไลบรารีอันทรงพลังนี้เปิดโลกแห่งความเป็นไปได้สำหรับนักพัฒนาที่ต้องการดึงข้อความจากรูปภาพอย่างแม่นยำ

## คำถามที่พบบ่อย

### คำถามที่ 1: ฉันสามารถใช้ Aspose.OCR สำหรับหลายภาษาในกระบวนการจดจำเดียวได้หรือไม่

A1: ได้ คุณสามารถตั้งค่าได้หลายภาษาใน RecognitionSettings เพื่อเพิ่มความแม่นยำในการรู้จำสำหรับเนื้อหาหลายภาษา

### คำถามที่ 2: ฉันจะจัดการรูปแบบรูปภาพต่างๆ ด้วย Aspose.OCR ได้อย่างไร

A2: Aspose.OCR รองรับรูปแบบภาพที่หลากหลาย รวมถึง PNG, JPEG และ TIFF เพียงระบุเส้นทางไฟล์ที่ถูกต้องในตัวแปรเส้นทางรูปภาพ

### คำถามที่ 3: มีการจำกัดขนาดของภาพที่ Aspose.OCR สามารถประมวลผลได้หรือไม่

A3: Aspose.OCR สามารถรองรับรูปภาพขนาดต่างๆ ได้ แต่รูปภาพขนาดใหญ่อาจต้องใช้เวลาและทรัพยากรในการประมวลผลมากขึ้น

### คำถามที่ 4: ฉันสามารถปรับการตั้งค่าการจดจำสำหรับพื้นที่เฉพาะภายในรูปภาพได้หรือไม่

A4: แน่นอน. ใช้คุณสมบัติ RecognitionAreas เพื่อกำหนดสี่เหลี่ยมเฉพาะภายในภาพเพื่อการจดจำเป้าหมาย

### คำถามที่ 5: Aspose.OCR เหมาะสำหรับทั้งโครงการส่วนตัวและเชิงพาณิชย์หรือไม่

A5: ใช่ Aspose.OCR เสนอตัวเลือกสิทธิ์การใช้งานที่ยืดหยุ่น ทำให้เหมาะสำหรับการใช้งานส่วนบุคคลและเชิงพาณิชย์
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---
title: การดำเนินการ OCR บนรูปภาพจาก URL ใน Aspose.OCR สำหรับ Java
linktitle: การดำเนินการ OCR บนรูปภาพจาก URL ใน Aspose.OCR สำหรับ Java
second_title: Aspose.OCR Java API
description: ปลดล็อกการแยกข้อความรูปภาพอย่างราบรื่นใน Java ด้วย Aspose.OCR OCR ความแม่นยำสูงพร้อมการรวมที่ง่ายดาย
weight: 11
url: /th/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การดำเนินการ OCR บนรูปภาพจาก URL ใน Aspose.OCR สำหรับ Java

## การแนะนำ

ยินดีต้อนรับสู่คำแนะนำทีละขั้นตอนของเราเกี่ยวกับการดำเนินการ Optical Character Recognition (OCR) บนรูปภาพจาก URL โดยใช้ Aspose.OCR สำหรับ Java บทช่วยสอนนี้ออกแบบมาเพื่อช่วยให้คุณผสานรวม Aspose.OCR เข้ากับแอปพลิเคชัน Java ของคุณได้อย่างราบรื่น ช่วยให้คุณสามารถแยกข้อความจากรูปภาพได้อย่างง่ายดาย Aspose.OCR เป็นไลบรารี OCR ที่ทรงพลังซึ่งรองรับรูปแบบรูปภาพที่หลากหลาย ทำให้เป็นเครื่องมืออันมีค่าสำหรับแอปพลิเคชันที่ต้องการการแยกข้อความ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา Java ที่ใช้งานได้บนเครื่องของคุณ

2.  ไลบรารี Aspose.OCR: ดาวน์โหลดและติดตั้ง Aspose.OCR สำหรับไลบรารี Java คุณสามารถค้นหาห้องสมุดและเอกสารที่เกี่ยวข้องได้ที่[เว็บไซต์ Aspose.OCR](https://reference.aspose.com/ocr/java/).

## แพ็คเกจนำเข้า

ในโปรเจ็กต์ Java ของคุณ ให้นำเข้าแพ็คเกจที่จำเป็นสำหรับ Aspose.OCR:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ API

เริ่มต้นอินสแตนซ์ของคลาส AsposeOCR:

```java
AsposeOCR api = new AsposeOCR();
```

## ขั้นตอนที่ 2: กำหนด URL รูปภาพ

ระบุ URL ของรูปภาพที่คุณต้องการใช้ OCR:

```java
String uri = "https://www.example.com/your-image.png";
```

## ขั้นตอนที่ 3: ตั้งค่าตัวเลือกการจดจำ

กำหนดการตั้งค่าการจดจำ เช่น การปิดใช้งานการเอียงอัตโนมัติ และการกำหนดพื้นที่การจดจำ:

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// กำหนดพื้นที่การจดจำโดยใช้สี่เหลี่ยม
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## ขั้นตอนที่ 4: ดำเนินการ OCR

เรียกใช้กระบวนการรับรู้ OCR:

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## ขั้นตอนที่ 5: พิมพ์ผลลัพธ์

แสดงผลการจดจำ รวมถึงข้อความที่แยกออกมา ข้อความพื้นที่การจดจำ เอาต์พุต JSON และคำเตือนใดๆ:

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```

ทำซ้ำขั้นตอนเหล่านี้เพื่อรวม Aspose.OCR เข้ากับแอปพลิเคชัน Java ของคุณและแยกข้อความจากรูปภาพอย่างแม่นยำ

## บทสรุป

โดยสรุป การใช้ประโยชน์จาก Aspose.OCR สำหรับ Java มอบโซลูชันที่มีประสิทธิภาพสำหรับงาน OCR ซึ่งช่วยให้นักพัฒนาสามารถแยกข้อความจากรูปภาพได้อย่างราบรื่น คำแนะนำทีละขั้นตอนช่วยให้มั่นใจได้ถึงกระบวนการบูรณาการที่ราบรื่น ทำให้นักพัฒนาทุกระดับสามารถเข้าถึงได้

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.OCR มีความแม่นยำเพียงใดในการจดจำข้อความจากรูปภาพ

A1: Aspose.OCR ให้ความแม่นยำสูงในการรู้จำข้อความ โดยเฉพาะอย่างยิ่งเมื่อกำหนดค่าด้วยพื้นที่การรู้จำที่แม่นยำ

### คำถามที่ 2: Aspose.OCR สามารถรองรับหลายภาษาในระหว่างการจดจำ OCR ได้หรือไม่

ตอบ 2: ใช่ Aspose.OCR รองรับการจดจำข้อความในหลายภาษา ให้ความคล่องตัวสำหรับการใช้งานที่หลากหลาย

### คำถามที่ 3: มีข้อควรพิจารณาในการอนุญาตให้ใช้ Aspose.OCR ในโครงการเชิงพาณิชย์หรือไม่

A3: ใช่ ตรวจสอบให้แน่ใจว่าปฏิบัติตามข้อกำหนดสิทธิ์การใช้งาน Aspose.OCR สำหรับการใช้งานเชิงพาณิชย์ อ้างถึง[buy.aspose.com](https://purchase.aspose.com/buy) สำหรับรายละเอียดใบอนุญาต

### คำถามที่ 4: ฉันจะได้รับการสนับสนุนสำหรับปัญหาที่เกี่ยวข้องกับ Aspose.OCR ได้อย่างไร

 A4: เยี่ยมชม[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) สำหรับการสนับสนุนและการอภิปรายของชุมชน สำหรับการสนับสนุนแบบพรีเมียม ให้พิจารณารับใบอนุญาตชั่วคราวจาก[ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 5: Aspose.OCR สำหรับ Java มีรุ่นทดลองใช้ฟรีหรือไม่

 A5: ใช่ สำรวจคุณสมบัติของ Aspose.OCR พร้อมทดลองใช้ฟรีได้ที่[releases.aspose.com](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

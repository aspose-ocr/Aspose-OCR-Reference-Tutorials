---
category: general
date: 2026-06-22
description: 'วิธีแก้ไขการเอียงของภาพสำหรับ OCR: เรียนรู้ขั้นตอนการเตรียมภาพก่อน OCR,
  กำจัดสัญญาณรบกวนแบบเกลือและพริกไทย, และเพิ่มความแม่นยำ.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: th
og_description: วิธีแก้เอียงภาพสำหรับ OCR, ลบสัญญาณรบกวนแบบเกลือและพริกไทย, และประยุกต์เทคนิคการเตรียมภาพล่วงหน้าสำหรับ
  OCR ในตัวอย่าง Java ฉบับสมบูรณ์.
og_title: วิธีแก้ไขการเอียงของภาพ – คู่มือการเตรียมภาพสำหรับ OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: วิธีแก้การเอียงของภาพ – คู่มือการเตรียมภาพสำหรับ OCR
url: /th/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพ – คู่มือการเตรียมภาพล่วงหน้าสำหรับ OCR

เคยสงสัยไหมว่า **how to deskew image** อย่างไรเพื่อให้เครื่อง OCR ของคุณอ่านข้อความได้จริง? คุณไม่ได้เป็นคนเดียว การสแกนที่เอียงสามารถทำให้เอกสารที่สมบูรณ์กลายเป็นความยุ่งเหยิง และนักพัฒนาส่วนใหญ่ก็เจอปัญหานี้อย่างน้อยหนึ่งครั้ง

ในบทแนะนำนี้เราจะพาคุณผ่านกระบวนการ **image preprocessing OCR** อย่างเต็มรูปแบบที่ไม่เพียงแก้ไขการหมุนเท่านั้น แต่ยัง **remove[s] salt pepper** ศิลปะและเพิ่มความคมชัด—โดยสรุปคือทุกอย่างที่คุณต้องการเพื่อ **preprocess images OCR**‑style ก่อนส่งให้เครื่องมือทำงาน เมื่อเสร็จคุณจะได้โค้ด Java ที่พร้อมรันและโมเดลความเข้าใจว่าทำไมแต่ละขั้นตอนจึงสำคัญ

## วิธีแก้ไขการเอียงของภาพ – การสร้างสายการประมวลผลล่วงหน้า

หัวใจของเวิร์กโฟลว์ที่เป็นมิตรต่อ OCR คืออ็อบเจ็กต์ **preprocess options** ที่ต่อเชื่อมฟิลเตอร์หลาย ๆ ตัวเข้าด้วยกัน คิดว่าเป็นสายพานลำเลียง: แต่ละฟิลเตอร์ทำงานหนึ่งอย่างแล้วส่งภาพต่อไปยังฟิลเตอร์ถัดไป ตัวอย่างที่เรียบง่ายแต่ครบถ้วนนี้ใช้ไลบรารี OCR สมมติที่มี `DeskewFilter`, `DenoiseFilter` และ `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

* **DeskewFilter** วิเคราะห์เส้นข้อความที่โดดเด่นของภาพ, ประมาณมุม, แล้วหมุนบิตแมพกลับสู่แนวนอน ส่วนใหญ่ไลบรารีจำกัดการแก้ไขที่ ±15° เพราะมุมที่ใหญ่กว่านั้นมักบ่งบอกว่าหน้าสแกนแย่มากและต้องการการแทรกแซงด้วยมือ
* **DenoiseFilter** มุ่งเป้าไปที่รูปแบบ *salt‑and‑pepper* แบบคลาสสิก—พิกเซลสีดำหรือสีขาวที่แยกเดี่ยวเหมือนสัญญาณสถิตบนทีวี การลบพวกมันจะป้องกันไม่ให้เครื่อง OCR สับสนระหว่างสัญญาณรบกวนกับอักขระ
* **ContrastBoostFilter** ขยายฮิสโตแกรม ทำให้เส้นที่อ่อนแอเด่นชัดขึ้น ตัวคูณ `1.5f` เป็นค่าเริ่มต้นที่ปลอดภัย; คุณสามารถเพิ่มได้หากสแกนของคุณซีดเกินไป

> **Pro tip:** หากคุณรู้ว่าเอกสารของคุณไม่มีการเอียงเกิน 10° ให้ส่งค่าขอบเขตที่เล็กกว่านั้นไปยัง `DeskewFilter`—อัลกอริธึมจะทำงานเร็วขึ้นและมีโอกาสแก้ไขเกินพิกัดน้อยลง

## Image Preprocessing OCR: การเพิ่มฟิลเตอร์ในลำดับที่ถูกต้อง

ลำดับสำคัญมาก ลองนึกภาพว่าคุณทำการลดสัญญาณรบกวน *ก่อน* การแก้ไขการเอียง; สัญญาณรบกวนอาจทำให้การตรวจจับมุมผิดพลาด ส่งผลให้ผลลัพธ์เอียงผิดตำแหน่ง ในทางกลับกัน การเพิ่มความคมชัด *หลัง* การแก้ไขการเอียงจะทำให้การหมุนไม่สร้างศิลปะใหม่

ต่อไปนี้คือเช็คลิสต์สั้น ๆ ที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์ใดก็ได้:

| ขั้นตอน | ตัวกรอง | เหตุผล |
|------|--------|--------|
| 1 | `DeskewFilter` | จัดแนวฐานข้อความให้ตรง |
| 2 | `DenoiseFilter` | ลบสัญญาณรบกวนพิกเซลที่แยกเดี่ยว |
| 3 | `ContrastBoostFilter` | เพิ่มความอ่านง่ายสำหรับ OCR |

หากคุณต้องการแทรกขั้นตอนเพิ่มเติม—เช่นฟิลเตอร์ **binarization** สำหรับ OCR แบบไบนารี—คุณควรวางไว้ **หลัง** การเพิ่มความคมชัด เพราะภาพที่คมชัดและมีคอนทราสต์สูงจะทำการไบนารีได้แม่นยำยิ่งขึ้น

## ลบสัญญาณรบกวน Salt Pepper ด้วย DenoiseFilter

สัญญาณรบกวน salt‑and‑pepper เป็นที่รู้จักกันดีในสแกนคุณภาพต่ำ โดยเฉพาะจากกล้องโทรศัพท์ราคาถูก `DenoiseFilter` ในไลบรารีของเรานำคอร์เนล median‑filter ไปใช้ ซึ่งจะแทนที่พิกเซลแต่ละตัวด้วยค่ามัธยฐานของเพื่อนบ้าน ผลลัพธ์? จุดรบกวนหายไปโดยไม่ทำให้ตัวอักษรเบลอ

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*เมื่อใดที่ควรเพิ่มขนาดคอร์เนล?* หากภาพต้นฉบับของคุณเต็มไปด้วยจุดรบกวนขนาดใหญ่ คอร์เนลที่ใหญ่ขึ้นจะทำความสะอาดได้ดีกว่า แต่ระวัง: ถ้าใหญ่เกินไปอาจทำให้เส้นบางของฟอนต์ขนาดเล็กหายไป

## Preprocess Images OCR – การใช้สายการประมวลผล

เมื่อคุณประกอบโซ่ฟิลเตอร์เสร็จ การผูกมันเข้ากับเอนจินก็ทำได้ด้วยบรรทัดเดียว (`engine.setPreprocessOptions`). ตั้งแต่นั้นเป็นต้น ทุกการเรียก `recognizeText` จะรันผ่านสายการประมวลผลโดยอัตโนมัติ ไม่ต้องเรียกฟิลเตอร์แต่ละตัวด้วยตนเอง—โค้ดของคุณจะสะอาด และการเปลี่ยนแปลงในอนาคต (เพิ่มฟิลเตอร์ใหม่, ปรับพารามิเตอร์) จะอยู่ศูนย์กลางเดียว

นี่คือตัวอย่างการรันสำเร็จด้วยสแกนตัวอย่างที่เดิมมีการเอียง 12° และมีสัญญาณรบกวน pepper ชัดเจน:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

สังเกตว่าข้อความดูสะอาด, มีการจัดแนวที่ถูกต้อง, และไม่มีอักขระแปลกปลอมที่อาจปรากฏเป็น “I n v o i c e” หรือ “$‑‑‑”

## กรณีขอบและข้อผิดพลาดทั่วไป

| สถานการณ์ | สิ่งที่ควรระวัง | วิธีแก้แนะนำ |
|-----------|-------------------|---------------|
| Rotation > 15° | DeskewFilter อาจหยุดทำงาน | ทำการหมุนล่วงหน้าด้วยตนเองหรือใช้ตัวกรองที่มีช่วงกว้างขึ้น |
| Extremely low resolution ( < 100 dpi ) | Contrast boost ไม่สามารถกู้รายละเอียด | ทำการ Resample ภาพก่อน (เช่น `ResampleFilter`) |
| Mixed noise (Gaussian + salt‑pepper) | DenoiseFilter เพียงอย่างเดียวไม่พอ | เชื่อมต่อ `GaussianBlurFilter` ก่อน `DenoiseFilter` |
| Color scans with colored text | ต้องแปลงเป็น Grayscale | แทรก `GrayscaleFilter` ก่อนการเพิ่มความคมชัด |

การคาดการณ์สถานการณ์เหล่านี้จะช่วยคุณประหยัดเวลาการดีบักในภายหลัง

## ตัวอย่างทำงานเต็มรูปแบบ (All‑in‑One)

ด้านล่างเป็นคลาส Java ที่สามารถวางลงในโปรเจกต์ Maven หรือ Gradle ใด ๆ ที่มี dependency `com.example.ocr` อยู่ มันสาธิต **how to deskew image**, **remove salt pepper** noise, และ **preprocess images OCR**‑style

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่า `scanned-document.png` เป็นใบแจ้งหนี้ที่ชัดเจน):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

หากคุณเปลี่ยนภาพเป็นภาพที่จัดแนวสมบูรณ์แล้ว คุณจะสังเกตว่าสายการประมวลผลยังทำงานต่อไป—ไม่มีการพังและความแม่นยำของ OCR ยังคงสูง

## สรุป

ตอนนี้คุณมีความเข้าใจที่มั่นคงเกี่ยวกับ **how to deskew image** และเหตุผลที่แต่ละขั้นตอนการเตรียมภาพ—**image preprocessing OCR**, **remove salt pepper**, และ **preprocess images OCR**—มีบทบาทสำคัญในการให้ได้ข้อความที่สะอาดและค้นหาได้ ตัวอย่างข้างต้นเป็นโค้ดครบชุด

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานแบบอื่นในโปรเจกต์ของคุณเอง

- [วิธีใช้ AspOCR: ตัวกรองการเตรียมภาพ OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [คำนวณมุมเอียงสำหรับการเตรียมภาพ OCR](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [วิธีตั้งค่าค่าธรณีใน OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
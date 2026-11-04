---
category: general
date: 2026-03-18
description: สร้าง PDF ที่ค้นหาได้จากไฟล์สแกนโดยใช้ Aspose OCR. เรียนรู้วิธีแปลง PDF
  สแกน, ตั้งค่าความละเอียดของ PDF, และเชี่ยวชาญการแปลง PDF ให้เป็นแบบค้นหาได้.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to convert pdf
- convert pdf to searchable
- set pdf resolution
language: th
og_description: สร้างไฟล์ PDF ที่ค้นหาได้จากไฟล์สแกนโดยใช้ Aspose OCR บทเรียนนี้แสดงวิธีแปลง
  PDF สแกน ตั้งค่าความละเอียดของ PDF และรับผลลัพธ์ที่สามารถค้นหาได้.
og_title: สร้าง PDF ที่ค้นหาได้ด้วย Java – คู่มือฉบับสมบูรณ์
tags:
- Java
- OCR
- PDF
- Aspose
title: สร้าง PDF ที่ค้นหาได้ด้วย Java – คู่มือฉบับสมบูรณ์
url: /th/java/advanced-ocr-techniques/create-searchable-pdf-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้ด้วย Java – คู่มือฉบับสมบูรณ์

เคยต้อง **สร้าง PDF ที่สามารถค้นหาได้** จากกองเอกสารสแกนหลายไฟล์แต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อต้องแปลง PDF ที่เป็นภาพอย่างเดียวให้เป็นไฟล์ที่ค้นหาได้ ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของ Java และไลบรารี Aspose OCR คุณสามารถ **แปลง PDF สแกน** ให้เป็น PDF ที่ค้นหาได้ในไม่กี่วินาที  

ในบทแนะนำนี้เราจะพาคุณผ่านทุกขั้นตอนที่ต้องรู้: ตั้งแต่การติดตั้งไลบรารี การกำหนดความละเอียด ไปจนถึงการทำการแปลงจริง เมื่อเสร็จสิ้นคุณจะสามารถ **สร้าง PDF ที่สามารถค้นหาได้** ที่ผู้ใช้ของคุณสามารถค้นหา คัดลอก และทำดัชนีได้โดยไม่ต้องเสียเวลา ไม่มีเนื้อหาเกินความจำเป็น มีเพียงตัวอย่างที่ทำงานได้จริงเท่านั้น

## สิ่งที่คุณต้องมี

ก่อนที่เราจะดำเนินการต่อ โปรดตรวจสอบว่าคุณมี:

- Java 17 หรือใหม่กว่า (โค้ดใช้ไวยากรณ์ `var` แบบสมัยใหม่ แต่คุณสามารถลดเวอร์ชันลงได้หากต้องการ)
- Maven หรือ Gradle เพื่อดึง dependency ของ Aspose OCR
- ไฟล์ PDF สแกน (เอกสารหลายหน้าใดก็ได้)
- IDE หรือโปรแกรมแก้ไขข้อความที่คุณชอบ—IntelliJ IDEA ทำงานได้ดี แต่ Eclipse ก็ใช้ได้เช่นกัน

การมีสิ่งเหล่านี้พร้อมจะทำให้กระบวนการเป็นไปอย่างราบรื่น—ไม่มีการหยุดชะงักกลางทาง

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ไปยังโปรเจกต์ของคุณ

แรกสุด เราต้องนำเอาเอนจิน OCR เข้าไปใน classpath หากคุณใช้ Maven ให้ใส่โค้ดต่อไปนี้ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- latest as of 2026 -->
</dependency>
```

ผู้ใช้ Gradle สามารถเพิ่มได้ดังนี้:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **เคล็ดลับ:** ตรวจสอบที่ repository Maven ของ Aspose อย่างสม่ำเสมอเพื่อหาเวอร์ชันล่าสุด; เวอร์ชันใหม่อาจมีการปรับปรุงประสิทธิภาพสำหรับ PDF ความละเอียดสูง

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine

เมื่อไลบรารีพร้อมใช้งานแล้ว เราจะสร้างอินสแตนซ์ของ `OcrEngine` คิดว่าอ็อบเจกต์นี้เป็นสมองที่อ่านหน้าที่แปลงเป็นราสเตอร์และเปลี่ยนพิกเซลเป็นข้อความ

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.PdfRecognitionOptions;

/**
 * Demonstrates how to create a searchable PDF from a scanned source.
 */
public class PdfToSearchableDemo {

    public static void main(String[] args) throws Exception {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

ทำไมเราต้องมีเอนจินแบบชัดเจน? เพราะ Aspose แยกตรรกะ OCR ออกจากตรรกะการจัดการไฟล์ ทำให้คุณสามารถควบคุมอย่างละเอียด เช่น แพ็คภาษาต่าง ๆ และโหมดการจดจำ

## ขั้นตอนที่ 3: กำหนดความละเอียดของ PDF – **set pdf resolution**

ความละเอียดคือ DPI (dots per inch) ที่ใช้เมื่อไลบรารีทำการแปลงแต่ละหน้าของ PDF ให้เป็นราสเตอร์ก่อนส่งให้ OCR ความละเอียดสูงจะให้ความแม่นยำของข้อความดียิ่งขึ้น แต่จะใช้หน่วยความจำและเวลา CPU มากขึ้น

```java
        // Step 3: Configure PDF recognition options
        PdfRecognitionOptions pdfOptions = new PdfRecognitionOptions();
        pdfOptions.setPageRange(1, 5);      // optional: process pages 1‑5 only
        pdfOptions.setResolution(300);     // 300 DPI is a sweet spot for most scans
```

หากคุณกำลังจัดการกับสแกนคุณภาพต่ำ ให้เพิ่มความละเอียดเป็น 400 DPI; สำหรับเอกสารขนาดใหญ่ที่ต้องการความเร็ว 200 DPI อาจเพียงพอ การเรียก `setPageRange` เป็นตัวเลือก—ละเว้นไว้หากต้องการประมวลผลไฟล์ทั้งหมด

## ขั้นตอนที่ 4: แปลง PDF สแกนเป็น PDF ที่ค้นหาได้ – **convert scanned pdf**

นี่คือหัวใจของกระบวนการ เมธอด `convertPdfToSearchablePdf` รับอาร์กิวเมนต์สามค่า: เส้นทางต้นทาง, เส้นทางปลายทาง, และตัวเลือกที่เราตั้งค่าไว้ก่อนหน้านี้

```java
        // Step 4: Convert the scanned PDF into a searchable PDF
        ocrEngine.convertPdfToSearchablePdf(
                "YOUR_DIRECTORY/scanned.pdf",      // input scanned PDF
                "YOUR_DIRECTORY/searchable.pdf",   // output searchable PDF
                pdfOptions);
```

เมื่อบรรทัดนี้ทำงาน Aspose จะทำการแปลงแต่ละหน้าเป็นราสเตอร์, รัน OCR, และฝังเลเยอร์ข้อความที่มองไม่เห็นไว้บนภาพต้นฉบับ ไฟล์ที่ได้จะดูเหมือนกับต้นฉบับ แต่คุณสามารถค้นหาคำใด ๆ ภายในได้แล้ว

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์

การพิมพ์ `System.out.println` อย่างเร็ว ๆ จะบอกตำแหน่งที่ไฟล์ถูกบันทึก หลังโปรแกรมทำงานเสร็จ เปิดไฟล์ผลลัพธ์ด้วยโปรแกรมอ่าน PDF ใดก็ได้และลองใช้ฟังก์ชันค้นหาในตัว (Ctrl + F) คุณควรเห็นผลลัพธ์แม้ว่า PDF ต้นฉบับจะเป็นเพียงรูปภาพเท่านั้น

```java
        // Step 5: Notify the user
        System.out.println("Searchable PDF created at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล**

```
Searchable PDF created at YOUR_DIRECTORY/searchable.pdf
```

และเมื่อคุณพิมพ์คำที่มีอยู่ในหน้าที่สแกน โปรแกรมอ่าน PDF จะไฮไลต์คำนั้น—เป็นหลักฐานว่าคุณได้ **สร้าง PDF ที่สามารถค้นหาได้** อย่างสำเร็จ

## ขั้นตอนที่ 6: ตัวเลือกเสริม – วิธีแปลง PDF เมื่อต้องการเฉพาะบางหน้า

บางครั้งคุณอาจต้องการทำให้เพียงส่วนหนึ่งของเอกสาร searchable (เช่น 10 หน้าแรกของสัญญา 200 หน้า) เพียงปรับการเรียก `setPageRange` ดังนี้:

```java
pdfOptions.setPageRange(1, 10); // process only pages 1‑10
```

ส่วนอื่น ๆ ยังคงเหมือนเดิม การปรับเล็ก ๆ นี้สามารถประหยัดเวลาการประมวลผลหลายชั่วโมงสำหรับคลังเอกสารขนาดใหญ่

## ขั้นตอนที่ 7: แนวทางปฏิบัติที่ดีที่สุดสำหรับการแปลง PDF ให้เป็นรูปแบบที่ค้นหาได้

- **การประมวลผลเป็นชุด:** ห่อโค้ดการแปลงไว้ในลูปหากคุณมีหลายสิบไฟล์ อย่าลืมใช้อินสแตนซ์ `OcrEngine` เดียวกันเพื่อ ลดภาระการสร้างใหม่
- **การจัดการหน่วยความจำ:** สำหรับ PDF ขนาดใหญ่มาก พิจารณาเพิ่ม heap ของ JVM (`-Xmx2g` หรือมากกว่า) เพื่อหลีกเลี่ยง `OutOfMemoryError`
- **การสนับสนุนภาษา:** โดยค่าเริ่มต้น Aspose OCR ตรวจจับภาษาอังกฤษ หากเอกสารของคุณเป็นสเปน ฝรั่งเศส หรือภาษาอื่น ให้โหลดแพ็คภาษาที่เหมาะสมผ่าน `ocrEngine.getLanguage().add(Language.Spanish);`
- **การประมวลผลหลังแปลง:** หลังจากแปลงแล้ว คุณอาจต้องการบีบอัด PDF (`PdfSaveOptions.setCompressionLevel`) เพื่อลดขนาดไฟล์โดยไม่ทำให้เลเยอร์ข้อความที่ซ่อนอยู่หายไป

## ภาพรวมโดยรวม

ด้านล่างเป็นแผนภาพง่าย ๆ ที่แสดงกระบวนการจาก PDF สแกนไปสู่ PDF ที่ค้นหาได้ คำอธิบายภาพ (alt text) มีคีย์เวิร์ดหลัก ช่วยให้ทั้งเครื่องมือค้นหาและโมเดล AI เข้าใจบริบทของภาพ

![สร้าง PDF ที่สามารถค้นหาได้ตัวอย่าง](https://example.com/images/create-searchable-pdf.png "เวิร์กโฟลว์สร้าง PDF ที่สามารถค้นหาได้")

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.PdfRecognitionOptions;

/**
 * Complete, runnable example that demonstrates how to create a searchable PDF
 * from a scanned PDF using Aspose OCR for Java.
 */
public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Configure PDF recognition options
        PdfRecognitionOptions pdfOptions = new PdfRecognitionOptions();
        pdfOptions.setPageRange(1, 5);      // optional: limit to pages 1‑5
        pdfOptions.setResolution(300);     // set PDF resolution (DPI)

        // Convert the scanned PDF into a searchable PDF
        ocrEngine.convertPdfToSearchablePdf(
                "YOUR_DIRECTORY/scanned.pdf",
                "YOUR_DIRECTORY/searchable.pdf",
                pdfOptions);

        // Notify the user
        System.out.println("Searchable PDF created at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

เรียกใช้คลาสนี้ ตั้งค่าเส้นทางให้ตรงกับไฟล์ของคุณ แล้วดูผลลัพธ์ที่เกิดขึ้นโดยอัตโนมัติ ไม่ต้องตั้งค่าพิเศษใด ๆ สำหรับการแปลงพื้นฐาน

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีสร้าง PDF ที่สามารถค้นหาได้** จากแหล่งสแกนโดยใช้ Java และ Aspose OCR ขั้นตอน—การติดตั้งไลบรารี, การเริ่มต้นเอนจิน, การตั้งค่าความละเอียด, และการเรียก `convertPdfToSearchablePdf`—เป็นเรื่องง่ายและโค้ดพร้อมใส่ลงในโปรเจกต์ใดก็ได้  

หากคุณพร้อมที่จะ **แปลง PDF สแกน** เป็นชุดใหญ่ ลองใช้เคล็ดลับการประมวลผลเป็นชุดที่กล่าวไว้ข้างต้น หรือสำรวจตัวเลือกเพิ่มเติมเช่น แพ็คภาษาของ OCR และการตั้งค่าการบีบอัดต่อไป คุณอาจอยากดู **วิธีแปลง PDF** ไปเป็นรูปแบบอื่น (DOCX, HTML) หรือทดลอง OCR สำหรับเอกสารหลายภาษา

ขอให้สนุกกับการเขียนโค้ด และขอให้ PDF ของคุณทั้งหมดเป็น PDF ที่ค้นหาได้เสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
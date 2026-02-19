---
category: general
date: 2026-02-19
description: ดึงข้อความจากภาพโดยใช้ Java OCR. เรียนรู้ตัวอย่าง Java OCR ที่โหลดภาพเพื่อทำ
  OCR และดึงข้อความจากไฟล์ใบแจ้งหนี้ในไม่กี่ขั้นตอน.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: th
og_description: ดึงข้อความจากภาพโดยใช้ Java OCR คู่มือนี้แสดงวิธีโหลดภาพสำหรับ OCR
  และดึงข้อความจากใบแจ้งหนี้ด้วยตัวอย่าง Java OCR อย่างง่าย.
og_title: สกัดข้อความจากภาพใน Java – ตัวอย่าง OCR ครบถ้วน
tags:
- OCR
- Java
- Aspose
- Image Processing
title: ดึงข้อความจากภาพใน Java – ตัวอย่าง OCR ครบวงจร
url: /th/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพใน Java – ตัวอย่าง OCR ฉบับสมบูรณ์

เคยต้องการ **extract text from image** แต่ไม่แน่ใจว่าจะเลือกไลบรารีใด? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องทำระบบอัตโนมัติการประมวลผลใบแจ้งหนี้หรือสร้างคลังข้อมูลที่สามารถค้นหาได้ ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ Java คุณสามารถโหลดรูปภาพสำหรับ OCR, กำหนด region of interest, และดึงข้อความที่ต้องการได้อย่างแม่นยำ.  

ในบทแนะนำนี้ เราจะพาไปผ่าน **java ocr example** ที่แสดงอย่างชัดเจนว่าอย่างไรจะ **load image for OCR**, ตั้งค่า ROI, และ **extract text from invoice** ด้วย Aspose.OCR. เมื่อเสร็จคุณจะได้โปรแกรมที่สามารถรันได้และนำไปใส่ในโปรเจค Java ใดก็ได้.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีสร้างอินสแตนซ์ `OcrEngine` และเหตุผลที่สำคัญ
- วิธีที่ถูกต้องในการ **load image for OCR** ด้วย `ImageStream` ของ Aspose
- การตั้งค่า **region of interest (ROI)** เพื่อให้คุณประมวลผลเฉพาะส่วนของรูปที่มีจำนวนเงินในใบแจ้งหนี้
- การดึงข้อความที่ถูกจดจำและพิมพ์ออกไปยังคอนโซล
- ข้อผิดพลาดทั่วไป (เช่น พิกัดสี่เหลี่ยมไม่ถูกต้อง) และวิธีแก้ไขอย่างรวดเร็ว

**ข้อกำหนดเบื้องต้น**

- ติดตั้ง Java 8 หรือใหม่กว่า
- Maven หรือ Gradle เพื่อดึงไลบรารี Aspose.OCR (`com.aspose:aspose-ocr`)
- ตัวอย่างรูปใบแจ้งหนี้ (`invoice.png`) ที่วางไว้ในไดเรกทอรีที่รู้จัก

พร้อมหรือยัง? ดี—มาเริ่มกันเลย.

![ดึงข้อความจากรูปภาพด้วย Java OCR](/images/extract-text-from-image-java.png "ตัวอย่างการดึงข้อความจากรูปภาพ")

## ดึงข้อความจากรูปภาพ – ตัวอย่าง Java OCR ทีละขั้นตอน

ด้านล่างเป็นซอร์สโค้ดเต็ม คุณสามารถคัดลอก‑วางลงในไฟล์ `RoiOcrExample.java` และรันโดยตรงได้.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### ทำไมแต่ละขั้นตอนถึงสำคัญ

1. **Creating the OCR engine** – หากไม่มี engine จะไม่มีบริบทสำหรับการประมวลผลภาพ วัตถุนี้ยังช่วยให้คุณปรับ language packs ภายหลังได้หากต้องการสนับสนุนหลายภาษา  
2. **Loading the image** – `ImageStream.fromFile` ทำให้ไม่ต้องกังวลเกี่ยวกับรูปแบบไฟล์, รับประกันว่า engine จะอ่านไบต์ได้อย่างถูกต้อง หากข้ามขั้นตอนนี้จะเกิด `NullPointerException`  
3. **Setting the ROI** – การประมวลผลทั้งหน้าอาจเสียเปล่า โดยการจำกัดสี่เหลี่ยมให้ตรงกับพื้นที่รวมยอดใบแจ้งหนี้ จะทำให้การจดจำเร็วขึ้นและลดสัญญาณรบกวน  
4. **Calling `recognize()`** – นี่คือจุดที่เกิดการทำงานของเวทมนตร์ วิธีนี้รันอัลกอริทึม OCR บน ROI และสร้างอ็อบเจ็กต์ผลลัพธ์  
5. **Printing the output** – ในโครงการจริงคุณอาจเก็บข้อความลงฐานข้อมูล, แต่ `System.out.println` เหมาะสำหรับการสาธิตอย่างรวดเร็ว  

## โหลดรูปภาพสำหรับ OCR

หากคุณสงสัยว่าพาธต้องเป็นแบบเต็มหรือสัมพันธ์ คำตอบคือทั้งสองแบบทำงานได้—แค่ตรวจสอบให้แน่ใจว่าโปรเซส Java สามารถอ่านไฟล์ได้ บน Windows ต้องหนีอักขระ backslash (`C:\\images\\invoice.png`) หรือใช้ slash ปกติ (`C:/images/invoice.png`).  

**Pro tip:** หากคุณประมวลผลใบแจ้งหนี้หลายใบในลูป ให้ใช้ `OcrEngine` อินสแตนซ์เดียวกันซ้ำ; มันจะเก็บแคชทรัพยากรภายในและเพิ่มประสิทธิภาพการทำงาน  

## กำหนด Region of Interest (ROI)

การเลือกสี่เหลี่ยมที่เหมาะสมอาจต้องลองและผิดพลาดบ้าง วิธีที่สะดวกในการหาพิกัดคือเปิดรูปในโปรแกรมแก้ไขกราฟิกใดก็ได้ (เช่น GIMP หรือ Paint.NET) แล้ววางเมาส์เหนือพื้นที่—คุณจะเห็นค่า X/Y ในแถบสถานะ.  

กรณีพิเศษ: ใบแจ้งหนี้บางฉบับมีเลย์เอาต์ที่เปลี่ยนแปลงได้ ในสถานการณ์นั้นคุณอาจทำการสแกนล่วงหน้าอย่างรวดเร็วบนรูปทั้งหมด, ค้นหาคำสำคัญเช่น “Total:” ด้วย regex, แล้วปรับ ROI อย่างไดนามิก  

## ทำ OCR และดึงข้อความ

การเรียก `recognize()` เป็นแบบ synchronous—เธรดของคุณจะบล็อกจนกว่า engine จะทำงานเสร็จ สำหรับชุดข้อมูลขนาดใหญ่คุณอาจต้องสร้าง thread pool เพื่อประมวลผลรูปภาพพร้อมกัน เพียงจำไว้ว่าทุกเธรดต้องมี `OcrEngine` อินสแตนซ์ของตนเอง; ไม่ปลอดภัยต่อการใช้หลายเธรดพร้อมกัน  

## รันและตรวจสอบผลลัพธ์

คอมไพล์และรัน:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

คุณควรเห็นผลลัพธ์ประมาณ:

```
ROI text: $1,254.00
```

หากผลลัพธ์ดูเป็นอักขระแปลก ๆ ให้ตรวจสอบพิกัด ROI อีกครั้งและตรวจสอบว่าคุณภาพรูปภาพสูง (300 dpi หรือมากกว่าดีที่สุด).  

### ข้อผิดพลาดทั่วไป & วิธีแก้

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| สตริงว่าง | ROI อยู่นอกขอบเขตของรูปภาพ | ตรวจสอบค่าสี่เหลี่ยมเทียบกับขนาดของรูปภาพ |
| คำที่สะกดผิด | ความละเอียดต่ำ | ใช้แหล่งที่มาความละเอียดสูงขึ้นหรือทำการประมวลผลภาพล่วงหน้า (เช่น การทำไบนารี) |
| `java.lang.NoClassDefFoundError` | ไม่มีไฟล์ JAR ของ Aspose ใน classpath | เพิ่ม `aspose-ocr.jar` ไปยัง `-cp` หรือใช้การจัดการ dependency ของ Maven/Gradle |

## สรุป

ตอนนี้คุณรู้วิธี **extract text from image** ใน Java ด้วย **java ocr example** ที่กระชับแล้ว การโหลดรูปภาพอย่างถูกต้อง, กำหนด ROI ที่โฟกัส, และเรียก `recognize()` ทำให้คุณสามารถ **extract text from invoice** ได้อย่างเชื่อถือและส่งข้อมูลนั้นไปยังระบบต่อไปได้  

ต่อไปทำอะไรดี? ลองเปลี่ยน ROI เพื่อดึงฟิลด์ต่าง ๆ (วันที่, ชื่อผู้ขาย), ทดลองใช้ language packs สำหรับใบแจ้งหนี้หลายภาษา, หรือรวมขั้นตอน OCR เข้าใน Spring Boot microservice. รูปแบบเดียวกันนี้ใช้ได้กับใบเสร็จ, หนังสือเดินทาง, หรือเอกสารใด ๆ ที่ต้องการการดึงข้อความที่แม่นยำ  

หากคุณมีคำถามเกี่ยวกับการขยายโซลูชันนี้หรือการจัดการสแกนที่มีสัญญาณรบกวน, แสดงความคิดเห็นด้านล่าง—ขอให้เขียนโค้ดอย่างสนุก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
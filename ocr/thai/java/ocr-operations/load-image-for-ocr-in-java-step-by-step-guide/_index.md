---
category: general
date: 2026-03-07
description: โหลดภาพสำหรับ OCR ใน Java อย่างรวดเร็ว เรียนรู้วิธีตั้งค่าเครื่องมือ
  OCR กำหนด ROI และดึงข้อความ – รวมตัวอย่างโค้ดเต็มและเคล็ดลับการตั้งค่า OCR.
draft: false
keywords:
- load image for OCR
- how to set OCR
- OCR region of interest
- Java OCR example
- image processing Java
language: th
og_description: โหลดภาพสำหรับ OCR ใน Java และเรียนรู้วิธีตั้งค่า OCR engine คู่มือนี้จะพาคุณผ่านการจัดการ
  ROI การหมุนภาพ และโค้ดเต็ม
og_title: โหลดรูปภาพสำหรับ OCR ด้วย Java – คู่มือการเขียนโปรแกรมแบบสมบูรณ์
tags:
- OCR
- Java
- Image Processing
title: โหลดภาพสำหรับ OCR ใน Java – คู่มือแบบทีละขั้นตอน
url: /th/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# โหลดรูปภาพสำหรับ OCR ใน Java – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยต้อง **โหลดรูปภาพสำหรับ OCR** แต่ไม่แน่ใจว่าจะเรียกใช้ฟังก์ชันอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาส่วนใหญ่มักเจออุปสรรคเมื่อต้องรับรูปภาพแรกและเครื่องมือ OCR ดูสับสน ข่าวดีคือวิธีแก้ไขค่อนข้างตรงไปตรงมาถ้าคุณรู้ขั้นตอนที่ถูกต้อง

ในบทเรียนนี้เราจะสาธิต **วิธีตั้งค่า OCR** พารามิเตอร์ กำหนดพื้นที่สนใจ (ROI) และสุดท้ายดึงข้อความออกจากส่วนของรูปภาพนั้น เมื่อเสร็จคุณจะได้โปรแกรม Java ที่สามารถโหลดรูปภาพสำหรับ OCR หมุนอัตโนมัติหากจำเป็นและพิมพ์ข้อความที่สกัดออกมา—โดยไม่มีการอธิบายที่ซับซ้อน

## สิ่งที่คุณต้องเตรียม

- Java 17 หรือใหม่กว่า (โค้ดใช้คีย์เวิร์ด `var` เพื่อความกระชับ แต่คุณสามารถลดเวอร์ชันลงได้หากจำเป็น)  
- OCR SDK ที่ให้คลาส `OcrEngine`, `OcrResult`, และ `ImageInputStream` – ตัวอย่างเช่น **Tesseract‑Java**, **ABBYY**, หรือโซลูชันที่เป็นกรรมสิทธิ์  
- รูปตัวอย่าง (`multi_page_form.png`) ที่มีข้อความที่คุณต้องการอ่าน  
- IDE เบื้องต้น (IntelliJ IDEA, Eclipse, VS Code) – ใดก็ได้

ไม่ต้องใช้ Maven หรือ Gradle พิเศษสำหรับตรรกะหลัก; เพียงแค่เพิ่ม JAR ของ OCR ลงใน classpath แล้วคุณก็พร้อมใช้งาน

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine – วิธีตั้งค่า OCR อย่างถูกต้อง

ก่อนที่คุณจะ **โหลดรูปภาพสำหรับ OCR** คุณต้องมีอินสแตนซ์ของเอนจินที่รู้ว่าจะมองหาอะไร ส่วนใหญ่ SDK จะเปิดเผยอ็อบเจ็กต์การกำหนดค่า; ที่นั่นคุณบอกเอนจินให้หมุนข้อความอัตโนมัติภายใน ROI

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.OcrConfig;

public class OcrSetup {
    public static OcrEngine createEngine() {
        OcrEngine engine = new OcrEngine();

        // Enable automatic rotation handling within the region of interest
        engine.getConfig().setAutoRotateWithinRegion(true);

        // You can also tweak language, confidence thresholds, etc.
        // engine.getConfig().setLanguage("eng");
        // engine.getConfig().setMinConfidence(0.75);

        return engine;
    }
}
```

**ทำไมจึงสำคัญ:** การเปิดใช้งาน `setAutoRotateWithinRegion` จะช่วยคุณประหยัดการประมวลผลหลังจากนั้นอย่างมาก ลองนึกภาพฟอร์มที่สแกนแล้วผู้ใช้เอียงหน้าเพียงเล็กน้อย—หากไม่มีแฟล็กนี้ OCR จะอ่านเป็นอักขระไร้สาระ การเปิดใช้งาน *วิธีตั้งค่า OCR* ทำให้ระบบมีความทนทานตั้งแต่แรก

## ขั้นตอนที่ 2: โหลดรูปภาพสำหรับ OCR – ป้อนข้อมูลให้เอนจิน

เมื่อเอนจินพร้อมแล้ว เราจริง ๆ **โหลดรูปภาพสำหรับ OCR** คลาส `ImageInputStream` จะจัดการไฟล์ให้คุณและทำให้ OCR SDK สามารถรับสตรีมโดยตรง

```java
import com.example.ocr.ImageInputStream;
import java.nio.file.Paths;

public class ImageLoader {
    public static ImageInputStream load(String path) throws Exception {
        // Validate the file exists and is readable
        if (!java.nio.file.Files.isReadable(Paths.get(path))) {
            throw new IllegalArgumentException("Cannot read image at: " + path);
        }

        // Create the stream – most SDKs accept a simple file path, but a stream is more flexible
        return new ImageInputStream(path);
    }
}
```

**เคล็ดลับ:** หากคุณทำงานกับ PDF หลายหน้า หลาย OCR library จะให้คุณส่งดัชนีหน้ามาในคอนสตรัคเตอร์ของสตรีม วิธีนี้ทำให้คุณวนลูปผ่านหน้าได้โดยไม่ต้องแปลงเพิ่มเติม

## ขั้นตอนที่ 3: กำหนดพื้นที่สนใจ (ROI)

การสแกนทั้งรูปภาพอาจเสียเวลาโดยเฉพาะกับฟอร์มขนาดใหญ่ การจำกัดโฟกัสเป็นสี่เหลี่ยมจะทำให้การประมวลผลเร็วขึ้นและความแม่นยำดีขึ้น

```java
import java.awt.Rectangle;

public class RoiHelper {
    public static Rectangle defineRoi() {
        // x, y, width, height – adjust these numbers to match your form layout
        int x = 120;
        int y = 350;
        int width = 800;
        int height = 200;

        return new Rectangle(x, y, width, height);
    }
}
```

**กรณีขอบ:** หาก ROI ขยายเกินขอบของรูปภาพ ส่วนใหญ่เอนจินจะโยนข้อยกเว้น การตรวจสอบความสมเหตุสมผลอย่างรวดเร็ว (เช่นเปรียบเทียบ `x + width` กับ `image.getWidth()`) จะช่วยป้องกันการครช

## ขั้นตอนที่ 4: รัน OCR บน ROI

เมื่อเอนจิน, รูปภาพ, และ ROI พร้อมแล้ว ถึงเวลา **โหลดรูปภาพสำหรับ OCR** และทำการจดจำข้อความจริง ๆ

```java
import com.example.ocr.OcrResult;

public class OcrRunner {
    public static OcrResult run(OcrEngine engine,
                                ImageInputStream image,
                                Rectangle roi) throws Exception {
        // The recognize method returns both text and confidence data
        return engine.recognize(image, roi);
    }
}
```

หากคุณต้องการคะแนนความเชื่อมั่นของแต่ละคำ, `OcrResult` มักจะเปิดเผยคอลเลกชัน `getWords()` ที่แต่ละรายการมีเมธอด `getConfidence()` การกรองคำที่ความเชื่อมั่นต่ำอาจมีประโยชน์สำหรับการตรวจสอบต่อไป

## ขั้นตอนที่ 5: ดึงข้อความออกและตรวจสอบผลลัพธ์

สุดท้าย เราพิมพ์สตริงที่สกัดออกมา ในแอปพลิเคชันจริงคุณอาจบันทึกลงฐานข้อมูลหรือส่งต่อให้ตัวพาร์สเซอร์, แต่การพิมพ์บนคอนโซลก็เพียงพอสำหรับการสาธิต

```java
public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = OcrSetup.createEngine();

        // Step 2: Load the image you want to process
        ImageInputStream imageStream = ImageLoader.load("YOUR_DIRECTORY/multi_page_form.png");

        // Step 3: Define where to look – the ROI
        Rectangle regionOfInterest = RoiHelper.defineRoi();

        // Step 4: Run OCR limited to that region
        OcrResult ocrResult = OcrRunner.run(ocrEngine, imageStream, regionOfInterest);

        // Step 5: Show the result
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า ROI มีข้อความ “Invoice #12345”, คุณจะเห็นประมาณนี้:

```
ROI text:
Invoice #12345
Date: 2026-03-07
Total: $1,250.00
```

หาก OCR engine ไม่พบข้อความใดเลย, `ocrResult.getText()` จะคืนสตริงว่าง – เป็นสัญญาณให้คุณตรวจสอบพิกัด ROI หรือคุณภาพของรูปภาพอีกครั้ง

## การจัดการกับปัญหาที่พบบ่อย

| ปัญหา | สาเหตุ | วิธีแก้เร็ว |
|---------|----------------|-----------|
| **ผลลัพธ์เป็นค่าว่าง** | ROI อยู่นอกขอบภาพหรือภาพเป็น grayscale ที่คอนทราสต์ต่ำ | ตรวจสอบพิกัดด้วยโปรแกรมแก้ไขภาพ; เพิ่มคอนทราสต์หรือทำการไบนารีก่อน OCR |
| **อักขระแปลก** | การหมุนไม่ได้รับการจัดการ, หรือใช้ language pack ไม่ถูก | ตรวจสอบให้ `setAutoRotateWithinRegion(true)` เปิดใช้งาน; โหลดโมเดลภาษาให้ถูก (`engine.getConfig().setLanguage("eng")`) |
| **ประสิทธิภาพช้า** | ประมวลผลทั้งภาพแทน ROI | ส่ง `Rectangle` เพื่อลิมิตพื้นที่สแกน; พิจารณาลดขนาดภาพขนาดใหญ่ก่อน |
| **Out‑of‑memory** | โหลดภาพขนาดใหญ่มากเป็นไบต์ดิบ | ใช้ API สตรีม (`ImageInputStream`) และหากสนับสนุน ให้ขอการประมวลผลแบบ tiled |

**เคล็ดลับระดับมืออาชีพ:** เมื่อทำงานกับฟอร์มหลายหน้า ให้ลูปเรียก OCR พร้อมเพิ่มดัชนีหน้า ส่วนใหญ่ SDK อนุญาตให้ใช้อินสแตนซ์ `OcrEngine` เดียวซ้ำได้ ซึ่งช่วยลดค่าใช้จ่ายในการเริ่มต้น

## ไปต่อ – ถ้าคุณต้องการเพิ่มฟีเจอร์อะไรบ้าง?

- **ประมวลผลเป็นชุด:** รวบรวมรายการพาธไฟล์, วนลูปผ่านไฟล์เหล่านั้น, และบันทึกผล OCR แต่ละไฟล์ลง CSV  
- **ROI แบบไดนามิก:** ใช้ OpenCV ตรวจจับฟิลด์ฟอร์มอัตโนมัติ, แล้วส่งพิกัดเหล่านั้นเข้าไปในขั้นตอน OCR  
- **หลังการประมวลผล:** ใช้ regex ทำความสะอาดวันที่, หมายเลขใบแจ้งหนี้, หรือค่าการเงินที่สกัดจาก ROI  

ส่วนขยายทั้งหมดนี้สร้างบนรูปแบบหลักที่เราอธิบาย: **โหลดรูปภาพสำหรับ OCR**, ตั้งค่า **วิธีตั้งค่า OCR**, กำหนดพื้นที่, รันเอนจิน, และจัดการผลลัพธ์

![Screenshot showing ROI highlighted on a form – load image for OCR example](roi-screenshot.png "load image for OCR example")

*ข้อความแทนรูปภาพ: โหลดรูปภาพสำหรับ OCR – พื้นที่สนใจที่ไฮไลท์บนฟอร์มตัวอย่าง*

## สรุป

คุณมีตัวอย่างโค้ดที่สมบูรณ์และสามารถรันได้แล้ว ซึ่งแสดงวิธี **โหลดรูปภาพสำหรับ OCR** ใน Java, ตั้งค่า **วิธีตั้งค่า OCR** อย่างถูกต้อง, และสกัดข้อความจากพื้นที่เฉพาะ ขั้นตอนต่าง ๆ แยกเป็นโมดูล ทำให้คุณสามารถสลับ OCR library หรือปรับ ROI ได้โดยไม่ต้องเขียนโค้ดใหม่ทั้งหมด

ต่อไปลองทดลองกับรูปแบบไฟล์ต่าง ๆ (TIFF, BMP) หรือเพิ่มขั้นตอนพรี‑โปรเซสซิงด้วย OpenCV เพื่อเพิ่มความแม่นยำบนสแกนที่มีนอยส์ หากคุณสนใจการจัดการหลายหน้า ให้ขยายลูปใน `RoiOcrExample` เพื่อวนดัชนีหน้า

ขอให้เขียนโค้ดสนุกและผลลัพธ์ OCR ของคุณใสสะอาดเหมือนคริสตัล!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
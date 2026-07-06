---
category: general
date: 2026-06-16
description: จดจำข้อความจากภาพได้อย่างรวดเร็วด้วย Aspose OCR ใน Java. เรียนรู้วิธีตั้งค่าอุปกรณ์
  GPU, แยกข้อความจากไฟล์ JPG, และอ่านข้อความจากรูปภาพโดยใช้การเร่งความเร็วด้วย GPU.
draft: false
keywords:
- recognize text image
- set gpu device
- extract text jpg
- how to recognize text
- read text picture
language: th
og_description: จดจำข้อความจากภาพด้วย Aspose OCR ใน Java คู่มือนี้แสดงวิธีตั้งค่าอุปกรณ์
  GPU, แยกข้อความจากไฟล์ JPG, และอ่านภาพข้อความอย่างมีประสิทธิภาพ.
og_title: รู้จำข้อความในภาพด้วย Java โดยใช้ Aspose OCR + GPU
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text image quickly with Aspose OCR in Java. Learn how to
    set gpu device, extract text jpg, and read text picture using GPU acceleration.
  headline: recognize text image in Java using Aspose OCR + GPU
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- GPU
title: รู้จำข้อความจากภาพใน Java ด้วย Aspose OCR + GPU
url: /th/java/advanced-ocr-techniques/recognize-text-image-in-java-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การจดจำข้อความในรูปภาพด้วย Java โดยใช้ Aspose OCR + GPU

เคยสงสัยไหมว่าจะจดจำข้อความในรูปภาพด้วยแอปพลิเคชัน Java อย่างไรโดยไม่ทำให้ CPU ของคุณทำงานหนักจนหยุด? คุณไม่ได้เป็นคนเดียว—นักพัฒนาต่างมองหา OCR pipeline ที่เร็วและเชื่อถือได้มากขึ้น ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันที่เร่งด้วย GPU ที่ทำให้คุณดึงข้อความจากไฟล์ JPG ได้ในพริบตา

เราจะเริ่มต้นด้วยการตั้งค่า Aspose OCR จากนั้นเปิดการเร่งความเร็วด้วย GPU และสุดท้ายจะแสดงวิธีอ่านไฟล์รูปภาพข้อความ พิมพ์ผลลัพธ์ และจัดการกับข้อผิดพลาดที่อาจเกิดขึ้น เมื่อเสร็จสิ้นคุณจะรู้ **วิธีจดจำข้อความ** บนภาพใด ๆ ไม่ว่าจะเป็นใบแจ้งหนี้ที่สแกนหรือภาพหน้าจอทั่วไป

## สิ่งที่คุณต้องเตรียม

- **Java 17** (หรือ JDK ล่าสุดใดก็ได้) – โค้ดทำงานบน runtime สมัยใหม่ทั้งหมด  
- **Aspose.OCR for Java** – มีให้ดาวน์โหลดผ่าน Maven Central  
- **GPU** ที่รองรับ CUDA (ไม่บังคับแต่แนะนำอย่างยิ่งสำหรับความเร็ว)  
- ตัวอย่างไฟล์ JPEG (เช่น `sample.jpg`) ที่คุณต้องการประมวลผล  

ไม่มีไลบรารีของบุคคลที่สามอื่น ๆ ที่จำเป็น; สิ่งที่เหลือทั้งหมดมาพร้อมกับ Aspose OCR

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ลงในโปรเจกต์ของคุณ

หากคุณใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ลงในไฟล์ `pom.xml` ของคุณ ผู้ใช้ Gradle สามารถคัดลอกบรรทัด `implementation` ที่เทียบเท่าได้

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **เคล็ดลับ:** รุ่นประเมินผลฟรีจะใส่น้ำหนักโลโก้เล็ก ๆ หากต้องการใช้งานจริง ให้รับไลเซนส์จากพอร์ทัลของ Aspose และเรียก `License license = new License(); license.setLicense("Aspose.OCR.lic");` ก่อนทำงาน OCR ใด ๆ

## ขั้นตอนที่ 2: โหลดภาพที่ต้องการประมวลผล

สิ่งแรกที่คุณทำเมื่ออยาก **จดจำข้อความในรูปภาพ** คือส่งภาพเข้าไปยังเอนจิน OCR Aspose มีตัวห่อ `ImageStream` ที่สะดวกซึ่งสามารถอ่านจากพาธไฟล์, `InputStream` หรือแม้แต่ byte array

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Load the image – replace the path with your own picture
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

สังเกตว่าเราเก็บโค้ดให้เหลือน้อยที่สุด; การเรียก `setImage` ยอมรับรูปแบบ raster ใดก็ได้ที่ Aspose รองรับ รวมถึง JPEG, PNG, และ BMP

## ขั้นตอนที่ 3: เปิดการเร่งความเร็วด้วย GPU (set gpu device)

ต่อมาคือส่วนที่ทำให้คู่มือนี้โดดเด่น: เราจะ **set gpu device** เพื่อให้เอนจิน OCR ทำงานบนการ์ดกราฟิกแทน CPU ซึ่งจะลดเวลาการประมวลผลเป็นวินาที โดยเฉพาะกับภาพความละเอียดสูง

```java
        // Enable GPU acceleration – this is where the magic happens
        engine.getRecognitionSettings().setUseGpu(true);

        // Optional: pick a specific GPU if you have more than one
        // engine.getRecognitionSettings().setGpuDeviceId(0);
```

หากคุณมี GPU หลายตัว ให้ยกคอมเมนต์บรรทัด `setGpuDeviceId` และเปลี่ยน `0` เป็นดัชนีของอุปกรณ์ที่คุณต้องการ Aspose จะย้อนกลับไปใช้ CPU อัตโนมัติหากไม่พบ GPU ที่เข้ากันได้ ดังนั้นคุณไม่ต้องกังวลเรื่องการขัดข้อง

## ขั้นตอนที่ 4: ทำ OCR – วิธีจดจำข้อความ

เมื่อโหลดภาพแล้วและเปิด GPU เราก็สามารถ **วิธีจดจำข้อความ** บนรูปภาพได้แล้ว เมธอด `recognize()` จะรันทั้ง pipeline — การเตรียมข้อมูลล่วงหน้า, การแยกส่วน, การจำแนกอักขระ, และการประมวลผลหลัง

```java
        // Execute the OCR process
        OcrResult result = engine.recognize();
```

อ็อบเจ็กต์ `OcrResult` ที่คืนค่ามีสตริงดิบ, คะแนนความเชื่อมั่น, และแม้แต่กล่องขอบ (bounding boxes) หากคุณต้องการข้อมูลโครงร่างในภายหลัง

## ขั้นตอนที่ 5: แสดงข้อความที่จดจำได้ – extract text jpg / read text picture

เราจะ **extract text jpg** และ **read text picture** เพียงแค่พิมพ์ผลลัพธ์ลงคอนโซล ในแอปจริงคุณอาจบันทึกลงฐานข้อมูลหรือไฟล์

```java
        // Show the recognized text in the console
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

เมื่อคุณรันโปรแกรม ควรเห็นผลลัพธ์ประมาณนี้:

```
Recognized text:
Invoice #12345
Date: 2026-06-15
Total: $1,250.00
```

หากภาพมีสัญญาณรบกวน คุณสามารถปรับค่าการเตรียมข้อมูลของ Aspose (คอนทราสต์, การไบนารี ฯลฯ) — แต่ค่าเริ่มต้นทำงานได้ดีกับไฟล์ JPG ที่ค่อนข้างสะอาด

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือคลาสที่พร้อมรันทั้งหมด:

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the image to be processed
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 2: Enable GPU acceleration for faster recognition
        engine.getRecognitionSettings().setUseGpu(true);
        // Optional: specify a GPU device index if multiple GPUs are present
        // engine.getRecognitionSettings().setGpuDeviceId(0);

        // Step 3: Perform OCR on the loaded image
        OcrResult result = engine.recognize();

        // Step 4: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

> **ผลลัพธ์ที่คาดหวัง:** คอนโซลจะแสดงข้อความที่ปรากฏใน `sample.jpg` อย่างแม่นยำ หากภาพเป็นรูปถ่ายของใบเสร็จ คุณจะเห็นแต่ละบรรทัดเป็นสตริงแยกกัน พร้อมคงการขึ้นบรรทัดใหม่

## กรณีขอบและข้อผิดพลาดทั่วไป

| สถานการณ์ | สิ่งที่ควรระวัง | วิธีแก้แนะนำ |
|-----------|-------------------|---------------|
| **หลาย GPU** | GPU เริ่มต้นอาจไม่ใช่ตัวที่แรงที่สุด | ใช้ `setGpuDeviceId` เพื่อระบุการ์ดที่มีประสิทธิภาพสูง |
| **หน่วยความจำไม่พอสำหรับภาพขนาดใหญ่** | JPG ความละเอียดสูงอาจทำให้หน่วยความจำของ GPU หมด | ปรับขนาดภาพก่อน (`engine.getPreprocessingSettings().setResizeFactor(0.5)`) |
| **ความเชื่อมั่นต่ำ** | ตัวอักษรอาจอ่านผิดหากภาพเบลอ | เปิด `engine.getRecognitionSettings().setUseLanguageModel(true)` เพื่อการแก้ไขตามบริบท |
| **รูปแบบภาพที่ไม่รองรับ** | Aspose OCR รองรับหลายรูปแบบ แต่ไม่รองรับ RAW sensor data | แปลงไฟล์เป็น JPEG หรือ PNG ก่อนส่งให้เอนจิน |

การจัดการกับสถานการณ์เหล่านี้จะทำให้ workflow **จดจำข้อความในรูปภาพ** ของคุณคงความเสถียรในสภาพแวดล้อมที่หลากหลาย

## เคล็ดลับสำหรับ OCR ที่เร็วและสะอาดยิ่งขึ้น

- **ประมวลผลเป็นชุด:** ใช้ตัว `OcrEngine` เพียงอันเดียวสำหรับหลายภาพ; บริบทของ GPU จะคงอยู่ ลดค่าโอเวอร์เฮดของการเริ่มต้น |
- **ความปลอดภัยของเธรด:** แต่ละเธรดควรมีอ็อบเจ็กต์ `OcrEngine` ของตนเอง; คลาสนี้ไม่รองรับการทำงานหลายเธรดพร้อมกัน |
- **โหลดไลเซนส์แต่เนิ่นๆ:** โหลดไลเซนส์ Aspose ตอนเริ่มแอปเพื่อหลีกเลี่ยงลายน้ำรุ่นประเมินผล |
- **บันทึก log:** เปิด `engine.getLogSettings().setEnableLogging(true)` หากต้องการดีบักว่าทำไมภาพบางภาพถึงล้มเหลว |

## สรุป

เราได้แสดงให้คุณเห็น **วิธีจดจำข้อความในรูปภาพ** ด้วย Java โดยใช้ Aspose OCR พร้อมการเร่งความเร็วด้วย GPU โดยทำตามขั้นตอน—เพิ่มไลบรารี, โหลด JPEG, **set gpu device**, รันเอนจิน OCR, และสุดท้าย **extract text jpg** หรือ **read text picture**—คุณก็สามารถแปลงภาพเป็นข้อความได้อย่างรวดเร็วและแม่นยำ

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
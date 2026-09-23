---
category: general
date: 2026-02-09
description: เรียนรู้วิธีทำ OCR แบบชุดใน Java ด้วย Aspose OCR ดึงข้อความจากภาพและจดจำข้อความจากไฟล์
  PNG, JPG และ TIFF ในหนึ่งคำสั่งเดียว.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: th
og_description: เชี่ยวชาญการทำ OCR แบบกลุ่มใน Java บทเรียนนี้จะแสดงวิธีดึงข้อความจากภาพ
  PNG, JPG และ TIFF ด้วย Aspose OCR พร้อมตัวอย่างโค้ดที่ชัดเจน
og_title: วิธีทำ OCR แบบกลุ่มใน Java – ดึงข้อความจากภาพอย่างมีประสิทธิภาพ
tags:
- OCR
- Java
- Aspose
title: วิธีทำ OCR แบบกลุ่มใน Java – คู่มือเต็มสำหรับการดึงข้อความจากภาพ
url: /th/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ใน Java – คู่มือเต็มสำหรับการดึงข้อความจากรูปภาพ

เคยสงสัย **วิธีทำ batch OCR** กับรูปภาพหลายไฟล์โดยไม่ต้องเขียนลูปสำหรับแต่ละไฟล์หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ คุณอาจได้รับโฟลเดอร์ที่เต็มไปด้วยสแกน—ใบเสร็จ PNG, ภาพหน้าจอ JPG, หรือแม้กระทั่ง TIFF หลายหน้า—and คุณต้องการข้อความอย่างรวดเร็ว  

ข่าวดีคือ Aspose OCR ให้คุณทำได้ตรงนั้น: เรียกเมธอดเดียวที่จดจำข้อความจากไฟล์ PNG, JPG, และ TIFF ทั้งหมดพร้อมกัน ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด ตั้งแต่การตั้งค่าโปรเจกต์จนถึงการพิมพ์ผลลัพธ์ เพื่อให้คุณเริ่มดึงข้อความจากรูปภาพได้ทันที

## สิ่งที่บทแนะนำนี้ครอบคลุม

* **วิธีทำ batch OCR** ด้วย `OcrBatchProcessor` ของ Aspose
* วิธี **ดึงข้อความจากรูปภาพ** ในรูปแบบต่าง ๆ (PNG, JPG, TIFF)
* เคล็ดลับการควบคุม parallelism เพื่อให้แอปของคุณตอบสนองได้ดี
* โปรแกรม Java ที่ทำงานได้ครบถ้วน คุณสามารถคัดลอก‑วางและรันได้ทันที

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose มาก่อน—แค่ติดตั้ง Java เบื้องต้นและ IDE ที่คุณชอบเท่านั้น เมื่อจบคุณจะมีพื้นฐานที่มั่นคงสำหรับการจดจำข้อความจากไฟล์ PNG, JPG, และ TIFF แบบเป็นกลุ่ม

---

![Diagram illustrating how to batch OCR multiple image files](/images/batch-ocr-diagram.png "how to batch ocr")

*ข้อความแทนรูป: แผนภาพวิธีทำ batch OCR แสดงไฟล์รูปหลายไฟล์ที่ถูกประมวลผลพร้อมกัน*

## ข้อกำหนดเบื้องต้น

| Requirement | Why it matters |
|-------------|----------------|
| Java 17 หรือใหม่กว่า | Aspose OCR รองรับ JVM รุ่นใหม่ |
| Maven หรือ Gradle | ทำให้การเพิ่มไลบรารี Aspose OCR ง่ายขึ้น |
| ความรู้พื้นฐาน Java | จำเป็นสำหรับการเข้าใจการไหลของโค้ด |
| ชุดรูปภาพตัวอย่าง (`.png`, `.jpg`, `.tif`) | เพื่อดูการดึงข้อความทำงานจริง |

ถ้าคุณมีทั้งหมดนี้แล้ว—ยอดเยี่ยม—มาลงมือกันต่อ

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ลงในโปรเจกต์ของคุณ

สิ่งแรกที่คุณต้องการคือ JAR ของ Aspose OCR. หากใช้ Maven ให้เพิ่มลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

หากคุณชอบ Gradle ให้ใช้รูปแบบต่อไปนี้:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

การเพิ่ม dependency นี้จะดึงทุกอย่างที่จำเป็นสำหรับ **recognize text from png**, **recognize text from jpg**, และ **recognize text from tiff** ไม่ต้องมีไลบรารี native เพิ่มเติม

## ขั้นตอนที่ 2: กำหนดไฟล์รูปภาพที่ต้องการประมวลผล

ต่อไปเราจะบอก engine OCR ว่าไฟล์ใดบ้างที่จะจัดการ นี่คือจุดที่ **how to batch OCR** ส่องแสง—แค่ส่งรายการพาธและให้ไลบรารีทำงานหนักให้

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **เคล็ดลับมืออาชีพ:** ใช้พาธแบบ absolute หรือใช้ `Paths.get(...)` เพื่อหลีกเลี่ยงปัญหาในระบบปฏิบัติการต่าง ๆ

## ขั้นตอนที่ 3: สร้าง Batch Processor และปรับ Parallelism

Aspose OCR มาพร้อมกับ `OcrBatchProcessor` ที่สามารถรันการจดจำหลาย ๆ งานพร้อมกัน การควบคุมจำนวนเธรดช่วยป้องกันแอปของคุณไม่ให้ใช้ CPU มากเกินไปเมื่อมีรูปหลายสิบรูป

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

ทำไมต้องจำกัด parallelism? หากคุณเปิดเธรดมากเกินไปบนแล็ปท็อปที่สเปคปานกลาง คุณอาจเห็นการช้าลงแทนที่จะเร็วขึ้น การตั้งค่า `setMaxParallelism` ช่วยให้คุณสมดุลระหว่างความเร็วและความเสถียร

## ขั้นตอนที่ 4: เรียกใช้ Batch OCR

นี่คือหัวใจของ **how to batch OCR**: การเรียก `recognize` ครั้งเดียวที่คืนค่าเป็นรายการของ `RecognitionResult` หนึ่งอ็อบเจกต์ต่อหนึ่งรูปภาพ

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

เมธอดนี้จะบล็อกจนกว่าทุกรูปจะประมวลผลเสร็จ แล้วจึงส่งข้อความกลับมา หากคุณต้องการพฤติกรรมแบบ non‑blocking สามารถห่อไว้ใน `CompletableFuture` ได้ แต่สำหรับสคริปต์ส่วนใหญ่การเรียกแบบ synchronous ทำให้โค้ดดูเรียบร้อย

## ขั้นตอนที่ 5: พิมพ์ข้อความที่ดึงได้

สุดท้าย ให้วนลูปผลลัพธ์และแสดงสตริงที่จดจำได้ นี่แสดงให้เห็นว่าเราสามารถ **extract text from images** ในรูปแบบต่าง ๆ ได้สำเร็จ

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### ผลลัพธ์ที่คาดหวัง

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

หาก engine OCR ไม่สามารถอ่านไฟล์ได้ เมธอด `getText()` จะคืนสตริงว่าง ดังนั้นคุณสามารถเพิ่มการตรวจสอบง่าย ๆ เพื่อบันทึกคำเตือนได้

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือคลาส Java ที่พร้อมรัน เพียงคัดลอกไปไฟล์ชื่อ `BatchOcrTutorial.java` ปรับพาธรูปภาพ แล้วรัน `javac && java`

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

รันแล้วคุณจะเห็นคอนโซลพิมพ์ข้อความที่ดึงจากแต่ละไฟล์ PNG, JPG, และ TIFF—พอดีกับสิ่งที่คุณต้องการเมื่อ **how to batch OCR** เป็นคำถามในใจ

## คำถามที่พบบ่อย & กรณีขอบ

### ถ้ามีรูปภาพมากกว่าสามรูปจะทำอย่างไร?

แค่เพิ่มรายการลงใน `imageFiles` รายการ Batch Processor จะจัดสรรงานอัตโนมัติไปยังเธรดที่คุณตั้งค่าไว้ด้วย `setMaxParallelism`

### รูปภาพของฉันอยู่ในโฟลเดอร์ย่อย—ต้องระบุแต่ละไฟล์ด้วยตนเองหรือไม่?

คุณสามารถรวบรวมไฟล์ทั้งหมดด้วยนามสกุลที่ต้องการโดยโปรแกรมได้:

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

วิธีนี้ทำให้โค้ดยืดหยุ่นและยังคงสอดคล้องกับ **how to batch OCR**

### จะจัดการผลลัพธ์ที่ความเชื่อมั่นต่ำอย่างไร?

`RecognitionResult` มีเมธอด `getConfidence()` คุณสามารถกรองผลลัพธ์ที่ต่ำกว่าขีดจำกัดและลองใหม่ด้วย DPI ที่สูงขึ้น:

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR รองรับภาษาอื่นหรือไม่?

ใช่—แค่เรียก `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (หรือ enum ที่สนับสนุนอื่น) ก่อนเรียก `recognize` นี้ทำให้การ **extract text from images** มีความหลายภาษาได้จริง

## เคล็ดลับด้านประสิทธิภาพ

* **ขนาด batch มีผล** – Batch ขนาดใหญ่ลดค่าโอเวอร์เฮด แต่รายการยาวมากอาจใช้หน่วยความจำมากเกินไป ทดสอบกับ 50–200 รูปต่อ batch
* **Parallelism** – บน CPU 4‑core การตั้งค่า `setMaxParallelism(4)` มักให้ throughput ที่ดีที่สุด ปรับตามภาระงานของเซิร์ฟเวอร์ของคุณ
* **การเตรียมภาพล่วงหน้า** – แปลงภาพเป็น grayscale หรือเพิ่มคอนทราสต์ก่อน OCR สามารถเพิ่มความแม่นยำได้ โดยเฉพาะกับสแกนที่มีสัญญาณรบกวน

## สรุป

คุณได้เรียนรู้ **how to batch OCR** ใน Java ด้วย Aspose OCR, วิธี **extract text from images** ของรูปแบบต่าง ๆ, และเหตุผลที่การควบคุม parallelism มีความสำคัญ ตัวอย่างโค้ดเต็มแสดงการจดจำข้อความจากไฟล์ PNG, JPG, และ TIFF ด้วยการเรียกเดียวที่มีประสิทธิภาพ

พร้อมก้าวต่อไปหรือยัง? ลองนำผลลัพธ์ OCR ไปใส่ในดัชนีการค้นหา, ฐานข้อมูล, หรือแม้กระทั่ง AI summarizer คุณยังสามารถทดลองรับไฟล์ PDF (Aspose OCR รองรับ) หรือผสานกับไลบรารีการเตรียมภาพอย่าง OpenCV เพื่อความแม่นยำที่สูงขึ้น

ขอให้สนุกกับการเขียนโค้ด และจำไว้ว่า—batch OCR ไม่จำเป็นต้องเป็นปัญหา หากมีเครื่องมือที่เหมาะสมและรูปแบบที่ชัดเจน คุณก็จะเปลี่ยนกองรูปภาพเป็นข้อความที่ค้นหาได้ในเวลาอันสั้น

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
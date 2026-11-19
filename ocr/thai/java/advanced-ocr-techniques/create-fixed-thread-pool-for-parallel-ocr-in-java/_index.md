---
category: general
date: 2026-05-03
description: สร้าง fixed thread pool ใน Java เพื่อดึงข้อความจากภาพอย่างรวดเร็ว เรียนรู้วิธีรัน
  OCR, แปลงภาพเป็นข้อความ, และเพิ่มประสิทธิภาพด้วยการประมวลผล OCR แบบขนาน
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: th
og_description: สร้าง Fixed Thread Pool ใน Java เพื่อดึงข้อความจากภาพอย่างรวดเร็ว
  เรียนรู้วิธีรัน OCR แปลงภาพเป็นข้อความ และเพิ่มประสิทธิภาพด้วยการประมวลผล OCR แบบขนาน
og_title: สร้าง Fixed Thread Pool สำหรับ OCR แบบขนานใน Java
tags:
- Java
- OCR
- Multithreading
title: สร้าง Fixed Thread Pool สำหรับ OCR แบบขนานใน Java
url: /th/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Fixed Thread Pool สำหรับการทำ OCR แบบขนานใน Java

เคยต้องการ **สร้าง fixed thread pool** เพื่อเร่งความเร็วงาน OCR แต่ไม่แน่ใจว่าจะเริ่มจากตรงไหนหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการที่มีรูปภาพจำนวนมาก จุดคอขวดมักเป็นการเรียก OCR แบบ single‑threaded และวิธีแก้ก็ง่ายกว่าที่คิด: สร้าง pool ของ worker threads แล้วให้พวกมันประมวลผลไฟล์แบบขนาน  

ในบทแนะนำนี้ คุณจะได้เรียนรู้วิธี **ดึงข้อความจากรูปภาพ** ด้วย Aspose OCR, วิธี **รัน OCR** อย่างมีประสิทธิภาพ, และวิธี **แปลงรูปภาพเป็นข้อความ** โดยไม่ทำให้ CPU ของคุณทำงานหนักเกินไป เมื่อเสร็จคุณจะมีโปรแกรม Java ที่พร้อมรันซึ่งแสดง **การประมวลผล OCR แบบขนาน** บนรูปตัวอย่างไม่กี่รูป

## สิ่งที่คุณจะสร้าง

เราจะประกอบแอปคอนโซลเล็ก ๆ ที่:

* อ่านรายการเส้นทางของรูปภาพ (PNG, JPG, TIFF, BMP).
* **สร้าง fixed thread pool** ที่มีขนาดเท่ากับจำนวนคอร์ของ CPU.
* ส่งมอบงาน OCR สำหรับแต่ละรูปภาพ.
* รวบรวมข้อความที่ได้รับการจดจำและพิมพ์ออกที่คอนโซล.
* ปิด executor อย่างสะอาด.

ไม่มีเครื่องมือ build ภายนอก ไม่มีเฟรมเวิร์กหรูหรา—แค่ Java ธรรมดาและไลบรารี Aspose OCR หากคุณมี Java 8+ และ IDE ที่ดี คุณก็พร้อมแล้ว

## ข้อกำหนดเบื้องต้น

* **Java Development Kit (JDK) 8 หรือใหม่กว่า** – โค้ดใช้ lambda ดังนั้นเวอร์ชันเก่าจะไม่คอมไพล์.
* **Aspose OCR for Java** – ดาวน์โหลด JAR จากเว็บไซต์ Aspose หรือดึงผ่าน Maven (`com.aspose:aspose-ocr`).
* โฟลเดอร์ที่มีรูปทดสอบหลายไฟล์ (โค้ดชี้ไปที่ `YOUR_DIRECTORY`).  
* ความคุ้นเคยพื้นฐานกับการทำ concurrency ของ Java (เราจะอธิบายส่วนที่เหลือ).

> *เคล็ดลับ:* หากคุณใช้ Maven ให้เพิ่ม dependency ลงใน `pom.xml` ของคุณและให้ IDE จัดการ classpath ให้เอง.  

---

## ขั้นตอนที่ 1: เพิ่มการนำเข้า (Imports) ที่จำเป็น

ก่อนอื่น ให้นำเข้าคลาสที่เราต้องการใช้เข้ามาในสโคป นี่ไม่ใช่แค่โค้ดซ้ำซ้อน; แต่ละ import บอก JVM ว่าจะหา engine OCR, ยูทิลิตี้การจัดการรูปภาพ, และเครื่องมือ concurrency ที่ทำให้เราสามารถ **สร้าง fixed thread pool** ได้.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – API OCR หลัก.  
* `java.util.*` – คอลเลกชันสำหรับเก็บเส้นทางรูปภาพและผลลัพธ์.  
* `java.util.concurrent.*` – แพคเกจ concurrency ที่มี `ExecutorService` และ `Future`.

---

## ขั้นตอนที่ 2: กำหนดรายการรูปภาพที่ต้องประมวลผล

ต่อไป เราจะระบุไฟล์ที่ต้องการ **ดึงข้อความจากรูปภาพ** การใช้ `Arrays.asList` ทำให้โค้ดกระชับและให้คุณเปลี่ยนเป็นไดเรกทอรีของคุณเองได้โดยไม่ต้องแก้ไขส่วนอื่นของตรรกะ.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

เพิ่มรายการได้ตามต้องการ; pool ของเธรดจะปรับขนาดอัตโนมัติตามจำนวนคอร์ของ CPU ที่คุณมี.

---

## ขั้นตอนที่ 3: **สร้าง Fixed Thread Pool** ให้ตรงกับจำนวนคอร์ของ CPU

นี่คือหัวใจของบทแนะนำ เราถาม runtime ว่ามีคอร์กี่คอร์และขอให้ factory `Executors` สร้าง pool ที่มีขนาดเท่านั้น ทำไมต้อง fixed? เพราะจำนวนเธรดที่คาดเดาได้ช่วยป้องกันการ “ระเบิดเธรด” ที่อาจทำให้ OS ขาดแคลนทรัพยากร.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` คืนค่าจำนวนคอร์ลอจิก (รวม hyper‑threads).  
* `newFixedThreadPool(coreCount)` รับประกันว่าเราไม่เกินความสามารถของ CPU ซึ่งเป็นวิธีที่ปลอดภัยที่สุดในการ **รัน OCR** แบบขนาน.

---

## ขั้นตอนที่ 4: ส่งมอบงาน OCR สำหรับแต่ละรูปภาพ

ตอนนี้เราจะแปลงแต่ละเส้นทางไฟล์ให้เป็น callable ที่ **รัน OCR**, จดจำข้อความ, และคืนผลลัพธ์ เราจะสร้าง `OcrEngine` ใหม่ภายใน lambda เพื่อหลีกเลี่ยงการแชร์สถานะของ engine ที่ไม่ปลอดภัยต่อเธรด.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* การเรียก `submit` แต่ละครั้งจะส่ง lambda ไปยัง pool ซึ่งจะจัดตารางให้กับเธรดที่ว่าง.  
* วัตถุ `Future<String>` ทำให้เราสามารถดึงข้อความที่จดจำได้ในภายหลัง และรักษาลำดับได้หากต้องการ.

---

## ขั้นตอนที่ 5: ดึงและแสดงข้อความที่จดจำได้

เมื่อทุกงานถูกคิวแล้ว เราเพียงแค่วนลูปผ่านรายการ `Future` เรียก `get()` เพื่อบล็อกจนกว่าแต่ละงาน OCR จะเสร็จ นี่คือขั้นตอน **แปลงรูปภาพเป็นข้อความ** ที่คุณจะเห็น: การเรียก `engine.getText()` จะคืนสตริงดิบ.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซลเป็นแบบนี้:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

ถ้าไฟล์ล้มเหลว (เช่นไฟล์เสีย) คุณจะเห็นบรรทัดที่เริ่มด้วย `Failed:` ตามด้วยเส้นทาง—สะดวกสำหรับการดีบักอย่างรวดเร็ว.

---

## ขั้นตอนที่ 6: ทำความสะอาด Executor Service

อย่าลืมปิด pool; มิฉะนั้น JVM อาจค้างอยู่เพราะคิดว่ามีงานค้างอยู่ การปิดอย่างสุภาพทำให้งานที่กำลังทำอยู่เสร็จก่อนที่โปรเซสจะจบ.

```java
executor.shutdown();
```

คุณยังสามารถเรียก `awaitTermination` หากต้องการกำหนด timeout, แต่สำหรับยูทิลิตี้บรรทัดคำสั่งส่วนใหญ่ `shutdown()` ธรรมดาก็เพียงพอ.

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่พร้อมรัน คัดลอกและวางลงในไฟล์ชื่อ `ParallelOcrTutorial.java`, ปรับเส้นทางรูปภาพ, แล้วรัน `javac` + `java` ตามปกติ.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เนื้อหาข้อความของแต่ละรูปภาพจะถูกพิมพ์ออกที่คอนโซลตามลำดับเดียวกับรายการ `imagePaths`. หากรูปใดไม่สามารถประมวลผลได้ คุณจะเห็นข้อความแจ้งความล้มเหลวแทนบรรทัดว่าง.

---

## คำถามทั่วไป & กรณีขอบ

### ถ้าฉันมีรูปภาพมากกว่าจำนวนเธรด?

Fixed thread pool จะจัดคิวงานที่เหลือโดยอัตโนมัติ เมื่อเธรดหนึ่งทำงาน OCR เสร็จ มันจะรับงานต่อไป การจัดคิวนี้คือแก่นของ **การประมวลผล OCR แบบขนาน** — คุณจะได้อัตราการผ่านสูงสุดโดยไม่ทำให้ CPU ทำงานหนักเกินไป.

### ฉันสามารถเปลี่ยนภาษาได้หรือไม่?

ได้เลย. แทนที่ `engine.getLanguage().setEnglish(true);` ด้วยฟลักซ์ภาษาที่ต้องการ เช่น `setFrench(true)` หรือเปิดหลายภาษาโดยเรียก setter หลายครั้งก่อน `recognize()`.

### จะจัดการกับรูปภาพขนาดใหญ่มากอย่างไร?

ไฟล์ขนาดใหญ่สามารถใช้หน่วยความจำต่อเธรดมาก หากคุณเจอ `OutOfMemoryError` ให้ลองย่อขนาดรูปก่อนส่งให้ engine, หรือเพิ่มขนาด heap ด้วย `-Xmx`. อีกวิธีหนึ่งคือใช้ **cached thread pool** (` 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
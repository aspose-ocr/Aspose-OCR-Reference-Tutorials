---
category: general
date: 2026-02-17
description: เรียนรู้วิธีใช้ Fixed Thread Pool ของ Java เพื่อดึงข้อความจากภาพ PNG
  ด้วยการประมวลผล OCR แบบขนานและปิดบริการ Executor อย่างถูกต้อง
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: th
og_description: ค้นพบว่า pool เธรดคงที่ใน Java สามารถดึงข้อความจากภาพ PNG แบบขนาน
  แปลงข้อความจากหน้าสแกน และปิดบริการ executor อย่างปลอดภัยได้อย่างไร.
og_title: พูลเธรดคงที่ใน Java – OCR แบบขนานสำหรับ PNG
tags:
- java
- ocr
- multithreading
- aspose
title: พูลเธรดคงที่ใน Java – OCR ขนานสำหรับ PNG
url: /th/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – OCR ขนานสำหรับ PNG

เคยสงสัยไหมว่าจะเร่งความเร็วของ OCR บนไฟล์ PNG จำนวนมากอย่างไรด้วย **fixed thread pool java**? ในบทเรียนนี้เราจะอธิบายขั้นตอนการ **extract text from PNG** ภาพแบบขนาน, **convert scanned pages text** ให้เป็นสตริงที่แก้ไขได้, และการ **shut down executor service** อย่างปลอดภัยเมื่อทำงานเสร็จ

ถ้าคุณเคยมองลูปแบบ single‑threaded ที่ใช้เวลานานหลายนาที คุณคงรู้สึกหงุดหงิดกับการต้องรอให้แต่ละหน้าเสร็จก่อนหน้าถัดไปจะเริ่มทำงาน ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของ Java และ Aspose OCR คุณสามารถใช้พลังของทุกคอร์ CPU, แปลงหน้าที่สแกนเป็นข้อความที่ค้นหาได้, และทำให้แอปพลิเคชันของคุณตอบสนองได้อย่างต่อเนื่อง  

ด้านล่างนี้เป็นตัวอย่างที่พร้อมรันเต็มรูปแบบ พร้อมคำอธิบายว่าทำไมแต่ละส่วนจึงสำคัญ, ข้อผิดพลาดที่พบบ่อย, และเคล็ดลับที่คุณสามารถนำไปใช้กับไลบรารี OCR ใดก็ได้

---

## สิ่งที่คุณต้องมี

- **Java 17** (หรือ JDK เวอร์ชันใหม่) – โค้ดใช้ไวยากรณ์ `var` แบบจำกัด, แต่ยังทำงานได้บนเวอร์ชันเก่า  
- **Aspose.OCR for Java** library – สามารถดึงจาก Maven Central หรือดาวน์โหลด trial จาก Aspose  
- ชุดไฟล์ **PNG** ที่ต้องการประมวลผล – เช่น ใบเสร็จสแกน, หน้าหนังสือ, หรือสกรีนช็อต  
- ความคุ้นเคยพื้นฐานกับการทำ concurrency ของ Java – ไม่จำเป็นแต่จะช่วยได้

แค่นี้แหละ ไม่มีบริการภายนอก, ไม่มี Docker, เพียง Java ธรรมดาและการทำ multithreading เล็กน้อย

---

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR Dependency & License (Optional)

ก่อนอื่นให้แน่ใจว่า JAR ของ Aspose OCR อยู่ใน classpath ของคุณ หากใช้ Maven ให้เพิ่ม:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

หากไม่มี license ไลบรารีจะทำงานในโหมด evaluation; โค้ดทำงานเช่นเดิม เพื่อโหลด license (แนะนำสำหรับ production) ให้วางไฟล์ `Aspose.OCR.lic` ในโฟลเดอร์ resources แล้วใช้:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** เก็บไฟล์ license ไว้ด้านนอกระบบ version control เพื่อหลีกเลี่ยงการเปิดเผยโดยบังเอิญ

---

## ขั้นตอนที่ 2: สร้างอินสแตนซ์ `OcrEngine` ที่ Thread‑Safe

`OcrEngine` ของ Aspose OCR เป็น thread‑safe ตราบใดที่คุณใช้อินสแตนซ์เดียวกันหลายงาน การสร้างเพียงครั้งเดียวช่วยประหยัดหน่วยความจำและลดค่าใช้จ่ายจากการรี‑อินิชิอัลไจ engine สำหรับแต่ละภาพ

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

ทำไมต้อง reuse? คิดว่า engine เป็น worker ตัวหนักที่โหลดโมเดลภาษาเข้า memory การสร้าง engine ใหม่สำหรับแต่ละภาพเหมือนจ้างผู้เชี่ยวชาญใหม่ทุกงาน – แพงและไม่จำเป็น

---

## ขั้นตอนที่ 3: ตั้งค่า Fixed Thread Pool Java

ต่อไปคือส่วนสำคัญ: **fixed thread pool java** เราจะกำหนดขนาดให้เท่ากับจำนวน logical processor เพื่อให้ทุกคอร์ทำงานโดยไม่เกิดการ oversubscribe

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

การใช้ *fixed* pool (แทน cached) ให้การใช้ทรัพยากรคาดเดาได้และป้องกัน “out‑of‑memory” spikes เมื่อมีภาพหลายร้อยไฟล์มาพร้อมกัน

---

## ขั้นตอนที่ 4: ระบุไฟล์ PNG ที่ต้องการประมวลผล (Extract Text from PNG)

รวบรวมพาธของภาพที่ต้องการ OCR ในโปรเจคจริงคุณอาจสแกนโฟลเดอร์หรืออ่านจากฐานข้อมูล; ที่นี่เราจะ hard‑code ตัวอย่างไม่กี่ไฟล์

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Note:** ส่วนขยายไฟล์ **png** มีความสำคัญเพราะ Aspose OCR ตรวจจับฟอร์แมตอัตโนมัติ, แต่คุณก็สามารถใส่ JPEG หรือ TIFF ได้เช่นกัน

---

## ขั้นตอนที่ 5: ส่งงาน OCR – Parallel OCR Processing

แต่ละภาพจะกลายเป็น callable ที่คืนค่าข้อความที่จดจำได้ เนื่องจาก `OcrEngine` ถูกแชร์ เราแค่ส่งพาธไฟล์เข้าไปใน task

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

ทำไมต้องห่อใน `Future`? เพราะมันทำให้เราส่งงานทั้งหมดไปพร้อมกัน, แล้วค่อยเก็บผลลัพธ์ตามลำดับที่ส่ง – เหมาะกับการรักษาลำดับหน้าเมื่อ **convert scanned pages text** กลับเป็นเอกสาร

---

## ขั้นตอนที่ 6: ดึงผลลัพธ์และแสดง (Convert Scanned Pages Text)

ตอนนี้เรารอแต่ละ `Future` ให้เสร็จและพิมพ์ผลลัพธ์ `get()` จะบล็อกเฉพาะงานนั้นเท่านั้น, ไม่ใช่ทั้ง pool

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

ผลลัพธ์ที่แสดงบน console ปกติจะเป็นเช่นนี้:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

หากต้องการบันทึกผลลงไฟล์ ให้แทนที่ `System.out.println` ด้วย `Files.writeString`

---

## ขั้นตอนที่ 7: ปิด Executor Service อย่างสะอาด

เมื่อทุกงานเสร็จสิ้น จำเป็นต้อง **shut down executor service** มิฉะนั้น JVM อาจค้าง thread ที่ไม่ใช่ daemon ทำให้ไม่สามารถออกจากโปรแกรมได้อย่างราบรื่น

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

รูปแบบ `awaitTermination` ให้ pool มีโอกาสทำงานที่ค้างอยู่ให้เสร็จก่อนที่เราจะบังคับปิด การละเลยขั้นตอนนี้เป็นสาเหตุหลักของ memory leak ในแอปพลิเคชันที่ทำงานต่อเนื่อง

---

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกส่วนเข้าด้วยกัน นี่คือโปรแกรมสมบูรณ์ที่คุณสามารถคัดลอก‑วางลงใน `ParallelBatchDemo.java` แล้วรันได้:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
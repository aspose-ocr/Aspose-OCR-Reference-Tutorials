---
category: general
date: 2026-02-14
description: 'OCR รูปภาพแบบชุดทำได้ง่าย: เรียนรู้วิธีดึงข้อความจากไฟล์ PNG ด้วย Aspose
  OCR พร้อมการประมวลผลแบบขนานใน Java.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: th
og_description: บทเรียน OCR แบบกลุ่มแสดงวิธีการดึงข้อความจากไฟล์ PNG โดยใช้ API แบบอะซิงโครนัสของ
  Aspose OCR ใน Java.
og_title: การทำ OCR รูปภาพเป็นชุดใน Java – การสกัดข้อความ PNG อย่างรวดเร็ว
tags:
- Java
- OCR
- Aspose
- Image Processing
title: OCR รูปภาพแบบชุดใน Java – ดึงข้อความจากไฟล์ PNG อย่างรวดเร็ว
url: /th/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

"RTL formatting if needed" not needed.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR รูปภาพแบบชุดใน Java – ดึงข้อความจากไฟล์ PNG อย่างรวดเร็ว

เคยต้องการทำ **batch image OCR** บนโฟลเดอร์ที่มีไฟล์ PNG สแกน แต่กังวลเรื่องความเร็วหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการจริง—เช่น การแปลงใบแจ้งหนี้เป็นดิจิทัล, การเก็บรักษาหนังสือสแกน, หรือการประมวลผลใบเสร็จ—นักพัฒนาต้อง **extract text from PNG** อย่างรวดเร็วและเชื่อถือได้  

ข่าวดีคืออะไร? ด้วย Aspose OCR API แบบอะซิงโครนัส คุณสามารถสร้าง pipeline OCR ขนานได้เพียงไม่กี่บรรทัดของ Java ในบทแนะนำนี้ เราจะเดินผ่านโซลูชันที่ทำงานได้เต็มรูปแบบ, อธิบายเหตุผลของแต่ละส่วน, และแสดงวิธีตรวจสอบผลลัพธ์ สุดท้ายคุณจะได้โปรแกรมที่ทำงานอิสระซึ่งประมวลผลชุดไฟล์ PNG ทั้งหมดพร้อมกันและให้ผลลัพธ์เป็นข้อความที่สะอาดและตรวจสอบการสะกดแล้ว

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการลิสต์ไฟล์ PNG เพื่อทำ batch processing  
- การตั้งค่า Aspose `OcrEngine` สำหรับภาษาอังกฤษและการแก้ไขการสะกดคำ  
- การรัน OCR แบบอะซิงโครนัสด้วย `processAsync` และการจัดการผลลัพธ์ `Future`  
- การอ่านและแสดงข้อความที่ได้รับการจดจำสำหรับแต่ละภาพ  
- เคล็ดลับการขยายขนาด, การจัดการข้อผิดพลาด, และการปรับประสิทธิภาพ  

### ข้อกำหนดเบื้องต้น

- Java 8 หรือใหม่กว่า (โค้ดใช้แพ็กเกจมาตรฐาน `java.util.concurrent`)  
- ใบอนุญาต Asp Aspose OCR for Java หรือเวอร์ชันทดลองฟรี (ดาวน์โหลดจากเว็บไซต์ Aspose)  
- โฟลเดอร์ที่มีไฟล์ PNG สกรีนช็อตหรือหน้าสแกนที่ต้องการทดสอบ  

ตอนนี้มาเริ่มกันเลย

## Step 1 – Gather Your PNG Files for a Batch

ก่อนที่เครื่อง OCR จะทำงานใด ๆ มันต้องรู้ว่าต้องประมวลผลภาพใดบ้าง วิธีที่ง่ายที่สุดคือการสร้าง `List<String>` ของพาธไฟล์แบบ absolute หรือ relative

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**ทำไมจึงสำคัญ:**  
การสร้างรายการล่วงหน้าช่วยให้ engine สามารถกำหนดเวลาการประมวลผลแต่ละไฟล์ได้อย่างอิสระ ซึ่งเป็นพื้นฐานของการทำ batch processing ที่แท้จริง หากคุณต้องการสแกนไดเรกทอรีแบบไดนามิกในภายหลัง เพียงเปลี่ยน `Arrays.asList` แบบคงที่เป็นสตรีม `Files.walk`

## Step 2 – Initialise and Tune the Aspose OCR Engine

`OcrEngine` ของ Aspose สามารถตั้งค่าได้หลายอย่าง ที่นี่เราตั้งค่าภาษาเป็น English และเปิดการแก้ไขการสะกดคำ—สองตัวเลือกที่ช่วยปรับคุณภาพของข้อความที่สกัดออกมาอย่างมาก โดยเฉพาะจาก PNG ที่มีสัญญาณรบกวน

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**เหตุผลของการตั้งค่าเหล่านี้:**  
- **Language selection** บอก engine ว่าจะใช้ชุดอักขระและพจนานุกรมใด เพื่อลดการจดจำผิดพลาด  
- **Spell correction** จับข้อผิดพลาด OCR ที่พบบ่อย (เช่น “1” กับ “l”) โดยไม่ต้องทำ post‑process เอง  

> **Pro tip:** หากภาพของคุณมีหลายภาษา คุณสามารถส่งรายการเช่น `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)` ได้

## Step 3 – Fire Off Asynchronous Batch Processing

การทำงานหนักเกิดขึ้นใน `processAsync` ซึ่งจะคืนค่า `Future<List<OcrResult>>` ทำให้เธรดหลักของคุณสามารถทำงานอื่นต่อได้ขณะ OCR ทำงานในพื้นหลัง

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**ทำไมต้อง async:**  
การรัน OCR ทีละไฟล์แบบต่อเนื่องอาจช้าอย่างน่าเบื่อ—แต่ละ PNG อาจใช้เวลาหนึ่งวินาทีหรือมากกว่า โดยการมอบหมายงานให้ thread pool คุณจะใช้หลาย core ของ CPU และลดระยะเวลารวมอย่างมหาศาล

## Step 4 – Retrieve the Results When They’re Ready

เมื่อพร้อมจะใช้ผลลัพธ์ เพียงเรียก `get()` บน `Future` คำสั่งนี้จะบล็อกเฉพาะจนกว่า OCR จะเสร็จ แล้วจะคืนรายการ `OcrResult` ในลำดับเดียวกับรายการอินพุต

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**การจัดการ time‑outs:**  
หากต้องการหลีกเลี่ยงการบล็อกไม่สิ้นสุด ใช้ `ocrFuture.get(60, TimeUnit.SECONDS)` แล้วจับ `TimeoutException` เพื่อนำไปสู่การ fallback

## Step 5 – Display the Recognised Text for Each PNG

ตอนนี้คุณมีผลลัพธ์แล้ว ให้วนลูปและพิมพ์ข้อความที่สกัดออกมาพร้อมกับชื่อไฟล์ต้นฉบับ นี่คือขั้นตอนสุดท้ายของการ **extract text from PNG** ไฟล์

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**ตัวอย่างผลลัพธ์ที่คาดหวัง**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

หาก engine ไม่สามารถจดจำหน้าใดหน้าได้ `getText()` จะคืนสตริงว่าง—ควรตรวจสอบในโค้ด production เสมอ

## Full Working Example

ด้านล่างเป็นโปรแกรมเต็มที่พร้อมรัน ซึ่งรวมทุกส่วนเข้าด้วยกัน คัดลอกและวางลงในไฟล์ชื่อ `ParallelOcrDemo.java` แทนที่ `YOUR_DIRECTORY` ด้วยพาธโฟลเดอร์ PNG ของคุณ แล้วรัน `javac ParallelOcrDemo.java && java ParallelOcrDemo`

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Running the Demo

1. **Compile** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Execute** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

คุณควรเห็นชื่อไฟล์ PNG แต่ละไฟล์ตามด้วยข้อความที่สกัดออกมา แยกด้วยเครื่องหมายขีด  

> **Note:** หากพบ `LicenseException` ให้แน่ใจว่าโหลดใบอนุญาต Aspose ก่อนสร้าง engine:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Scaling Up – Tips for Real‑World Batch OCR

| Situation | Recommendation |
|-----------|----------------|
| **Hundreds of PNGs** | เพิ่มขนาด thread pool ด้วย `ocrEngine.setThreadPoolSize(8)` (หรือมากกว่าตามจำนวน core ของ CPU) |
| **Memory constraints** | ประมวลผลไฟล์เป็นชิ้นเล็ก ๆ (เช่น batch ขนาด 50) แล้วปล่อยรายการ `OcrResult` หลังแต่ละชิ้น |
| **Variable image quality** | เปิด `setPreprocessingOptions` เพื่อ auto‑rotate, deskew หรือเพิ่มความคอนทราสต์ก่อนจดจำ |
| **Multiple languages** | เรียก `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` และอาจตั้งพจนานุกรมกำหนดเอง |
| **Error handling** | ห่อ `ocrFuture.get()` ด้วย try‑catch สำหรับ `ExecutionException` เพื่อบันทึกไฟล์ที่ล้มเหลวโดยไม่หยุด batch ทั้งหมด |

กลยุทธ์เหล่านี้ช่วยให้ pipeline **batch image OCR** ของคุณคงทนแม้ชุดข้อมูลขยายใหญ่ขึ้น

## Frequently Asked Questions

**Q: Does this work with JPEG or TIFF files?**  
A: Absolutely. The `processAsync` method accepts any format supported by Aspose OCR (PNG, JPEG, TIFF, BMP, etc.). Just change the file extensions in your list.

**Q: What if I need to preserve layout (tables, columns)?**  
A: Aspose OCR provides a `getLayoutResult()` method that returns positional data. You can reconstruct tables by analyzing the bounding boxes of each word.

**Q: Can I run this on a serverless platform?**  
A: Yes—just package the JAR with the Aspose library and deploy to AWS Lambda, Azure Functions, or Google Cloud Functions. Remember to keep the function’s memory allocation high enough for the OCR thread pool.

## Conclusion

คุณมีโซลูชัน **batch image OCR** ที่ครบถ้วนและอิสระแล้ว ซึ่งสามารถ **extract text from PNG** ไฟล์ได้อย่างมีประสิทธิภาพด้วย Aspose OCR API แบบอะซิงโครนัสใน Java บทแนะนำนี้ครอบคลุมตั้งแต่การเตรียมรายการไฟล์, การตั้งค่าภาษาและการตรวจสอบการสะกด, การเปิดใช้งานการประมวลผลขนาน, การจัดการผลลัพธ์, และการขยาย pipeline สำหรับการใช้งานในระดับผลิต

พร้อมก้าวต่อไปหรือยัง? ลองเปลี่ยนภาษาเป็น French, ทดลองพจนานุกรมกำหนดเอง, หรือรวมผลลัพธ์เข้ากับ ElasticSearch ที่ค้นหาได้ การผสมผสาน OCR ชุดเร็วกับความสามารถของ Java concurrency ทำให้คุณทำได้ไม่มีขีดจำกัด

Happy coding, and may your text extraction be swift and spot‑on! 

![Diagram showing parallel OCR workers handling multiple PNG files](/images/batch-ocr-diagram.png){: .center alt="แผนภาพการประมวลผล OCR ขนานกับไฟล์ PNG หลายไฟล์"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
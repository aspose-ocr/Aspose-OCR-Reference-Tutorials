---
category: general
date: 2026-03-07
description: ทำ OCR บนภาพด้วย Java. เรียนรู้วิธีจดจำข้อความจากไฟล์ PNG, ดึงข้อความจากใบเสร็จ,
  และโหลดภาพสำหรับ OCR พร้อมตัวอย่าง Java OCR ที่สมบูรณ์.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: th
og_description: ทำ OCR บนรูปภาพด้วย Java คู่มือนี้แสดงวิธีจดจำข้อความจาก PNG, ดึงข้อความจากใบเสร็จ,
  และโหลดรูปภาพสำหรับ OCR ด้วยตัวอย่าง Java OCR ฉบับเต็ม.
og_title: รัน OCR บนรูปภาพด้วย Java – การสกัดข้อความด้วย GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: เรียกใช้ OCR บนภาพด้วย Java – การสกัดข้อความด้วย GPU
url: /th/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on Image with Java – GPU Powered Text Extraction

เคยต้อง **run OCR on image** แต่ไม่รู้ว่าจะเริ่มต้นอย่างไรใน Java หรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อต้องดึงข้อความจากใบเสร็จสแกนหรือภาพ PNG screenshot ครั้งแรก  

ในบทเรียนนี้เราจะพาคุณผ่าน **ตัวอย่าง Java OCR แบบครบวงจร** ที่ไม่เพียง **recognize text from PNG** เท่านั้น แต่ยังแสดงวิธี **extract text from receipt** พร้อมใช้การเร่งความเร็วด้วย GPU เพื่อความเร็วที่สูงขึ้น เมื่อจบคุณจะได้โปรแกรมที่พร้อมรัน โหลดภาพเพื่อ OCR ประมวลผล แล้วพิมพ์ผลลัพธ์เป็นข้อความธรรมดาออกมา

## What You’ll Learn

- วิธี **load image for OCR** ด้วย `ImageInputStream` อย่างง่าย
- การเปิดใช้งาน GPU เพื่อให้เอนจินทำงานเร็วขึ้นบนฮาร์ดแวร์สมัยใหม่
- ขั้นตอนที่แน่นอนในการ **recognize text from PNG** และดึงสตริงที่มีประโยชน์จากใบเสร็จ
- ข้อผิดพลาดทั่วไป (เช่น GPU device ID ผิด) และเคล็ดลับการปฏิบัติที่ดีที่สุด
- โค้ดเต็มที่สามารถรันได้ซึ่งคุณสามารถคัดลอก‑วางลงใน IDE ของคุณได้เลย

**Prerequisites**

- Java 17 หรือใหม่กว่า (โค้ดใช้คีย์เวิร์ด `var` เพื่อความกระชับ แต่คุณสามารถเปลี่ยนเป็นประเภทที่ระบุชัดเจนได้หากใช้ Java 8)
- ไลบรารี OCR ที่มีคลาส `OcrEngine`, `ImageInputStream`, และ `OcrResult` (เช่น *FastOCR* SDK สมมติ; แทนที่ด้วยไลบรารีที่คุณใช้จริง)
- เครื่องที่เปิดใช้งาน GPU หากต้องการเพิ่มประสิทธิภาพ (ไม่บังคับแต่แนะนำ)

---

## Step 1: Run OCR on Image – Enable GPU Acceleration

สิ่งแรกที่ต้องทำคือสร้าง OCR engine และบอกให้ใช้ GPU ขั้นตอนนี้สำคัญมาก เพราะหากไม่มีการสนับสนุน GPU เอนจินจะถอยกลับไปใช้ CPU ซึ่งจะช้ากว่ามากสำหรับใบเสร็จความละเอียดสูง

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Why this matters:**  
GPU acceleration ช่วยยกภาระการคำนวณเมทริกซ์หนักที่ OCR engine ทำออกจาก CPU หากคุณมี GPU หลายตัว สามารถเลือกตัวที่มีหน่วยความจำมากที่สุดได้โดยเปลี่ยนค่า `setGpuDeviceId` การลืมเปิด GPU เป็นสาเหตุทั่วไปของข้อร้องเรียน “ทำไม OCR ของฉันช้า?”

> **Pro tip:** หากเครื่องของคุณไม่มี GPU ที่เข้ากันได้ การเรียก `setUseGpu(true)` จะถูกละเว้นโดยไม่มีการขัดข้อง—แต่จะทำให้การประมวลผลช้าลงเท่านั้น

---

## Step 2: Load Image for OCR

เมื่อเอนจินพร้อมแล้ว เราต้องป้อนภาพให้มัน ตัวอย่างด้านล่างแสดงวิธีโหลดใบเสร็จ PNG ที่เก็บบนดิสก์ คุณสามารถเปลี่ยนเส้นทางเป็นรูปแบบไฟล์ใดก็ได้ที่ไลบรารี OCR ของคุณรองรับ

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Edge case:**  
หากไฟล์ไม่มีอยู่หรือเส้นทางผิด `ImageInputStream` จะโยน `IOException` ให้ห่อการเรียกในบล็อก try‑catch แล้วบันทึกข้อความที่เป็นประโยชน์:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Step 3: Recognize Text from PNG

เมื่อโหลดภาพแล้ว OCR engine สามารถทำงานของมันได้ ขั้นตอนนี้จะ **recognize text from PNG** (หรือรูปแบบที่รองรับอื่น) และคืนค่าเป็นอ็อบเจกต์ `OcrResult`

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**What’s happening under the hood?**  
เอนจินทำการพรี‑โปรเซส (deskew, binarization) รันเครือข่ายประสาทเทียมเพื่อจำแนกอักขระ แล้วประกอบเป็นบรรทัดข้อความ เนื่องจากเราเปิด GPU ไว้ การคำนวณเครือข่ายประสาทเทียมเหล่านี้จะทำบนการ์ดกราฟิก ทำให้ลดเวลาในการทำงานหลายวินาที

---

## Step 4: Extract Text from Receipt

หลังจากการจดจำแล้ว คุณมักต้องการเพียงข้อความดิบ คลาส `OcrResult` ปกติจะมีเมธอด `getText()` ที่คืนค่า `String` เดียว คุณสามารถทำ post‑process ต่อ (เช่น ใช้ regex ดึงยอดรวม, วันที่ ฯลฯ)

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Typical receipt output:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

ตอนนี้คุณสามารถส่งสตริงนี้ไปยังพาร์เซอร์ของคุณเองเพื่อดึงยอดรวม รายการสินค้า หรือข้อมูลภาษีได้

---

## Step 5: Full Java OCR Example – Ready to Run

รวมทุกอย่างเข้าด้วยกัน นี่คือ **complete Java OCR example** ที่คุณสามารถวางลงในไฟล์ `Main.java` อย่าลืมเพิ่มไลบรารี OCR ลงใน classpath

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Expected console output** (สมมติใช้ใบเสร็จตัวอย่างข้างบน):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

หากผลลัพธ์ดูเป็นอักขระแปลก ๆ ให้ตรวจสอบว่าภาพชัดเจน (DPI สูง) และว่าแพ็คเกจภาษาของ OCR ตรงกับภาษาของใบเสร็จหรือไม่

---

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| *What if my GPU isn’t detected?* | เอนจินจะถอยกลับไปใช้ CPU โดยอัตโนมัติ ตรวจสอบไดรเวอร์และให้แน่ใจว่า `setGpuDeviceId` ตรงกับอุปกรณ์ที่มีอยู่ (`nvidia-smi` บน Linux สามารถช่วยได้) |
| *Can I process JPEG or TIFF files?* | ใช่—แค่เปลี่ยนส่วนขยายไฟล์ใน `ImageInputStream` ไลบรารี OCR ส่วนใหญ่จะตรวจจับรูปแบบโดยอัตโนมัติ |
| *Is there a way to batch‑process many receipts?* | ห่อโค้ดการจดจำในลูปและใช้อินสแตนซ์ `OcrEngine` เดียวกัน; การรี‑อินิชิอไลซ์ต่อภาพจะทำให้ใช้หน่วยความจำ GPU มากเกินไป |
| *How do I improve accuracy on low‑contrast receipts?* | พรี‑โปรเซสภาพก่อนส่งให้ OCR (เพิ่มคอนทราสต์, แปลงเป็น grayscale) บางไลบรารีมี API `preprocess` ให้ใช้ |

---

## Conclusion

คุณได้เรียนรู้ **how to run OCR on image** ด้วย Java ตั้งแต่การโหลดภาพจนถึงการดึงข้อความที่สะอาดจากใบเสร็จ บทเรียนนี้ครอบคลุม **recognize text from PNG**, **extract text from receipt**, และแสดง **java OCR example** ที่คุณสามารถปรับใช้กับโปรเจกต์ใดก็ได้  

ขั้นตอนต่อไป? ลองปิด GPU flag เพื่อดูความแตกต่างของประสิทธิภาพ ทดลองกับความละเอียดภาพต่าง ๆ หรือรวมพาร์เซอร์ที่ใช้ regex เพื่อดึงยอดรวมโดยอัตโนมัติ หากสนใจหัวข้อขั้นสูงเพิ่มเติม ให้มองหา **OCR post‑processing**, **language model correction**, หรือ **batch processing pipelines**  

Happy coding, and may your receipts always be readable!  

![ตัวอย่างการ run OCR บนภาพ](/images/run-ocr-on-image.png "run OCR on image – ตัวอย่าง Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
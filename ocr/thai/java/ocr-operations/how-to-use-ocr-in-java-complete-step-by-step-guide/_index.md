---
category: general
date: 2026-02-22
description: วิธีใช้ OCR ใน Java เพื่อดึงข้อความจากภาพ ปรับปรุงความแม่นยำของ OCR และโหลดภาพสำหรับ
  OCR พร้อมตัวอย่างโค้ดที่ใช้งานได้จริง
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: th
og_description: วิธีใช้ OCR ใน Java เพื่อดึงข้อความจากภาพและปรับปรุงความแม่นยำของ
  OCR. ปฏิบัติตามคำแนะนำนี้เพื่อรับตัวอย่างที่พร้อมใช้งาน
og_title: วิธีใช้ OCR ใน Java – คู่มือขั้นตอนเต็มรูปแบบ
tags:
- OCR
- Java
- Image Processing
title: วิธีใช้ OCR ใน Java – คู่มือขั้นตอนโดยละเอียด
url: /th/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน Java – คู่มือขั้นตอนเต็ม

เคยต้องการ **how to use OCR** บนภาพหน้าจอที่เอียงและสงสัยว่าทำไมผลลัพธ์ถึงดูเป็นอักษรไร้ความหมาย? คุณไม่ได้เป็นคนเดียว ในแอปพลิเคชันจริงหลาย ๆ อย่าง—การสแกนใบเสร็จ, การแปลงฟอร์มเป็นดิจิทัล, หรือการดึงข้อความจากมส์—การได้ผลลัพธ์ที่เชื่อถือได้ขึ้นอยู่กับการตั้งค่าไม่กี่อย่างง่าย ๆ.

ในบทแนะนำนี้เราจะพาคุณผ่านขั้นตอน **how to use OCR** เพื่อ *extract text from image* ไฟล์, แสดงวิธี **improve OCR accuracy**, และสาธิตวิธีที่ถูกต้องในการ **load image for OCR** ด้วยไลบรารี OCR ของ Java ที่เป็นที่นิยม เมื่อจบคุณจะมีโปรแกรมที่พร้อมใช้งานซึ่งสามารถนำไปใส่ในโครงการใดก็ได้.

## สิ่งที่คุณจะได้เรียนรู้

- โค้ดที่แม่นยำที่คุณต้องการสำหรับ **load image for OCR** (ไม่มีการพึ่งพาที่ซ่อนอยู่)
- ธงการเตรียมข้อมูลล่วงหน้าที่ช่วยเพิ่ม **improve OCR accuracy** และเหตุผลที่สำคัญ
- วิธีอ่านผลลัพธ์ OCR และพิมพ์ออกที่คอนโซล
- ข้อผิดพลาดทั่วไป—เช่นลืมตั้งค่าพื้นที่สนใจหรือไม่ทำการลดสัญญาณรบกวน—และวิธีหลีกเลี่ยง

### ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับ JDK ล่าสุดใดก็ได้)
- ไลบรารี OCR ที่มีคลาส `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput` และ `OcrResult` (เช่นแพ็กเกจสมมติ `com.example.ocr` ที่ใช้ในตัวอย่าง) ให้แทนที่ด้วยไลบรารีจริงที่คุณใช้
- ภาพตัวอย่าง (`skewed_noisy.png`) ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงได้

> **เคล็ดลับ:** หากคุณใช้ SDK เชิงพาณิชย์ ตรวจสอบให้ไฟล์ไลเซนส์อยู่ใน classpath; มิฉะนั้นเอนจินจะโยนข้อผิดพลาดการเริ่มต้น

---

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ของ OCR Engine – **how to use OCR** อย่างมีประสิทธิภาพ

สิ่งแรกที่คุณต้องการคืออ็อบเจ็กต์ `OcrEngine` คิดว่าเป็นสมองที่จะตีความพิกเซล

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*ทำไมเรื่องนี้สำคัญ:* หากไม่มีเอนจินคุณจะไม่มีบริบทสำหรับโมเดลภาษา, ชุดอักขระ, หรืออัลกอริทึมภาพ การสร้างมันตั้งแต่ต้นยังทำให้คุณสามารถแนบตัวเลือกการเตรียมข้อมูลล่วงหน้าในภายหลังได้

---

## ขั้นตอนที่ 2: ตั้งค่าการเตรียมภาพ – **improve OCR accuracy**

การเตรียมข้อมูลล่วงหน้าเป็นซอสลับลับที่ทำให้การสแกนที่มีสัญญาณรบกวนกลายเป็นข้อความที่สะอาดและอ่านได้โดยเครื่อง ด้านล่างเราจะเปิดใช้งาน deskew, การลดสัญญาณรบกวนระดับสูง, auto‑contrast, และพื้นที่สนใจ (ROI) เพื่อโฟกัสส่วนที่เกี่ยวข้องของภาพ

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*ทำไมเรื่องนี้สำคัญ:*  
- **Deskew** ปรับแนวข้อความที่หมุน, ซึ่งจำเป็นเมื่อสแกนใบเสร็จที่ไม่เรียบเรียงอย่างสมบูรณ์  
- **Noise reduction** ลบพิกเซลรบกวนที่อาจถูกตีความเป็นอักขระ  
- **Auto‑contrast** ขยายช่วงโทนสี ทำให้ตัวอักษรที่จางขึ้นเด่นชัดขึ้น  
- **ROI** บอกเอนจินให้ละเว้นขอบที่ไม่เกี่ยวข้อง, ประหยัดเวลาและหน่วยความจำ  

หากคุณข้ามขั้นตอนใดขั้นตอนหนึ่ง คุณอาจเห็นผลลัพธ์ **improve OCR accuracy** ลดลง

---

## ขั้นตอนที่ 3: โหลดภาพสำหรับ OCR – **load image for OCR** อย่างถูกต้อง

ตอนนี้เราจะชี้เอนจินไปที่ไฟล์ที่ต้องการอ่าน คลาส `OcrInput` สามารถรับหลายภาพได้ แต่ในตัวอย่างนี้เราจะทำให้เรียบง่าย

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*ทำไมเรื่องนี้สำคัญ:* เส้นทางต้องเป็นแบบ absolute หรือ relative ต่อไดเรกทอรีทำงาน; มิฉะนั้นเอนจินจะโยน `FileNotFoundException`. นอกจากนี้ ชื่อเมธอด `add` บ่งบอกว่าคุณสามารถคิวหลายภาพได้—สะดวกสำหรับการประมวลผลเป็นชุด

---

## ขั้นตอนที่ 4: ทำ OCR และแสดงข้อความที่รู้จำ – **how to use OCR** แบบครบวงจร

สุดท้าย เราขอให้เอนจินทำการรู้จำข้อความและพิมพ์ออก `OcrResult` มีสตริงดิบ, คะแนนความมั่นใจ, และเมตาดาต้ารายบรรทัด (หากคุณต้องการใช้ในภายหลัง)

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าภาพตัวอย่างมีข้อความ “Hello, OCR World!”):

```
=== OCR Output ===
Hello, OCR World!
```

หากผลลัพธ์ดูเป็นอักษรผสม, กลับไปที่ขั้นตอน 2 และปรับตัวเลือกการเตรียมข้อมูลล่วงหน้า—อาจลดระดับการลดสัญญาณรบกวนหรือปรับสี่เหลี่ยม ROI

---

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรม Java ที่สมบูรณ์ซึ่งคุณสามารถคัดลอก‑วางลงในไฟล์ชื่อ `OcrDemo.java`. มันรวมทุกขั้นตอนที่เราได้อธิบายไว้

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

บันทึกไฟล์, คอมไพล์ด้วย `javac OcrDemo.java`, และรัน `java OcrDemo`. หากทุกอย่างตั้งค่าอย่างถูกต้อง คุณจะเห็นข้อความที่สกัดออกมาพิมพ์ที่คอนโซล

---

## คำถามทั่วไป & กรณีขอบ

| Question | Answer |
|----------|--------|
| **ถ้าภาพของฉันเป็นรูปแบบ JPEG จะทำอย่างไร?** | เมธอด `OcrInput.add()` ยอมรับรูปแบบ raster ที่รองรับทั้งหมด—PNG, JPEG, BMP, TIFF. เพียงเปลี่ยนส่วนขยายไฟล์ในเส้นทาง |
| **ฉันสามารถประมวลผลหลายหน้าในครั้งเดียวได้ไหม?** | ได้เลย. เรียก `ocrInput.add()` สำหรับแต่ละไฟล์, แล้วส่ง `ocrInput` เดียวกันไปยัง `recognize()`. เอนจินจะคืนค่า `OcrResult` ที่ต่อเนื่องกัน |
| **ถ้าผลลัพธ์ OCR ว่างเปล่าจะทำอย่างไร?** | ตรวจสอบให้แน่ใจว่า ROI มีข้อความจริง ๆ. อีกทั้งตรวจสอบว่า `setDeskewEnabled(true)` เปิดอยู่; การหมุน 90° จะทำให้เอนจินคิดว่าภาพว่าง |
| **ฉันจะเปลี่ยนโมเดลภาษาอย่างไร?** | ไลบรารีส่วนใหญ่มีเมธอด `setLanguage(String)` บน `OcrEngine`. เรียกก่อน `recognize()`, เช่น `ocrEngine.setLanguage("eng")`. |
| **มีวิธีรับคะแนนความมั่นใจหรือไม่?** | มี, `OcrResult` มักให้ `getConfidence()` ต่อบรรทัดหรืออักขระ. ใช้เพื่อกรองผลลัพธ์ที่ความมั่นใจต่ำ |

---

## สรุป

เราได้ครอบคลุม **how to use OCR** ใน Java ตั้งแต่ต้นจนจบ: การสร้างเอนจิน, การตั้งค่าการเตรียมข้อมูลล่วงหน้าเพื่อ **improve OCR accuracy**, การ **load image for OCR** อย่างถูกต้อง, และสุดท้ายการพิมพ์ข้อความที่สกัดออกมา. โค้ดเต็มพร้อมรันแล้ว, และคำอธิบายตอบคำถาม “ทำไม” ของแต่ละบรรทัด

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเปลี่ยนสี่เหลี่ยม ROI เพื่อโฟกัสส่วนต่าง ๆ ของภาพ, ทดลองกับ `NoiseReduction.MEDIUM`, หรือรวมผลลัพธ์เข้าเป็น PDF ที่ค้นหาได้. คุณยังสามารถสำรวจหัวข้อที่เกี่ยวข้องเช่น **extract text from image** ด้วยบริการคลาวด์, หรือประมวลผลเป็นชุดหลายพันไฟล์ด้วยคิวหลายเธรด

มีคำถามเพิ่มเติมเกี่ยวกับ OCR, การเตรียมภาพ, หรือการรวม Java? แสดงความคิดเห็นได้เลย, และขอให้สนุกกับการเขียนโค้ด! 

![ตัวอย่างการใช้ OCR](/images/ocr-demo.png "how to use OCR – ตัวอย่าง Java แสดงการเตรียมข้อมูลและผลลัพธ์")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
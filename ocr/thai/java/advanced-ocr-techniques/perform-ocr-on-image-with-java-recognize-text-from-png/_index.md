---
category: general
date: 2026-03-28
description: ทำการ OCR บนภาพโดยใช้ Aspose OCR ใน Java. เรียนรู้วิธีจดจำข้อความจากไฟล์
  PNG และปรับปรุงความแม่นยำของ OCR ด้วยการแก้ไขการสะกดในตัว.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- read image text
- improve OCR accuracy
- Aspose OCR Java
- spell correction OCR
language: th
og_description: ทำการ OCR บนภาพด้วย Aspose OCR สำหรับ Java คู่มือนี้แสดงวิธีการจดจำข้อความจากไฟล์
  PNG และปรับปรุงความแม่นยำของ OCR ภายในไม่กี่นาที
og_title: ทำ OCR บนรูปภาพด้วย Java – คู่มือฉบับสมบูรณ์
tags:
- OCR
- Java
- Aspose
- Image Processing
title: ทำ OCR บนภาพด้วย Java – แยกข้อความจาก PNG
url: /th/java/advanced-ocr-techniques/perform-ocr-on-image-with-java-recognize-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพด้วย Java – จดจำข้อความจาก PNG

เคยต้องการ **ทำ OCR บนรูปภาพ** แต่ผลลัพธ์กลับเป็นข้อความที่อ่านไม่ออกหรือเปล่า? คุณไม่ได้เป็นคนเดียว—การสแกนที่มีเสียงรบกวน, PNG ที่คอนทราสต์ต่ำ, และฟอนต์แปลก ๆ สามารถทำให้เอกสารที่สะอาดกลายเป็นกลุ่มอักขระที่ยุ่งยาก  

ในคู่มือนี้เราจะพาคุณผ่านตัวอย่าง Java ที่สมบูรณ์และพร้อมรันที่ใช้ Aspose OCR เพื่อ **จดจำข้อความจาก PNG** และเราจะสาธิตวิธี **ปรับปรุงความแม่นยำของ OCR** ด้วยฟีเจอร์การแก้ไขการสะกดของไลบรารี เมื่อเสร็จสิ้นคุณจะสามารถ **อ่านข้อความจากรูปภาพ** ได้อย่างเชื่อถือได้ แม้แหล่งข้อมูลจะไม่สมบูรณ์ก็ตาม

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่า Aspose OCR สำหรับ Java ในโครงการ Maven  
- ขั้นตอนที่แน่นอนเพื่อ **ทำ OCR บนรูปภาพ** ตั้งแต่การโหลดไฟล์จนถึงการสกัดข้อความที่สะอาด  
- ทำไมการเปิดใช้งานการแก้ไขการสะกดจึงสามารถเพิ่มคุณภาพของผลลัพธ์ได้อย่างมาก  
- ปัญหาที่พบบ่อย (ไฟล์หาย, ฟอร์แมตที่ไม่รองรับ) และวิธีจัดการอย่างราบรื่น  
- ตัวอย่างโค้ดเต็มที่คัดลอก‑วาง‑พร้อมใช้ที่คุณสามารถรันได้ทันที

### ข้อกำหนดเบื้องต้น

- Java 8 หรือใหม่กว่า ติดตั้งบนเครื่องของคุณ  
- Maven สำหรับการจัดการ dependency (IDE ใดก็ได้ที่รองรับ Maven ก็พอ)  
- รูป PNG ที่มีข้อความบางส่วนที่อ่านได้ — ควรเป็นรูปที่มีเสียงรบกวนบ้างเพื่อให้เห็นประโยชน์ของการแก้ไขการสะกด

> **เคล็ดลับ:** หากคุณไม่มี PNG อยู่ในมือ ให้จับภาพหน้าจอของเอกสารหรือถ่ายรูปป้ายใดป้ายหนึ่ง ยิ่ง “เสียงรบกวน” มากเท่าไหร่ คุณก็จะยิ่งชื่นชมการเพิ่มความแม่นยำได้มากเท่านั้น

---

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR Dependency

สิ่งแรกที่ต้องทำ — เพิ่มไลบรารี Aspose OCR ลงใน `pom.xml` ของคุณ บรรทัดเดียวนี้จะดึงเวอร์ชันล่าสุด (ณ มีนาคม 2026) และจัดการ dependency ทั้งหมดที่เกี่ยวข้อง

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **ทำไมจึงสำคัญ:** หากไม่มีไลบรารีคุณจะไม่สามารถสร้าง `OcrEngine` ได้ และกระบวนการ **ทำ OCR บนรูปภาพ** ทั้งหมดจะล้มเหลวในขณะรัน

---

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine

การสร้าง engine ทำได้ง่าย แต่มีเหตุผลสำคัญที่ควรแยกการเริ่มต้นออกจากการเรียกจดจำ: จะทำให้คุณมีที่สำหรับปรับตั้งค่าต่าง ๆ เช่น ภาษา, DPI หรือที่สำคัญที่สุดสำหรับเรา คือการแก้ไขการสะกด

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {

    public static void main(String[] args) {
        try {
            // Step 2: Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Pro tip: you can set the language here if you need something other than English
            // ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

สังเกตคอมเมนต์ — การตั้งค่าภาษาอาจช่วยชีวิตคุณได้เมื่อ PNG ของคุณมีอักขระที่ไม่ใช่ภาษาอังกฤษ  

---

## ขั้นตอนที่ 3: เปิดใช้งาน Spell Correction เพื่อ **ปรับปรุงความแม่นยำของ OCR**

Aspose OCR มาพร้อมโมดูลการแก้ไขการสะกดในตัวที่ทำงานคล้ายพจนานุกรมเบา ๆ การเปิดใช้งานเพียงบรรทัดเดียวเท่านั้น แต่ผลกระทบต่อผลลัพธ์สุดท้ายอาจใหญ่โต โดยเฉพาะกับภาพที่มีเสียงรบกวน

```java
            // Step 3: Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);
```

> **ถ้าคุณไม่ต้องการใช้?** เพียงตั้งค่า flag เป็น `false` การปิดใช้งานอาจเป็นประโยชน์สำหรับข้อความเฉพาะโดเมนที่พจนานุกรมอาจมองคำที่ถูกต้องว่าเป็นข้อผิดพลาด

---

## ขั้นตอนที่ 4: โหลดและจดจำ PNG

ตอนนี้เราจะ **อ่านข้อความจากรูปภาพ** จากไฟล์จริง ๆ เมธอด `recognizeImage` รับพาธเป็นสตริง แต่คุณก็สามารถส่ง `java.io.InputStream` ได้หากดึงรูปจากฐานข้อมูลหรือเว็บ

```java
            // Step 4: Perform OCR on the input image
            String imagePath = "YOUR_DIRECTORY/noisy-image.png"; // replace with your actual path
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

หากไฟล์ไม่พบ Aspose จะโยน exception ที่อธิบายรายละเอียดให้คุณ — ไม่จำเป็นต้องตรวจสอบ `File.exists()` ด้วยตนเอง อย่างไรก็ตาม การห่อเมธอดใน `try/catch` (เช่นที่ทำในตัวอย่าง) จะให้ข้อความข้อผิดพลาดที่ชัดเจนต่อผู้ใช้ปลายทาง

---

## ขั้นตอนที่ 5: แสดงข้อความที่แก้ไขแล้ว

สุดท้าย พิมพ์ผลลัพธ์ออกที่คอนโซล ในแอปจริงคุณอาจบันทึกลงฐานข้อมูลหรือส่งต่อให้บริการอื่น ๆ แต่คอนโซลก็เพียงพอสำหรับการสาธิตอย่างรวดเร็ว

```java
            // Step 5: Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่า PNG มีประโยค “Aspose OCR library” พร้อมเสียงรบกวน):

```
Corrected text:
Aspose OCR library
```

หากคุณปิดการแก้ไขการสะกด คุณอาจเห็นอย่างเช่น “Asp0se OCR libr@ry” — นี่คือเหตุผลที่ **ปรับปรุงความแม่นยำของ OCR** มีความสำคัญ

---

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์ – ระบบ **อ่านข้อความจากรูปภาพ** จริงหรือไม่?

อาจอยากเชื่อผลลัพธ์จากคอนโซลโดยไม่ตั้งข้อสงสัย แต่การตรวจสอบอย่างง่าย ๆ สามารถประหยัดเวลาหลายชั่วโมงต่อมา นี่คือวิธีตรวจสอบข้อความที่สกัดได้:

1. **ตรวจสอบความยาว** – เปรียบเทียบ `ocrResult.getText().length()` กับจำนวนอักขระที่คาดหวัง  
2. **ค้นหาคำสำคัญ** – ใช้ `String.contains("Aspose")` เพื่อให้แน่ใจว่าคำหลักปรากฏอยู่  
3. **Unit test** – หากคุณนำโค้ดนี้ไปรวมกับระบบใหญ่ ให้เขียน JUnit test ที่ตรวจสอบว่าผลลัพธ์ตรงกับค่าที่รู้ล่วงหน้า

```java
// Example sanity check
if (ocrResult.getText().contains("Aspose")) {
    System.out.println("✅ Text successfully read from image.");
} else {
    System.out.println("⚠️ Unexpected OCR result – consider tweaking settings.");
}
```

---

## กรณีขอบเขตทั่วไป & วิธีจัดการ

| สถานการณ์ | สาเหตุ | วิธีแก้เร็ว |
|-----------|--------|-------------|
| **ไฟล์ไม่พบ** | พาธผิดหรือไม่มีสิทธิ์เข้าถึง | ตรวจสอบ `imagePath` และใช้ `Files.isReadable(Paths.get(imagePath))` ก่อนเรียก `recognizeImage` |
| **ฟอร์แมตไม่รองรับ** | Aspose OCR รองรับ PNG, JPEG, BMP, TIFF ฯลฯ | แปลงรูปเป็น PNG ก่อน (เช่นด้วย ImageIO) หรือใช้ `ocrEngine.recognizeImage(InputStream)` |
| **DPI ต่ำมาก** | OCR ต้องการอย่างน้อย ~300 DPI เพื่อความแม่นยำที่ดี | ขยายภาพด้วย `BufferedImage` และ `Graphics2D` ก่อนส่งให้ engine |
| **ศัพท์เฉพาะโดเมน** | การแก้ไขการสะกดอาจแทนที่คำที่ถูกต้องด้วยคำในพจนานุกรม | ปิดการแก้ไขการสะกด (`setEnableSpellCorrection(false)`) หรือใส่พจนานุกรมกำหนดเองผ่าน `ocrEngine.getRecognitionSettings().setCustomDictionary(...)` |

---

## ตัวอย่างทำงานเต็ม (คัดลอก‑วาง‑พร้อมใช้)

ด้านล่างเป็นไฟล์ซอร์สทั้งหมด พร้อมคอมไพล์และรัน แค่เปลี่ยน `YOUR_DIRECTORY/noisy-image.png` ให้เป็นพาธของรูปทดสอบของคุณ

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) {
        try {
            // Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);

            // Path to the PNG you want to process
            String imagePath = "YOUR_DIRECTORY/noisy-image.png";

            // Perform OCR on the input image
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

            // Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());

            // Simple verification that we actually read image text
            if (ocrResult.getText().toLowerCase().contains("aspose")) {
                System.out.println("✅ OCR succeeded – key term found.");
            } else {
                System.out.println("⚠️ OCR may need tweaking – key term missing.");
            }
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

รันด้วยคำสั่ง:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectExample
```

คุณควรเห็น **ข้อความที่แก้ไขแล้ว** แสดงบนคอนโซล ยืนยันว่าคุณได้ **ทำ OCR บนรูปภาพ** สำเร็จแล้ว

---

## สรุปภาพรวม

![Perform OCR on image example](/images/ocr-example.png){alt="ทำ OCR บนรูปภาพ – ก่อนและหลังการแก้ไขการสะกด"}

ภาพหน้าจอแสดง PNG ที่มีเสียงรบกวนด้านซ้ายและผลลัพธ์ที่สะอาดพร้อมการแก้ไขการสะกดด้านขวา

---

## สรุป

เราได้เดินผ่านโซลูชันครบวงจรจากต้นจนจบเพื่อ **ทำ OCR บนรูปภาพ** ด้วย Aspose OCR สำหรับ Java โดยการเปิดใช้ฟีเจอร์การแก้ไขการสะกดในตัว คุณสามารถ **ปรับปรุง

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
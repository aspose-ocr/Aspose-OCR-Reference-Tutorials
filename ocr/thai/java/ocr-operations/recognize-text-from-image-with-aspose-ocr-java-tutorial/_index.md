---
category: general
date: 2026-02-17
description: เรียนรู้วิธีจดจำข้อความจากภาพและโหลดภาพสำหรับ OCR ด้วยไลบรารี Aspose
  OCR Java คู่มือแบบขั้นตอนพร้อมตัวแก้ไขการสะกดคำ
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: th
og_description: จดจำข้อความจากภาพด้วย Aspose OCR Java การสอนนี้แสดงวิธีโหลดภาพสำหรับ
  OCR, เปิดการแก้ไขการสะกดคำ, และส่งออกข้อความที่สะอาด.
og_title: การจดจำข้อความจากภาพ – คู่มือ Aspose OCR Java ฉบับสมบูรณ์
tags:
- Java
- OCR
- Aspose
title: แยกข้อความจากภาพด้วย Aspose OCR – บทเรียน Java
url: /th/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากรูปภาพด้วย Aspose OCR – Java Tutorial

เคยต้องการ **จดจำข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าจะเลือกไลบรารีใดใช่ไหม? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—เช่น การสแกนใบแจ้งหนี้, การแปลงโน้ตมือเป็นดิจิทัล, หรือการดึงคำบรรยายจากภาพหน้าจอ—การได้ผลลัพธ์ OCR ที่แม่นยำเป็นสิ่งสำคัญ  

ในคู่มือนี้เราจะอธิบายขั้นตอนการโหลดรูปภาพสำหรับ OCR, เปิดใช้งาน spell corrector ในตัวของ Aspose OCR, และสุดท้ายพิมพ์ข้อความที่ทำความสะอาดแล้วออกมา เมื่อเสร็จคุณจะมีโปรแกรม Java ที่พร้อมรันและ **จดจำข้อความจากรูปภาพ** เพียงไม่กี่บรรทัดของโค้ด

## สิ่งที่บทเรียนนี้ครอบคลุม

- วิธีนำใบอนุญาต Aspose OCR ของคุณเข้าไปใช้ (เพื่อให้ตัวอย่างทำงานโดยไม่มีลายน้ำ)  
- การสร้างอินสแตนซ์ `OcrEngine` และเลือกภาษาอังกฤษเป็นภาษาการจดจำ  
- **โหลดรูปภาพสำหรับ OCR** ด้วย `OcrInput` และชี้ไปที่ไฟล์ PNG ที่มีคำสะกดผิด  
- การเปิดใช้งาน spell‑corrector พร้อมกับการระบุพจนานุกรมแบบกำหนดเอง (ถ้าต้องการ)  
- การรันการจดจำและพิมพ์ผลลัพธ์ที่ได้รับการแก้ไข  

ไม่มีบริการภายนอก, ไม่มีไฟล์กำหนดค่าที่ซ่อนอยู่—แค่ Java ธรรมดาและ JAR ของ Aspose OCR

> **เคล็ดลับ:** หากคุณใหม่กับ Aspose, ดาวน์โหลดใบอนุญาตทดลองใช้ฟรี 30‑วันจากเว็บไซต์ Aspose แล้ววางไฟล์ `.lic` ลงในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ดได้

## ข้อกำหนดเบื้องต้น

- Java 8 หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ JDK 11 ด้วย)  
- Aspose.OCR for Java JAR อยู่ใน classpath ของคุณ  
- ไฟล์ `Aspose.OCR.lic` ที่ถูกต้อง (หรือคุณสามารถรันในโหมดประเมินผลได้, แต่ตัวอย่างจะมีลายน้ำ)  
- ไฟล์รูปภาพ (`misspelled.png`) ที่มีข้อความพร้อมข้อผิดพลาดการสะกดโดยเจตนา—เหมาะสำหรับดูการทำงานของ spell corrector  

พร้อมหรือยัง? ดี—มาเริ่มกันเลย

## ขั้นตอน 1: นำใบอนุญาต Aspose OCR ไปใช้

ก่อนที่เอนจินจะทำงานหนัก, มันต้องรู้ว่าคุณมีใบอนุญาตแล้ว มิฉะนั้นคุณจะเห็นแบนเนอร์ “Trial version” ในผลลัพธ์

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*ทำไมขั้นตอนนี้สำคัญ:* การกำหนดใบอนุญาตจะปิดลายน้ำเวอร์ชันทดลองและเปิดพจนานุกรม spell‑corrector เต็มรูปแบบ การข้ามขั้นตอนนี้ก็ทำได้, แต่ผลลัพธ์ของคุณจะเต็มไปด้วยข้อความ “Aspose OCR Demo”

## ขั้นตอน 2: สร้างและกำหนดค่า OCR Engine

ตอนนี้เราจะสตาร์ทเอนจินและบอกให้มันใช้ภาษาอะไร ภาษาอังกฤษเป็นภาษาที่ใช้บ่อยที่สุด, แต่ Aspose รองรับหลายสิบภาษา

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*ทำไมต้องตั้งค่าภาษา:* โมเดลภาษาเป็นตัวกำหนดชุดอักขระและมีผลต่อคำแนะนำของ spell‑corrector การใช้ภาษาที่ไม่ตรงอาจทำให้ความแม่นยำลดลงอย่างมาก

## ขั้นตอน 3: เปิดใช้งาน Spell Correction และ (ถ้าต้องการ) ระบุพจนานุกรมแบบกำหนดเอง

Aspose OCR มาพร้อมพจนานุกรมภาษาอังกฤษในตัว, แต่คุณสามารถใส่ของคุณเองได้หากมีคำเฉพาะด้าน (เช่น คำศัพท์ทางการแพทย์หรือรหัสสินค้า)

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*สิ่งที่ตัวแก้ไขทำ:* เมื่อเอนจิน OCR พบคำที่ไม่มีในพจนานุกรม, มันจะพยายามแทนที่ด้วยคำที่ใกล้เคียงที่สุด นี่คือเหตุผลที่ตัวอย่างสามารถเปลี่ยน “recieve” เป็น “receive” ได้โดยอัตโนมัติ

## ขั้นตอน 4: โหลดรูปภาพสำหรับ OCR

นี่คือส่วนที่ตอบคำถาม **โหลดรูปภาพสำหรับ OCR** โดยตรง เราจะสร้างอ็อบเจ็กต์ `OcrInput` แล้วเพิ่มไฟล์ PNG ของเราเข้าไป

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*ทำไมต้องใช้ `OcrInput`:* มันทำหน้าที่แยกความซับซ้อนของการอ่านไฟล์และให้คุณเพิ่มหลายหน้าได้ในภายหลัง หากต้องการประมวลผล PDF หลายหน้า หรือชุดรูปภาพหลายไฟล์

## ขั้นตอน 5: รันการจดจำและดึงข้อความที่แก้ไขแล้วออกมา

เอนจินจะทำงานหนักในขั้นตอนนี้—จดจำอักขระ, ใช้โมเดลภาษา, และสุดท้ายแก้ไขการสะกด

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*ผลลัพธ์ที่คาดหวัง:* สมมติว่า `misspelled.png` มีประโยค “Ths is a smple test”, คอนโซลจะพิมพ์:

```
Corrected text:
This is a simple test
```

สังเกตว่าคำที่สะกดผิด (`Ths`, `smple`) ถูกแก้ไขโดยอัตโนมัติแล้ว

## ตัวอย่างเต็มพร้อมรัน

ด้านล่างเป็นโปรแกรมทั้งหมดในบล็อกเดียว คัดลอก‑วาง, ปรับเส้นทางไฟล์, แล้วกด **Run**

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**เคล็ดลับ:** หากต้องการประมวลผล JPEG หรือ BMP แทน PNG เพียงเปลี่ยนนามสกุลไฟล์—Aspose OCR รองรับรูปแบบ raster ทั่วไปทั้งหมด

## คำถามที่พบบ่อย & กรณีขอบ

- **ถ้ารูปภาพของฉันความละเอียดต่ำล่ะ?**  
  เพิ่ม DPI ก่อนส่งให้ Aspose โดยปรับขนาดด้วยไลบรารีเช่น `java.awt.Image` DPI ที่สูงจะให้พิกเซลมากขึ้นกับเอนจิน, ซึ่งมักทำให้ความแม่นยำดีขึ้น

- **ฉันสามารถจดจำหลายภาษาในรูปเดียวกันได้ไหม?**  
  ทำได้. เรียก `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` และอาจเพิ่มรายการภาษาผ่าน `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);`

- **พจนานุกรมที่กำหนดเองของฉันไม่ทำงาน—ทำไม?**  
  ตรวจสอบให้แน่ใจว่าโฟลเดอร์มีไฟล์ข้อความธรรมดาที่มีหนึ่งคำต่อบรรทัดและเส้นทางเป็นแบบ absolute หรือ relative อย่างถูกต้องต่อไดเรกทอรีทำงานของคุณ

- **จะดึงคะแนนความเชื่อมั่นออกมาอย่างไร?**  
  `result.getConfidence()` คืนค่า float ระหว่าง 0 และ 1 สำหรับหน้าเต็ม. สำหรับความเชื่อมั่นต่ออักขระ, สำรวจ `result.getWordList()`

## สรุป

คุณได้เรียนรู้วิธี **จดจำข้อความจากรูปภาพ** ด้วย Aspose OCR สำหรับ Java, วิธี **โหลดรูปภาพสำหรับ OCR**, และวิธีเปิดใช้งาน spell‑corrector เพื่อทำความสะอาดข้อผิดพลาดทั่วไป ตัวอย่างเต็มด้านบนพร้อมใส่ลงในโปรเจกต์ Maven หรือ Gradle ใดก็ได้, และด้วยการปรับเล็กน้อยคุณสามารถขยายให้ประมวลผลหลายโฟลเดอร์, เชื่อมต่อกับเว็บเซอร์วิส, หรือรวมกับระบบจัดการเอกสารได้

พร้อมก้าวต่อไปหรือยัง? ลองใส่ PDF หลายหน้า, ทดลองพจนานุกรมแบบกำหนดเองสำหรับศัพท์เฉพาะอุตสาหกรรม, หรือเชื่อมต่อผลลัพธ์กับ API แปลภาษา ความเป็นไปได้ไม่มีที่สิ้นสุด, และรูปแบบหลัก—license → engine → language → spell‑corrector → input → recognize → output—ยังคงเหมือนเดิม

ขอให้เขียนโค้ดสนุก, และขอให้ผลลัพธ์ OCR ของคุณแม่นยำเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
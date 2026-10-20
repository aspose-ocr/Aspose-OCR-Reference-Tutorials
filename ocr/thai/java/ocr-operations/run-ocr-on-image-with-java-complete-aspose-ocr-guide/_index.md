---
category: general
date: 2026-02-09
description: ใช้ Aspose OCR ใน Java เพื่อทำ OCR บนภาพ – เรียนรู้วิธีดึงข้อความจากไฟล์
  PNG และเปิดใช้งานการตรวจจับภาษาอัตโนมัติของ OCR เพียงไม่กี่ขั้นตอน.
draft: false
keywords:
- run OCR on image
- extract text from PNG
- auto detect language OCR
- Aspose OCR Java
- Hindi OCR example
language: th
og_description: ทำ OCR บนภาพได้ทันที. คู่มือนี้แสดงวิธีการดึงข้อความจากไฟล์ PNG และเปิดใช้งานการตรวจจับภาษาอัตโนมัติของ
  OCR ด้วย Aspose OCR สำหรับ Java.
og_title: เรียกใช้ OCR บนรูปภาพด้วย Java – คู่มือ Aspose OCR ฉบับเต็ม
tags:
- OCR
- Java
- Aspose
title: เรียกใช้ OCR บนภาพด้วย Java – คู่มือ Aspose OCR ฉบับสมบูรณ์
url: /th/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เรียกใช้ OCR บนรูปภาพด้วย Java – คู่มือ Aspose OCR ฉบับสมบูรณ์

เคยต้องการ **ทำ OCR บนรูปภาพ** ไฟล์แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? บางทีคุณอาจมีภาพ PNG สกรีนช็อตหลายภาพที่มีข้อความภาษาฮินดีและสงสัยว่า Java สามารถดึงคำออกมาได้หรือไม่โดยไม่ต้องตั้งค่า machine‑learning ขนาดใหญ่ ข่าวดีคือ: คุณทำได้และมันง่ายกว่าที่คิดด้วย Aspose OCR.

ในบทแนะนำนี้ เราจะเดินผ่านตัวอย่างจริงที่ **ดึงข้อความจาก PNG** ไฟล์, แสดงวิธีเปิดใช้งาน **auto detect language OCR**, และให้โปรแกรม Java ที่พร้อมรัน. เมื่อจบคุณจะมีโค้ดสั้นที่พิมพ์อักขระฮินดีลงคอนโซลและคุณจะเข้าใจว่าทำไมแต่ละบรรทัดจึงสำคัญ.

## สิ่งที่คุณต้องการ

- **Java Development Kit (JDK) 8** หรือใหม่กว่า – โค้ดจะคอมไพล์ได้กับเวอร์ชันล่าสุดใดก็ได้.  
- **Aspose.OCR for Java** library – ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์ Aspose หรือ Maven Central.  
- ภาพตัวอย่าง (`hindi_sample.png`) ที่มีสคริปต์ Devanagari – คุณสามารถสร้างได้ด้วยเครื่องมือจับภาพใดก็ได้.  
- IDE หรือโปรแกรมแก้ไขข้อความง่าย – ฉันใช้ IntelliJ IDEA แต่ `javac` ธรรมดาก็ใช้ได้ดี.

ไม่มีบริการภายนอก ไม่มีคีย์ API ของคลาวด์ เพียง JAR ภายในเครื่องและรูปภาพเดียวเท่านั้น ง่ายใช่ไหม?

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ลงในโปรเจกต์ของคุณ

แรกสุด ตรวจสอบให้แน่ใจว่า JAR ของ Aspose OCR อยู่ใน classpath ของคุณ หากคุณใช้ Maven ให้เพิ่ม dependency นี้:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

หากคุณชอบวิธีแบบแมนนวล ให้ดาวน์โหลด `aspose-ocr-23.10.jar` แล้ววางไว้ในโฟลเดอร์ `libs/` จากนั้นคอมไพล์ด้วย:

```bash
javac -cp "libs/*" LanguageExample.java
```

> **เคล็ดลับ:** เก็บหมายเลขเวอร์ชันของ JAR ไว้ในคอมเมนต์ที่ด้านบนของไฟล์ซอร์สของคุณ – จะช่วยให้คุณในอนาคตจำได้ว่าคุณใช้ API ใด

## ขั้นตอนที่ 2: สร้างอินสแตนซ์ของ OCR Engine

ตอนนี้เราจะสร้างอ็อบเจกต์หลักที่ทำงานหนักทั้งหมด คิดว่า `OcrEngine` คือสมองของกระบวนการนี้.

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

ทำไมต้องสร้างที่นี่? Engine จะเก็บการตั้งค่าการกำหนดค่า (เช่น ภาษา) และทรัพยากรที่ใช้ซ้ำได้ ดังนั้นการสร้างเพียงครั้งเดียวต่อแอปพลิเคชันจะลดภาระ.

## ขั้นตอนที่ 3: ตั้งค่าการกำหนดภาษ (และเปิดใช้งาน Auto‑Detect)

หากคุณรู้ภาษาล่วงหน้า—เช่น ฮินดี—คุณสามารถบอก engine ให้โฟกัสที่ Devanagari ซึ่งจะเพิ่มความแม่นยำและเร่งการประมวลผล.

```java
// Step 3a: Force Hindi (Devanagari) recognition
ocrEngine.getConfiguration().setLanguage(Language.HINDI);

// Step 3b (optional): Let the engine guess the language if you're unsure
ocrEngine.getConfiguration().setAutoDetectLanguage(true);
```

บรรทัด `setAutoDetectLanguage(true)` คือสวิตช์ **auto detect language OCR**. เมื่อคุณป้อนภาพที่มีหลายภาษา engine จะพยายามระบุสคริปต์แต่ละตัวโดยอัตโนมัติ ซึ่งสะดวกสำหรับงานแบชที่คุณไม่สามารถแท็กไฟล์แต่ละไฟล์ด้วยตนเอง.

## ขั้นตอนที่ 4: เรียกใช้ OCR บนภาพ PNG

นี่คือจุดที่เราจริง ๆ **ทำ OCR บนรูปภาพ** ข้อมูล. เมธอด `recognize` รับพาธไฟล์, อ่านบิตแมพ, และคืนค่า `RecognitionResult`.

```java
// Step 4: Perform OCR on the PNG file
RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");
```

แทนที่ `YOUR_DIRECTORY` ด้วยพาธโฟลเดอร์จริง. หากไฟล์ไม่พบ Aspose จะโยน exception ที่ชัดเจน – ไม่ต้องเดาว่าทำไมจึงล้มเหลวในภายหลัง.

## ขั้นตอนที่ 5: ดึงและแสดงข้อความที่สกัดออกมา

สุดท้าย ดึงสตริงที่ได้รับการจดจำออกจากอ็อบเจกต์ผลลัพธ์และพิมพ์ออกมา. สำหรับฮินดี คุณจะเห็นอักขระ Unicode ในคอนโซล หากเทอร์มินัลของคุณรองรับ UTF‑8.

```java
// Step 5: Output the recognized Hindi text
System.out.println("Hindi text:");
System.out.println(result.getText());
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าภาพตัวอย่างมีข้อความ “नमस्ते दुनिया”):

```
Hindi text:
नमस्ते दुनिया
```

หากคุณเปิดใช้งาน auto‑detect และภาพมีภาษาอังกฤษด้วย ผลลัพธ์จะรวมสคริปต์ทั้งสองอย่างผสมผสานอย่างสวยงาม.

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และสามารถรันได้ คัดลอก‑วางลงใน `LanguageExample.java` ปรับพาธรูปภาพ แล้วคุณพร้อมใช้งาน.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to be recognized (Hindi – Devanagari script)
        ocrEngine.getConfiguration().setLanguage(Language.HINDI);

        // Step 3: (Optional) Enable automatic fallback to language detection
        ocrEngine.getConfiguration().setAutoDetectLanguage(true);

        // Step 4: Run OCR on the input image
        RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");

        // Step 5: Print the extracted Hindi text
        System.out.println("Hindi text:");
        System.out.println(result.getText());
    }
}
```

> **หมายเหตุ:** หากคุณใช้ IDE ตรวจสอบให้แน่ใจว่าเส้นทางการสร้างของโปรเจกต์รวม JAR ของ Aspose OCR ไว้ ใน IntelliJ ไปที่ *File → Project Structure → Libraries* แล้วเพิ่ม JAR ที่นั่น.

## คำถามทั่วไปและกรณีขอบ

### ถ้าภาพ PNG ของฉันมีความละเอียดต่ำ?

ความแม่นยำของ OCR ลดลงอย่างมากเมื่อความละเอียดต่ำกว่า 150 dpi. ปรับขนาดภาพด้วยเครื่องมือเช่น ImageMagick (`convert input.png -resize 200% output.png`) ก่อนส่งให้ engine. ธง `auto detect language OCR` ยังทำงานอยู่ แต่คุณจะเห็นการจดจำผิดน้อยลง.

### ฉันสามารถประมวลผลหลายภาพในลูปได้หรือไม่?

แน่นอน. ห่อเมธอด `recognize` ไว้ในลูป `for` และใช้อินสแตนซ์ `OcrEngine` เดียวกันซ้ำ. การใช้ engine ซ้ำจะหลีกเลี่ยงการโหลดโมเดลภาษาใหม่ในแต่ละรอบ ซึ่งช่วยประหยัดหน่วยความจำและเวลา CPU.

```java
String[] files = {"img1.png", "img2.png", "img3.png"};
for (String file : files) {
    RecognitionResult r = ocrEngine.recognize(file);
    System.out.println("Text from " + file + ":");
    System.out.println(r.getText());
}
```

### ฉันจะจัดการกับคอนโซลที่ไม่รองรับ Unicode อย่างไร?

หากเทอร์มินัลของคุณแสดงสัญลักษณ์ผิดรูป ให้ตั้งค่าการเข้ารหัสไฟล์เป็น UTF‑8 เมื่อคุณเรียกใช้ Java:

```bash
java -Dfile.encoding=UTF-8 -cp "libs/*" LanguageExample
```

### มีวิธีใดบ้างที่จะได้คะแนนความเชื่อมั่น?

มี. `RecognitionResult` มีเมธอด `getConfidence()` ที่คืนค่า float ระหว่าง 0 ถึง 1 สำหรับแต่ละบรรทัดที่จดจำได้ คุณสามารถวนลูป `result.getLines()` เพื่อดึงค่าต่าง ๆ — มีประโยชน์สำหรับการกรองผลลัพธ์ที่ความเชื่อมั่นต่ำ.

## เคล็ดลับสำหรับการใช้งานใน Production

- **Cache language models**: หากคุณประมวลผลภาพหลายพันภาพ ให้คง engine อยู่ตลอดชุดงาน.  
- **Parallel processing**: ห่อแต่ละภาพใน `Callable` แล้วส่งให้ thread pool. เพียงจำไว้ว่า engine ไม่ปลอดภัยต่อการทำงานหลายเธรด; สร้างหนึ่งอินสแตนซ์ต่อเธรด.  
- **Logging**: ใช้ logger ที่เหมาะสม (SLF4J) แทน `System.out.println` สำหรับงานขนาดใหญ่.  
- **Memory management**: เรียก `ocrEngine.dispose()` หลังจากเสร็จเพื่อปล่อยทรัพยากรเนทีฟ.

## ภาพรวมเชิงภาพ

![แผนภาพตัวอย่างการ Run OCR บนภาพ](ocr_flow.png "แผนภาพตัวอย่างการ Run OCR บนภาพ")

แผนภาพด้านบนแสดงกระบวนการ: **run OCR on image → language configuration → auto detect language OCR (optional) → extract text from PNG**.

## สรุป

เราเพิ่งสาธิตวิธี **run OCR on image** ไฟล์โดยใช้ Aspose OCR สำหรับ Java, วิธี **extract text from PNG** ด้วยการตั้งค่าที่เจาะจงภาษา, และวิธีสลับ **auto detect language OCR** สำหรับสถานการณ์หลายภาษาแบบยืดหยุ่น ตัวอย่างโค้ดเต็มพร้อมคัดลอก, คอมไพล์, และรัน—ไม่มีขั้นตอนที่ซ่อนอยู่, ไม่มีบริการภายนอก.

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองเปลี่ยน `Language.HINDI` เป็น `Language.AUTO` แล้วป้อนเอกสารที่มีหลายสคริปต์, หรือทดลองใช้อินพุต PDF (Aspose OCR ยังรองรับ PDF). คุณยังสามารถรวมสคริปต์นี้เข้าไปใน Spring Boot REST endpoint เพื่อเปิดให้ OCR เป็นบริการเว็บได้.

ขอให้เขียนโค้ดอย่างสนุกสนานและภาพของคุณอ่านได้เสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
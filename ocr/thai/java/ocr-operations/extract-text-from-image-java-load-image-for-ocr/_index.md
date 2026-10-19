---
category: general
date: 2026-04-29
description: ดึงข้อความจากรูปภาพด้วย Java และ Aspose OCR – เรียนรู้วิธีโหลดรูปภาพสำหรับ
  OCR และจดจำข้อความจากใบเสร็จในรูปแบบ JSON.
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: th
og_description: ดึงข้อความจากภาพด้วย Java และ Aspose OCR. บทเรียนนี้แสดงวิธีโหลดภาพเพื่อ
  OCR และจดจำข้อความจากใบเสร็จ พร้อมส่งออกเป็น JSON.
og_title: การดึงข้อความจากภาพด้วย Java – คู่มือฉบับสมบูรณ์
tags:
- Java
- OCR
- Aspose
title: ดึงข้อความจากภาพใน Java – โหลดภาพสำหรับ OCR
url: /th/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extract text from image java – คู่มือฉบับสมบูรณ์

เคยต้องการ **extract text from image java** แต่ไม่แน่ใจว่าจะเลือกไลบรารีใดใช่ไหม? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาจำนวนมากเจออุปสรรคเมื่อพยายาม **load image for OCR** แล้วได้ข้อความดิบในรูปแบบที่ยากต่อการใช้งาน  

ในบทแนะนำนี้ เราจะพาไปผ่านโซลูชันที่สะอาดและครบวงจร ซึ่งไม่เพียงแต่ **load image for OCR** แต่ยัง **recognize text from receipt** และส่งออกเป็นสตริง JSON ที่เป็นระเบียบ เมื่อจบคุณจะได้คลาส Java ที่พร้อมรันซึ่งสามารถใส่ลงในโปรเจกต์ใดก็ได้—ไม่ต้องปรับแต่งเพิ่มเติม

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่า Aspose OCR for Java (ไลบรารีที่ทำงานหนักให้เป็นเรื่องง่าย)  
- ขั้นตอนที่แน่นอนในการ **load image for OCR** จากดิสก์  
- วิธีกำหนดค่าเอนจินให้ส่งผลลัพธ์เป็น JSON ซึ่งเหมาะสำหรับการประมวลผลต่อเนื่อง  
- วิธี **recognize text from receipt** ภาพและตรวจสอบผลลัพธ์  

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose มาก่อน; เพียงแค่มี JDK ที่ทำงานได้และ IDE ที่คุณคุ้นเคย

## ข้อกำหนดเบื้องต้น

| Requirement | Why it matters |
|-------------|----------------|
| **Java 17+** (or any recent JDK) | Aspose OCR มีไบนารีที่คอมไพล์ไว้สำหรับรันไทม์ Java สมัยใหม่ |
| **Maven or Gradle** (to pull the Aspose OCR dependency) | ทำให้การจัดการ dependencies ง่ายดาย |
| **A sample receipt image** (e.g., `receipt.png`) | เราจะใช้ไฟล์นี้เพื่อสาธิต **recognize text from receipt** |
| **Internet connection** (once) | จำเป็นต้องดาวน์โหลด Aspose JAR ครั้งแรก |

ถ้าคุณมีทั้งหมดแล้ว เยี่ยม—มาเริ่มกันเลย

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ลงในโปรเจกต์ของคุณ

สิ่งแรกที่คุณต้องการคือไลบรารี Aspose OCR หากคุณใช้ Maven ให้เพิ่มโค้ดสแนปพท์ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

สำหรับ Gradle จะเป็นแบบนี้:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **เคล็ดลับ:** ควบคุมหมายเลขเวอร์ชัน การอัปเกรดในภายหลังอาจทำให้เกิดการเปลี่ยนแปลง API ที่ละเอียดอ่อนซึ่งทำให้โค้ดของคุณพัง

เมื่อ dependencies ถูกจัดการแล้ว คุณพร้อมที่จะเขียนโค้ด Java ที่จริง ๆ แล้ว **extract text from image java**

## ขั้นตอนที่ 2: โหลดภาพสำหรับ OCR

ต่อไปเราจะแสดงบรรทัดที่แน่นอนสำหรับการ **load image for OCR** Aspose มี helper `ImageStream.fromFile` ที่สะดวก

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

แทนที่ `YOUR_DIRECTORY` ด้วยพาธแบบ absolute หรือ relative ไปยังไฟล์ใบเสร็จของคุณ หากพาธผิด เอนจินจะโยน `FileNotFoundException` ดังนั้นตรวจสอบการสะกดให้ถูกต้อง

> **ทำไมเรื่องนี้สำคัญ:** การโหลดภาพอย่างถูกต้องเป็นพื้นฐาน หากภาพไม่ถูกอ่าน เอนจิน OCR จะไม่มีอะไรให้จดจำและคุณจะได้ผลลัพธ์ JSON ว่างเปล่า

## ขั้นตอนที่ 3: บอกเอนจินให้ส่งผลลัพธ์เป็น JSON

Aspose OCR สามารถส่งผลลัพธ์เป็น XML, plain text หรือ JSON สำหรับ API สมัยใหม่ JSON เป็นรูปแบบที่ยืดหยุ่นที่สุด ดังนั้นเราจะตั้งค่ารูปแบบอย่างชัดเจน

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

คุณสามารถสลับเป็น `OcrResultFormat.XML` ด้วยการแก้ไขเพียงบรรทัดเดียว หากระบบต่อไปของคุณต้องการ XML API ถูกออกแบบให้สลับกันได้

## ขั้นตอนที่ 4: เรียกกระบวนการจดจำ

เมื่อโหลดภาพและตั้งค่ารูปแบบแล้ว ขั้นตอนต่อไปคือการ **recognize text from receipt** จริง ๆ นี่คือจุดที่ทำงานหนักเกิดขึ้น

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

คำสั่ง `recognize()` จะบล็อกจนกว่าเอนจินจะวิเคราะห์ภาพเสร็จ สำหรับภาพขนาดใหญ่คุณอาจต้องรันใน background thread แต่สำหรับใบเสร็จทั่วไปจะเสร็จในเศษวินาที

## ขั้นตอนที่ 5: ดึงผลลัพธ์ JSON

สุดท้าย เราจะดึงสตริง JSON ดิบและพิมพ์ออกมา สตริงนี้ประกอบด้วยข้อความที่จดจำได้ทั้งหมด, bounding box, คะแนนความมั่นใจ, และอื่น ๆ

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมเต็มกับใบเสร็จที่ชัดเจนจะให้ผลลัพธ์ประมาณนี้:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

สังเกตว่าทุกบรรทัดของใบเสร็จเป็นบล็อกแยกกันพร้อมคะแนนความมั่นใจ ตอนนี้คุณสามารถส่ง JSON นี้ไปยังระบบต่อไปใดก็ได้—เก็บในฐานข้อมูล, ส่งผ่าน HTTP, หรือป้อนให้โมเดล machine‑learning

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นคลาส Java ที่สมบูรณ์และทำงานอิสระซึ่งรวมทุกอย่างเข้าด้วยกัน คัดลอกวาง, ปรับพาธภาพ, แล้วรัน `mvn compile exec:java` (หรือคำสั่ง Gradle ที่เทียบเท่า)

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **ระวัง:**  
> • **ข้อผิดพลาดของพาธไฟล์** – ตรวจสอบเครื่องหมายสแลชบน Windows vs. macOS/Linux อีกครั้ง  
> • **Out‑of‑memory** – ภาพขนาดใหญ่อาจต้องใช้ `ocrEngine.setMemoryOptimization(true)`  
> • **การตั้งค่าภาษา** – หากใบเสร็จของคุณมีอักขระที่ไม่ใช่ละติน ให้เรียก `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (หรือภาษาใดที่รองรับ) ก่อน `recognize()`

## การทดสอบโซลูชัน

1. **Run the program** – คุณควรเห็น JSON blob แสดงบนคอนโซล  
2. **Validate the JSON** – คัดลอกผลลัพธ์ไปยัง <https://jsonlint.com/> เพื่อยืนยันว่าเป็นรูปแบบที่ถูกต้อง  
3. **Parse it** – ในโปรเจกต์จริงคุณอาจใช้ไลบรารีเช่น Jackson หรือ Gson เพื่อแมป JSON ไปยัง POJO เพื่อการจัดการที่ง่ายขึ้น  

หากคุณพบว่า `pages` array ว่างเปล่า สาเหตุที่พบบ่อยคือ: ไม่พบไฟล์ภาพ หรือภาพเบลอเกินกว่าการตั้งค่าเริ่มต้นของเอนจิน ในกรณีหลังลองเพิ่ม DPI หรือทำขั้นตอนการประมวลผลล่วงหน้า (เช่น binarization) ก่อนส่งให้ Aspose

## ความแปรผันและกรณีขอบ

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน |
|----------|----------------|
| **Multiple pages** (เช่น PDF หลายหน้าแปลงเป็นภาพ) | วนลูปแต่ละภาพ, เรียก `ocrEngine.setImage(...)` ภายในลูป, และรวมผลลัพธ์ JSON |
| **Different output format** | สลับ `OcrResultFormat.JSON` กับ `OcrResultFormat.XML` หรือ `OcrResultFormat.PLAIN_TEXT` |
| **Performance tuning** | ใช้ `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)` เพื่อความเร็ว, หรือ `OcrRecognitionMode.ACCURATE` เพื่อคุณภาพ |
| **Non‑receipt documents** | ปรับ `ocrEngine.getPageSegmentationSettings().setDetectTables(true)` หากต้องการสกัดตาราง |

## สรุป

เราได้อธิบายวิธีที่กระชับและพร้อมใช้งานในระดับ production เพื่อ **extract text from image java** ด้วย Aspose OCR โดยทำตามห้าขั้นตอน—สร้างเอนจิน, **load image for OCR**, ตั้งค่าการส่งออกเป็น JSON, **recognize text from receipt**, และสุดท้ายอ่าน JSON—คุณสามารถผสาน OCR เข้ากับแบ็กเอนด์ Java ใดก็ได้โดยไม่มีความยุ่งยาก  

จากนี้คุณอาจต้องการ:

- เก็บ JSON ในฐานข้อมูล NoSQL เพื่อการวิเคราะห์ในภายหลัง  
- ส่งผลลัพธ์ไปยัง chatbot ที่ตอบคำถามเกี่ยวกับใบเสร็จ  
- ผสานกับ Apache Tika เพื่อจัดการ PDF, DOCX, และรูปแบบอื่น ๆ  

ลองใช้งาน ปรับตั้งค่าให้ตรงกับเอกสารของคุณ แล้วให้เครื่องทำงานหนักในขณะที่คุณมุ่งเน้นการสร้างคุณค่า

---

![ดึงข้อความจากรูปภาพด้วย Java](placeholder-image.png "ดึงข้อความจากรูปภาพด้วย Java")

*รูปภาพ: การแสดงภาพกระบวนการ OCR – จากไฟล์รูปภาพไปยังผลลัพธ์ JSON.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
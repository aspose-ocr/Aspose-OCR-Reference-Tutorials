---
category: general
date: 2026-02-17
description: เรียนรู้วิธีใช้ OCR ใน Java เพื่อจดจำข้อความจากไฟล์รูปภาพ ดึงข้อความจากใบเสร็จ
  PNG และแปลงใบเสร็จเป็น JSON ด้วย Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: th
og_description: คู่มือแบบขั้นตอนต่อขั้นตอนเกี่ยวกับวิธีใช้ OCR ใน Java เพื่อจดจำข้อความจากภาพ
  ดึงข้อความจากใบเสร็จ PNG และแปลงใบเสร็จเป็น JSON.
og_title: วิธีใช้ OCR ใน Java – แยกข้อความจากรูปภาพ
tags:
- OCR
- Java
- Aspose
- Image Processing
title: วิธีใช้ OCR ใน Java – แยกข้อความจากรูปภาพอย่างรวดเร็ว
url: /th/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน Java – รับรู้ข้อความจากภาพอย่างรวดเร็ว

เคยสงสัย **how to use OCR** เพื่อดึงข้อความออกจากรูปถ่ายของใบเสร็จหรือไม่? บางครั้งคุณอาจลองใช้เครื่องมือออนไลน์หลายตัวแล้วได้ผลลัพธ์เป็นอักขระที่บิดเบี้ยวหรือรูปแบบที่อ่านไม่ออก ข่าวดีคือด้วยโค้ด Java เพียงไม่กี่บรรทัดคุณก็สามารถ **recognize text from image** จากไฟล์ภาพ, **extract text from PNG** ใบเสร็จ, และแม้กระทั่ง **convert receipt to JSON** เพื่อการประมวลผลต่อไปได้  

ในบทแนะนำนี้เราจะเดินผ่านขั้นตอนการทำงานทั้งหมด—ตั้งแต่การขอใบอนุญาต Aspose OCR library จนถึงการได้ JSON payload ที่สะอาดพร้อมนำเข้าไปยังฐานข้อมูลหรือโมเดลแมชชีน‑เลิร์นนิง ไม่เสียเวลา แค่ตัวอย่างที่ทำงานได้จริงที่คุณสามารถคัดลอก‑วางลงใน IDE ของคุณได้เลย เมื่อทำเสร็จคุณจะมีโปรแกรมที่รับ `receipt.png` แล้วส่งออกเป็นสตริง JSON ที่พร้อมใช้

## สิ่งที่คุณต้องเตรียม

- **Java Development Kit (JDK) 8+** – เวอร์ชันล่าสุดใดก็ได้
- **Aspose OCR for Java** library (Maven artifact คือ `com.aspose:aspose-ocr`)
- ไฟล์ **ใบอนุญาต Aspose OCR ที่ใช้งานได้** (`Aspose.OCR.lic`) รุ่นทดลองฟรีใช้สำหรับทดสอบได้ แต่ใบอนุญาตเต็มจะลบข้อจำกัดการประเมินผลออก
- ไฟล์ภาพ (PNG, JPEG ฯลฯ) ที่มีข้อความที่คุณต้องการอ่าน—สมมติว่าเป็น `receipt.png` และวางไว้ในโฟลเดอร์ที่รู้จัก
- IDE ที่คุณชื่นชอบ (IntelliJ IDEA, Eclipse, VS Code…) – เลือกตามสบาย

> **Pro tip:** เก็บไฟล์ใบอนุญาตไว้ไกลจากโฟลเดอร์ซอร์สและอ้างอิงด้วยพาธแบบ absolute หรือ relative เพื่อหลีกเลี่ยงการคอมมิตเข้า version control

เมื่อเงื่อนไขเบื้องต้นพร้อมแล้ว ไปต่อที่โค้ดจริงกันเลย

## วิธีใช้ OCR – ขั้นตอนหลัก

ด้านล่างเป็นภาพรวมระดับสูงของการกระทำที่เราจะทำ:

1. **Load the Aspose OCR library** และใช้ใบอนุญาตของคุณ  
2. **Create an `OcrEngine` instance** – ตัว engine ที่ทำงานหนักให้  
3. **Prepare an `OcrInput` object** ชี้ไปที่ภาพที่ต้องการประมวลผล  
4. **Call `recognize` with `ResultFormat.JSON`** เพื่อรับผลเป็น JSON ของข้อความที่สกัดออกมา  
5. **Handle the JSON output** – พิมพ์, เขียนไฟล์, หรือแปลงต่อในขั้นตอนถัดไป  

แต่ละขั้นจะอธิบายรายละเอียดในส่วนต่อไป

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR และใช้ใบอนุญาต

แรกสุดให้เพิ่ม dependency ของ Aspose OCR ลงใน `pom.xml` หากคุณใช้ Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

จากนั้นในโค้ด Java ของคุณให้โหลดใบอนุญาต ขั้นตอนนี้สำคัญ; หากข้ามจะทำให้ไลบรารีทำงานในโหมดประเมินผลและอาจใส่ลายน้ำในผลลัพธ์

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Why this matters:** วัตถุ `License` บอกให้ OCR engine รู้ว่าคุณได้รับสิทธิ์ใช้ฟีเจอร์เต็มรูปแบบ ซึ่งรวมถึงการรับรู้ความแม่นยำสูงและการส่งออกเป็น JSON การข้ามขั้นตอนนี้คุณยังสามารถ **recognize text from image** ได้ แต่ผลลัพธ์อาจถูกจำกัด

## ขั้นตอนที่ 2 – สร้างอินสแตนซ์ของ OCR Engine

คลาส `OcrEngine` เป็นจุดเริ่มต้นของทุกการทำ OCR คิดว่าเป็น “สมอง” ที่อ่านพิกเซลและตัดสินใจว่าอักขระใดเป็นตัวแทน

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

คุณสามารถปรับแต่ง engine (เช่น ตั้งค่าภาษา, เปิด deskew) ภายหลังได้ หากใบเสร็จของคุณมีสคริปต์ที่ไม่ใช่ละตินหรือสแกนมุมเอียง สำหรับใบเสร็จส่วนใหญ่ในสหรัฐฯ ค่าเริ่มต้นทำงานได้ดี

## ขั้นตอนที่ 3 – โหลดภาพที่ต้องการประมวลผล

ต่อไปเราจะชี้ OCR engine ไปที่ไฟล์ใบเสร็จ `OcrInput` สามารถรับหลายภาพได้ แต่ในบทแนะนำนี้เราจะใช้ PNG เพียงไฟล์เดียวเพื่อความง่าย

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

หากต้องการ **extract text from PNG** เป็นจำนวนมาก เพียงเรียก `input.add()` ซ้ำหลายครั้งหรือส่งรายการพาธไฟล์

## ขั้นตอนที่ 4 – รับรู้ข้อความและ **convert receipt to JSON**

นี่คือหัวใจของบทแนะนำ เราขอให้ engine รับรู้ข้อความและขอผลในรูปแบบ JSON ธง `ResultFormat.JSON` จะทำงานหนักให้เรา

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

Payload JSON จะรวมแต่ละบรรทัดที่รับรู้, กล่องขอบเขต, คะแนนความเชื่อมั่น, และข้อความดิบ โครงสร้างนี้ทำให้การ **convert receipt to JSON** เป็นเรื่องง่ายและสามารถส่งต่อไปยัง API ใดก็ได้

## ขั้นตอนที่ 5 – รวมทุกอย่างและรันโปรแกรม

ด้านล่างเป็นคลาส Java เต็มรูปแบบที่พร้อมรัน ซึ่งรวมทุกขั้นตอนเข้าด้วยกัน บันทึกเป็น `JsonExportDemo.java` (หรือชื่ออื่นที่คุณชอบ) แล้วรันจาก IDE หรือ command line

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อรันโปรแกรมจะพิมพ์สตริง JSON คล้ายกับตัวอย่างต่อไปนี้ (เนื้อหาอาจแตกต่างตามใบเสร็จของคุณ)

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

ตอนนี้คุณสามารถนำ JSON นี้ไปใส่ในฐานข้อมูล, REST endpoint, หรือ pipeline การวิเคราะห์ข้อมูลได้ ขั้นตอน **convert receipt to JSON** ทำเสร็จแล้ว

## คำถามที่พบบ่อยและกรณีขอบ

### ถ้าภาพถูกหมุน?

Aspose OCR จะตรวจจับและแก้ไขการหมุนเล็กน้อยอัตโนมัติ สำหรับภาพที่เอียงมาก ให้เรียก `engine.getImagePreprocessingOptions().setDeskew(true)` ก่อนทำการรับรู้

### จะจัดการหลายภาษาอย่างไร?

ใช้ `engine.getLanguage()` ตั้งค่าภาษา เช่น `engine.setLanguage(Language.FRENCH)` เหมาะเมื่อคุณต้อง **recognize text from image** ที่มีใบเสร็จหลายภาษา

### สามารถส่งออกเป็นข้อความธรรมดาแทน JSON ได้ไหม?

ทำได้เลย เปลี่ยน `ResultFormat.JSON` เป็น `ResultFormat.TEXT` แล้วเรียก `result.getText()`

### มีวิธีจำกัด OCR ให้ทำงานเฉพาะพื้นที่ที่กำหนดหรือไม่?

มี — ใช้ `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` เพื่อโฟกัสที่ส่วนใบเสร็จ ซึ่งช่วยเพิ่มความเร็วและความแม่นยำ

## เคล็ดลับสำหรับ OCR ที่พร้อมใช้งานใน Production

- **Cache ใบอนุญาต** หากต้องประมวลผลหลายไฟล์ในลูป; การสร้างใหม่ทุกครั้งเพิ่ม overhead
- **Batch process**: โหลดพาธใบเสร็จทั้งหมดลงใน `OcrInput` เดียวแล้วเรียก `recognize` ครั้งเดียว JSON จะมีอาเรย์ของหน้าแต่ละหน้า
- **Validate JSON**: หลังได้สตริงแล้วให้พาร์สด้วยไลบรารีอย่าง Jackson เพื่อตรวจสอบความสมบูรณ์ก่อนเก็บ
- **Monitor confidence**: JSON มีฟิลด์ `confidence` ต่อบรรทัด กรองบรรทัดที่ต่ำกว่า threshold (เช่น 0.85) เพื่อหลีกเลี่ยงข้อมูลขยะ
- **Secure ใบอนุญาต**: เก็บ `Aspose.OCR.lic` ใน vault หรือ environment variable โดยเฉพาะใน deployment บนคลาวด์

## สรุป

เราได้ครอบคลุม **how to use OCR** ใน Java เพื่อ **recognize text from image**, **extract text from PNG** ใบเสร็จ, และ **convert receipt to JSON** — ทั้งหมดด้วยตัวอย่างสั้น ๆ ที่ทำงานได้ครบวงจร ขั้นตอนง่าย ๆ โค้ดพร้อมรัน และผลลัพธ์ JSON ที่พร้อมใช้ในระบบต่อไป

ต่อไปคุณอาจสำรวจสถานการณ์ขั้นสูง: ส่ง JSON ไปยัง Apache Kafka เพื่อประมวลผลแบบเรียลไทม์, ใช้ regex ดึงยอดรายการ, หรือเชื่อมต่อกับบริการ OCR บนคลาวด์เพื่อสเกลใหญ่ ไม่ว่าคุณจะเลือกทำอะไร พื้นฐานที่คุณเรียนรู้วันนี้จะยังคงเป็นหัวใจ

มีคำถามหรือเจอปัญหาในขณะทำตามขั้นตอน? แสดงความคิดเห็นด้านล่างและเราจะช่วยกันแก้ไข ขอให้สนุกกับการเขียนโค้ดและแปลงภาพใบเสร็จที่ยุ่งยากให้เป็นข้อมูลที่สะอาดและค้นหาได้ง่าย!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-04-29
description: เรียนรู้วิธีทำ OCR ไฟล์ TIFF ด้วยโหมดสตรีมมิงของ Aspose OCR คู่มือนี้จะแสดงวิธีสกัดข้อความจากแผ่นภาพ
  TIFF ที่แบ่งเป็นแผ่นอย่างมีประสิทธิภาพ.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: th
og_description: วิธีทำ OCR ไฟล์ TIFF ด้วย Aspose OCR streaming. โค้ดแบบขั้นตอนต่อขั้นตอนเพื่อสกัดข้อความจากภาพ
  TIFF ขนาดใหญ่.
og_title: วิธีทำ OCR ไฟล์ TIFF – คู่มือสตรีมมิ่งครบถ้วน
tags:
- OCR
- Java
- Aspose
- TIFF
title: วิธีทำ OCR ไฟล์ TIFF – สตรีม TIFF ขนาดใหญ่และดึงข้อความจากแผ่นภาพใน Java
url: /th/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธี OCR TIFF – สตรีม TIFF ขนาดใหญ่และสกัดข้อความจากไทล์ใน Java

เคยสงสัย **วิธี OCR TIFF** ไฟล์ที่ใหญ่เกินกว่าจะโหลดเข้าหน่วยความจำทั้งหมดในครั้งเดียวหรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อภาพ TIFF ของพวกเขาถูกแบ่งเป็นหลายสิบไทล์ และการเรียก `ocrEngine.recognize()` ปกติก็ทำให้โปรแกรมค้าง  

ข่าวดีคือ? โหมดสตรีมของ Aspose OCR ให้คุณส่งแต่ละไทล์เป็นสตรีมแยกกันได้ ดังนั้นคุณสามารถ **สกัดข้อความจากไทล์** ได้โดยไม่ทำให้ heap พุ่งสูงเกินไป ในบทแนะนำนี้เราจะเดินผ่านตัวอย่าง Java ที่พร้อมรันเต็มรูปแบบ อธิบายว่าทำไมแต่ละบรรทัดถึงสำคัญ และชี้ให้เห็นกับดักที่คุณควรหลีกเลี่ยง

> **สิ่งที่คุณจะได้:** โปรแกรมที่รันได้ซึ่งต่อภาพ TIFF ที่แบ่งเป็นไทล์แบบเรียลไทม์ พิมพ์ข้อความที่รวมกันแล้ว และแสดงวิธีปรับโค้ดให้ใช้กับภาษาอื่นหรือรูปแบบภาพอื่น

---

## ข้อกำหนดเบื้องต้น

- **Java 17** หรือใหม่กว่า (โค้ดใช้ try‑with‑resources ดังนั้น JDK 8+ ทำงานได้ แต่ JDK 17 เป็น LTS ปัจจุบัน)
- ไลบรารี **Aspose.OCR for Java** (เวอร์ชัน 23.10 หรือใหม่กว่า) เพิ่มผ่าน Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- โฟลเดอร์ที่บรรจุไทล์ TIFF แต่ละไฟล์ (เช่น `tile_0.tif`, `tile_1.tif`, …)  
- ตัวเลือก: IDE อย่าง IntelliJ IDEA หรือ VS Code – แต่ก็สามารถใช้เครื่องมือแก้ไขข้อความธรรมดาได้

---

## ขั้นตอนที่ 1 – เตรียมเส้นทางของไทล์ (ทำไมจึงสำคัญ)

ก่อนที่เครื่อง OCR จะทำอะไรได้ มันต้องรู้ว่าชิ้นส่วนภาพแต่ละอันอยู่ที่ไหน การกำหนดเส้นทางแบบคงที่เป็นวิธีที่ง่ายสำหรับการสาธิต แต่ในสภาพแวดล้อมจริงคุณอาจสแกนไดเรกทอรีหรืออ่านไฟล์ manifest

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **เคล็ดลับ:** เก็บไทล์ไว้ตามลำดับเชิงอักษร (0, 1, 2…) เพราะเครื่องจะต่อข้อความที่รู้จำตามลำดับเดียวกับที่คุณป้อนสตรีม

---

## ขั้นตอนที่ 2 – เปิดใช้งานโหมดสตรีมบน OCR Engine (คีย์เวิร์ดหลัก)

ต่อไปเราจะสร้างอินสแตนซ์ `OcrEngine` และเปิดโหมดสตรีม นี่คือหัวใจของ **วิธี OCR TIFF** โดยไม่ต้องโหลดภาพทั้งหมดเข้าสู่ RAM

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**ทำไมต้องสตรีม?**  
เมื่อเรียก `setEnableStreaming(true)` เครื่องจะถือทุก `ImageStream` ที่เข้ามาเป็นส่วนต่อเนื่องของสตรีมก่อนหน้า มันสร้างแคนวาสเสมือนภายใน ต่อไทล์แบบเสมือนจริง และทำ OCR ครั้งเดียวเมื่อครบทั้งหมด วิธีนี้ช่วยหลีกเลี่ยง “OutOfMemoryError” ที่จะเกิดขึ้นหากพยายามโหลด TIFF ขนาดหลายกิกะไบต์ในครั้งเดียว

---

## ขั้นตอนที่ 3 – เพิ่มแต่ละไทล์เป็น Input Stream (คีย์เวิร์ดรอง)

นี่คือลูปที่ป้อนไทล์ทุกไฟล์ให้กับเครื่อง `try‑with‑resources` ทำให้แน่ใจว่าไฟล์จะถูกปิดอย่างรวดเร็ว ซึ่งสำคัญมากเมื่อต้องจัดการกับหลายสิบไฟล์

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

สังเกตว่าประโยค **extract text tiles** ถูกฝังอย่างเป็นธรรมชาติ: ทุกการวนลูป *สกัด* ข้อความจากไทล์หนึ่งและเพิ่มเข้าไปในผลลัพธ์ที่กำลังเติบโต

---

## ขั้นตอนที่ 4 – รันการจดจำและแสดงข้อความที่รวมกัน (คีย์เวิร์ดหลัก)

หลังจากไทล์ทั้งหมดถูกจัดคิวแล้ว การเรียกครั้งเดียวจะทำ OCR บนภาพเสมือนจริง ผลลัพธ์จะมีข้อความเต็มเหมือนกับว่าคุณมี TIFF ขนาดมหาศาลไฟล์เดียว

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าไทล์แต่ละอันมีคำว่า “Hello World” แบ่งกัน):

```
=== OCR Output ===
Hello World
```

หากไทล์ของคุณมีหลายบรรทัด ข้อความจะปรากฏตามลำดับที่คุณให้ไว้ คุณยังสามารถเขียน `ocrResult.getText()` ลงไฟล์เพื่อการประมวลผลต่อไปได้

---

## ขั้นตอนที่ 5 – ตัวอย่างเต็มที่สามารถรันได้ (รวมทุกขั้นตอนในที่เดียว)

ด้านล่างเป็นโปรแกรมครบชุดที่คุณสามารถคัดลอก‑วางลงใน `StreamingExample.java` มีการนำเข้า, คอมเมนต์, และการจัดการข้อผิดพลาดครบถ้วน

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

บันทึก, คอมไพล์, แล้วรัน:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

คุณควรเห็นข้อความ OCR ที่ต่อกันแสดงบนคอนโซล

---

## เคล็ดลับขั้นสูง & ความผิดพลาดที่พบบ่อย (ทำไมวิธีนี้ถึงได้ผล)

| Issue | Why It Happens | How to Fix / Optimize |
|-------|----------------|-----------------------|
| **Out‑of‑memory errors** | การโหลด TIFF ขนาดเต็มเข้าสู่ `BufferedImage` ใช้หน่วยความจำทั้งหมด | ใช้โหมดสตรีม (`setEnableStreaming(true)`) – เครื่องจะไม่สร้างภาพเต็มรูปแบบ |
| **Tile order mismatch** | ไฟล์ถูกจัดเรียงตามตัวอักษรแทนลำดับตัวเลข (เช่น `tile_10.tif` มาก่อน `tile_2.tif`) | เติมศูนย์หน้าตัวเลข (`tile_00.tif`, `tile_01.tif`) หรือเรียงลำดับด้วย `Comparator` |
| **Wrong language** | OCR ตั้งค่าเป็นภาษาอังกฤษโดยค่าเริ่มต้น; ข้อความที่ไม่ใช่อังกฤษจะอ่านออกเป็นอักขระผิด | เรียก `ocrEngine.getLanguageSettings().setLanguage("fr")` (หรือรหัส ISO ที่รองรับอื่น) |
| **Partial failures** | ไทล์ที่เสียหายหนึ่งไฟล์ทำให้กระบวนการทั้งหมดหยุด | ดัก `IOException` แยกตามไทล์, บันทึก log, แล้วตัดสินใจว่าจะดำเนินต่อหรือยกเลิก |
| **Performance bottleneck** | การอ่าน/เขียนดิสก์เป็นคอขวดเมื่ออ่านไฟล์เล็กจำนวนมาก | รวมไทล์เป็น ZIP แล้วสตรีมจากหน่วยความจำ, หรือใช้ SSD ที่เร็วกว่า |

---

## เมื่อใดควรใช้สตรีม vs. OCR แบบภาพเดียว

- **สตรีม** เหมาะสำหรับ:
  - TIFF หลายหน้า หรือสแกนขนาดกิกะพิกเซล
  - สภาพแวดล้อมที่หน่วยความจำจำกัด (เช่น Docker container, อุปกรณ์มือถือ)
  - พายป์ไลน์ที่รับข้อมูลภาพเป็นชิ้นส่วน (เช่น ฟีดจากกล้อง)

- **OCR แบบภาพเดียว** เหมาะสำหรับ:
  - ไฟล์ PNG/JPEG ขนาดเล็ก (< 5 MB)
  - การสแกนครั้งเดียวที่ความเรียบง่ายสำคัญกว่าประสิทธิภาพ

---

## สรุป

ตอนนี้คุณมีความเข้าใจที่มั่นคงเกี่ยวกับ **วิธี OCR TIFF** ด้วยความสามารถสตรีมของ Aspose OCR และรู้วิธี **สกัดข้อความจากไทล์** อย่างมีประสิทธิภาพ โซลูชันครบชุด – การเริ่มต้นเครื่อง, เปิดสตรีม, เพิ่มไทล์แต่ละอัน, แล้วทำการจดจำบนแคนวาสเสมือน – ครอบคลุม “อะไร”, “ทำไม”, และ “อย่างไร” ที่คุณต้องการสำหรับโค้ดพร้อมผลิต

ขั้นตอนต่อไป? ลองเปลี่ยน `"en"` เป็นภาษอื่น หรือทดลองกับรูปแบบภาพต่าง ๆ (`.png`, `.jpg`) คุณอาจส่งผลลัพธ์ OCR ตรงไปยังดัชนีการค้นหา หรือสร้าง PDF ตัวสร้างก็ได้ รูปแบบยังคงเหมือนเดิม: สตรีม, ต่อ, จดจำ  

มีคำถามเกี่ยวกับการขยายเป็นหลายร้อยไทล์ หรืออยากขอคำแนะนำเรื่องการจัดการข้อผิดพลาด? แสดงความคิดเห็นด้านล่าง แล้วขอให้เขียนโค้ดอย่างสนุกสนาน!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
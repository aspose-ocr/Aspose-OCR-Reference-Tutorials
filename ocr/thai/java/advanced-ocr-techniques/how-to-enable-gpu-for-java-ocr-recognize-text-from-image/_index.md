---
category: general
date: 2026-02-22
description: เรียนรู้วิธีเปิดใช้งาน GPU ใน Java OCR เพื่อจดจำข้อความจากภาพและสกัดข้อความจากใบแจ้งหนี้อย่างรวดเร็วด้วย
  Aspose OCR.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from invoice
- java ocr example
- load image for ocr
language: th
og_description: วิธีเปิดใช้งาน GPU ใน Java OCR, จดจำข้อความจากภาพและสกัดข้อความจากใบแจ้งหนี้ด้วยตัวอย่าง
  Java OCR อย่างครบถ้วน.
og_title: วิธีเปิดใช้งาน GPU สำหรับ Java OCR – คู่มือด่วน
tags:
- Java
- OCR
- GPU
- Aspose
title: วิธีเปิดใช้งาน GPU สำหรับ Java OCR – แยกข้อความจากภาพ
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ Java OCR – การจดจำข้อความจากภาพ

เคยสงสัย **วิธีเปิดใช้งาน GPU** เมื่อทำ OCR ด้วย Java หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาจำนวนมากเจออุปสรรคด้านประสิทธิภาพเมื่อประมวลผลเอกสารขนาดใหญ่และความละเอียดสูงเช่นใบแจ้งหนี้ ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถสลับสวิตช์เดียวและให้การ์ดกราฟิกทำงานหนักแทน ในบทเรียนนี้เราจะพาไปผ่าน **java ocr example** ที่โหลดภาพ, เปิดการประมวลผลด้วย GPU, และดึงข้อความจากใบแจ้งหนี้อย่างรวดเร็ว

เราจะครอบคลุมทุกอย่างตั้งแต่การติดตั้งไลบรารีจนถึงการจัดการกรณีขอบเช่นไดรเวอร์ GPU ที่หายไป เมื่อจบคุณจะสามารถ **recognize text from image** ไฟล์ได้แบบเรียลไทม์ และคุณจะมีเทมเพลตที่มั่นคงสำหรับโครงการ OCR ใด ๆ ในอนาคต ไม่ต้องอ้างอิงภายนอก—เพียงโค้ดที่ทำงานได้จริง

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK) 11** หรือใหม่กว่า ที่ติดตั้งบนเครื่องของคุณ  
- **Maven** (หรือ Gradle) สำหรับการจัดการ dependencies  
- ระบบที่ **รองรับ GPU** พร้อมไดรเวอร์อัปเดต (NVIDIA, AMD, หรือ Intel)  
- ไฟล์ภาพของใบแจ้งหนี้ (เช่น `large_invoice_300dpi.png`)  

หากคุณขาดสิ่งใดสิ่งหนึ่ง ให้จัดการให้เรียบร้อยก่อน; ส่วนที่เหลือของคู่มือสมมติว่ามีพร้อมแล้ว

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ไปยังโปรเจกต์ของคุณ

สิ่งแรกที่เราต้องการคือไลบรารี Aspose OCR. กับ Maven เพียงแค่วางโค้ดสแนปป์ต่อไปนี้ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro tip:** หมายเลขเวอร์ชันมีการเปลี่ยนแปลงบ่อย; ตรวจสอบ Maven Central เพื่อรับรุ่นล่าสุดและอัปเดตอยู่เสมอ

หากคุณชอบใช้ Gradle ทางเลือกที่เทียบเท่าคือ:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

เมื่อ dependency ถูก resolve แล้ว คุณก็พร้อมเขียนโค้ดที่สื่อสารกับ OCR engine

## ขั้นตอนที่ 2: วิธีเปิดใช้งาน GPU ใน Aspose OCR Engine

ตอนนี้มาถึงจุดสำคัญ—การเปิดการประมวลผลด้วย GPU. Aspose OCR มีโหมดการประมวลผลสามแบบ:

| Mode | Description |
|------|-------------|
| `CPU_ONLY` | ใช้ CPU อย่างเดียว, ปลอดภัยสำหรับเครื่องใดก็ได้ |
| `GPU_ONLY` | บังคับใช้ GPU, จะล้มเหลหากไม่มีอุปกรณ์ที่เข้ากันได้ |
| `AUTO_GPU` | ตรวจจับ GPU และใช้เมื่อมี, หากไม่มีจะกลับไปใช้ CPU |

สำหรับสถานการณ์ส่วนใหญ่ เราแนะนำ **`AUTO_GPU`** เพราะให้ประสิทธิภาพที่ดีที่สุดของทั้งสองโลก นี่คือวิธีเปิดใช้งาน:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU processing (AUTO_GPU uses GPU when available)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // The rest of the steps follow...
    }
}
```

> **Why this matters:** การเปิดใช้งาน GPU สามารถลดเวลาการประมวลผลสำหรับใบแจ้งหนี้ 300 dpi จากหลายวินาทีเหลือภายใต้หนึ่งวินาที, ขึ้นอยู่กับฮาร์ดแวร์ของคุณ

## ขั้นตอนที่ 3: โหลดภาพสำหรับ OCR – การจดจำข้อความจากภาพ

ก่อนที่ engine จะอ่านอะไรได้ คุณต้องส่งภาพให้มัน Aspose OCR’s `OcrInput` class รองรับเส้นทางไฟล์, stream, หรือแม้แต่ `BufferedImage` objects. เพื่อความง่าย เราจะใช้เส้นทางไฟล์:

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **Edge case:** หากภาพใหญ่กว่า 5 MB, ควรทำการ down‑sampling ก่อนเพื่อหลีกเลี่ยงข้อผิดพลาด out‑of‑memory บน GPU

## ขั้นตอนที่ 4: ทำ OCR และดึงข้อความจากใบแจ้งหนี้

ตอนนี้เราขอให้ engine ทำเวทมนตร์ของมัน. เมธอด `recognize` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่มีข้อความที่ดึงออกมา, คะแนนความมั่นใจ, และข้อมูลการจัดวาง

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

เมื่อคุณรันโปรแกรม คุณควรเห็นผลลัพธ์ประมาณนี้:

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

หากผลลัพธ์ดูเป็นอักขระผสม, ตรวจสอบให้แน่ใจว่าภาพชัดเจนและภาษาของ OCR ถูกตั้งค่าอย่างถูกต้อง (Aspose ตั้งค่าเริ่มต้นเป็น English, แต่คุณสามารถเปลี่ยนได้ผ่าน `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)` เป็นต้น)

## ขั้นตอนที่ 5: ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นคลาส Java ที่สมบูรณ์และเป็นอิสระ. คัดลอกไปวางใน IDE ของคุณ, ปรับเส้นทางภาพ, แล้วกด **Run**

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU (auto‑detect)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace with the absolute or relative path to your invoice image
        ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png");

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโค้ดบนใบแจ้งหนี้ 300 dpi ที่ชัดเจนโดยทั่วไปจะให้ผลลัพธ์เป็นข้อความธรรมดาที่แสดงทุกบรรทัดในเอกสาร. ผลลัพธ์ที่แน่นอนขึ้นอยู่กับรูปแบบของใบแจ้งหนี้, แต่คุณจะเห็นฟิลด์เช่น *Invoice Number*, *Date*, *Total Amount*, และคำอธิบายรายการสินค้า

## ข้อผิดพลาดทั่วไป & วิธีแก้ไข

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError`** | GPU driver หายหรือไม่เข้ากัน | ติดตั้งไดรเวอร์ล่าสุดจาก NVIDIA/AMD/Intel |
| **Very slow processing** | GPU fallback ไปใช้ CPU อย่างเงียบ | ตรวจสอบว่า `ocrEngine.getProcessingMode()` คืนค่า `AUTO_GPU` และ `SystemInfo.isGpuAvailable()` เป็น true |
| **Blank output** | ภาพมืดเกินไปหรือคอนทราสต์ต่ำ | ทำการพรี‑โปรเซสภาพ (เพิ่มคอนทราสต์, ทำ binary) ก่อนส่งให้ OCR |
| **Out‑of‑Memory** | ภาพใหญ่มาก (>10 MP) | ปรับขนาดหรือแบ่งภาพเป็นหลาย tile; ประมวลผลแต่ละ tile แยกกัน |

## สรุปขั้นตอน‑โดย‑ขั้นตอน (อ้างอิงเร็ว)

| Step | What You Did |
|------|--------------|
| 1 | เพิ่ม Aspose OCR dependency |
| 2 | สร้าง `OcrEngine` และตั้งค่า `AUTO_GPU` |
| 3 | โหลดภาพใบแจ้งหนี้ผ่าน `OcrInput` |
| 4 | เรียก `recognize` และพิมพ์ `ocrResult.getText()` |
| 5 | จัดการข้อผิดพลาดทั่วไปและตรวจสอบผลลัพธ์ |

## ก้าวต่อไป – ขั้นตอนต่อไป

- **Batch processing:** วนลูปโฟลเดอร์ของใบแจ้งหนี้และเก็บผลลัพธ์แต่ละรายการในฐานข้อมูล  
- **Language support:** เปลี่ยนเป็น `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` สำหรับใบแจ้งหนี้หลายภาษา  
- **Post‑processing:** ใช้ regular expressions เพื่อดึงฟิลด์เช่น *Invoice Number* หรือ *Total Amount* จากข้อความดิบ  
- **GPU tuning:** หากคุณมีหลาย GPU, สำรวจ `ocrEngine.setGpuDeviceId(int id)` เพื่อเลือกอันที่เร็วที่สุด  

## สรุป

เราได้แสดง **วิธีเปิดใช้งาน GPU** สำหรับ Java OCR, สาธิต **java ocr example** ที่สะอาด, และอธิบายขั้นตอนทั้งหมดตั้งแต่ **load image for OCR** ถึง **extract text from invoice**. ด้วยการใช้โหมด `AUTO_GPU` ของ Aspose คุณจะได้บูสต์ประสิทธิภาพโดยไม่เสียความเข้ากันได้—เหมาะสำหรับเครื่องพัฒนาหรือเซิร์ฟเวอร์ผลิตจริง

ลองใช้ ปรับการพรี‑โปรเซสภาพ และทดลองทำงานแบบ batch. ความเป็นไปได้ไม่มีขีดจำกัดเมื่อคุณผสานการเร่งความเร็วด้วย GPU กับไลบรารี OCR ที่แข็งแกร่ง

---

![แผนภาพแสดงกระบวนการ OCR ที่เร่งด้วย GPU – วิธีเปิดใช้งาน GPU สำหรับ Java OCR](https://example.com/images/gpu-ocr-pipeline.png "วิธีเปิดใช้งาน GPU สำหรับ Java OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
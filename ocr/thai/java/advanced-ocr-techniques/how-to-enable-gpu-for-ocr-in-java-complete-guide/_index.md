---
category: general
date: 2026-02-19
description: วิธีเปิดใช้งาน GPU เพื่อการประมวลผล OCR อย่างรวดเร็ว เรียนรู้การโหลดภาพความละเอียดสูง
  การจดจำภาพข้อความ และการดึงข้อความด้วย Aspose OCR.
draft: false
keywords:
- how to enable gpu
- load high resolution image
- recognize text image
- how to extract text
- enable gpu processing
language: th
og_description: วิธีเปิดใช้งาน GPU เพื่อการประมวลผล OCR ที่เร็วขึ้น คู่มือนี้จะแสดงวิธีโหลดภาพความละเอียดสูง,
  จดจำข้อความในภาพ, และดึงข้อความด้วย Aspose OCR.
og_title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – คู่มือครบถ้วน
tags:
- OCR
- Java
- GPU
- Aspose
title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – คู่มือเต็ม
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีเปิดใช้งาน GPU** สำหรับ pipeline OCR ของคุณและลดเวลาการประมวลผลลงเป็นวินาทีหรือไม่? คุณไม่ได้อยู่คนเดียว ในโครงการที่มีภาพจำนวนมาก บ่อยครั้งขั้นตอนการสกัดข้อความที่ทำงานบน CPU จะเป็นคอขวด และการสลับไปใช้ GPU สามารถเปลี่ยนเกมได้อย่างมาก

ในบทแนะนำนี้เราจะพาคุณผ่านการโหลด **ภาพความละเอียดสูง**, การตั้งค่า Aspose OCR ให้ทำงานบน GPU, และสุดท้าย **การจดจำภาพข้อความ** และ **การสกัดข้อความ** ด้วยเพียงไม่กี่บรรทัดของ Java. เมื่อเสร็จสิ้นคุณจะมีโปรแกรมพร้อมรันที่สาธิต **การเปิดใช้งานการประมวลผลด้วย GPU** ตั้งแต่ต้นจนจบ

## สิ่งที่คุณต้องเตรียม

- Java 17 หรือใหม่กว่า (โค้ดใช้ระบบโมดูล แต่ทำงานบน JDK เก่าได้ด้วยการปรับเล็กน้อย)  
- Aspose OCR for Java 23.10 (หรือเวอร์ชันล่าสุด) – สามารถดึงพิกัด Maven จากเว็บไซต์ Aspose  
- GPU NVIDIA ที่ติดตั้งไดรเวอร์ CUDA 12+ (หากไม่มีไลบรารีจะไม่สามารถเริ่มทำงานได้)  
- ตัวอย่างภาพความละเอียดสูง (PNG หรือ JPEG) ที่คุณต้องการอ่านข้อความจาก  

เท่านี้แค่นั้น ไม่ต้องใช้บริการภายนอก ไม่ต้องใช้เครดิตคลาวด์ เพียงเครื่องของคุณและไดรเวอร์สแต็กที่เหมาะสม

![GPU OCR workflow – how to enable GPU processing](gpu-ocr-workflow.png)

*ข้อความแทนภาพ: แผนภาพแสดงวิธีเปิดใช้งาน GPU สำหรับการประมวลผล OCR ใน Java.*

## การดำเนินการแบบขั้นตอนต่อขั้นตอน

ด้านล่างเราจะแบ่งวิธีแก้เป็นส่วนย่อย ๆ แต่ละส่วนมีโค้ดสั้น ๆ คำอธิบาย **ทำไม** ขั้นตอนนั้นสำคัญ และเคล็ดลับปฏิบัติที่คุณอาจชื่นชอบในภายหลัง

### วิธีเปิดใช้งาน GPU สำหรับ OCR – ขั้นตอน 1: ติดตั้ง Dependencies & ตรวจสอบ CUDA

ก่อนที่โค้ด Java ใด ๆ จะทำงาน runtime ของ CUDA ต้องสามารถค้นพบได้บนระบบของคุณ บน Windows คุณสามารถตรวจสอบได้ด้วย:

```bat
nvcc --version
```

บน Linux:

```bash
nvidia-smi
```

หากคำสั่งแสดงเวอร์ชันของไดรเวอร์และรายละเอียดของ GPU คุณก็พร้อมแล้ว หากไม่แสดง ให้ไปที่เว็บไซต์ของ NVIDIA ดาวน์โหลดไดรเวอร์ที่เหมาะสมและติดตั้ง CUDA toolkit (ตรวจสอบให้เวอร์ชันตรงกับข้อกำหนดของ Aspose OCR – ปัจจุบันคือ 12.x)

**เคล็ดลับ:** ควรอัปเดตไดรเวอร์ GPU อย่างสม่ำเสมอ แต่หลีกเลี่ยง “latest‑beta” เพราะบางครั้งอาจทำให้ความเข้ากันได้ของไบนารีกับไลบรารีเนทีฟของ Aspose แตกหัก

### วิธีเปิดใช้งาน GPU สำหรับ OCR – ขั้นตอน 2: เพิ่ม Dependency ของ Aspose OCR ใน Maven

เพิ่มโค้ดต่อไปนี้ลงใน `pom.xml` ของคุณ เพื่อดึงเอา core OCR engine และไบนารี GPU เนทีฟสำหรับ Windows, Linux, และ macOS

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

หากคุณใช้ Gradle ให้ใช้รูปแบบที่เทียบเท่า:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

หลังจากรีเฟรชโปรเจกต์แล้ว คลาส `OcrEngine`, `OcrDeviceType`, และ `ImageStream` จะพร้อมใช้งาน

### วิธีเปิดใช้งาน GPU สำหรับ OCR – ขั้นตอน 3: สร้าง OCR Engine และเปิดใช้งาน GPU

ตอนนี้เราจะบอก Aspose ให้ทำงานบน GPU. `OcrEngine` มีอ็อบเจกต์ `Device` ที่เราสามารถสลับประเภทอุปกรณ์ประมวลผลได้

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 3.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3.2: Enable GPU processing (requires a CUDA‑enabled driver & runtime)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Optional: limit the number of GPU streams for better resource control
        ocrEngine.getDevice().setStreamCount(2);

        // Step 3.3: Load the high‑resolution image to be recognized
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample-highres.png"));

        // Step 3.4: Perform OCR and retrieve the recognized text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 3.5: Display the extracted text
        System.out.println("=== OCR RESULT ===");
        System.out.println(recognizedText);
    }
}
```

**ทำไมขั้นตอนนี้สำคัญ:** การตั้งค่า `OcrDeviceType.GPU` จะสลับ engine การสรุปผลจากการทำงานบน CPU‑only ไปเป็น CUDA‑accelerated. การเรียก `setStreamCount` แบบเลือกจะช่วยควบคุมระดับการทำงานขนาน; สองสตรีมเป็นค่าเริ่มต้นที่ปลอดภัยสำหรับการ์ดผู้บริโภคส่วนใหญ่

### วิธีเปิดใช้งาน GPU สำหรับ OCR – ขั้นตอน 4: โหลดภาพความละเอียดสูง

แหล่งข้อมูลความละเอียดสูงให้โมเดล OCR มีรายละเอียดภาพมากขึ้น ซึ่งแปลเป็นความแม่นยำที่สูงกว่า โดยเฉพาะสำหรับฟอนต์ขนาดเล็กหรือสคริปต์ซับซ้อน `ImageStream.fromFile` ช่วยอ่านไฟล์เข้าสู่รูปแบบที่ engine คาดหวัง

หากคุณต้องการ **โหลดภาพความละเอียดสูง** จาก URL หรืออาร์เรย์ไบต์ในหน่วยความจำ สามารถใช้โค้ดต่อไปนี้:

```java
byte[] imageBytes = java.nio.file.Files.readAllBytes(Paths.get("remote-image.png"));
ocrEngine.setImage(ImageStream.fromBytes(imageBytes));
```

**กรณีขอบ:** GPU บางรุ่นมีขนาดเทกซ์เจอร์สูงสุด (มัก 16384 × 16384). หากภาพของคุณใหญ่เกินกว่านั้น ให้พิจารณาลดขนาดลงเป็นขนาดที่ยังคงอ่านได้ (เช่น 3000 × 2000). OCR engine จะปรับขนาดอัตโนมัติหากคุณเรียก `ocrEngine.setResizeFactor(0.5)` ก่อนโหลด

### วิธีเปิดใช้งาน GPU สำหรับ OCR – ขั้นตอน 5: จดจำภาพข้อความและสกัดข้อความ

การเรียก `ocrEngine.recognize()` จะทำให้ neural network inference ทำงานบน GPU. เมธอดนี้คืนค่าเป็นอ็อบเจกต์ `OcrResult`; `getText()` จะดึงสตริงข้อความธรรมดาออกมา คุณยังสามารถดึง bounding boxes, คะแนนความเชื่อมั่น, หรือ JSON ดิบได้หากต้องการข้อมูลที่ละเอียดกว่า

```java
OcrResult result = ocrEngine.recognize();
String plainText = result.getText();
System.out.println("Detected text length: " + plainText.length());

// Optional: iterate over each line with its confidence
result.getPages().forEach(page -> {
    page.getLines().forEach(line -> {
        System.out.printf("Line: \"%s\" (Confidence: %.2f%%)%n",
                line.getText(), line.getConfidence() * 100);
    });
});
```

**ทำไมคุณอาจต้องการขั้นตอนนี้:** ขั้นตอน `recognize text image` คือจุดที่ GPU แสดงพลัง – ภาพขนาดใหญ่ที่อาจใช้เวลาหลายนาทีบน CPU จะประมวลผลในส่วนเล็กของเวลานั้น คะแนนความเชื่อมั่นช่วยกรองผลลัพธ์คุณภาพต่ำ, เป็นเทคนิคที่มีประโยชน์เมื่อคุณต่อไป **วิธีสกัดข้อความ** สำหรับการวิเคราะห์ต่อเนื่อง

### เคล็ดลับพิเศษ & ปัญหาที่พบบ่อย

| สถานการณ์ | วิธีแก้ |
|-----------|------------|
| **ข้อผิดพลาด Out‑of‑memory** บน GPU | ลด `setStreamCount` ลงเป็น 1, หรือทำการลดขนาดภาพก่อนส่งให้ engine |
| **อักขระไม่ถูกต้อง** แม้ภาพจะความละเอียดสูง | ตรวจสอบให้โมเดลภาษา (`ocrEngine.setLanguage(OcrLanguage.ENGLISH)`) ตรงกับภาษาของข้อความ |
| **CUDA version mismatch** | ปรับเวอร์ชันของ CUDA toolkit ให้ตรงกับที่บรรจุใน Aspose OCR (ดู release notes) |
| **หลาย GPU** | ใช้ `ocrEngine.getDevice().setDeviceId(1)` เพื่อเลือก GPU ตัวที่สองหากตัวแรกกำลังทำงาน |
| **รันบนเซิร์ฟเวอร์ headless** | ไม่ต้องทำขั้นตอนเพิ่มเติม; ไดรเวอร์ GPU ทำงานได้โดยไม่มีหน้าจอ |

## วิธีสกัดข้อความ – ตรวจสอบผลลัพธ์

เมื่อคุณรันคลาสด้านบน ควรเห็นผลลัพธ์ประมาณนี้:

```
=== OCR RESULT ===
Welcome to the Aspose OCR demo!
Your GPU is now accelerating text extraction.
```

หากผลลัพธ์ดูเป็นอักขระแปลก ๆ ให้ตรวจสอบว่าภาพเป็นความละเอียดสูงจริงและไดรเวอร์ GPU ถูกติดตั้งอย่างถูกต้อง คุณยังสามารถเปิดการบันทึกแบบละเอียดได้:

```java
ocrEngine.setLogLevel(OcrLogLevel.DEBUG);
```

บันทึกจะแสดงว่า kernel CUDA เนทีฟถูกโหลดสำเร็จหรือไม่

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

- **การประมวลผลแบบแบตช์:** วาง `OcrEngine` ไว้ในลูปและป้อนรายการพาธของภาพ อย่าลืมใช้ instance เดียวกันเพื่อหลีกเลี่ยงค่าใช้จ่ายในการเริ่มต้น GPU ซ้ำหลายครั้ง  
- **การตรวจจับภาษา:** Aspose OCR รองรับกว่า 30 ภาษา สลับด้วย `ocrEngine.setLanguage(OcrLanguage.FRENCH)`  
- **การประมวลผลหลังการสกัด:** ใช้ regular expressions ทำความสะอาดสตริงที่สกัดได้ หรือส่งต่อไปยัง pipeline NLP ต่อไป  
- **อุปกรณ์ทางเลือก:** หากคุณไม่มี GPU ที่รองรับ CUDA สามารถกลับไปใช้ `OcrDeviceType.CPU` ได้ โค้ดเดียวกันทำงาน; เพียงเปลี่ยนประเภทอุปกรณ์  
- **การวัดประสิทธิภาพ:** ใช้ `System.nanoTime()` ก่อนและหลัง `recognize()` เพื่อวัดความแตกต่างของเวลาและประเมินผลประโยชน์จาก **การเปิดใช้งานการประมวลผลด้วย GPU**  

---

### สรุป

เราได้ครอบคลุม **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR ใน Java ตั้งแต่การติดตั้งไดรเวอร์ที่เหมาะสม ไปจนถึงการโหลด **ภาพความละเอียดสูง**, **จดจำภาพข้อความ**, และสุดท้าย **วิธีสกัดข้อความ** จากผลลัพธ์ ตัวอย่างที่สมบูรณ์และรันได้ข้างต้นควรทำงานได้ทันทีบน NVIDIA GPU รุ่นใหม่ใดก็ได้

ลองใช้งาน ปรับขนาดภาพต่าง ๆ และสังเกตการเพิ่มขึ้นของอัตราการประมวลผล OCR ของคุณ หากเจออุปสรรคใด ๆ ให้กลับไปตรวจสอบส่วนเคล็ดลับหรือดู release notes ของ Aspose สำหรับคำแนะนำล่าสุดเกี่ยวกับ **การเปิดใช้งานการประมวลผลด้วย GPU**  

ขอให้เขียนโค้ดสนุกและ GPU ของคุณทำงานเย็น ๆ ขณะประมวลผลข้อความ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-11-17
description: วิธีเปิดใช้งาน GPU ใน Java OCR เพื่อดึงข้อความจากภาพอย่างรวดเร็ว เรียนรู้วิธีตั้งค่า
  GPU, ดึงข้อความและจดจำข้อความใน Java ด้วย Aspose OCR.
draft: false
keywords:
- how to enable gpu
- high resolution ocr
- aspose ocr java
- extract text image java
- gpu acceleration ocr
lastmod: 2026-11-17
og_description: วิธีเปิดใช้งาน GPU สำหรับ Java OCR อย่างรวดเร็ว คู่มือนี้แสดงวิธีตั้งค่า
  GPU, ดึงข้อความจากภาพและจดจำข้อความใน Java ด้วย Aspose OCR.
og_image_alt: 'Developer guide: Enable GPU for Java OCR using Aspose OCR library'
og_title: วิธีเปิดใช้งาน GPU สำหรับ Java OCR – คู่มือแบบขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to enable GPU in Java OCR to extract text from image fast. Learn
    how to configure GPU, extract text and recognize text java with Aspose OCR.
  headline: How to enable GPU for Java OCR – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes, you can pass a PDF file directly to `setImage`; the library rasterizes
      each page before OCR.
    question: Does Aspose OCR support PDF input?
  - answer: Use `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` to
      improve recognition of specialized vocabulary.
    question: How do I add custom dictionaries for domain‑specific terms?
  - answer: Currently only CUDA‑compatible NVIDIA GPUs on Windows and Linux are supported;
      macOS users fall back to CPU.
    question: Is GPU acceleration available on macOS?
  - answer: Absolutely—`OcrResult` includes a `getConfidence()` method for each `OcrWord`
      object.
    question: Can I retrieve the confidence score for each recognized word?
  - answer: A commercial Aspose OCR license is required for production deployments;
      a free evaluation license works for development and testing.
    question: What license is required for production use?
  type: FAQPage
tags:
- gpu ocr
- java ocr
- aspose ocr
- high resolution ocr
- java image processing
title: วิธีเปิดใช้งาน GPU สำหรับ Java OCR – คู่มือแบบขั้นตอนต่อขั้นตอน
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ Java OCR – คู่มือขั้นตอนต่อขั้นตอน

หากคุณกำลังมองหา **วิธีเปิดใช้งาน GPU** เมื่อดึงข้อความจากภาพด้วย Java คุณมาถูกที่แล้ว การเร่งความเร็วด้วย GPU สามารถลดเวลาการประมวลผล OCR จากหลายวินาทีเหลือส่วนเศษของวินาที โดยเฉพาะกับการสแกนความละเอียดสูง ในคู่มือนี้เราจะอธิบายขั้นตอนการติดตั้ง Aspose OCR การกำหนดค่าอุปกรณ์ GPU และการรันโปรแกรมดึงข้อความที่ทำงานได้อย่างเสถียรทั้งบนเครื่องที่เปิดใช้งาน GPU และเครื่องที่ใช้ CPU เท่านั้น

## คำตอบเร็ว
- **เวอร์ชัน Java ขั้นต่ำคืออะไร?** Java 17 or newer.
- **ประเภท GPU ที่ต้องการคืออะไร?** Any CUDA‑compatible NVIDIA GPU (CUDA 11+).
- **ฉันต้องการไลเซนส์เพื่อรันตัวอย่างหรือไม่?** A free trial works for development; a commercial license is required for production.
- **GPU OCR เร็วขึ้นกี่เท่า?** Up to 5× faster on a 4 MP image compared with CPU.
- **ฉันสามารถกลับไปใช้ CPU โดยอัตโนมัติได้หรือไม่?** Yes—Aspose OCR reverts to CPU if no GPU is detected.

## การเร่งความเร็วด้วย GPU สำหรับ OCR คืออะไร?
การเร่งความเร็วด้วย GPU สำหรับ OCR หมายถึงการรันขั้นตอนการสรุปผลของเครือข่ายประสาทเทียบบนหน่วยประมวลผลกราฟิกแทน CPU ซึ่งทำให้สามารถทำงานแบบขนานหลายพันครั้งได้ การทำเช่นนี้ลดความหน่วงของการสรุปผลอย่างมาก โดยเฉพาะสำหรับภาพความละเอียดสูงที่ CPU จะกลายเป็นคอขวด

## ทำไมต้องใช้ Aspose OCR สำหรับ Java?
Aspose OCR รองรับ **รูปแบบอินพุตกว่า 50 ประเภท** (รวมถึง PNG, JPEG, TIFF, PDF) และสามารถประมวลผลเอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ API ของ Java มีคลาส `OcrEngine` เพียงคลาสเดียวที่ซ่อนการเรียกใช้ CUDA ระดับต่ำ ทำให้คุณสามารถมุ่งเน้นที่ตรรกะธุรกิจได้

## ข้อกำหนดเบื้องต้น
- ติดตั้ง Java 17+ JDK แล้ว
- Maven 3.6+ หรือ Gradle 7+ สำหรับการจัดการ dependencies
- GPU NVIDIA ที่รองรับ CUDA พร้อมไดรเวอร์ที่ตรงกับ CUDA 11.x หรือใหม่กว่า
- การเชื่อมต่ออินเทอร์เน็ตเพื่อดาวน์โหลดไลบรารี Aspose OCR

## วิธีเปิดใช้งาน GPU สำหรับ Java OCR?
โหลดไลบรารี Aspose OCR, สร้าง `OcrEngine`, และเปิดการสนับสนุน GPU เพียงไม่กี่บรรทัดของโค้ด เอนจินจะตรวจจับอุปกรณ์ที่พร้อมใช้งานโดยอัตโนมัติ; คุณยังสามารถระบุ device ID เพื่อเลือก GPU เฉพาะในสภาพแวดล้อมที่มีหลาย GPU

## OcrEngine ทำงานอย่างไร?
`OcrEngine` เป็นคลาสหลักที่ประสานการเตรียมภาพ, การสรุปผลของเครือข่ายประสาทเทียม, และการรวมผลลัพธ์ มันรับภาพในรูปแบบเส้นทางไฟล์, วัตถุ `java.io.File`, หรืออินสแตนซ์ `java.awt.image.BufferedImage`, ทำให้คุณมีความยืดหยุ่นในการป้อนข้อมูลเข้าสู่ pipeline

## วิธีกำหนดค่า GPU acceleration (วิธีกำหนดค่า GPU)
นี่คือขั้นตอนที่คุณบอก Aspose OCR ให้ใช้ GPU และเลือกอุปกรณ์ใด

เพื่อเปิดใช้งาน GPU acceleration คุณสร้างอินสแตนซ์ `GpuConfiguration`, ตั้งค่า `setEnable(true)`, สามารถเลือกอุปกรณ์ด้วย `setDeviceId(int)` ได้ตามต้องการ, แล้วแนบเข้ากับ `OcrEngine` ผ่าน `setGpuConfiguration`. การกำหนดค่านี้ยังให้คุณกำหนดกลยุทธ์ fallback เช่น การกลับไปใช้ CPU เมื่ออุปกรณ์ที่ร้องขอไม่พร้อมใช้งาน เพื่อให้แอปพลิเคชันคงเสถียร  
```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

ทำไมต้องเปิดใช้ GPU? pipeline OCR รันหลาย convolutional neural network การดำเนินงานเหล่านี้บน GPU ใช้ประโยชน์จากคอร์ขนานหลายพันคอร์ ลดเวลาการสรุปผลจาก 3–5 วินาทีบน CPU เหลือน้อยกว่า 1 วินาทีบน RTX 3080 รุ่นใหม่สำหรับภาพ 4 MP หากอุปกรณ์ที่ระบุไม่มีอยู่ Aspose จะกลับไปใช้ CPU อย่างเงียบ ๆ เพื่อป้องกันการขัดข้อง

### การจัดการกรณีขอบ
แอปพลิเคชันที่มั่นคงต้องตรวจสอบว่ามีการติดตั้งไดรเวอร์ CUDA ก่อนที่จะทำงานกับ GPU  
```java
        // Verify that a GPU was actually engaged
        if (!gpuConfig.isEnabled() || !gpuConfig.isDeviceAvailable()) {
            System.out.println("GPU not detected – falling back to CPU. " +
                               "Performance will be slower.");
        }
```

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR และเตรียมภาพของคุณ (วิธีเปิดใช้งาน GPU)

แรกสุดให้เพิ่ม dependency ของ Aspose OCR เข้าไปในโปรเจกต์ของคุณ หากคุณใช้ Maven ให้เพิ่ม:  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

ผู้ใช้ Gradle สามารถเพิ่ม:  
```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

วางไฟล์ความละเอียดสูง (เช่น `sample-highres.png`) ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ดได้ ภาพควรมีความละเอียดอย่างน้อย 300 dpi เพื่อความแม่นยำสูงสุดของ OCR  

> **เคล็ดลับ:** หากคุณกำลังทดสอบบนแล็ปท็อปที่ไม่มี GPU แยก คุณยังสามารถรันโค้ดได้; เอนจินจะกลับไปใช้ CPU โดยอัตโนมัติ  

![ภาพประกอบวิธีเปิดใช้งาน GPU](placeholder.png "แผนภาพแสดง pipeline OCR ของ Java พร้อมการเร่งความเร็วด้วย GPU – วิธีเปิดใช้งาน GPU")
[ภาพประกอบวิธีเปิดใช้งาน GPU](placeholder.png "แผนภาพแสดง pipeline OCR ของ Java พร้อมการเร่งความเร็วด้วย GPU – วิธีเปิดใช้งาน GPU")

## ขั้นตอนที่ 2 – สร้าง OCR engine และโหลดภาพ (ดึงข้อความจากภาพ)

`OcrEngine` เป็นอ็อบเจ็กต์ระดับบนสุดที่แทนเซสชัน OCR หนึ่งครั้ง.  
```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.*;

public class GpuOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to process
        // Replace with the absolute or relative path to your PNG/JPEG/TIFF
        ocrEngine.setImage("YOUR_DIRECTORY/sample-highres.png");
```

เมธอด `setImage` รับพาธไฟล์, `java.io.File`, หรือ `java.awt.image.BufferedImage`. การใช้แหล่งที่มาความละเอียดสูงทำให้ GPU มีพิกเซลเพียงพอให้คอร์ทั้งหมดทำงานเต็มที่ ซึ่งส่งผลให้เห็นการเพิ่มความเร็วอย่างชัดเจน

## ขั้นตอนที่ 3 – กำหนดค่า GPU acceleration (วิธีกำหนดค่า GPU)

อ็อบเจ็กต์ `GpuConfiguration` ให้คุณเปิดการใช้ GPU, เลือกอุปกรณ์, และกำหนดพฤติกรรม fallback สำหรับ OCR engine.  
```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

## ขั้นตอนที่ 4 – ทำการจดจำข้อความ (recognize text java)

เมื่อเอนจินและ GPU พร้อมแล้ว คุณสามารถดึงอักขระได้ในที่สุด เมธอด `recognize()` รัน pipeline OCR และคืนค่า `OcrResult` ที่มีข้อความธรรมดา, คะแนนความมั่นใจ, และข้อมูล bounding‑box ทางเลือก  
```java
        // Step 4: Perform the recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนเพื่อความกระชับ):  
```
Recognized text:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

หากภาพของคุณมีหลายภาษา คุณสามารถเพิ่ม language pack ก่อนเรียก `recognize()` ได้:  
```java
ocrEngine.getLanguage().add(OcrLanguage.FRENCH);
ocrEngine.getLanguage().add(OcrLanguage.SPANISH);
```

## ขั้นตอนที่ 5 – ตรวจสอบผลลัพธ์และขั้นตอนต่อไป

รันโปรแกรมด้วย:  
```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrTutorial
```

บนเครื่องที่มี GPU ที่ดีพอ OCR จะเสร็จสิ้นใน **น้อยกว่าวินาทีเดียวสำหรับภาพ 4 MP**, เทียบกับ 3–5 วินาทีบน CPU เพียงอย่างเดียว การเพิ่มความเร็วนี้มีคุณค่าอย่างยิ่งในสถานการณ์การประมวลผลเป็นชุดหรือ pipeline การรับเอกสารแบบเรียลไทม์

### คำถามทั่วไป
* **ถ้าฉันได้รับข้อผิดพลาด “CUDA driver version is insufficient” จะทำอย่างไร?**  
  อัปเดตไดรเวอร์ NVIDIA ของคุณเป็นเวอร์ชันล่าสุดที่ตรงกับชุดเครื่องมือ CUDA ที่รวมมาใน Aspose (โดยทั่วไปคือ CUDA 11.x ในปี 2026).

* **ฉันสามารถประมวลผลชุดของภาพได้หรือไม่?**  
  ได้. ใช้ `OcrEngine` ตัวเดียวซ้ำภายในลูปเพื่อหลีกเลี่ยงการสร้าง context GPU ซ้ำ ซึ่งจะเพิ่มอัตราการทำงาน

* **มีขีดจำกัดหน่วยความจำหรือไม่?**  
  การใช้หน่วยความจำ GPU จะสเกลตามขนาดภาพ; สำหรับ TIFF ขนาดใหญ่มาก ให้แบ่งภาพเป็นส่วนย่อยก่อนป้อนให้เอนจินเพื่อให้อยู่ในขีดจำกัดหน่วยความจำ GPU ปกติที่ประมาณ 8 GB

### เคล็ดลับเชิงมืออาชีพ
* **Pin the GPU** – ในเซิร์ฟเวอร์ที่มีหลาย GPU ให้ตั้งค่า `gpuConfig.setDeviceId(1)` เพื่อจอง GPU ตัวที่สองสำหรับ OCR ส่วน GPU ตัวแรกทำงานอื่น.  
* **Warm‑up** – เรียก `ocrEngine.recognize()` กับภาพ dummy ขนาดเล็กหนึ่งครั้งตอนเริ่มต้น; การทำเช่นนี้โหลด neural net ไปยัง GPU ทำให้ไม่มีความหน่วงของการเรียกครั้งแรก.  
* **Thread safety** – แต่ละเธรดควรมีอินสแตนซ์ `OcrEngine` ของตนเอง; คลาสนี้ไม่ปลอดภัยต่อการทำงานหลายเธรด, การแชร์ระหว่างเธรดอาจทำให้เกิด race condition.

## คำถามที่พบบ่อย

**Q: Aspose OCR รองรับการป้อน PDF หรือไม่?**  
A: ใช่, คุณสามารถส่งไฟล์ PDF ไปยัง `setImage` โดยตรง; ไลบรารีจะทำการแปลง raster แต่ละหน้า ก่อนทำ OCR  

**Q: ฉันจะเพิ่มพจนานุกรมกำหนดเองสำหรับคำเฉพาะโดเมนได้อย่างไร?**  
A: ใช้ `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` เพื่อปรับปรุงการจดจำคำศัพท์เฉพาะ  

**Q: การเร่งความเร็วด้วย GPU มีให้ใช้บน macOS หรือไม่?**  
A: ปัจจุบันรองรับเฉพาะ GPU NVIDIA ที่เข้ากันได้กับ CUDA บน Windows และ Linux; ผู้ใช้ macOS จะต้องใช้ CPU  

**Q: ฉันสามารถดึงคะแนนความมั่นใจสำหรับแต่ละคำที่จดจำได้หรือไม่?**  
A: แน่นอน—`OcrResult` มีเมธอด `getConfidence()` สำหรับแต่ละอ็อบเจ็กต์ `OcrWord`  

**Q: ต้องการไลเซนส์แบบใดสำหรับการใช้งานในผลิตภัณฑ์?**  
A: จำเป็นต้องมีไลเซนส์ Aspose OCR เชิงพาณิชย์สำหรับการใช้งานในผลิตภัณฑ์; ไลเซนส์ประเมินผลฟรีใช้ได้สำหรับการพัฒนาและทดสอบ  

**อัปเดตล่าสุด:** 2026-11-17  
**ทดสอบด้วย:** Aspose OCR 24.11 for Java  
**ผู้เขียน:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

## บทแนะนำที่เกี่ยวข้อง

- [ตัวอย่าง Aspose OCR Java ดึงข้อความจากภาพด้วย GPU](/ocr/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/)
- [จดจำข้อความจากภาพด้วย Java OCR พร้อมการเร่งความเร็วด้วย GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [บทแนะนำ OCR เร่งความเร็วด้วย GPU สำหรับ Java: คู่มือแปลงภาพเป็นข้อความอย่างรวดเร็ว](/ocr/java/advanced-ocr-techniques/gpu-accelerated-ocr-tutorial-java-guide-to-fast-image-to-tex/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
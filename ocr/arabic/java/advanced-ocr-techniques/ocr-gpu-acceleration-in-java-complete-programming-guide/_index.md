---
category: general
date: 2026-06-25
description: تسريع OCR باستخدام GPU في جافا يتيح لك التعرف على النص من الصورة بسرعة.
  تعلم استخراج النص من ملف JPG، ضبط حد ذاكرة GPU، ومعالجة الصورة باستخدام OCR.
draft: false
keywords:
- ocr gpu acceleration
- recognize text from image
- extract text from jpg
- set gpu memory limit
- process image with OCR
language: ar
og_description: تسريع OCR باستخدام GPU في جافا يساعدك على التعرف على النص من الصورة
  بسرعة. اكتشف كيفية استخراج النص من ملفات JPG، وتحديد حد ذاكرة الـ GPU، ومعالجة الصورة
  باستخدام OCR.
og_title: دليل كامل لتسريع OCR باستخدام GPU في جافا
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: OCR GPU acceleration in Java lets you recognize text from image quickly.
    Learn to extract text from jpg, set GPU memory limit, and process image with OCR.
  headline: OCR GPU Acceleration in Java – Complete Programming Guide
  type: TechArticle
- description: OCR GPU acceleration in Java lets you recognize text from image quickly.
    Learn to extract text from jpg, set GPU memory limit, and process image with OCR.
  name: OCR GPU Acceleration in Java – Complete Programming Guide
  steps:
  - name: Point to the Image You Want to Process
    text: '```java // Step 1 – Specify the image file (can be a JPG, PNG, BMP, etc.)
      String imagePath = "YOUR_DIRECTORY/sample.jpg"; ```'
  - name: Build an OCR Configuration with GPU Support
    text: '```java // Step 2 – Create OCR configuration and turn on GPU acceleration
      OcrConfig ocrConfig = new OcrConfig() .setGpuSettings(new GpuSettings() .setEnabled(true)
      // <-- enable GPU usage .setDeviceId(0) // first GPU in the system .setMemoryLimitMb(4096));
      // optional: set GPU memory limit ```'
  - name: Instantiate the OCR Engine
    text: '```java // Step 3 – Create the OCR engine with the GPU‑enabled configuration
      AsposeOCR ocrEngine = new AsposeOCR(ocrConfig); ```'
  - name: Run the Recognition
    text: '```java // Step 4 – Perform text recognition on the chosen image ImageRecognitionResult
      result = ocrEngine.recognizeImage(imagePath); ```'
  - name: Output the Recognized Text
    text: '```java // Step 5 – Print the extracted text to the console System.out.println("Recognized
      text:

      " + result.getText()); ```'
  type: HowTo
tags:
- Java
- OCR
- GPU
title: تسريع OCR باستخدام GPU في جافا – دليل برمجة شامل
url: /ar/java/advanced-ocr-techniques/ocr-gpu-acceleration-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تسريع OCR باستخدام GPU في جافا – دليل برمجة كامل

هل تساءلت يومًا كيف يمكن لتقنية **ocr gpu acceleration** أن توفر ثوانٍ من عملية استخراج النص؟ إذا كنت تتصفح يدويًا صفحات من ملفات PDF الممسوحة ضوئيًا أو تعاني من بطء OCR المعتمد على CPU فقط، فأنت لست وحدك. ببضع أسطر من جافا يمكنك **recognize text from image** بسرعة، حتى عندما تكون ملفات JPG كبيرة.

في هذا الدرس سنستعرض مثالًا واقعيًا يوضح لك كيفية **extract text from jpg**، وضبط حد للذاكرة باستخدام **set gpu memory limit**، وأخيرًا **process image with OCR** باستخدام مكتبة Aspose Java SDK. في النهاية ستحصل على برنامج جاهز للنسخ واللصق يعمل على أي جهاز يحتوي على GPU مدعوم.

## ما ستحتاجه

| المتطلب المسبق | سبب أهميته |
|--------------|------------|
| Java 17 (أو أحدث) | مكتبة Aspose OCR تستهدف إصدارات JDK الحديثة. |
| Maven أو Gradle | لجلب تبعية `aspose-ocr`. |
| GPU متوافق مع CUDA (NVIDIA) بذاكرة VRAM لا تقل عن 4 GB | يُمكّن **ocr gpu acceleration**؛ وإلا سيعود SDK إلى CPU. |
| ملف صورة (`sample.jpg`) تريد قراءته | سنقوم **extract text from jpg** في العرض. |

إذا كان أي من هذه العناصر مفقودًا، سيظل الكود يعمل—لكن توقع أداءً أبطأ.

## OCR GPU Acceleration – إعداد البيئة

أولًا، أضف مكتبة Aspose OCR إلى مشروعك. مع Maven يبدو الأمر هكذا:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the latest version -->
</dependency>
```

> **نصيحة احترافية:** حافظ على تحديث رقم الإصدار؛ الإصدارات الأحدث غالبًا ما تقدم دعمًا أفضل للـ GPU وإصلاحات للأخطاء.

بعد حل التبعية، أنت جاهز لتفعيل **ocr gpu acceleration**.

## Recognize Text from Image Using Aspose OCR

جوهر الحل يكمن في أربع خطوات بسيطة. لنفصلها.

### الخطوة 1: تحديد مسار الصورة التي تريد معالجتها

```java
// Step 1 – Specify the image file (can be a JPG, PNG, BMP, etc.)
String imagePath = "YOUR_DIRECTORY/sample.jpg";
```

> **لماذا؟** يحتاج محرك OCR إلى مسار ملف محدد؛ المسارات النسبية تعمل أيضًا طالما يستطيع JVM العثور على الملف.

### الخطوة 2: بناء تكوين OCR يدعم GPU

```java
// Step 2 – Create OCR configuration and turn on GPU acceleration
OcrConfig ocrConfig = new OcrConfig()
        .setGpuSettings(new GpuSettings()
                .setEnabled(true)          // <-- enable GPU usage
                .setDeviceId(0)            // first GPU in the system
                .setMemoryLimitMb(4096));  // optional: set GPU memory limit
```

* `setEnabled(true)` هو المفتاح الذي يخبر Aspose باستخدام الـ GPU بدلاً من الـ CPU.  
* `setDeviceId(0)` يختار أول GPU؛ غيّر الفهرس إذا كان لديك عدة بطاقات.  
* `setMemoryLimitMb(4096)` **set gpu memory limit** إلى 4 GB، مما يمنع تعطل الذاكرة عند الصور الكبيرة. اضبط هذه القيمة وفقًا لمواصفات جهازك.

### الخطوة 3: إنشاء كائن محرك OCR

```java
// Step 3 – Create the OCR engine with the GPU‑enabled configuration
AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);
```

المحرك الآن يعرف أنه يجب توجيه العمليات الثقيلة إلى الـ GPU، مما يترجم إلى أوقات تعرف أسرع—خاصةً للصور عالية الدقة.

### الخطوة 4: تشغيل عملية التعرف

```java
// Step 4 – Perform text recognition on the chosen image
ImageRecognitionResult result = ocrEngine.recognizeImage(imagePath);
```

خلف الكواليس، يقوم SDK ببث الصورة إلى الـ GPU، تشغيل شبكة عصبية تلافيفية، وإرجاع كائن نتيجة يحتوي على النص المستخرج.

### الخطوة 5: إخراج النص المتعرف عليه

```java
// Step 5 – Print the extracted text to the console
System.out.println("Recognized text:\n" + result.getText());
```

**الناتج المتوقع** (مقتطع للت brevity):

```
Recognized text:
Hello, world!
This is a sample image containing text.
```

إذا لم يتوفر الـ GPU، يقوم Aspose تلقائيًا بالتحول إلى وضع CPU ويطبع تحذيرًا—وبالتالي لا يتعطل برنامجك.

## استخراج النص من JPG – معالجة مسارات الملفات

عند التعامل مع **extract text from jpg**، من الشائع مواجهة مشاكل ترميز المسار على Windows. نهج آمن هو استخدام `java.nio.file.Paths`:

```java
import java.nio.file.Paths;

// Convert a possibly relative path to an absolute one
String absolutePath = Paths.get(imagePath).toAbsolutePath().toString();
ImageRecognitionResult result = ocrEngine.recognizeImage(absolutePath);
```

هذه اللمسة الصغيرة تُزيل مفاجآت “الملف غير موجود”، خاصةً عندما تشغل البرنامج من IDE مقارنةً بسطر الأوامر.

## ضبط حد ذاكرة GPU لأداء مستقر

قد تتساءل لماذا نستخدم `setMemoryLimitMb`. تُخصص الـ GPUs الحديثة الذاكرة حسب الحاجة، ويمكن لمهمة OCR غير مُتحكم فيها أن تستهلك كل الـ VRAM، مما يؤدي إلى إيقاف العملية. بتحديد حد للذاكرة:

```java
.setMemoryLimitMb(2048) // limit to 2 GB if your GPU is modest
```

تحمِ نظامك من نقص موارد الرسوميات. إذا كان الحد منخفضًا جدًا، سيقوم SDK تلقائيًا بالتحويل إلى RAM النظام، وهو أبطأ لكنه لا يزال يعمل.

> **احذر من:** ضبط الحد أقل من حجم الذاكرة المطلوبة للصورة قد يسبب `GpuMemoryException`. في هذه الحالة، إما زد الحد أو قلل حجم الصورة قبل OCR.

## معالجة الصورة باستخدام OCR – مثال كامل من البداية للنهاية

بدمج كل ما سبق، إليك فئة كاملة جاهزة للتنفيذ:

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.config.GpuSettings;
import com.aspose.ocr.config.OcrConfig;
import com.aspose.ocr.ImageRecognitionResult;
import java.nio.file.Paths;

public class GpuExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Specify the image to be processed
        String imagePath = "YOUR_DIRECTORY/sample.jpg";

        // 2️⃣ Build OCR configuration with GPU acceleration enabled
        OcrConfig ocrConfig = new OcrConfig()
                .setGpuSettings(new GpuSettings()
                        .setEnabled(true)          // enable GPU usage
                        .setDeviceId(0)            // select the first GPU device
                        .setMemoryLimitMb(4096));  // optional memory limit

        // 3️⃣ Create the OCR engine using the configured settings
        AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);

        // 4️⃣ Convert to absolute path (helps when extracting text from jpg)
        String absolutePath = Paths.get(imagePath).toAbsolutePath().toString();

        // 5️⃣ Perform text recognition on the image
        ImageRecognitionResult recognitionResult = ocrEngine.recognizeImage(absolutePath);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + recognitionResult.getText());
    }
}
```

**تشغيل البرنامج**:

```bash
$ mvn compile exec:java -Dexec.mainClass=GpuExample
```

سترى طباعة في وحدة التحكم للنص الموجود في `sample.jpg`. إذا لاحظت أن العملية تستغرق أكثر من بضع ثوانٍ، تحقق من تحديث برنامج تشغيل الـ GPU وتأكد من أن علم `setGpuSettings().setEnabled(true)` مُفعَّل (سيتضمن السجل سطرًا مثل *“GPU acceleration enabled – device 0”*).

## أسئلة شائعة وحالات خاصة

| السؤال | الإجابة |
|--------|----------|
| **ماذا لو لم يكن لدي GPU؟** | يتراجع SDK بأناقة إلى وضع CPU. يمكنك الاستمرار باستخدام نفس الكود؛ فقط اضبط `setEnabled(false)` أو احذف كتلة `GpuSettings`. |
| **صورةي بدقة 8 K – هل ستعمل؟** | نعم، لكن قد تحتاج إلى رفع قيمة `setMemoryLimitMb` أو تقليل حجم الصورة لتجنب `GpuMemoryException`. |
| **هل يمكنني معالجة مجموعة من الصور؟** | ضع استدعاء التعرف داخل حلقة. إعادة استخدام نفس كائن `AsposeOCR` أكثر كفاءة لأن سياق الـ GPU يبقى فعالًا. |
| **هل هناك طريقة للحصول على درجات الثقة؟** | `ImageRecognitionResult` يوفّر `getConfidence()` لكل كتلة مُتعرف عليها؛ يمكنك تسجيلها أو تصفية النتائج ذات الثقة المنخفضة. |
| **كيف أبدل إلى جهاز GPU مختلف؟** | غيّر `setDeviceId(1)` (أو أي فهرس يطابق بطاقتك الثانية). استخدم `nvidia-smi` لعرض المعرفات. |

## نصائح للنشر في بيئات الإنتاج

1. **تسخين الـ GPU** – شغّل صورة تجريبية صغيرة مرة واحدة عند بدء التشغيل؛ هذا يُجنب ارتفاع زمن الاستجابة في أول استدعاء.  
2. **سلامة الخيوط** – كائن `AsposeOCR` آمن للاستخدام عبر الخيوط بعد التهيئة، لذا يمكنك مشاركته عبر a  

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
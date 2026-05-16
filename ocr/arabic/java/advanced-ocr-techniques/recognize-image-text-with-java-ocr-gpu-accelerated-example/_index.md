---
category: general
date: 2026-03-28
description: تعرّف على كيفية التعرف على نص الصور في جافا باستخدام Aspose OCR، واستخراج
  نص ملفات PNG، واستخدام تسريع GPU للحصول على OCR سريع للصور الكبيرة.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: ar
og_description: اكتشف كيفية التعرف على نص الصورة في جافا، استخراج نص ملفات PNG، واستخدام
  تسريع GPU للتعرف الضوئي على الأحرف للصور الكبيرة.
og_title: التعرف على نص الصورة باستخدام Java OCR – مثال مع تسريع GPU
tags:
- OCR
- Java
- GPU
title: التعرف على نص الصورة باستخدام Java OCR – مثال مُسرّع بالمعالج الرسومي
url: /ar/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على نص الصورة باستخدام Java OCR – مثال مع تسريع GPU

هل احتجت يومًا إلى **التعرف على نص الصورة** من ملف PNG ضخم لكن نسخة الـ CPU كانت بطيئة جدًا؟ لست وحدك. في العديد من خطوط الأنابيب الواقعية—مثل مسح الفواتير أو أرشفة الوثائق التاريخية—يمكن أن يصبح حجم الصورة هائلًا، ومحرك OCR الافتراضي لا يستطيع مواكبة السرعة.  

الخبر السار: Aspose OCR for Java يتيح لك **استخدام تسريع GPU** لتسريع العملية، والكود مضغوط بشكل مفاجئ. في هذا البرنامج التعليمي ستشاهد مثالًا كاملاً وقابلًا للتنفيذ بلغة Java OCR **يستخرج نص PNG**، ويستفيد من GPU مفعَّل بـ CUDA، ويتعامل مع **OCR large image** ببضع أسطر من الكود فقط. في النهاية ستعرف بالضبط كيف تُدمج ذلك في مشروع Java الخاص بك ولماذا كل إعداد مهم.

## ما ستتعلمه

- كيفية إعداد Aspose OCR في مشروع Maven أو Gradle.  
- العملية خطوة بخطوة **للتعرف على نص الصورة** على الـ GPU.  
- لماذا يمكن لتكوين عدد تدفقات GPU تحسين الإنتاجية.  
- كيفية التحقق من المخرجات ومعالجة المشكلات الشائعة.  

> **المتطلبات المسبقة** – Java 17 (أو أحدث)، GPU متوافق مع CUDA مع أحدث برنامج تشغيل، ورخصة صالحة لـ Aspose OCR for Java (الإصدار التجريبي المجاني يكفي للتقييم). لا توجد مكتبات خارجية أخرى مطلوبة.

---

## الخطوة 1: إضافة تبعية Aspose OCR

أولاً، أضف مكتبة Aspose OCR إلى بناء المشروع. إذا كنت تستخدم **Maven**، أضف المقتطف التالي إلى ملف `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

لـ **Gradle**، ضع هذا في `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **نصيحة احترافية:** أحدث نسخة (اعتبارًا من مارس 2026) تتضمن تحسينات أداء لأعباء عمل GPU، لذا احرص دائمًا على سحب أحدث إصدار.

---

## الخطوة 2: تهيئة محرك OCR وتمكين GPU

إنشاء محرك OCR سهل. الجزء الحاسم هو تشغيل علامة GPU—وإلا سيعود المحرك إلى وضع CPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### لماذا تمكين GPU؟

عند تمكين `setUseGpu(true)`، تقوم Aspose بنقل حسابات الشبكة العصبية التلافيفية الثقيلة إلى بطاقة الرسوميات. هذا يمكن أن يقلل الثواني من وقت معالجة **ocr large image**، خاصةً عندما يتجاوز حجم الصورة 4000 × 4000 بكسل. إذا كان بيئتك لا تحتوي على GPU متوافق، فإن الاستدعاء يصبح مجرد لا فعل (no‑op) ويستمر المحرك على CPU—بدون تعطل، فقط بأداء أبطأ.

---

## الخطوة 3: التعرف على صورة PNG واستخراج نصها

الآن وجه المحرك إلى الملف الذي تريد معالجته. يستخدم المثال `sample-large.png`، لكن يمكنك استبداله بأي ملف PNG أو JPEG.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

هذا الإخراج يؤكد أن عملية **recognize image text** نجحت وأنك **extract text png** بنجاح.

---

## الخطوة 4: التحقق من استخدام GPU (اختياري لكن مفيد)

إذا كنت تتساءل ما إذا كان الـ GPU يُستَخدم فعلاً، افتح أداة مراقبة GPU في نظامك (مثل `nvidia-smi` على لينكس). أثناء تشغيل عملية Java، يجب أن ترى ارتفاعًا طفيفًا في استهلاك الذاكرة واستخدام الحوسبة.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

إذا لم تشاهد أي نشاط، تحقق من التالي:

1. أن برنامج تشغيل CUDA يتطابق مع طراز الـ GPU.  
2. أن استدعاء `setUseGpu(true)` لم يتم تجاوزه لاحقًا في الكود.  
3. أن ملف الترخيص الخاص بك (إن وجد) لا يقيد استخدام GPU.

---

## الخطوة 5: معالجة الحالات الحدية الشائعة

### صور كبيرة تتجاوز ذاكرة GPU

عندما تكون الصورة ضخمة (مثلاً 8000 × 8000 بكسل)، قد تنفد ذاكرة الـ GPU. حل سريع هو تقليل حجم الصورة قبل تمريرها إلى Aspose:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

ثم مرّر `"sample-resized.png"` إلى `recognizeImage`. هذا يحافظ على دقة OCR مع البقاء ضمن حدود GPU.

### ملفات PDF متعددة الصفحات

يمكن لـ Aspose OCR أيضًا معالجة ملفات PDF صفحة بصفحة. قم بالتكرار على كل صفحة، حوّلها إلى صورة، ومرّرها إلى المحرك. نفس علامة **use gpu acceleration** تنطبق، مما يمنحك خط أنابيب PDF‑to‑text سريع.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي الفئة الكاملة بلغة Java، جاهزة للترجمة والتنفيذ. استبدل `YOUR_DIRECTORY` بمسار ملف PNG الخاص بك.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**الإخراج المتوقع** – تمثيل نصي عادي لكل ما استطاع المحرك قراءته من الصورة. إذا احتوت الصورة على جدول، ستحصل على محتويات الخلايا متصلة بفواصل أسطر؛ Aspose لا يحافظ على التخطيط، لكن يمكنك معالجة السلسلة لاحقًا إذا لزم الأمر.

---

## الأسئلة المتكررة

| السؤال | الجواب |
|----------|--------|
| **هل أحتاج إلى رخصة مدفوعة؟** | النسخة التجريبية تعمل حتى 200 صفحة وتزيل العلامة المائية لـ OCR. للإنتاج، الرخصة تزيل الحدود وتفتح كامل مجموعة GPU. |
| **ماذا لو كان الـ GPU قديمًا (مثل GTX 750)؟** | قد يعمل الـ GPU القديم لكن بسرعة أقل؛ تأكد من أن لديك على الأقل Compute Capability 3.0. |
| **هل يمكنني معالجة ملفات JPG أو BMP؟** | بالتأكيد—`recognizeImage` يقبل أي صيغة يدعمها Java ImageIO. |
| **هل هناك طريقة لمعالجة دفعة من الصور؟** | ضع استدعاء OCR داخل حلقة، وفكّر في زيادة `setGpuStreams` لتطابق عدد التدفقات المتزامنة التي تريدها. |
| **ماذا إذا كنت أحتاج للحفاظ على التخطيط؟** | استخدم `LayoutOptions` في Aspose OCR للحصول على إطارات الحدود؛ هذا خارج نطاق هذا الدليل السريع لكنه موثق في الـ API. |

---

## الخلاصة

أصبح لديك الآن مثال **java ocr** مختصر وشامل **يتعرف على نص الصورة**، **يستخرج نص PNG**، و**يستخدم تسريع GPU** لتسريع معالجة **ocr large image**. من خلال تعديل عدد تدفقات GPU، وإذا لزم الأمر تقليل حجم الصور الضخمة، يمكنك تكييف الحل مع أي تكوين عتادي تقريبًا.

هل أنت مستعد للخطوة التالية؟ جرّب تغذية مجلد من الإيصالات الممسوحة ضوئيًا عبر نفس الخط الأنابيب، أو جرب واجهة `TextRegion` في Aspose للحفاظ على التخطيط الأصلي. وإذا واجهت أي صعوبات، فإن منتديات Aspose وJavadoc موارد ممتازة—تذكر الأساسيات التي غطيناها هنا.

برمجة سعيدة، ولتكن OCR الخاص بك سريعة كالبرق!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
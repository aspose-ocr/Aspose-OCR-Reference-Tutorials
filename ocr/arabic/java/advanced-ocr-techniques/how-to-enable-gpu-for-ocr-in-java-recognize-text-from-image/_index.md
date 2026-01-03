---
category: general
date: 2026-01-02
description: كيفية تمكين وحدة معالجة الرسومات (GPU) في Java OCR للتعرف على النص من
  الصورة بسرعة. تعلم استخراج النص من PNG، وضبط خيارات الصورة، والتعرف على النص بكفاءة.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from png
- how to set image
- how to recognize text
language: ar
og_description: كيفية تمكين وحدة معالجة الرسومات (GPU) في Java OCR للتعرف على النص
  من الصورة بسرعة. يوضح هذا الدليل كيفية استخراج النص من PNG، وضبط خيارات الصورة،
  والتعرف على النص بكفاءة.
og_title: كيفية تمكين GPU للتعرف الضوئي على الحروف في جافا – التعرف على النص من الصورة
  بسرعة
tags:
- OCR
- Java
- GPU
title: كيفية تمكين وحدة معالجة الرسومات (GPU) للتعرف الضوئي على الأحرف (OCR) في جافا
  – التعرف السريع على النص من الصورة
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين وحدة معالجة الرسومات (GPU) لتقنية OCR في جافا – التعرف على النص من الصورة بسرعة

تمكين وحدة معالجة الرسومات (GPU) في تطبيق OCR الخاص بجافا هو عائق شائع للمطورين الذين يحتاجون إلى استخراج نص سريع. في هذا الدرس سنوضح لك **كيفية تمكين GPU**، والتعرف على النص من الصورة، واستخراج النص من PNG باستخدام مكتبة Aspose OCR.  

إذا سبق لك أن واجهت عملية OCR بطيئة وتساءلت ما إذا كانت بطاقة الرسومات يمكنها تسريع الأمور، فأنت في المكان الصحيح. سنغطي أيضًا كيفية ضبط خيارات معالجة الصورة حتى يقرأ محرك OCR ملفاتك بدقة، وسنجيب على الأسئلة المتكررة حول “كيفية التعرف على النص”.

## ما ستحتاجه

- **Java 17** أو أحدث (الكود يمكن أن يُترجم مع إصدارات أقدم، لكن 17 هو الخيار المثالي).  
- **Aspose OCR for Java** – يمكنك الحصول على أحدث ملف JAR من موقع Aspose أو Maven Central.  
- جهاز **مدعوم بـ GPU** (NVIDIA RTX 3060 أو أي بطاقة متوافقة مع CUDA ستكفي).  
- ملف صورة للاختبار – PNG لفاتورة كبيرة يعمل بشكل ممتاز لتقييم الأداء.

> **نصيحة احترافية:** إذا كنت تستخدم لابتوب ببطاقة رسومات مدمجة، تأكد من اختيار بطاقة GPU المنفصلة في إعدادات التعريف؛ وإلا ستعود المكتبة إلى المعالج المركزي (CPU) بصمت.

![مثال على تمكين GPU](image.png "مثال على تمكين GPU")

*نص بديل: مثال على تمكين GPU يظهر مقتطف كود جافا.*

## الخطوة 1 – تثبيت Aspose OCR والتحقق من توفر GPU

قبل أن تتمكن من *كيفية تمكين GPU*، تحتاج إلى إضافة المكتبة إلى مسار الفئات (classpath). أضف تبعية Maven (أو ضع ملف JAR في `libs/`):

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

بمجرد إضافة التبعية، نفّذ فحص سريع للتأكد من التوافر:

```java
import com.aspose.ocr.GpuSettings;

public class GpuCheck {
    public static void main(String[] args) {
        GpuSettings settings = new GpuSettings();
        System.out.println("GPU enabled? " + settings.getEnable());
        System.out.println("Detected GPU count: " + settings.getDeviceCount());
    }
}
```

إذا أظهر الإخراج عدد أجهزة غير صفرية، فإن JVM يكتشف وجود GPU. إذا أظهر الصفر، تحقق مرة أخرى من تثبيت التعريف وأن متغيّر البيئة `CUDA_PATH` مضبوط.

## الخطوة 2 – كيفية تمكين GPU في Aspose OCR

الآن بعد أن النظام اعترف ببطاقة الرسومات، لنقم بتفعيلها فعليًا. الكلمة المفتاحية الأساسية تظهر مباشرة في العنوان، لتلبية قاعدة تحسين محركات البحث.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.GpuSettings;
import com.aspose.ocr.ImageProcessingOptions;
import com.aspose.ocr.RecognitionLanguage;
import com.aspose.ocr.OcrResult;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // 2️⃣ Enable GPU processing (auto‑detects available device)
        GpuSettings gpuSettings = new GpuSettings();
        gpuSettings.setEnable(true);          // turn GPU on
        gpuSettings.setDeviceId(0);           // first GPU (change if you have multiple)
        ocrEngine.setGpuSettings(gpuSettings);

        // 3️⃣ Optimize image preprocessing for GPU performance
        ImageProcessingOptions imgOpts = new ImageProcessingOptions();
        imgOpts.setAutoDeskew(true);
        imgOpts.setBinarization(true);
        ocrEngine.setImageProcessingOptions(imgOpts);

        // 4️⃣ Recognize text from an image file (PNG in this case)
        OcrResult result = ocrEngine.recognizeImage(
                "YOUR_DIRECTORY/large_invoice.png",
                RecognitionLanguage.ENGLISH);

        // 5️⃣ Output the detected text
        System.out.println("Detected text:\n" + result.getText());
    }
}
```

### لماذا تمكين GPU؟

تسريع GPU يخفّف عبء عمليات الضرب المصفوفي الثقيلة التي تقوم بها نماذج OCR إلى آلاف الأنوية المتوازية. عمليًا ستلاحظ **سرعات 2‑5×** على بطاقة RTX 2060 متوسطة، وأكثر على البطاقات الأحدث. العيب هو استهلاك طفيف أعلى للذاكرة، لكنه عادةً ليس مشكلة للـ PNG بحجم الفاتورة المعتاد.

## الخطوة 3 – التعرف على النص من الصورة (واستخراج النص من PNG)

مع تشغيل GPU، لنركز الآن على خطوة *التعرف على النص من الصورة*. الكود أعلاه يقوم بذلك بالفعل، لكن إليك نسخة مبسطة تعزل استدعاء OCR:

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**ما ستلاحظه:** طريقة `recognizeImage` تكتشف نوع الملف تلقائيًا، لذا يمكنك تمرير JPEG أو TIFF أو PNG دون إعدادات إضافية. لهذا السبب *استخراج النص من PNG* يعمل مباشرةً.

### معالجة الملفات الكبيرة

إذا كان حجم PNG أكبر من 5 MB، فكر في تصغيره قبل OCR:

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

التقليل من الدقة يقلل من استهلاك ذاكرة GPU وغالبًا ما يحسن الدقة لأن النموذج يرى حوافًا أنظف.

## الخطوة 4 – كيفية ضبط خيارات الصورة للحصول على دقة أفضل

عبارة *كيفية ضبط الصورة* تظهر طبيعيًا عندما نتحدث عن ما قبل المعالجة. Aspose OCR يقدم مجموعة من الإعدادات:

| الخيار                | ما يفعله                                   | القيمة النموذجية |
|-----------------------|--------------------------------------------|-----------------|
| `setAutoDeskew(true)`| يقوم بتصحيح النص المائل                    | true            |
| `setBinarization(true)`| يحول إلى أبيض وأسود لزيادة التباين        | true            |
| `setResizeFactor(x)` | يغير حجم الصورة (0 < x ≤ 1)                | 0.5‑0.8         |
| `setContrastAdjustment(y)`| يزيد التباين (0‑100)                     | 30              |

يمكنك دمجها بأي ترتيب؛ المكتبة تطبقها تسلسليًا قبل تمرير الصورة إلى الشبكة العصبية. التجربة هي المفتاح—فواتير مختلفة قد تحتاج إلى عتبات مختلفة.

## الخطوة 5 – كيفية التعرف على النص في الحالات الخاصة

حتى مع قوة GPU، هناك سيناريوهات قد تعيق OCR:

1. **مسحات منخفضة الدقة (< 150 dpi).** قم بتكبيرها أولًا أو اطلب من المستخدم مسحًا بدقة أعلى.  
2. **ملاحظات مكتوبة بخط اليد.** النموذج الافتراضي يركز على النص المطبوع؛ ستحتاج إلى نموذج مدرب خصيصًا للخطوط المتصلة.  
3. **لغات متعددة.** مرّر قائمة مفصولة بفواصل إلى `RecognitionLanguage`، مثال: `RecognitionLanguage.ENGLISH_FRENCH`.

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## النتيجة المتوقعة

تشغيل الفئة الكاملة `GpuExample` ضد `large_invoice.png` يجب أن يطبع شيئًا مشابهًا لـ:

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

إذا ظهر لك نص غير مفهوم، تحقق مرة أخرى من أن `gpuSettings.setEnable(true)` تم تفعيله فعلاً (سيسرد الطرفية جهاز GPU إذا فعلت تسجيل الأخطاء).

## الأخطاء الشائعة ونصائح احترافية

- **نسيت ضبط معرف جهاز GPU.** في الأنظمة ذات بطاقات متعددة، قد تحتاج إلى `setDeviceId(1)`.  
- **التشغيل داخل Docker بدون بيئة تشغيل NVIDIA.** أضف `--gpus all` إلى أمر `docker run`.  
- **خلط مسارات الكود بين CPU‑only وGPU‑enabled.** حافظ على وجود نسخة واحدة من `AsposeOCR` لكل خيط لتجنب تعارض الحالات.  
- **تسرب الذاكرة.** استدعِ `ocrEngine.dispose()` عند الانتهاء، خاصة في الخدمات طويلة التشغيل.

## الخلاصة

لقد استعرضنا **كيفية تمكين GPU** لـ Aspose OCR في جافا، وأظهرنا لك **كيفية التعرف على النص من الصورة**، وبيّنّا أبسط طريقة **لاستخراج النص من PNG**، وشرحنا **كيفية ضبط خيارات الصورة** للمعالجة، وتطرقنا إلى تفاصيل **كيفية التعرف على النص** في الملفات الواقعية. مع تشغيل GPU، يجب أن يصبح خط أنابيب OCR أسرع بشكل ملحوظ، مما يجعله مناسبًا للسيناريوهات ذات الإنتاجية العالية مثل معالجة الفواتير دفعةً أو مسح المستندات مباشرةً.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال النموذج الإنجليزي الافتراضي بنموذج متعدد اللغات، أو جرب خطوط معالجة مخصصة للإيصالات ذات الضوضاء. السماء هي الحد—خاصة عندما يكون لديك GPU يتولى الأعمال الثقيلة.

---

*برمجة سعيدة، ولتكن تقنية OCR لديك سريعة دائمًا!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
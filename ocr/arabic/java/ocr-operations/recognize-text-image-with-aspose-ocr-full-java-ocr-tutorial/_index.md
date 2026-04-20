---
category: general
date: 2026-02-27
description: تعلم كيفية تنفيذ مثال OCR بلغة Java باستخدام Aspose OCR، استخراج النص
  من الصورة، معالجة OCR مسبقًا، وإنشاء ملف PDF قابل للبحث باستخدام OCR في Java.
draft: false
keywords:
- recognize text image
- how to extract text
- java ocr example
- how to preprocess ocr
- aspose ocr java tutorial
og_description: مثال Java OCR باستخدام Aspose OCR في Java – دليل خطوة بخطوة لاستخراج
  النص من الصورة، ومعالجة OCR مسبقًا، وإنشاء PDF قابل للبحث باستخدام OCR.
og_title: مثال Java OCR – التعرف على نص الصورة باستخدام Aspose OCR
tags:
- OCR
- Java
- Aspose
- GPU
title: مثال جافا OCR – التعرف على صورة النص باستخدام Aspose OCR – دليل جافا OCR الكامل
url: /ar/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مثال java ocr – التعرف على نص الصورة – دليل Aspose OCR Java الكامل

إذا كنت تبحث عن **مثال java ocr** يتيح لك **استخراج النص من صورة** بسرعة وموثوقية، فأنت في المكان الصحيح. في العديد من المشاريع الواقعية، أكبر عائق ليس محرك OCR نفسه بل الحصول على الإعدادات الصحيحة—خاصة عندما تريد تسريعًا باستخدام GPU ودقة عالية. يشرح هذا الدليل برنامج Java كامل قابل للتنفيذ يُظهر **كيفية ما قبل معالجة OCR**، ويستفيد من الباني السلس لـ Aspose OCR، ويشير أيضًا إلى إنشاء **PDF قابل للبحث باستخدام OCR** لاحقًا.

## إجابات سريعة
- **ماذا يغطي هذا الدليل؟** مثال java ocr كامل باستخدام Aspose OCR، بما في ذلك إعداد GPU ومعالجة ما قبل العتبة التكيفية.  
- **هل أحتاج إلى GPU؟** لا، لكن تمكينه (`enableGpu(true)`) يسرّع المعالجة بشكل كبير على الأجهزة المدعومة.  
- **ما اللغة التي يتم توضيحها؟** الإنجليزية، لكن يمكنك التبديل إلى أي لغة مدعومة عبر الباني.  
- **كيف أستخرج النص من الصورة؟** استدعِ `ocrEngine.recognize(imagePath)` ثم اقرأ `ocrResult.getText()`.  
- **هل يمكنني إنشاء PDF قابل للبحث؟** نعم – بعد الاستخراج يمكنك دمج طبقة النص في PDF باستخدام Aspose.PDF (غير موضح هنا).

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- **Java Development Kit (JDK) 11 أو أحدث** – يدعم Aspose OCR Java 8+، لكن JDK 11 يقدم أفضل معالجة للوحدات.  
- **Aspose.OCR for Java** JAR (حمّله من موقع Aspose أو أضفه عبر Maven/Gradle).  
  مثال Maven:
  ```xml
  <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-ocr</artifactId>
      <version>23.10</version>
  </dependency>
  ```
- **برنامج تشغيل متوافق مع GPU** (CUDA 11+ إذا كنت تخطط لتمكين تسريع GPU). إذا لم يكن لديك GPU، عيّن `enableGpu(false)` وسيتراجع الكود إلى CPU.  
- **صورة عالية الدقة تجريبية** (`sample-highres.png`) موجودة في مجلد يمكنك الإشارة إليه، مثل `C:/ocr-demo/`.

هذا كل شيء—لا تحتاج إلى ملفات ثنائية أصلية إضافية أو ملفات إعداد معقدة.

![مخطط يوضح خط أنابيب OCR للتعرف على نص الصورة باستخدام Aspose OCR Java](https://example.com/ocr-pipeline.png "التعرف على نص الصورة باستخدام Aspose OCR Java")

*نص بديل للصورة: التعرف على نص الصورة باستخدام Aspose OCR Java*

## لماذا يهم هذا المثال java ocr

- **السرعة:** يمكن لتسريع GPU تقليل وقت المعالجة من ثوانٍ إلى أجزاء من الثانية على الصور الكبيرة.  
- **الدقة:** اختيار اللغة الصحيحة وتطبيق **كيفية ما قبل معالجة OCR** (العتبة التكيفية) يحسّن التعرف على الأحرف بشكل كبير.  
- **المرونة:** يمكن لاحقًا استخدام نفس المحرك لإنشاء **PDF قابل للبحث باستخدام OCR**، مما يجعل مستنداتك قابلة للبحث دون أدوات إضافية.

## الخطوة 1: إعداد محرك OCR – التعرف على نص الصورة مع الخيارات الصحيحة

أول ما نقوم به هو إنشاء كائن `OcrEngine`. توفر Aspose نمط الباني الذي يتيح لك ربط استدعاءات الإعداد، مما يجعل الشيفرة قابلة للقراءة والمرونة.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Build the OCR engine:
        // • Language: English
        // • GPU acceleration: enabled
        // • Pre‑processing: Adaptive Threshold to improve contrast
        OcrEngine ocrEngine = new OcrEngineBuilder()
                .setLanguage(Language.English)          // set OCR language
                .enableGpu(true)                        // turn on GPU (requires CUDA)
                .addPreprocessFilter(PreprocessFilter.AdaptiveThreshold) // improve binarization
                .build();
```

**لماذا هذا مهم:**  
- **اختيار اللغة** يخبر المحرك بمجموعة الأحرف المتوقعة، مما يحسّن الدقة بشكل كبير.  
- **تسريع GPU** يمكن أن يقلل وقت المعالجة من ثوانٍ إلى أجزاء من الثانية للصور الكبيرة.  
- **معالجة ما قبل العتبة التكيفية** هي حيلة كلاسيكية للتعامل مع الإضاءة غير المتساوية—بالضبط النوع من المشكلات التي تواجهها عندما تحاول **كيفية ما قبل معالجة OCR** للمستندات الممسوحة.

## الخطوة 2: التعرف على نص الصورة – تشغيل OCR

الآن بعد أن أصبح المحرك جاهزًا، نمرره إلى صورتنا. تُعيد طريقة `recognize` كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، وحتى بيانات الصناديق المحيطة إذا احتجت إليها لاحقًا.

```java
        // Path to the high‑resolution image you want to analyze
        String imagePath = "C:/ocr-demo/sample-highres.png";

        // Perform OCR – this is where we actually recognize text image
        OcrResult ocrResult = ocrEngine.recognize(imagePath);
```

**نقطة أساسية:** استدعاء `recognize` متزامن؛ ينتظر حتى ينتهي OCR. إذا كنت تعالج عشرات الملفات، فكر في تغليفه في مجموعة خيوط، لكن لصورة واحدة البساطة هي الأفضل.

## الخطوة 3: استخراج وعرض النص – كيفية استخراج النص من النتيجة

أخيرًا، نستخرج النص العادي من النتيجة ونطبعه. يمكنك أيضًا كتابته إلى ملف، أو إرساله إلى فهرس بحث، أو تمريره إلى واجهة برمجة تطبيقات ترجمة.

```java
        // Print the extracted text to the console
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());

        // Optional: you can also check confidence if needed
        System.out.println("Confidence: " + ocrResult.getConfidence());
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مثل:

```
=== OCR Output ===
This is a sample document.
It contains several lines of text.
The OCR engine recognized it successfully!
Confidence: 0.97
```

إذا كان الإخراج مشوشًا، تحقق من وضوح الصورة وأن خطوة **كيفية ما قبل معالجة OCR** (العتبة التكيفية) تتطابق مع ظروف إضاءة الصورة.

## المشكلات الشائعة والنصائح الاحترافية (مثال java ocr)

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **GPU غير مكتشف** | نقص برامج تشغيل CUDA أو GPU غير متوافق | ثبّت CUDA 11+، تحقق من عمل `nvidia-smi`، أو عيّن `.enableGpu(false)` |
| **دقة منخفضة على خلفيات داكنة** | قد تُفرط العتبة التكيفية في التنعيم | جرّب `PreprocessFilter.GaussianBlur` قبل العتبة |
| **نفاد الذاكرة على صور ضخمة** | حد ذاكرة GPU | قلّص حجم الصورة إلى عرض أقصى 2000 px قبل OCR، أو استخدم وضع CPU |
| **لغة خاطئة** | اللغة الافتراضية هي الإنجليزية، لكن المستند متعدد اللغات | استدعِ `.setLanguage(Language.French)` أو استخدم `Language.Multilingual` |

**نصيحة احترافية:** عندما تبني **مثال java ocr** للمعالجة الدفعة، احفظ كائن `OcrEngine` بدلاً من إنشائه لكل ملف. الباني رخيص، لكن إنشاء سياق GPU أصلي يمكن أن يكون مكلفًا.

## توسيع المثال – ما التالي بعد أن تستطيع التعرف على نص الصورة؟

1. **إنشاء PDF قابل للبحث باستخدام OCR** – يمكن لـ Aspose OCR دمج النص المعترف به كطبقة مخفية، محوّلًا ملفات PDF الممسوحة إلى مستندات قابلة للبحث بالكامل.  
2. **دمج مع Aspose.PDF** – ادمج ناتج OCR مع توليد PDF لإنتاج سير عمل مستندات من الطرف إلى الطرف.  
3. **OCR فيديو في الوقت الحقيقي** – التقط إطارات من كاميرا ويب، ومرّرها إلى نفس المحرك، واعرض ترجمات حية.  
4. **ما بعد المعالجة** – استخدم تعبيرات نمطية لتنظيف الأخطاء الشائعة في OCR (`"0"` مقابل `"O"`)، خاصة عندما تكون **كيفية استخراج النص** للتحليلات اللاحقة.

## الشيفرة الكاملة (جاهزة للنسخ)

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Build the OCR engine with English language, GPU acceleration,
        // and adaptive‑threshold preprocessing
        OcrEngine ocrEngine = new OcrEngineBuilder()
                .setLanguage(Language.English)
                .enableGpu(true)
                .addPreprocessFilter(PreprocessFilter.AdaptiveThreshold)
                .build();

        // Step 2: Recognize text from a high‑resolution image
        String imagePath = "C:/ocr-demo/sample-highres.png";
        OcrResult ocrResult = ocrEngine.recognize(imagePath);

        // Step 3: Print the extracted text to the console
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
        System.out.println("Confidence: " + ocrResult.getConfidence());
    }
}
```

احفظها باسم `GpuOcrDemo.java`، ثم قم بترجمتها باستخدام `javac -cp "aspose-ocr-23.10.jar;." GpuOcrDemo.java`، وشغّلها عبر `java -cp "aspose-ocr-23.10.jar;." GpuOcrDemo`. إذا تم الإعداد بشكل صحيح، ستظهر النصوص المستخرجة في الشاشة—دليل على أنك نجحت في **التعرف على نص الصورة** باستخدام Aspose OCR.

## الأسئلة المتكررة

**س: هل يمكنني إنشاء PDF قابل للبحث مباشرةً من هذا المثال؟**  
ج: نعم. بعد استخراج النص، استخدم Aspose.PDF لإنشاء PDF ودمج طبقة النص OCR، مما يحول الملف إلى PDF قابل للبحث.

**س: ماذا لو لم يكن لدي GPU متوافق مع CUDA؟**  
ج: ما عليك سوى تغيير `.enableGpu(true)` إلى `.enableGpu(false)`؛ سيعود المحرك إلى وضع CPU مع تأثير أداء معتدل فقط.

**س: كيف أتعامل مع مستندات متعددة اللغات؟**  
ج: استخدم `Language.Multilingual` أو عيّن تعداد اللغة المناسب لكل مستند قبل استدعاء `recognize`.

**س: هل هناك طريقة لمعالجة دفعة من الصور بكفاءة؟**  
ج: نعم. أنشئ كائن `OcrEngine` واحد، ثم كرّر عبر قائمة الصور، مع إمكانية استخدام مجموعة خيوط لتوازي استدعاءات `recognize`.

**س: أين يمكنني العثور على مرشحات ما قبل المعالجة المتقدمة؟**  
ج: يتضمن تعداد `PreprocessFilter` خيارات مثل `GaussianBlur`، `MedianFilter`، و`ContrastStretch`. جرّب ما يناسب مجموعة صورك.

---

**آخر تحديث:** 2026-02-27  
**تم الاختبار مع:** Aspose.OCR 23.10 for Java  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
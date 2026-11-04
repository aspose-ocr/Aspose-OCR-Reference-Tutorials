---
category: general
date: 2026-10-30
description: تعلم كيفية استخراج النص من الصورة بسرعة باستخدام دعم Aspose OCR GPU في
  Java. يوضح هذا الدليل كيفية تعيين GPU device ID وتحقيق OCR عالي الأداء.
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: تعلم كيفية استخراج النص من الصورة بسرعة باستخدام دعم Aspose OCR GPU
  في Java. يوضح هذا الدليل كيفية تعيين GPU device ID لتحقيق الأداء الأمثل.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: كيفية استخراج النص من الصورة باستخدام Aspose OCR GPU في Java
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: كيفية استخراج النص من الصورة باستخدام Aspose OCR GPU في Java
url: /ar/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص من صورة باستخدام Aspose OCR GPU في Java

إذا حاولت يومًا **استخراج النص من صورة** في تطبيق Java ووجدت أن المعالج يواجه صعوبة مع المسحات عالية الدقة، فأنت لست وحدك. يواجه العديد من المطورين اختناقات أداء عند معالجة المستندات الكبيرة. يزيل Aspose OCR for Java هذه العقبة من خلال السماح لك بتشغيل OCR على وحدة معالجة الرسومات GPU، مما يقلل زمن المعالجة بشكل كبير. في هذا البرنامج التعليمي ستشاهد مثالًا كاملًا جاهزًا للتنفيذ يوضح كيفية ضبط الترخيص، تمكين تسريع GPU، و**تعيين معرف جهاز GPU** عندما تكون هناك بطاقات رسومية متعددة.

## إجابات سريعة
- **ما هي أسرع طريقة لاستخراج النص من صورة في Java؟** استخدم Aspose OCR مع تسريع GPU وقم بتعيين معرف جهاز GPU المناسب.  
- **ما نسخة Java المطلوبة؟** يُنصح باستخدام Java 17 أو أحدث للحصول على أفضل أداء.  
- **هل أحتاج إلى ترخيص لدعم GPU؟** نعم — ميزات GPU تُفعل فقط بوجود ترخيص Aspose OCR صالح.  
- **هل يمكن تشغيله على خادم بدون واجهة رسومية؟** بالتأكيد؛ فقط يحتاج إلى برنامج تشغيل GPU وأدوات CUDA.  
- **كم عدد اللغات المدعومة؟** أكثر من 30 لغة، بما في ذلك الإنجليزية، الصينية، العربية، والهندية.

## ما هو استخراج النص من صورة؟
يعني استخراج النص من صورة تحويل التمثيل البصري للأحرف المخزنة في صيغ bitmap مثل PNG أو JPG أو TIFF إلى نص Unicode قابل للتحرير والبحث. هذه العملية، المعروفة باسم التعرف الضوئي على الأحرف (OCR)، تمكّن من مهام لاحقة مثل الفهرسة، الترجمة، واستخراج البيانات.

## لماذا نستخدم Aspose OCR GPU؟
يستفيد Aspose OCR من تسريع GPU للتعامل مع الصور الكبيرة وعالية الدقة بكفاءة أكبر مقارنة بالمعالجة باستخدام CPU فقط. يدعم أكثر من 30 صيغة إدخال ويمكنه معالجة صور تصل إلى 5000 × 5000 بكسل مع الحفاظ على استهلاك منخفض للذاكرة، مما يوفر سرعة تعرّف تصل إلى خمس مرات أسرع على وحدات NVIDIA الحديثة.

## ما ستحتاجه
- **Java 17** أو أحدث (متوافق مع Java 8+، لكن إصدارات LTS توفر أداء JIT أفضل).  
- مكتبة **Aspose OCR for Java** (قم بتحميل ملف JAR من موقع Aspose).  
- ملف ترخيص **Aspose OCR** صالح (`Aspose.OCR.lic`). النسخة التجريبية المجانية تعمل، لكن ميزات GPU تتطلب نسخة مرخصة.  
- ملف صورة (`sample-image.png`) يحتوي على نص واضح قابل للقراءة آليًا.  
- وحدة معالجة رسومات NVIDIA متوافقة مع CUDA (أو ما يعادلها) مع تثبيت برنامج التشغيل المناسب.

إذا كان أي من هذه غير مألوف، لا تقلق — سيتم شرح كل نقطة من النقاط أثناء المتابعة.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك
أولاً، أدرج ملف JAR الخاص بـ Aspose OCR في مسار الفئات الخاص بك. إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

لـ Gradle، استخدم:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

إذا كنت تفضل الطريقة اليدوية، ضع ملف JAR في مجلد `libs/` وأضفه إلى مسار الوحدة في IDE.

> **نصيحة احترافية:** حافظ على توافق رقم الإصدار مع ملاحظات الإصدار؛ غالبًا ما تتضمن الإصدارات الأحدث تحسينات أداء لمعالجة GPU.

## الخطوة 2: تحميل ترخيص Aspose OCR (مطلوب لاستخدام GPU)
بدون ترخيص، سيعود استدعاء `setEnableGpu(true)` بهدوء إلى وضع CPU. قم بتحميل الترخيص في بداية `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي حيث خزنت ملف `.lic`. يؤدي المسار غير الصحيح إلى حدوث `FileNotFoundException`، لذا تحقق من التهجئة.

## الخطوة 3: إنشاء محرك OCR وتمكين تسريع GPU
فئة `OcrEngine` هي المكوّن الأساسي الذي ينفّذ عمليات OCR على الصور.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

لماذا نهتم بمعرف الجهاز؟ في بيئة متعددة الـ GPU يمكنك تخصيص بطاقة واحدة للمعالجة المسبقة وأخرى لـ OCR. يضمن تعيين المعرف تشغيل العملية على العتاد المقصود.

## الخطوة 4: إعداد صورة الإدخال
فئة `OcrInput` تمثل مجموعة الصور التي تريد معالجتها.

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

إذا كنت بحاجة لمعالجة تدفق (مثل ملف تم رفعه)، استخدم `ocrInput.add(InputStream)` بدلاً من ذلك.

## الخطوة 5: تشغيل عملية التعرف واسترجاع النتيجة
فئة `OcrResult` تُغلف النص العادي، درجات الثقة، ومعلومات التخطيط الاختيارية التي يُرجعها المحرك.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

ستظهر وحدة التحكم شيئًا مشابهًا لـ:

```
Recognized text:
Hello, world!
This is a sample image.
```

إذا كانت الصورة غير واضحة أو اللغة غير مدعومة، قد تكون النتيجة فارغة. في هذه الحالة، افحص قيمة `ocrResult.getConfidence()` (0‑100) لتقرر ما إذا كنت ستعيد المحاولة مع معالجة مسبقة.

## مثال كامل قابل للتنفيذ
جمع كل الأجزاء معًا يمنحك فئة Java واحدة يمكنك نسخها ولصقها في IDE الخاص بك:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **الناتج المتوقع:** تقوم وحدة التحكم بطباعة النص الدقيق الموجود في `sample-image.png`. عندما يكون GPU نشطًا، ينخفض زمن المعالجة عادةً من عدة ثوانٍ (CPU) إلى أقل من ثانية لمسح بدقة 300 dpi نموذجي.

## أسئلة شائعة وحالات خاصة

### هل يعمل هذا على خادم بدون واجهة رسومية؟
نعم. يجب تثبيت برنامج تشغيل GPU، لكن لا يلزم وجود شاشة. تأكد من توفر أدوات `CUDA` (أو ما يعادلها لبطاقة GPU الخاصة بك) في مسار النظام `PATH`. يتيح هذا الإعداد تشغيل OCR في بيئات سحابية أو حاويات بدون واجهة رسومية.

### ماذا لو كان لدي أكثر من GPU وأريد استخدام GPU 1؟
غيّر معرف الجهاز كما هو موضح:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

تعيين المعرف إلى `1` يوجه محرك OCR لاستخدام الـ GPU الثاني في النظام، وهو مفيد عندما يكون الـ GPU الأول محجوزًا لأعباء عمل أخرى.

### كيف أستخرج النص من صورة بلغة مختلفة؟
حدد اللغة قبل استدعاء `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

يدعم Aspose OCR **أكثر من 30 لغة**، بما في ذلك النصوص من اليمين إلى اليسار مثل العربية والعبرية. اختيار اللغة الصحيحة يحسن الدقة بشكل كبير.

### ماذا لو كانت الصورة تحتوي على صفحات متعددة (مثل PDF تم تحويله إلى صور)؟
أنشئ إدخال `OcrInput` منفصل لكل صفحة، أو كرّر عبر الملفات:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

يقوم المحرك بدمج النتائج بالترتيب، محافظًا على تسلسل الصفحات في النتيجة النهائية.

### كيف أتعامل مع النتائج ذات الثقة المنخفضة؟
تحقق من درجة الثقة:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

تشمل خطوات المعالجة المسبقة الشائعة التحويل إلى ثنائي، تقليل الضوضاء، أو تغيير الحجم إلى 300 dpi. إعادة تشغيل OCR بعد هذه المعالجة غالبًا ما يرفع مستويات الثقة.

## نصائح الأداء
- **معالجة دفعات:** إضافة العديد من الصور إلى `OcrInput` واحد يقلل من عبء تهيئة سياق GPU المتكرر.  
- **التسخين:** نفّذ عملية تعرّف تجريبية مرة واحدة بعد بدء JVM؛ الاستدعاء الأول يتسبب في تأخير تهيئة برنامج التشغيل.  
- **إدارة الذاكرة:** حرّر كائنات `OcrInput` الكبيرة (`ocrInput.clear()`) بعد الانتهاء لتفريغ ذاكرة GPU.  

## الخلاصة
أنت الآن تعرف كيفية **استخراج النص من صورة** بفعالية باستخدام محرك GPU الخاص بـ Aspose OCR في Java، وكيفية **تعيين معرف جهاز GPU** عند العمل مع بطاقات رسومية متعددة، وكيفية التعامل مع السيناريوهات متعددة اللغات. يجب أن يعمل الكود الكامل القابل للتنفيذ أعلاه مباشرةً — فقط استبدل مسارات الترخيص والصورة الخاصة بك.

هل أنت مستعد للخطوة التالية؟ جرّب معالجة مجلد كامل من ملفات PDF الممسوحة، جرب خيارات `setLanguage` المختلفة، أو دمج مخرجات OCR مع نموذج تعلم آلي للمعالجة اللاحقة. تجعل تحسينات الأداء بفضل تسريع GPU المشاريع الكبيرة قابلة للتنفيذ.

برمجة سعيدة، ولا تتردد في ترك تعليق إذا واجهت أي مشاكل!

## الأسئلة المتكررة

**س: هل يمكنني استخدام هذا في تطبيق تجاري؟**  
**ج:** نعم — فقط قم بتثبيت ترخيص Aspose OCR صالح. النسخة التجريبية مجانية للتقييم فقط.

**س: هل يعمل إصدار GPU على خوادم Linux؟**  
**ج:** بالتأكيد؛ طالما تم تثبيت برنامج تشغيل NVIDIA وأدوات CUDA، تعمل المكتبة في بيئات Linux بدون واجهة رسومية.

**س: ما هو الحد الأقصى لحجم الصورة المدعوم؟**  
**ج:** يمكن لـ Aspose OCR معالجة صور تصل إلى **5000 × 5000 px** دون تحميل الملف بالكامل إلى الذاكرة.

**س: كيف أقوم بترقية إلى أحدث نسخة من Aspose OCR؟**  
**ج:** استبدل ملف JAR القديم بالجديد وقم بتحديث رقم نسخة الاعتماد في Maven/Gradle.

**س: هل هناك طريقة للحصول على إحداثيات الصناديق المحيطة لكل كلمة؟**  
**ج:** نعم — `OcrResult` يوفر معلومات التخطيط، بما في ذلك الصناديق المحيطة على مستوى الكلمة، عندما تقوم بتمكين خيار `setIncludeLayout(true)`.

---

**آخر تحديث:** 2026-10-30  
**تم الاختبار مع:** Aspose OCR for Java 24.11  
**المؤلف:** Aspose

## دروس ذات صلة

- [التعرف على النص من صورة Java OCR مع تسريع GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [كيفية تمكين GPU لـ OCR في Java لاستخراج النص من صورة](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [استخراج النص من صورة باستخدام Aspose OCR Java دليل سريع](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-06
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في Java. تعلّم تحويل
  الصورة إلى PDF، وتمكين تصحيح الأخطاء الإملائية، واستخدام GPU للـ OCR للحصول على
  نتائج سريعة.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في Java. يوضح
  هذا الدليل كيفية تحويل الصورة إلى PDF، وتمكين تصحيح الإملاء، واستخدام GPU للتعرف
  الضوئي على الحروف.
og_title: إنشاء ملف PDF قابل للبحث من صورة باستخدام Java OCR
tags:
- OCR
- Java
- PDF
title: إنشاء ملف PDF قابل للبحث من صورة باستخدام Java OCR
url: /ar/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من صورة باستخدام Java OCR

هل احتجت يومًا إلى **إنشاء PDF قابل للبحث** من صورة ممسوحة ضوئيًا لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك — فمعظم المطورين يواجهون هذه المشكلة عندما يتعاملون لأول مرة مع ملفات PDF المستندة إلى الصور. لحسن الحظ، مع Aspose OCR for Java يمكنك **تحويل الصورة إلى PDF**، وتحويل النص إلى محتوى يمكن تحديده، وحتى إضافة تصحيح إملائي للحصول على نتيجة مصقولة.

في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ يوضح كيفية **استخدام OCR GPU** عندما يكون متاحًا، وكيفية **معالجة OCR للصورة** بكفاءة، ولماذا يُعد تمكين تصحيح الإملائي مهمًا للبحث اللاحق. في النهاية ستحصل على طريقة بنقرة واحدة لإنشاء PDF قابل للبحث يمكنك إرساله للمستخدمين أو أرشفته للامتثال.

> **نصيحة احترافية:** إذا كنت تعمل على جهاز بدون GPU، فإن الكود ينتقل بسلاسة إلى CPU، لذا لا تحتاج إلى إعادة كتابة أي شيء.

## ما الذي ستحتاجه

- **Java 8+** (الكود يُترجم باستخدام JDK 8 أو أحدث)
- **Aspose OCR for Java** library (حمّل أحدث ملف JAR من موقع Aspose)
- صورة **إدخال** (JPEG, PNG, TIFF، إلخ) التي تريد تحويلها إلى PDF قابل للبحث
- (اختياري) **GPU** مع دعم CUDA إذا كنت تريد أسرع عملية التعرف الممكنة

لا أطر إضافية، ولا سحر Maven/Gradle — مجرد ملف JAR واحد على مسار الفئات وستكون جاهزًا للانطلاق.

## الخطوة 1: تهيئة محرك OCR – قلب العملية  

أولاً نقوم بإنشاء نسخة من `OcrEngine` ونشير إليها إلى ملف المصدر. هذا الكائن هو العامل الأساسي الذي سيقرأ الصورة، ويشغل الشبكة العصبية، ويعيد لنا النص.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*لماذا هذا مهم:* تهيئة المحرك مرة واحدة وإعادة استخدامه يتجنب عبء تحميل المكتبات الأصلية بشكل متكرر — فوز صغير في الأداء يتراكم عندما تعالج مئات الملفات على دفعات.

## الخطوة 2: اختيار جهاز المعالجة – استخدم OCR GPU عندما يكون ممكنًا  

إذا كان جهازك يحتوي على GPU متوافق، يمكنك إخبار Aspose بتنفيذ العمليات الثقيلة عليه. وإلا فإن المحرك يتحول تلقائيًا إلى CPU.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*ما الفائدة؟* تسريع GPU يمكن أن يقلل الثواني من كل صفحة، خاصةً للماسحات ذات الدقة العالية. التراجع يضمن أن يعمل نفس الكود في أي مكان، وهذا هو السبب في توصيتنا بـ **use OCR GPU** كإعداد افتراضي.

## الخطوة 3: تسريع الفحص – استغلال جميع نوى CPU  

حتى عندما يكون GPU مشغولًا، يمكن تنفيذ خطوات ما قبل المعالجة المحيطة بشكل متوازي. ضبط عدد الخيوط على عدد المعالجات المتاحة يمنح المحرك فرصة لمعالجة عدة أجزاء في آن واحد.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*ملاحظة:* على حاسوب محمول بأربع نوى سيُنشئ أربعة خيوط؛ على محطة عمل بـ 16 نواة ستحصل على الفائدة الكاملة. فقط كن على علم أن زيادة عدد الخيوط يعني استهلاكًا أعلى للذاكرة.

## الخطوة 4: تنظيف الصورة – مرشحات ما قبل المعالجة  

المسح الضبابي أو الملوث سينتج نصًا غير مفهوم. إضافة بعض المرشحات المدمجة تحسن الدقة بشكل كبير.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*لماذا هذه المرشحات؟* `DeskewFilter` يصحح الدوران الذي يحدث غالبًا عندما يُمرَّ الوثيقة عبر الماسح بزاوية. `NoiseRemovalFilter` يزيل البكسلات العشوائية التي قد تُفسَّر كحروف. فكر في ذلك كأنك تعطي محرك OCR ورقة نظيفة للقراءة.

## الخطوة 5: تفعيل الميزات الذكية – تمكين تصحيح الإملائي واكتشاف اللغة تلقائيًا  

إذا كنت تتعامل مع مستندات متعددة اللغات، أو تريد تقليل الأخطاء المطبعية، فعّل مدقق الإملاء المدمج ودع المحرك يتعرف على اللغة.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*متى يكون هذا مفيدًا؟* افترض أن مسحك يحتوي على أقسام بالإنجليزية والإسبانية. ميزة الاكتشاف التلقائي تبدل القواميس في الوقت الحقيقي، بينما تصحيح الإملائي ينظف الأحرف التي قرأها الخطأ مثل “0” بدلًا من “O”. هذه الخطوة أساسية لإنتاج **PDF قابل للبحث** يعرض نتائج صحيحة.

## الخطوة 6: حفظ النتيجة – تحويل الصورة إلى PDF وجعلها قابلة للبحث  

أخيرًا نطلب من المحرك كتابة ملف PDF حيث تكون الصورة الأصلية خلف طبقة نصية غير مرئية. هذه هي عملية **تحويل الصورة إلى PDF** الكلاسيكية، لكن الآن يصبح PDF قابلًا للبحث.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

يمكن فتح ملف الإخراج (`output-searchable.pdf`) في أي عارض PDF؛ سيمكنك تحديد النص، نسخه، والبحث فيه كما في PDF أصلي. لا تحتاج إلى أدوات إضافية.

## مثال كامل يعمل – الصق‑وشغّل  

فيما يلي البرنامج الكامل، جاهزًا للترجمة. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على `input.jpg`.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**الناتج المتوقع:** عند تشغيل البرنامج ستظهر سطر في وحدة التحكم *“Searchable PDF generated successfully.”* فتح `output-searchable.pdf` في Adobe Reader يتيح لك كتابة كلمة من الصورة الأصلية في مربع البحث والانتقال فورًا إلى موقعها.

## أسئلة شائعة وحالات خاصة  

- **ماذا لو لم يتم اكتشاف GPU؟**  
  استدعاء `setDeviceType(OcrDeviceType.GPU)` لا يطرح استثناءً؛ فهو فقط يوجه المحرك لتجربة GPU أولًا. إذا فشل، يعود المحرك إلى CPU بصمت.

- **هل يمكنني معالجة صور متعددة في تشغيل واحد؟**  
  نعم. ضع الكود داخل حلقة، غيّر اسم الملف في كل تكرار، وأعد استخدام نفس نسخة `OcrEngine` لتقليل استهلاك الذاكرة.

- **ملف PDF كبير—كيف يمكن تصغيره؟**  
  بعد OCR يمكنك تشغيل واجهات تحسين PDF من Aspose، أو ببساطة تقليل أبعاد الصورة المصدر قبل تمريرها إلى المحرك (`ImageStream.fromFile(...).setResolution(150)` للحصول على 150 DPI).

- **أحتاج إلى الحفاظ على دقة الصورة الأصلية للامتثال القانوني.**  
  تنسيق `PDF_SEARCHABLE` يحافظ على البت ماب الأصلي تمامًا؛ تُضاف طبقة النص غير المرئية فوقه دون تعديل الجودة البصرية.

## ملخص بصري  

![مثال إنشاء PDF قابل للبحث](placeholder-image.png "مثال إنشاء PDF قابل للبحث")

*مثال إنشاء PDF قابل للبحث – محرك Java OCR يحول JPG ممسوحًا إلى PDF قابل للبحث.*

## الخاتمة  

أصبح لديك الآن **حل كامل من البداية إلى النهاية** لتحويل أي صورة إلى **PDF قابل للبحث** باستخدام Aspose OCR for Java. من خلال **تحويل الصورة إلى PDF**، **تمكين تصحيح الإملائي**، و**استخدام OCR GPU** عندما يكون ممكنًا، ستحصل على نتائج سريعة ودقيقة وقابلة للبحث تعمل عبر المنصات.

ما التالي؟ جرّب التجربة مع:

- **تنسيقات إخراج مختلفة** (`PDF`, `DOCX`, `HTML`) لمعرفة كيفية تصرف طبقة النص.
- **قواميس مخصصة** إذا كنت تعالج مصطلحات خاصة بمجال معين.
- **معالجة دفعات** للتعامل مع آلاف المسحات تلقائيًا.

لا تتردد في تعديل عدد الخيوط، تبديل المرشحات، أو ربط خط أنابيب ما قبل المعالجة الخاص بك. النمط الأساسي يبقى نفسه: تحميل → ما قبل المعالجة → تكوين → OCR → حفظ.

برمجة سعيدة، ولتكن ملفات PDF الخاصة بك دائمًا قابلة للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-06-22
description: إنشاء ملف PDF قابل للبحث في جافا باستخدام Aspose OCR. تعلّم كيفية تحويل
  ملفات PDF الممسوحة ضوئياً، ومعالجة OCR للغات المختلطة، وتعزيز الدقة.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to ocr document
- mixed language ocr
- aspose ocr java
language: ar
og_description: إنشاء ملف PDF قابل للبحث في جافا باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية تحويل مستند إلى نص باستخدام OCR، ومعالجة النصوص ذات اللغات المختلطة، وإنتاج
  ملف PDF قابل للبحث.
og_title: إنشاء ملف PDF قابل للبحث من الصور الممسوحة ضوئياً – دليل Java OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  headline: Create Searchable PDF from Scanned Images – Java OCR Guide
  type: TechArticle
- description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  name: Create Searchable PDF from Scanned Images – Java OCR Guide
  steps:
  - name: Expected Output
    text: 'When you open `processed.pdf` in Adobe Reader (or any PDF viewer), you
      should be able to:'
  - name: 1. What if my document contains more than two languages?
    text: '`config.setLanguage` accepts a var‑args list, so you can pass as many `OcrLanguage`
      constants as you need:'
  - name: 2. Can I run this on a headless server without a GPU?
    text: Absolutely. Set `config.setUseGpu(false)` or simply omit the call. The engine
      will fall back to multi‑core CPU processing, which is still fast thanks to the
      thread pool we configured.
  - name: 3. How do I handle huge PDFs (hundreds of pages)?
    text: Aspose OCR streams pages one‑by‑one, so memory usage stays modest. However,
      you might want to split the PDF into smaller chunks using Aspose PDF’s `split`
      method, process each chunk, then merge the results back together.
  - name: 4. Is there a way to keep the original PDF’s metadata (author, creation
      date)?
    text: 'Yes. After you obtain `searchablePdf`, you can copy metadata from the original
      PDF:'
  type: HowTo
tags:
- OCR
- Java
- PDF
title: إنشاء ملف PDF قابل للبحث من الصور الممسوحة ضوئياً – دليل Java OCR
url: /ar/java/advanced-ocr-techniques/create-searchable-pdf-from-scanned-images-java-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من الصور الممسوحة – دليل OCR للجاڤا

هل تساءلت يومًا كيف تُنشئ **PDF قابل للبحث** من مجموعة من الصفحات الممسوحة ضوئيًا دون إنفاق ثروة على الخدمات الخارجية؟ لست وحدك. يواجه العديد من المطورين نفس المشكلة عندما يحتاجون إلى **تحويل ملفات PDF الممسوحة** إلى شيء يمكن لمستخدميهم البحث فيه فعليًا.  

في هذا الدليل سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يستخدم **Aspose OCR for Java** لتنفيذ مهام **OCR على مستوى المستند**، ومعالجة **OCR متعدد اللغات**، وأخيرًا إنتاج ملف PDF قابل للبحث مصقول. في النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع Maven أو Gradle والبدء في معالجة المستندات اليوم.

## المتطلبات المسبقة – ما ستحتاجه

- Java 17 (أو أي JDK حديث) مثبت ومُعد في PATH الخاص بك.  
- بيئة تطوير متكاملة (IDE) أو محرر تشعر بالراحة معه (IntelliJ IDEA، Eclipse، VS Code…).  
- مكتبة Aspose.OCR for Java – يمكنك الحصول على أحدث JAR من [Aspose Maven repository](https://repo.aspose.com/repo/com/aspose/aspose-ocr/).  
- ملف PDF ممسوح ضوئيًا متعدد الصفحات ترغب في تحويله إلى قابل للبحث.  
- (اختياري) جهاز يدعم GPU إذا كنت تخطط لاستخدام `setUseGpu(true)` لتسريع المعالجة.

وجود هذه العناصر جاهزة يعني أنك تستطيع نسخ‑لصق الشيفرة أدناه وتشغيل **Run** دون الحاجة للبحث عن تبعيات مفقودة.

## الخطوة 1: إعداد المشروع واستيراد Aspose OCR

أولاً، أنشئ وحدة Maven جديدة (أو مشروع Gradle) وأضف تبعية Aspose OCR:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

إذا كنت تفضل Gradle، السطر المكافئ هو:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

بعد مزامنة البناء، ستتمكن من استيراد الفئات التي نحتاجها.

## الخطوة 2: تهيئة محرك OCR

إنشاء المحرك سهل، لكن من المفيد فهم سبب القيام به مبكرًا. كائن `OcrEngine` يحتفظ بالإعدادات، وإدارة الخيوط، وإعدادات GPU التي تؤثر على كل عملية لاحقة.

```java
import com.aspose.ocr.*;

public class AdvancedOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine – this is the heart of the create searchable pdf process
        OcrEngine ocrEngine = new OcrEngine();
```

> **نصيحة احترافية:** إنشاء المحرك مرة واحدة وإعادة استخدامه لعدة ملفات يقلل من الحمل الزائد، خاصةً عند معالجة دفعة من ملفات PDF.

## الخطوة 3: تحميل PDF الممسوح (أو تدفق الصورة)

يعمل Aspose OCR مع تدفقات الصور، لذا نقوم بتمرير PDF الممسوح مباشرة. تقوم المكتبة داخليًا بتحويل كل صفحة إلى نقطية، وهذا هو السبب في أنه يمكنك البدء من PDF والانتهاء بملف PDF قابل للبحث في خطوة واحدة.

```java
        // Load the source PDF – replace the path with your actual file location
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page_scanned.pdf"));
```

إذا كان لديك مجموعة من ملفات TIFF أو JPEG بدلاً من ذلك، فقط وجه `ImageStream.fromFile` إلى تلك الملفات؛ يبقى باقي خط الأنابيب كما هو.

## الخطوة 4: ضبط إعدادات OCR لدعم اللغات المختلطة

هنا يبرز **OCR متعدد اللغات**. بتمرير عدة قيم `OcrLanguage` تخبر المحرك بالبحث عن كل من الإنجليزية والروسية (أو أي تركيبة أخرى) في نفس الصفحة.

```java
        // Grab the mutable config object
        OcrConfig config = ocrEngine.getConfig();

        // Enable English + Russian detection – you can add more languages as needed
        config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN);

        // Speed vs. accuracy trade‑off: use all available cores
        config.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Turn on GPU acceleration if the runtime detects a compatible device
        config.setUseGpu(true);

        // Spell‑check improves accuracy for noisy scans
        config.setEnableSpellCorrection(true);

        // Tell Aspose we want a searchable PDF as the final output
        config.setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

> **لماذا هذا مهم:** بدون تحديد اللغات، يفرض المحرك اللغة الإنجليزية فقط، مما يقلل بشكل كبير من معدلات التعرف على المستندات التي تحتوي على السيريلي أو أي نصوص أخرى.

## الخطوة 5: إضافة فلاتر ما قبل المعالجة لتنظيف المسح

غالبًا ما تعاني ملفات PDF الممسوحة من الميل، البقع، أو انخفاض التباين. إضافة `DeskewFilter` و `DenoiseFilter` يساعد محرك OCR على رؤية الأحرف بوضوح أكبر.

```java
        // Set up image preprocessing
        ImagePreprocessOptions preprocess = new ImagePreprocessOptions();
        preprocess.addFilter(new DeskewFilter());   // Straighten tilted pages
        preprocess.addFilter(new DenoiseFilter()); // Reduce background noise
        ocrEngine.setPreprocessOptions(preprocess);
```

يمكنك ربط فلاتر إضافية—مثل `ContrastFilter` أو `BinarizationFilter`—إذا كان مصدر المادة الخاص بك متسخًا بشكل خاص.

## الخطوة 6: تشغيل OCR وإنشاء PDF قابل للبحث

الآن يبدأ العمل الشاق. استدعاء `recognizeToPdf()` ينفذ خط أنابيب OCR، يطبق خطوات ما قبل المعالجة، ويكتب النص المعترف به في طبقة نصية غير مرئية داخل PDF.

```java
        // Perform OCR and retrieve a searchable PDF document object
        PdfDocument searchablePdf = ocrEngine.recognizeToPdf();
```

الكائن `PdfDocument` المُعاد هو كائن Aspose PDF كامل، مما يعني أنه يمكنك تعديل البيانات الوصفية، إضافة إشارات مرجعية، أو دمجه مع ملفات PDF أخرى قبل الحفظ.

## الخطوة 7: حفظ النتيجة والتحقق

أخيرًا، احفظ الناتج على القرص. رسالة وحدة التحكم تعطيك إشارة بصرية سريعة بأن كل شيء تم بنجاح.

```java
        // Save the searchable PDF to the desired location
        searchablePdf.save("YOUR_DIRECTORY/processed.pdf");
        System.out.println("OCR completed – searchable PDF saved at YOUR_DIRECTORY/processed.pdf");
    }
}
```

### النتيجة المتوقعة

عند فتح `processed.pdf` في Adobe Reader (أو أي عارض PDF)، يجب أن تكون قادرًا على:

1. **تحديد النص** – انقر واسحب فوق أي كلمة ثم انسخها.  
2. **بحث** – اضغط `Ctrl+F` واكتب عبارة تظهر في أحد المسحات الأصلية.  
3. **الحفاظ على التخطيط الأصلي** – المظهر البصري يبقى مطابقًا للمصدر الممسوح؛ تم إضافة طبقة نصية غير مرئية فقط.

إذا رأيت أحرفًا مشوشة أو صفحات مفقودة، تحقق مرة أخرى من إعدادات اللغة وتأكد من أن PDF المصدر غير محمي بكلمة مرور.

## أسئلة شائعة وحالات خاصة

### 1. ماذا لو كان المستند يحتوي على أكثر من لغتين؟

`config.setLanguage` يقبل قائمة var‑args، لذا يمكنك تمرير عدد ما تريد من ثوابت `OcrLanguage` حسب الحاجة:

```java
config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN, OcrLanguage.CHINESE_SIMPLIFIED);
```

فقط تذكر أن كل لغة إضافية تزيد من زمن المعالجة قليلاً.

### 2. هل يمكن تشغيل هذا على خادم بدون واجهة (headless) دون GPU؟

بالطبع. اضبط `config.setUseGpu(false)` أو ببساطة احذف الاستدعاء. سيعود المحرك إلى المعالجة باستخدام CPU متعدد النوى، وهو لا يزال سريعًا بفضل مجموعة الخيوط التي قمنا بتكوينها.

### 3. كيف أتعامل مع ملفات PDF الضخمة (مئات الصفحات)؟

يقوم Aspose OCR ببث الصفحات واحدةً تلو الأخرى، لذا يبقى استهلاك الذاكرة معتدلًا. ومع ذلك، قد ترغب في تقسيم PDF إلى أجزاء أصغر باستخدام طريقة `split` في Aspose PDF، معالجة كل جزء، ثم دمج النتائج مرة أخرى.

### 4. هل هناك طريقة للحفاظ على بيانات التعريف الأصلية لملف PDF (المؤلف، تاريخ الإنشاء)؟

نعم. بعد الحصول على `searchablePdf`، يمكنك نسخ بيانات التعريف من PDF الأصلي:

```java
PdfDocument original = new PdfDocument("YOUR_DIRECTORY/multi_page_scanned.pdf");
searchablePdf.getInfo().setAuthor(original.getInfo().getAuthor());
// repeat for other metadata fields
```

## نصائح احترافية لـ OCR جاهز للإنتاج

- **معالجة الدفعات:** ضع كامل التدفق داخل حلقة تت iterates over a directory of files. أعد استخدام نسخة واحدة من `OcrEngine` لتجنب عبء التهيئة المتكرر.  
- **معالجة الأخطاء:** امسك `OcrException` لتسجيل الملفات التي فشلت، ثم استمر بالوثيقة التالية.  
- **مراقبة الأداء:** استخدم `System.nanoTime()` قبل وبعد `recognizeToPdf()` لتسجيل زمن المعالجة لكل ملف؛ هذا يساعدك على اتخاذ قرار ما إذا كنت ستوسع إلى مجموعة عمال سحابية.  
- **الأمان:** إذا كنت تتعامل مع مستندات حساسة، فكر في تشفير ملف PDF الناتج باستخدام `searchablePdf.encrypt(...)` قبل الحفظ.

## الخلاصة

لقد غطينا الآن كل ما تحتاجه **لإنشاء ملفات PDF قابلة للبحث** من مصادر ممسوحة باستخدام **Aspose OCR for Java**. أظهر لك الدليل كيفية **تحويل PDF الممسوح**، تكوين **OCR متعدد اللغات**، وضبط فلاتر ما قبل المعالجة—كل ذلك مع الحفاظ على شفرة مختصرة وجاهزة للإنتاج.  

من هنا قد تستكشف إضافة صور مصغرة مولدة بواسطة OCR، دمجها مع نظام إدارة مستندات، أو حتى تغذية النص المستخرج إلى فهرس بحث مثل Elasticsearch. الاحتمالات واسعة بقدر حجم المستندات التي تحتاج إلى رقمنتها.  

هل لديك المزيد من الأسئلة حول **كيفية OCR المستند** في Java، أو ترغب في رؤية شرح أعمق لتعامل مع PDF؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
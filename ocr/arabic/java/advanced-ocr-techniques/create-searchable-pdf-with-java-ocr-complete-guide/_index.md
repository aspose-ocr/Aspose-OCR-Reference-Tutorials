---
category: general
date: 2026-05-25
description: إنشاء ملف PDF قابل للبحث في Java باستخدام Aspose OCR. تعلم كيفية تحويل
  PDF إلى PDF قابل للبحث، تحميل PDF للتعرف الضوئي على الأحرف، وتسريع العملية باستخدام
  وحدة معالجة الرسومات.
draft: false
keywords:
- create searchable pdf
- convert pdf to searchable pdf
- load pdf for ocr
- ocr pdf with gpu
language: ar
og_description: إنشاء PDF قابل للبحث في Java باستخدام Aspose OCR. يوضح هذا الدرس كيفية
  تحويل PDF إلى PDF قابل للبحث، وتحميل PDF للتعرف الضوئي على الأحرف، واستخدام تسريع
  GPU.
og_title: إنشاء ملف PDF قابل للبحث باستخدام Java OCR – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  headline: Create Searchable PDF with Java OCR – Complete Guide
  type: TechArticle
- description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  name: Create Searchable PDF with Java OCR – Complete Guide
  steps:
  - name: Runs OCR on each page image.
    text: Runs OCR on each page image.
  - name: Generates an invisible text layer that matches the visual content.
    text: Generates an invisible text layer that matches the visual content.
  - name: Embeds that layer into a new PDF, preserving the original appearance.
    text: Embeds that layer into a new PDF, preserving the original appearance.
  type: HowTo
tags:
- OCR
- Java
- PDF
- Aspose
title: إنشاء PDF قابل للبحث باستخدام Java OCR – دليل كامل
url: /ar/java/advanced-ocr-techniques/create-searchable-pdf-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث باستخدام Java OCR – دليل كامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من المستندات الممسوحة ضوئياً لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. يواجه العديد من المطورين نفس المشكلة عند محاولة تحويل ملفات PDF التي تحتوي على صور فقط إلى أصول قابلة للبحث بالنص، خاصة عندما تكون الأداء مهمة.

في هذا الدرس سنستعرض حلاً عمليًا **ينشئ PDF قابل للبحث** باستخدام Aspose OCR للـ Java. سنظهر لك أيضًا كيفية **تحويل PDF إلى PDF قابل للبحث**، **تحميل PDF للـ OCR**، وحتى **OCR PDF مع تسريع GPU** — كل ذلك في سكريبت واحد سهل القراءة. في النهاية ستحصل على برنامج قابل للتنفيذ وفهم واضح لأهمية كل خطوة.

> **ما ستحصل عليه**  
> * مشروع Java كامل يقرأ PDF متعدد اللغات  
> * OCR مدعوم بـ GPU يسرّع المعالجة على الأجهزة الحديثة  
> * ملف PDF قابل للبحث يمكنك إدراجه في أي نظام إدارة مستندات  

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* Java 17 (أو أحدث) مثبت – الإصدارات الأقدم قد تفتقد إلى الـ APIs المطلوبة.  
* Maven أو Gradle لإدارة الاعتمادات – سنستخدم Maven في الأمثلة.  
* رخصة Aspose OCR للـ Java (الإصدار التجريبي المجاني يكفي للاختبار).  
* ملف PDF يحتوي على صفحات ممسوحة ضوئيًا (المثال يستخدم `mixed_lang.pdf`).  

إذا كان أي من هذه غير مألوف لك، لا تقلق – الخطوات أدناه تتضمن الأوامر الدقيقة لتجهيز البيئة.

![إنشاء PDF قابل للبحث باستخدام Aspose OCR Java](https://example.com/images/create-searchable-pdf.png "إنشاء PDF قابل للبحث باستخدام Aspose OCR Java")

## الخطوة 1: إعداد المشروع و **إنشاء PDF قابل للبحث** – تهيئة المشروع

أولاً، أنشئ مشروع Maven. افتح الطرفية ونفّذ:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=SearchablePdfDemo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

انتقل إلى المجلد:

```bash
cd SearchablePdfDemo
```

أضف اعتماد Aspose OCR إلى `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- check Maven Central for the latest -->
    </dependency>
</dependencies>
```

> **لماذا هذا مهم:** عملية **إنشاء PDF قابل للبحث** تعتمد على فئة `OcrEngine` الموجودة داخل مكتبة Aspose OCR. بدون الإصدار الصحيح ستحصل على أخطاء تجميع أو فقدان للميزات.

الآن أنشئ الفئة الرئيسية Java `QuickDemo.java` داخل `src/main/java/com/example/ocr/`.

## الخطوة 2: تمكين تسريع GPU – **OCR PDF مع GPU**

يمكن لتسريع GPU أن يقلل الدقائق من مهمة OCR متعددة الصفحات. يتيح لك Aspose OCR تفعيله بسطر واحد:

```java
// Enable GPU processing
engine.getEngineOptions().setUseGpu(true);
```

إذا كان جهازك يحتوي على GPU متوافق من NVIDIA أو AMD وتم تثبيت التعريفات المناسبة، سيقوم محرك OCR بتحميل الجزء الثقيل إلى بطاقة الرسوميات. وإلا، سيعود التنفيذ إلى المعالج CPU بأمان — لا يحدث تعطل، فقط يكون التنفيذ أبطأ.

> **نصيحة احترافية:** على نظام Linux، قد تحتاج إلى ضبط `LD_LIBRARY_PATH` للإشارة إلى مكتبات CUDA قبل تشغيل JVM.

## الخطوة 3: **تحميل PDF للـ OCR** وتكوين دعم اللغة

الآن نقوم فعليًا **بتحميل PDF للـ OCR**. يتعامل Aspose OCR مع صفحات PDF كصور داخليًا، لذا ما عليك سوى توجيه المحرك إلى الملف:

```java
// Load the source PDF document (image‑only PDF)
engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");
```

بعد ذلك، أخبر المحرك أي لغة تتوقعها. في مثالنا نركز على اللغة التايلاندية، لكن يمكنك تمرير مصفوفة من اللغات إذا كان المستند يخلط بين النصوص:

```java
engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
```

إذا كان لديك قاموس مخصص (مثلاً مصطلحات متخصصة)، قم بدمجه:

```java
engine.getEngineOptions().getSpellCorrectorOptions()
      .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");
```

> **لماذا نحدد اللغة؟** تعتمد دقة OCR على نموذج اللغة. توفير `OcrLanguage` الصحيح يقلل الأخطاء بشكل كبير، خاصة للخطوط غير اللاتينية.

## الخطوة 4: **تحويل PDF إلى PDF قابل للبحث** في نداء واحد

يتألق Aspose OCR لأنه يمكنه **تحويل PDF إلى PDF قابل للبحث** باستخدام نداء طريقة واحدة — دون الحاجة لتجميع طبقات الصور والنص يدويًا.

```java
// Export a searchable PDF in a single operation
engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");
```

خلف الكواليس، يقوم المحرك بـ:

1. تشغيل OCR على كل صورة صفحة.  
2. إنشاء طبقة نص غير مرئية تتطابق مع المحتوى البصري.  
3. دمج تلك الطبقة في PDF جديد، مع الحفاظ على المظهر الأصلي.

النتيجة ملف يبدو مطلقًا كالملف الأصلي لكنه يمكن فهرسته بواسطة أي عارض PDF.

## الخطوة 5: استرجاع النص المعترف به والتحقق من النتيجة

على الرغم من أننا حفظنا بالفعل PDF قابل للبحث، قد ترغب أيضًا في الحصول على النص الخام للتسجيل أو المعالجة الإضافية:

```java
// Output the recognized text to the console
System.out.println(engine.recognize().getText());
```

عند تشغيل البرنامج، يجب أن ترى النص التايلاندي المستخرج يُطبع في وحدة التحكم، يليه ملف `mixed_lang_searchable.pdf` جديد في الدليل الخاص بك.

### ناتج وحدة التحكم المتوقع (مقتطع)

```
สวัสดีครับ นี่คือเอกสารตัวอย่าง...
...
```

افتح الـ PDF المُولد في Adobe Reader أو أي عارض، اضغط **Ctrl + F**، وستتمكن من البحث عن الكلمات التي رأيتها للتو في وحدة التحكم. هذا هو الدليل على أننا نجحنا في **إنشاء PDF قابل للبحث**.

## الخطوة 6: المشكلات الشائعة و **نصائح احترافية** لأداء OCR عالي السرعة

| المشكلة | العرض | الحل |
|-------|----------|-----|
| **GPU غير مكتشف** | لا يوجد تسريع، المحرك يعود إلى CPU | تأكد من تثبيت تعريفات CUDA وأن `java.library.path` يحتوي على مكتبات GPU. |
| **خطوط مفقودة** | طبقة النص تظهر أحرفًا مشوهة | ثبّت الخطوط اللغوية المناسبة على نظام التشغيل أو دمجها عبر `engine.getEngineOptions().setEmbedFonts(true)`. |
| **PDF كبير (> 500 صفحة)** | أخطاء نفاد الذاكرة | زد حجم heap للـ JVM (`-Xmx4g`) واضبط `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors())` لتوزيع العمل على الأنوية. |
| **القاموس المخصص غير مُطبق** | يبدو أن مصحح الإملاء مُهمل | تحقق من أن المسار مطلق والملف يستخدم ترميز UTF‑8. |

> **تذكر:** السطر `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());` أساسي عندما تريد **OCR PDF مع GPU** والاستفادة الكاملة من الأنوية المتعددة. فهو يطلب من المحرك إنشاء عامل لكل نواة، مما يبقي GPU مشغولًا بينما يتولى CPU المعالجة المسبقة واللاحقة.

## مثال كامل يعمل

فيما يلي البرنامج الكامل القابل للتنفيذ بلغة Java والذي يدمج كل خطوة ناقشناها. استبدل مسارات العناصر النائبة بمساراتك الخاصة.

```java
import com.aspose.ocr.*;

public class QuickDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Enable GPU acceleration and use all available CPU cores
        engine.getEngineOptions().setUseGpu(true);
        engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 3: Configure language support and a custom spell‑corrector dictionary
        engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
        engine.getEngineOptions().getSpellCorrectorOptions()
              .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");

        // Step 4: Load the source PDF document (this is where we **load pdf for ocr**)
        engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");

        // Step 5: Export a searchable PDF in a single operation (**convert pdf to searchable pdf**)
        engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");

        // Step 6: Output the recognized text to the console
        System.out.println(engine.recognize().getText());
    }
}
```

الترجمة والتنفيذ:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.QuickDemo"
```

إذا تم ربط كل شيء بشكل صحيح، سترى النص المستخرج يُطبع وملف PDF قابل للبحث جديد بجوار الملف الأصلي.

## الخلاصة

لقد استعرضنا كيفية **إنشاء PDF قابل للبحث** في Java باستخدام Aspose OCR، بدءًا من إعداد المشروع وحتى المعالجة المسرّعة بـ GPU. عبر **تحميل PDF للـ OCR**، تكوين دعم اللغة، واستدعاء طريقة **تحويل PDF إلى PDF قابل للبحث** ذات السطر الواحد، ستحصل على مستند مفهرس بالكامل جاهز لمحركات البحث أو أنظمة الاسترجاع الداخلية.

ما الخطوة التالية؟ جرّب استبدال `OcrLanguage.THAI` بـ `OcrLanguage.ENGLISH` أو دمج عدة لغات لملفات PDF متعددة اللغات. جرب ضبط `engine.getEngineOptions().setResolution(300)` لتلاحظ كيف يؤثر DPI على الدقة، أو دمج خطوط مخصصة لتحسين العرض على العارضات القديمة.

هل لديك أسئلة حول تحسين الأداء، الترخيص، أو دمج هذا التدفق في خدمة Spring Boot؟ اترك تعليقًا أدناه أو راجع وثائق Aspose OCR للـ Java لمزيد من التفاصيل. ترميز سعيد، واستمتع بتحويل تلك المسحات الثابتة إلى كنوز قابلة للبحث!

## دروس ذات صلة

- [التعرف على نص PDF – عمليات OCR مع Aspose.OCR للـ Java](/ocr/english/java/ocr-operations/)
- [OCR للتعرف على مستندات PDF في Aspose.OCR للـ Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [كيفية OCR PDF في .NET باستخدام Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
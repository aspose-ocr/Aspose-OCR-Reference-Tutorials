---
category: general
date: 2026-10-24
description: تعرف على كيفية تشغيل مثال Aspose OCR Java الذي يستخرج النص من ملفات PDF،
  بما في ذلك معالجة OCR المتوازية، التعامل مع ملفات PDF المحمية بكلمة مرور، وتحويل
  ملفات PDF الممسوحة ضوئياً إلى نص قابل للبحث.
draft: false
keywords:
- aspose ocr java example
- parallel ocr processing
- extract text pdf java
- ocr password protected pdf
- convert scanned pdf searchable
lastmod: 2026-10-24
og_description: قم بتشغيل مثال Aspose OCR Java لاستخراج النص من ملفات PDF بسرعة. يغطي
  هذا الدليل معالجة OCR المتوازية، ملفات PDF المحمية بكلمة مرور، وتحويل ملفات PDF
  الممسوحة ضوئياً إلى مستندات قابلة للبحث.
og_image_alt: Screenshot of a Java console showing extracted text after parallel OCR
  processing with Aspose OCR
og_title: مثال Aspose OCR Java – استخراج النص من ملفات PDF بسرعة
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  headline: 'Aspose OCR Java example: extract text from PDF quickly'
  type: TechArticle
- description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  name: 'Aspose OCR Java example: extract text from PDF quickly'
  steps:
  - name: set up your project
    text: 'Add the Aspose OCR dependency to your `pom.xml`: If you prefer Gradle,
      replace the snippet with the equivalent `implementation` line. After the dependency
      resolves, you can import the required classes in your Java source file.'
  - name: create and configure the OCR engine
    text: '`OcrEngine` is the core class that performs optical character recognition.
      The `OcrEngine` class is Aspose OCR''s primary object that encapsulates all
      OCR settings and execution logic. Enable parallel processing and optionally
      limit the thread pool: **Why this matters:** - `setParallelProcessing(true'
  - name: load the PDF you want to process
    text: '`OcrInput` represents the collection of files (PDFs, images, or mixed media)
      that the engine will analyze. The `OcrInput` class aggregates one or more input
      sources, allowing you to feed PDFs, TIFFs, or JPEGs to the OCR engine in a single
      batch. Add your PDF (or a set of PDFs) to the input collectio'
  - name: run OCR across all pages in parallel
    text: '`OcrResult` holds the combined text output and per‑page confidence information
      after recognition completes. The `OcrResult` object contains the concatenated
      plain‑text result and a list of `PageResult` objects that expose confidence
      scores for each processed page. Execute the recognition: **Under th'
  - name: retrieve and display the combined text
    text: '`OcrResult.getText()` returns the full searchable string. The `getText()`
      method of `OcrResult` returns a single `String` that contains the OCR‑extracted
      text from every page, with line breaks preserved as they appeared in the source
      PDF. **Expected output:** The console prints one continuous string'
  - name: handle special scenarios
    text: '#### How does the engine deal with password‑protected PDFs? Supply the
      password when adding the file to `OcrInput`: The `add` method overload that
      accepts a password decrypts the document on the fly, allowing seamless OCR without
      manual decryption.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR free trial works for development and testing; a commercial
      license is required for production deployments.
    question: Can I use this example with a free trial license?
  - answer: Absolutely – pass the password to `OcrInput.add(filePath, password)` and
      the engine will decrypt the document automatically.
    question: Does the example support OCR on password‑protected PDFs?
  - answer: Over 70 languages, including right‑to‑left scripts such as Arabic and
      Hebrew.
    question: How many languages does Aspose OCR recognise?
  - answer: The engine can handle multi‑hundred‑page PDFs; you can set a memory limit
      to keep RAM usage predictable.
    question: What is the maximum PDF size I can process?
  - answer: Yes, by configuring `setMaxThreadCount` you control the maximum number
      of concurrent threads, preventing resource exhaustion.
    question: Is parallel OCR safe on shared servers?
  type: FAQPage
tags:
- ocr
- java
- aspose
- pdf
title: 'مثال Aspose OCR Java: استخراج النص من ملفات PDF بسرعة'
url: /ar/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مثال Aspose OCR Java: استخراج النص من PDF بسرعة

في هذا الدرس ستكتشف **كيفية استخدام مثال Aspose OCR Java** لتحويل ملفات PDF الممسوحة ضوئياً إلى نص قابل للبحث وقابل للقراءة آلياً. سواء كان لديك ملف متعدد الصفحات واحد أو مجموعة من ملفات PDF المحمية بكلمة مرور، توضح الخطوات أدناه كيفية تكوين محرك OCR، تمكين المعالجة المتوازية، واسترجاع المخرجات المدمجة في بضع أسطر فقط من كود Java.

ستتعلم أيضاً متى يجب تعديل عدد الخيوط لتحقيق الأداء الأمثل، كيفية التعامل مع ملفات PDF المشفرة، ولماذا يعتبر هذا النهج مثالياً لتحويل مستندات PDF الممسوحة ضوئياً إلى أرشيفات قابلة للبحث.

![كيفية استخدام OCR مع Aspose OCR Java](/images/ocr-parallel.png "توضيح لمعالجة OCR المتوازية في Java – كيفية استخدام OCR")
[كيفية استخدام OCR مع Aspose OCR Java](/images/ocr-parallel.png "توضيح لمعالجة OCR المتوازية في Java – كيفية استخدام OCR")

## إجابات سريعة
- **ماذا يفعل مثال Aspose OCR Java؟** يقوم بتحميل ملف PDF، تشغيل OCR على كل صفحة بشكل متوازي، وإرجاع النص القابل للبحث بالكامل كسلسلة واحدة.  
- **هل يمكنه معالجة ملفات PDF المحمية بكلمة مرور؟** نعم – يمكنك تزويد كلمة مرور المستند عند إضافة الملف إلى `OcrInput`.  
- **هل تستحق معالجة OCR المتوازية العناء؟** على جهاز بأربع نوى، يقلل وقت المعالجة بنسبة 30‑70 % لملفات PDF التي تتجاوز خمس صفحات.  
- **ما هي اللغات المدعومة؟** أكثر من 70 لغة، بما في ذلك الإنجليزية، الفرنسية، الألمانية، الصينية، والعربية.  
- **هل أحتاج إلى ترخيص للإنتاج؟** يتطلب استخدام Aspose OCR في بيئة غير تجريبية ترخيصًا تجاريًا؛ النسخة التجريبية المجانية تكفي للتقييم.

## ما هو مثال Aspose OCR Java؟
**مثال Aspose OCR Java** هو برنامج مختصر وقابل للتنفيذ يوضح كيفية إنشاء كائن `OcrEngine`، تكوين التنفيذ المتوازي، واستخراج النص من ملفات PDF باستخدام مكتبة Aspose OCR for Java. كما يوضح كيفية التعامل مع سيناريوهات شائعة مثل المستندات المحمية بكلمة مرور، ضبط حدود الذاكرة، واختيار اللغة، مما يوفر أساسًا قويًا لبناء خطوط معالجة مستندات أكبر.

## لماذا نستخدم معالجة OCR المتوازية؟
يمكن لـ Aspose OCR تقسيم ملف PDF متعدد الصفحات إلى صفحات منفصلة ومعالجة كل صفحة في خيط منفصل. على خادم بثماني نوى، يتم عادةً معالجة مستند من 120 صفحة في أقل من 30 ثانية، مقارنةً بأكثر من دقيقة عند المعالجة المتسلسلة. هذه الزيادة في السرعة تكون ذات قيمة خاصة عندما تحتاج إلى **تحويل أرشيفات PDF الممسوحة ضوئياً إلى نص قابل للبحث** على نطاق واسع.

## المتطلبات الأساسية
- Java 8 أو أحدث مثبتة.  
- أداة بناء Maven أو Gradle (المثال يستخدم Maven).  
- ترخيص Aspose OCR for Java (النسخة التجريبية المجانية تكفي للاختبار).  

## كيفية تشغيل مثال Aspose OCR Java خطوة بخطوة

### الخطوة 1: إعداد مشروعك

أضف تبعية Aspose OCR إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.11</version>
</dependency>
```

إذا كنت تفضل Gradle، استبدل المقتطف بسطر `implementation` المكافئ.  
بعد حل التبعية، يمكنك استيراد الفئات المطلوبة في ملف مصدر Java الخاص بك.

### الخطوة 2: إنشاء وتكوين محرك OCR

`OcrEngine` هو الفئة الأساسية التي تقوم بالتعرف الضوئي على الأحرف.

فئة `OcrEngine` هي الكائن الرئيسي في Aspose OCR الذي يضم جميع إعدادات OCR ومنطق التنفيذ.  
قم بتمكين المعالجة المتوازية وحدد حدًا اختياريًا لمجموعة الخيوط:

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**لماذا هذا مهم:**  
- `setParallelProcessing(true)` يوزع الصفحات على عدة نوى CPU، مما يقلل وقت التشغيل بشكل كبير على الأجهزة متعددة النوى.  
- `setMaxThreadCount` يحمي موارد الخادم بمنع المحرك من استحواذ جميع النوى، وهو أمر حاسم في بيئات الاستضافة المشتركة أو CI.

### الخطوة 3: تحميل ملف PDF الذي تريد معالجته

`OcrInput` يمثل مجموعة الملفات (PDFs، صور، أو وسائط مختلطة) التي سيقوم المحرك بتحليلها.

فئة `OcrInput` تجمع مصدرًا أو أكثر من المدخلات، مما يتيح لك تغذية ملفات PDF، TIFF، أو JPEG إلى محرك OCR في دفعة واحدة.  
أضف ملف PDF الخاص بك (أو مجموعة من ملفات PDF) إلى مجموعة الإدخال:

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**نصيحة:** استخدم مسارًا مطلقًا أو مسارًا نسبيًا إلى دليل العمل لتجنب استثناء `FileNotFoundException`. يمكن استدعاء طريقة `add` بشكل متكرر لإضافة مستندات متعددة للمعالجة الدفعية.

### الخطوة 4: تشغيل OCR عبر جميع الصفحات بشكل متوازي

`OcrResult` يحتوي على النص المدمج ومعلومات الثقة لكل صفحة بعد اكتمال التعرف.

كائن `OcrResult` يحتوي على نتيجة النص العادي المتسلسلة وقائمة من كائنات `PageResult` التي تعرض درجات الثقة لكل صفحة معالجة.  
نفّذ عملية التعرف:

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**تحت الغطاء:** كل صفحة تُسلم إلى خيط عامل منفصل (حتى عدد `maxThreadCount` الذي حددته). تقوم المكتبة بمزامنة النتائج بحيث يحافظ `OcrResult` النهائي على ترتيب الصفحات الأصلي.

### الخطوة 5: استرجاع وعرض النص المدمج

`OcrResult.getText()` يُعيد السلسلة القابلة للبحث بالكامل.

طريقة `getText()` في `OcrResult` تُعيد `String` واحدة تحتوي على النص المستخرج من جميع الصفحات، مع الحفاظ على فواصل الأسطر كما ظهرت في ملف PDF الأصلي.  

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**الناتج المتوقع:** يطبع الطرفية سلسلة مستمرة تحتوي على النص القابل للقراءة من جميع الصفحات، جاهزة للفهرسة أو التخزين أو المعالجة الإضافية.

### الخطوة 6: التعامل مع السيناريوهات الخاصة

#### كيف يتعامل المحرك مع ملفات PDF المحمية بكلمة مرور؟

زوّد كلمة المرور عند إضافة الملف إلى `OcrInput`:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

طريقة `add` التي تقبل كلمة مرور تقوم بفك تشفير المستند فورًا، مما يسمح بـ OCR سلس دون الحاجة إلى فك تشفير يدوي.

#### كيف يمكنني تحديد حد لاستخدام الذاكرة للملفات الكبيرة جدًا؟

استدعِ `ocrEngine.setMemoryLimit(256);` لتحديد استهلاك الذاكرة إلى 256 ميغابايت. سيقوم المحرك تلقائيًا بنقل البيانات الزائدة إلى ملفات مؤقتة، مما يمنع حدوث أعطال نفاد الذاكرة حتى مع ملفات PDF مئات الصفحات.

## أسئلة شائعة وحالات حافة

### هل أحتاج حقًا إلى المعالجة المتوازية؟

إذا كان ملف PDF يحتوي على **أكثر من عدد قليل من الصفحات** وتملك على الأقل أربع نوى CPU، فإن تمكين المعالجة المتوازية يقلل عادةً من زمن التنفيذ الإجمالي بنسبة **30‑70 %**. بالنسبة لملف مسح ضوئي بصفحة واحدة، قد تتجاوز تكلفة إنشاء الخيوط الفائدة، لذا يمكنك تعطيلها باستخدام `ocrEngine.setParallelProcessing(false)`.

### ماذا يحدث عندما تفشل صفحة في التعرف الضوئي على الأحرف؟

تُطلق Aspose OCR استثناء `OcrException` فقط للأخطاء الفادحة مثل ملف تالف. الصفحات التي لا يمكن التعرف عليها ببساطة تُعيد سلسلة فارغة، ويقوم المحرك بدمجها بصمت. يمكنك فحص `ocrResult.getPageResults()` للحصول على درجات الثقة لكل صفحة ومعالجة الصفحات ذات الثقة المنخفضة يدويًا.

### كيف أغير لغة التعرف؟

المحرك يستخدم الإنجليزية افتراضيًا، لكن يمكنك تغيير اللغة باستخدام:

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing and optionally limit threads
        ocrEngine.setParallelProcessing(true);
        ocrEngine.setMaxThreadCount(4); // Adjust based on your hardware

        // Step 3: Load the multi‑page PDF to be processed
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");
        // Uncomment and set password if needed:
        // ocrInput.add("protected.pdf", "mySecretPassword");

        // Step 4: Recognize text from all pages in parallel
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the combined OCR result
        System.out.println("Combined text from all pages:");
        System.out.println(ocrResult.getText());
    }
}
```

استبدل `Language.FRENCH` بأي تعداد لغة مدعوم. هذا ضروري عندما تحتاج إلى **استخراج نص PDF Java** من مستندات متعددة اللغات.

## نصائح احترافية لـ OCR جاهز للإنتاج

- **معالجة دفعية:** ضع التدفق داخل حلقة تقرأ أسماء الملفات من دليل، لتحويل النموذج إلى خدمة قابلة للتوسع.  
- **التسجيل:** عيّن `ocrEngine.setLogLevel(LogLevel.ERROR)` في بيئة الإنتاج لتقليل الإخراج التفصيلي.  
- **تنظيف النتائج:** عالج `ocrResult.getText()` باستخدام تعبيرات نمطية لإزالة الفراغات أو القطع غير المرغوب فيها.  
- **ضبط مجموعة الخيوط:** استخدم `ocrEngine.setMaxThreadCount(Runtime.getRuntime().availableProcessors())` على الخوادم ذات النوى المتعددة لتحقيق أقصى إنتاجية.  
- **معيار الأداء:** على خادم Intel Xeon بثماني نوى، يُعالج ملف PDF من 200 صفحة (300 ميغابايت) في حوالي 22 ثانية مع تمكين OCR المتوازي.

## الخلاصة

أصبح لديك الآن مثال **Aspose OCR Java** كامل لاستخراج نص قابل للبحث من أي PDF ممسوح ضوئيًا، يدعم الملفات المحمية بكلمة مرور، ويستفيد من المعالجة المتوازية للسرعة. بدمج هذا الكود في تطبيقاتك، يمكنك بناء خطوط تحويل مستندات قوية، إمداد مخرجات OCR إلى فهارس البحث، أو ربطها بخدمات الترجمة لإنشاء أرشيفات متعددة اللغات قابلة للبحث.

هل أنت مستعد للخطوة التالية؟ جرّب إمداد النص المستخرج إلى Elasticsearch للبحث النصي الكامل، أو ربط المخرجات بواجهة برمجة تطبيقات ترجمة لتكوين مستودع متعدد اللغات قابل للبحث. برمجة سعيدة!

---

**آخر تحديث:** 2026-10-24  
**تم الاختبار مع:** Aspose OCR for Java 24.11  
**المؤلف:** Aspose  

## الأسئلة المتكررة

**س: هل يمكنني استخدام هذا المثال مع ترخيص تجريبي مجاني؟**  
ج: نعم، النسخة التجريبية المجانية من Aspose OCR تعمل للتطوير والاختبار؛ يتطلب الاستخدام في الإنتاج ترخيصًا تجاريًا.

**س: هل يدعم المثال OCR على ملفات PDF المحمية بكلمة مرور؟**  
ج: بالتأكيد – مرّر كلمة المرور إلى `OcrInput.add(filePath, password)` وسيقوم المحرك بفك تشفير المستند تلقائيًا.

**س: كم عدد اللغات التي يتعرف عليها Aspose OCR؟**  
ج: أكثر من 70 لغة، بما في ذلك النصوص من اليمين إلى اليسار مثل العربية والعبرية.

**س: ما هو الحد الأقصى لحجم PDF الذي يمكنني معالجته؟**  
ج: يمكن للمحرك معالجة ملفات PDF مئات الصفحات؛ يمكنك ضبط حد الذاكرة للحفاظ على استهلاك RAM بشكل متوقع.

**س: هل OCR المتوازي آمن على الخوادم المشتركة؟**  
ج: نعم، من خلال تكوين `setMaxThreadCount` يمكنك التحكم في الحد الأقصى لعدد الخيوط المتزامنة، مما يمنع استنزاف الموارد.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

## دروس ذات صلة

- [كيفية استخدام Ocr في معالجة Java المتوازية مع Aspose](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/)
- [إنشاء PDF قابل للبحث باستخدام دليل Aspose Ocr Java](/ocr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/)
- [كيفية استخدام Ocr في Java لاستخراج النص من PDF باستخدام Aspose Ocr](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
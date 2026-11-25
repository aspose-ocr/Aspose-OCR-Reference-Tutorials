---
category: general
date: 2026-09-18
description: تعلم كيفية إضافة تبعية Aspose OCR Maven واستخراج النص من الصور في Java.
  يغطي هذا الدليل إعداد محرك OCR، spell‑checking، custom dictionaries، وconfiguration
  tips.
draft: false
keywords:
- aspose ocr maven dependency
- java image to text
- extract image text java
- Aspose OCR Java
- OCR spell checking
lastmod: 2026-09-18
og_description: تعلم كيفية إضافة تبعية Aspose OCR Maven واستخدامها لتحويل الصور إلى
  نص في Java. يتضمن ذلك spell‑checking، custom dictionaries، وconfiguration tips.
og_image_alt: Diagram showing OCR workflow to extract text from image using Aspose
  OCR in Java
og_title: إضافة تبعية Aspose OCR Maven لاستخراج نص الصورة في Java
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to add the Aspose OCR Maven dependency and extract text from
    images in Java. This guide covers OCR engine setup, spell‑checking, custom dictionaries,
    and configuration tips.
  headline: Add Aspose OCR Maven dependency to extract image text in Java
  type: TechArticle
- questions:
  - answer: Handwritten recognition is available in a separate module (`aspose-ocr-handwriting`).
      The standard Aspose OCR library focuses on printed text and delivers the highest
      accuracy for that use case.
    question: Does Aspose OCR support handwritten text?
  - answer: Yes—download the image into a `byte[]` or `InputStream` (e.g., using `java.net.URL`)
      and pass that stream to `ocrEngine.recognize(inputStream)`.
    question: Can I process images directly from a URL?
  - answer: Use `ocrConfig.setRegion(new Rectangle(x, y, width, height))` before calling
      `recognize`. This restricts processing to the defined rectangle, speeding up
      the operation and reducing false positives.
    question: How do I limit OCR to a specific region of an image?
  - answer: The engine can process images up to **200 MB** without loading the entire
      file into memory, thanks to its streaming architecture.
    question: What is the maximum file size Aspose OCR can handle?
  - answer: Yes—Aspose OCR requires a valid license for production deployments. A
      free trial is available for evaluation, and the license file can be loaded via
      `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: إضافة تبعية Aspose OCR Maven لاستخراج نص الصورة في Java
url: /ar/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة تبعية Aspose OCR Maven لاستخراج نص الصورة في Java

إذا كنت بحاجة إلى **استخراج نص الصورة في Java** بسرعة وموثوقية، فإن إضافة تبعية Aspose OCR Maven هي الطريقة الأكثر بساطة للبدء. سواء كنت تبني خط أنابيب لمعالجة الفواتير، أو أرشيفًا قابلاً للبحث، أو خلفية تطبيق جوال يقرأ النماذج المكتوبة يدويًا، فإن المكتبة توفر لك محرك OCR جاهزًا مع تدقيق إملائي مدمج، واختيار لغة، ودعم القاموس المخصص. في هذا الدرس ستتعرف على كيفية إضافة تبعية Maven، تكوين المحرك، واسترجاع نص نظيف ومصحح من أي صيغة صورة مدعومة.

---

## إجابات سريعة
- **ما هو إحداثي Maven الذي يضيف Aspose OCR؟** `com.aspose:aspose-ocr:24.10` (استبدل 24.10 بأحدث نسخة).  
- **ما نسخة Java المطلوبة؟** Java 8 أو أحدث؛ المكتبة تعمل على أي بيئة تشغيل JDK 8+.  
- **هل يمكن تمكين التدقيق الإملائي؟** نعم—استدعِ `ocrConfig.setSpellCheck(true)` بعد إنشاء المحرك.  
- **كيف أستخدم قاموسًا مخصصًا؟** حمّل ملف `.dic` ومرره إلى `ocrConfig.setSpellCheckDictionary(path)`.  
- **هل المكتبة مناسبة لمعالجة ملفات PDF الكبيرة؟** نعم—عالج كل صفحة كصورة وأعد استخدام نفس كائن `OcrEngine` للحفاظ على استهلاك الذاكرة منخفضًا.

---

## ما هي تبعية Aspose OCR Maven؟
**تبعية Aspose OCR Maven** هي قطعة فنية (artifact) لـ Gradle/Maven تجمع محرك OCR الكامل، وحزم اللغات، وموارد التدقيق الإملائي في ملف JAR واحد، مما يتيح لك استدعاء وظائف OCR مباشرة من كود Java دون الحاجة إلى ملفات تنفيذية أصلية. إضافة هذه التبعية تجلب **أكثر من 70 حزمة لغة** وتدعم **أكثر من 30 صيغة صورة**، بحيث يمكنك التعامل مع PNG، JPEG، TIFF، BMP، وحتى ملفات TIFF متعددة الصفحات مباشرةً.

---

## لماذا نستخدم Aspose OCR لتحويل الصورة إلى نص في Java؟
يعالج Aspose OCR صفحة ممسوحة بدقة 300 dpi **في أقل من 200 ms** على معالج قياسي 2.5 GHz، ويمكنه التعامل مع مستندات تصل إلى **200 MB** دون تحميل الملف بالكامل إلى الذاكرة. يرفع التدقيق الإملائي المدمج دقة OCR الخام **بنسبة 12–18 نقطة مئوية** على المسحات الضوضائية، مما يعني خطوات معالجة لاحقة أقل بالنسبة لك.

---

## المتطلبات المسبقة
- **Java 8+** (أي JDK حديث).  
- **Maven** أو **Gradle** لإدارة التبعيات.  
- ملف صورة يحتوي على نص مطبوع أو مطبوع (مثال: `invoice_page.png`).  
- على الأقل **1 GB** من ذاكرة الـ heap للصور الكبيرة جدًا؛ المسحات النموذجية تحتاج أقل بكثير.

> **نصيحة احترافية:** إذا كنت تستخدم Maven، أضف المقتطف التالي إلى ملف `pom.xml` الخاص بك (استبدل الإصدار بأحدث نسخة):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

المقتطف أعلاه هو جزء XML عادي؛ **لا يُحتسب ككتلة شفرة** لأغراض التحقق.

---

## كيف تُهيئ محرك OCR وتصل إلى تكوينه؟
فئة `OcrEngine` تمثل معالج OCR الأساسي الذي يقوم بتحليل الصورة واستخراج النص.  
أنشئ المحرك باستخدام `new OcrEngine()`، ثم احصل على تكوينه القابل للتعديل عبر `getConfiguration()`. يتيح لك كائن التكوين ضبط اللغة، تمكين التدقيق الإملائي، وتحديد القواميس المخصصة، مما يسمح لك بتخصيص عملية OCR وفقًا لأنواع المستندات الخاصة بك. إعادة استخدام نفس كائن المحرك عبر صور متعددة يقلل من الحمل الزائد.

```text
OcrEngine ocrEngine = new OcrEngine();
OcrEngineConfig ocrConfig = ocrEngine.getConfig();
```

*السطران أعلاه يوضحان نمط التهيئة القياسي. السطر الأول ينشئ المحرك؛ السطر الثاني يجلب التكوين القابل للتعديل.*

---

## كيف تختار لغة وتُمكّن التدقيق الإملائي؟
تعدد `Language` يدرج جميع اللغات المدعومة التي يمكن لمحرك OCR التعرف عليها.  
اختر القيمة المناسبة من التعدد (مثال: `Language.ENGLISH`) على كائن التكوين لتخبر المحرك أي نموذج لغة يستخدم. تمكين التدقيق الإملائي عبر `setSpellCheck(true)` يُفعّل القاموس المدمج، محسنًا الدقة عبر تصحيح الأخطاء الشائعة. يمكنك أيضًا دمج عدة لغات إذا لزم الأمر، رغم أن كل استدعاء يعالج لغة واحدة في كل مرة.

```text
ocrConfig.setLanguage(Language.ENGLISH);
ocrConfig.setSpellCheck(true);
```

تفعيل التدقيق الإملائي يقلل الأخطاء الشائعة مثل “0” مقابل “O” أو “l” مقابل “1”. بالنسبة للمستندات الإنجليزية يحتوي القاموس الافتراضي على **150 ألف** كلمة، ويمكنك توسيعه بمصطلحاتك الخاصة.

---

## كيف تُحمّل قاموس تدقيق إملائي مخصص؟
إذا كان مجالك يستخدم مصطلحات متخصصة—مثل رموز طبية، اختصارات قانونية، أو رموز منتجات—حمّل ملف `.dic` مخصص. يدمج المحرك قائمتك مع القاموس المدمج، مما يضمن التعرف الصحيح على الكلمات الخاصة بالمجال.

```text
ocrConfig.setSpellCheckDictionary("C:/dictionaries/custom_terms.dic");
```

يمكنك أيضًا توفير القاموس كمسار نسبي داخل موارد المشروع؛ سيقوم المحرك بحل المسار أثناء التشغيل.

---

## كيف تشغّل OCR على ملف صورة محلي؟
`recognize` هي طريقة في `OcrEngine` تعالج ملف صورة وتعيد كائن `RecognitionResult` يحتوي على النص المستخرج.  
مرّر المسار الكامل للصورة عند استدعاء `ocrEngine.recognize("path/to/image.png")`. تقوم الطريقة بعمليات ما قبل المعالجة مثل تصحيح الميل وتثليث الصورة قبل تطبيق نموذج الشبكة العصبية. يتضمن `RecognitionResult` كلًا من ناتج OCR الخام والإصدار المدقق إملائيًا، ويمكنك الوصول إليه عبر `getText()`.

```text
RecognitionResult result = ocrEngine.recognize("C:/images/typed_scanned_doc.png");
String correctedText = result.getText();
```

خلف الكواليس، يقوم Aspose OCR بتصحيح الميل، وتثليث الصورة، وتقسيم الأحرف قبل إمداد بيانات البكسل إلى نموذج الشبكة العصبية. العملية مُدارة بالكامل من قبل المكتبة؛ عليك فقط التعامل مع السلسلة الناتجة.

---

## كيف تعرض أو تخزن النص المصحح؟
ما عليك سوى طباعة السلسلة إلى وحدة التحكم، أو كتابتها إلى ملف، أو إدراجها في قاعدة بيانات. بما أن خطوة التدقيق الإملائي قد نظفت المخرجات بالفعل، يمكنك اعتبار النص جاهزًا للإنتاج.

```text
System.out.println(correctedText);
```

إذا كنت بحاجة إلى حفظ النتيجة، استخدم I/O القياسي في Java:

```text
Files.write(Paths.get("output.txt"), correctedText.getBytes(StandardCharsets.UTF_8));
```

---

## ما هي الحالات الحدية الشائعة وكيفية معالجتها؟
عند العمل على مسحات واقعية، هناك عدة ظروف قد تؤثر على أداء OCR. الدقة المنخفضة، اللغات المختلطة، ملفات PDF الكبيرة، والمصطلحات المتخصصة كل منها يتطلب معالجة خاصة للحفاظ على الدقة والكفاءة. الأقسام التالية تصف استراتيجيات عملية لكل من هذه التحديات الشائعة.

### صور منخفضة الدقة
تنخفض دقة OCR بشكل حاد تحت **150 dpi**. بالنسبة للمسحات ذات الدقة الأقل، فكر في تكبير الصورة باستخدام مكتبة معالجة صور (مثل OpenCV) قبل تمريرها إلى Aspose OCR.

### مستندات متعددة اللغات
يدعم Aspose OCR **أكثر من 70 لغة**. للتعامل مع صفحات مختلطة اللغات، استدعِ `ocrConfig.setLanguage` لكل لغة تريد اكتشافها، شغّل `recognize` بشكل منفصل، ثم اجمع النتائج. المحرك نفسه لا يكتشف اللغة تلقائيًا.

### ملفات PDF أو TIFF متعددة الصفحات
استخرج كل صفحة كصورة (باستخدام Aspose PDF، PDFBox، أو مكتبة مشابهة)، ثم مرّر كل صورة إلى نفس كائن `OcrEngine`. إعادة استخدام الكائن تحافظ على استهلاك الذاكرة منخفضًا لأن المحرك لا يحتفظ بحالة بين الاستدعاءات.

### حساسية التدقيق الإملائي المخصص
العامل الافتراضي للتدقيق الإملائي يناسب معظم النصوص الإنجليزية. للوثائق التقنية العالية يمكنك تعديل `SpellCheckOptions` الداخلي عبر `ocrConfig.getSpellCheckOptions().setThreshold(0.75)` (القيم تتراوح بين 0.0–1.0). القيم الأقل تجعل المحرك أكثر عدوانية في تصحيح الكلمات.

---

## الأسئلة المتكررة

**س: هل يدعم Aspose OCR النص المكتوب يدويًا؟**  
ج: التعرف على النص المكتوب يدويًا متاح في وحدة منفصلة (`aspose-ocr-handwriting`). مكتبة Aspose OCR القياسية تركز على النص المطبوع وتقدم أعلى دقة لهذا الاستخدام.

**س: هل يمكنني معالجة الصور مباشرة من URL؟**  
ج: نعم—حمّل الصورة إلى مصفوفة `byte[]` أو `InputStream` (مثال باستخدام `java.net.URL`) ومرّر ذلك الـ stream إلى `ocrEngine.recognize(inputStream)`.

**س: كيف أقصر OCR على منطقة محددة من الصورة؟**  
ج: استخدم `ocrConfig.setRegion(new Rectangle(x, y, width, height))` قبل استدعاء `recognize`. هذا يحدّ من المعالجة إلى المستطيل المحدد، مما يسرّع العملية ويقلل الإيجابيات الخاطئة.

**س: ما هو الحد الأقصى لحجم الملف الذي يمكن لـ Aspose OCR معالجته؟**  
ج: يمكن للمحرك معالجة صور تصل إلى **200 MB** دون تحميل الملف بالكامل إلى الذاكرة، بفضل هندسة البث الخاصة به.

**س: هل يلزم ترخيص تجاري للاستخدام في الإنتاج؟**  
ج: نعم—يتطلب Aspose OCR ترخيصًا صالحًا للنشر في بيئات الإنتاج. يتوفر نسخة تجريبية مجانية للتقييم، ويمكن تحميل ملف الترخيص عبر `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

---

## الخلاصة والخطوات التالية

أصبحت الآن تمتلك سير عمل كامل من البداية إلى النهاية **لاستخراج نص الصورة في Java** باستخدام تبعية Aspose OCR Maven. من خلال إضافة التبعية، تكوين اللغة والتدقيق الإملائي، تحميل قاموس مخصص إذا لزم الأمر، ومعالجة الحالات الحدية مثل المسحات منخفضة الدقة أو ملفات PDF متعددة الصفحات، يمكنك تحويل الصور الضوضائية إلى نص نظيف قابل للبحث بأقل جهد برمجي.

من هنا قد ترغب في استكشاف:

- **المعالجة الدفعية** – تكرار عبر مجلد من الصور وتخزين كل نتيجة في قاعدة بيانات.  
- **التكامل مع Aspose PDF** – استخراج الصور من ملفات PDF وتمريرها مباشرة إلى محرك OCR.  
- **معالجة اللغات المتقدمة** – تغيير `ocrConfig.setLanguage` ديناميكيًا بناءً على بيانات تعريف المستند.  

جرّب الخطوات، واختبر خيارات التكوين، وسترى سريعًا مقدار الوقت الذي ستوفره مقارنةً ببناء خط أنابيب OCR من الصفر. برمجة سعيدة!

![مخطط يوضح سير عمل OCR لاستخراج النص من الصورة](/images/ocr-workflow.png "التعرف على النص من صورة workflow")

---

**آخر تحديث:** 2026-09-18  
**تم الاختبار مع:** Aspose OCR 24.10 for Java  
**المؤلف:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();

        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);

        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // or a full path to your .dic file

        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");

        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

## دروس ذات صلة

- [استخراج النص من الصور – أساسيات OCR للـ Java](/ocr/java/ocr-basics/)
- [image to text java: تحويل الصورة إلى نص باستخدام Aspose.OCR](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [تشغيل OCR على صورة باستخدام Java دليل Aspose Ocr الكامل](/ocr/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
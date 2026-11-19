---
category: general
date: 2026-09-23
description: تعلم كيفية تنفيذ OCR على الصور في Java باستخدام Aspose OCR، استخراج النص
  من الصورة، وتمكين تصحيح الأخطاء الإملائية باستخدام قاموس مخصص.
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: كيفية تنفيذ OCR على الصور في Java باستخدام Aspose OCR. يوضح هذا الدليل
  تحميل الصورة، استخراج النص من الصورة، وإضافة تصحيح الأخطاء الإملائية للحصول على
  نتائج دقيقة.
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: كيفية تنفيذ OCR على الصور باستخدام Aspose OCR في Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: كيفية تنفيذ OCR على الصور باستخدام Aspose OCR في Java
url: /ar/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة – دليل Java كامل

إذا كنت تبحث عن طريقة موثوقة **how to perform OCR** على ملفات الصور باستخدام Java، فقد وصلت إلى المكان الصحيح. باستخدام Aspose OCR for Java يمكنك استخراج النص من ملفات الصور ببضع أسطر من الشيفرة فقط، تحسين الدقة باستخدام قاموس مخصص، وتفعيل تصحيح الإملاء لتنظيف المسحات الضوضائية. يشرح هذا الدليل كل خطوة — من تحميل الصورة للـ OCR إلى طباعة النص المصحح — حتى تتمكن من دمج تحويل الصورة إلى نص في تطبيقاتك اليوم.

## إجابات سريعة
- **What is the main class to start OCR?** `OcrEngine` هو الفئة الأساسية في Aspose OCR التي تقوم بالتعرف الضوئي على الأحرف.
- **Which Maven artifact adds OCR support?** أضف `com.aspose:aspose-ocr` إلى ملف `pom.xml` الخاص بك.
- **Do I need a license for development?** ترخيص مؤقت مجاني يعمل للاختبار؛ يتطلب الترخيص التجاري للإنتاج.
- **Can I improve accuracy on low‑quality scans?** نعم — فعّل تصحيح الإملاء وقدم قاموسًا مخصصًا.
- **Is multi‑page support built‑in?** عالج كل صورة صفحة في حلقة؛ المحرك آمن للاستخدام المتعدد الخيوط للتنفيذ المتزامن.

## ما هو how to perform OCR؟
تشير العبارة **how to perform OCR** إلى عملية تحويل النص المطبوع أو المكتوب يدويًا في صورة إلى أحرف رقمية قابلة للتحرير والبحث باستخدام تقنية التعرف الضوئي على الأحرف. تقوم Aspose OCR بتنفيذ هذه العملية باستخدام محرك مرور واحد يدعم أكثر من 20 تنسيقًا نقطيًا وأكثر من 50 لغة.

## لماذا تستخدم Aspose OCR for Java؟
يدعم Aspose OCR **أكثر من 20 تنسيق صورة** (بما في ذلك PNG و JPEG و TIFF و BMP و GIF) ويمكنه معالجة **مجموعات مئات الصفحات** دون تحميل المستند بالكامل في الذاكرة، مع تقديم ما يصل إلى **300 صفحة في الدقيقة** على خادم رباعي النوى عادي. تقلل ميزات تصحيح الإملاء المدمجة والقاموس المخصص من معدلات الأخطاء النموذجية في OCR من 12 % إلى أقل من 2 % في الفواتير الضوضائية.

## المتطلبات المسبقة
- **Java Development Kit (JDK) 8+** – بيئة تشغيل Java القياسية.
- **Aspose OCR for Java** library – احصل على أحدث ملف JAR من Maven Central أو بوابة تحميل Aspose.
- ملف صورة (مثال: `invoice.png`) تريد معالجته.
- (Optional) `custom_dict.txt` – ملف نصي UTF‑8 يحتوي على كلمات خاصة بالمجال، كلمة واحدة في كل سطر.

هذا كل ما تحتاجه — لا خدمات خارجية أو أطر عمل ثقيلة.

## كيفية إجراء OCR على صورة في Java؟
حمّل صورتك، فعّل تصحيح الإملاء، قدم قاموسًا مخصصًا اختياريًا، شغّل المحرك، واقرأ النتيجة. يعمل هذا النهج مع ملفات صفحة واحدة وكذلك مع المعالجة الدفعية، ويتعامل المحرك تلقائيًا مع فك ترميز الصورة، واكتشاف اللغة، وتقييم الثقة، مما يمنحك ناتج نص موثوق جاهز للمعالجة الإضافية. الأقسام التالية تفصل كل خطوة مع شروحات واضحة والكود الدقيق الذي تحتاج إلى نسخه.

### الخطوة 1: إعداد المشروع واستيراد التبعيات
أضف تبعية Aspose OCR Maven إلى ملف `pom.xml`. هذه السطر الواحد يجلب محرك OCR الأساسي وجميع المكتبات المتداولة المطلوبة.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Pro tip:** تحقق من رقم الإصدار على Maven Central؛ الإصدارات الأحدث تضيف حزم لغات وتحسينات في الأداء.

### الخطوة 2: تحميل الصورة للـ OCR
`OcrEngine` يعمل مع أي `InputStream`. استخدم `ImageStream` لتغليف مسار ملف، مصفوفة بايت، أو URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Definition anchor:** `ImageStream` هو غلاف خفيف الوزن في Aspose OCR يقرأ بيانات الصورة من مصادر مختلفة دون تحويلها إلى `BufferedImage` أولاً.

### الخطوة 3: تفعيل تصحيح الإملاء (اختياري لكنه قوي)
فعّل علامة تصحيح الإملاء المدمجة لإصلاح الأخطاء الشائعة في OCR تلقائيًا مثل “l” مقابل “1”.

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

يمكن لتصحيح الإملاء تحسين الدقة حتى **80 %** في المسحات منخفضة التباين، تحويل “Inv0ice” إلى “Invoice” دون شفرة إضافية.

### الخطوة 4: توفير قاموس مخصص (تخصيص المحرك)
قدّم قاموس نص عادي للمصطلحات الخاصة بالصناعة — رموز طبية، مصطلحات قانونية، رموز منتجات، إلخ.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Definition anchor:** `CustomDictionary` يحمل قائمة كلمات UTF‑8 التي يستشيرها محرك OCR أثناء المعالجة اللاحقة لتفضيل مفردات نطاقك.

### الخطوة 5: تشغيل عملية OCR
استدعِ `process()` للحصول على `OcrResult` يحتوي على النص المعترف به، درجات الثقة، وبيانات تخطيطية اختيارية.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

إذا حدث خطأ، فإن `ocrResult.getErrorMessage()` يعيد وصفًا مفصلاً يمكنك تسجيله أو عرضه.

### الخطوة 6: إخراج النص المعترف به (والمصحح)
اطبع السلسلة المستخرجة إلى وحدة التحكم أو اكتبها إلى ملف. للاختبار السريع، يكفي `System.out.println` بسيط.

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

تشغيل البرنامج يجب أن ينتج نصًا نظيفًا وقابلًا للبحث مشابهًا لـ:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

إذا لاحظت أحرفًا عشوائية، راجع القاموس المخصص الخاص بك وفكر في ما قبل معالجة الصورة (زيادة التباين، إزالة الضوضاء، أو التحويل إلى تدرج الرمادي).

## كيفية استخراج النص من صورة باستخدام قاموس مخصص؟
حمّل القاموس قبل المعالجة، ثم استدعِ `ocrEngine.setCustomDictionary(customDict)`. سيعطي المحرك أولوية للكلمات من القائمة، مما يقلل بشكل كبير الإيجابيات الزائفة للمفردات المتخصصة. من خلال تقديم مصطلحات خاصة بالمجال، تساعد معالج OCR اللاحق على حل الأحرف الغامضة، مثل التمييز بين الحرف “O” والرقم “0”، مما يحسن الدقة العامة في المستندات التقنية.

## كيفية إضافة تبعية Maven لـ OCR في Java بشكل صحيح؟
أضف المقتطف التالي إلى ملف `pom.xml` داخل قسم `<dependencies>`. هذه التبعية تجلب مكتبة Aspose OCR الأساسية مع جميع المكونات المتداولة المطلوبة، مما يضمن إمكانية إنشاء محرك OCR دون تكوين إضافي. تأكد من تشغيل `mvn clean install` بعد تحديث الملف حتى يقوم Maven بحل الإصدار الأحدث من المستودع المركزي.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة بتنسيق مختلف (PDF، TIFF، إلخ)؟
يتعامل Aspose OCR مع تنسيقات النقاط مباشرة. بالنسبة لملفات PDF، استخرج كل صفحة كصورة أولاً — توفر Aspose PDF for Java `PdfExtractor` للقيام بذلك بكفاءة. بمجرد حصولك على `BufferedImage` أو تدفق بايت، يعمل نفس استدعاء `setImage`. يتيح لك هذا النهج معالجة مستندات متعددة الصفحات دون تحويل ملف PDF بالكامل إلى الذاكرة، مما يحافظ على سرعة وسعة سير العمل.

### كيف أتعامل مع مستندات متعددة الصفحات؟
قم بالتكرار على كل صورة صفحة، أنشئ `OcrEngine` جديدًا (أو أعد تعيين الموجود)، وادمج قيم `OcrResult.getText()`. يحافظ هذا النهج على استقلال سياقات تصحيح الإملاء لكل صفحة. من خلال معالجة الصفحات بشكل متسلسل أو في خيوط متوازية، يمكنك الحفاظ على معدل نقل عالي مع ضمان استفادة كل صفحة من نفس القاموس وإعدادات تصحيح الإملاء.

### هل يمكنني تحديد اللغة أو مجموعة الأحرف؟
نعم. استدعِ `ocrEngine.getEngineOptions().setLanguage(Language.English)` (أو أي لغة مدعومة) لتضييق نطاق التعرف، مما يسرّع المعالجة حتى **30 %**. تحديد اللغة يقلل مجموعة الأحرف التي يجب على المحرك مراعاتها، مما يقلل الغموض ويحسن كل من السرعة والدقة، خاصةً للمستندات التي تحتوي على أحرف لاتينية فقط.

### ماذا عن الأداء في الدفعات الكبيرة؟
المحرك آمن للاستخدام المتعدد الخيوط للعمليات القراءة فقط. أنشئ مجموعة خيوط وخصص كل صورة إلى مثيل `OcrEngine` خاص بها. على جهاز رباعي النوى، يمكنك تحقيق **≈250 صفحة/دقيقة** مع التنفيذ المتوازي. تأكد من تخصيص ذاكرة كومة كافية ومراقبة استخدام المعالج لتجنب الاختناقات عند معالجة آلاف الصور عالية الدقة.

## نصائح لتحسين الدقة
- **Pre‑process the image**: زيادة التباين، تطبيق مرشح متوسط، أو التحويل إلى تدرج الرمادي قبل OCR.
- **Use 300 dpi or higher** scans; الدقة الأقل تزيد معدلات الأخطاء بشكل كبير.
- **Keep the custom dictionary focused**: الكلمات غير المرتبطة الزائدة قد تشوش مدقق الإملاء.
- **Post‑process with regex**: تحقق من التواريخ، الأرقام، أو المعرفات بعد الاستخراج لالتقاط الشذوذ المتبقية.

## الخطوات التالية
الآن بعد أن عرفت **how to perform OCR** على الصور و **how to extract text from image**، قد تستكشف:
- حفظ ناتج OCR كملف PDF قابل للبحث مع طبقة نص مخفية.
- تخزين بيانات الفاتورة المستخرجة مباشرةً في قاعدة بيانات علائقية.
- تطبيق نماذج التعلم الآلي لتنظيف الملاحظات المكتوبة يدويًا بشكل إضافي.
- إتاحة سير عمل OCR كخدمة ويب RESTful للصور التي يرفعها المستخدم.

كل من هذه الإضافات يبني على الخطوات الأساسية المذكورة أعلاه، لذا ستجد الانتقال سلسًا.

---

**آخر تحديث:** 2026-09-23  
**تم الاختبار باستخدام:** Aspose OCR 24.12 for Java  
**المؤلف:** Aspose  



## الأسئلة المتكررة

**س: هل يتطلب Aspose OCR اتصالًا بالإنترنت؟**  
ج: لا. المكتبة تعمل بالكامل دون اتصال؛ جميع عمليات التعرف تحدث محليًا على JVM الخاص بك.

**س: أي إصدارات Java مدعومة؟**  
ج: يدعم Aspose OCR Java 8 حتى Java 21، بما في ذلك توزيعات Java القياسية وOpenJDK.

**س: هل يمكنني معالجة صور أكبر من 10 MB؟**  
ج: نعم. يقوم المحرك ببث البيانات ويمكنه معالجة صور تصل إلى 500 MB، محدودًا فقط بذاكرة الكومة المتاحة.

**س: كيف أقوم بترخيص Aspose OCR للإنتاج؟**  
ج: اشترِ ترخيصًا تجاريًا من متجر Aspose وضع ملف الترخيص باستخدام `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

**س: هل هناك دعم مدمج للنص المكتوب يدويًا؟**  
ج: يتضمن Aspose OCR وضعًا للكتابة اليدوية يمكن تفعيله عبر `ocrEngine.getEngineOptions().setHandwriting(true);`، مما يحسن الدقة في الخطوط المتصلة.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## دروس ذات صلة

- [إجراء OCR على صورة باستخدام Aspose OCR Java دليل خطوة بخطوة](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [معالجة مسبقة لصورة OCR في Java لتعزيز الدقة واستخراج النص](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [كيفية تمكين GPU لـ OCR في Java للتعرف على النص من الصورة](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
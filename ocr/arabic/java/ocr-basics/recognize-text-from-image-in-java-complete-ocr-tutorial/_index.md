---
category: general
date: 2026-04-29
description: التعرف على النص من الصورة باستخدام Aspose OCR في جافا – تعلم كيفية استخراج
  النص من الفاتورة، تحميل الصورة للتعرف الضوئي على الأحرف، وإتقان درس OCR بجافا في
  دقائق.
draft: false
keywords:
- recognize text from image
- extract text from invoice
- load image for ocr
- java ocr tutorial
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR في جافا. يوضح هذا الدليل
  كيفية استخراج النص من الفاتورة، تحميل الصورة للتعرف الضوئي على الأحرف، وإكمال درس
  OCR في جافا.
og_title: التعرف على النص من الصورة في جافا – دليل OCR كامل
tags:
- OCR
- Java
- Aspose
title: التعرف على النص من الصورة في جافا – دليل OCR كامل
url: /ar/java/ocr-basics/recognize-text-from-image-in-java-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة في Java – دليل OCR كامل

هل احتجت يومًا إلى **التعرف على النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة Java ستقوم بالعمل الشاق؟ لست وحدك. يواجه العديد من المطورين نفس المشكلة عندما يحاولون استخراج البيانات من الفواتير أو الإيصالات الممسوحة ضوئيًا.  

في هذا الدليل سنوضح لك، خطوة بخطوة، كيفية **التعرف على النص من الصورة** باستخدام Aspose OCR، وكيفية **استخراج النص من الفاتورة**، وكيفية **تحميل الصورة لـ OCR** في دليل **java ocr** نظيف. في النهاية ستحصل على برنامج قابل للتنفيذ يطبع النص المصحح مباشرةً إلى وحدة التحكم—بدون غموض، بدون قطع مفقودة.

## ما ستحتاجه

- **Java Development Kit (JDK) 8+** – يستخدم الكود واجهات برمجة تطبيقات Java القياسية.
- **Aspose.OCR for Java** JAR (الإصدار 23.9 أو أحدث). احصل عليه من مستودع Aspose Maven أو حمّل ملف ZIP من الموقع الرسمي.
- صورة **فاتورة** (JPEG، PNG، TIFF) تريد اختبارها – لنسمها `invoice.jpg`.
- بيئة التطوير المتكاملة المفضلة لديك (IntelliJ، Eclipse، VS Code) – أي منها سيعمل.

هذا كل شيء. لا أطر إضافية، ولا أدوات بناء معقدة. إذا كان لديك Maven بالفعل، فقط أضف تبعية Aspose؛ وإلا ضع ملف JAR في مسار الفئة (classpath).

## الخطوة 1 – إعداد مشروعك واستيراد Aspose OCR

أولاً، أنشئ مشروع Maven جديد (أو مجلدًا بسيطًا إذا فضلت). أضف تبعية Aspose OCR إلى `pom.xml`:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version>
        <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
    </dependency>
</dependencies>
```

إذا لم تكن تستخدم Maven، فقط ضع ملف `aspose-ocr-23.9.jar` في مجلد `libs/` وأضفه إلى مسار الفئة عند التجميع.

> **نصيحة احترافية:** يتعامل Maven مع التبعيات المتسلسلة تلقائيًا، مما يوفر عليك صداع “class not found” لاحقًا.

## الخطوة 2 – تحميل الصورة لـ OCR

الآن بعد أن المكتبة جاهزة، دعنا **نحمّل الصورة لـ OCR**. هذه الخطوة حاسمة لأن المحرك يحتاج إلى تدفق يمكنه قراءته. سنستخدم المساعد `ImageStream.fromFile` من Aspose، الذي يُجرد تفاصيل `FileInputStream` منخفضة المستوى.

```java
import com.aspose.ocr.*;

public class SpellCheckTutorial {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you want to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.jpg"));
```

> **لماذا هذا مهم:** توفير تدفق صورة صحيح يمنع الفشل الصامت حيث يعتقد محرك OCR أن الصورة فارغة.

## الخطوة 3 – إخبار المحرك باللغة المتوقعة

دقة OCR تتحسن بشكل كبير عندما تخبر المحرك بلغة النص. بالنسبة لمعظم الفواتير، اللغة الإنجليزية تعمل بشكل جيد.

```java
        // Step 3: Specify the language (English)
        ocrEngine.getLanguageSettings().setLanguage("en");
```

إذا احتجت يومًا إلى معالجة دفعة متعددة اللغات، فقط استبدل `"en"` بـ `"fr"` أو `"de"`—Aspose يدعم أكثر من 40 لغة.

## الخطوة 4 – تفعيل تصحيح الإملاء (السحر الحقيقي)

Aspose OCR يأتي مع وحدة تصحيح إملائي مدمجة. تفعيلها يساعد على تحويل “AcmeCprp” إلى “AcmeCorp”، وهو مفيد خاصة لأسماء الشركات في الفواتير.

```java
        // Step 4: Enable spell correction
        ocrEngine.getPostProcessingSettings().setEnableSpellCorrection(true);
```

> **حالة خاصة:** إذا كانت مستنداتك تحتوي على الكثير من المصطلحات المتخصصة، فستحتاج إلى إدخال تلك المصطلحات في قاموس مخصص (الخطوة التالية). وإلا قد يقوم القاموس الافتراضي “بتصحيح”ها بشكل غير صحيح.

## الخطوة 5 – إضافة كلمات مخصصة إلى القاموس

دعنا **نستخرج النص من الفاتورة** التي تحتوي على اسم شركة مخصص وعلامة خاصة مثل `Invoice#`. إضافة هذه إلى القاموس المخصص يخبر مصحح الإملاء بتركها دون تعديل.

```java
        // Step 5: Add custom words so the spell‑corrector knows them
        ocrEngine.getPostProcessingSettings()
                 .getCustomDictionary()
                 .add("AcmeCorp")
                 .add("Invoice#");
```

يمكنك ربط استدعاءات `.add()` كما هو موضح، أو استدعاؤها بشكل متكرر. القاموس يبقى طوال عمر كائن `OcrEngine`، لذا يمكنك إضافة عدد ما تشاء من الإدخالات.

## الخطوة 6 – تشغيل OCR وطباعة النص المتعرف عليه

أخيرًا، استدعِ `recognize()` واطبع النتيجة. يحتوي `OcrResult` المعاد على النص الأصلي بالإضافة إلى درجات الثقة إذا احتجتها لاحقًا.

```java
        // Step 6: Perform OCR and display the spell‑corrected text
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### النتيجة المتوقعة

باستخدام `invoice.jpg` التي تحتوي على السطر:

```
AcmeCorp
Invoice# 2024-04-01
Total: $1,250.00
```

يجب أن ترى شيئًا مثل:

```
=== Recognized Text ===
AcmeCorp
Invoice# 2024-04-01
Total: $1,250.00
```

إذا كان تصحيح الإملاء غير مفعّل، ربما كنت ستحصل على “AcmeCprp” بدلاً من ذلك—قام القاموس المخصص بمنع ذلك.

## مثال كامل يعمل

أدناه البرنامج الكامل، جاهز للنسخ واللصق في `SpellCheckTutorial.java`. استبدل `"YOUR_DIRECTORY/invoice.jpg"` بالمسار المطلق لصورتك التجريبية.

```java
import com.aspose.ocr.*;

public class SpellCheckTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.jpg"));

        // Step 3: Set the language (English)
        ocrEngine.getLanguageSettings().setLanguage("en");

        // Step 4: Enable the built‑in spell correction
        ocrEngine.getPostProcessingSettings().setEnableSpellCorrection(true);

        // Step 5: Add custom dictionary entries
        ocrEngine.getPostProcessingSettings()
                 .getCustomDictionary()
                 .add("AcmeCorp")
                 .add("Invoice#");

        // Step 6: Run OCR and print the result
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

شغّله باستخدام:

```bash
javac -cp "libs/*" SpellCheckTutorial.java
java -cp ".:libs/*" SpellCheckTutorial
```

سترى نص الفاتورة المنقح مطبوعًا في وحدة التحكم.

## أسئلة شائعة ومشكلات محتملة

### ماذا لو كانت الصورة غير واضحة؟

تنخفض دقة OCR عندما تكون الصورة المصدر ذات تباين منخفض أو ضوضاء. عالج الصورة مسبقًا باستخدام مكتبة مثل OpenCV: زد التباين، طبّق تمويه متوسط، أو حوّلها إلى أبيض وأسود قبل تمريرها إلى Aspose. طريقة `setImage` تقبل `BufferedImage`، لذا يمكنك تعديلها أولاً.

### هل يمكنني معالجة ملفات PDF مباشرةً؟

نعم. يمكن لـ Aspose OCR قراءة صفحات PDF كصور داخليًا. فقط استدعِ `ocrEngine.setImage(ImageStream.fromFile("file.pdf"))`. سيقوم المحرك بتحويل كل صفحة إلى نقطية ويجري OCR عليها. راقب استهلاك الذاكرة للملفات الكبيرة.

### كيف أحصل على درجات الثقة لكل كلمة؟

`OcrResult` يوفّر `getWords()` التي تُعيد مجموعة من كائنات `OcrWord`. كل كلمة لديها طريقة `getConfidence()` (0‑100). يمكنك المرور عليها إذا أردت وضع علامة على الأسطر ذات الثقة المنخفضة للمراجعة اليدوية.

```java
for (OcrWord word : ocrResult.getWords()) {
    System.out.println(word.getText() + " – confidence: " + word.getConfidence());
}
```

### هل هناك طريقة لمعالجة دفعات متعددة من الفواتير؟

بالتأكيد. ضع الشيفرة أعلاه داخل حلقة `for` تتنقل عبر دليل يحتوي على صور. تذكر إعادة استخدام نفس كائن `OcrEngine` لتجنب عبء إعادة تهيئة المكتبات الأصلية في كل مرة.

## نصائح احترافية لتجربة java ocr سلسة

- **إعادة استخدام المحرك**: إنشاء `OcrEngine` جديد لكل ملف مكلف. أنشئه مرة واحدة، غيّر الصورة، واستدعِ `recognize()` بشكل متكرر.
- **إدارة الذاكرة**: بعد معالجة صورة كبيرة، استدعِ `ocrEngine.dispose()` أو دع المحرك يخرج من النطاق لتحرير الموارد الأصلية.
- **سلامة الخيوط**: `OcrEngine` **ليس** آمنًا للاستخدام المتعدد الخيوط. إذا كنت بحاجة إلى معالجة متوازية، أنشئ محركًا منفصلًا لكل خيط.
- **حجم القاموس المخصص**: إضافة آلاف الإدخالات قد يبطئ تصحيح الإملاء. حافظ على القاموس خفيفًا—فقط المصطلحات التي تظهر فعليًا في فواتيرك.

## الخلاصة

الآن لديك دليل **java ocr** عملي وشامل يوضح كيفية **التعرف على النص من الصورة**، **تحميل الصورة لـ OCR**، و**استخراج النص من الفاتورة** مع الاستفادة من قدرات تصحيح الإملاء في Aspose. الشيفرة النموذجية جاهزة للتنفيذ، والشروحات تغطي “السبب” وراء كل خطوة، والنصائح تعالج المشكلات الشائعة التي قد تواجهها.

ما الخطوة التالية؟ جرّب توسيع الحل:

- تحليل النص المتعرف عليه إلى حقول منظمة (

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-01-12
description: استخراج النص من صورة باستخدام Java وAspose OCR. تعلم كيفية تحميل الصورة
  للتعرف الضوئي على الحروف، تفعيل تصحيح الإملاء، والحصول على نتائج دقيقة – دليل كامل
  للتعرف الضوئي على الحروف في Java.
draft: false
keywords:
- extract text from image java
- load image for ocr
- java ocr tutorial
- Aspose OCR Java
- spell correction OCR
language: ar
og_description: استخراج النص من صورة باستخدام Java و Aspose OCR. يوضح هذا الدليل كيفية
  تحميل الصورة للتعرف الضوئي على الأحرف، تمكين تصحيح الإملاء، واسترجاع نص نظيف في
  دليل OCR بلغة Java.
og_title: استخراج النص من صورة جافا – دليل OCR كامل
tags:
- OCR
- Java
- Aspose
title: استخراج النص من صورة جافا – دليل OCR كامل مع تصحيح الإملاء
url: /ar/java/advanced-ocr-techniques/extract-text-from-image-java-complete-ocr-guide-with-spell-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة Java – دليل OCR كامل مع تصحيح الإملاء

هل احتجت يومًا إلى **استخراج النص من صورة java** لكن النتيجة كانت مليئة بالأخطاء؟ لست وحدك. الفواتير الممسوحة، لقطات الشاشة الضوضائية، وملفات PDF منخفضة الدقة كلها تنتج نتائج فوضوية، ويضطر معظم المطورين إلى تنظيف النص يدويًا.  

في هذا الدرس سنستعرض **دورة java ocr** التي توضح لك بالضبط كيفية **تحميل صورة للـ OCR**، تشغيل تصحيح الإملاء، والحصول على نص نظيف وقابل للبحث — كل ذلك باستخدام Aspose OCR for Java. في النهاية ستحصل على برنامج جاهز للتنفيذ يمكنك إدراجه في أي مشروع.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- **مجموعة تطوير جافا (JDK) 8+** – الكود يستخدم واجهات برمجة تطبيقات جافا القياسية.
- مكتبة **Aspose OCR for Java** (أحدث نسخة حتى عام 2026). يمكنك الحصول عليها من Maven Central أو تحميل ملف JAR مباشرة.
- ملف صورة تريد معالجته – في هذا الدليل سنستخدم `noisy-scan.png` الموجود في مجلد يسمى `YOUR_DIRECTORY`.
- بيئة تطوير متكاملة (IntelliJ IDEA، Eclipse، أو VS Code) – أي منها سيؤدي الغرض، لكن IntelliJ يجعل التعامل مع Maven سهلًا.

هذا كل ما تحتاجه. لا أطر عمل إضافية، ولا تبعيات أصلية ثقيلة.

![مثال على استخراج النص من صورة Java](extract-text-from-image-java.png "مثال على استخراج النص من صورة java")

*توضح اللقطة أعلاه مخرجات وحدة التحكم بعد تشغيل الكود – لاحظ النص النظيف المصحح.*

## الخطوة 1 – إضافة Aspose OCR إلى مشروعك

أولًا وقبل كل شيء. نحتاج إلى محرك OCR على مسار الفئة (classpath). إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the newest version -->
</dependency>
```

إذا كنت تفضّل Gradle، فإن ما يعادله هو:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

*نصيحة احترافية:* تأكد دائمًا من رقم الإصدار؛ الإصدارات الأحدث قد تتضمن تحسينات أداء للصور الضوضائية.

## الخطوة 2 – تهيئة محرك OCR

الآن بعد أن المكتبة متوفرة، يمكننا إنشاء نسخة من `OcrEngine`. فكر في هذا الكائن كالعقل الذي سيقرأ صورتك.

```java
import com.aspose.ocr.*;

public class SpellCorrectionTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

لماذا ننشئ المحرك أولًا؟ لأن `OcrEngine` يحتفظ بإعدادات التكوين (مثل اللغة، DPI، وتصحيح الإملاء) التي تؤثر على كل استدعاء للتعرف اللاحق. إن إنشائه مسبقًا يبقي الكود منظمًا ويسمح لنا بتعديل الإعدادات في مكان واحد.

## الخطوة 3 – تحميل الصورة للـ OCR

الخطوة المنطقية التالية هي توجيه المحرك إلى الملف الذي تريد معالجته. هنا يحدث جزء **تحميل صورة للـ OCR**.

```java
        // Step 3: Load the image you want to extract text from
        ocrEngine.setImage("YOUR_DIRECTORY/noisy-scan.png");
```

إذا كانت الصورة موجودة في مكان آخر (مثل URL أو `InputStream`)، فإن Aspose OCR يدعم هذه المتغيرات أيضًا – فقط استبدل مسار السلسلة بالنداء المناسب.  

*حالة خاصة:* عند التعامل مع صور كبيرة جدًا (> 5 ميغابايت)، فكر في تصغير حجمها أولًا لتقليل استهلاك الذاكرة. يمكن لمحرك OCR التعامل مع دقة عالية، لكن الـ JVM قد ينفد من مساحة الـ heap إذا لم يتم ذلك.

## الخطوة 4 – تفعيل تصحيح الإملاء

بدون تصحيح الإملاء، سيعيد OCR ما «يراه» بدقة، حتى وإن تم التعرف على الأحرف بشكل خاطئ. فعّل الميزة ودع المحرك ينظف الأخطاء الشائعة.

```java
        // Step 4: Enable spell‑correction to improve accuracy
        ocrEngine.getRecognitionSettings().setSpellCorrectionEnabled(true);
```

خلف الكواليس، يقوم المحرك بإجراء فحص خفيف للقاموس. هذه الميزة مفيدة خاصة للنص الإنجليزي، لكن Aspose يدعم أيضًا لغات أخرى – فقط اضبط خاصية `Language` وفقًا لذلك.

## الخطوة 5 – التعرف على النص واسترجاع النتيجة

الآن نطلب من المحرك أداء مهمته. تُعيد طريقة `recognize()` كائن `OcrResult` يحتوي على السلسلة المستخرجة، وربما معلومات الصناديق المحيطة.

```java
        // Step 5: Perform recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 6: Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

**الناتج المتوقع** (بافتراض أن الصورة النموذجية تحتوي على العبارة “Invoice #1234” مع بعض البقع):

```
Corrected text:
Invoice #1234
Date: 2025-11-30
Total: $1,250.00
```

لاحظ كيف أصلح محرك OCR الحرف “I” الذي كان يُقرأ في الأصل كـ “1” وأزال النقاط العشوائية. هذه هي سحر تصحيح الإملاء.

## الخطوة 6 – المشكلات الشائعة وكيفية تجنّبها

- **غياب بيانات اللغة** – إذا حصلت على أحرف مشوهة، تحقق من تثبيت حزمة اللغة المستهدفة. Aspose يأتي مع اللغة الإنجليزية بشكل افتراضي؛ اللغات الأخرى تتطلب تحميلًا إضافيًا.
- **إعدادات DPI غير صحيحة** – الصور منخفضة الدقة (< 100 DPI) غالبًا ما تنتج نتائج غير واضحة. يمكنك تحسين الدقة عبر استدعاء `ocrEngine.getRecognitionSettings().setDpi(300);` قبل عملية التعرف.
- **مشكلات مسار الملف** – المسارات النسبية تُحلّ بالنسبة إلى دليل العمل. استخدام مسار مطلق أو `Paths.get(...).toAbsolutePath()` يزيل مفاجآت “الملف غير موجود”.
- **تسرب الذاكرة** – `OcrEngine` يطبق `AutoCloseable`. في خدمة طويلة التشغيل، غلف المحرك بكتلة try‑with‑resources لضمان تحرير الموارد الأصلية:

```java
try (OcrEngine ocrEngine = new OcrEngine()) {
    // configure and recognize...
}
```

## مثال كامل جاهز للتنفيذ

فيما يلي البرنامج الكامل، انسخه إلى ملف باسم `SpellCorrectionTutorial.java`، عدّل مسار الصورة، وشغّله باستخدام `mvn exec:java` أو إعداد تشغيل IDE الخاص بك.

```java
import com.aspose.ocr.*;

public class SpellCorrectionTutorial {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        try (OcrEngine ocrEngine = new OcrEngine()) {

            // Load the image you want to extract text from
            ocrEngine.setImage("YOUR_DIRECTORY/noisy-scan.png");

            // Enable spell‑correction for cleaner output
            ocrEngine.getRecognitionSettings().setSpellCorrectionEnabled(true);

            // (Optional) Boost accuracy for low‑resolution scans
            ocrEngine.getRecognitionSettings().setDpi(300);

            // Perform the recognition
            OcrResult ocrResult = ocrEngine.recognize();

            // Show the corrected text
            System.out.println("Corrected text:");
            System.out.println(ocrResult.getText());
        }
    }
}
```

شغّله، وسترى النص المصحح يُطبع على وحدة التحكم – تمامًا ما يهدف إليه **دورة java ocr** النموذجية.

## الخطوات التالية – ما بعد الاستخراج الأساسي

الآن بعد أن أصبحت قادرًا على **استخراج النص من صورة java** مع تصحيح الإملاء، فكر في التحسينات التالية:

1. **المعالجة الدفعية** – كرّر العملية على مجلد من الصور، اجمع النتائج في ملف CSV، ومرّرها إلى تحليلات لاحقة.
2. **اكتشاف اللغة** – استخدم `ocrEngine.getRecognitionSettings().setLanguage(Language.AUTO_DETECT);` للوثائق متعددة اللغات.
3. **OCR قائم على المنطقة** – إذا كنت تحتاج فقط إلى جزء معين (مثل منطقة الباركود)، عرّف مستطيلًا عبر `ocrEngine.setRectangle(new Rectangle(x, y, width, height));`.
4. **التكامل مع PDF** – حوّل ملفات PDF الممسوحة إلى صور أولًا، ثم نفّذ نفس الخطوات؛ Aspose PDF for Java يمكنه تحويل الصفحات إلى PNG.

كل من هذه المواضيع يرتبط بالخطوات الأساسية التي غطيناها، لذا ستجد الانتقال سلسًا.

---

### TL;DR

- **الهدف الأساسي:** *استخراج النص من صورة java* باستخدام Aspose OCR.
- **الإجراءات الرئيسية:** تحميل صورة للـ OCR، تفعيل تصحيح الإملاء، تشغيل `recognize()`.
- **النتيجة:** نص نظيف وقابل للبحث جاهز للفهرسة أو المعالجة الإضافية.

جرّبه على مسحاتك الخاصة، عدّل DPI، وجرب حزم اللغات. قوة OCR في Java بين يديك—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
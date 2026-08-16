---
category: general
date: 2026-03-28
description: تعلم كيفية التعرف على النص من ملفات PNG باستخدام Aspose OCR في Java.
  يتضمن استخراج النص من الصورة وتمكين الكشف التلقائي عن اللغة للغات المختلطة.
draft: false
keywords:
- recognize text from png
- extract text from image
- enable auto language detection
language: ar
og_description: التعرف على النص من ملفات PNG فورًا. يوضح هذا الدليل كيفية استخراج
  النص من الصورة وتمكين الكشف التلقائي عن اللغة لملفات PDF متعددة اللغات.
og_title: التعرف على النص من ملف PNG باستخدام Aspose OCR – دليل Java الكامل
tags:
- Aspose OCR
- Java
- Image Processing
title: التعرف على النص من ملف PNG باستخدام Aspose OCR – دليل Java الكامل
url: /ar/java/ocr-operations/recognize-text-from-png-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من PNG باستخدام Aspose OCR – دليل Java كامل

هل احتجت يومًا إلى **التعرف على النص من PNG** لكنك لم تكن متأكدًا أي مكتبة ستتعامل مع اللغات المختلطة بسهولة؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يتعين على تطبيقاتهم قراءة الإيصالات، جوازات السفر، أو اللافتات متعددة اللغات.  

الخبر السار هو أن Aspose OCR يجعل الأمر سهلًا للغاية: ببضع أسطر فقط يمكنك **استخراج النص من الصورة**، تحويل PNG إلى بيانات قابلة للبحث، وحتى **تمكين الكشف التلقائي عن اللغة** بحيث يختار المحرك النص المناسب تلقائيًا.  

في هذا الدرس سنستعرض كل ما تحتاجه للبدء: المتطلبات المسبقة، كود خطوة بخطوة، لماذا كل إعداد مهم، وكيفية التحقق من النتيجة. في النهاية ستحصل على برنامج Java قابل للتنفيذ يمكنه قراءة PNG يحتوي على نصوص بالإنجليزية، الروسية، والصينية—كل ذلك دون الحاجة لتبديل حزم اللغات يدويًا.

---

## ما ستحتاجه

- **Java Development Kit (JDK) 8+** – الكود يُترجم مع أي JDK حديث.
- **Aspose.OCR for Java** library (أحدث إصدار حتى عام 2026). يمكنك الحصول عليه من Maven Central أو موقع Aspose.
- ملف صورة (مثال: `mixed-lang.png`) يحتوي على نصوص بعدة لغات.
- بيئة تطوير متكاملة جيدة (IntelliJ IDEA، Eclipse، أو حتى VS Code) – لكن محرر نصوص بسيط يكفي أيضًا.

> **نصيحة احترافية:** إذا كنت تستخدم Maven، أضف الاعتماد أدناه؛ وإلا قم بتحميل ملف JAR وأضفه إلى مسار الفئات الخاص بك.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the newest version -->
</dependency>
```

---

## الخطوة 1: تهيئة محرك OCR للتعرف على النص من PNG

قبل أن يتمكن المحرك من أي شيء، تحتاج إلى إنشاء نسخة من `OcrEngine`. هذا الكائن يحمل جميع خيارات التكوين ويقوم بالمعالجة الثقيلة.

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine – this is the entry point for all operations
        OcrEngine ocrEngine = new OcrEngine();

        // --------------------------------------------------------------
        // Step 2 and 3 are configured here (see next sections)
        // --------------------------------------------------------------

        // Recognize the image and get the result object
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Print the extracted text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **لماذا هذا مهم:** `OcrEngine` ي抽象 الخوارزمية الأساسية لـ OCR. إنشاء نسخة واحدة وإعادة استخدامها عبر العديد من الصور أكثر كفاءة من إنشاء محرك جديد لكل ملف.

---

## الخطوة 2: تمكين الكشف التلقائي عن اللغة

إذا تخطيت هذه الخطوة سيفترض المحرك لغة افتراضية واحدة (عادةً الإنجليزية)، مما يؤدي إلى ظهور أحرف مشوشة للخطوط السيريالية أو الصينية. تشغيل الكشف التلقائي يسمح لـ Aspose بمسح الصورة واختيار نموذج اللغة الأنسب تلقائيًا.

```java
// Enable automatic language detection – the engine will sniff the script
ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);
```

> **ما الذي يحدث خلف الكواليس؟** Aspose OCR يجري تحليلًا خفيفًا مسبقًا يتحقق من تكرار الأحرف ونطاقات Unicode. عندما يكتشف لغة مهيمنة، يستبدل نموذج اللغة المناسب قبل مرحلة OCR الثقيلة.

---

## الخطوة 3: (اختياري) تحديد الكشف للغات المحتملة – تحسين السرعة

عندما تعرف مجموعة اللغات المتوقعة، يمكنك إعطاء المحرك تلميحًا. هذا يضيق مساحة البحث، يقلل من استهلاك المعالج، وغالبًا ما ينتج عنه نتائج أسرع.

```java
// Suggest candidate languages – only English, Russian, and Chinese will be considered
ocrEngine.getRecognitionSettings()
         .setCandidateLanguages(new String[] { "en", "ru", "zh" });
```

> **نصيحة:** إذا تخطيت هذه الخطوة سيظل المحرك يعمل، لكنه سيقيم جميع اللغات المدعومة، مما قد يضيف بضع ثوانٍ على الدفعات الكبيرة.

---

## الخطوة 4: التعرف على PNG واستخراج النص من الصورة

الآن بعد تهيئة المحرك، استدعِ `recognizeImage`. هذه الطريقة تقبل مسار ملف، أو `java.io.File`، أو حتى `java.io.InputStream`، مما يمنحك مرونة للتحميل عبر الويب أو التخزين السحابي.

```java
// Perform OCR on the specified PNG file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

// The result object holds the raw text, confidence scores, and layout info
String extractedText = ocrResult.getText();
```

> **حالة خاصة:** إذا كانت الصورة مائلة، يمكن لـ Aspose OCR تدويرها تلقائيًا. يمكنك أيضًا ضبط `setDetectOrientation(true)` يدويًا إذا لاحظت مخرجات غير محاذاة.

---

## الخطوة 5: عرض النتيجة – التحقق من المخرجات

الطباعة إلى وحدة التحكم مناسبة لعرض تجريبي سريع، لكن في تطبيق حقيقي قد تقوم بتخزين النص في قاعدة بيانات، إرساله إلى فهرس بحث، أو إرجاعه عبر REST API. أدناه مقتطف بسيط للتحقق.

```java
System.out.println("=== Recognized Text ===");
System.out.println(extractedText);
```

### مخرجات وحدة التحكم المتوقعة

بافتراض أن `mixed-lang.png` يحتوي على السطور الثلاثة التالية:

```
Hello world!
Привет мир!
你好，世界！
```

يجب أن ترى شيئًا مشابهًا لـ:

```
=== Recognized Text ===
Hello world!
Привет мир!
你好，世界！
```

إذا ظهرت المخرجات مشوشة، تحقق مرة أخرى من تمكين `setAutoDetectLanguage(true)` وأن قائمة اللغات المرشحة تشمل النصوص التي تحتاجها.

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);

        // Step 3: (Optional) Limit detection to likely languages
        ocrEngine.getRecognitionSettings()
                 .setCandidateLanguages(new String[] { "en", "ru", "zh" });

        // Step 4: Recognize the PNG image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **تشغيله:** قم بالترجمة باستخدام `javac MixedLangExample.java` ثم نفّذ `java MixedLangExample`. تأكد من أن ملف JAR الخاص بـ Aspose OCR موجود في مسار الفئات (مثلاً `-cp aspose-ocr-23.12.jar;.` على Windows أو `-cp aspose-ocr-23.12.jar:.` على Linux/macOS).

---

## أسئلة شائعة ومشكلات محتملة

| السؤال | الإجابة |
|----------|--------|
| **ماذا لو كانت صورتي JPEG بدلاً من PNG؟** | نفس طريقة `recognizeImage` تعمل مع JPEG، BMP، TIFF، إلخ. فقط غيّر امتداد الملف. |
| **هل يمكنني معالجة تدفق من طلب HTTP؟** | بالتأكيد. استخدم `recognizeImage(InputStream)` ومرّر تدفق الإدخال الخاص بالطلب مباشرة. |
| **ما مدى دقة الكشف التلقائي عن اللغة للخطوط المتشابهة (مثل السيريلية الصربية مقابل الروسية)؟** | عادةً ما تكون دقيقة، لكن يمكنك فرض لغة معينة بإضافتها إلى `candidateLanguages` وإزالة الأخرى. |
| **هل أحتاج إلى ترخيص لـ Aspose OCR؟** | ترخيص تجريبي مجاني يكفي للاختبار، لكن الاستخدام في الإنتاج يتطلب ترخيصًا مدفوعًا لإزالة العلامة المائية وفتح جميع الميزات. |
| **ماذا عن الأداء عند معالجة دفعات كبيرة؟** | أعد استخدام نسخة واحدة من `OcrEngine` وعالج الصور تسلسليًا أو باستخدام مجموعة خيوط. المحرك آمن للقراءة المتعددة. |

---

## الخطوات التالية والمواضيع ذات الصلة

- **استخراج النص من الصورة** في ملفات PDF – دمج Aspose PDF مع OCR للمستندات الممسوحة.
- **معالجة دفعات** – استخدم `ExecutorService` في Java لتوازي معالجة آلاف ملفات PNG.
- **معالجة لاحقة** – تطبيق التدقيق الإملائي أو التجزئة الخاصة باللغة بعد الاستخراج.
- **التكامل مع التخزين السحابي** – قراءة PNG مباشرة من AWS S3 أو Azure Blob Storage باستخدام التدفقات.

لا تتردد في التجربة: جرّب إضافة `setDetectOrientation(true)` إذا كان لديك مسحات مائلة، أو غيّر قائمة اللغات المرشحة لتشمل اليابانية (`"ja"`) أو العربية (`"ar"`). الـ API مرن بما يكفي لمعظم المشاريع التي تركز على OCR.

---

## الخلاصة

أصبح لديك الآن مثال شامل من البداية للنهاية يوضح كيفية **التعرف على النص من PNG** باستخدام Aspose OCR، **استخراج النص من الصورة**، و**تمكين الكشف التلقائي عن اللغة** للمحتوى متعدد اللغات. الكود كامل، والشروحات تغطي “كيف” و “لماذا”، وقد رأيت المخرجات المتوقعة لتتمكن من التحقق من عمل كل شيء على جهازك.

هل لديك حالة استخدام مختلفة؟ اترك تعليقًا، شارك نتائجك، أو استكشف الخطوات التالية أعلاه. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
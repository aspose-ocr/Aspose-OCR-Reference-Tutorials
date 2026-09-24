---
category: general
date: 2026-02-09
description: تعلم كيفية التعرف على النص من الصورة باستخدام Aspose OCR في Java. يغطي
  هذا الدليل خطوة بخطوة أيضًا التدقيق الإملائي والقواميس المخصصة وتكوين محرك OCR.
draft: false
keywords:
- recognize text from image
- Aspose OCR Java
- OCR spell checking
- custom OCR dictionary
- Java image processing
language: ar
og_description: التعرف على النص من الصورة في جافا باستخدام Aspose OCR. اتبع هذا الدليل
  لتمكين التدقيق الإملائي، وتحديد اللغة، والحصول على النتيجة المصححة فورًا.
og_title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل Java الكامل
tags:
- OCR
- Java
- Aspose
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل Java الكامل
url: /ar/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة – دليل جافا كامل

هل احتجت يوماً إلى **التعرف على النص من الصورة** لكن لم تكن متأكدًا أي API تثق به؟ لست وحدك. في العديد من المشاريع—مسح الفواتير، تحويل الملاحظات المكتوبة بخط اليد إلى نص رقمي، أو بناء أرشيف قابل للبحث—القدرة على استخراج نص نظيف وقابل للقراءة من صورة تُعد تغييرًا جذريًا.

الخبر السار؟ باستخدام Aspose OCR for Java يمكنك فعل ذلك ببضع أسطر فقط، وستحصل أيضًا على تدقيق إملائي مدمج لتنظيف مخرجات OCR. في هذا الدرس سنستعرض العملية بالكامل، من إنشاء محرك OCR إلى طباعة النتيجة المصححة. في النهاية ستحصل على فئة جافا جاهزة للتنفيذ **تتعرف على النص من الصورة** بشكل موثوق.

---

## ما ستحتاجه

- **Java 8+** (الكود يعمل مع أي JDK حديث)
- مكتبة **Aspose OCR for Java** – يمكنك الحصول على أحدث JAR من مستودع Aspose Maven أو تنزيله مباشرة من موقع Aspose.
- ملف صورة يحتوي على نص مطبوع أو مكتوب (مثال: `typed_scanned_doc.png`).
- كمية معتدلة من الذاكرة RAM؛ OCR ليس ثقيلًا، لكن كومة بحجم 1 GB تكفي لمعظم المسحات.

> *نصيحة احترافية:* إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

الآن بعد أن انتهينا من المتطلبات المسبقة، دعنا نغوص في الكود.

---

## الخطوة 1: تهيئة محرك OCR والحصول على تكوينه

أول ما تقوم به هو إنشاء كائن `OcrEngine`. هذا الكائن هو قلب المكتبة؛ فهو يحمل جميع الإعدادات التي ستضبطها لاحقًا.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

لماذا هذا مهم: كائن التكوين يمنحك وصولًا مباشرًا إلى اختيار اللغة، وعلامات تدقيق الإملاء، ومسارات القواميس. بدون ذلك ستعتمد على الإعدادات الافتراضية التي قد لا تتطابق مع مادة المصدر الخاصة بك.

---

## الخطوة 2: اختيار اللغة وتفعيل تدقيق الإملاء

بعد ذلك، أخبر المحرك باللغة المتوقعة في الصورة. هنا نختار الإنجليزية، لكن Aspose يدعم عشرات اللغات.

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

تفعيل تدقيق الإملاء اختياري، لكنه يحسن بشكل كبير من قابلية قراءة المخرجات—خاصةً في المستندات الممسوحة حيث قد يخطئ محرك OCR في تفسير “0” كـ “O”.

---

## الخطوة 3: (اختياري) تحميل قاموس تدقيق إملائي مخصص

إذا كنت تتعامل مع مصطلحات متخصصة—مثل المصطلحات الطبية، الاختصارات القانونية، أو رموز المنتجات الخاصة—يسمح لك Aspose بدمج قاموسك الخاص.

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

يمكنك أيضًا توجيه `setSpellCheckDictionary` إلى ملف `.dic` كامل المسار إذا كان لديك قائمة مخصصة. سيقوم المحرك بدمج كلماتك المخصصة مع القاموس المدمج، مما يضمن بقاء المفردات المتخصصة سليمة.

---

## الخطوة 4: تشغيل OCR على ملف الصورة الخاص بك

الآن يبدأ العمل الحقيقي. قدم مسار الصورة إلى المحرك ودعه يقوم بسحره.

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

خلف الكواليس، يطبق Aspose سلسلة من خطوات ما قبل المعالجة—إزالة الميل، التحويل إلى ثنائي، وتقسيم الأحرف—قبل تمرير بيانات البكسل إلى مُعرّف الشبكة العصبية. النتيجة تُغلف في كائن `RecognitionResult` يحتوي على النص الأصلي والنص المصحح.

---

## الخطوة 5: عرض النص المصحح

أخيرًا، اطبع السلسلة المنقحة إلى وحدة التحكم. سترى مخرجات OCR **مع تطبيق تدقيق الإملاء**، والتي غالبًا ما تكون جاهزة للتخزين مباشرة في قاعدة بيانات أو إدخالها في فهرس بحث.

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

### النتيجة المتوقعة

بافتراض أن `typed_scanned_doc.png` يحتوي على الجملة *“The quick brown fox jumps over the lazy dog.”*، ستظهر وحدة التحكم:

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

إذا كان المسح الأصلي يحتوي على بقعة حولّلت كلمة “quick” إلى “qu1ck”، فإن مدقق الإملاء سيصححها تلقائيًا إلى “quick”.

---

## التعامل مع الحالات الشائعة

### 1. الصور منخفضة الدقة

تنخفض دقة OCR بشكل حاد تحت 150 dpi. إذا كانت صورك منخفضة الدقة، فكر في تكبيرها أولًا (مثلاً باستخدام OpenCV) أو اطلب مسحًا بجودة أعلى.

### 2. مستندات متعددة اللغات

يمكن لـ Aspose OCR تبديل اللغات أثناء التشغيل، لكن يجب ضبط تعداد `Language` المناسب قبل كل استدعاء `recognize`. للصفحات المختلطة اللغات، قد تحتاج إلى تشغيل الصورة عبر المحرك مرتين—مرة لكل لغة—ثم دمج النتائج.

### 3. ملفات PDF الكبيرة أو TIFF متعددة الصفحات

إذا كنت بحاجة إلى **التعرف على النص من صورة** مدمجة في ملفات PDF، استخرج كل صفحة كصورة (باستخدام Aspose PDF أو مكتبة أخرى) ومررها بشكل منفرد إلى محرك OCR. المحرك لا يحتفظ بحالة، لذا يمكنك إعادة استخدام نفس كائن `OcrEngine` عبر الصفحات.

### 4. تخصيص حساسية التدقيق الإملائي

الحد الافتراضي لتدقيق الإملاء يناسب معظم النصوص الإنجليزية. للوثائق التقنية العالية يمكنك خفض الحساسية بتعديل `SpellCheckOptions` الداخلية—على الرغم من أن ذلك يتطلب الغوص في API المتقدم لـ Aspose، وهو خارج نطاق هذا الدليل للمبتدئين.

---

## مثال كامل جاهز (انسخ‑الصق)

فيما يلي الفئة الجافا الكاملة، جاهزة للترجمة والتنفيذ. استبدل `YOUR_DIRECTORY/typed_scanned_doc.png` بالمسار الفعلي لصورتك.

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

الترجمة باستخدام:

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

يجب أن ترى النص المصحح يُطبع على وحدة التحكم، مؤكدًا أنك نجحت في **التعرف على النص من الصورة** وتطبيق تدقيق الإملاء.

---

## الأسئلة المتكررة

**س: هل يدعم Aspose OCR التعرف على الخط اليدوي؟**  
ج: المكتبة مُحسّنة للنص المطبوع. التعرف على الخط اليدوي متاح في وحدة منفصلة (`aspose-ocr-handwriting`)، يمكن دمجها بنفس الطريقة.

**س: هل يمكنني معالجة الصور من عنوان URL بدلاً من ملف محلي؟**  
ج: نعم. قم بتحميل الصورة إلى ذاكرة مؤقتة (مثلاً باستخدام `java.net.URL`) ومرّر مصفوفة البايتات إلى `ocrEngine.recognize(InputStream)`.

**س: ماذا لو أردت استخراج مناطق محددة فقط من الصورة؟**  
ج: استخدم `ocrEngine.setRegion(Rectangle)` قبل استدعاء `recognize`. هذا يحدّ OCR على المستطيل المحدد، مما يوفر الوقت ويقلل الإيجابيات الزائفة.

---

## الخلاصة

لقد استعرضنا مثالًا كاملاً من البداية إلى النهاية لكيفية **التعرف على النص من الصورة** باستخدام Aspose OCR for Java. من خلال ضبط محرك OCR، وتفعيل تدقيق الإملاء، وتحميل قاموس مخصص إذا لزم الأمر، يمكنك تحويل المسحات الضوضائية إلى نص نظيف وقابل للبحث بأقل قدر من الشيفرة.

من هنا يمكنك استكشاف:

- **المعالجة الدفعية** – تكرار عبر مجلد من الصور وتخزين كل نتيجة في قاعدة بيانات.  
- **التكامل مع Aspose PDF** – استخراج الصور من ملفات PDF وتمريرها إلى محرك OCR.  
- **دعم لغات متقدمة** – تغيير `ocrConfig.setLanguage` إلى `Language.FRENCH` أو `Language.SPANISH` للمشاريع متعددة اللغات.  

جرّبه، عدّل الإعدادات، ولاحظ كيف تتحسن الجودة لحالتك الخاصة. برمجة سعيدة، ولتكن مسحاتك دائمًا واضحة!

![مخطط يوضح سير عمل OCR للتعرف على النص من الصورة](/images/ocr-workflow.png "سير عمل التعرف على النص من الصورة")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
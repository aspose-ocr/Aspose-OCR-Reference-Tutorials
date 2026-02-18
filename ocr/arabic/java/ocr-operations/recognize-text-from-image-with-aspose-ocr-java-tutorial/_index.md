---
category: general
date: 2026-02-17
description: تعلم كيفية التعرف على النص من الصورة وتحميل الصورة للتعرف الضوئي على
  الأحرف باستخدام مكتبة Aspose OCR للغة Java. دليل خطوة بخطوة مع مصحح إملائي.
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR Java. يوضح هذا الدرس
  كيفية تحميل الصورة للتعرف الضوئي على الحروف، وتمكين تصحيح الإملاء، وإخراج نص نظيف.
og_title: التعرف على النص من الصورة – دليل Aspose OCR الكامل لجافا
tags:
- Java
- OCR
- Aspose
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل Java
url: /ar/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة باستخدام Aspose OCR – دليل Java

هل احتجت يوماً إلى **التعرف على النص من صورة** لكن لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك. في العديد من المشاريع الواقعية—مثل مسح الفواتير، رقمنة الملاحظات المكتوبة يدويًا، أو استخراج العناوين من لقطات الشاشة—يكون الحصول على نتائج OCR دقيقة أمرًا حاسمًا.  

في هذا الدليل سنستعرض تحميل صورة للـ OCR، تشغيل مصحح الأخطاء الإملائية المدمج في Aspose OCR، وأخيرًا طباعة النص المنقح. بنهاية الشرح ستحصل على برنامج Java جاهز للتنفيذ **يتعرف على النص من صورة** ببضع أسطر من الشيفرة.

## ما يغطيه هذا الدرس

- كيفية تطبيق رخصة Aspose OCR (لتشغيل العرض التجريبي بدون علامات مائية)  
- إنشاء كائن `OcrEngine` واختيار اللغة الإنجليزية كلغة للتعرف  
- **تحميل صورة للـ OCR** باستخدام `OcrInput` وتوجيهه إلى ملف PNG يحتوي على كلمات مكتوبة خطأً  
- تفعيل مصحح الأخطاء الإملائية، مع إمكانية توجيهه إلى قاموس مخصص  
- تشغيل عملية التعرف وطباعة النتيجة المصححة  

لا توجد خدمات خارجية، ولا ملفات إعداد مخفية—فقط Java صافية وملف JAR الخاص بـ Aspose OCR.

> **نصيحة محترف:** إذا كنت جديدًا على Aspose، احصل على رخصة تجريبية مجانية لمدة 30 يومًا من موقع Aspose وضع ملف `.lic` في مجلد يمكنك الإشارة إليه من الشيفرة.

## المتطلبات المسبقة

- Java 8 أو أحدث (الشيفرة تُجمّع أيضًا مع JDK 11)  
- ملف JAR الخاص بـ Aspose.OCR for Java في مسار الـ classpath  
- ملف رخصة صالح `Aspose.OCR.lic` (أو يمكنك التشغيل في وضع التقييم، لكن العرض التجريبي سيضيف علامة مائية)  
- ملف صورة (`misspelled.png`) يحتوي على نص مع أخطاء إملائية متعمدة—مثالي لرؤية مصحح الأخطاء يعمل  

هل لديك كل ذلك؟ رائع—لنبدأ.

## الخطوة 1: تطبيق رخصة Aspose OCR الخاصة بك

قبل أن يبدأ المحرك بأي معالجة، يجب أن يعرف أنك مرخص. وإلا ستحصل على شريط “Trial version” في الناتج.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*لماذا هذا مهم:* الترخيص يزيل العلامة المائية التجريبية ويفتح القاموس الكامل لمصحح الأخطاء. تخطي هذه الخطوة يعمل، لكن سيظهر في الناتج نص “Aspose OCR Demo”.

## الخطوة 2: إنشاء وتكوين محرك OCR

الآن نقوم بتشغيل المحرك ونخبره أي لغة نريد استخدامها. الإنجليزية هي الأكثر شيوعًا، لكن Aspose يدعم عشرات اللغات.

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*لماذا نحدد اللغة:* نموذج اللغة يحدد مجموعة الأحرف ويؤثر على اقتراحات مصحح الأخطاء. استخدام لغة خاطئة قد يقلل الدقة بشكل كبير.

## الخطوة 3: تفعيل تصحيح الإملاء و(اختياريًا) توجيه إلى قاموس مخصص

يأتي Aspose OCR مع قاموس إنجليزي مدمج، لكن يمكنك توفير قاموسك الخاص إذا كان لديك مصطلحات متخصصة (مثل المصطلحات الطبية أو رموز المنتجات).

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*ما يفعله المصحح:* عندما يكتشف محرك OCR كلمة غير موجودة في القاموس، يحاول استبدالها بأقرب تطابق. لهذا السبب يستطيع العرض التجريبي تحويل “recieve” إلى “receive” تلقائيًا.

## الخطوة 4: تحميل الصورة للـ OCR

هذا هو الجزء الذي يجيب مباشرة على **تحميل صورة للـ OCR**. ننشئ كائن `OcrInput` ونضيف ملف PNG الخاص بنا.

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*لماذا نستخدم `OcrInput`*: فهو يج abstracts منطق قراءة الملفات ويسمح لك بإضافة صفحات متعددة لاحقًا إذا احتجت معالجة PDF متعدد الصفحات أو مجموعة من الصور.

## الخطوة 5: تشغيل التعرف واسترجاع النص المصحح

الآن يقوم المحرك بالعمل الشاق—التعرف على الأحرف، تطبيق نموذج اللغة، وأخيرًا تصحيح الإملاء.

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*الناتج المتوقع:* بافتراض أن `misspelled.png` يحتوي على العبارة “Ths is a smple test”، سيطبع الطرفية:

```
Corrected text:
This is a simple test
```

لاحظ كيف تم تصحيح الكلمات الخاطئة (`Ths`, `smple`) تلقائيًا.

## مثال كامل جاهز للتنفيذ

فيما يلي البرنامج بالكامل في كتلة واحدة. انسخه، عدل المسارات، ثم اضغط **Run**.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**نصيحة:** إذا أردت معالجة JPEG أو BMP بدلاً من PNG، فقط غير امتداد الملف—Aspose OCR يدعم جميع صيغ الرسوم النقطية الشائعة.

## أسئلة شائعة وحالات خاصة

- **ماذا لو كانت صورتي منخفضة الدقة؟**  
  زد الـ DPI قبل تمريرها إلى Aspose عبر إعادة التحجيم باستخدام مكتبة مثل `java.awt.Image`. DPI أعلى يمنح المحرك المزيد من البكسلات للعمل عليها، مما يحسن الدقة عادةً.

- **هل يمكنني التعرف على لغات متعددة في نفس الصورة؟**  
  نعم. استدعِ `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` ويمكنك إضافة قائمة لغات عبر `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);`.

- **القاموس المخصص لا يُستخدم—لماذا؟**  
  تأكد أن المجلد يحتوي على ملفات نصية عادية كلمة واحدة في كل سطر، وأن المسار إما مطلق أو نسبي بشكل صحيح إلى دليل العمل الخاص بك.

- **كيف أستخرج درجات الثقة؟**  
  `result.getConfidence()` يعيد قيمة عائمة بين 0 و 1 للصفحة بأكملها. للحصول على الثقة لكل حرف، استكشف `result.getWordList()`.

## الخلاصة

أنت الآن تعرف كيف **تتعرف على النص من صورة** باستخدام Aspose OCR for Java، وكيف **تحمل صورة للـ OCR**، وكيفية تفعيل مصحح الأخطاء لتنقية الأخطاء الشائعة. المثال الكامل أعلاه جاهز للإدراج في أي مشروع Maven أو Gradle، ومع بعض التعديلات يمكنك توسيعه لمعالجة دفعات من المجلدات، ربطه بخدمة ويب، أو دمجه مع نظام إدارة مستندات.

هل أنت مستعد للخطوة التالية؟ جرّب معالجة PDF متعدد الصفحات، جرب قاموسًا مخصصًا لمصطلحات صناعية، أو اربط الناتج بواجهة برمجة تطبيقات ترجمة. الاحتمالات لا حصر لها، والنمط الأساسي—رخصة → محرك → لغة → مصحح إملائي → إدخال → التعرف → إخراج—يبقى هو نفسه.

برمجة سعيدة، ولتكن نتائج OCR دائمًا دقيقة! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
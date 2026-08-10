---
category: general
date: 2026-06-19
description: التعرف على النص من الصورة باستخدام Aspose OCR في جافا. تعلم كيفية تمكين
  التدقيق الإملائي، إضافة القاموس، وإجراء OCR مع التدقيق الإملائي في دليل واحد.
draft: false
keywords:
- recognize text from image
- how to enable spellcheck
- how to add dictionary
- ocr with spell check
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspense OCR في جافا. يوضح هذا الدليل
  كيفية تمكين التدقيق الإملائي، إضافة القاموس، وتشغيل OCR مع التدقيق الإملائي.
og_title: التعرف على النص من الصورة – دليل تدقيق إملائي باستخدام Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  headline: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  type: TechArticle
- description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  name: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  steps:
  - name: How to Enable SpellCheck
    text: 'The spell checker lives inside the engine, but it’s disabled by default.
      Flip the switch with a single line:'
  - name: Expected Output
    text: 'Assuming `receipt.png` contains the line “Totel: $12.99” and your custom
      dictionary includes “Total”, the console will display:'
  - name: What if I need multiple languages?
    text: You can call `ocrEngine.setLanguage(Language.English, Language.French)`
      to enable multilingual recognition. Spell‑checking will follow each language’s
      rules, but you still need to enable it with `setEnable(true)`.
  - name: How does the engine handle unknown words?
    text: If a word isn’t in the internal dictionary *and* not in your custom dictionary,
      the spell checker attempts a best‑guess correction based on Levenshtein distance.
      For truly unknown terms, add them to `my-terms.txt`.
  - name: Does the spell checker work on numbers?
    text: By default, numeric strings are left untouched. If you have alphanumeric
      codes (e.g., “AB12C”), add them to your custom dictionary; otherwise the engine
      may try to “fix” them to real words.
  - name: Performance considerations
    text: Enabling spell checking adds a modest overhead—roughly 10‑15 % extra CPU
      per page. For batch processing, consider disabling it on the first pass, then
      re‑run only on pages that failed quality checks.
  type: HowTo
tags:
- OCR
- Java
- SpellCheck
title: التعرف على النص من الصورة في جافا – دليل شامل لتدقيق الإملاء باستخدام Aspose
  OCR
url: /ar/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-aspose-ocr-spell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة في جافا – دليل كامل لتصحيح إملائي باستخدام Aspose OCR

هل احتجت يوماً إلى **التعرف على النص من الصورة** لكنك كنت قلقاً من أن يكون الناتج مليئاً بالأخطاء الإملائية؟ لست وحدك. في العديد من مشاريع مسح الفواتير أو رقمنة المستندات يبدو النص الخام الناتج عن OCR كأنه كتبته قطة نائمة. الخبر السار؟ باستخدام Aspose OCR يمكنك تحويل هذا الفوضى إلى نص نظيف ومصحح إملائياً — مباشرة داخل جافا.

في هذا الدرس سنستعرض مثالاً جاهزاً للتنفيذ يوضح **كيفية تمكين التصحيح الإملائي**، **كيفية إضافة مدخلات القاموس** للمصطلحات الخاصة بالمجال، وفي النهاية **كيفية إجراء OCR مع تصحيح إملائي**. بنهاية الدرس ستحصل على برنامج مستقل يقرأ ملف صورة، يصحح الإملاء أثناء التشغيل، ويطبع النتيجة المصقولة.

## ما ستتعلمه

- كيفية تطبيق ترخيص Aspose OCR بحيث يعمل الـ API بأقصى سرعة.  
- الخطوات الدقيقة **لتمكين التصحيح الإملائي** على محرك OCR.  
- الطريقة الصحيحة **لإضافة قاموس مخصص** لكلمات مثل رموز المنتجات أو أسماء العلامات التجارية.  
- كيفية استدعاء `recognizeImage` والحصول على نص نظيف ومصحح.  

بدون أدوات خارجية، بدون مكتبات تصحيح إملائي يدوية — فقط جافا صافية وAspose OCR.

## المتطلبات المسبقة

- Java 8+ (الكود يتوافق مع أي JDK حديث).  
- ملف ترخيص Aspose OCR (`Aspose.OCR.lic`). إذا كنت تختبر فقط، النسخة التجريبية المجانية تعمل لكن ستضيف علامة مائية.  
- Maven أو Gradle لجلب تبعية `aspose-ocr`، أو يمكنك إضافة ملفات JAR يدوياً.  
- صورة نموذجية (مثلاً، صورة فاتورة بصيغة PNG) وملف نصي يحتوي على المصطلحات المخصصة.

> **نصيحة احترافية:** احفظ القاموس المخصص بترميز UTF‑8 وسطر واحد لكل مصطلح — Aspose OCR يقرأه مباشرة من نظام الملفات.

---

## الخطوة 1: إعداد المشروع وإضافة تبعية Aspose OCR

إذا كنت تستخدم Maven، أضف المقتطف التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.8</version> <!-- use the latest version -->
</dependency>
```

لـ Gradle، الفكرة نفسها:

```groovy
implementation 'com.aspose:aspose-ocr:23.8'
```

بعد حل التبعية، أنشئ فئة جافا جديدة تسمى `SpellCheckDemo`. هنا يحدث السحر.

## الخطوة 2: تطبيق ترخيص Aspose OCR

قبل أي عملية OCR، يجب إخبار Aspose بأنه مسموح له بالعمل بدون قيود. تخطي هذه الخطوة يسبب استثناءً أثناء التشغيل.

```java
// Apply the Aspose OCR license – this removes evaluation watermarks
License license = new License();
license.setLicense("Aspose.OCR.lic");   // path to your .lic file
```

> **لماذا هذا مهم:** الترخيص يفتح محرك OCR بالكامل، بما في ذلك وحدة التصحيح الإملائي المدمجة. بدون الترخيص، يظل المحرك يعمل لكنه سيرفض استخدام بعض الميزات المتميزة.

## الخطوة 3: إنشاء وتكوين محرك OCR

الآن نقوم بإنشاء كائن `OcrEngine` الأساسي ونحدد اللغة إلى الإنجليزية. هذا هو الأساس لكل من التعرف والتصحيح الإملائي.

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.setLanguage(Language.English);   // choose the language that matches your image
```

### كيفية تمكين التصحيح الإملائي

المصحح الإملائي موجود داخل المحرك، لكنه معطل بشكل افتراضي. فعّل المفتاح بسطر واحد:

```java
ocrEngine.getSpellChecker().setEnable(true);   // enables spell‑checking
```

هذا السطر يلبي متطلب **كيفية تمكين التصحيح الإملائي**. بمجرد التفعيل، سيقارن المحرك كل كلمة مُعترف بها مع القاموس الداخلي ويقترح تصحيحات تلقائيًا.

## الخطوة 4: تحميل قاموس مخصص (كيفية إضافة القاموس)

إذا كانت مستنداتك تحتوي على مصطلحات خاصة — مثل رموز المنتجات، المصطلحات الطبية، أو أسماء العلامات التجارية — ستحتاج إلى تعليم المصحح الإملائي عنها. يتيح لك Aspose OCR الإشارة إلى ملف نصي عادي، سطر واحد لكل كلمة.

```java
// Load a custom word list for spell‑checking
Path customDict = java.nio.file.Paths.get("YOUR_DIRECTORY/my-terms.txt");
ocrEngine.getSpellChecker().addUserDictionary(customDict);
```

> **ماذا لو لم يُعثر على الملف؟** الـ API يرمي استثناءً من نوع `FileNotFoundException`. احwrap الاستدعاء داخل `try/catch` إذا أردت معالجة الأخطاء برفق.

الآن يعرف المحرك كلمات مثل “AcmeWidget” أو “RX‑9000” ولن يعتبرها أخطاء إملائية.

## الخطوة 5: التعرف على النص من الصورة

بعد تجهيز المحرك، يمكنك أخيرًا **التعرف على النص من الصورة**. الطريقة `recognizeImage` تُعيد كائن `OcrResult` يحتوي على النص الخام والنص المصحح.

```java
// Recognize text from the image file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png");
```

نظرًا لأننا فعلنا التصحيح الإملائي مسبقًا، فإن استدعاء `getText()` يُعيد النسخة المصححة مباشرة.

## الخطوة 6: إخراج النص المصحح

كل ما تبقى هو طباعة (أو تخزين) السلسلة المنقحة.

```java
// Output the corrected, spell‑checked text
System.out.println(ocrResult.getText());
```

عند تشغيل البرنامج، يجب أن ترى فاتورة منسقة بشكل جميل مع إملاء صحيح، حتى وإن كانت الصورة الأصلية تحتوي على أحرف مشوشة.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه‑الصقه في بيئة التطوير الخاصة بك، عدل مسارات الملفات، ثم اضغط **Run**.

```java
import com.aspose.ocr.*;

import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCheckDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");   // <-- replace with your license path

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.English);

        // Step 3: Load a custom word list for spell‑checking
        Path dictPath = Paths.get("YOUR_DIRECTORY/my-terms.txt"); // <-- your dictionary file
        ocrEngine.getSpellChecker().addUserDictionary(dictPath);
        ocrEngine.getSpellChecker().setEnable(true); // <-- how to enable spellcheck

        // Step 4: Recognize text from the image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png"); // <-- your image

        // Step 5: Output the corrected text
        System.out.println(ocrResult.getText());
    }
}
```

### النتيجة المتوقعة

افترض أن `receipt.png` يحتوي على السطر “Totel: $12.99” وأن القاموس المخصص يتضمن كلمة “Total”، سيظهر في وحدة التحكم:

```
Total: $12.99
```

تم تصحيح الخطأ الإملائي “Totel” تلقائيًا بفضل **OCR مع تصحيح إملائي**.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى لغات متعددة؟

يمكنك استدعاء `ocrEngine.setLanguage(Language.English, Language.French)` لتمكين التعرف متعدد اللغات. سيُطبق التصحيح الإملائي قواعد كل لغة، لكن لا يزال عليك تفعيله باستخدام `setEnable(true)`.

### كيف يتعامل المحرك مع الكلمات غير المعروفة؟

إذا لم تكن الكلمة موجودة في القاموس الداخلي *ولا* في القاموس المخصص، يحاول المصحح الإملائي اقتراح تصحيح بناءً على مسافة Levenshtein. بالنسبة للمصطلحات غير المعروفة تمامًا، أضفها إلى `my-terms.txt`.

### هل يعمل المصحح الإملائي على الأرقام؟

افتراضيًا، تُترك السلاسل الرقمية دون تعديل. إذا كان لديك رموز مختلطة (مثلاً “AB12C”) أضفها إلى القاموس المخصص؛ وإلا قد يحاول المحرك “إصلاحها” إلى كلمات حقيقية.

### اعتبارات الأداء

تفعيل التصحيح الإملائي يضيف عبئًا بسيطًا — حوالي 10‑15 % من استهلاك المعالج لكل صفحة. للمعالجة الدفعية، فكر في تعطيله في المرور الأول، ثم أعد تشغيله فقط على الصفحات التي فشلت في فحص الجودة.

---

## ملخص

غطينا كل ما تحتاجه **للتعرف على النص من الصورة** باستخدام Aspose OCR في جافا مع الحفاظ على نظافة الإخراج. الخطوات كانت:

1. تطبيق الترخيص.  
2. إنشاء `OcrEngine` وتحديد اللغة.  
3. **كيفية إضافة القاموس** – تحميل قائمة كلمات مخصصة.  
4. **كيفية تمكين التصحيح الإملائي** – تفعيل الميكانيزم.  
5. تشغيل `recognizeImage` (النداء الأساسي لـ **OCR مع تصحيح إملائي**).  
6. طباعة النص المصحح.

بهذا تكون قد أنجزت كامل خط الأنابيب — من البكسلات الخام إلى سلاسل نصية مصقولة ومصححة إملائيًا.

---

## ما التالي؟

- **المعالجة الدفعية:** تكرار عبر مجلد من الصور وكتابة كل نتيجة إلى ملف `.txt` منفصل.  
- **إخراج PDF:** استخدم Aspose PDF لدمج النص المصحح داخل PDF قابل للبحث.  
- **قواميس متقدمة:** حمّل قواميس مستخدم متعددة لمجالات مختلفة (مثلاً المالية مقابل الطبية).  
- **درجات الثقة:** تفحص `ocrResult.getConfidence()` لتصفية النتائج ذات عدم اليقين العالي.

لا تتردد في التجربة — غيّر اللغة، عدّل القاموس، أو اجمع هذا مع مكتبات ما قبل معالجة الصور للحصول على دقة أعلى.

إذا واجهت أي صعوبات، اترك تعليقًا أدناه. برمجة سعيدة، ولتكن OCR دائمًا مصححة إملائيًا!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
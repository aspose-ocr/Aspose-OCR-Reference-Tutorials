---
category: general
date: 2026-06-16
description: التعرف على النص من الصورة باستخدام Java OCR. تعلم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، واكتشاف اللغات في الصورة، وتمكين الكشف التلقائي عن اللغة
  في بضع خطوات.
draft: false
keywords:
- recognize text from image
- load image for OCR
- detect languages in image
- enable auto language detection
language: ar
og_description: التعرف على النص من الصورة بسرعة. يوضح هذا الدرس كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، واكتشاف اللغات في الصورة، وتمكين الكشف التلقائي عن اللغة
  باستخدام جافا.
og_title: التعرف على النص من الصورة باستخدام Java OCR – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using Java OCR. Learn how to load image for
    OCR, detect languages in image, and enable auto language detection in a few steps.
  headline: recognize text from image with Java OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Java
- Image Processing
- Multilingual OCR
title: التعرف على النص من الصورة باستخدام Java OCR – دليل كامل
url: /ar/java/ocr-operations/recognize-text-from-image-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Java OCR – دليل كامل

هل احتجت يومًا إلى **التعرف على النص من الصورة** لكنك لم تكن متأكدًا أي واجهة برمجة تطبيقات Java ستتعامل مع الصور متعددة اللغات؟ لست وحدك—المطورون يواجهون باستمرار مسحًا متعدد اللغات، إيصالات، أو لافتات تتحدى إعداد لغة واحدة.  

في هذا الدرس سنرشدك خطوة بخطوة إلى تحميل صورة للـ OCR، تفعيل الكشف التلقائي عن اللغة، وأخيرًا استخراج النص المستخرج من النتيجة. في النهاية ستحصل على برنامج Java جاهز للتنفيذ **يكتشف اللغات في الصورة** ويطبع المحتوى المعترف به—بدون أي إعدادات إضافية.

> **ما ستحصل عليه:** فئة Java مستقلة، شروحات خطوة بخطوة، ونصائح للتعامل مع الحالات الخاصة مثل المسحات منخفضة الدقة أو النصوص غير المدعومة.

## المتطلبات المسبقة

- Java 8 أو أحدث مثبت (الكود يتوافق أيضًا مع JDK 11).  
- مكتبة OCR حديثة تدعم الكشف التلقائي عن اللغة—نستخدم هنا **Aspose.OCR for Java**، لكن أي مكتبة توفر إعدادات مشابهة ستعمل.  
- ملف صورة (`mixed_languages.png`) يحتوي على نص بأكثر من لغة.  
- إلمام أساسي بـ Maven أو Gradle لإدارة التبعيات (سنظهر مقتطف Maven).

إذا كان أي من هذه غير مألوف لك، لا تقلق؛ الخطوات أدناه تتضمن إحداثيات Maven الدقيقة وملف `pom.xml` بسيط يمكنك نسخه ولصقه وتشغيله فورًا.

## إعداد المشروع

أنشئ مشروع Maven جديد (أو أضف إلى مشروع موجود) وضمّن تبعية OCR:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Check for the latest version -->
    </dependency>
</dependencies>
```

شغّل `mvn clean compile` لجلب المكتبة. بمجرد الانتهاء، ستكون جاهزًا لكتابة الكود.

## الخطوة 1: استيراد الفئات المطلوبة

أولًا، نستورد الفئات التي سنحتاجها. تشمل محرك OCR، أدوات معالجة الصور، وحاويات النتائج.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ImageStream;
import com.aspose.ocr.OcrResult;
```

> **نصيحة احترافية:** حافظ على تنظيم الاستيرادات—اختصارات IDE (`Ctrl+Shift+O` في IntelliJ) يمكنها تنظيمها تلقائيًا.

## الخطوة 2: إنشاء كائن محرك OCR

المحرك هو قلب العملية. إنشاؤه يمنحنا الوصول إلى إعدادات مثل كشف اللغة.

```java
// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

لماذا نفصل إنشاء المحرك عن تحميل الصورة؟ ذلك يسمح لك بإعادة استخدام نفس المحرك لعدة صور دون إعادة تهيئة الموارد الثقيلة، ما يوفر أداءً أفضل في سيناريوهات الدفعات.

## الخطوة 3: تحميل الصورة للـ OCR

الآن نقوم فعليًا **بتحميل الصورة للـ OCR**. طريقة `ImageStream.fromFile` تقرأ الملف إلى تدفق يمكن للمحرك استهلاكه.

```java
// Step 3: Load the image that contains mixed languages
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed_languages.png"));
```

استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي حيث توجد صورة الاختبار الخاصة بك. إذا كان المسار خاطئًا، ستظهر لك استثناء `FileNotFoundException`—وهو خطأ شائع للمبتدئين.

> **نصيحة صورة:** للحصول على أفضل النتائج، استخدم صيغ PNG أو TIFF؛ ضغط JPEG قد يضيف تشويهات تُربك المُعرّف.

## الخطوة 4: تفعيل الكشف التلقائي عن اللغة

هذه هي جوهر الدرس: **تفعيل الكشف التلقائي عن اللغة** بحيث يقرر المحرك أي نماذج لغة يُطبقها أثناء التشغيل.

```java
// Step 4: Turn on automatic language detection
engine.getRecognitionSettings().setAutoDetectLanguage(true);
```

عندما تكون هذه العلامة `true`، يقوم محرك OCR بمسح الصورة، تحديد اللغات الموجودة، وتحميل حزم اللغة المناسبة داخليًا. إذا تخطيت هذه الخطوة، سيفترض المحرك اللغة الأساسية (عادةً الإنجليزية)، وستفقد النصوص بالخطوط الأخرى.

## الخطوة 5: تنفيذ التعرف على OCR

بعد ضبط كل شيء، ن finally **نتعرف على النص من الصورة** ونستخرج كلًا من قائمة اللغات المكتشفة والنص المستخرج.

```java
// Step 5: Run the recognition process
OcrResult result = engine.recognize();

// Display detected languages and the extracted text
System.out.println("Detected languages: " + result.getDetectedLanguages());
System.out.println("Extracted text:\n" + result.getText());
```

طريقة `getDetectedLanguages()` تُعيد مجموعة مثل `[en, fr, de]`، مما يتيح لك التحقق من أن المحرك حدد المحتوى متعدد اللغات بشكل صحيح.

## مثال كامل يعمل

فيما يلي الفئة Java الكاملة والقابلة للتنفيذ. انسخها إلى `src/main/java/com/example/OcrDemo.java`، عدّل مسار الصورة، ثم نفّذ `mvn exec:java -Dexec.mainClass="com.example.OcrDemo"`.

```java
package com.example;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ImageStream;
import com.aspose.ocr.OcrResult;

/**
 * Demo program that recognises text from an image,
 * automatically detects languages present, and prints the result.
 */
public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load image for OCR – change the path as needed
        String imagePath = "YOUR_DIRECTORY/mixed_languages.png";
        engine.setImage(ImageStream.fromFile(imagePath));

        // 3️⃣ Enable auto language detection so we can detect languages in image
        engine.getRecognitionSettings().setAutoDetectLanguage(true);

        // 4️⃣ Perform the recognition
        OcrResult result = engine.recognize();

        // 5️⃣ Output the findings
        System.out.println("Detected languages: " + result.getDetectedLanguages());
        System.out.println("Extracted text:\n" + result.getText());
    }
}
```

**الناتج المتوقع** (قد تختلف اللغات الفعلية):

```
Detected languages: [en, es, fr]
Extracted text:
Hello World!
¡Hola Mundo!
Bonjour le monde!
```

إذا كانت الصورة تحتوي على الإنجليزية فقط، ستظهر القائمة `[en]` وسيعكس النص تلك اللغة الوحيدة.

## معالجة الحالات الشائعة

| الحالة | لماذا يهم | الحل السريع |
|-----------|----------------|-----------|
| صورة منخفضة الدقة | قد يخطئ المحرك في اكتشاف الأحرف، مما يؤدي إلى مخرجات مشوشة. | عالج الصورة مسبقًا (زيادة DPI، تطبيق التث_bin_ation) قبل تمريرها إلى OCR. |
| نص غير مدعوم (مثل البنغالية) | سيُهمل الكشف التلقائي النصوص غير المعروفة، فيُعيد نصًا فارغًا لتلك الجزء. | أضف حزمة اللغة يدويًا إذا كانت المكتبة تدعمها، أو استخدم محرك OCR آخر. |
| دفعة كبيرة من الصور | إنشاء محرك جديد في كل مرة يضيف عبئًا. | أعد استخدام كائن `OcrEngine` واحد فقط واستدعِ `setImage` لكل ملف جديد. |
| بيئة ذات ذاكرة محدودة | تحميل العديد من الصور عالية الدقة قد يستهلك مساحة الذاكرة. | استخدم `ImageStream.fromFile` مع خيارات البث أو قلل أبعاد الصور أثناء التشغيل. |

## نصائح احترافية وأفضل الممارسات

- **تخزين حزم اللغة مؤقتًا**: بعض مكتبات OCR تسمح بتحميل بيانات اللغة مسبقًا. ذلك يقلل زمن الاستجابة عند معالجة ملفات متعددة.  
- **سجّل اللغات المكتشفة**: حفظ قائمة اللغات جنبًا إلى جنب مع النص المستخرج يساعد في التحليلات اللاحقة (مثل تحليل المشاعر حسب اللغة).  
- **تحقق من صحة المخرجات**: فحص regex بسيط لمجموعات الأحرف المتوقعة يمكنه اكتشاف فشل OCR مبكرًا في خط الأنابيب.  

## الخطوات التالية

الآن بعد أن أصبحت قادرًا على **التعرف على النص من الصورة** مع الكشف التلقائي عن اللغة، فكر في توسيع الحل:

- **تصدير إلى PDF**: غلف النص المستخرج في PDF قابل للبحث باستخدام iText أو Apache PDFBox.  
- **دمجه مع قاعدة بيانات**: احفظ مسار الصورة، اللغات المكتشفة، ونص OCR للاسترجاع لاحقًا.  
- **إضافة واجهة مستخدم**: أنشئ واجهة خفيفة باستخدام Swing أو JavaFX بحيث يتمكن المستخدمون غير التقنيين من سحب الصور والحصول على النتائج فورًا.  

كل هذه المواضيع ترتبط بكلماتنا المفتاحية الثانوية—**load image for OCR**, **detect languages in image**, و **enable auto language detection**—وبالتالي ستستمر في البناء على نفس الأساس.

---

*برمجة سعيدة! إذا واجهت أي مشكلة، اترك تعليقًا أدناه وسنساعدك على حلها معًا.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استخراج نص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [التعرف على نص الصورة باستخدام Aspose OCR – دليل Java OCR كامل](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
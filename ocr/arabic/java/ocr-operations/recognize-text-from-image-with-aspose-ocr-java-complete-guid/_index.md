---
category: general
date: 2026-03-18
description: تعلم كيفية التعرف على النص من الصورة في جافا باستخدام Aspose OCR. يوضح
  هذا الدليل خطوة بخطوة كيفية تحميل الصورة للتعرف الضوئي على الأحرف وإيقاف تصحيح الإملاء.
draft: false
keywords:
- recognize text from image
- load image for ocr
- aspose ocr java example
- extract text from image
- turn off spell corrector
language: ar
og_description: التعرف على النص من الصورة في جافا باستخدام Aspose OCR. تعلم كيفية
  تحميل الصورة للتعرف الضوئي على الأحرف وإيقاف مصحح الإملاء في هذا الدرس العملي.
og_title: التعرف على النص من الصورة باستخدام Aspose OCR Java – دليل كامل
tags:
- Aspose OCR
- Java
- Image Processing
title: التعرف على النص من الصورة باستخدام Aspose OCR Java – دليل كامل
url: /ar/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Aspose OCR Java – دليل شامل

هل احتجت يومًا إلى **التعرف على النص من الصورة** لكن لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك. في العديد من المشاريع الواقعية—مثل مسح الإيصالات، رقمنة النماذج، أو استخراج التسميات التوضيحية من لقطات الشاشة—الحصول على نص نظيف من صورة نقطية هو مهمة يومية.  

في هذا الدرس سنستعرض مثالًا عمليًا **Aspose OCR Java** يوضح لك بالضبط كيف **تحمّل صورة للتعرف الضوئي على الأحرف (OCR)**، تشغيل المحرك، وحتى **إيقاف مصحح الإملاء** عندما تحتاج إلى الأحرف كما هي دون تعديل. في النهاية ستحصل على برنامج قابل للتنفيذ يستخرج النص من الصورة دون أي تعديلات غير مرغوبة.

## ما ستحصل عليه بعد الانتهاء

- صورة واضحة عن سير عمل **Aspose OCR** للغة Java.
- الشيفرة الدقيقة اللازمة **للتعرف على النص من الصورة** و**استخراج النص من الصورة** بصيغته الأصلية.
- نصائح حول متى قد ترغب في تعطيل مصحح الإملاء المدمج وكيفية القيام بذلك بأمان.
- فحص سريع يمكنك تشغيله للتحقق من أن المخرجات تتطابق مع توقعاتك.

### المتطلبات الأساسية (الحد الأدنى)

- Java 8 أو أحدث مثبتة على جهازك.
- Maven أو Gradle لإدارة الاعتمادات (سنظهر مقتطف Maven).
- ملف JAR الخاص بـ `Aspose.OCR` (يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose).
- ملف صورة (PNG، JPG، BMP، إلخ) يحتوي على النص الذي تريد قراءته. في المثال سنستخدم `mixed-lang.png`.

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة عدد كبير من الصور، فكر في تحميلها كـ streams لتجنب تسرب مقابض الملفات.

---

![Diagram showing OCR pipeline – recognize text from image](ocr-pipeline.png)

*نص بديل: مخطط يوضح خطوات التعرف على النص من الصورة باستخدام Aspose OCR.*

## الخطوة 1 – إعداد المشروع وإضافة اعتماد Aspose OCR

قبل أن نتمكن من استدعاء أي من طرق OCR، يجب أن تكون المكتبة موجودة في مسار الـ classpath. إذا كنت تستخدم Maven، أضف ما يلي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

إذا كنت تفضّل Gradle، فالمكافئ هو:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

بعد حل الاعتماد، يمكنك استيراد الصنفين الذين سنحتاجهما:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
```

> **لماذا هذا مهم:** إضافة الـ JAR عبر أداة بناء تضمن استخدام النسخة الصحيحة عبر جميع البيئات، مما يلغي مشاكل “class not found” لاحقًا.

## الخطوة 2 – إنشاء محرك OCR وإيقاف مصحح الإملاء

يأتي Aspose OCR مع مصحح إملائي مدمج يحاول تخمين ما كنت تقصده. هذا مفيد للمستندات النظيفة، لكن إذا كنت تمسح لافتات متعددة اللغات أو مقتطفات شفرة، ستحصل على “تصحيحات” غير مرغوبة. إليك طريقة تعطيله:

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Disable the automatic spell correction
ocrEngine.getSpellCorrector().setEnabled(false);
```

**ما الذي يحدث خلف الكواليس؟** كائن `SpellCorrector` يجري تمريرة قائمة على القاموس بعد فك تشفير الحروف الخام. باستدعاء `setEnabled(false)`، نخبر المحرك بتخطي تلك التمريرة، وبالتالي نحافظ على تسلسل الأحرف الذي تم اكتشافه بالضبط.

## الخطوة 3 – تحميل الصورة للتعرف الضوئي على الأحرف

الآن نقوم فعليًا **بتحميل الصورة للتعرف الضوئي على الأحرف**. طريقة `Image.load` في Aspose تقبل مسار ملف، أو `InputStream`، أو حتى مصفوفة بايت. للتبسيط سنستخدم مسار الملف:

```java
// Replace the path with the location of your image file
Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");
```

> **حالة حدية:** إذا كان حجم الصورة أكبر من 5 ميغابايت، فكر في تصغيرها أولًا. الصور الكبيرة تستهلك ذاكرة أكثر وقد تبطئ محرك التعرف.

## الخطوة 4 – التعرف على النص والتقاط النتيجة الخام

مع جاهزية المحرك والصورة في الذاكرة، يصبح التعرف عملية سطر واحد:

```java
// Perform OCR and store the raw text
String rawText = ocrEngine.recognize(inputImage);
```

طريقة `recognize` تُعيد `String` يحتوي على **استخراج النص من الصورة** تمامًا كما رآه المحرك—بدون تدقيق إملائي، بدون معالجة لاحقة.

## الخطوة 5 – عرض النتيجة (بدون تدقيق إملائي)

أخيرًا، لنطبع ناتج OCR الخام إلى وحدة التحكم حتى تتمكن من التحقق منه:

```java
System.out.println("Raw OCR (no spell‑check):\n" + rawText);
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
Raw OCR (no spell‑check):
Hello, 世界!
12345
```

إذا كانت الصورة تحتوي على لغات مختلطة أو رموز خاصة، فستظهر دون تغيير لأننا أوقفنا مصحح الإملاء.

## مثال كامل قابل للتنفيذ

بتجميع كل الأجزاء معًا، إليك **مثال Aspose OCR Java الكامل** الذي يمكنك نسخه ولصقه في ملف `SpellCorrectionDemo.java`:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;

public class SpellCorrectionDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn off the built‑in spell corrector
        ocrEngine.getSpellCorrector().setEnabled(false);

        // Step 3: Load the image you want to recognize
        Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");

        // Step 4: Run OCR on the image and obtain the raw text
        String rawText = ocrEngine.recognize(inputImage);

        // Step 5: Display the OCR result without spell‑checking
        System.out.println("Raw OCR (no spell‑check):\n" + rawText);
    }
}
```

### كيفية التشغيل

1. احفظ الملف باسم `SpellCorrectionDemo.java`.
2. قم بالترجمة: `javac -cp "path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo.java`
3. نفّذ: `java -cp ".;path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo`

استبدل `path/to` بالمسار الفعلي لملف الـ JAR الخاص بـ Aspose على نظامك.

## أسئلة شائعة ومشكلات محتملة

### ماذا لو كانت الصورة بصيغة مختلفة (مثل PDF)؟

يمكن لـ Aspose OCR أيضًا قراءة صفحات PDF مباشرة، لكن عليك أولًا تحويل صفحة PDF إلى صورة أو استخدام overload `OcrEngine.recognizePdf`. هذا موضوع درس آخر، لكن مبدأ **التعرف على النص من الصورة** يبقى نفسه.

### هل يؤثر إيقاف مصحح الإملاء على الأداء؟

قليلًا. تخطي تمريرة القاموس يوفر بضع مليثانية لكل صفحة، ما قد يتراكم عند معالجة آلاف الملفات. المقابل هو فقدان التصحيح التلقائي للأخطاء الإملائية—لذا قرر بناءً على جودة بياناتك.

### هل يمكنني الحصول على نتائج مخصصة للغة؟

نعم. المحرك يكتشف النص تلقائيًا، لكن يمكنك فرض لغة معينة باستدعاء `ocrEngine.setLanguage(OcrEngine.Language.English)`، على سبيل المثال. هذا مفيد عندما تعرف أن الصورة تحتوي على لغة واحدة فقط وتريد تحسين الدقة.

### كيف أتعامل مع ملفات TIFF متعددة الصفحات؟

عامل كل صفحة ككائن `Image` منفصل: `Image.load("file.tif", pageIndex)`. قم بالتكرار عبر الصفحات، تعرف على كل واحدة، ثم اجمع النتائج.

## نصائح احترافية للمشاريع الواقعية

- **المعالجة الدفعية:** غلف منطق OCR في دالة تقبل `InputStream`. هذا يتيح لك بث الصور من S3، Azure Blob، أو أي تخزين آخر دون الحاجة للوصول إلى نظام الملفات.
- **إدارة الذاكرة:** استدعِ `ocrEngine.dispose()` بعد الانتهاء لتحرير الموارد الأصلية.
- **التسجيل (Logging):** احفظ الناتج الخام في ملف سجل لتتبع التدقيق—خاصةً عندما تكون قد أوقفت تصحيح الإملاء.
- **الاختبار:** اكتب اختبار وحدة يمرر صورة معروفة ويتحقق من السلسلة الخام المتوقعة. يضمن ذلك أن تحديثات المكتبة المستقبلية لا تغير السلوك بصمت.

## الخلاصة

لقد أظهرنا لك كيفية **التعرف على النص من الصورة** باستخدام Aspose OCR للغة Java، وكيفية **تحميل صورة للتعرف الضوئي على الأحرف**، والخطوات الدقيقة **لإيقاف مصحح الإملاء** عندما تحتاج إلى الأحرف كما هي. الشيفرة القصيرة المستقلة أعلاه جاهزة للإدماج في أي مشروع Java، والشروحات توضح لك “السبب” وراء كل سطر.

بعد ذلك، قد ترغب في استكشاف **استخراج النص من الصورة** على نطاق واسع، تجربة تلميحات اللغة، أو دمج الناتج في فهرس بحث. مهما كان اختيارك، الأساسيات التي غطيناها هنا ستجعل خط أنابيب OCR الخاص بك موثوقًا وسهل الصيانة.

هل لديك تعديل أو تجربة تريد مشاركتها؟ لا تتردد بترك تعليق أو مشاركة **مثال Aspose OCR Java** الخاص بك. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
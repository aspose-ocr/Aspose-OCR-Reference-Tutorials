---
category: general
date: 2026-05-06
description: كيفية استخدام OCR لاستخراج النص من الصورة في جافا. تعلم تحويل الصورة
  إلى نص باستخدام OCR، وتصحيح أخطاء OCR، وتحميل الصورة لـ OCR باستخدام Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: ar
og_description: كيفية استخدام OCR في جافا لاستخراج النص من الصورة، وتصحيح أخطاء OCR،
  وتحميل الصورة للـ OCR باستخدام Aspose OCR.
og_title: كيفية استخدام OCR في جافا – دليل شامل
tags:
- OCR
- Java
- Aspose
title: كيفية استخدام OCR في جافا – استخراج النص من الصورة مع تصحيح الأخطاء الإملائية
url: /ar/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في Java – استخراج النص من الصورة مع تصحيح الإملاء

هل تساءلت يومًا **كيفية استخدام OCR** لتحويل صورة إيصال غير واضحة إلى نص نظيف وقابل للبحث؟ لست وحدك. في العديد من المشاريع—تطبيقات تتبع النفقات، خطوط تحويل الفواتير إلى رقمية، أو حتى سكريبت سريع لتدوين الملاحظات—الحصول على نص موثوق من صورة هو العائق الأول.  

هذا الدليل يوضح لك بالضبط كيفية استخدام OCR في Java، بدءًا من تحميل الصورة للـ OCR وحتى تصحيح أخطاء الـ OCR بحيث يبدو الناتج كما لو أنه مكتوب يدويًا. في النهاية، ستتمكن من **استخراج النص من الصورة**، إجراء تحويل **OCR من صورة إلى نص**، وإصلاح الأخطاء الشائعة تلقائيًا.

## ما ستقوم ببنائه

سننشئ برنامجًا صغيرًا في سطر الأوامر بلغة Java يقوم بـ:

1. تحميل ملف PNG (أو أي صيغة مدعومة) إلى محرك Aspose OCR.  
2. تفعيل ميزة تصحيح الإملاء المدمجة **لتصحيح أخطاء OCR**.  
3. تشغيل عملية التعرف وطباعة النص المنقح.  

بدون خدمات خارجية، بدون أطر عمل ثقيلة—فقط ملف JAR واحد وبعض الأسطر البرمجية.

### المتطلبات المسبقة

- مجموعة تطوير Java (JDK) 8 أو أحدث.  
- Maven (أو أي أداة بناء) لجلب مكتبة Aspose OCR.  
- ملف صورة (مثال: `receipt.png`) تريد تحليله.  

إذا كنت تفتقد ملف Aspose OCR JAR، أضف هذا الاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **نصيحة احترافية:** النسخة التجريبية المجانية تعمل للاختبار، لكن الترخيص يزيل علامة التقييم.

## الخطوة 1 – تهيئة محرك OCR (الكلمة المفتاحية الأساسية في التنفيذ)

أول شيء تحتاج إلى القيام به هو إنشاء مثيل من `OcrEngine`. فكر فيه كالعقل الذي سيقرأ البكسلات ويحولها إلى أحرف.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*لماذا هذا مهم:* تهيئة المحرك تُعد الموارد الداخلية (نماذج اللغة، القواميس، إلخ). تخطي هذه الخطوة سيتسبب في حدوث `NullPointerException` لاحقًا عندما تحاول تحميل صورة.

## الخطوة 2 – تحميل الصورة للـ OCR

الآن نقوم فعليًا **بتحميل الصورة للـ OCR**. توفر Aspose المساعد `ImageStream.fromFile` لسهولة الاستخدام، لكن يمكنك أيضًا تمرير `byte[]` إذا فضلت ذلك.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*خطأ شائع:* يجب أن يكون مسار الملف مطلقًا أو نسبيًا إلى دليل العمل. إذا لم يتم العثور على الصورة، سيُطلق المحرك استثناء `IOException`. تحقق من المسار، خاصةً عند التشغيل من بيئة تطوير متكاملة مقارنةً بملف JAR مُعبأ.

## الخطوة 3 – تفعيل تصحيح الإملاء **لتصحيح أخطاء OCR**

الـ OCR الجاهز قد يكون صاخبًا—مثل ظهور “l0ve” بدلًا من “love” أو “0” بدلًا من “O”. تفعيل تصحيح الإملاء يُخبر المحرك بتنفيذ مرحلة ما بعد المعالجة التي تُصلح الأخطاء النموذجية.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*لماذا قد تحتاج ذلك:* بدون تصحيح الإملاء، قد تضطر إلى تنظيف المخرجات يدويًا، مما يُفقدك هدف الأتمتة. القاموس المدمج يعمل جيدًا للإنجليزية وعدة لغات أخرى.

## الخطوة 4 – إجراء التعرف (**OCR من صورة إلى نص**)

مع تحميل الصورة وتفعيل تصحيح الإملاء، يمكننا الآن طلب من المحرك التعرف على النص.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*حالة حدية:* إذا كانت الصورة منخفضة التباين أو مائلة بشدة، قد يظل الناتج يحتوي على رموز غير مفهومة. فكر في معالجة مسبقة (مثل التحويل إلى ثنائي، تصحيح الميل) قبل تمريرها إلى المحرك.

## الخطوة 5 – إخراج النص المنقح

الخطوة الأخيرة هي ببساطة طباعة النتيجة. في تطبيق حقيقي قد تكتبها إلى قاعدة بيانات أو ملف، لكن لهذا العرض `System.out` كافية.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### النتيجة المتوقعة

بافتراض أن `receipt.png` يحتوي على قائمة واضحة من العناصر، قد ترى شيئًا مثل:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

لاحظ كيف تم كتابة “Qty” و “Price” بشكل صحيح حتى وإن كان المسح الأصلي يحتوي على “Qy” عشوائي.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في ملف باسم `SpellCorrectDemo.java`. تأكد من أن ملف Aspose OCR JAR موجود في مسار الـ classpath.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

شغّله باستخدام:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

يجب الآن أن ترى النص المنقح يُطبع في وحدة التحكم.

## مكافأة: تعديل الإعدادات للحصول على دقة أعلى

بينما يعمل الإعداد الافتراضي لمعظم المستندات المطبوعة، قد تحتاج إلى تعديل بعض المعاملات للسيناريوهات المتخصصة:

| الإعداد | ما يفعله | متى يجب تغييره |
|---------|----------|----------------|
| `setLanguage(OcrLanguage.English)` | يفرض القاموس الإنجليزي (يقلل الإيجابيات الزائفة) | إذا كانت الصورة تحتوي على نص إنجليزي فقط. |
| `setResolution(300)` | يُخبر المحرك بدقة DPI للصورة المصدر | للمسحات عالية الدقة. |
| `setEnableAutoSkewCorrection(true)` | يُصحح تلقائيًا الصفحات المائلة قليلًا | عندما تُلتقط الصور بهاتف. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات PDF؟**  
ج: نعم. حوّل كل صفحة PDF إلى صورة (مثلاً باستخدام Aspose PDF) ومرّر الصورة إلى محرك OCR.

**س: ماذا لو كانت صورتي بصيغة BMP؟**  
ج: `ImageStream.fromFile` يدعم PNG، JPEG، BMP، TIFF، و GIF مباشرة. فقط غيّر امتداد الملف.

**س: هل يمكنني إيقاف تصحيح الإملاء؟**  
ج: بالتأكيد—استخدم `setEnableSpellCorrection(false)` إذا كنت تحتاج مخرجات OCR خام للمعالجة اللاحقة.

## الخلاصة

أنت الآن تعرف **كيفية استخدام OCR** في Java لـ **استخراج النص من الصورة**، وتصحيح **أخطاء OCR** تلقائيًا، وتحميل **الصورة للـ OCR** باستخدام Aspose OCR. تدفق الخطوات الخمس—التهيئة، التحميل، تفعيل تصحيح الإملاء، التعرف، والإخراج—يغطي معظم مهام OCR اليومية.  

من هنا، يمكنك ربط هذه المنطق بكتابة إلى قاعدة بيانات، أو نقطة نهاية REST، أو معالج دفعات للتعامل مع عشرات الإيصالات دفعة واحدة. جرّب جدول الإعدادات الإضافية أعلاه لاستخراج أقصى دقة ممكنة.

برمجة سعيدة، ولتكن نتائج OCR دائمًا أنظف من إيصالاتك الملطخة بالقهوة! 

![مخطط كيفية استخدام OCR يُظهر الصورة → محرك OCR → النص المصحح]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-31
description: تعلم كيفية التعرف على النص داخل منطقة الاهتمام (ROI) باستخدام Aspose
  OCR للغة Java. يوضح لك هذا الدليل كيفية استخراج النص من منطقة أو صورة نموذج في بضع
  أسطر فقط.
draft: false
keywords:
- recognize text in ROI
- extract text from region
- extract text from form image
language: ar
og_description: التعرف على النص في منطقة الاهتمام باستخدام Aspose OCR للـ Java. اتبع
  هذا الدليل خطوة بخطوة لاستخراج النص من المنطقة أو صورة النموذج بسرعة.
og_title: التعرف على النص داخل منطقة الاهتمام باستخدام Aspose OCR – دليل جافا
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text in ROI using Aspose OCR for Java. This
    guide shows you how to extract text from region or form image in just a few lines.
  headline: recognize text in ROI with Aspose OCR – Java Tutorial
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image Processing
title: التعرف على النص في منطقة الاهتمام باستخدام Aspose OCR – دليل جافا
url: /ar/java/ocr-operations/recognize-text-in-roi-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص في منطقة الاهتمام باستخدام Aspose OCR – دليل Java

هل احتجت يومًا إلى **التعرف على النص في منطقة الاهتمام** لكنك لم تكن متأكدًا من كيفية عزل الجزء الذي يهمك فقط؟ لست وحدك. سواء كنت تستخرج حقل الاسم من نموذج ممسوح ضوئيًا أو تلتقط الرقم التسلسلي من ملصق، فإن تركيز OCR على منطقة محددة يوفر الوقت ويزيد الدقة.

في هذا الدليل سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح لك كيفية **استخراج النص من منطقة** وحتى **استخراج النص من صورة نموذج** باستخدام Aspose OCR للـ Java. في النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع، بالإضافة إلى مجموعة من النصائح للتعامل مع الحالات الخاصة.

---

## ما ستحتاجه

- **Java 17** أو أحدث (الكود يعمل مع أي JDK حديث)  
- مكتبة **Aspose OCR for Java** – يمكنك الحصول على أحدث JAR من مستودع Aspose Maven أو تنزيله مباشرة من موقع Aspose.  
- **ملف ترخيص** (`Aspose.OCR.Java.lic`). النسخة التجريبية المجانية تعمل جيدًا للاختبار، لكن الترخيص المناسب يزيل حدود التقييم.  
- صورة عينة (`form_with_fields.png`) تحتوي على نموذج به حقل “Name” أو أي منطقة تريد استهدافها.  

هذا كل ما تحتاجه—لا محركات OCR إضافية، لا تبعيات أصلية، فقط Java عادية وJAR واحد من طرف ثالث.

---

## الخطوة 1: تطبيق ترخيص Aspose OCR (التعرف على النص في ROI)

قبل أن يتمكن المحرك من معالجة أي شيء، يجب أن تخبر Aspose بأنه مرخص. تخطي هذه الخطوة سيجعل OCR يعمل في وضع العرض التجريبي، مما يحد من طول المخرجات ويضيف علامة مائية.

```java
import com.aspose.ocr.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
```

*لماذا هذا مهم:* الترخيص يفتح كامل محرك OCR، مما يسمح لك **بالتعرف على النص في ROI** دون حد 1 KB للمخرجات في النسخة التجريبية. إذا نسيت هذه السطر، سيستمر المحرك في العمل لكن ستحصل على نتائج مقطوعة—وهو ما يسبب إرباكًا للعديد من المبتدئين.

---

## الخطوة 2: إنشاء وتكوين محرك OCR

الآن نقوم بإنشاء نسخة من `OcrEngine`، نحدد اللغة، ونشير إلى ملف الصورة الذي يحتوي على النموذج.

```java
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(OcrLanguage.ENGLISH); // Adjust if you need another language
        OcrImage image = new OcrImage("YOUR_DIRECTORY/form_with_fields.png");
        engine.setImage(image);
```

*نصيحة احترافية:* إذا كان النموذج يحتوي على لغات متعددة (مثل الإنجليزية والإسبانية)، يمكنك تمرير قائمة مفصولة بفواصل مثل `OcrLanguage.ENGLISH, OcrLanguage.SPANISH`. سيقوم المحرك تلقائيًا بتبديل السياق حسب كل منطقة.

---

## الخطوة 3: تعريف المنطقة(ات) – استخراج النص من المنطقة

سحر ROI (منطقة الاهتمام) يكمن في فئة `OcrRegion`. تقوم بإخبار المحرك بالمستطيل الدقيق (x, y, العرض, الارتفاع) الذي يحيط بالحقل الذي يهمك.

```java
        // Define the region that contains the "Name" field (x, y, width, height)
        OcrRegion nameRegion = new OcrRegion(120, 350, 480, 80);
        engine.addRegion(nameRegion); // You can add more regions later
```

*لماذا نفعل ذلك:* من خلال تقييد OCR إلى **منطقة**، يتخطى المحرك بقية الصفحة، مما يقلل الضوضاء ويحسن السرعة بشكل كبير—خاصةً في النماذج الممسوحة الكبيرة. يمكنك إضافة عدد من المناطق حسب الحاجة؛ كل واحدة ستُعالج بشكل مستقل.

**تنوع شائع:** إذا لم تكن تعرف الإحداثيات الدقيقة، يمكنك استخدام محرر صور (مثل GIMP أو Paint.NET) لتتحرك فوق الحقل وتدوّن قيم البكسل، أو كتابة سكريبت صغير يقرأ أبعاد الصورة ويحسب الإزاحات بشكل ديناميكي.

---

## الخطوة 4: تشغيل OCR على ROI المحدد

مع وجود المنطقة، استدعاء `recognize()` يُشغِّل المحرك لمسح ذلك المستطيل فقط.

```java
        // Perform OCR only within the specified region(s)
        String extractedName = engine.recognize();
```

*حالة خاصة:* عندما تحتوي المنطقة على عدة أسطر (مثل كتلة العنوان)، تُعيد `recognize()` سلسلة واحدة مع فواصل أسطر (`\n`). يمكنك تقسيمها لاحقًا باستخدام `String.split("\n")` إذا كنت تحتاج كل سطر على حدة.

---

## الخطوة 5: إخراج النص المعترف به – استخراج النص من صورة النموذج

أخيرًا، نقوم بطباعة النتيجة. عملية القص (trim) تزيل أي مسافات زائدة قد يضيفها OCR في النهاية.

```java
        // Output the recognized text
        System.out.println("Extracted Name: " + extractedName.trim());
    }
}
```

تشغيل البرنامج يجب أن ينتج شيئًا مثل:

```
Extracted Name: John Doe
```

إذا كان الناتج فارغًا أو مشوّهًا، تحقق مرة أخرى من الإحداثيات، تأكد من أن الصورة عالية الدقة (300 dpi أو أعلى هو المثالي)، وتأكد من أن إعداد اللغة يطابق النص.

---

## إضافي: معالجة حقول متعددة في تمريرة واحدة

غالبًا ما يحتوي النموذج على أكثر من مجرد اسم—فكر في “Date”، “Address”، و“Signature”. يمكنك إضافة عدة كائنات `OcrRegion` قبل استدعاء `recognize()`. سيقوم المحرك بدمج النتائج بترتيب إضافة المناطق.

```java
        OcrRegion dateRegion = new OcrRegion(600, 350, 200, 80);
        engine.addRegion(dateRegion);

        OcrRegion addressRegion = new OcrRegion(120, 450, 680, 120);
        engine.addRegion(addressRegion);

        String allText = engine.recognize();
        System.out.println("All extracted fields:\n" + allText);
```

*لماذا هذا مفيد:* بدلاً من تشغيل مهام OCR منفصلة لكل حقل، تقوم بتجميعها في استدعاء واحد، مما يقلل من عبء الإدخال/الإخراج ويحافظ على تنظيم الكود.

---

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| **إخراج فارغ** | إحداثيات المنطقة لا تغطي النص فعليًا. | افتح الصورة في محرر، فعّل شبكة البكسل، وتحقق من المستطيل. |
| **حروف غير مفهومة** | صورة منخفضة الدقة أو ضبط لغة غير صحيح. | استخدم مسحًا بدقة 300 dpi واضبط `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)`. |
| **كلمات جزئية** | المنطقة تقص الأحرف عند الحواف. | أضف بضع بكسلات إضافية إلى العرض/الارتفاع لمنح OCR مساحة للتنفس. |
| **بطء الأداء** | معالجة الصورة بالكامل بدلاً من ROI. | أضف دائمًا على الأقل `OcrRegion` واحدة؛ يتخطى المحرك كل شيء آخر. |

---

## اختبار إعدادك – سكريبت التحقق السريع

إذا لم تكن متأكدًا من أن المكتبة مثبتة بشكل صحيح، شغّل هذا المقتطف البسيط قبل إضافة المناطق:

```java
OcrEngine testEngine = new OcrEngine();
testEngine.setImage(new OcrImage("sample.png"));
System.out.println(testEngine.recognize());
```

إذا رأيت بضع أسطر من النص من الصورة بالكامل، فإن المكتبة تعمل. ثم تابع إلى النسخة المركزة على ROI أعلاه.

---

## الخطوات التالية: ما بعد ROI البسيط

- **اكتشاف ROI ديناميكي:** استخدم معالجة الصور (مثل OpenCV) لتحديد الحقول تلقائيًا بناءً على الخطوط أو الصناديق.  
- **معالجة لاحقة:** تطبيق أنماط regex لتنظيف الأخطاء الشائعة في OCR (`0` مقابل `O`, `1` مقابل `l`).  
- **تصدير إلى JSON:** غلف كل حقل مستخرج في كائن JSON لتسهيل الاستهلاك لاحقًا.  

جميع هذه تبني على الأساس الذي تعلمته للتو—**التعرف على النص في ROI** باستخدام Aspose OCR.

---

## الخلاصة

أصبح لديك الآن مثال كامل جاهز للنسخ واللصق يوضح كيفية **التعرف على النص في ROI** باستخدام Aspose OCR للـ Java، وقد رأيت كيف **استخراج النص من منطقة** و**استخراج النص من صورة نموذج** بطريقة جاهزة للإنتاج. من خلال تضييق OCR إلى المنطقة الدقيقة التي تهمك، ستحصل على نتائج أسرع وأنظف وتتفادى الأخطاء الشائعة في التعرف على الصفحة بالكامل.

جرّبه مع نماذجك الخاصة، عدّل الإحداثيات، وسرعان ما ستقوم بأتمتة إدخال البيانات من المستندات الممسوحة كالمحترفين. هل لديك أسئلة أو نموذج صعب لا يتعاون؟ اترك تعليقًا أدناه—برمجة سعيدة!

![مثال Java OCR ROI – التعرف على النص في ROI](/images/ocr-roi-example.png){alt="التعرف على النص في ROI باستخدام Aspose OCR Java"}

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

- [كيفية التعرف على مستطيلات الصفحات لتعرف النص باستخدام OCR في Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [تحويل الصورة إلى نص – التعرف على النص من الصورة واسترجاع مستطيلات مناطق النص](/ocr/english/java/ocr-basics/get-rectangles-with-text-areas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}